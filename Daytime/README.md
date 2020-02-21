# Daytime Protocol

Daytime protocol is defined in [RFC 867](https://tools.ietf.org/html/rfc867). Reading that, you see that the daytime server listens on port `13`, and that the server sends the time in a human-readable format and closes the connection.

You can test the daytime server with Telnet like this:

```bash
$ telnet time.nist.gov 13
Trying 132.163.96.2...
Connected to ntp1.glb.nist.gov.
Escape character is '^]'.

58895 20-02-16 12:17:34 00 0 0 135.6 UTC(NIST) * 
Connection closed by foreign host.
```



## Reference

- [Daytime Protocol](https://tools.ietf.org/html/rfc867) 非常简短


