# INTEGRATE-1469: Create a storedPayload

This repository is not meant for production, testing only.  It is a fork of [boilerplate](https://github.com/LayerZero-Labs/boilerplate).  Please do not distribute this anywhere, as it will likely be removed one day.

This repository sets up a "mock" ExampleOFT on mainnet (polygon & optimism) and testnet (goerli and bsc-testnet).  It
takes advantage of a low adapterParamsV1 `dstGasLimit` to ensure that the payload is stored on the target chain.

:warning: Ensure you have the proper funds on the above networks in order to perform the steps below!

## Setup

1. Set up your mnemonic in a `.env` file.  See `.env.example` for an example.
2. Run `yarn install`.

## mainnet environment

OFTv1 deployment on Polygon and Optimism.

### Deployment Steps

This has already performed, just here for documentation purposes:

```shell
npx hardhat deploy --network polygon --tags ExampleOFT
npx hardhat deploy --network arbitrum --tags ExampleOFT
npx hardhat wireAll --e mainnet --config-path "./constants/oftConfig/wireUpConfig-mainnet.json"
```

### Create a StoredPayload on mainnet

#### Create a StoredPayload on Optimism

Note, this takes a while to run, as Polygon has long probabilistic finality times.  Try the opposite direction for a
quicker test.

```shell
npx hardhat --network polygon oftSend --qty 1 --target-network optimism
```

Example:

Polygon srcTxHash: https://polygonscan.com/tx/0x85024cd8049360fe7c1f3742cb734e7860a402bb55f75ddd70c701a2227ce6cf

Scan Link: https://layerzeroscan.com/109/address/0x3d1aaf8bcfae58b8a972191459d5fb501be32070/message/111/address/0x3d1aaf8bcfae58b8a972191459d5fb501be32070/nonce/1


#### Create a StoredPayload on Polygon

```shell
npx hardhat --network optimism oftSend --qty 1 --target-network polygon
```

Optimism srcTxHash: https://optimistic.etherscan.io/tx/0x63b2c80ef6b1995f3be950269b30e3bc4abb797dd71f4cd9762c960530833818

Scan Link: https://layerzeroscan.com/111/address/0x3d1aaf8bcfae58b8a972191459d5fb501be32070/message/109/address/0x3d1aaf8bcfae58b8a972191459d5fb501be32070/nonce/1

#### Send a regular transfer which shouldn't cause a StoredPayload (optimism to polygon)

```shell
npx hardhat --network optimism oftSend --qty 1 --target-network polygon --dst-gas-limit 100000
```

## testnet environment

OFTv1 deployment on Goerli and BSC.

### Deployment Steps

This has already performed, just here for documentation purposes:

```shell
npx hardhat deploy --network goerli --tags ExampleOFT
npx hardhat deploy --network bsc-testnet --tags ExampleOFT
npx hardhat wireAll --e mainnet --config-path "./constants/oftConfig/wireUpConfig-testnet.json"
```


### Create a StoredPayload on bsc-testnet

```shell
npx hardhat --network goerli oftSend --qty 1 --target-network bsc-testnet
```

### Create a StoredPayload on goerli

