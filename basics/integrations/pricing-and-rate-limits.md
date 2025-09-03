---
description: This document details FlashBlock's pricing plans and API rate limits.
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

# Pricing & Rate-Limits

***

## <mark style="color:$success;">Pricing Plans</mark> <a href="#pricing-plans" id="pricing-plans"></a>

| Feature/Plan      | Trial      | Entry           | Intermediate           | Advanced               | Enterprise             |
| ----------------- | ---------- | --------------- | ---------------------- | ---------------------- | ---------------------- |
| Price             | Free       | $200/month      | $400/month             | $800/month             | Custom                 |
| Transaction Rate  | 10 TPS     | 20 TPS          | 40 TPS                 | 80 TPS                 | 100+ TPS               |
| SWQoS             | Dedicated  | Dedicated       | Dedicated              | Dedicated              | Dedicated              |
| Technical Support | No Support | Limited Support | Discord Ticket Support | Direct Message Support | Direct Message Support |

***

## <mark style="color:$success;">Exceeding Limits</mark> <a href="#exceeding-limits" id="exceeding-limits"></a>

* When rate limits are exceeded, the API will return a 429 status code
* Implement exponential backoff retry mechanism
* Consider upgrading your plan for higher limits

***

## <mark style="color:$success;">Billing Information</mark> <a href="#billing-information" id="billing-information"></a>

1. **Billing Cycle**
   * Monthly billing
   * Automatic renewal
   * Cancel anytime
2. **Plan Upgrade**
   * Log in to your account
   * Go to billing settings
   * Select new plan
   * Confirm payment

***

## Contact Sales <a href="#contact-sales" id="contact-sales"></a>

For more information about Enterprise plans, please [contact us](contact-us.md).
