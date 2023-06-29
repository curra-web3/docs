# API

## Prerequisites

To perform authorized requests, you can use JS/TS SDK or form HTTP requests by providing your [Ownership NFT ID](/obsidian/security/ownership_nft.md) and the [secret](/obsidian/security/authorization/index.md).

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

