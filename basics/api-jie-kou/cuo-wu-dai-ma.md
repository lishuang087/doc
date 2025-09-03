---
icon: '6'
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

# 错误代码

***

## <mark style="color:$success;">错误代码参考</mark> <a href="#error-codes-reference" id="error-codes-reference"></a>

| Error Code | Description                                         |
| ---------- | --------------------------------------------------- |
| 1001       | Batch validation error                              |
| 1002       | Invalid wallet address                              |
| 1003       | Insufficient funds                                  |
| 1004       | Network error                                       |
| 1005       | Invalid amount                                      |
| 1006       | Rate limit exceeded                                 |
| 1007       | Batch size exceeded                                 |
| 1008       | Transaction error                                   |
| 1009       | No authentication information in the request header |

***

## <mark style="color:$success;">重要注意事项</mark> <a href="#important-notes" id="important-notes"></a>

1. 确保 `transactions` 数组包含至少一个到小费地址的交易，否则验证将失败
2. 交易必须正确编码为 base64 格式
3. 批量提交有数量限制；超出这些限制将导致错误代码 1007
4. 提交前确保钱包有足够资金以避免错误代码 1003
5. 一旦提交并确认，交易无法撤销
6. 成功响应将包含一个 `bundleId` 和每个交易包中交易的 `transactionIds` 列表
