# Time Protocol

The server listens for a connection on port `37`.  When the connection is established, the server returns a 32-bit time value and closes the connection.

The time protocol specifies that the time be sent as the number of seconds since midnight, January 1, 1900, Greenwich Mean Time. However, this is not sent as an ASCII string like 2,524,521,600 or -1297728000. Rather, it is sent as a 32-bit, unsigned, big-endian binary number.

If the server is unable to determine the time at its site, it should either refuse the connection or close it without sending anything.

## Reference

- [RFC 868: Time Protocol](https://tools.ietf.org/html/rfc868)
