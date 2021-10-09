# Kijang TCP / Serial Protocol

To communicate between Kijang's server and its clients, the client would connected to the designated TCP port on the server, or via a serial port. Each request would be sent in its own packet using the below protocol.

The contents of each request are as follows (in bytes):

Version 1 (0001):

| Start | End | Description |
|-|-|-|
| 1 | 4 | Version of the protocol |
| 5 | 6 | Module that the packet was sent for |
| 7 | 8 | Communication code |
| 9 | 12 | Client ID |
| 13 | 20 | Request ID |
| 21 | 24 | Packet Count |
| 25 | 28 | Current Packet |
| 29 | - | Data of request |

This version of the protocol is currently in use in Kijang's TCP server as the TCP protocol would handle the size of the remaining datagram.

Version 2 (0002):

| Start | End | Description |
|-|-|-|
| 1 | 4 | Version of the protocol |
| 5 | 6 | Module that the packet was sent for |
| 7 | 8 | Communication code |
| 9 | 12 | Client ID |
| 13 | 20 | Request ID |
| 21 | 24 | Packet Count |
| 25 | 28 | Current Packet |
| 29 | 32 | Size of remaining data (in bytes) |
| 29 | - | Data of request |

This version of the protocol would be in use in serial connections with Kijang.

- All numbers (protocol version, communication code, client ID, request ID, packet count) are stored in big endian format for readability.
- For bytes 5-6, the first bit represents whether the module is a request from the client to the server (0) or from the server to the client (1). Although there would not be any collision with module names, this is done to allow for the packet data to be more easily readable.
- Client ID, request ID and packet count can not be 0.
- On the first request from the client to the server, the client can use a client ID of \0 as it had not been assigned an ID yet.
- A request can be split across multiple packets. As long as the Request ID remains the same, the server would be able to recognise them as the same request.
