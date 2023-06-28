# Create address by salt

## Intro

Use this method when you want to create an address with specific salt. Useful when you want to create same address across different blockchains. Example:

```ts
const ethereumForwarder = await curraEthereum.createNextForwarder()
const polygonForwarder = await curraPolygon.createForwarder({
  salt: ethereumForwarder.salt
})

// addresses are same if same ownership id and salt are used to create curra instances on multiple blockchains
assert(ethereumForwarder.address === polygonForwarder.address)
```

## SDK

```js
const { address } = await curra.createForwarder({
  salt: "0x00000000000000000000000000000000000000000001" 
})

// new address with additional fields
const { address } = await curra.createForwarder({
  salt: "0x00000000000000000000000000000000000000000001",
  destination: "0x67b1d87101671b127f5f8714789C7192f7ad340e", // specify if your rule smart contract supports multiple destinations
  uniqueId: "i'm unique", // optional unique id 
  meta: "my user id?", // custom data can be linked to the address, will be included in  incomes webhooks
})

// catch error and resolve
import { RequesterError } from '@curra/sdk'

try {
	const { address } = await curra.createForwarder({
	  salt: "0x00000000000000000000000000000000000000000001",
	  uniqueId: "i'm not unique"
	})
} catch (e) {
	if (e instanceof RequesterError) {
      // unique id error example,
      // for all errors that can occur look at the HTTP endpoint reference below
	  if (e.body.error === 'UNIQUE_ID') {
		  // your logic here
	  }	
	} else {
	  throw e
	}
}
```

### HTTP

**method**: `POST`

**path**: `/forwarders`

**headers**: 
- content-type: application/json

**request body**:
```ts
// TS notation
{
  salt: string, // hex value which will be used to generate your address, format: 0x00000000000000000000000000000000000000000000, 32 bytes
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

**invalid salt response** ❌:

status: 422\
body:
```ts
{ 
  "error": "INVALID_SALT", 
  "message": "Salt should be in hex format and represent 32 bytes 0x00000000000000000000000000000000000000000000" 
}
```

**Salt in not unique response** ❌:

status: 400\
body:
```json
{ 
  "error": "SALT_IS_NOT_UNIQUE",
  "message": "Salt is not unique"
}
```
