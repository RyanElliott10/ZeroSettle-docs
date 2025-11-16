---
title: TransactionReceipt
---

# TransactionReceipt

Transaction receipt after confirmation.

## Declaration

```swift
struct TransactionReceipt
```

## Overview

`TransactionReceipt` contains information about a transaction after it has been confirmed on the blockchain.

## Instance Properties

### hash

The transaction hash.

```swift
let hash: String
```

### blockNumber

Block number.

```swift
let blockNumber: Int?
```

### status

Whether the transaction was successful.

```swift
let status: Bool
```

### gasUsed

Gas used.

```swift
let gasUsed: String?
```

## See Also

- [PreparedTransaction](/docs/api/structures/preparedtransaction)
- [ZeroSettleDelegate](/docs/api/protocols/zerosettledelegate)
