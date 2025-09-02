---
description: >-
  FlashBlock provides a complete set of API interfaces for interacting with our
  services.
icon: arrows-to-circle
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

# API Documentation

***

## <mark style="color:$success;">API Basics</mark> <a href="#api-basics" id="api-basics"></a>

* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Most endpoints require API key (except tip-related endpoints)
* **Format**: All requests and responses use JSON format

***

## <mark style="color:$success;">Available Endpoints</mark> <a href="#available-endpoints" id="available-endpoints"></a>

1. Send Transaction
   * Submit transactions using JSON-RPC 2.0 or custom REST API format
2. Get Random Tip Address
   * Get system-generated random tip address
3. Get Priority Fee
   * Get current priority fee in lamports
4. Adaptive Tip
   * Get adaptive tip amount based on network conditions
5. Get Transaction Error Details
   * Query error details by transaction hash
6. Error Codes
   * Complete list of error codes and descriptions

***

## <mark style="color:$success;">Authentication</mark> <a href="#authentication" id="authentication"></a>

Most API requests require an API key in the request header:

{% code lineNumbers="true" %}
```
Authorization: YOUR_API_KEY
```
{% endcode %}

**Note**: Tip-related endpoints (`/api/v2/randomTipAddress`, `/api/v2/prioritizeTipping`, `/api/v2/tip-floor`) do not require authentication.

To obtain your API key, please send an email to support@flashblock.trade with your request.

***

## <mark style="color:$success;">Support</mark> <a href="#support" id="support"></a>

If you have any questions, please visit our [Support Page](../integrations/contact-us.md).
