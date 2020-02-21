# Echo Protocol

The echo protocol, defined in RFC 862, is one of the simplest interactive TCP services. The client opens a socket to port `7` on the echo server and sends data. The server sends the data back. This continues until the client closes the connection. The echo protocol is useful for testing the network to make sure that data is not mangled by a misbehaving router or firewall.

You can test echo with Telnet like this:

```java
telnet rama.poly.edu 7
```

## Reference

- [Echo Protocol](https://tools.ietf.org/html/rfc862)
