---
description: Node.js Curra integration package
---

# JavaScript/TS SDK

## Overview

**Features:**

* New forwarder addresses allocation

**What happens under the hood:**

1. Communication with the [Network](broken-reference) Coordinator to inform keepers of new addresses allocated;
2. Synchronizing token configuration and addresses between Network and Connector.

To get a clear understanding of you can use SDK you can check out our **demo apps**:

* [Decentralized invoices](broken-reference)

## Getting started&#x20;

### Prerequisites&#x20;

To start using Curra SDK only one action required – create a wallet of supported blockchain to obtain a private key and provide it to your local SDK.&#x20;

{% hint style="info" %}
**Note:** All Curra layers are fully non-custodial (private keys stores on your side)\
Private key is required to sign nonce messages to the [Curra Network](broken-reference) coordinator only to identify your ownership, also you can check out the [GitHub repository](https://github.com/poloplayingsolo/curra-js-sdk) (SDK is completely open-source) to make sure that your key is in a safe.
{% endhint %}

Also, you may want to deploy the [Сonnector](broken-reference) of the corresponding blockchain and obtain its API URL to take advantage of the following features: notifications, transfers API, etc (learn more [here](broken-reference)).&#x20;

Currently, all examples are for [Goerli Ethereum testnet blockchain](https://goerli.net/). More blockchains will be available soon.

### Installation

```javascript
// NPM
npm i @curra/sdk
// Yarn
yarn add @curra/sdk
```

### Create instance

No connector (curra network only mode):

```javascript
const { Blockchain, Curra } = require("@curra/sdk");

const curra = new Curra(Blockchain.GOERLI, {
    privateKey: "YOUR_WALLET_PRIVATE_KEY_HERE"
});
```

With connector (curra network + connector):

<pre class="language-javascript"><code class="lang-javascript">const { Blockchain, Curra } = require("@curra/sdk");

<strong>const curra = new Curra(Blockchain.GOERLI, {
</strong><strong>    // we have deployed the connector on 8080 port locally 
</strong><strong>    connectorUrl: "localhost:8080",
</strong>    privateKey: "YOUR_WALLET_PRIVATE_KEY_HERE"
});
</code></pre>

### Get forwarder address

Allocate the next free address:

```javascript
const { Blockchain, Curra } = require("@curra/sdk");

const curra = new Curra(Blockchain.GOERLI, {...});
const address = await curra.getNextAddress()
```

Allocate/get the free address by index (salt):

```javascript
const { Blockchain, Curra } = require("@curra/sdk");

const curra = new Curra(Blockchain.GOERLI, {...});
const address = await curra.getAddress(0) // index of the address >0
```
