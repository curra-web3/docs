# Gas pump

## General

As mentioned in the [introduction](/obsidian/intoduction/what_is_curra.md), Curra doesn't charge processing fees, meaning you pay only for blockchain network fees. All funds that are received to [receive addresses](../features/receive_addresses/index.md) have to be forwarded to your wallet, in order to make it possible you have to fill your balance with coins which will be used to pay for these transactions. Balance can be filled using the Curra <a href="https://app.curra.io/" target="_blank">application</a>. Curra doesn't charge you any fees, coins are used only to cover blockchain miner fees.


> ⚠️ **Attention!**
>  
> Values provided in the table below are applicable to the default configuration. [Contact us](../contact_us.md) and we will help you to find a suitable configuration

|Asset|First deposit|Second and further deposits to an address|Gas price range|
|-|-|-|-|
|Ethereum ETH|0.00091 ETH - 0.0027|0 ETH|20-60 gwei|
|Ethereum Token ERC20|0.00096 ETH - 0.0028 ETH|0.00026 ETH – 0.000785 ETH|20-60 gwei|
|Binance Smart Chain BNB|0.01 BNB|0 BNB|Constant|
|Binance Smart Chain Token BEP20|0.0002 BNB|0.00015 BNB|Constant|
|Polygon MATIC|0.0136 - 0.032 MATIC|0 MATIC|170-400 GWEI|
|Polygon Token ERC20|0.0142 MATIC|0.033 MATIC|170-400 GWEI|


## How to make it cheaper

### Enable bundles

In order to reduce your expenses x2-3 times you can enable bundles on the <a href="https://app.curra.io/configuration" target="_blank">configuration page</a>. After bundles are enabled, the Curra coordinator will wait until the configured count of deposits is confirmed on your [receive addresses](/obsidian/features/receive_addresses/index.md). After that, that will be forwarded within a single transaction, reducing fees significantly. Recommended bundle size is – 15

### Reuse addresses

The first deposit to a [receive address](/obsidian/features/receive_addresses/index.md) is ~3 times more expensive than the second and further deposits to the same address
