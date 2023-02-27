# Onboarding

## Security

First things first. To start accepting crypto payments you need to set Forwarding Rules (Ownership NFT + Rules Smart Contract) to declare authorised addresses where assets can be forwarded to and/or create automations on the top (Swap, Refund, etc.).&#x20;

### 1. Mint Ownership NFT

Ownership NFT serves as a personal identifier and a key for Protocol User to gain access to Curra.

You can mint Ownership NFT via [**Curra DApp**](https://app.curra.io)**.**

### 2. Deploy Rules Smart Contract

Rules Smart Contract deployed to protect Protocol User and set rules and restrictions for Operator on how to settle payments.

For example:&#x20;

* Flush USDC, ETH and UNI to Hot Wallet 1
* Flush only if total balance of receiving wallet exceeds 250 USDC
* If transaction risk score exceeds 20% - flush tokens to Risk Assets Wallet
* If transaction amount exceeds 100,000 USDC flush to Cold Wallet
* If WBTC received - swap to USDC via Uniswap and send to Hot Wallet 3

{% hint style="info" %}
If you have any questions at any point in time, feel free to reach us out on [**Discord**](https://discord.com/invite/5Qpn6Ksm)
{% endhint %}

### 3. Choose Operator

Operators are responsible for executing transactional clearing for Protocol User, triggering on-chain transaction from **Receiving Wallet** and Relaying Withdrawals for Protocol User with their own pricing model and feature set.&#x20;

Depending on your needs, you can find a suitable operator.

### Curra Core

**Pricing**: From 20% Premium Percent of consumed Gas

* [x] Assets Forwarding
* [x] Relayer

{% hint style="info" %}
Other operators with third-party integrations to be available soon, or you can deploy private operator to avoid premium fee. [How to Deploy Operator?](../deploy-operator.md)
{% endhint %}
