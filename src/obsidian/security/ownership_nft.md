# Ownership NFT

## What and why

Obtaining the Ownership NFT is the first step to start your journey with Curra. This token serves as a personal identifier and a key for you to gain access to Curra protocol.

The Ownership NFT offers the following advantages:

- Only the NFT owner can communicate with the protocol and its participants.
- Only the NFT owner can change forwarding rules.
- Crosschain: the protocol operates on NFT numeric IDs instead of addresses, which can differ on multiple blockchains.
- NFT IDs are used as a salt when generating deterministic forwarding addresses and are the backbone of the protocol security.

Also:

- NFTs can be transferred to other addresses, including smart contract wallets such as ChainSafe.
- A single account can possess multiple NFTs.
- NFTs can be staked or swapped on any protocol that supports ERC721 tokens.
- Tokens can be transferred to other accounts, unlike common crypto accounts/addresses where private keys cannot be rotated or regenerated.

## How to obtain

Here are few ways:
- Complete onboarding on Curra <a href="https://app.curra.io" target="_blank">application</a>
- `mint()` method on the Curra main contract <a href="https://github.com/curra-web3/contracts/blob/main/src/Curra.sol#L49" target="_blank">Curra.sol</a>. 

After NFT is minted you can get Ownership NFT ID on Curra <a href="https://app.curra.io" target="_blank">application</a> via wallet modal:


![where to get ownership id](/obsidian/images/get_ownership_id.png)
