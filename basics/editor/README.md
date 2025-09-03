---
description: 这里包含了 FlashBlock API 的详细使用示例和最佳实践。
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

# 使用示例

***

## <mark style="color:$success;">文档列表</mark> <a href="#documentation-list" id="documentation-list"></a>

* [小费地址使用示例](xiao-fei-di-zhi-shi-yong-shi-li.md) - 如何在交易中包含小费地址
* [交易优化指南](jiao-yi-you-hua-zhi-nan.md) - 交易优化最佳实践

***

## <mark style="color:$success;">快速开始</mark> <a href="#quick-start" id="quick-start"></a>

#### 基础示例 <a href="#basic-example" id="basic-example"></a>

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

#### 高级示例 <a href="#advanced-example" id="advanced-example"></a>

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

## <mark style="color:$success;">最佳实践</mark> <a href="#best-practices" id="best-practices"></a>

1. **错误处理**: 始终实现适当的错误处理机制
2. **重试策略**: 使用指数退避重试策略
3. **监控**: 监控交易状态和错误率
4. **优化**: 根据网络条件调整优先级费用

更多详细信息请查看各个示例文档。
