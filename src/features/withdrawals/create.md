# Create withdrawal

## SDK

```js
import { Blockchain } from "@curra/sdk";

const assetId =
    "you can use getAssets method or using GET /assets endpoint to retrive id of desired asset";
const value = "0.01";
const to = "0xe688b84b23f322a994A53dbF8E15FA82CDB71127"; // <-- example destination of payment

// estimate withdraw fee
const fee = await curra.estimateWithdrawal({
    assetId,
    blockchain: Blockchain.ETHEREUM,
    to,
    value,
});

const withdrawal = await curra.createWithdrawal({
    assetId,
    blockchain: Blockchain.ETHEREUM,
    to,
    value,
    feeData: fee.data
});
```

## HTTP

### Estimate
**path**: `/withdrawals/estimate`\
**method**: `POST`

Method reference <a href="https://api.curra.io/documentation/static/index.html#/default/post_withdrawals_estimate" target="_blank">here</a>

### Create
**path**: `/withdrawals`\
**method**: `POST`

Method reference <a href="https://api.curra.io/documentation/static/index.html#/default/post_withdrawals" target="_blank">here</a>


