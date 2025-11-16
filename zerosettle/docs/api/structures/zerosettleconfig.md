---
title: ZeroSettleConfig
---

# ZeroSettleConfig

Configuration for ZeroSettleKit.

## Declaration

```swift
struct ZeroSettleConfig
```

## Overview

`ZeroSettleConfig` contains all the configuration settings needed to initialize `ZeroSettleManager`. This includes API keys, network settings, and customization options.

## Instance Properties

### privyAppId

Your Privy application ID.

```swift
let privyAppId: String
```

Get your Privy App ID from the [Privy Dashboard](https://dashboard.privy.io).

### privyClientId

Your Privy client ID.

```swift
let privyClientId: String
```

### supportedChains

The blockchain networks supported by your application.

```swift
let supportedChains: [BlockchainNetwork]
```

Defaults to `[.solana]`.

### paymentProcessor

The payment processor to use for fiat onramp.

```swift
let paymentProcessor: PaymentProcessor
```

Defaults to `CoinbasePaymentProcessor`.

### defaultNetwork

The default blockchain network to use.

```swift
let defaultNetwork: BlockchainNetwork
```

Defaults to `.solana`.

### rpcEndpoints

RPC endpoints for each supported network.

```swift
let rpcEndpoints: [BlockchainNetwork: String]
```

Provide custom RPC URLs if you want to use your own infrastructure.

### theme

Optional theme configuration for UI components.

```swift
let theme: ZeroSettleTheme?
```

### defaultFundingAmounts

Default funding amounts to display in the UI (in cents/smallest unit).

```swift
let defaultFundingAmounts: [Int]
```

Defaults to `[1000, 2500, 5000, 10000]` (representing $10, $25, $50, $100).

### apiBaseURL

Base URL for ZeroSettle partner API calls.

```swift
let apiBaseURL: URL
```

### partnerAppId

Partner app identifier for payout configuration.

```swift
let partnerAppId: Int
```

Defaults to `2` (WordPlay).

### partnerAuthTokenProvider

Optional provider for partner session tokens to authorize API calls.

```swift
let partnerAuthTokenProvider: (() -> String?)?
```

## Example

```swift
let config = ZeroSettleConfig(
    privyAppId: "your-privy-app-id",
    privyClientId: "your-privy-client-id",
    supportedChains: [.solana, .base],
    paymentProcessor: CoinbasePaymentProcessor(),
    defaultNetwork: .solana,
    rpcEndpoints: [:],  // Use defaults
    theme: nil,          // Use default theme
    defaultFundingAmounts: [1000, 2500, 5000],
    apiBaseURL: URL(string: "https://api.zerosettle.com")!,
    partnerAppId: 2,
    partnerAuthTokenProvider: nil
)
```

## See Also

- [ZeroSettleManager](/docs/api/classes/zerosettlemanager)
- [Getting Started](/docs/getting-started)
