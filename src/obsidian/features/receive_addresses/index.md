# Receive addresses

## Introduction

![receive address example](/obsidian/images/receive_address_example.png)

If you operate a retail-oriented crypto business such as an exchange, lending desk, or neobank, you probably receive a significant number of ERC20/coin deposits on a daily basis. To effectively handle and track these deposits, it is necessary to assign a new address to each client. Received  funds are automatically forwarded to your configured address.

## Prerequisites

Before you can create addresses, you should [authorize](/obsidian/security/api_authorization.md) your server.

> 📖 **Notes on addresses**
> 
> Every address is generated from unique salt (can be considered an unique identifier) and addresses remain the same across different EVM chains if their salts are equal. This means you can utilize the same addresses across multiple EVM blockchains that are supported.

## Available methods

  - [Create new addresses](/obsidian/features/receive_addresses/create.md)

