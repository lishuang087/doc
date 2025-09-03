---
description: 本文档详细说明了 FlashBlock 的定价计划和 API 速率限制。
icon: lock-hashtag
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

# 定价与限制

***

## <mark style="color:$success;">定价计划</mark> <a href="#pricing-plans" id="pricing-plans"></a>

| 功能/计划 | 试用版    | 入门版    | 中级版        | 高级版    | 企业版      |
| ----- | ------ | ------ | ---------- | ------ | -------- |
| 价格    | 免费     | $200/月 | $400/月     | $800/月 | 定制       |
| 交易速率  | 10 TPS | 20 TPS | 40 TPS     | 80 TPS | 100+ TPS |
| SWQoS | 专用     | 专用     | 专用         | 专用     | 专用       |
| 技术支持  | 无支持    | 有限支持   | Discord 工单 | 直接消息支持 | 直接消息支持   |

***

## <mark style="color:$success;">超出限制</mark> <a href="#exceeding-limits" id="exceeding-limits"></a>

* 当超出速率限制时，API 将返回 429 状态码
* 实现指数退避重试机制
* 考虑升级您的计划以获得更高限制

***

## <mark style="color:$success;">计费信息</mark> <a href="#billing-information" id="billing-information"></a>

1. **计费周期**
   * 按月计费
   * 自动续费
   * 随时取消
2. **计划升级**
   * 登录您的账户
   * 进入计费设置
   * 选择新计划
   * 确认付款

***

## <mark style="color:$success;">联系销售</mark> <a href="#contact-sales" id="contact-sales"></a>

有关企业计划的更多信息，请[联系我们](lian-xi-wo-men.md)。
