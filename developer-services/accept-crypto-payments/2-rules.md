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

As mentioned before users can deploy their own rules contracts, those contracts are required to implement [Rule.sol](https://github.com/curra-web3/contracts/blob/main/src/Rule.sol) interface, let's take at look at it:

```solidity
interface Rule {
    function exec(uint256 ownershipId, address forwarder, uint256 value, address dest)
        external
        view
        returns (address, uint256);

    function execERC20(uint256 ownershipId, address forwarder, address token, uint256 value, address dest)
        external
        view
        returns (address, uint256);

    function execERC721(uint256 ownershipId, address forwarder, address token, uint256 id, address dest)
        external
        view
        returns (address);

    function execERC1155(uint256 ownershipId, address forwarder, address token, uint256 id, uint256 value, address dest)
        external
        view
        returns (address, uint256);
}
```

As you can see here are mutiple methods for each token standard, for example, let's look at the `execERC20()` method, which is going to be executed everytime when operator tries to forward your erc20 assets. For details on each token standard you can check out documented source code [here](https://github.com/curra-web3/contracts/blob/main/src/Rule.sol). `execERC20()` method accepts following params:

* `ownershipId` – id of your Ownership NFT
* `forwarder` – receiving address which is going to be processed by a operator
* `token` – address of ERC20 asset that is going to be forwarded
* `value` – amount of ERC20 asset that is going to be forwarded
* `dest` – forwarding destination address

To clearify how rule contract can be implemented, let's examine this method wihin the default rule [WhitelistedAddressRule.sol](https://github.com/curra-web3/contracts/blob/main/src/Rule.sol) which is automatically assigned to your Ownership NFT after it's minted. It serves only for a single feature: allow forwarding only to the address which minted an NFT.

```solidity
contract WhitelistedAddressRule is Rule {
    address public immutable whitelisted;

    constructor(address _whitelisted) {
        whitelisted = _whitelisted;
    }

    function execERC20(uint256, address, address, uint256 value, address dest)
        external
        view
        override
        returns (address, uint256)
    {
        if (dest == address(0x0)) {
            return (whitelisted, value);
        }
        require(dest == whitelisted, "Dest");
        return (dest, value);
    }
}
```

First thing you can notice is that [WhitelistedAddressRule.sol](https://github.com/curra-web3/contracts/blob/main/src/WhitelistedAddressRule.sol) implements the [Rule.sol](https://github.com/curra-web3/contracts/blob/main/src/Rule.sol) interface, which is required for all rules to implement.

The code above does the following:

1. If the destination specified by the operator is a null address, just return the whitelisted address `whitelisted`.
2. If a destination is provided by the operator, ensure that it's equal to the whitelisted address.
   * If it's not equal, abort.
   * If it's equal, allow forwarding.
