# Incoming payments

## Introduction

![webooks](/obsidian/images/webooks.png)

Notification sent on each new incoming payment to a [receive address](/obsidian/features/receive_addresses/index.md)

## Setup

You can set your server URL on the <a href="https://app.curra.io/notifications" target="_blank">notifications page</a> to start receiving incomes notifications:

![webhooks_setup](/obsidian/images/webhooks_setup_incomes.png)

## Webhook payload

**method**: POST

**headers**:

- content-type: application/json
- x-api-key: your_api_key

**body**:

possible variants of `status`:

- "pending" - on each `confirmations` field update
- "success" – income considered successfull, assets received and confirmed on the address

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
	"status": "pending", // status of the income, use this field to determine status of the income
	"subStatus": "pending", 
	"statusDescription": "Waiting for confirmations", // status human-readable description
}
```
