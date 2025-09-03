---
description: FlashBlock 提供了一套完整的 API 接口，用于与我们的服务进行交互。
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

# API 接口

***

## <mark style="color:$success;">API 基础</mark> <a href="#api-basics" id="api-basics"></a>

* **基础 URL**: `https://api.flashblock.trade`
* **身份验证**: 大多数端点需要 API 密钥（小费相关端点除外）
* **格式**: 所有请求和响应都使用 JSON 格式

***

## <mark style="color:$success;">可用端点</mark> <a href="#available-endpoints" id="available-endpoints"></a>

1. 发送交易接口
   * 使用 JSON-RPC 2.0 或自定义 REST API 格式提交交易
2. 获取随机小费地址
   * 获取系统生成的随机小费地址
3. 获取优先级费用
   * 获取当前 lamports 中的优先级费用
4. 自适应小费
   * 根据网络条件获取自适应小费金额
5. 获取交易错误详情
   * 通过交易哈希查询错误详情
6. 错误代码
   * 完整的错误代码和描述列表

***

## <mark style="color:$success;">身份验证</mark> <a href="#authentication" id="authentication"></a>

大多数 API 请求需要在请求头中包含 API 密钥：

{% code lineNumbers="true" %}
```
Authorization: YOUR_API_KEY
```
{% endcode %}

**注意**: 小费相关端点（`/api/v2/randomTipAddress`、`/api/v2/prioritizeTipping`、`/api/v2/tip-floor`）不需要身份验证。

要获取您的 API 密钥，请发送邮件至 support@flashblock.trade 并说明您的需求。

***

## <mark style="color:$success;">支持</mark> <a href="#support" id="support"></a>

如果您有任何问题，请访问我们的[支持页面](../integrations/lian-xi-wo-men.md)
