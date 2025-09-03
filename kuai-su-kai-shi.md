---
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

# 👉 快速开始

***

## <mark style="color:blue;">**终端节点**</mark>

* 美国纽约: `http://ny.flashblock.trade`
* 美国盐湖城: `http://slc.flashblock.trade`
* 荷兰阿姆斯特丹: `http://ams.flashblock.trade`
* 德国法兰克福: `http://fra.flashblock.trade`
* 新加坡: `http://singapore.flashblock.trade`
* 英国伦敦：`http://london.flashblock.trade`

> 建议在访问上述终端节点时使用HTTP协议并保持持久连接（例如：`http://ny.flashblock.trade`）

***

## <mark style="color:blue;">**小费钱包**</mark>

您的交易必须包含一个标准的SOL转账指令，发送到我们的小费钱包。

* 最小小费: 0.001 SOL
* 更高小费 = 更高优先级

***

## <mark style="color:blue;">**小费钱包地址**</mark>

```
FLaShB3iXXTWE1vu9wQsChUKq3HFtpMAhb8kAh1pf1wi
FLashhsorBmM9dLpuq6qATawcpqk1Y2aqaZfkd48iT3W
FLaSHJNm5dWYzEgnHJWWJP5ccu128Mu61NJLxUf7mUXU
FLaSHR4Vv7sttd6TyDF4yR1bJyAxRwWKbohDytEMu3wL
FLASHRzANfcAKDuQ3RXv9hbkBy4WVEKDzoAgxJ56DiE4
FLasHstqx11M8W56zrSEqkCyhMCCpr6ze6Mjdvqope5s
FLAShWTjcweNT4NSotpjpxAkwxUr2we3eXQGhpTVzRwy
FLasHXTqrbNvpWFB6grN47HGZfK6pze9HLNTgbukfPSk
FLAshyAyBcKb39KPxSzXcepiS8iDYUhDGwJcJDPX4g2B
FLAsHZTRcf3Dy1APaz6j74ebdMC6Xx4g6i9YxjyrDybR
```

***

## <mark style="color:blue;">**API调用示例**</mark>

```bash
curl -X POST 'http://ny.flashblock.trade/api/v2/submit-batch' \
     -H "Authorization: $AUTH_HEADER" \
     -H "Content-Type: application/json" \
     -d '{
       "transactions": [
         "AaBU8zC90i...MAAAAAAAA="  #仅支持base64格式
         "AaBU8zC90i...MAAAAAAAA="  #支持多笔交易
       ]
     }'
```

***

## <mark style="color:blue;">**使用说明**</mark>

* 选择最近的终端节点
* 在您的交易中添加小费转账指令
* 将交易发送到选定的终端节点

***

## <mark style="color:blue;">**重要注意事项**</mark>

* 确保小费金额至少为0.001 SOL
* 使用最近的终端节点以获得最佳性能
* 更高的小费金额会带来更高的交易优先级
