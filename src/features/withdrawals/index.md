# Non-custodial withdrawals API

## Overview

![flow](/images/withdrawals-flow.png)

The non-custodial withdrawals API simplifies the process of creating blockchain withdrawal payments. It enables users to securely manage private keys on the client side and delegates the signing process to the client, streamlining development across various blockchains.

The non-custodial API provides a straightforward solution for secure and uniform withdrawal creation, offering efficiency and enhanced security in blockchain development.

## Key advantages

**Uniform API for all supported blockchains:**

Developers use the same API for withdrawals on any supported blockchain, eliminating the need to learn and implement blockchain-specific details.

**Enhanced security:**

The API delegates the signing process to the client, maintaining the security of private keys. Private keys remain on the client side, following a non-custodial approach to bolster security.

**Time and resource savings:**

Developers save time by avoiding the complexities of learning and implementing withdrawal mechanisms for each blockchain.

**Automatic issues resolving:**

Curra also monitors all withdrawal transactions and automatically resolves any blockchain-related issues like:
- Stuck transactions
- Failed transactions

