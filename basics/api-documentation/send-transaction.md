---
icon: '1'
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

# Send-Transaction

***

## <mark style="color:$success;">Overview</mark> <a href="#overview" id="overview"></a>

The Send Transaction API provides two formats for submitting Solana transactions: standard JSON-RPC 2.0 format and custom REST API format.

***

## <mark style="color:$success;">Service Information</mark> <a href="#service-information" id="service-information"></a>

* **Base URL**: `http://ams.flashblock.trade`
* **Authentication**: Authorization Header required
* **Protocol**: HTTP/HTTPS

***

## <mark style="color:$success;">API Endpoints</mark> <a href="#api-endpoints" id="api-endpoints"></a>

### <mark style="color:blue;">1. JSON-RPC Transaction Submission</mark> <a href="#id-1-json-rpc-transaction-submission" id="id-1-json-rpc-transaction-submission"></a>

**POST /**

Submit transactions using JSON-RPC 2.0 specification.

**Request Format**:

{% code lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "sendBundle",
  "params": [
    [
      "base64_encoded_transaction_1",
      "base64_encoded_transaction_2"
    ],
    {
      "encoding": "base64"
    }
  ]
}
```
{% endcode %}

**Request Parameters**:

* `jsonrpc`: Fixed value "2.0"
* `id`: Request ID for response matching
* `method`: Fixed value "sendBundle"
* `params`: Parameter array
  * `params[0]`: Array of base64-encoded transactions
  * `params[1]`: Encoding configuration object
    * `encoding`: Encoding format, fixed as "base64"

**Request Headers**:

{% code lineNumbers="true" %}
```
Content-Type: application/json
Authorization: YOUR_API_KEY
```
{% endcode %}

**Success Response**:

{% code lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "result": "5XHA7ofPAf3FaLUAY3kT52c...",
  "id": 1
}
```
{% endcode %}

**Error Response**:

{% code lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "error": {
    "code": -1009,
    "message": "Missing or invalid Authorization header",
    "data": null
  },
  "id": null
}
```
{% endcode %}

**Error Codes**:

* `-1009`: Missing or invalid Authorization header
* `-1010`: Transaction length too short or doesn't meet requirements
* `-1013`: Bundle method setting error, requires sendBundle

***

### <mark style="color:blue;">2. Custom REST API Transaction Submission</mark> <a href="#id-2-custom-rest-api-transaction-submission" id="id-2-custom-rest-api-transaction-submission"></a>

**POST /api/v2/submit-batch**

Submit transactions using custom REST API format.

**Request Format**:

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

**Request Parameters**:

* `transactions`: Array of base64-encoded transactions (optional, defaults to empty array)

**Request Headers**:

{% code lineNumbers="true" %}
```
Content-Type: application/json
Authorization: YOUR_API_KEY
```
{% endcode %}

**Success Response**:

{% code lineNumbers="true" %}
```json
{
  "success": true,
  "code": 200,
  "message": "The transaction was submitted successfully, but the status of the transaction is pending.",
  "data": {
    "signatures": [
      "5XHA7ofPAf3FaLUAY3kT52c...",
      "4cmupyS9kyiEbfsW8kZkyEh..."
    ]
  }
}
```
{% endcode %}

**Error Response**:

{% code lineNumbers="true" %}
```json
{
  "success": false,
  "code": 1009,
  "message": "Missing or invalid Authorization header",
  "data": {
    "signatures": []
  }
}
```
{% endcode %}

**Error Codes**:

* `1009`: Missing or invalid Authorization header
* `1010`: Transaction length too short or doesn't meet requirements

***

## <mark style="color:$success;">Transaction Limits</mark> <a href="#transaction-limits" id="transaction-limits"></a>

* **Maximum Transactions**: 4 transactions per submission
* **Transaction Format**: All transactions must be valid base64 encoded
* **Minimum Tip**: Each transaction must include at least 0.001 SOL tip

***

## <mark style="color:$success;">Best Practices</mark> <a href="#best-practices" id="best-practices"></a>

Tip Integration Recommendation

**It's recommended to include the tip directly in the original transaction rather than creating a separate tip transaction, regardless of the number of transactions.** This approach:

* Reduces transaction count and complexity
* Improves transaction success rate
* Minimizes gas costs
* Provides better atomicity
* Ensures consistent transaction ordering

***

## <mark style="color:$success;">Example Code</mark> <a href="#example-code" id="example-code"></a>

#### JavaScript/Node.js <a href="#javascript-node-js" id="javascript-node-js"></a>

**JSON-RPC Format**

{% code lineNumbers="true" %}
```javascript
const axios = require('axios');

async function submitTransactionRPC(transactions, apiKey) {
  const payload = {
    jsonrpc: "2.0",
    id: 1,
    method: "sendBundle",
    params: [
      transactions,
      { encoding: "base64" }
    ]
  };

  const response = await axios.post('http://ams.flashblock.trade/', payload, {
    headers: {
      'Content-Type': 'application/json',
      'Authorization': apiKey
    }
  });

  return response.data;
}
```
{% endcode %}

**Custom API Format**

{% code lineNumbers="true" %}
```javascript
async function submitTransactionAPI(transactions, apiKey) {
  const payload = {
    transactions: transactions
  };

  const response = await axios.post('http://ams.flashblock.trade/api/v2/submit-batch', payload, {
    headers: {
      'Content-Type': 'application/json',
      'Authorization': apiKey
    }
  });

  return response.data;
}
```
{% endcode %}

#### Python <a href="#python" id="python"></a>

**JSON-RPC Format**

{% code lineNumbers="true" %}
```python
import requests

def submit_transaction_rpc(transactions, api_key):
    payload = {
        "jsonrpc": "2.0",
        "id": 1,
        "method": "sendBundle",
        "params": [
            transactions,
            {"encoding": "base64"}
        ]
    }
    
    headers = {
        'Content-Type': 'application/json',
        'Authorization': api_key
    }
    
    response = requests.post('http://ams.flashblock.trade/', 
                           json=payload, 
                           headers=headers)
    
    return response.json()
```
{% endcode %}

**Custom API Format**

{% code lineNumbers="true" %}
```python
def submit_transaction_api(transactions, api_key):
    payload = {
        "transactions": transactions
    }
    
    headers = {
        'Content-Type': 'application/json',
        'Authorization': api_key
    }
    
    response = requests.post('http://ams.flashblock.trade/api/v2/submit-batch', 
                           json=payload, 
                           headers=headers)
    
    return response.json()
```
{% endcode %}
