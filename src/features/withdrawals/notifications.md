# Notifications

Notification sent on each status update of withdrawal

> 🔄 **Retries**
>
> Curra will try to notify you 20 times every 10 minutes in case your server response status isn't 2xx

## Setup

You can set your server URL on the <a href="https://app.curra.io/notifications" target="_blank">notifications page</a> to start receiving withdrawal status update notifications

![webhooks_setup](/images/webhooks_setup_withdrawals.png)

## Webhook payload

**method**: POST

**headers**:

-   content-type: application/json

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
<td>unique identifier</td>
</tr>
<tr>

<td>toAddress</td>
<td>
string*
</td>
<td>
recipient address
</td>
</tr>

<tr>
<td>valueUnits</td>
<td>
string*
</td>
<td>
payment amount in units
</td>
</tr>

<tr>
<td>value</td>
<td>
string*
</td>
<td>
payment amount in decimal format
</td>
</tr>

<tr>
<td>blockchain</td>
<td>
string*
</td>
<td>
available values at "API value" column <a href="/introduction/availability.html">here<a/>
</td>
</tr>

<tr>
<td>block</td>
<td>
number
</td>
<td>
block number in which payment was mined
</td>
</tr>

<tr>
<td>from</td>
<td>
string*[]
</td>
<td>
sender addresses
</td>
</tr>

<tr>
<td>txHash</td>
<td>
string
</td>
<td>
trasaction hash, appears after payment is signed and broadcasted, can change in case if payment stuck
</td>
</tr>

<tr>
<td>confirmations</td>
<td>
number
</td>
<td>
blockchain confirmations count, appears after payment is signed and broadcasted
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
<td>fee</td>
<td>
{ assetId: string*, data: object*, value: string* }
</td>
<td>
assetId – asset in which fee for payment is payed<br/>
data – blockchain specific fee data<br/>
value – fee amount in decimal format
</td>
</tr>

<tr>
<td>rawUnsigned</td>
<td>
string*[]<br/>{ path: string*, value: string* }
</td>
<td>
unsigned transactions list, learn more <a href="/features/withdrawals/sign.html" target="_blank">here</a>
</td>
</tr>

<tr>
<td>rawSigned</td>
<td>
string[]
</td>
<td>
signed transactions list
</td>
</tr>

<tr>
<td>status</td>
<td>
string*<br/>
"waiting-for-signature" or
"insufficient-funds" or
"pending" or
"failed" or
"dropped" or
"stuck" or
"confirmed" or
"canceled" or
"signed" or
</td>
<td>
<b>"waiting-for-signature"</b> waiting to be signed<br/>
<b>"insufficient-funds"</b> – not enough funds to pay for withdrawal, will be sent as soon as funds will be available<br/>
<b>"pending"</b> – brodcasted, waiting for confirmations<br/>
<b>"failed"</b> – payment failed, retry attempt will be performed automatically<br/>
<b>"dropped"</b> - payment is dropped, retry attempt will be performed automatically<br/>
<b>"stuck"</b> – payment stuck, will be unstucked automatically<br/>
<b>"confirmed"</b> payment confirmed on the blockchain<br/>
<b>"canceled"</b> payment cancelled<br/>
<b>"signed"</b> payment signed and ready to be broadcasted<br/>
</td>
</tr>

</tbody>
</table>

**example**:

```json
{
    "id": 99,
    "toAddress": {
        "value": "0xf51eb0786cbdb8eb6e8175f0f32ecf90b04ceb84",
        "uniqueId": "unique id you specified when address was created or default one",
        "meta": "meta you specified when address was created"
    },
    "value": "1.0",
    "valueUnits": "1000000000000000000",
    "blockchain": "ETHEREUM",
    "fromAddresses": ["0x67b1d87101671b127f5f8714789c7192f7ad340e"],
    "block": 171,
    "txHash": "0x0b15d671d9fe9cfe110c2d3a03867cc0525f6aeee45fe21ff66d07e0fd38ef46",
    "confirmations": 21,
    "assetId": "asset-id-123-123",
    "status": "success",
    "subStatus": "forwarded",
    "statusDescription": "Waiting for confirmations"
}
```
