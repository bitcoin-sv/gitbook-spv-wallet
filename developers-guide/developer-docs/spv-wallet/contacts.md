# Contacts

## Configuration

Contacts feature is currently under development. That means that it is hidden behind a feature flag. To enable it in various components, you need to set 

```json
{
    "experimental_features":{
        "pike_enabled": true
    }
}
```

## Contact states (statuses)

* *unconfirmed* - new added contact or accepted contact request
* *confirmed* - contact that has been confirmed
* *awaiting* - contact waiting for acceptance added via PIKE capability
* *rejected* - rejected contact request added via PIKE capability

## Features

### Upserting contact

SPV Wallet issues the endpoint `PUT /contact/{paymail}` to upsert contacts which handles payload:
```go
type UpsertContact struct {
	// The complete name of the contact, including first name, middle name (if applicable), and last name.
	FullName string `json:"fullName" binding:"required"`
	// Accepts a JSON object for embedding custom metadata, enabling arbitrary additional information to be associated with the resource
	Metadata engine.Metadata `json:"metadata" swaggertype:"object,string" example:"key:value,key2:value2"`
	// Optional paymail address owned by the user to bind the contact to. It is required in case if user has multiple paymail addresses
	RequesterPaymail string `json:"requesterPaymail"`
}
```

New contact is stored with status *unconfirmed*. 

>NOTICE: `RequesterPaymail` in pyaload is respected and required only if user has multiple paymail addresses binded to its `XPub`.

If contact's wallet has PIKE capability request to add user paymail as contact is sent.

### Confirming contact

SPV Wallet issues the endpoint `PATCH /contact/confirmed/{paymail}` to mark contact as confirmed.

>NOTICE: only contacts in *unconfirmed* status can be accepted.

Server responses with statuses:

| HTTP Code | Description |
|-----------|-------------|
| 200 | success |
| 422 | contact has other status then *unconfirmed* |
| 404 | contact doesn't exist |

### Adding contact request (PIKE)

SPV Wallet handles PIKE Add Contact Request functionality. If contact doesn't exist it's saved with *awaiting* status. If already exists and contat PKI has changed since creation and is confirmed already its status shifts to *unconfirmed*.

>NOTICE: no additional contact information, besides public key and status, can be overwritten using this functionality.

### Accepting contact request

SPV Wallet issues the endpoint `PATCH /contact/accepted/{paymail}` to accept contact request and mark contact as *unconfirmed*.

>NOTICE: only contacts in *awaiting* status can be accepted.

Server responses with statuses:

| HTTP Code | Description |
|-----------|-------------|
| 200 | success |
| 422 | contact has other status then *awaiting* |
| 404 | contact doesn't exist |

### Rejecting contact request

SPV Wallet issues the endpoint `PATCH /contact/rejected/{paymail}` to reject contact request. SPV Wallet deletes contacts on rejection but due to using soft delete the record has additionaly status set to *rejected*.

>NOTICE: only contacts in *awaiting* status can be rejected.

Server responses with statuses:

| HTTP Code | Description |
|-----------|-------------|
| 200 | success |
| 422 | contact has other status then *awaiting* |
| 404 | contact doesn't exist |
