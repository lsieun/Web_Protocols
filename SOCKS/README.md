# SOCKS

## SOCKS 5

```txt
client <---> server <---> host
```

### Client 01

The client connects to the server, and sends a **version identifier**/**method selection** message:

| VER  | NMETHODS | METHODS  |
| ---- | -------- | -------- |
| 1    | 1        | 1 to 255 |

The `VER` field is set to X'05' for this version of the protocol. The `NMETHODS` field contains the number of method identifier octets that appear in the `METHODS` field.

### Server 01

The server selects from one of the methods given in `METHODS`, and sends a METHOD selection message:

| VER  | METHOD |
| ---- | ------ |
| 1    | 1      |

If the selected `METHOD` is X'FF', none of the methods listed by the client are acceptable, and the client MUST close the connection.

The values currently defined for `METHOD` are:

- X'00' NO AUTHENTICATION REQUIRED
- X'01' GSSAPI
- X'02' USERNAME/PASSWORD
- X'03' to X'7F' IANA ASSIGNED
- X'80' to X'FE' RESERVED FOR PRIVATE METHODS
- X'FF' NO ACCEPTABLE METHODS

The client and server then enter a method-specific sub-negotiation.

### Client 02

The SOCKS request is formed as follows:

| VER  | CMD  | RSV   | ATYP | DST.ADDR | DST.PORT |
| ---- | ---- | ----- | ---- | -------- | -------- |
| 1    | 1    | X'00' | 1    | Variable | 2        |

- VER: protocol version: X'05'
- CMD
  - CONNECT X'01'
  - BIND X'02'
  - UDP ASSOCIATE X'03'
- RSV: RESERVED
- ATYP: address type of following address
  - IP V4 address: X'01'
  - DOMAINNAME: X'03'
  - IP V6 address: X'04'
- DST.ADDR: desired destination address
- DST.PORT: desired destination port in network octet order

The SOCKS server will typically evaluate the request based on source and destination addresses, and return one or more reply messages, as appropriate for the request type.

### Server 02

The server evaluates the request, and returns a reply formed as follows:

| VER  | REP  | RSV   | ATYP | BND.ADDR | BND.PORT |
| ---- | ---- | ----- | ---- | -------- | -------- |
| 1    | 1    | X'00' | 1    | Variable | 2        |

- VER: protocol version: X'05'
- REP: Reply field
  - X'00' succeeded
  - X'01' general SOCKS server failure
  - X'02' connection not allowed by ruleset
  - X'03' Network unreachable
  - X'04' Host unreachable
  - X'05' Connection refused
  - X'06' TTL expired
  - X'07' Command not supported
  - X'08' Address type not supported
  - X'09' to X'FF' unassigned
- RSV: RESERVED
- ATYP: address type of following address
  - IP V4 address: X'01'
  - DOMAINNAME: X'03'
  - IP V6 address: X'04'
- BND.ADDR: server bound address
- BND.PORT: server bound port in network octet order







## Reference

- [SOCKS Protocol Version 5](https://tools.ietf.org/html/rfc1928)
- [SOCKS Protocol Version 6](https://tools.ietf.org/id/draft-olteanu-intarea-socks-6-00.html)
