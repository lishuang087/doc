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

# 👉 Quick Start

***

## <mark style="color:blue;">**Endpoints**</mark>

* New York City, USA: `http://ny.flashblock.trade`
* Salt Lake City, USA: `http://slc.flashblock.trade`
* Amsterdam, Netherlands: `http://ams.flashblock.trade`
* Frankfurt, Germany: `http://fra.flashblock.trade`
* Singapore: `http://singapore.flashblock.trade`
* London, UK：`http://london.flashblock.trade`

> It is recommended to use the HTTP protocol with persistent connections when accessing the above endpoints (e.g., `http://ny.flashblock.trade`)

***

## <mark style="color:blue;">**Tip Wallet**</mark>

Your transaction must include a standard SOL transfer instruction to our tip wallet.

* Minimum Tip: 0.001 SOL
* Higher Tip = Higher Priority

***

## <mark style="color:blue;">**Tip Wallet Addresses**</mark>

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

## <mark style="color:blue;">**API Call Example**</mark>

{% code lineNumbers="true" %}
```bash
curl -X POST 'http://ny.flashblock.trade/api/v2/submit-batch'
    -H "Authorization: $AUTH_HEADER"
    -H "Content-Type: application/json"
    -d '{
    "transactions": [
    "AaBU8zC90i...MAAAAAAAA=" #base64 only
    "AaBU8zC90i...MAAAAAAAA=" #multiple transactions allowed
    ]
    }'
```
{% endcode %}

***

## <mark style="color:blue;">**Usage Instructions**</mark>

* Select the nearest endpoint
* Add tip transfer instruction to your transaction
* Send transaction to the selected endpoint

## <mark style="color:blue;">**Important Notes**</mark>

* Ensure tip amount is at least SOL
* Use the nearest endpoint for optimal performance
* Higher tip amount results in higher transaction priority
