---
description: >-
  This guide will help you optimize your FlashBlock transactions, improve
  success rates, and reduce costs.
icon: '3'
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Transaction Optimization Guide

***

## <mark style="color:$success;">Transaction Optimization Strategies</mark> <a href="#transaction-optimization-strategies" id="transaction-optimization-strategies"></a>

### 1. Choose the Nearest Server Endpoint <a href="#id-1-choose-the-nearest-server-endpoint" id="id-1-choose-the-nearest-server-endpoint"></a>

Selecting the geographically closest server will provide the lowest latency:

* **North America Users**: Use `http://ny.flashblock.trade` or `http://slc.flashblock.trade`
* **Europe Users**: Use `http://ams.flashblock.trade` or `http://fra.flashblock.trade`
* **Other Regions**: Choose the best endpoint based on network latency tests

### 2. Optimize Tip Amount <a href="#id-2-optimize-tip-amount" id="id-2-optimize-tip-amount"></a>

The tip amount directly affects transaction priority:

* **Minimum Tip**: 0.001 SOL
* **Recommended Tip**: 0.001 - 0.01 SOL (adjust based on network congestion)
* **High Priority**: 0.01+ SOL (urgent transactions)

### 3. Monitor Network Status <a href="#id-4-monitor-network-status" id="id-4-monitor-network-status"></a>

Before sending transactions, check:

* Solana network status
* Current network congestion
* Average transaction confirmation time

### 4. Transaction Structure Optimization <a href="#id-5-transaction-structure-optimization" id="id-5-transaction-structure-optimization"></a>

**Correct Transaction Format**

{% code lineNumbers="true" %}
```json
{
  "transactions": [
    "base64_encoded_transaction_1",
    "base64_encoded_transaction_2"
  ]
}
```
{% endcode %}

**Tip Instruction Example**

{% code lineNumbers="true" %}
```javascript
// Add a tip transfer instruction to your transaction
const tipInstruction = SystemProgram.transfer({
  fromPubkey: wallet.publicKey,
  toPubkey: new PublicKey("FLaShB3iXXTWE1vu9wQsChUKq3HFtpMAhb8kAh1pf1wi"),
  lamports: 1000000 // 0.001 SOL
});
```
{% endcode %}

### 5. 🧪 Sandwich Mitigation Feature <a href="#id-6-sandwich-mitigation-feature" id="id-6-sandwich-mitigation-feature"></a>

We have introduced a new feature to help mitigate sandwich attacks—without the need for the vote account method.

<mark style="color:$success;">**How It Works**</mark>

In your Solana transaction, add any valid Solana public key that starts with `jitodontfront` to any instruction. For example:\
`jitodontfront1111111flashblockdottrade` or `jitodontfront1111111flashblockdottrade`

Any bundle containing a transaction with the `jitodontfront` account will be **rejected by the block engine** unless that transaction appears first (at index 0) in the bundle.

Transactions and bundles that do not contain this account are **not impacted** by this change.

**✅ Allowed bundle patterns:**

* `[tx_with_dont_front, tip]`
* `[tx_with_dont_front, arbitrage, tip]`

**❌ Disallowed bundle patterns:**

* `[tip, tx_with_dont_front]`
* `[txA_with_dont_front, txB_with_dont_front]`
* `[txA_with_dont_front, txB_with_dont_front, tip]`
* `[trade, tx_with_dont_front, arbitrage, tip]`

**📌 Important Points**

* The account **does not** need to exist on-chain but **must** be a valid public key
* Mark the account as **read-only** to optimize landing speed
* **(Optional)** Use a unique variation of `jitodontfront` for your application (use your own pubkey), for example:\
  `jitodontfront1111111flashblockdottradejitodontfront1111111flashblockdottrade`
* Supports **AddressLookupTables**

**📋 Example**

{% code lineNumbers="true" %}
```javascript
// Add the protection account to your transaction instruction
const dontFrontAccount = new PublicKey("jitodontfront1111111flashblockdottrade");

// Add to any instruction (recommended as read-only)
const protectedInstruction = {
  programId: yourProgramId,
  keys: [
    { pubkey: dontFrontAccount, isSigner: false, isWritable: false }, // read-only
    // ... other accounts
  ],
  data: instructionData
};
```
{% endcode %}

***

## <mark style="color:$success;">Performance Optimization Tips</mark> <a href="#performance-optimization-tips" id="performance-optimization-tips"></a>

### 1. Connection Optimization <a href="#id-1-connection-optimization" id="id-1-connection-optimization"></a>

* Use persistent HTTP connections
* Enable connection reuse
* Set reasonable timeout values
* Send a ping request every 30 seconds

### 2. Error Handling <a href="#id-2-error-handling" id="id-2-error-handling"></a>

{% code lineNumbers="true" %}
```javascript
try {
  const response = await fetch('http://ny.flashblock.trade/api/v2/submit-batch', {
    method: 'POST',
    headers: {
      'Authorization': authHeader,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ transactions: batch })
  });

  const result = await response.json();

  if (result.success) {
    console.log('Batch submitted successfully:', result.data);
  } else {
    console.error(`Error: ${result.message} (Code: ${result.code})`);
  }
} catch (error) {
  console.error('API request failed:', error);
  throw error;
}
```
{% endcode %}

***

## <mark style="color:$success;">Cost Optimization</mark> <a href="#cost-optimization" id="cost-optimization"></a>

&#x20; Tip Strategy

* Adjust the tip based on transaction urgency
* Use the minimum tip for non-urgent transactions
* Dynamically adjust based on network congestion

***

## <mark style="color:$success;">Troubleshooting</mark> <a href="#troubleshooting" id="troubleshooting"></a>

### 1. Transaction Failure <a href="#id-1-transaction-failure" id="id-1-transaction-failure"></a>

* Check if the tip is sufficient
* Verify transaction format
* Confirm network connection

### 2. High Latency <a href="#id-2-high-latency" id="id-2-high-latency"></a>

* Switch to a closer endpoint
* Increase the tip amount
* Check network status

### 3. High Cost <a href="#id-3-high-cost" id="id-3-high-cost"></a>

* Optimize batch size
* Adjust tip strategy
* Choose the appropriate time window

***

## <mark style="color:$success;">Best Practices Summary</mark> <a href="#best-practices-summary" id="best-practices-summary"></a>

1. **Always use the nearest server endpoint**
2. **Dynamically adjust the tip based on network status**
3. **Implement a reasonable retry mechanism**
4. **Monitor key performance indicators**
5. **Optimize transaction batch size**
6. **Maintain robust error handling in your code**

By following these optimization strategies, you will significantly improve transaction success rates, reduce latency, and optimize cost efficiency.
