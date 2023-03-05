# Choose Operator

Operators are responsible for executing transactional clearing for Protocol User, triggering on-chain transaction from **Receive Address** and Relaying Withdrawals for Protocol User with their own pricing model and feature set.

Depending on your needs, you can find a suitable operator.

### Curra Core Operator

Currently, the Curra Operator is the only operator available and is chosen by default. Anyone who wants to use it will need to replenish the operator's balance, which will be used to compensate transaction fees.

**Pricing**: From 20% Premium Percent of consumed Gas

* [x] Assets Forwarding
* [x] Relayer

{% hint style="info" %}
Other operators with third-party integrations to be available soon, or you can deploy private operator to avoid premium fee. [How to Deploy Operator?](../deploy-operator.md)
{% endhint %}
