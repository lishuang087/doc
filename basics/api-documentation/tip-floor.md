---
icon: '4'
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

# Tip-Floor

***

## <mark style="color:$success;">API Information</mark> <a href="#api-information" id="api-information"></a>

* **Method**: GET
* **URL**: `/api/v2/tip-floor`
* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Not required

***

## <mark style="color:$success;">Request Example</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/tip-floor
```
{% endcode %}

***

## <mark style="color:$success;">Successful Response</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "tip": 0.0
}
```
{% endcode %}

***

## <mark style="color:$success;">Response Description</mark> <a href="#response-description" id="response-description"></a>

* `tip`: The adaptive tip amount based on current network conditions
* This value represents the recommended tip amount for optimal transaction processing
* The tip amount automatically adjusts based on network congestion and demand

***

## <mark style="color:$success;">Usage Notes</mark> <a href="#usage-notes" id="usage-notes"></a>

* No authentication is required for this endpoint
* The returned value is dynamically calculated based on current network conditions
* This helps you set appropriate tip amounts for optimal transaction processing
* The value is updated automatically by the system
