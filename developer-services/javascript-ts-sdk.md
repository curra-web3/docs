---
description: JS/TS integration package
---

# JS/TS SDK

## Overview

**Features:**

* New forwarder addresses allocation

## Getting started

### Prerequisites

Before using Curra SDK next actions should be performed:

1. Create a wallet of supported blockchain to obtain a private key and provide it to SDK, or if you use other signing method, you can provide [ethers.Signer](https://docs.ethers.org/v5/api/signer/).
2. [Obtain Ownership NFT](developer-services/accept-crypto-payments/1-obtain-ownership-nft.md)

{% hint style="info" %}
**Note:** All Curra layers are completely non-custodial (private keys stores on your side)\
Private key is required to sign nonce messages to the Curra Protocol coordinator only to identify your ownership, also you can check out the [GitHub repository](https://github.com/curraprotocol/js-sdk) (SDK is completely open-source) to make sure that your key is in a safe.
{% endhint %}

Currently, all examples are for [Goerli Ethereum testnet blockchain](https://goerli.net/). More blockchains will be available soon.

### Installation

```javascript
// NPM
npm i @curra/sdk
// Yarn
yarn add @curra/sdk
```

### Create instance

From private key:

```javascript
const { Blockchain, CurraCoordinator } = require("@curra/sdk");

const curra = CurraCoordinator.fromPrivateKey({
  blockchain: Blockchain.GOERLI,
  privateKey: "YOUR_WALLET_PRIVATE_KEY_HERE",
  ownershipId: "YOUR_OWNERSHIP_ID"
});
```

From signer:

```javascript
const { Blockchain, CurraCoordinator} = require("@curra/sdk");
const { Signer } = require("ethers");

const curra = CurraCoordinator.fromSigner({
  blockchain: Blockchain.GOERLI,
  signer: new Signer(/* your signer implementation */),
  ownershipId: "YOUR_OWNERSHIP_ID"
});
```

### Get forwarder address

Allocate the next free address:

```javascript
const address = await curra.getNextAddress()
```

Allocate/get the free address by index (salt):

```javascript
const address = await curra.getAddress(0) // index of the address >0
```
