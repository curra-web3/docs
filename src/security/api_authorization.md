# API authorization

## Webhooks

In order to authorize Curra webhooks, like [transfer notifications](/features/transfer_notifications.md), you can use JS/TS SDK or verify it manually.

### JS/TS SDK

Using a public key recovery (more secure way):

```js
// raw string body should be provided
const body = request.rawBody
const signature = request.headers.signature

// boolean here
const ok = await curra.verifyWebhookRequest(req.rawBody, req.headers.signature)
```

Using secret:

```js
const secret = request.headers.secret

const originalSecret = await curra.getSecret();
const ok = secret === originalSecret
```

### Manually authorize HTTP request

Here are two ways you can verify a webhook request:
1. Compare the `SECRET` header with your secret
2. Recover the public key from the `SIGNATURE` header using ECDSA recovery and compare it with API public key, which can be retrieved using `GET /pubkey` API endpoint


