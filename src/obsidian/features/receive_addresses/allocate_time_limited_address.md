# Allocate time-limited address 🔜

## Intro

![time limited address](/obsidian/images/temporary_addresses.png)

Use this method to allocate a time-limited address. You can specify time to reserve an address for an operation, once time elapsed – address is ready for a new reservation

> 💸 **Why?**
> 
> As you noticed in [gas pump costs](/obsidian/costs/gas_pump.md): first deposit to the [receive address](obsidian/features/receive_addresses/index.md) is more expensive then the second and subsequent deposits,
> therefore, it's expedient to allocate single address multiple times for different users.

## SDK

```js
// just new address
const { address } = await curra.allocateRotatingForwarder()

// new address with additional fields
const { address } = await curra.allocateRotatingForwarder({
  destination: "0x67b1d87101671b127f5f8714789C7192f7ad340e", // specify if your rule smart contract supports multiple destinations
  uniqueId: "i'm unique", // optional unique id, default: none
  meta: "my user id?", // custom data can be linked to the address, will be included in  incomes webhooks, default: none
  time: 1000 * 60 * 60 // millis, default: 48 hours
})

// catch error and resolve
import { RequesterError } from '@curra/sdk'

try {
	const { address } = await curra.createRotatingForwarder({
	  uniqueId: "i'm not unique"
	})
} catch (e) {
	if (e instanceof RequesterError) {
      // unique id error example,
      // for all errors that can occur look at the HTTP endpoint reference below
	  if (e.body?.error === 'UNIQUE_ID') {
		  // your logic here
	  }	
	} else {
	  throw e
	}
}
```

## HTTP

**method**: `POST`\

**path**: `/forwarders/rotating/free`\

**headers**: 
- content-type: application/json

**request body**:
```ts
// TS notation
{
  destination?: string, // specify if your rule smart contract supports multiple destinations
  uniqueId?: string, // optional unique id 
  meta?: string, // custom data can be linked to the address, will be included in incomes webhooks
  time?: number, // reservation time in millis, default: 48 hours
}
```

**success response** ✅:

status: 200\
body:
```ts
// TS notation
{
  address: string, // address value
  salt: string, // unique address salt used for address generation
  meta?: string, // custom data linked to the address
  uniqueId?: string, // unique id of the address
  time?: number, // reservation time in millis, default: 48 hours
}
```

**unique id collision response** ❌:

status: 400\
body:
```ts
{ 
  "error": "UNIQUE_ID", 
  "message": "Unique id collision" 
}
```
