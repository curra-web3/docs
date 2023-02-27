# Create Receiving Wallet

Merchants and Custodians create unique receiving wallets to accept payments from end-users for identification purposes.

With Curra, you can create Receiving Wallets on your side using the SDK. All Receiving Wallets are pre-calculated (from Ownership NFT) off-chain with the cost-efficient [CREATE2](https://docs.openzeppelin.com/cli/2.8/deploying-with-create2) method.

After end-user send assets to Receiving Wallet - Operator deploy a smart contract to this wallet (for first flush) and flush the asset according to forwarding rule specified in Rules Smart Contract, charging Operator specific fee for this operation.
