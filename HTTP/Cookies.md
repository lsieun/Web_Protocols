# Cookies

<!-- TOC -->

- [1. Intro](#1-intro)
  - [1.1. Theory](#11-theory)
  - [1.2. Charset](#12-charset)
- [2. Server and Client](#2-server-and-client)
  - [2.1. Set-Cookie](#21-set-cookie)
  - [2.2. Cookie](#22-cookie)
  - [2.3. Multi Set-Cookie](#23-multi-set-cookie)
- [3. Cookie Scope](#3-cookie-scope)
  - [3.1. domain](#31-domain)
  - [3.2. path](#32-path)
  - [3.3. domain and path](#33-domain-and-path)
  - [3.4. expire](#34-expire)
  - [3.5. Max-Age](#35-max-age)
  - [3.6. secure](#36-secure)
  - [3.7. httponly](#37-httponly)

<!-- /TOC -->

## 1. Intro

### 1.1. Theory

Many websites use small strings of text known as **cookies** to store persistent client-side state between connections. Cookies are passed from server to client and back again in the HTTP headers of requests and responses.

Cookies can be used by a server to indicate session IDs, shopping cart contents, login credentials, user preferences, and more.

### 1.2. Charset

Cookies are limited to nonwhitespace ASCII text, and may not contain commas or semicolons.

## 2. Server and Client

### 2.1. Set-Cookie

To set a cookie in a browser, the server includes a `Set-Cookie` header line in the HTTP header. For example, this HTTP header sets the cookie “cart” to the value “ATVPD‐KIKX0DER”:

```txt
HTTP/1.1 200 OK
Content-type: text/html
Set-Cookie: cart=ATVPDKIKX0DER
```

### 2.2. Cookie

If a browser makes a second request to the same server, it will send the cookie back in a `Cookie` line in the HTTP request header like so:

```txt
GET /index.html HTTP/1.1
Host: www.example.org
Cookie: cart=ATVPDKIKX0DER
Accept: text/html
```

### 2.3. Multi Set-Cookie

Servers can set more than one cookie. For example, a request I just made to Amazon fed my browser five cookies:

```txt
Set-Cookie:skin=noskin
Set-Cookie:ubid-main=176-5578236-9590213
Set-Cookie:session-token=Zg6afPNqbaMv2WmYFOv57zCU1O6Ktr
Set-Cookie:session-id-time=2082787201l
Set-Cookie:session-id=187-4969589-3049309
```

## 3. Cookie Scope

In addition to a simple `name=value` pair, cookies can have several attributes that control their scope including **expiration date**, **path**, **domain**, **port**, **version**, and **security** options.

### 3.1. domain

For example, by default, a cookie applies to the server it came from. If a cookie is originally set by `www.foo.example.com`, the browser will only send the cookie back to `www.foo.example.com`. However, a site can also indicate that a cookie applies within **an entire subdomain**, not just at the original server. For example, this request sets a user cookie for the entire `foo.example.com` domain:

```txt
Set-Cookie: user=elharo;Domain=.foo.example.com
```

The browser will echo this cookie back not just to `www.foo.example.com`, but also to `lothar.foo.example.com`, `eliza.foo.example.com`, `enoch.foo.example.com`, and any other host somewhere in the `foo.example.com` domain. However, a server can only set cookies for **domains it immediately belongs** to. `www.foo.example.com` cannot set a cookie for `www.oreilly.com`, `example.com`, or `.com`, no matter how it sets the domain.

### 3.2. path

Cookies are also scoped by `path`, so they’re returned for some directories on the server, but not all. **The default scope is the original URL and any subdirectories**. For instance, if a cookie is set for the URL `http://www.cafeconleche.org/XOM/`, the cookie also applies in `http://www.cafeconleche.org/XOM/apidocs/`, but not in `http://www.cafeconleche.org/slides/` or `http://www.cafeconleche.org/`.

However, **the default scope can be changed using a `Path` attribute in the cookie**. For example, this next response sends the browser a cookie with the name “user” and the value “elharo” that applies only within the server’s `/restricted` subtree, not on the rest of the site:

```txt
Set-Cookie: user=elharo; Path=/restricted
```

When requesting a document in the subtree `/restricted` from the same server, the client echoes that cookie back. However, it does not use the cookie in other directories on the site.

### 3.3. domain and path

A cookie can include both a `domain` and a `path`. For instance, this cookie applies in the `/restricted` path on any servers within the `example.com` domain:

```txt
Set-Cookie: user=elharo;Path=/restricted;Domain=.example.com
```

The order of the different cookie attributes doesn’t matter, as long as they’re all separated by semicolons and the cookie’s own name and value come first.

However, this isn’t true when the client is sending the cookie back to the server. In this case, the `path` must precede the `domain`, like so:

```txt
Cookie: user=elharo; Path=/restricted;Domain=.foo.example.com
```

### 3.4. expire

A cookie can be set to expire at a certain point in time by setting the `expires` attribute to a date in the form `Wdy, DD-Mon-YYYY HH:MM:SS GMT`. Weekday and month are given as three-letter abbreviations. The rest are numeric, padded with initial zeros if necessary. In the pattern language used by `java.text.SimpleDateFormat`, this is `E, dd-MMM-yyyy H:m:s z`.

For instance, this cookie expires at 3:23 P.M. on December 21, 2015:

```txt
Set-Cookie: user=elharo; expires=Wed, 21-Dec-2015 15:23:00 GMT
```

The browser should remove this cookie from its cache after that date has passed.

### 3.5. Max-Age

The `Max-Age` attribute that sets the cookie to expire after a certain number of seconds have passed instead of at a specific moment. For instance, this cookie expires one hour (3,600 seconds) after it’s first set:

```txt
Set-Cookie: user="elharo"; Max-Age=3600
```

The browser should delete this cookie after this amount of time has elapsed.

### 3.6. secure

Because cookies can contain sensitive information such as passwords and session keys, some cookie transactions should be secure. Most of the time this means using HTTPS instead of HTTP; but whatever it means, each cookie can have a `secure` attribute with no value, like so:

```txt
Set-Cookie: key=etrogl7*;Domain=.foo.example.com; secure
```

Browsers are supposed to refuse to send such cookies over insecure channels.

### 3.7. httponly

For additional security against cookie-stealing attacks like XSRF, cookies can set the `HttpOnly` attribute. This tells the browser to only return the cookie via HTTP and HTTPS and specifically not by JavaScript:

```txt
Set-Cookie: key=etrogl7*;Domain=.foo.example.com; secure; httponly
```

