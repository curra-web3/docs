# Allocate time-limited address 🔜

## Intro

![time limited address](/images/temporary_addresses.png)

Use this method to allocate a time-limited address. You can specify time to reserve an address for an operation, once time elapsed – address is ready for a new reservation

> 💸 **Why?**
>
> As you noticed in [gas pump costs](/costs/gas_pump.md): first deposit to the [receive address](/features/receive_addresses/index.md) is more expensive then the second and subsequent deposits,
> therefore, it's expedient to allocate single address multiple times for different users.

## SDK

```js
import { Blockchain } from "@curra/sdk";

// interface is same as in curra.createAddresses() method
const addresses = await curra.allocateRotatingAddresses({
	blockchains: [Blockchain.ETHEREUM],
	uniqueId: "i'm unique", // optional unique id, default: none
	meta: "my user id?", // custom data can be linked to the address, will be included in  incomes webhooks, default: none
	time: 1000 * 60 * 60, // millis, default: 48 hours
});
```

## HTTP

**path**: `/addresses/time-limited`\
**method**: `POST`

Method reference coming soon! 
