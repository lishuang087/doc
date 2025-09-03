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

# 发送交易接口

***

## <mark style="color:$success;">概述</mark> <a href="#overview" id="overview"></a>

发送交易 API 提供两种格式用于提交 Solana 交易：标准的 JSON-RPC 2.0 格式和自定义的 REST API 格式。

***

## <mark style="color:$success;">服务信息</mark> <a href="#service-information" id="service-information"></a>

* **基础 URL**: `http://ams.flashblock.trade`
* **认证方式**: 需要 Authorization Header
* **协议**: HTTP/HTTPS

***

## <mark style="color:$success;">API 端点</mark> <a href="#api-endpoints" id="api-endpoints"></a>

### <mark style="color:blue;">1. JSON-RPC 交易提交</mark> <a href="#id-1-json-rpc-transaction-submission" id="id-1-json-rpc-transaction-submission"></a>

POST/

使用 JSON-RPC 2.0 规范提交交易。

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

**请求参数说明:**

* `jsonrpc`: 固定值 "2.0"
* `id`: 请求ID，用于匹配响应
* `method`: 固定值 "sendBundle"
* `params`: 参数数组
  * `params[0]`: base64 编码的交易数组
  * `params[1]`: 编码配置对象
    * `encoding`: 编码格式，固定为 "base64"

&#x20;**请求头：**

{% code lineNumbers="true" %}
```
Content-Type: application/json
Authorization: YOUR_API_KEY
```
{% endcode %}

**成功响应：**

{% code lineNumbers="true" %}
```json
{
  "jsonrpc": "2.0",
  "result": "5XHA7ofPAf3FaLUAY3kT52c...",
  "id": 1
}
```
{% endcode %}

**错误响应：**

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

**错误码说明**:

* `-1009`: 缺少或无效的 Authorization 头
* `-1010`: 交易长度过短或不符合要求
* `-1013`: Bundle 方法设置错误，需要 sendBundle

***

### <mark style="color:blue;">2. 自定义 REST API 交易提交</mark> <a href="#id-2-zi-ding-yi-restapi-jiao-yi-ti-jiao" id="id-2-zi-ding-yi-restapi-jiao-yi-ti-jiao"></a>

**POST /api/v2/submit-batch**

使用自定义 REST API 格式提交交易。

**请求格式**:

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

**请求参数说明**:

* `transactions`: Array of base64-encoded transactions (optional, defaults to empty array)

**请求头**:

{% code lineNumbers="true" %}
```
Content-Type: application/json
Authorization: YOUR_API_KEY
```
{% endcode %}

**成功响应**:

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

**错误响应**:

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

**错误码说明**:

* `1009`: 缺少或无效的 Authorization 头
* `1010`: 交易长度过短或不符合要求

***

## <mark style="color:$success;">交易限制</mark> <a href="#transaction-limits" id="transaction-limits"></a>

* **最大交易数**: 单次提交最多 4 笔交易
* **交易格式**: 所有交易必须是有效的 base64 编码
* **最小小费**: 每笔交易必须包含至少 0.001 SOL 的小费

***

## <mark style="color:$success;">最佳实践</mark> <a href="#best-practices" id="best-practices"></a>

### 小费集成建议 <a href="#xiao-fei-ji-cheng-jian-yi" id="xiao-fei-ji-cheng-jian-yi"></a>

**建议直接在原交易中包含小费，而不是创建单独的小费交易，无论交易数量多少。** 这种方式：

* 减少交易数量和复杂度
* 提高交易成功率
* 最小化 gas 成本
* 提供更好的原子性
* 确保一致的交易排序

***

## <mark style="color:$success;">示例代码</mark> <a href="#example-code" id="example-code"></a>

#### JavaScript/Node.js <a href="#javascript-node-js" id="javascript-node-js"></a>

**JSON-RPC 格式**

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

**自定义 API 格式**

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

**JSON-RPC 格式**

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
    
    return response.json()z格式 API Format
```
{% endcode %}

**自定义 API 格式**

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
