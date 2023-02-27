# Architecture

<figure><img src="../.gitbook/assets/Frame 48098604 (2).png" alt=""><figcaption></figcaption></figure>

Curra Architecture is responsible for ensuring that crypto processing flow is executed correctly, secure and efficiently.&#x20;

In essence the Curra Protocol role is to continuously check if the conditions for a crypto processing  Jobs to execute have been met and when they are met, Delegate Job to relevant Operator and ensure that it gets completed as efficiently as possible.&#x20;

## Curra Protocol Roles

### **Protocol User**

The **Protocol User** is a Merchant or Custodian who wants to accept cryptocurrency as a payment method and/or initiate withdrawals for employees or end-users.&#x20;

**Protocol User** is required to deploy a **Rules Smart Contract**, which includes a list of approved addresses to forward funds to, and outlines the steps for executing on-chain automations during the clearing process, that are impossible to violate.

Each **Protocol User** has to choose appropriate **Operator** for transactional clearing and gasless withdrawals relaying, depending on Operator pricing model and feature set or deploy it's own private Operator with custom logic.

{% hint style="info" %}
**Clearing** is a set of activities related to the settling process that assets must go through,&#x20;

e.g. Forward to Cold Wallet, Settle assets in Stablecoin/Fiat, Execute AML Forwarding Rules, etc.
{% endhint %}

### **Operator (aka. Acquirer)**

The Operator is responsible for executing transactional clearing for Protocol User, triggering on-chain transaction from **Receiving Wallet** and Relaying Withdrawals for Protocol User**.**

**Operators** are restricted to transferring assets solely to the wallet of the **Protocol User (Target Address),** specified in **Rules Smart Contract** or executing automations as outlined in the **Rules Smart Contract.**&#x20;

{% hint style="success" %}
**Protocol User** assets, located on **Receiving Wallet** secured on-chain by **Rules Smart Contract**

**Protocol User** creates an **Ownership NFT** with specified forwarding rules, for example "forward only to hot wallet". All **Operator** transactions must comply with this rule, protecting Merchants and Custodians from Malicious activity of counterparties, otherwise transaction, initiated by Operator, will be rejected by network.
{% endhint %}

Anybody can deploy their own Operator implementing Forwarding Rules Interface to enhance crypto processing with consumer-oriented features.

We anticipate that Fiat Off-ramp services, Compliance Services, Custodians, and other B2B Crypto Solutions will become Operators, contributing and expanding Curra Protocol, with their own monetisation model, to reach new clients, providing additional services along with crypto processing, not bothering with Crypto Processing Back-end.

**Operator Example**: Retail Store that wants to accept crypto and directly settle it to its Bank Account. They can choose Off-ramp Operator and accept crypto with automated settlements, where Operator can cover all Gas Costs, on it’s own.

### **Coordinator**

The **Coordinator** role is to delegate clearance Jobs (Tasks) to **Operators** and monitor for malicious behaviour, with the power to "Punish" Operators by reducing their stake for inappropriate on-chain conduct.

