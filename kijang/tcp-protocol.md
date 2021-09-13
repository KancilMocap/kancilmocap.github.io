# Kijang TCP Protocol

To communicate between Kijang's TCP server and its clients, the client would connected to the designated TCP port on the server. Each request would be sent in its own TCP packet.

The contents of each request are as follows (in bytes):

| Start | End | Description |
|-|-|-|
| 1 | 2 | Module that the packet was sent for |
| 3 | 4 | Communication code |
| 5 | 8 | Client ID |
| 9 | 16 | Request ID |
| 17 | 20 | Packet Count |
| 21 | - | Data of request |

- All numbers (communication code, client ID, request ID, packet count) are stored in big endian format for readability.
- For bytes 1-2, the first bit represents whether the module is a request from the client to the server (0) or from the server to the client (1). Although there would not be any collision with module names, this is done to allow for the packet data to be more easily readable.
- Client ID, request ID and packet count can not be 0.
- On the first request from the client to the server, the client can use a client ID of \0 as it had not been assigned an ID yet.
- A request can be split across multiple packets. As long as the Request ID remains the same, the server would be able to recognise them as the same request.
