# Incoming payments

## Introduction

![webooks](/images/webooks.png)

Notification sent on each new incoming payment to a [receive address](/features/receive_addresses/index.md)

> 🔄 **Retries**
> 
> Curra will try to notify you 20 times every 10 minutes in case your server response status isn't 2xx

## Setup

You can set your server URL on the <a href="https://app.curra.io/notifications" target="_blank">notifications page</a> to start receiving incomes notifications:

![webhooks_setup](/images/webhooks_setup_incomes.png)

## Webhook payload

**method**: POST

**headers**:

-   content-type: application/json
-   x-api-key: your_api_key

**body**:

possible variants of `status`:

-   "pending" - on each `confirmations` field update
-   "success" – income considered successfull, assets received and confirmed on the address

**fields**:

\* - non-optional field

<table>
<thead>
<tr>
<th>Key</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>

<tr>
<td>id</td>
<td><i>string*</i></td>
<td>identifier of a payment</td>
</tr>
<tr>
<td>toAddress</td>
<td>
value: <i>string*</i><br/>
uniqueId: <i>string*</i><br/>
meta: <i>string</i><br/>
</td>
<td>
value – receive address<br/>
uniqueId - uniqueId provided on address creation, generated if not provided<br/>
meta – meta provided on address creation
</td>
</tr>

<tr>
<td>id</td>
<td><i>string*</i></td>
<td>identifier of a payment</td>
</tr>

<tr>
<td>fromAddress</td>
<td>
string*
</td>
<td>
sender address
</td>
</tr>

<tr>
<td>value</td>
<td>
string*
</td>
<td>
payment amount in units
</td>
</tr>

<tr>
<td>valueDecimal</td>
<td>
string*
</td>
<td>
payments amount in decimal format
</td>
</tr>

<tr>
<td>blockchain</td>
<td>
string*
</td>
<td>
available values at "API value" column <a href="/introduction/availability.html" target="_blank">here</td>
</tr>

<tr>
<td>fromAddress</td>
<td>
string*
</td>
<td>
sender address
</td>
</tr>

<tr>
<td>block</td>
<td>
number*
</td>
<td>
block number in which payment was mined
</td>
</tr>

<tr>
<td>txHash</td>
<td>
string*
</td>
<td>
trasaction hash
</td>
</tr>

<tr>
<td>confirmations</td>
<td>
number*
</td>
<td>
blockchain confirmations count
</td>
</tr>

<tr>
<td>assetId</td>
<td>
string*
</td>
<td>
asset id of a payment 
</td>
</tr>

<tr>
<td>status</td>
<td>
string*<br/>"pending" or "success"
</td>
<td>
pending – payment is not confirmed yet <br/>
success - payment confirmed on the address
</td>
</tr>

<tr>
<td>subStatus</td>
<td>
string*
</td>
<td>
blockchain-specific status, can be used in informational purposes  
</td>
</tr>

<tr>
<td>statusDescription</td>
<td>
string*
</td>
<td>
human-readable description of status field
</td>
</tr>
</tbody>
</table>

**example of pending payment**:

```json
{
	"id": 99,
	"toAddress": {
		"value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84",
		"uniqueId": "unique id you specified when address was created",
		"meta": "meta you specified when address was created"
	},
	"value": "1000000000000000000",
	"valueDecimal": "1.0",
	"blockchain": "ETHEREUM",
	"fromAddress": "0x67b1d87101671b127f5f8714789c7192f7ad340e",
	"block": 171,
	"txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46",
	"confirmations": 10,
	"assetId": "asset-id-123-123",
	"status": "pending",
	"subStatus": "pending",
	"statusDescription": "Waiting for confirmations"
}
```

**example of success payment**:

```json
{
	"id": 99,
	"toAddress": {
		"value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84",
		"uniqueId": "unique id you specified when address was created",
		"meta": "meta you specified when address was created"
	},
	"value": "1000000000000000000",
	"valueDecimal": "1.0",
	"blockchain": "ETHEREUM",
	"fromAddress": "0x67b1d87101671b127f5f8714789c7192f7ad340e",
	"block": 171,
	"txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46",
	"confirmations": 21,
	"assetId": "asset-id-123-123",
	"status": "success",
	"subStatus": "deposited",
	"statusDescription": "Deposited"
}
```
