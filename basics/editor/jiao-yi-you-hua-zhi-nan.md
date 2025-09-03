---
description: 本指南将帮助您优化FlashBlock交易，提高成功率并降低成本。
icon: '3'
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

# 交易优化指南

***

## <mark style="color:$success;">交易优化策略</mark> <a href="#transaction-optimization-strategies" id="transaction-optimization-strategies"></a>

### 1. 选择最近的服务器端点 <a href="#id-1-xuan-ze-zui-jin-de-fu-wu-qi-duan-dian" id="id-1-xuan-ze-zui-jin-de-fu-wu-qi-duan-dian"></a>

选择地理位置最近的服务器将提供最低延迟：

* **北美用户**: 使用 `http://ny.flashblock.trade` 或 `http://slc.flashblock.trade`
* **欧洲用户**: 使用 `http://ams.flashblock.trade` 或 `http://fra.flashblock.trade`
* **其他地区**: 基于网络延迟测试选择最佳端点

### 2. 优化小费金额 <a href="#id-2-you-hua-xiao-fei-jin-e" id="id-2-you-hua-xiao-fei-jin-e"></a>

小费金额直接影响交易优先级：

* **最小小费**: 0.001 SOL
* **推荐小费**: 0.001 - 0.01 SOL (根据网络拥堵情况调整)
* **高优先级**: 0.01+ SOL (紧急交易)

### 3. 监控网络状态 <a href="#id-4-jian-kong-wang-luo-zhuang-tai" id="id-4-jian-kong-wang-luo-zhuang-tai"></a>

发送交易前，检查：

* Solana网络状态
* 当前网络拥堵情况
* 平均交易确认时间

### 4. 交易结构优化 <a href="#id-5-jiao-yi-jie-gou-you-hua" id="id-5-jiao-yi-jie-gou-you-hua"></a>

**正确的交易格式**

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

小费指令示例

{% code lineNumbers="true" %}
```javascript
// Add a tip transfer instruction to your transaction
const tipInstruction = SystemProgram.transfer({
  fromPubkey: wallet.publicKey,
  toPubkey: new PublicKey("FLaShB3iXXTWE1vu9wQsChUKq3HFtpMAhb8kAh1pf1wi"),
  lamports: 1000000 // 0.001 SOL
});
```
{% endcode %}

### 5. 🧪三明治攻击缓解功能 <a href="#id-6-sandwich-mitigation-feature" id="id-6-sandwich-mitigation-feature"></a>

我们引入了一个新功能来帮助缓解三明治攻击——无需投票账户方法。

<mark style="color:$success;">**工作原理**</mark>

在您的Solana交易中，向任何指令添加以`jitodontfront`开头的任何有效Solana公钥。例如：\
`jitodontfront1111111flashblockdottrade` 或 `jitodontfront1111111flashblockdottrade`

任何包含`jitodontfront`账户的交易包将被**区块引擎拒绝**，除非该交易在包中首先出现（索引0）。

不包含此账户的交易和包**不受**此更改影响。

**✅ 允许的包模式:**

* `[tx_with_dont_front, tip]`
* `[tx_with_dont_front, arbitrage, tip]`

**❌ 不允许的包模式:**

* `[tip, tx_with_dont_front]`
* `[txA_with_dont_front, txB_with_dont_front]`
* `[txA_with_dont_front, txB_with_dont_front, tip]`
* `[trade, tx_with_dont_front, arbitrage, tip]`

**📌 重要要点**

* 账户**不需要**在链上存在，但**必须**是有效的公钥
* 将账户标记为**只读**以优化落地速度
* **(可选)** 为您的应用程序使用`jitodontfront`的唯一变体（使用您自己的公钥），例如：\
  `jitodontfront1111111flashblockdottradejitodontfront1111111flashblockdottrade`
* 支持**AddressLookupTables**

**📋 示例**

{% code lineNumbers="true" %}
```javascript
// Add the protection account to your transaction instruction
const dontFrontAccount = new PublicKey("jitodontfront1111111flashblockdottrade");

// Add to any instruction (recommended as read-only)
const protectedInstruction = {
  programId: yourProgramId,
  keys: [
    { pubkey: dontFrontAccount, isSigner: false, isWritable: false }, // read-only
    // ... other accounts
  ],
  data: instructionData
};
```
{% endcode %}

***

## <mark style="color:$success;">性能优化技巧</mark> <a href="#performance-optimization-tips" id="performance-optimization-tips"></a>

### 1. 连接优化 <a href="#id-1-lian-jie-you-hua" id="id-1-lian-jie-you-hua"></a>

* 使用持久HTTP连接
* 启用连接重用
* 设置合理的超时值
* 每30秒发送一次ping请求

### 2. 错误处理 <a href="#id-2-cuo-wu-chu-li" id="id-2-cuo-wu-chu-li"></a>

{% code lineNumbers="true" %}
```javascript
try {
  const response = await fetch('http://ny.flashblock.trade/api/v2/submit-batch', {
    method: 'POST',
    headers: {
      'Authorization': authHeader,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ transactions: batch })
  });

  const result = await response.json();

  if (result.success) {
    console.log('Batch submitted successfully:', result.data);
  } else {
    console.error(`Error: ${result.message} (Code: ${result.code})`);
  }
} catch (error) {
  console.error('API request failed:', error);
  throw error;
}
```
{% endcode %}

***

## <mark style="color:$success;">成本优化</mark> <a href="#cost-optimization" id="cost-optimization"></a>

小费策略

* 根据交易紧急程度调整小费
* 对非紧急交易使用最小小费
* 根据网络拥堵情况动态调整

***

## <mark style="color:$success;">故障排除</mark> <a href="#troubleshooting" id="troubleshooting"></a>

### 1. 交易失败 <a href="#id-1-jiao-yi-shi-bai" id="id-1-jiao-yi-shi-bai"></a>

* 检查小费是否足够
* 验证交易格式
* 确认网络连接

### 2. 高延迟 <a href="#id-2-gao-yan-chi" id="id-2-gao-yan-chi"></a>

* 切换到更近的端点
* 增加小费金额
* 检查网络状态

### 3. 高成本 <a href="#id-3-gao-cheng-ben" id="id-3-gao-cheng-ben"></a>

* 优化批量大小
* 调整小费策略
* 选择合适的时间窗口

***

## <mark style="color:$success;">最佳实践总结</mark> <a href="#best-practices-summary" id="best-practices-summary"></a>

1. **始终使用最近的服务器端点**
2. **根据网络状态动态调整小费**
3. **实现合理的重试机制**
4. **监控关键性能指标**
5. **优化交易批量大小**
6. **在代码中保持强大的错误处理**

通过遵循这些优化策略，您将显著提高交易成功率，减少延迟，并优化成本效率。
