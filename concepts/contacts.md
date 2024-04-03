---
description: SPV Wallet implementation of Contacts feature based on PIKE protocol. TODO - add BRC URL describing PIKE.
---

# 🤝 Contacts

## Table of Contents

- [🤝 Contacts](#-contacts)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Configuration](#configuration)
  - [Described flow](#described-flow)
  - [Contact states (statuses)](#contact-states-statuses)
  - [Features](#features)
    - [Adding contact](#adding-contact)
    - [Approving contact](#approving-contact)
    - [Rejecting contact](#rejecting-contact)

## Overview

// TODO 

Add a brief overview of the Contacts feature here. Paste some diagrams and flowcharts to help the reader understand the feature better.

## Configuration

Contacts feature is currently under development. That means that it is hidden behind a feature flag. To enable it in various components, you need to set...

// TODO - add configuration details

## Described flow

Describe the flow of the Contacts feature here. Use Alice and Bob as actors and describe how they interact with the SPV Wallet to add each other as contacts.

## Contact states (statuses)

List all possible states (statuses) of a contact in the SPV Wallet.

## Features

### Adding contact

Describe how to add a contact in the SPV Wallet. Discuss some edge cases like multpile contacts with the same paymail, etc.
How we deal with duplicates, list known errors.

### Approving contact

Same as above, but for approving a contact. Discuss some edge cases like approving a contact that is already approved, etc.

### Rejecting contact

Mention soft delete in this approach.
