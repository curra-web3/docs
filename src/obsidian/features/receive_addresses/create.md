# Create new addresses

## Intro

To start accepting payments you can allocate unique addresses.

> 📖 **Notes on addresses**
>
> Every address is generated from unique salt (can be considered an unique identifier) and addresses remain the same across different EVM chains if their salts are equal. This means you can utilize the same addresses across multiple EVM blockchains that are supported.

## SDK

```js
import { Blockchain } from "@curra/sdk";

// just new addresses
// NOTICE: returns two identical addresses created in two different EVM blockchains
const addresses = await curra.createAddresses({
	blockchains: [Blockchain.ETHEREUM, Blockchain.SMART_CHAIN],
});

// new address with additional fields
const [address] = await curra.createAddresses({
	blockchains: [Blockchain.ETHEREUM],
	uniqueId: "I'm unique", // optional unique id
	meta: "my user id?", // custom data can be linked to the address, will be included in  incomes webhooks
});
```

## HTTP

**path**: `/addresses`\
**method**: `POST`

Method reference <a href="https://api.curra.io/documentation/static/index.html#/default/post_addresses" target="_blank">here</a>
