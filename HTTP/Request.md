# Request

<!-- TOC -->

- [1. request line](#1-request-line)
- [2. HTTP header](#2-http-header)

<!-- /TOC -->

Each request and response has the same basic form: **a request line**, **an HTTP header** containing metadata, **a blank line**, and then **a message body**.

A typical client request looks something like this:

```txt
GET /index.html HTTP/1.1
User-Agent: Mozilla/5.0
Host: en.wikipedia.org
Connection: keep-alive
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

```

GET requests like this one do not contain a message body, so the request ends with a blank line.

## 1. request line

```txt
GET /index.html HTTP/1.1
```

The first line is called the **request line**, and includes **a method**, **a path to a resource**, and **the version of HTTP**. The method specifies the operation being requested. The `GET` method asks the server to return a representation of a resource. `/index.html` is the path to the resource requested from the server. `HTTP/1.1` is the version of the protocol that the client understands.

## 2. HTTP header

Although the **request line** is all that is required, a client request usually includes other information as well in **a header**. Each line takes the following form:

```txt
Keyword: Value
```

Keywords are not case sensitive. Values sometimes are and sometimes aren’t. Both keywords and values should be ASCII only. If a value is too long, you can add a space or tab to the beginning of the next line and continue it.

Lines in the header are terminated by **a carriage-return linefeed pair**(`\r\n`).

Finally, the request is terminated with **a blank line**—that is, **two carriage return/linefeed pairs**, `\r\n\r\n`.
