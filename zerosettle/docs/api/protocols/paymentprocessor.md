---
title: PaymentProcessor
---

# PaymentProcessor

Protocol for payment processors that handle fiat-to-crypto onramp.

## Declaration

```swift
protocol PaymentProcessor
```

## Overview

`PaymentProcessor` defines the interface for payment processors that convert fiat currency (USD, etc.) to cryptocurrency (USDC, etc.). Implementations handle the integration with specific payment providers like Coinbase Commerce.

## Instance Properties

### supportedMethods

The supported payment methods for this processor.

```swift
var supportedMethods: [PaymentMethod] { get }
```

## Instance Methods

### initiateFunding(amount:currency:destination:network:)

Initiate a funding transaction.

```swift
func initiateFunding(
    amount: Decimal,
    currency: String,
    destination: String,
    network: BlockchainNetwork
) async throws -> FundingSession
```

**Parameters:**
- `amount`: The amount to fund
- `currency`: The currency code (e.g., "USD")
- `destination`: The destination wallet address
- `network`: The blockchain network for this transaction

**Returns:** A `FundingSession` that can be used to monitor payment status

**Throws:** Payment processor errors if initiation fails

### handlePaymentEvent(_:)

Handle a payment event from the processor.

```swift
func handlePaymentEvent(_ event: PaymentEvent) async throws
```

**Parameters:**
- `event`: The payment event to handle

**Throws:** Errors if event handling fails

## See Also

- [FundingSession](/docs/api/structures/fundingsession)
- [BlockchainNetwork](/docs/api/enumerations/blockchainnetwork)
