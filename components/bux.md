---
description: Suite of tools used to create a non-custodial hosted wallet.
---

# 🏷 Bux

### Wallet App & API

The frontend web wallet application allows users to register, make transactions, and see their balance. This is what we'd expect you to replace with your own application front end, but is included in the deployment to provide a working demo for basic payment functionality.

The backend API is coupled with the web wallet, and demonstrates use of the Wallet Client library.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### SPV Wallet Server

This component does the heavy lifting. It exposes the secure Client API, and public Paymail Endpoints; runs SPV on inbound transactions; stores transactions and metadata; and broadcasts valid transactions, exposing a callback for Merkle paths.

{% content-ref url="../resources/bux-server-endpoints.md" %}
[bux-server-endpoints.md](../resources/bux-server-endpoints.md)
{% endcontent-ref %}

### Database

A Postgres DB used to store user accounts, transactions, utxos, public keys, accounts, and metadata.

### Cache

The cache is used for handling spikes in usage of the application. The idea being all requests can be queued and responses made on a FIFO basis.

### Admin Console

This is a window into the data stored by the SPV Wallet server which allows inspection of all stored data and metadata. It allows manual creation of destinations, addition of user accounts, and transactions. Helpful if you're ever trying to troubleshoot.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Admin Console</p></figcaption></figure>

{% content-ref url="pulse.md" %}
[pulse.md](pulse.md)
{% endcontent-ref %}
