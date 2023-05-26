# Transfer notifications

## General

![webooks](../images/webooks.png)

In order to react to payments coming to your [receive addresses](receive_addresses.md) you can setup income notifications. Every time income considered confirmed on the receive address Curra will send HTTP webhook request to your server.

What we offer:
1. Retries on failed requests. Every 10th minute
2. Webhook request on every confirmation transfer get. Up to 21 confirmations

## Setup
You can set your server url on <a href="https://app.curra.io/notifications" target="_blank">notifications page</a>:

![webhooks_setup](../images/webhooks_setup.png)

## Data

Webhook HTTP request Curra send you has content type is `application/json` and method `POST`.

### Coin transfer example

```json
{
  "id": 99, // transfer id, unique for each transfer
  "fromAddress": {
    "value": "0x67b1d87101671b127f5f8714789c7192f7ad340e",
    "owned": false
  },
  "toAddress": {
    "value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84", // your receive address
    "owned": true
  },
  "value": "1000000000000000000", // tx amount in raw format, 1000000000000000000 wei
  "valueDecimal": "1.000000000000000000", // tx amount in decimal format: 1 ETH
  "block": 171, // included in the block
  "txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46", // tx hash
  "txIndex": 0, // tx index within transaction
  "index": 0, // tx index within transaction
  "dropped": false, // tx has dropped from blockchain
  "confirmations": 1, // confirmations count
  "assetMetadata": { // some usefull information abount transfer asset
    "decimals": 18,
    "name": "ETHEREUM",
    "symbol": "ETH"
  },
  "failed": false // tx failed
}
```

### ERC20 transfer example

Same as coin, but includes `assetMetadata.address` which represents token contract address:

```json
{
  "id": 99, // transfer id, unique for each transfer
  "fromAddress": {
    "value": "0x67b1d87101671b127f5f8714789c7192f7ad340e",
    "owned": false
  },
  "toAddress": {
    "value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84", // your receive address
    "owned": true
  },
  "value": "1000000", // tx amount in raw format
  "valueDecimal": "1.000000", // tx amount in decimal format: 1 USDT
  "block": 171, // included in the block
  "txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46", // tx hash
  "txIndex": 0, // tx index within transaction
  "index": 0, // tx index within transaction
  "dropped": false, // tx has dropped from blockchain
  "confirmations": 1, // confirmations count
  "assetMetadata": { // some usefull information abount transfer asset
    "decimals": 6,
    "name": "Tether USD",
    "symbol": "USDT",
    "address": "0xdAC17F958D2ee523a2206206994597C13D831ec7" // contract address
  },
  "failed": false // tx failed
}
```