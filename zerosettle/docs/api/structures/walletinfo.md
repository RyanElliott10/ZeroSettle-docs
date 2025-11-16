---
title: WalletInfo
---

# WalletInfo

Information about a user's wallet.

## Declaration

```swift
struct WalletInfo
```

## Overview

`WalletInfo` contains information about a user's blockchain wallet, including the address, network, and whether it was newly created.

## Instance Properties

### address

The wallet address.

```swift
let address: String
```

### network

The blockchain network.

```swift
let network: BlockchainNetwork
```

### isNew

Whether this is a newly created wallet.

```swift
let isNew: Bool
```

### type

Optional wallet type/provider.

```swift
let type: String?
```

## See Also

- [BlockchainNetwork](/docs/api/enumerations/blockchainnetwork)
- [ZeroSettleDelegate](/docs/api/protocols/zerosettledelegate)
