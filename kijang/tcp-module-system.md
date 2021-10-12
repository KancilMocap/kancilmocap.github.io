# System Modules

The following module codes are designated for the following modules:

| Module code | Designation |
|-|-|
| 7FFF | Control module (client) |
| FFFE | Control module (server) |
| FFFF | Async response (internal) |

FFFF module codes are reserved for internal communications in servers and clients respectively. Once the request is received, the server / client will wait until a response is received, or until a timeout is received.

## Control Module (Server) - FFFE

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Diagnostic / basic codes |
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
| 000E | Disconnects client | - |
| 000F | Reserved | - |

- Once 000E is sent, future requests from the client would be ignored.

### System Information

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Returns of the block of codes is blocked | [Auth requirement](./tcp-module-auth) |
| 0011 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block (\0 means granted, anything else means denied) |
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

## Control Module (Client) - 7FFF

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Diagnostic / basic codes |
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
| 000E | Reserved | - |
| 000F | Request disconnect from server | - |

- Once 000F is sent, future requests from the server would be ignored.

### System Information

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Request whether the block of codes is blocked | - |
| 0011 | Request access to block | [Auth request](./tcp-module-auth) |
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
