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

# 随机小费地址接口

***

## <mark style="color:$success;">API 信息</mark> <a href="#api-information" id="api-information"></a>

* **方法**: GET
* **URL**: `/api/v2/randomTipAddress`
* **基础 URL**: `https://api.flashblock.trade`
* **身份验证**: 不需要

***

## <mark style="color:$success;">请求示例</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/randomTipAddress
```
{% endcode %}

***

## <mark style="color:$success;">成功响应</mark> <a href="#successful-response" id="successful-response"></a>

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

***

## <mark style="color:$success;">错误响应</mark> <a href="#error-response" id="error-response"></a>

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

***

## <mark style="color:$success;">使用说明</mark> <a href="#usage-notes" id="usage-notes"></a>

* 此端点返回一个随机选择的小费钱包地址
* 返回的地址应作为小费转账包含在您的交易中
* 此端点不需要身份验证
