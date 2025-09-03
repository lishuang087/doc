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

# Random-Tip-Address

***

## <mark style="color:$success;">API Information</mark> <a href="#api-information" id="api-information"></a>

* **Method**: GET
* **URL**: `/api/v2/randomTipAddress`
* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Not required

## <mark style="color:$success;">Request Example</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/randomTipAddress
```
{% endcode %}

## <mark style="color:$success;">Successful Response</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "success": true,
  "code": 200,
  "data": {
    "tip_account": "FLaShB3iXXTWE1vu9wQsChUKq3HFtpMAhb8kAh1pf1wi"
  },
  "message": "success"
}
```
{% endcode %}

## <mark style="color:$success;">Error Response</mark> <a href="#error-response" id="error-response"></a>

{% code lineNumbers="true" %}
```json
{
  "success": false,
  "code": 1007,
  "data": [],
  "message": "Batch size exceeded"
}
```
{% endcode %}

## <mark style="color:$success;">Usage Notes</mark> <a href="#usage-notes" id="usage-notes"></a>

* This endpoint returns a randomly selected tip wallet address
* The returned address should be included in your transaction as a tip transfer
* No authentication is required for this endpoint
