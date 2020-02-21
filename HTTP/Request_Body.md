# Request Body

The **HTTP header** should include two fields that specify the nature of the body:

- A `Content-length` field that specifies how many bytes are in the body.
- A `Content-type` field that specifies the MIME media type of the bytes.

```txt
POST /cgi-bin/register.pl HTTP 1.0
Date: Sun, 27 Apr 2013 12:32:36
Host: www.cafeaulait.org
Content-type: application/x-www-form-urlencoded
Content-length: 54
username=Elliotte+Harold&email=elharo%40ibiblio.org
```
