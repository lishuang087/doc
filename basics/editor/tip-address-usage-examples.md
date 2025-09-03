---
icon: '2'
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Tip Address Usage Examples

***

## <mark style="color:$success;">Functionality Overview</mark> <a href="#functionality-overview" id="functionality-overview"></a>

The system will check for the presence of our tip address in submitted transactions and will return an error if it's not found. This document provides an example of how to incorporate the tip address directly into your original transaction (recommended approach).

***

## <mark style="color:$success;">Implementation Steps</mark> <a href="#implementation-steps" id="implementation-steps"></a>

1. First, obtain a random tip address from the `/api/v2/randomTipAddress` endpoint
2. Include the tip transfer directly in your original transaction
3. Submit the single transaction with integrated tip to the batch submission endpoint

***

## <mark style="color:$success;">Code Example (Transfer Example)</mark> <a href="#code-example-transfer-example" id="code-example-transfer-example"></a>

{% code lineNumbers="true" %}
```javascript
// Step 1: Get a random tip address
async function createTransferWithTip(fromPrivateKey, toAddress, amountSOL) {
  try {
    // 1. Get a random tip address
    const tipAddressResponse = await fetch('https://ams.flashblock.trade/api/v2/randomTipAddress', {
      method: 'GET',
      headers: { 'Authorization': '7ebb9180244b50a47ca1993370dc4d5a' }
    });
    
    const tipData = await tipAddressResponse.json();
    if (!tipData.success) {
      throw new Error(`Failed to get tip address: ${tipData.message}`);
    }
    
    const tipAddress = tipData.data.tipAccount;
    
    // 2. Calculate amounts
    const mainLamports = Math.round(amountSOL * 1e9);
    const tipLamports = Math.round(mainLamports * 0.001); // 0.1% tip
    
    // 3. Create keypair from private key
    const payer = Keypair.fromSecretKey(bs58.decode(fromPrivateKey));
    const toPubkey = new PublicKey(toAddress);
    const tipPubkey = new PublicKey(tipAddress);
    
    // 4. Create transaction with both transfers
    const transaction = new Transaction()
      .add(
        SystemProgram.transfer({
          fromPubkey: payer.publicKey,
          toPubkey: toPubkey,
          lamports: mainLamports,
        })
      )
      .add(
        SystemProgram.transfer({
          fromPubkey: payer.publicKey,
          toPubkey: tipPubkey,
          lamports: tipLamports,
        })
      );
    
    // 5. Set recent blockhash
    const { blockhash } = await connection.getLatestBlockhash();
    transaction.recentBlockhash = blockhash;
    transaction.feePayer = payer.publicKey;
    
    // 6. Sign transaction
    transaction.sign(payer);
    
    // 7. Serialize to base64
    const serializedTransaction = transaction.serialize();
    const base64Transaction = Buffer.from(serializedTransaction).toString('base64');
    
    return base64Transaction;
  } catch (error) {
    console.error('Error creating transaction:', error);
    throw error;
  }
}

// Usage example
async function submitBatchTransactions(transactionsBase64) {
  try {
    const response = await fetch('http://ams.flashblock.trade/api/v2/submit-batch', {
      method: 'POST',
      headers: {
        'Authorization': '7ebb9180244b50a47ca1993370dc4d5a',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        transactions: transactionsBase64
      })
    });
    
    const result = await response.json();
    
    if (result.success) {
      console.log('Batch submitted successfully:', result.data);
      return result.data;
    } else {
      console.error(`Error: ${result.message} (Code: ${result.code})`);
      return null;
    }
  } catch (error) {
    console.error('API request failed:', error);
    throw error;
  }
}

// Usage example
const transactions = [
  "AaBU8zC90i...MAAAAAAAA=",
  "AaN9N7CCvi...MAAAAAAAA="
];

submitBatchTransactions(transactions)
  .then(result => {
    if (result) {
      console.log(`Batch ID: ${result.batch_id}`);
      result.results.forEach(tx => {
        console.log(`Transaction ${tx.txid}: ${tx.status}`);
      });
    }
  })
  .catch(err => {
    console.error('Failed to submit batch:', err);
  });
```
{% endcode %}

\
