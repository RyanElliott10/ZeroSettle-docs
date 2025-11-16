---
title: ZeroSettlePayoutTable
---

# ZeroSettlePayoutTable

Normalized representation of an app-specific payout table.

## Declaration

```swift
struct ZeroSettlePayoutTable
```

## Overview

`ZeroSettlePayoutTable` represents a configured payout table for distributing payments across multiple recipients. Partner apps can configure different payout tables in the ZeroSettle dashboard, and this structure provides the normalized representation of those configurations.

## Creating a Payout Table

### init(id:appId:name:version:status:createdAt:tiers:)

Creates a new payout table.

```swift
init(
    id: Int,
    appId: Int,
    name: String,
    version: Int,
    status: String,
    createdAt: String,
    tiers: [PayoutTier]
)
```

**Parameters:**
- `id`: Internal database identifier
- `appId`: The partner app identifier
- `name`: Human readable name
- `version`: Incrementing version number
- `status`: Current status (e.g., "active", "draft", "archived")
- `createdAt`: ISO8601 timestamp string
- `tiers`: Normalized tier list

## Instance Properties

### id

Internal database identifier for the payout table record.

```swift
let id: Int
```

### appId

The partner app identifier that owns this payout table.

```swift
let appId: Int
```

### name

Human readable name shown in partner dashboard.

```swift
let name: String
```

### version

Incrementing version number (1-based).

```swift
let version: Int
```

### status

Current status (e.g., `active`, `draft`, `archived`).

```swift
let status: String
```

### createdAt

ISO8601 timestamp string for when this version was created.

```swift
let createdAt: String
```

### tiers

Normalized tier list, sorted by guesses used ascending.

```swift
let tiers: [PayoutTier]
```

## Example Usage

```swift
// Fetch the latest payout table for your app
let payoutTable = try await manager.fetchLatestPayoutTable()

print("Payout table: \(payoutTable.name) v\(payoutTable.version)")
print("Status: \(payoutTable.status)")
print("Number of tiers: \(payoutTable.tiers.count)")

// Iterate through payout tiers
for tier in payoutTable.tiers {
    print("Tier: \(tier)")
}
```

## See Also

- [ZeroSettleManager](/docs/api/classes/zerosettlemanager)
