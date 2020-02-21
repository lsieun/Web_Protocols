# Response Code

<!-- TOC -->

- [1. 1XX-Informational](#1-1xx-informational)
- [2. 2XX-Request succeeded](#2-2xx-request-succeeded)
- [3. 3XX-Relocation and redirection](#3-3xx-relocation-and-redirection)
- [4. 4XX-Client error](#4-4xx-client-error)
- [5. 5XX-Server error](#5-5xx-server-error)

<!-- /TOC -->

Regardless of version, a response code from `100` to `199` always indicates an informational response, `200` to `299` always indicates success, `300` to `399` always indicates redirection, `400` to `499` always indicates a client error, and `500` to `599` indicates a server error.

## 1. 1XX-Informational

- **100 Continue**: The server is prepared to accept the request body and the client should send it; allows clients to ask whether the server will accept a request before they send a large amount of data as part of the request.
- **101 Switching Protocols**: The server accepts the client’s request in the Upgrade header field to change the application protocol (e.g., from HTTP to WebSockets.)

## 2. 2XX-Request succeeded

- **200 OK**: The most common response code. If the request method was `GET` or `POST`, the requested data is contained in the response along with the usual headers. If the request method was `HEAD`, only the header information is included. (`HTTP_OK`)
- **201 Created**: The server has created a resource at the URL specified in the body of the response. The client should now attempt to load that URL. This code is only sent in response to `POST` requests.(`HTTP_CREATED`)
- **202 Accepted**: This rather uncommon response indicates that a request (generally from `POST`) is being processed, but the processing is not yet complete, so no response can be returned. However, the server should return an HTML page that explains the situation to the user and provide an estimate of when the request is likely to be completed, and, ideally, a link to a status monitor of some kind.(`HTTP_ACCEPTED`)
- **203 Non-authoritative Information**: The resource representation was returned from a caching proxy or other local source and is not guaranteed to be up to date.(`HTTP_NOT_AUTHORITATIVE`)
- **204 No Content**: The server has successfully processed the request but has no information to send back to the client. This is normally the result of a poorly written form-processing program on the server that accepts data but does not return a response to the user.(`HTTP_NO_CONTENT`)
- **205 Reset Content**: The server has successfully processed the request but has no information to send back to the client. Furthermore, the client should clear the form to which the request is sent.(`HTTP_RESET`)
- **206 Partial Content**: The server has returned the part of the resource the client requested using the byte range extension to HTTP, rather than the whole document.(`HTTP_PARTIAL`)
- **226 IM Used**: Response is delta encoded.

## 3. 3XX-Relocation and redirection

- **300 Multiple Choices**: The server is providing a list of different representations (e.g., PostScript and PDF) for the requested document.(`HTTP_MULT_CHOICE`)
- **301 Moved Permanently**: The resource has moved to a new URL. The client should automatically load the resource at this URL and update any bookmarks that point to the old URL.(`HTTP_MOVED_PERM`)
- **302 Moved Temporarily**: The resource is at a new URL temporarily, but its location will change again in the foreseeable future; therefore, bookmarks should not be updated. Sometimes used by proxies that require the user to log in locally before accessing the Web.(`HTTP_MOVED_TEMP`)
- **303 See Other**: Generally used in response to a `POST` form request, this code indicates that the user should retrieve a resource from a different URL using `GET`.(`HTTP_SEE_OTHER`)
- **304 Not Modified**: The `If-Modified-Since` header indicates that the client wants the document only if it has been recently updated. This status code is returned if the document has not been updated. In this case, the client should load the document from its cache.(`HTTP_NOT_MODIFIED`)
- **305 Use Proxy**: The `Location` header field contains the address of a proxy that will serve the response.(`HTTP_USE_PROXY`)
- **307 Temporary Redirect**: Similar to `302` but without allowing the HTTP method to change.
- **308 Permanent Redirect**: Similar to `301` but without allowing the HTTP method to change.

## 4. 4XX-Client error

- **400 Bad Request**: The client request to the server used improper syntax. This is rather `HTTP_BAD_REQUEST` unusual in normal web browsing but more common when debugging custom clients.(`HTTP_BAD_REQUEST`)
- **401 Unauthorized**: Authorization, generally a username and password, is required to access this page. Either a username and password have not yet been presented or the username and password are invalid.(`HTTP_UNAUTHORIZED`)
- **402 Payment Required**: Not used today, but may be used in the future to indicate that some sort of payment is required to access the resource.(`HTTP_PAYMENT_REQUIRED`)
- **403 Forbidden**: The server understood the request, but is deliberately refusing to process it. Authorization will not help. This is sometimes used when a client has exceeded its quota.(`HTTP_FORBIDDEN`)
- **404 Not Found**: This most common error response indicates that the server cannot find the requested resource. It may indicate a bad link, a document that has moved with no forwarding address, a mistyped URL, or something similar.(`HTTP_NOT_FOUND`)
- **405 Method Not Allowed**: The request method is not allowed for the specified resource; for instance, you tried to `PUT` a file on a web server that doesn’t support `PUT` or tried to `POST` to a `URI` that only allows `GET`.(`HTTP_BAD_METHOD`)
- **406 Not Acceptable**: The requested resource cannot be provided in a format the client is willing to accept, as indicated by the `Accept` field of the request HTTP header.(`HTTP_NOT_ACCEPTABLE`)
- **407 Proxy Authentication Required**: An intermediate proxy server requires authentication from the client, probably in the form of a username and password, before it will retrieve the requested resource.(`HTTP_PROXY_AUTH`)
- **408 Request Timeout**: The client took too long to send the request, perhaps because of network congestion.(`HTTP_CLIENT_TIMEOUT`)
- **409 Conflict**: A temporary conflict prevents the request from being fulfilled; for instance, two clients are trying to `PUT` the same file at the same time.(`HTTP_CONFLICT`)
- **410 Gone**: Like a `404`, but makes a stronger assertion about the existence of the resource. The resource has been deliberately deleted (not moved) and will not be restored. Links to it should be removed.(`HTTP_GONE`)
- **411 Length Required**: The client must but did not send a `Content-length` field in the client request HTTP header.(`HTTP_LENGTH_REQUIRED`)
- **412 Precondition Failed**: A condition for the request that the client specified in the request HTTP header is not satisfied.(`HTTP_PRECON_FAILED`)
- **413 Request Entity Too Large**: The body of the client request is larger than the server is able to process at this time.(`HTTP_ENTITY_TOO_LARGE`)
- **414 Request-URI Too Long**: The URI of the request is too long. This is important to prevent certain buffer overflow attacks.(`HTTP_REQ_TOO_LONG`)
- **415 Unsupported Media Type**: The server does not understand or accept the MIME content type of the request body.(`HTTP_UNSUPPORTED_TYPE`)
- **416 Requested range Not Satisfiable**: The server cannot send the byte range the client requested.
- **417 Expectation Failed**: The server cannot meet the client’s expectation given in an `Expect` request header field.
- **418 I’m a teapot**: Attempting to brew coffee with a teapot.
- **420 Enhance Your Calm**: The server is rate limiting the request. Nonstandard; used only by Twitter.
- **422 Unprocessable Entity**: The content type of the request body is recognized, and the body is syntactically correct, but nonetheless the server can’t process it.
- **424 Failed Dependency**: Request failed as a result of the failure of a previous request.
- **426 Upgrade Required**: Client is using a too old or insecure a version of the HTTP protocol.
- **428 Precondition Required**: Request must supply an `If-Match` header.
- **429 Too Many Requests**: The client is being rate limited and should slow down.
- **431 Request Header Fields Too Large**: Either the header as a whole is too large, or one particular header field is too large.
- **451 Unavailable For Legal Reasons**: Experimental; the server is prohibited by law from servicing the request.

## 5. 5XX-Server error

- **500 Internal Server Error**: An unexpected condition occurred that the server does not know how to handle.(`HTTP_SERVER_ERROR`, `HTTP_INTERNAL_ERROR`)
- **501 Not Implemented**: The server does not have a feature that is needed to fulfill this request. A server that cannot handle `PUT` requests might send this response to a client that tried to `PUT` form data to it.(`HTTP_NOT_IMPLEMENTED`)
- **502 Bad Gateway**: This code is applicable only to servers that act as proxies or gateways. It indicates that the proxy received an invalid response from a server it was connecting to in an effort to fulfill the request.(`HTTP_BAD_GATEWAY`)
- **503 Service Unavailable**: The server is temporarily unable to handle the request, perhaps due to overloading or maintenance.(`HTTP_UNAVAILABLE`)
- **504 Gateway Timeout**: The proxy server did not receive a response from the upstream server within a reasonable amount of time, so it can’t send the desired response to the client.(`HTTP_GATEWAY_TIMEOUT`)
- **505 HTTP Version Not Supported**: The server does not support the version of HTTP the client is using (e.g., the as-yet-nonexistent HTTP 2.0).(`HTTP_VERSION`)
- **507 Insufficient Storage**: Server does not have enough space to store the supplied request entity; typically used for `POST` or `PUT`.
- **511 Network Authentication Required**: The client needs to authenticate to gain network access (e.g., on a hotel wireless network).
