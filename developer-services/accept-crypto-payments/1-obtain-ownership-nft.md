---
description: Your Custody in NFT
---

# Obtain Ownership NFT

Obtaining the Ownership NFT is the first step to start your journey with Curra. This token serves as a personal identifier and a key for Protocol User to gain access to Curra.

The Ownership NFT offers the following advantages:

* Only the NFT owner can communicate with the protocol and its participants.
* Only the NFT owner can change forwarding rules.
* Crosschain: the protocol operates on NFT numeric IDs instead of addresses, which can differ on multiple blockchains.
* NFT IDs are used as a salt when generating deterministic forwarding addresses and are the backbone of the protocol security.

Also:

* NFTs can be transferred to other addresses, including smart contract wallets such as ChainSafe.
* A single account can possess multiple NFTs.
* NFTs can be staked or swapped on any protocol that supports ERC721 tokens.
* Multiple NFTs can be held by a single account.
* Tokens can be transferred to other accounts, unlike common crypto accounts/addresses where private keys cannot be rotated or regenerated.

### How to Obtain

You can mint the Ownership NFT via [Curra DApp](https://app.curra.io), or by calling the `mint()` method on the Curra main contract [Curra.sol](https://github.com/curra-web3/contracts/blob/main/src/Curra.sol#L49).

{% hint style="info" %}
By default, minted NFTs will be linked with the [Whitelisted Address Rule](2-rules.md), enabling asset forwarding only to the address that minted the NFT.
{% endhint %}
