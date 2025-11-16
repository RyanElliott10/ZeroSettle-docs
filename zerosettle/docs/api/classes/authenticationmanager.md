---
title: AuthenticationManager
---

# AuthenticationManager

Manages Privy authentication and wallet operations.

## Declaration

```swift
final class AuthenticationManager
```

## Overview

`AuthenticationManager` handles all authentication and wallet operations through Privy. It manages phone number authentication, embedded Solana wallet creation, and wallet operations.

This class conforms to `ObservableObject` and automatically publishes state changes for use with SwiftUI.

## Creating an Authentication Manager

### init(config:)

Creates a new AuthenticationManager with the specified configuration.

```swift
init(config: ZeroSettleConfig)
```

**Parameters:**
- `config`: The configuration object containing Privy app ID and settings

## Instance Properties

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

### currentUser

The current authenticated Privy user, if any.

```swift
var currentUser: PrivyUser?
```

Returns `nil` if no user is authenticated.

### walletAddress

The current user's Solana wallet address, if authenticated.

```swift
var walletAddress: String?
```

Returns `nil` if no user is authenticated or no wallet exists.

### solanaBalance

The current Solana balance as a Decimal.

```swift
var solanaBalance: Decimal
```

### delegate

Optional delegate for receiving authentication callbacks.

```swift
var delegate: ZeroSettleDelegate?
```

## Instance Methods

### initialize()

Call this to initialize Privy SDK (synchronous version).

```swift
func initialize()
```

**Note:** Must run on MainActor as Privy may present web views.

Call this method when your app starts, typically in the `App`'s `task` modifier.

### initializeInBackground()

Initialize Privy completely in background, only update UI on main thread when ready.

```swift
func initializeInBackground() async
```

### checkAuthState()

Check the user's current authentication state.

```swift
func checkAuthState() async
```

### hasAuthenticatedUser()

Check if a user is currently cached inside Privy.

```swift
func hasAuthenticatedUser() async -> Bool
```

**Returns:** `true` if a user is cached, `false` otherwise

### sendOTPCode(to:)

Step 1: Send OTP code to phone number.

```swift
func sendOTPCode(to phoneNumber: String) async throws
```

**Parameters:**
- `phoneNumber`: The phone number to send the OTP to (E.164 format recommended)

**Throws:** `AuthenticationError` if the request fails

### loginWithOTP(code:phoneNumber:)

Step 2: Verify OTP and login.

```swift
func loginWithOTP(code: String, phoneNumber: String) async throws
```

**Parameters:**
- `code`: The OTP code received via SMS
- `phoneNumber`: The phone number that received the OTP

**Throws:** `AuthenticationError` if verification fails

### logout()

Logout from Privy and clear all session data.

```swift
func logout() async
```

### createSolanaWallet(allowAdditional:)

Create an embedded Solana wallet for the authenticated user.

```swift
func createSolanaWallet(allowAdditional: Bool) async throws -> EmbeddedSolanaWallet
```

**Parameters:**
- `allowAdditional`: Whether to allow creating additional wallets

**Returns:** The created embedded Solana wallet

**Throws:** Errors if wallet creation fails

### getSolanaWallets()

Get the user's embedded Solana wallets.

```swift
func getSolanaWallets() -> [EmbeddedSolanaWallet]
```

**Returns:** Array of embedded Solana wallets

### sendTransaction(_:)

Sign and send a Solana transaction.

```swift
func sendTransaction(_ transaction: String) async throws -> String
```

**Parameters:**
- `transaction`: The base64-encoded transaction to send

**Returns:** The transaction signature

**Throws:** Errors if transaction fails

### signTransaction(_:)

Sign a Solana transaction (alias to sendTransaction for compatibility).

```swift
func signTransaction(_ transaction: String) async throws -> String
```

**Parameters:**
- `transaction`: The base64-encoded transaction to sign

**Returns:** The transaction signature

### signMessage(_:)

Sign a message with the user's Solana wallet.

```swift
func signMessage(_ message: String) async throws -> String
```

**Parameters:**
- `message`: The message to sign

**Returns:** The signature as a hex string

### formatWalletAddress(_:)

Format wallet address for display (shortened).

```swift
func formatWalletAddress(_ address: String) -> String
```

**Parameters:**
- `address`: The full wallet address

**Returns:** A shortened version suitable for display (e.g., "0x1234...5678")

### formattedSolanaBalance()

Get formatted Solana balance string.

```swift
func formattedSolanaBalance() -> String
```

**Returns:** Formatted balance string

### getPrivyInstance()

Get the Privy instance (use with caution, prefer using manager methods).

```swift
func getPrivyInstance() -> Privy?
```

**Returns:** The Privy instance if initialized

## See Also

- [ZeroSettleManager](/docs/api/classes/zerosettlemanager)
- [ZeroSettleConfig](/docs/api/structures/zerosettleconfig)
- [Architecture](/docs/architecture)
