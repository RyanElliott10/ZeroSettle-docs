---
title: BlockchainNetwork
---

# BlockchainNetwork

Supported blockchain networks.

## Declaration

```swift
enum BlockchainNetwork
```

## Overview

`BlockchainNetwork` enumerates the blockchain networks supported by ZeroSettleKit, including Solana and multiple EVM-compatible chains.

## Enumeration Cases

### solana

```swift
case solana
```

Solana blockchain network.

### base

```swift
case base
```

Base (Coinbase L2) blockchain network.

### ethereum

```swift
case ethereum
```

Ethereum mainnet.

### arbitrum

```swift
case arbitrum
```

Arbitrum network.

### optimism

```swift
case optimism
```

Optimism network.

### polygon

```swift
case polygon
```

Polygon (formerly Matic) network.

## Instance Properties

### displayName

Display name for the network.

```swift
var displayName: String { get }
```

### chainId

Chain ID for EVM networks (nil for non-EVM like Solana).

```swift
var chainId: Int? { get }
```

## See Also

- [ZeroSettleConfig](/docs/api/structures/zerosettleconfig)
- [FundingSession](/docs/api/structures/fundingsession)
