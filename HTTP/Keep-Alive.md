# Keep-Alive

HTTP 1.0 opens a new connection for each request. In practice, the time taken to open and close all the connections in a typical web session can outweigh the time taken to transmit the data, especially for sessions with many small documents. This is even more problematic for encrypted HTTPS connections using SSL or TLS, because the handshake to set up a secure socket is substantially more work than setting up a regular socket.

In HTTP 1.1 and later, the server doesn’t have to close the socket after it sends its response. It can leave it open and wait for a new request from the client on the same socket. Multiple requests and responses can be sent in series over a single TCP connection. However, the **lockstep pattern** of a client request followed by a server response remains the same.

> The meaning of "lockstep" is not special, but is the English-language meaning, interpreted as "at the same time".

A client indicates that it’s willing to reuse a socket by including a `Connection` field in the HTTP request header with the value `Keep-Alive`:

```txt
Connection: Keep-Alive
```
