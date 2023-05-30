# Protocol

## Motivation

As mentioned in the [introduction](/obsidian/what_is_curra.md) Curra leverages an on-chain protocol to replace the centralized nature of crypto processing. Through smart contracts within the protocol, we guarantee that all funds belong solely to you, those contracts are called **Rules**. At every stage of the processing, you maintain full ownership of your client's funds, with no intermediaries involved. All assets are securely directed straight to your wallet, which is specified in the rule.

## How it works?

Rules are smart contracts deployed by Curra Protocol users to ensure that users' assets can only be forwarded to certain addresses and make the protocol the first-ever payment processing tool that doesn't require direct access to your assets for processing. These rules are executed every time assets are going to be forwarded by the coordinator.

As mentioned before users can deploy their own rules contracts, those contracts are required to extend <a href="https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol" target="_blank">RuleBase.sol</a> interface, let's take a look at it:
```
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

As you can see here are multiple methods for each token standard, for example, let's look at the `execERC20()` method, which is going to be executed every time when coordinator tries to forward your ERC20 assets. For details on each token standard, you can check out documented source code <a href="https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol" target="_blank">here</a>. `_execERC20()` method accepts the following params:

- `forwarder` – receiving address which is going to be processed by an coordinator
- `token` – address of ERC20 asset that is going to be forwarded
- `value` – amount of ERC20 asset that is going to be forwarded
- `dest` – forwarding destination address

To clarify how to rule contract can be implemented, let's examine this method with the default rule <a href="https://github.com/curra-web3/contracts/blob/main/src/WhitelistedAddressRule.sol" target="_blank">WhitelistedAddressRule.sol</a> which is automatically assigned to your Ownership NFT after it's minted. It serves only for a single feature: allow forwarding only to the address which minted an NFT.

```
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

        // return value provided by the coordinator (total balance of the forwarder usually)
        v = value;
    }
}
```
The first thing you can notice is that <a href="https://github.com/curra-web3/contracts/blob/main/src/WhitelistedAddressRule.sol" target="_blank">WhitelistedAddressRule.sol</a> extends the [RuleBase.sol](https://github.com/curra-web3/contracts/blob/main/src/RuleBase.sol) contract, which is required for all rules to extend and implement virtual methods.
