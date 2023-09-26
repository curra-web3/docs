# API

## Prerequisites

To perform authorized requests, you can use JS/TS SDK or form HTTP requests by providing your [API key](/obsidian/security/authorization/index.md)

### JS/TS SDK

Install SDK:

```
npm i @curra/sdk
```

Create `Curra` instance:

```js
const { Blockchain, Curra } = require("@curra/sdk");

const curra = Curra.fromApiKey({
  apiKey: "paste your API key here",
});
```

Now you can use the instance to perform requests, and create an address for example:

```js
const address = await curra.getNextAddress();
```

### HTTP

API URL is [https://api.curra.io](https://api.curra.io)

Set `X-API-KEY` header to your API key to authorize your HTTP request

HTTP request example to create an address on Ethereum blockchain:

```
GET /me
HOST: api.curra.io
X-API-KEY: your_api_key
```
