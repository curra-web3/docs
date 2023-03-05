# Create Receive Wallet

Merchants and Custodians create unique receive wallets to accept payments from end-users for identification purposes.

With Curra, you can create Receive Wallets on your side using the SDK. All Receiving Wallets are pre-calculated off-chain (from Ownership NFT) using the CREATE2 algorithm.

After the end-user sends assets to the Receive Wallet, the Operator deploys a smart contract to this wallet (for the first flush) and flushes the asset according to the forwarding rule specified in the Rules Smart Contract, charging the protocol user a fee for this operation.

### Usage

You can create forwarding addresses via [Curra DApp](https://app.curra.io) or use [Curra SDK](developer-services/javascript-ts-sdk.md).

### How it works

Let's describe the full flow from address creation to assets being forwarded to the target address in detail using the following example: "Receive 1 USDC ERC20 to the address with index 5i and ownership NFT ID #100."

1. The address is deterministically pre-calculated based on the NFT ID and address index using the **CREATE2** algorithm. '#100' + '5i' is used as salt.
2. The address is imported to the Coordinator, which indexes it for incoming transactions.
3. 1 USDC is transacted to the address.
4. The Coordinator detects the transaction and broadcasts a forwarding job to all operators.
5. If you have chosen a specific operator, it will create a forwarding transaction for you.
   * If it is the first transaction to the address, the operator will deploy a forwarder contract to receive address that will automatically transfer ETH.
   * If it is not the first transaction, the operator will trigger forwarding on the previously deployed contract.
6. If the operator's transaction satisfies the rule smart contract linked to the ownership NFT, the assets will be forwarded to the destination address. If transaction doesn't satisfies the rule smart contract - transaction will be failed by blockchain.

The process of assets forwarding is completely trustless and backed by [Curra Smart Contracts](https://github.com/curra-web3/contracts).
