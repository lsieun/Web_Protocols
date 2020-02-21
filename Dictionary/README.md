# A Dictionary Server Protocol

One simple bidirectional TCP protocol is `dict`, defined in [RFC 2229](https://tools.ietf.org/html/rfc2229). In this protocol, the client opens a socket to port `2628` on the dict server and sends commands such as “DEFINE fd-eng-lat gold”. This tells the server to send a definition of the word gold using its English-to-Latin dictionary. (Different servers have different dictionaries installed.) After the first definition is received, the client can ask for another. When it’s done it sends the command “quit”.

You can explore dict with Telnet like this:

```bash
$ telnet dict.org 2628
Trying 216.18.20.172...
Connected to dict.org.
Escape character is '^]'.
220 pan.alephnull.com dictd 1.12.1/rf on Linux 4.4.0-1-amd64 <auth.mime> <100831419.1794.1581872352@pan.alephnull.com>
DEFINE fd-eng-lat gold    # 查询gold单词
150 1 definitions retrieved
151 "gold" fd-eng-lat "English-Latin FreeDict Dictionary ver. 0.1.1"
gold /gould/
 1. aurarius; aureus; chryseus
 2. aurum; chrysos
.
250 ok [d/m/c = 1/0/10; 0.000r 0.000u 0.000s]
QUIT  # 退出
221 bye [d/m/c = 0/0/0; 42.000r 0.000u 0.000s]
Connection closed by foreign host.
```

## Reference

- [RFC 2229: A Dictionary Server Protocol](https://tools.ietf.org/html/rfc2229)
