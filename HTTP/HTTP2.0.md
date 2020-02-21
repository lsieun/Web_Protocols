# HTTP 2.0

HTTP is the standard protocol for communication between web browsers and web servers. HTTP specifies how a client and server establish a connection, how the client requests data from the server, how the server responds to that request, and finally, how the connection is closed. HTTP connections use the TCP/IP protocol for data transfer. For each request from client to server, there is a sequence of four steps:

1. The client opens a TCP connection to the server on port `80`, by default; other ports may be specified in the URL.
2. The client sends a message to the server requesting the resource at a specified path. The request includes a header, and optionally (depending on the nature of the request) a blank line followed by data for the request.
3. The server sends a response to the client. The response begins with a response code, followed by a header full of metadata, a blank line, and the requested document or an error message.
4. The server closes the connection.

HTTP 2.0, which is mostly based on the SPDY protocol invented at Google, further optimizes HTTP transfers through header compression, pipelining requests and responses, and asynchronous connection multiplexing. However, these optimizations are usually performed in a translation layer that shields application programmers from the details, so the code you write will still mostly follow the preceding steps 1–4. Java does not yet support HTTP 2.0; but when the capability is added, your programs shouldn’t need to change to take advantage of it, as long as you access HTTP servers via the `URL` and `URLConnection` classes.
