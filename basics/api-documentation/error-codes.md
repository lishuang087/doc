---
icon: '6'
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

# Error-Codes

***

## <mark style="color:$success;">Error Codes Reference</mark> <a href="#error-codes-reference" id="error-codes-reference"></a>

| Error Code | Description                                         |
| ---------- | --------------------------------------------------- |
| 1001       | Batch validation error                              |
| 1002       | Invalid wallet address                              |
| 1003       | Insufficient funds                                  |
| 1004       | Network error                                       |
| 1005       | Invalid amount                                      |
| 1006       | Rate limit exceeded                                 |
| 1007       | Batch size exceeded                                 |
| 1008       | Transaction error                                   |
| 1009       | No authentication information in the request header |

***

## <mark style="color:$success;">Important Notes</mark> <a href="#important-notes" id="important-notes"></a>

1. Ensure that the `transactions` array includes at least one transaction to the tip address, or validation will fail
2. Transactions must be correctly encoded in base64 format
3. Batch submissions have quantity limits; exceeding these limits will result in error code 1007
4. Before submitting, ensure the wallet has sufficient funds to avoid error code 1003
5. Once submitted and confirmed, transactions cannot be reversed
6. The successful response will include a `bundleId` and a list of `transactionIds` for each transaction in the bundle
