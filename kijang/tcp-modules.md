# TCP Modules

The following module codes are designated for the following modules:

| Module code | Designation |
|-|-|
| 7FFD | KancilMocap |
| 7FFE | Pilanduk |
| 7FFF | Control module (client) |
| FFFE | Kijang |
| FFFF | Control module (server) |

## Control Module (Server) - FFFF

| Start | End | Designation |
|-|-|-|
| 0000 | 00FF | Diagnostic / basic codes |
| 0010 | 002F | System Information |
| F000 | FFFF | Error codes |

### Diagnostic / Basic Codes

| Byte | Designation | Contents |
|-|-|-|
| 0000 | Generic response | String of response |
| 0001 | Provision of Client ID | Client ID |
| 0002 | (Client -> Server) Pong | - |
| 0003 | (Server -> Client) Ping | - |
| 0004 | Returns server name | String containing server name |
| 0005 | Returns server version | String containing semver compliant server version |
| 00FE | Disconnects client | - |
| 00FF | Client disconnection request received | - |

- Once 00FE and 00FF is sent, future requests from the client would be ignored.

### System Information

### Error Codes

## Control Module (Client)

## Kijang - FFFE

## Pilanduk / KancilMocap - 7FFD/7FFE
