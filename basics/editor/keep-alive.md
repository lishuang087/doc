---
description: >-
  This article details how to leverage HTTP Keep-Alive to enhance network
  performance when using the Solana transaction acceleration service on
  FlashBlock, with practical code examples provided.
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

# Keep-Alive

***

## <mark style="color:$success;">Introduction to HTTP Keep-Alive Mechanism</mark> <a href="#introduction-to-http-keep-alive-mechanism" id="introduction-to-http-keep-alive-mechanism"></a>

HTTP Keep-Alive is a network optimization mechanism that allows multiple HTTP requests and responses to be sent and received over a single TCP connection. Traditional HTTP requests establish a new TCP connection for each request and close it afterward. This approach is inefficient for frequent requests due to the overhead of repeatedly establishing and closing connections. By keeping the connection open, HTTP Keep-Alive avoids redundant connection setup and teardown processes, significantly improving network request efficiency.

***

## <mark style="color:$success;">How HTTP Keep-Alive Works</mark> <a href="#how-http-keep-alive-works" id="how-http-keep-alive-works"></a>

Below is the basic workflow of the HTTP Keep-Alive mechanism:

* **Without Keep-Alive**:
  1. Client establishes a TCP connection with the server.
  2. Client sends an HTTP request.
  3. Server returns an HTTP response.
  4. TCP connection closes.
  5. Next request requires a new TCP connection.
* **With Keep-Alive**:
  1. Client establishes a TCP connection with the server.
  2. Client sends HTTP Request 1.
  3. Server returns HTTP Response 1.
  4. Connection remains open.
  5. Client sends HTTP Request 2.
  6. Server returns HTTP Response 2.
  7. Connection can be reused until closed.

***

## <mark style="color:$success;">Benefits of HTTP Keep-Alive</mark> <a href="#benefits-of-http-keep-alive" id="benefits-of-http-keep-alive"></a>

Using HTTP Keep-Alive offers the following advantages:

1. **Reduced TCP Handshake Overhead**: Eliminates the three-way handshake for every request.
2. **Avoids TCP Slow Start Impact**: Reuses existing connections, bypassing the slow start phase.
3. **Lower System Resource Consumption**: Reduces the number of simultaneous open connections.
4. **Faster Page Load Times**: Particularly effective for webpages requiring multiple resources.

***

## <mark style="color:$success;">About</mark> <mark style="color:$success;"></mark><mark style="color:$success;">**HTTP Keep-Alive**</mark> <mark style="color:$success;"></mark><mark style="color:$success;">from FlashBlock</mark> <a href="#about-http-keep-alive-from-flashblock" id="about-http-keep-alive-from-flashblock"></a>

The maximum duration for a FlashBlock Keep-Alive is 30 seconds. It is recommended to perform an access approximately every 30 seconds.

***

## <mark style="color:$success;">Example Code</mark> <a href="#example-code" id="example-code"></a>

To demonstrate how to leverage HTTP Keep-Alive in practice, we provide a Nodejs script showing how the Solana transaction acceleration service on FlashBlock optimizes network requests using HTTP Keep-Alive.

Code Implementation

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
