# HAPI Ethereum Proxy documentation

This repository contains currently deployed Solidity source code and ABI for HAPI Ethereum Proxy smart contract.

# Networks

We support various Ethereum-based networks

| Network | Contract Address |
|---------|------------------|
| Ethereum Mainnet | 0x730c549587b3d6068F78DcED2C0d18Ae6c731B02 |
| OKC Mainnet | 0x82edC3E28B5bF80b42900464dDbf5316Eed49258 |
| OKC Testnet | 0x82edC3E28B5bF80b42900464dDbf5316Eed49258 |

# Methods

## createReporter

Arguments:
- `address` reporterAddress
- `uint8` permissionLevel

This is a method that adds a new reporter to the contract. It can only be called by the contract owner.

## updateReporter

Arguments:
- `address` reporterAddress
- `uint8` permissionLevel

This is a method that updates an existing reporter. It can only be called by the contract owner.

## createAddress

Arguments:
- `address` address
- `Category` category
- `uint8` risk

This is a method to add a new address to the contract. This can only be called by a reporter with permission level of 1 or more.

## createAddresses

Arguments:
- `address[]` address
- `Category` category
- `uint8` risk

This is a method to add multiple new addresses to the contract. This can only be called by a reporter with permission level of 1 or more.

## updateAddress

Arguments:
- `address` address
- `Category` category
- `uint8` risk

This is a method update an existing address. This can only be called by a reporter with permission level of 2.

## getAddress

Arguments:
- `address` address

This is a method to get the addresses category index and risk score. Can be called by anyone.

## getReporter

Arguments:
- `address` reporterAddress

This is a method to get the permission level of a reporter. Can be called by anyone.

# Categories

Category is represented by an enum with the following values:

| Category | Index |
|----------|-------|
| None | 0 |
| WalletService | 1 |
| MerchantService | 2 |
| MiningPool | 3 |
| Exchange | 4 |
| DeFi | 5 |
| OTCBroker | 6 |
| ATM | 7 |
| Gambling | 8 |
| IllicitOrganization | 9 |
| Mixer | 10 |
| DarknetService | 11 |
| Scam | 12 |
| Ransomware | 13 |
| Theft | 14 |
| Counterfeit | 15 |
| TerroristFinancing | 16 |
| Sanctions | 17 |
| ChildAbuse | 18 |

# Example

Here's an example of getting address information using [Gochain's web3 client](https://github.com/gochain/web3):

Command:
```sh
web3 --rpc-url $RPC_URL contract call --address $CONTRACT_ADDRESS --abi HapiProxy.abi --function getAddress $TARGET_ADDRESS
```

`$RPC_URL` is a link to an RPC node to connect to. `$CONTRACT_ADDRESS` is an address from the contract address table above (depends on the network). `$TARGET_ADDRESS` is an address to get risk data for (example: `0xa0c7BD318D69424603CBf91e9969870F21B8ab4c` for Ethereum or `0x9e8B0eFD2194cF08AA8424d6B55B64a585914bAa` for OKC).

Example output:
```
12
10
```

12 is category (Spam from the category table above). 10 is risk score (on the scale from 0..10, i.e. max risk).
