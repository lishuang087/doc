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

# 优先级费用接口

***

## <mark style="color:$success;">API 信息</mark> <a href="#api-information" id="api-information"></a>

* **方法**: GET
* **URL**: `/api/v2/prioritizeTipping`
* **基础 URL**: `https://api.flashblock.trade`
* **身份验证**: 不需要

***

## <mark style="color:$success;">请求示例</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/prioritizeTipping
```
{% endcode %}

***

## <mark style="color:$success;">成功响应</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "priority_fee_lamports": 0
}
```
{% endcode %}

***

## <mark style="color:$success;">响应说明</mark> <a href="#response-description" id="response-description"></a>

* `priority_fee_lamports`: 当前 lamports 中的优先级费用
* 此值由后台任务定期更新
* 使用此值为您的交易设置适当的优先级费用

***

## <mark style="color:$success;">使用说明</mark> <a href="#usage-notes" id="usage-notes"></a>

* 此端点不需要身份验证
* 返回的值代表当前推荐的优先级费用
* 此费用有助于确保您的交易以更高优先级处理
* 该值由系统自动更新
