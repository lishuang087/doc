---
icon: '5'
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

# Get Transaction Error Details

***

## <mark style="color:$success;">API Information</mark> <a href="#api-information" id="api-information"></a>

* **Method**: GET
* **URL**: `/api/v1/tx/error-details/{tx_hash}`
* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Not required

## <mark style="color:$success;">Request Example</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
# Replace {tx_hash} with the actual transaction hash you want to query
curl https://api.flashblock.trade/api/v1/tx/error-details/{tx_hash}
```
{% endcode %}

## <mark style="color:$success;">Parameter Description</mark> <a href="#parameter-description" id="parameter-description"></a>

* `{tx_hash}`: The transaction hash you want to query for error details

## <mark style="color:$success;">Successful Response</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "success": true,
  "code": 200,
  "message": [
    "Transaction failed: Transaction is not recent"
  ]
}
```
{% endcode %}

## <mark style="color:$success;">Error Response</mark> <a href="#error-response" id="error-response"></a>

{% code lineNumbers="true" %}
```json
{
  "success": false,
  "code": 500,
  "message": "Transaction not found"
}
```
{% endcode %}

## <mark style="color:$success;">Response Description</mark> <a href="#response-description" id="response-description"></a>

* `success`: Boolean indicating if the query was successful
* `code`: HTTP status code (200 for success, 500 for error)
* `message`: Array of error messages (for successful queries) or error description (for failed queries)

## <mark style="color:$success;">Usage Notes</mark> <a href="#usage-notes" id="usage-notes"></a>

* No authentication is required for this endpoint
* The endpoint returns detailed error information for failed transactions
* If the transaction is not found, it will return a 500 error
* The error messages array may contain multiple error details
