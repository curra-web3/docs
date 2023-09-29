# Notifications

Notification sent on each status update of withdrawal

> 🔄 **Retries**
>
> Curra will try to notify you 10 times in case your server response status isn't 2xx

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
<td>userId</td>
<td>
string*
</td>
<td>
id of Curra user
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
    "confirmations": 1,
    "txHash": "0xb375384a94d17ae8f47546e5285eac3a53ae6b175227411de0417451b3f29717",
    "blockchain": "ETHEREUM",
    "userId": "6516ee52f1e77dee6e93bcd9",
    "id": "6516ee57330333208c3401ea",
    "assetId": "6516ee52330333208c34018a",
    "fromAddresses": ["0x5D871c6227290C63Fc4881a80c903dF8518116F8"],
    "toAddress": "0x5D871c6227290C63Fc4881a80c903dF8518116F8",
    "block": 340,
    "value": "0.01",
    "valueUnits": "10000000000000000",
    "rawUnsigned": [
        {
            "value": "7cd909cbd6b9043938f41c96e6a158ea6b75e69ea201ee4448b98ef120262821",
            "path": "m/44'/60'/0'/0/0"
        },
        {
            "value": "51286facfed4cf6e9fa112cee7858846d31ffdf6784aaf0de44424a96eb09ab6",
            "path": "m/44'/60'/0'/0/0"
        },
        {
            "value": "33dcaecef5c1271e7462bc5fe38c38546e9325ab77ad44a59144eea38dc1ab08",
            "path": "m/44'/60'/0'/0/0"
        },
        {
            "value": "9e3fb550eae0781c4641ddb5be8270853225758dbe3045e6e9fa681de7259241",
            "path": "m/44'/60'/0'/0/0"
        }
    ],
    "rawSigned": [
        "0x02f87382053980843b9aca00843b9aca10825208945d871c6227290c63fc4881a80c903df8518116f8872386f26fc1000080c001a076c9188df0e9834f91be3911bee5d020865f0ea07aea1db90a83801ea16d3100a01da9ffb5ba10c142ef211947c6ae84bb33b9f2ecc3250079a55fc0448fa3e587",
        "0x02f87382053980843b9aca008459682f18825208945d871c6227290c63fc4881a80c903df8518116f8872386f26fc1000080c080a08549b3c8ec6d7dd954f514f37ec3e35b231bbd16e0c397d376ebcf2cae3bc7b8a061f92d4963ecc970c382849949caebb845e93e7b49d3bb0154c706f767c861d5",
        "0x02f87382053980843b9aca008477359420825208945d871c6227290c63fc4881a80c903df8518116f8872386f26fc1000080c080a02cb5f67f1da22a224d8176b87f7d4b9b1cf6e867583e3159eee825f75f54e190a05bf65f899ff230837d830d2dab0c3cf4713cd88b3b3a0be0e87b0615da4c9a4c",
        "0x02f86c82053980843b9aca00849502f928825208945d871c6227290c63fc4881a80c903df8518116f88080c001a02ba4ea374c040a33e3d503833d06f0845062176794d2ff4879f9364982f22c76a031623c68b108de7162ae6eb2a219da2080b8b88af5e8d2e85002845e012fa552"
    ],
    "fee": {
        "assetId": "6516ee52330333208c34018a",
        "value": "0.000021",
        "valueUnits": "21000000000000",
        "data": {
            "gasLimit": "21000",
            "maxFeePerGas": "1000000016",
            "maxPriorityFeePerGas": "1000000000"
        }
    },
    "status": "confirmed"
}
```
