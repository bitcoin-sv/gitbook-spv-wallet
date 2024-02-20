---
description: Wraps the core functionality together.
---

# 🌐 SPV Wallet Server

This component does the heavy lifting. It exposes the secure Client API, and public [Paymail](../resources/paymail.md) Endpoints; runs [SPV](../key-concepts/spv-definition.md) on inbound transactions; stores transactions and metadata; and broadcasts valid transactions, exposing a callback for Merkle paths.

There are a lot of endpoints - so we've detailed them in a resource page of their own.

{% content-ref url="../resources/endpoints.md" %}
[endpoints.md](../resources/endpoints.md)
{% endcontent-ref %}

At a high level there are admin functionalities exposed like creating a new alias, adding a new xpub, deleting things.&#x20;

The client functionality is more about drafting new transactions, modifying them, signing an actioning them in terms of sending to counterparty hosts, generating new locking scripts.

The public facing endpoints are all associated with Paymail service discovery and capabilities, which are detailed in [Payments Flow](../key-concepts/payments-flow.md).
