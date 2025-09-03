---
description: >-
  This section contains detailed usage examples and best practices for the
  FlashBlock API.
icon: user-check
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

# Usage Examples

***

## <mark style="color:$success;">Documentation List</mark> <a href="#documentation-list" id="documentation-list"></a>

* [Tip Address Usage Examples](tip-address-usage-examples.md) - How to include tip address in transactions
* [Transaction Optimization Guide](transaction-optimization-guide.md) - Transaction optimization best practices

***

## <mark style="color:$success;">Quick Start</mark> <a href="#quick-start" id="quick-start"></a>

#### Basic Example <a href="#basic-example" id="basic-example"></a>

{% code lineNumbers="true" %}
```typescript
const url = "http://ny.flashblock.trade/api/v2/submit-batch";

const response = await axios.post(
    url,
    {
        transactions: [...base64Transactions],
    },
    {
        headers: {
            'Content-Type': 'application/json',
            Authorization: 'YOUR_API_KEY',
        },
    },
);
```
{% endcode %}

#### Advanced Example <a href="#advanced-example" id="advanced-example"></a>

{% code lineNumbers="true" %}
```typescript
const body = {
    id: 1,
    jsonrpc: "2.0",
    method: "sendBundle",
    params: [
        [...base64Transactions],
        {
            encoding: "base64",
        }
    ],
    mev: false,
};
```
{% endcode %}

***

## <mark style="color:$success;">Best Practices</mark> <a href="#best-practices" id="best-practices"></a>



1. **Error Handling**: Always implement appropriate error handling mechanisms
2. **Retry Strategy**: Use exponential backoff retry strategies
3. **Monitoring**: Monitor transaction status and error rates
4. **Optimization**: Adjust priority fees based on network conditions

For more detailed information, please refer to the individual example documents.
