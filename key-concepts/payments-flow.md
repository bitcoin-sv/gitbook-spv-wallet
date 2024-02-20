---
description: Paymail Capability Extensions
---

# 💵 Payments Flow

The SPV Wallet uses Paymail capabilities to publicly reveal their ability to interpret SPV transaction data.

{% hint style="info" %}
### What is Paymail?

It's a service discovery mechanism for counterparty web APIs. It allows users to pay something which looks like an email address, but under the hood resolves a specific endpoint for a wallet to use for payment negotiation.\
\
<mark style="color:yellow;">**user@domain.tld**</mark> -> _<mark style="color:blue;">https://domain.tld/api/some/specific/endpoint</mark>_
{% endhint %}

### Sequence Diagram

<div data-full-width="true">

<figure><img src="../.gitbook/assets/cae55929eb3dc7aee3651b63bf8a0b76.png" alt=""><figcaption></figcaption></figure>

</div>

### Capability Specifications

Further details on exactly how these requests and responses should be formulate are defined in these BRC documents:

{% embed url="https://bsv.brc.dev/payments/0028" %}
Getting Outputs to Pay To
{% endembed %}

{% embed url="https://bsv.brc.dev/payments/0070" %}
The Paymail Capability for Delivering SPV Transactions
{% endembed %}
