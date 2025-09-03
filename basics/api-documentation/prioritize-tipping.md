---
icon: '3'
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

# Prioritize-Tipping

***

## <mark style="color:$success;">API Information</mark> <a href="#api-information" id="api-information"></a>

* **Method**: GET
* **URL**: `/api/v2/prioritizeTipping`
* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Not required

## <mark style="color:$success;">Request Example</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/prioritizeTipping
```
{% endcode %}

## <mark style="color:$success;">Successful Response</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "priority_fee_lamports": 0
}
```
{% endcode %}

## <mark style="color:$success;">Response Description</mark> <a href="#response-description" id="response-description"></a>

* `priority_fee_lamports`: Current priority fee in lamports
* This value is updated periodically by background tasks
* Use this value to set appropriate priority fees for your transactions

## <mark style="color:$success;">Usage Notes</mark> <a href="#usage-notes" id="usage-notes"></a>

* No authentication is required for this endpoint
* The returned value represents the current recommended priority fee
* This fee helps ensure your transactions are processed with higher priority
* The value is updated automatically by the system
