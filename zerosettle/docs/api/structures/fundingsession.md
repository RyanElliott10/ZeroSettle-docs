---
title: FundingSession
---

# FundingSession

A funding session created by a payment processor.

## Declaration

```swift
struct FundingSession
```

## Overview

`FundingSession` represents an active payment session created by a `PaymentProcessor`. It contains all the information needed to complete a payment and track its status.

## Instance Properties

### paymentURL

The payment URL to load in a web view or browser.

```swift
let paymentURL: URL
```

This URL should be loaded in a web view to allow the user to complete the payment.

### sessionId

The unique session/order ID for this payment.

```swift
let sessionId: String
```

Use this ID to query payment status or cancel the session.

### amount

The amount being funded.

```swift
let amount: Decimal
```

### currency

The currency code (e.g., "USD").

```swift
let currency: String
```

### destinationAddress

The blockchain address that will receive the funds.

```swift
let destinationAddress: String
```

### network

The blockchain network for this funding session.

```swift
let network: BlockchainNetwork
```

### metadata

Additional metadata from the payment processor.

```swift
let metadata: [String: String]?
```

## Example Usage

```swift
// Create a funding session
let session = try await manager.initiateFunding(
    amount: 10.00,
    currency: "USD",
    destination: nil
)

// Open the payment URL in a web view
if let url = session.paymentURL {
    // Present web view with this URL
    presentPaymentView(url: url)
}

// Monitor the session status
Task {
    let status = try await paymentProcessor.getPaymentStatus(
        sessionId: session.sessionId
    )
    print("Payment status: \(status)")
}
```

## See Also

- [ZeroSettleManager](/docs/api/classes/zerosettlemanager)
- [PaymentProcessor](/docs/api/protocols/paymentprocessor)
