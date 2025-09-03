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

# 自适应小费接口

***

## <mark style="color:$success;">API 信息</mark> <a href="#api-information" id="api-information"></a>

* **方法**: GET
* **URL**: `/api/v2/tip-floor`
* **基础 URL**: `https://api.flashblock.trade`
* **身份验证**: 不需要

***

## <mark style="color:$success;">请求示例</mark> <a href="#request-example" id="request-example"></a>

{% code lineNumbers="true" %}
```bash
curl https://api.flashblock.trade/api/v2/tip-floor
```
{% endcode %}

***

## <mark style="color:$success;">成功响应</mark> <a href="#successful-response" id="successful-response"></a>

{% code lineNumbers="true" %}
```json
{
  "tip": 0.0
}
```
{% endcode %}

***

## <mark style="color:$success;">响应说明</mark> <a href="#response-description" id="response-description"></a>

* `tip`: 基于当前网络条件的自适应小费金额
* 此值代表用于最佳交易处理的推荐小费金额
* 小费金额会根据网络拥堵和需求自动调整

***

## <mark style="color:$success;">使用说明</mark> <a href="#usage-notes" id="usage-notes"></a>

* 此端点不需要身份验证
* 返回的值是基于当前网络条件动态计算的
* 这有助于您设置适当的小费金额以获得最佳交易处理
* 该值由系统自动更新
