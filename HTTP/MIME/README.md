# MIME

<!-- TOC -->

- [1. Intro](#1-intro)
- [2. Common](#2-common)
  - [2.1. Application](#21-application)
- [3. Reference](#3-reference)

<!-- /TOC -->

## 1. Intro

```txt
Accept: text/html, text/plain, image/gif, image/jpeg
```

MIME types are classified at two levels: a **type** and a **subtype**. The **type** shows very generally what kind of data is contained: is it a picture, text, or movie? The **subtype** identifies the specific type of data: GIF image, JPEG image, TIFF image. For example, HTML’s content type is `text/html`; the type is `text`, and the subtype is `html`. The content type for a JPEG image is `image/jpeg`; the type is `image`, and the subtype is `jpeg`.

Eight top-level types have been defined:

- `text/*` for human-readable words
- `image/*` for pictures
- `model/*` for 3D models such as VRML files
- `audio/*` for sound
- `video/*` for moving pictures, possibly including sound
- `application/*` for binary data
- `message/*` for protocol-specific envelopes such as email messages and HTTP responses
- `multipart/*` for containers of multiple documents and resources

Each of these has many different subtypes.

In addition, **nonstandard custom types and subtypes** can be freely defined as long as they begin with `x-`. For example, Flash files are commonly assigned the type `application/x-shockwave-flash`.

```txt
application/x-www-form-urlencoded
```

## 2. Common

### 2.1. Application

- msword: `application/msword`
- pdf: `application/pdf`
- zip: `application/zip`

## 3. Reference

- [Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml)最新的MIME参考地址
