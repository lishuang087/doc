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

# 交易错误详情接口

***

## <mark style="color:$success;">API 信息</mark> <a href="#api-information" id="api-information"></a>

* **Method**: GET
* **URL**: `/api/v1/tx/error-details/{tx_hash}`
* **Base URL**: `https://api.flashblock.trade`
* **Authentication**: Not required

***

## <mark style="color:$success;">请求示例</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
# Replace {tx_hash} with the actual transaction hash you want to query
curl https://api.flashblock.trade/api/v1/tx/error-details/{tx_hash}
```
{% endcode %}

***

## <mark style="color:$success;">参数说明</mark> <a href="#parameter-description" id="parameter-description"></a>

* `{tx_hash}`: The transaction hash you want to query for error details

***

## <mark style="color:$success;">成功响应</mark> <a href="#successful-response" id="successful-response"></a>

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

***

## <mark style="color:$success;">错误响应</mark> <a href="#error-response" id="error-response"></a>

{% code lineNumbers="true" %}
```json
{
  "success": false,
  "code": 500,
  "message": "Transaction not found"
}
```
{% endcode %}

***

## <mark style="color:$success;">响应说明</mark> <a href="#response-description" id="response-description"></a>

* `success`: 布尔值，表示查询是否成功
* `code`: HTTP 状态码（200 表示成功，500 表示错误）
* `message`: 错误消息数组（成功查询时）或错误描述（失败查询时）

***

## <mark style="color:$success;">使用说明</mark> <a href="#usage-notes" id="usage-notes"></a>

* 此端点不需要身份验证
* 端点返回失败交易的详细错误信息
* 如果未找到交易，将返回 500 错误
* 错误消息数组可能包含多个错误详情
