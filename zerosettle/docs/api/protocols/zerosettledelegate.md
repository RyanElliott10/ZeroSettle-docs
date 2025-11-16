---
title: ZeroSettleDelegate
---

# ZeroSettleDelegate

Delegate protocol for ZeroSettle events.

## Declaration

```swift
protocol ZeroSettleDelegate : AnyObject
```

## Overview

`ZeroSettleDelegate` provides callbacks for important events in the ZeroSettleKit framework, such as authentication, funding, and transaction events. All methods have default implementations, so you only need to implement the methods you care about.

## Instance Methods

### didAuthenticate(userId:wallet:)

Called when user successfully authenticates.

```swift
func didAuthenticate(userId: String, wallet: WalletInfo)
```

**Parameters:**
- `userId`: The authenticated user's ID
- `wallet`: Information about the user's wallet

### didLogout()

Called when user logs out.

```swift
func didLogout()
```

### didInitiateFunding(amount:currency:)

Called when user initiates a funding transaction.

```swift
func didInitiateFunding(amount: Decimal, currency: String)
```

**Parameters:**
- `amount`: The funding amount
- `currency`: The currency code

### didCompleteFunding(amount:currency:transactionHash:)

Called when funding completes successfully.

```swift
func didCompleteFunding(amount: Decimal, currency: String, transactionHash: String?)
```

**Parameters:**
- `amount`: The funded amount
- `currency`: The currency code
- `transactionHash`: Optional transaction hash

### didFailFunding(error:)

Called when funding fails.

```swift
func didFailFunding(error: Error)
```

**Parameters:**
- `error`: The error that occurred

### willSendTransaction(transaction:)

Called before sending a transaction.

```swift
func willSendTransaction(transaction: PreparedTransaction)
```

**Parameters:**
- `transaction`: The prepared transaction about to be sent

### didSendTransaction(txHash:)

Called when transaction is successfully sent.

```swift
func didSendTransaction(txHash: String)
```

**Parameters:**
- `txHash`: The transaction hash

### didConfirmTransaction(txHash:receipt:)

Called when transaction is confirmed on-chain.

```swift
func didConfirmTransaction(txHash: String, receipt: TransactionReceipt)
```

**Parameters:**
- `txHash`: The transaction hash
- `receipt`: The transaction receipt

### didFailTransaction(error:)

Called when transaction fails.

```swift
func didFailTransaction(error: Error)
```

**Parameters:**
- `error`: The error that occurred

## Example Usage

```swift
class MyDelegate: ZeroSettleDelegate {
    func didAuthenticate(userId: String, wallet: WalletInfo) {
        print("User \(userId) authenticated with wallet \(wallet.address)")
    }

    func didCompleteFunding(amount: Decimal, currency: String, transactionHash: String?) {
        print("Funding complete: \(amount) \(currency)")
    }
}

let delegate = MyDelegate()
manager.delegate = delegate
```

## See Also

- [ZeroSettleManager](/docs/api/classes/zerosettlemanager)
- [WalletInfo](/docs/api/structures/walletinfo)
- [PreparedTransaction](/docs/api/structures/preparedtransaction)
- [TransactionReceipt](/docs/api/structures/transactionreceipt)
