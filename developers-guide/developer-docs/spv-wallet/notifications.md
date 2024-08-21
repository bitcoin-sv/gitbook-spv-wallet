# Notifications

## Overview

The notifications system has the following features:

- allows clients to subscribe and unsubscribe their webhook URLs
- subscriptions are persisted in the database, so clients do not need to re-subscribe after an spv-wallet restart.
- all instances of spv-wallet observe the status of currently-registered webhooks
- each client has its own queue (golang's buffered channel) so a malfunctioning client does not block other clients
- retries and timed bans on failure are implemented
- a webhook call includes a list of events
- 'Notifications Listener' is implemented in `go-client` so it's ready to use, without detailed knowledge about webhooks.
  - It handles subscription and unsubscription,
  - you only need to register a handler for a specific event type
  - Check out the [example](https://github.com/bitcoin-sv/spv-wallet-go-client/blob/main/examples/webhooks/webhooks.go)

## Event types

Currently implemented event types are defined here: [spv-wallet: models/notifications.go](https://github.com/bitcoin-sv/spv-wallet/blob/main/models/notifications.go)

#### TransactionEvent is sent when transaction is made or its status changes (e.g. from "unconfirmed" to "mined")

```go
// UserEvent - event with user identifier
type UserEvent struct {
	XPubID string `json:"xpubId"`
}

// TransactionEvent - event for transaction changes
type TransactionEvent struct {
	UserEvent `json:",inline"`

	TransactionID   string           `json:"transactionId"`
	Status          string           `json:"status"`
	XpubOutputValue map[string]int64 `json:"xpubOutputValue"`
}
```

The `XpubOutputValue` maps xpub ids to actual satoshi values.
**It's crucial to note that these values can be either positive or negative.**
Based on that you can determine if this is `outgoing (negative)` or `incomming (positive)` transaction from the particual `xpubID` perspective.

## Subscribing to Webhooks

To receive HTTP-based notifications on a specified URL, clients need to make a **POST** request to `<spv-wallet-url>/v1/admin/webhooks/subscriptions` with `admin-key` [authentication](./authentication.md#authenticate-with-admin-xpub) and with json body defined as:

```json
{
  "url": "http://your-webhook-url.com",
  "tokenHeader": "Authorization",
  "tokenValue": "Bearer your-token"
}
```

where only the `url` is required.

The client must run an HTTP server that listens on the specified URL to receive events from the spv-wallet.

Additional security layer to make sure that only the spv-wallet instance can send notifications is based on `tokenHeader` and `tokenValue`.
If these are defined, for each request, spv-wallet will include such header (`<tokenHeader>: <tokenValue>`) and the client should check if it equals to what was defined during the subscription process.

## Unsubscribing from Webhooks

Subscriptions are stored in the spv-wallet's database and persist until the client unsubscribes.

To unsubscribe, the client should call `<spv-wallet-url>/v1/admin/webhooks/subscriptions` (the same endpoint as for subscription) but using **DELETE** HTTP method and with json body with only one field - `url`. Similarly to subscribe the `admin-key` [authentication](./authentication.md#authenticate-with-admin-xpub) is required.

## Request with the list of events from spv-wallet to defined webhook

The spv-wallet will send a POST request containing a list of events to the defined webhook URL as soon as possible.
While processing events, if new events arrive in the input channel before the current batch is dispatched, these new events are accumulated and included in the next webhook call.
To prevent excessively large payloads, the maximum number of events included in a single webhook call is capped at `100`.
The webhook request always contains an array of events in its JSON payload. In scenarios with low event frequency, this array might often contain only a single event.

The json body of the request with events will look like this:

```json
[
  {
    "type": "TransactionEvent",
    "content": {
      "xpubId": "some-xpub-id",
      "transactionId": "some-transaction-id",
      "status": "MINED",
      "xpubOutputValue": { "xpub-id-1": 1000, "xpub-id-2": -1000 }
    }
  },
  {
    // possible other event of the same or different type
  }
  // ...
]
```

The `type` aka event name is automatically generated based on the name of the struct using the `reflect` package, like this:

```go
reflect.TypeOf(instance).Elem().Name()
```

## Webhook client implementation in go-client

There is no need for potential clients to implement those webhook logic and endpoint events listeners on their own.
A 'Notifications Listener' is included as part of the [go-client](https://github.com/bitcoin-sv/spv-wallet-go-client) to simplify webhook integration.

- check out the [example](https://github.com/bitcoin-sv/spv-wallet-go-client/blob/main/examples/webhooks/webhooks.go) how to configure it to receive notifications about transactions.

The parameters required to start the "Notification Listener" are:

- admin key (the `xpub` part corresponding to the `xpriv` defined in `spv-wallet` configuration)
- spv-wallet `url` to allow the client to call subscribe and unsubscribe requests
- full URL of the endpoint on which the client wants to listen for new events

To register a handler for a specific event type, the client should call `RegisterHandler` method with the handler function with propper event type, like this:

```go
if err = notifications.RegisterHandler(wh, func(gpe *models.TransactionEvent) {
	fmt.Printf("XPubID: %s, TxID: %s, Status: %s\n", gpe.XPubID, gpe.TransactionID, gpe.Status)
}); err != nil {
	// handle an error - could not register handler
}

```

- The `wh` is an instance of webhook client and the `gpe` is the event instance.
- Interesting fact is that the `RegisterHandler` function will detect what type of event is passed to the handler function and will call it only if the event type matches the handler type.
- Even though, the events are transported in groups (array of events), the handler function will be called for each event separately.

## What's under the hood?

![spv-wallet: services/notifications.go](/.gitbook/assets/notifications.png)

The implementation is based on `goroutines` which are communicating via channels ensuring concurrent and efficient handling of events.

There are three main components:

- notification-service
- webhook-manager
- webhook-notifier

Channels of type `(chan *models.RawEvent)` can be added to the notification-service. The service will send new events to all registered channels. This approach allows for future extensibility, such as adding support for WebSockets, gRPC, and other communication methods.

When the client calls `subscribe/unsubscribe` endpoint with `url` provided, the state of db webhooks table is updated and then the webhook-manager updates instances of `webhook-notifier`s.

During synchronisation to the new state of webhooks, the manager can:

- add a new webhook record and start new webhook-notifier
- update existing record & notifier if the url already exists but auth params changes
- remove the db record and stop corresponsing webhook-notifier if a client calls `unsubscribe`

The manager also have a goroutine which periodically observes the `notifications` table and, based on that, updates the webhook-notifiers. It is necessary, because, there can be multiple instances of spv-wallet, and the subscription request, handled by one instance has to be applied to all of those instacnes.

The `webhook-notifier` has its own buffered channel and a separate goroutine responsible for getting pending events, group them and send via HTTP. Also the retries and ban logic is here.
