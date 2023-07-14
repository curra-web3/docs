# Create new address

## Intro

Use this method to allocate a new never used address.

## SDK

```js
// just new address
const { address } = await curra.createNextForwarder()

// new address with additional fields
const { address } = await curra.createNextForwarder({
  destination: "0x67b1d87101671b127f5f8714789C7192f7ad340e", // specify if your rule smart contract supports multiple destinations
  uniqueId: "i'm unique", // optional unique id 
  meta: "my user id?", // custom data can be linked to the address, will be included in  incomes webhooks
})

// catch error and resolve
import { RequesterError } from '@curra/sdk'

try {
	const { address } = await curra.createNextForwarder({
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

**path**: `/forwarders/next`\

**headers**: 
- content-type: application/json

**request body**:
```ts
// TS notation
{
  destination?: string, // specify if your rule smart contract supports multiple destinations
  uniqueId?: string, // optional unique id 
  meta?: string, // custom data can be linked to the address, will be included in  incomes webhooks
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
