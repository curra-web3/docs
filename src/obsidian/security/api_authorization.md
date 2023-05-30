# API authorization

## Non-custodial nature

Curra API is operated by the coordinator (trustless authority), which indexes various blockchains to obtain data related to Curra features. API is completely non-custodial and doesn't require your private keys to work, you can treat it as "read-only".

## Obtain API secret

To get the API secret you should complete onboarding on the Curra <a href="https://app.curra.io" target="_blank">application</a>.
After that, the secret can be obtained on the <a href="https://app.curra.io/configuration" target="_blank">configuration page</a>:


![get_api_secret](/obsidian/images/get_api_secret.png)

## Requests

To perform authorized requests, you can use JS/TS SDK or form HTTP requests by providing your ownership NFT ID and secret.

### JS/TS SDK

Blockchain values:

- `Blockchain.GOERLI` – Goerli blockchain
- `Blockchain.ETHEREUM` – Ethereum mainnet blockchain
- `Blockchain.BSC` – Binance Smart Chain blockchain
- `Blockchain.POLYGON` – Polygon blockchain

Install SDK:

```
npm i @curra/sdk
```

Create `Curra` instance:

```js
const { Blockchain, Curra } = require("@curra/sdk");

const curra = Curra.fromSecret({
  blockchain: Blockchain.ETHEREUM,
  secret: "YOUR_SECRET",
  ownershipId: "YOUR_OWNERSHIP_ID"
});
```

Now you can use the instance to perform requests, and create an address for example:

```js
const address = await curra.getNextAddress()
```

### HTTP

Construct blockchain-specific API URL. Replace `{blockchain}` with the desired blockchain:
`https://{blockchain}.coordinator.curra.io`

Blockchain URLs:

- Ethereum – `https://ethereum.coordinator.curra.io`
- Polygon – `https://polygon.coordinator.curra.io`
- Goerli – `https://goerli.coordinator.curra.io`
- Binance Smart Chain – `https://bsc.coordinator.curra.io`

Add the following headers to authorize your HTTP request:

- add `OWNERSHIP: your_ownership_nft_id` header
- add `SECRET: your_secret` header

HTTP request example to create an address on Ethereum blockchain:

```
POST /addresses/next
HOST: https://ethereum.coordinator.curra.io
SECRET: your_secret
OWNERSHIP: your_ownership_id
```

## Webhooks

In order to authorize Curra webhooks, like [transfer notifications](/obsidian/features/transfer_notifications.md), you can use JS/TS SDK or verify it manually.

### JS/TS SDK

Using a public key recovery (more secure way):

```js
// raw string body should be provided
const body = request.rawBody
const signature = request.headers.signature

// boolean here
const ok = await curra.verifyWebhookRequest(req.rawBody, req.headers.signature)
```

Using secret:

```js
const secret = request.headers.secret

const originalSecret = await curra.getSecret();
const ok = secret === originalSecret
```

### Manually authorize HTTP request

Here are two ways you can verify a webhook request:
1. Compare the `SECRET` header with your secret
2. Recover the public key from the `SIGNATURE` header using ECDSA recovery and compare it with API public key, which can be retrieved using `GET /pubkey` API endpoint


