---
description: >-
  本文将详细介绍如何通过 HTTP Keep-Alive 机制，在使用 FlashBlock 的 Solana
  交易加速服务时提升网络性能，并附带实用的代码示例。
icon: '4'
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

# 优化网络请求性能

***

## <mark style="color:$success;">HTTP Keep-Alive 机制简介</mark> <a href="#introduction-to-http-keep-alive-mechanism" id="introduction-to-http-keep-alive-mechanism"></a>

HTTP Keep-Alive 是一种网络优化机制，允许多个 HTTP 请求和响应在同一个 TCP 连接上连续传输。传统的 HTTP 请求在每次请求时都要新建 TCP 连接，并在请求结束后关闭。这种方式在高频请求场景下效率低下，因为频繁的连接建立与关闭会带来额外开销。而启用 Keep-Alive 后，连接可保持打开状态，从而避免多次建立和关闭连接的过程，显著提升网络请求的效率。

***

## <mark style="color:$success;">HTTP Keep-Alive 工作原理</mark> <a href="#how-http-keep-alive-works" id="how-http-keep-alive-works"></a>

下面是 HTTP Keep-Alive 与未启用时的基本工作流程对比：

* **未启用 Keep-Alive**：
  1. 客户端与服务器建立一个 TCP 连接
  2. 客户端发送一次 HTTP 请求
  3. 服务器返回一次 HTTP 响应
  4. TCP 连接关闭
  5. 下一个请求需重新建立 TCP 连接
* **启用 Keep-Alive**：
  1. 客户端与服务器建立一个 TCP 连接
  2. 客户端发送 HTTP 请求 1
  3. 服务器返回 HTTP 响应 1
  4. 连接保持打开状态
  5. 客户端发送 HTTP 请求 2
  6. 服务器返回 HTTP 响应 2
  7. 连接可持续复用，直到显式关闭

***

## <mark style="color:$success;">HTTP Keep-Alive 启用优势</mark> <a href="#benefits-of-http-keep-alive" id="benefits-of-http-keep-alive"></a>

使用 HTTP Keep-Alive 带来以下优势：

1. **减少 TCP 握手开销**：避免每次请求都进行三次握手。
2. **避免 TCP 慢启动影响**：连接复用跳过慢启动阶段。
3. **降低系统资源消耗**：减少并发连接数量，减轻服务器负担。
4. **加快页面加载速度**：尤其适用于需加载多个资源的页面或接口调用。

***

## <mark style="color:$success;">**关于 FlashBlock 的 HTTP Keep-Alive 支持**</mark> <a href="#about-http-keep-alive-from-flashblock" id="about-http-keep-alive-from-flashblock"></a>

FlashBlock 的 HTTP Keep-Alive 最长保持时长为 **30 秒**。推荐每 **30 秒** 进行一次请求，以保持连接持续有效。

***

## <mark style="color:$success;">示例代码</mark> <a href="#example-code" id="example-code"></a>

为了演示如何在实践中利用 HTTP Keep-Alive，我们提供了一个 Nodejs 脚本，展示了 FlashBlock 上的 Solana 事务加速服务如何使用 HTTP Keep-Alive 优化网络请求。

代码实现

```js
import fetch from "node-fetch";
import http from "http";

(async () => {
  try {
    const keepAliveAgent = new http.Agent({
      keepAlive: true,
      keepAliveMsecs: 300000
    });

    const authHeader = ""; // Your APIKEY
    const batch = []; // Empty data
    const response = await fetch(
      "http://ny.flashblock.trade/api/v2/submit-batch",
      {
        method: "POST",
        headers: {
          Authorization: authHeader,
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ transactions: batch }),
        agent: keepAliveAgent
      }
    );

    const result = await response.json();
    // Err: Transaction length is too short
    // The return value is normal
  } catch (error) {
    console.error("Err:", error);
    throw error;
  }
})();
```
