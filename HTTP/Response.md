# Response

The response begins with a **status line**, followed by a **header** describing the response using the same “name: value” syntax as the request header, **a blank line**, and **the requested resource**.

A typical successful response looks something like this:

```txt
HTTP/1.1 200 OK
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
Content-length: 115

<html>
<head>
<title>
A Sample HTML file
</title>
</head>
<body>
The rest of the document goes here
</body>
</html>
```

## status line

```txt
HTTP/1.1 200 OK
```

The **first line** indicates the **protocol** the server is using (`HTTP/1.1`), followed by a response code. `200 OK` is the most common response code, indicating that the request was successful.

## header

```txt
Date: Sun, 21 Apr 2013 15:12:46 GMT
Server: Apache
Connection: close
Content-Type: text/html; charset=ISO-8859-1
Content-length: 115
```

The other header lines identify the date the request was made in the server’s time frame, the server software (`Apache`), a promise that the server will `close` the connection when it’s finished sending, the MIME media type, and the length of the document delivered (not counting this header)—in this case, `115` bytes.
