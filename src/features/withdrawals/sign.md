# Sign withdrawal

## Intro

API is completly non-custodial, signer with keys are on user's custody.
To accomplish non-custodial design curra forms transactions and sends those to a signer for
<a href="https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm" target="_blank">ECDSA signature</a>

Any signer implementation that supports BIP32 ECDSA signing can be seamlessly used with Curra

## SDK

```js
const withdrawal = await curra.getWithdrawal({
    blockchain: Blockchain.ETHEREUM,
    id: "withdrawal id",
});

// replace mnemonic phrase with yours
const mnemonic =
    "frost senior river admit load drill response swamp joke between label leader medal coconut photo";
const curraWithdrawals = CurraWithdrawals.fromMnemonic(curra, mnemonic);
const signatures = await curraWithdrawals.sign(withdrawal.rawUnsigned);

await curra.signWithdrawal({
    // <-- payment is signed and broadcasted to the blockchain
    blockchain: Blockchain.ETHEREUM,
    id: withdrawal.id,
    signatures,
});
```

## Without SDK

To sign withdrawal you can use any signer which supports BIP32.

`"rawUnsigned"` field of the payment contrains list of the following format

-   path – BIP32 HD wallet path. Example: `m/44'/60'/0'/0/0`
-   value – hash in hex format which represents a transaction

You should retrive private key for the `path` and sign the `value` with it.

After signing complete you can send signatures to Curra API using following endpoint:

**path**: `/withdrawals/sign`\
**method**: `POST`

Method reference <a href="https://api.curra.io/documentation/static/index.html#/default/post_withdrawals" target="_blank">here</a>
