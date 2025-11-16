---
title: Quickstart
sidebar_position: 3
---

# Quickstart

Build a complete payment flow in 10 minutes.

## Prerequisites

Complete the [Getting Started](/docs/getting-started) guide first to install and configure ZeroSettleKit.

## 1. Authenticate Users

```swift
// Send OTP
try await manager.sendOTPCode(to: "+14155551234")

// Verify and login
try await manager.loginWithOTP(code: "123456", phoneNumber: "+14155551234")
```

## 2. Initiate Payment

```swift
let session = try await manager.initiateFunding(
    amount: 10.00,
    currency: "USD",
    destination: nil  // Uses current user's wallet
)

// Open payment URL in web view
presentPaymentView(url: session.paymentURL)
```

## 3. Monitor Payment Status

```swift
// Check payment status
let status = try await paymentProcessor.getPaymentStatus(
    sessionId: session.sessionId
)

// Or wait for completion
try await session.waitForCompletion()
```

## 4. Check Balance

```swift
// Access current balances
let usdcBalance = manager.balances[.usdc]

// Refresh balance
try await manager.refreshBalance()
```

## Complete Example

```swift
struct ContentView: View {
    @EnvironmentObject var manager: ZeroSettleManager

    var body: some View {
        if manager.isAuthenticated {
            VStack {
                Text("Balance: \(manager.balances[.usdc] ?? 0) USDC")

                Button("Add $10") {
                    Task {
                        let session = try await manager.initiateFunding(
                            amount: 10.00,
                            currency: "USD",
                            destination: nil
                        )
                        // Present payment UI
                    }
                }
            }
        } else {
            Button("Sign In") {
                Task {
                    try await manager.sendOTPCode(to: phoneNumber)
                    // Show OTP input, then call loginWithOTP
                }
            }
        }
    }
}
```

## Next Steps

- [Architecture Guide](/docs/architecture) - Understand how it works
- [API Reference](/docs/api/classes/zerosettlemanager) - Full API documentation
