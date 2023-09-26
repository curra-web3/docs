# Forwarding payments

## Introduction

![webooks](/obsidian/images/forwarding_notifications.png)

Notification sent when balance of a [receive address](/obsidian/features/receive_addresses/index.md) is forwarded to a configured wallet

## Setup

You can set your server URL on the <a href="https://app.curra.io/notifications" target="_blank">notifications page</a> to start receiving incomes notifications:

![webhooks_setup](/obsidian/images/webhooks_setup_forwarding.png)

## Webhook payload

**method**: POST

**headers**:

- content-type: application/json

**body**:

possible variants of `status` field:

- `"success"` – income considered successfull, assets are confirmed on the receive address

possible variants of `subStatus` field:

- `"forwarded"` – assets are forwarded to your wallet from receive address

```json
{
	"id": 99, // transfer id, unique for each transfer
	"toAddress": {
		"value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84", // your receive address
		"uniqueId": "unique id you specified when address was created", // optional
		"meta": "meta you specified when address was created" // optional
	},
	"value": "1000000000000000000", // tx amount in raw format, 1000000000000000000 wei
	"valueDecimal": "1.0", // tx amount in decimal format: 1 ETH
	"blockchain": "ETHEREUM",
	"fromAddress": "0x67b1d87101671b127f5f8714789c7192f7ad340e", // sender address
	"block": 171, // included in the block
	"txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46", // tx hash
	"confirmations": 1, // confirmations count of income
	"assetId": "asset-id-123-123", // to get additional information about asset look at GET /assets/:id on API reference
	"status": "success", // status of the income, use this field to determine status of the income
	"subStatus": "forwarded",
	"statusDescription": "Waiting for confirmations" // status human-readable description
}
```
