---
title: ZeroSettleManager
---

# ZeroSettleManager

Main manager that coordinates authentication, funding, and wallet operations.

## Declaration

```swift
@MainActor
class ZeroSettleManager
```

## Overview

`ZeroSettleManager` is the primary interface for interacting with the ZeroSettleKit framework. It coordinates authentication, payment processing, and wallet operations, providing a unified API for your application.

This class conforms to `ObservableObject`, making it perfect for use with SwiftUI. All state changes are published automatically, allowing your UI to reactively update when authentication status, balances, or other properties change.

## Creating a Manager

### init(config:)

Creates a new ZeroSettleManager with the specified configuration.

```swift
init(config: ZeroSettleConfig)
```

**Parameters:**
- `config`: The configuration object containing API keys and settings

**Example:**

```swift
let config = ZeroSettleConfig(
    privyAppId: "your-privy-app-id",
    coinbaseApiKey: "your-coinbase-api-key",
    environment: .sandbox
)

let manager = ZeroSettleManager(config: config)
```

## Instance Properties

### config

The configuration object.

```swift
let config: ZeroSettleConfig
```

### authManager

The authentication manager instance.

```swift
let authManager: AuthenticationManager
```

### isInitialized

Whether the manager has completed initialization.

```swift
var isInitialized: Bool
```

This property is `@Published` and can be observed in SwiftUI views.

### isAuthenticated

Whether a user is currently authenticated.

```swift
var isAuthenticated: Bool
```

This property is `@Published` and updates automatically when authentication state changes.

###wallet Address

The current user's wallet address, if authenticated.

```swift
var walletAddress: String?
```

Returns `nil` if no user is authenticated.

### balances

Current token balances by token type.

```swift
var balances: [TokenType: Decimal]
```

This dictionary contains balance information for each supported token type (e.g., USDC, SOL).

### pendingTransactions

Array of pending transaction hashes.

```swift
var pendingTransactions: [String]
```

Automatically updated as transactions are submitted and confirmed.

### delegate

Optional delegate for receiving callbacks.

```swift
var delegate: ZeroSettleDelegate?
```

## Instance Methods

### initialize()

Initializes the manager and underlying services.

```swift
func initialize() async
```

Call this method when your app starts, typically in the `App`'s `task` modifier:

```swift
.task {
    await manager.initialize()
}
```

### sendOTPCode(to:)

Sends a one-time password to the specified phone number.

```swift
func sendOTPCode(to phoneNumber: String) async throws
```

**Parameters:**
- `phoneNumber`: The phone number to send the OTP to (E.164 format recommended)

**Throws:** `AuthenticationError` if the request fails

**Example:**

```swift
do {
    try await manager.sendOTPCode(to: "+14155551234")
    // Show OTP input UI
} catch {
    // Handle error
}
```

### loginWithOTP(code:phoneNumber:)

Verifies the OTP code and completes authentication.

```swift
func loginWithOTP(code: String, phoneNumber: String) async throws
```

**Parameters:**
- `code`: The OTP code received via SMS
- `phoneNumber`: The phone number that received the OTP

**Throws:** `AuthenticationError` if verification fails

**Example:**

```swift
try await manager.loginWithOTP(code: "123456", phoneNumber: "+14155551234")
// User is now authenticated
```

### logout()

Logs out the current user.

```swift
func logout() async
```

Clears authentication state and removes cached data.

### initiateFunding(amount:currency:destination:)

Initiates a funding transaction to add funds to a wallet.

```swift
func initiateFunding(
    amount: Decimal,
    currency: String,
    destination: String?
) async throws -> FundingSession
```

**Parameters:**
- `amount`: The amount to fund
- `currency`: The currency code (e.g., "USD")
- `destination`: Optional destination wallet address (defaults to current user's wallet)

**Returns:** A `FundingSession` that can be used to monitor payment status

**Example:**

```swift
let session = try await manager.initiateFunding(
    amount: 10.00,
    currency: "USD",
    destination: nil
)

// Monitor the session...
```

### sendTransaction(_:)

Sends a prepared transaction to the blockchain.

```swift
func sendTransaction(_ transaction: PreparedTransaction) async throws -> String
```

**Parameters:**
- `transaction`: The prepared transaction to send

**Returns:** The transaction hash

**Throws:** Transaction errors if sending fails

### signMessage(_:)

Signs a message with the user's wallet.

```swift
func signMessage(_ message: String) async throws -> String
```

**Parameters:**
- `message`: The message to sign

**Returns:** The signature as a hex string

### monitorTransaction(_:)

Monitors a transaction until it's confirmed.

```swift
func monitorTransaction(_ hash: String)
```

**Parameters:**
- `hash`: The transaction hash to monitor

Automatically adds the transaction to `pendingTransactions` and removes it when confirmed.

### handlePaymentCompletion(success:amount:transactionHash:)

Handles a payment completion event from the payment processor.

```swift
func handlePaymentCompletion(
    success: Bool,
    amount: Decimal,
    transactionHash: String?
)
```

**Parameters:**
- `success`: Whether the payment succeeded
- `amount`: The payment amount
- `transactionHash`: Optional transaction hash

This method is typically called internally by payment processors.

### fetchLatestPayoutTable()

Fetches the latest configured payout table for the current partner app.

```swift
func fetchLatestPayoutTable() async throws -> ZeroSettlePayoutTable
```

**Returns:** The latest payout table configuration

**Throws:** Network or configuration errors

### formatAddress(_:)

Formats a wallet address for display (shortens to first/last characters).

```swift
func formatAddress(_ address: String) -> String
```

**Parameters:**
- `address`: The full wallet address

**Returns:** A shortened version suitable for display (e.g., "0x1234...5678")

## See Also

- [ZeroSettleConfig](/docs/api/structures/zerosettleconfig)
- [ZeroSettleDelegate](/docs/api/protocols/zerosettledelegate)
- [AuthenticationManager](/docs/api/classes/authenticationmanager)
- [Architecture Guide](/docs/architecture)
