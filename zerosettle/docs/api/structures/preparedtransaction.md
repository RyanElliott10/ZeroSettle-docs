---
title: PreparedTransaction
---

# PreparedTransaction

A prepared transaction ready to be signed and sent.

## Declaration

```swift
struct PreparedTransaction
```

## Overview

`PreparedTransaction` represents a blockchain transaction that has been prepared and is ready to be signed and sent to the network.

## Instance Properties

### to

The destination address.

```swift
let to: String
```

### value

The value being sent (in smallest unit - wei, lamports, etc.).

```swift
let value: String?
```

### data

The transaction data/payload.

```swift
let data: String?
```

### network

The blockchain network.

```swift
let network: BlockchainNetwork
```

### feeEstimate

Gas/fee estimates.

```swift
let feeEstimate: FeeEstimate?
```

## See Also

- [BlockchainNetwork](/docs/api/enumerations/blockchainnetwork)
- [TransactionReceipt](/docs/api/structures/transactionreceipt)
