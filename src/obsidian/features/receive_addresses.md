# Receive addresses

## Introduction

![receive address example](/obsidian/images/receive_address_example.png)

If you operate a retail-oriented crypto business such as an exchange, lending desk, or neobank, you probably receive a significant number of ERC20/ deposits on a daily basis. To effectively handle and track these deposits, it is necessary to assign a new address to each client. Received  funds are automatically forwarded to your configured address

> 📖 **Notes on addresses**
> 
> Every address is assigned a unique index that can be considered as its identifier. These addresses are deterministically generated using these indexes and remain the same across different EVM chains. This means you can utilize the same addresses across multiple EVM blockchains that are supported.


## Quick start

Before you can create addresses, you should [authorize](/obsidian/security/api_authorization.md) your server.

### JS/TS SDK

Create a new receive address:

```js
const address = await curra.getNextAddress()
```

Create a new receive address by its index:

```js
const address = await curra.getAddress(6)
```

### HTTP

**Create new address**:

method: `POST`\
endpoint: `/forwarders/next`\
body: `{}`

**Create or get address by index (salt):**

method: `POST`\
endpoint: `/forwarders`\
body: `{ salt: number }`. *example:* `{ salt: 6 }`
