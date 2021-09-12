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

- Once 00FF is sent, future requests from the client would be ignored.
- Once 00FE is sent, only 00FE response from the client would be acknowledged.

### System Information

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Returns of the block of codes is blocked | 2 bytes response on whether the block is password protected, as well as the type of hashing required |
| 0011 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0012 | Returns motherboard information | String containing motherboard information |
| 0013 | Returns CPU information | String containing CPU information |
| 0014 | Returns GPU information | String containing GPU information |
| 0015 | Returns hard disk information | String containing hard disk information |
| 0016 | Returns RAM information | String containing RAM information |
| 0017 | Returns peripheral device information | String containing peripheral device information |
| 0020 | Returns kernel name | String containing kernel name |
| 0021 | Returns kernel version | String containing kernel version |
| 0022 | Returns OS type | String containing OS type |
| 0023 | Returns OS version | String containing OS version |

### Error Codes

| Byte | Designation | Contents |
|-|-|-|
| F000 | Generic error | String of error |
| F001 | Invalid client ID | - |
| F002 | Invalid module | - |
| F003 | Unix time out of sync | int64 representing duration that the client is off by |
| F004 | Invalid request parameters | - |
| F005 | Timeout | uint32 representing duration that the client would be timed out for (in ms) |
| F006 | Permission denied |

## Control Module (Client)

| Start | End | Designation |
|-|-|-|
| 0000 | 00FF | Diagnostic / basic codes |
| 0010 | 002F | System Information |

### Diagnostic / Basic Codes

| Start | End | Designation |
|-|-|-|
| Byte | Designation | Contents |
|-|-|-|
| 0000 | Generic response | String of response |
| 0001 | Request Client ID | - |
| 0002 | (Client -> Server) Ping | - |
| 0003 | (Server -> Client) Pong | - |
| 0004 | Request server name | - |
| 0005 | Request server version | - |
| 00FE | Server disconnection request received | - |
| 00FF | Request disconnect from server | - |

- Once 00FE is sent, future requests from the server would be ignored.
- Once 00FF is sent, only 00FF response from the server would be acknowledged.

### System Information

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Request whether the block of codes is blocked | - |
| 0011 | Request access to block | 2 bytes on the type of hashing used, remaining bytes is hashed password |
| 0012 | Request motherboard information | - |
| 0013 | Request CPU information | - |
| 0014 | Request GPU information | - |
| 0015 | Request hard disk information | - |
| 0016 | Request RAM information | - |
| 0017 | Request peripheral device information | - |
| 0020 | Request kernel name | - |
| 0021 | Request kernel version | - |
| 0022 | Request OS type | - |
| 0023 | Request OS version | - |

## Kijang - FFFE

## Pilanduk / KancilMocap - 7FFD/7FFE
