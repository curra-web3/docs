---
description: Ensure your assets are safe using rules contracts
---

# Rules

## Introduction

Rules are smart contracts deployed by Curra Protocol users ensure that user's assets can only be forwarded to certained addresses and make the protocol the first-ever payment processing tool that doesn't require direct access to your assets for processing. These rules are executed every time assets are going to be forwarded by the operator.

Example rules:

* Forward USDC, ETH, and UNI to Hot Wallet 1
* Forward only if the total balance of the receiving wallet exceeds 250 USDC
* If the transaction risk score exceeds 20%, forward tokens to the Risk Assets Wallet
* If the transaction amount exceeds 100,000 USDC, forward to Cold Wallet
* If WBTC is received, swap to USDC via Uniswap and send to Hot Wallet 3

{% hint style="info" %}
If you have any questions at any point in time, feel free to reach out to us on [Discord](https://discord.com/invite/5Qpn6Ksm)
{% endhint %}

## How to use

As mentioned before users can deploy their own rules contracts, those contracts are required to extend [RuleBase.sol](https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol) interface, let's take at look at it:

```solidity
abstract contract RuleBase {
    function _exec(address forwarder, uint256 value, address dest) internal view virtual returns (address, uint256);

    function _execERC20(address forwarder, address token, uint256 value, address dest)
        internal
        view
        virtual
        returns (address, uint256);

    function _execERC721(address forwarder, address token, uint256 id, address dest)
        internal
        view
        virtual
        returns (address);

    function _execERC1155(address forwarder, address token, uint256 id, uint256 value, address dest)
        internal
        view
        virtual
        returns (address, uint256);

    // ...............
}
```

As you can see here are mutiple methods for each token standard, for example, let's look at the `execERC20()` method, which is going to be executed everytime when operator tries to forward your erc20 assets. For details on each token standard you can check out documented source code [here](https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol). `_execERC20()` method accepts following params:

* `forwarder` – receiving address which is going to be processed by a operator
* `token` – address of ERC20 asset that is going to be forwarded
* `value` – amount of ERC20 asset that is going to be forwarded
* `dest` – forwarding destination address

To clearify how rule contract can be implemented, let's examine this method wihin the default rule [WhitelistedAddressRule.sol](https://github.com/curra-web3/contracts/blob/main/src/WhitelistedAddressRule.sol) which is automatically assigned to your Ownership NFT after it's minted. It serves only for a single feature: allow forwarding only to the address which minted an NFT.

```solidity
contract WhitelistedAddressRule is Rule {
    // here is address where assets will be forwarded
    address public immutable whitelisted;

    constructor(address _whitelisted) {
        whitelisted = _whitelisted;
    }

    function _execERC20(address, address, uint256 value, address)
        internal
        view
        override
        returns (address d, uint256 v)
    {
        // return whitelisted address from this function, so all assets can be forwarded only to it
        d = whitelisted;

        // return value provided by operator
        v = value;
    }
}
```

First thing you can notice is that [WhitelistedAddressRule.sol](https://github.com/curra-web3/contracts/blob/main/src/WhitelistedAddressRule.sol) extends the [RuleBase.sol](https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol) contract, which is required for all rules to extends and implement virtual methods.
