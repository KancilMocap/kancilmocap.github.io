# TCP Modules

The following module codes are designated for the following modules:

| Module code | Designation |
|-|-|
| 7FFD | KancilMocap |
| 7FFE | Pilanduk |
| 7FFF | Control module (client) |
| FFFD | Kijang |
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
| 000F | Reserver | - |

- Once 000E is sent, future requests from the client would be ignored.

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

## Kijang - FFFD

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Output IO devices |
| 0010 | 001F | Input IO devices |
| 0020 | 002F | Plugin management |

### Output IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0000 | Returns of the block of codes is blocked | 2 bytes response on whether the block is password protected, as well as the type of hashing required |
| 0001 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0002 | Returns all available audio, video and motion devices | See below |
| 0003 | Returns all available audio devices | Multiple 6+n bytes sequence, first 4 bytes is audio device ID, next n bytes is audio device preset, last 2 bytes is uint16 representing UDP port |
| 0004 | Returns all available video devices | Multiple 6+n bytes sequence, first 4 bytes is video device ID, next n bytes is video device preset, last 2 bytes is uint16 representing UDP port |
| 0005 | Returns all available motion devices | Multiple 10 bytes sequence, first 4 bytes is motion device ID, next 4 bytes is motion device preset, last 2 bytes is uint16 representing UDP port |

n is currently TBD.

### 0002 Response

When providing all available audio, video and motion devices, the response consist of 3 main segments for the response of 0003, 0004 and 0005 respectively. Each segment would be prefixed by a 8 byte header representing the byte size of the response for that specific segment.

For instance, the response would start with the byte size of response 0003 followed by the entirety of response 0003; then the byte size of response 0004 followed by the entirety of response 0004; then the byte size of response 0005 followed by the entirety of response 0005.

### Input IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Returns of the block of codes is blocked | 2 bytes response on whether the block is password protected, as well as the type of hashing required |
| 0011 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0012 | Reserved | - |
| 0013 | Returns port for audio device to bind to | 2 bytes representing uint16 port number |
| 0014 | Returns port for video device to bind to | 2 bytes representing uint16 port number |
| 0015 | Returns port for motion device to bind to | 2 bytes representing uint16 port number |
| 0016 | Audio device removal acknowledged | - |
| 0017 | Video device removal acknowledged | - |
| 0018 | Motion device removal acknowledged | - |

### Plugin Management

| Byte | Designation | Contents |
|-|-|-|
| 0020 | Returns of the block of codes is blocked | 2 bytes response on whether the block is password protected, as well as the type of hashing required |
| 0021 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0022 | Returns all plugins on Kijang | A JSON file containing the metadata of all plugins currently installed on the server |
| 0023 | Returns metadata on the specified plugin on Kijang | A JSON file containing the metadata of the plugin specified, returns nothing if the plugin is not installed |
| 0024 | Acknowleges the request to enable / disable the specified plugin | 1 byte response on whether the plugin was successfully enabled or disabled, followed by its corresponding error if any |
| 0025 | Returns type of plugin needed (.dll, .dylib, .so) | 1 byte response on the type of plugin needed |
| 0024 | Returns status of online plugin installation | 1 byte representing status of plugin install, followed by its corresponding error if any |
| 0025 | Returns port for plugin data to be transferred | 1 byte representing whether request is approved, followed by 2 bytes representing uint16 port number |
| 0026 | Returns status of offline plugin installation | 1 byte representing status of plugin install, followed by its corresponding error if any |
| 0027 | Acknowleges the request to delete the specified plugin | 1 byte response on whether the plugin was successfully removed, followed by its corresponding error if any |

## Pilanduk / KancilMocap - 7FFD/7FFE

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Output IO devices |
| 0010 | 001F | Input IO devices |
| 0020 | 002F | Plugin management |

### Output IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0000 | Request whether the block of codes is blocked | - |
| 0001 | Request access to block | 2 bytes on the type of hashing used, remaining bytes is hashed password |
| 0002 | Request all available audio, video and motion devices | TBD |
| 0003 | Request all available audio devices | - |
| 0004 | Request all available video devices | - |
| 0005 | Request all available motion devices | - |

### Input IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Request whether the block of codes is blocked | - |
| 0011 | Request access to block | 2 bytes on the type of hashing used, remaining bytes is hashed password |
| 0012 | Reserved | - |
| 0013 | Request to add audio device | n bytes representing audio device preset |
| 0014 | Request to add video device | n bytes representing video device preset |
| 0015 | Request to add motion device | 4 bytes representing motion device preset |
| 0016 | Request to remove audio device | 2 bytes representing uint16 port number |
| 0017 | Request to remove video device | 2 bytes representing uint16 port number |
| 0018 | Request to remove motion device | 2 bytes representing uint16 port number |

n is TBD.

### Plugin Management

| Byte | Designation | Contents |
|-|-|-|
| 0020 | Request whether the block of codes is blocked | - |
| 0021 | Request access to block | 2 bytes on the type of hashing used, remaining bytes is hashed password |
| 0022 | Request all plugins on Kijang | - |
| 0023 | Request metadata on the specified plugin on Kijang | 4 bytes representing ID of plugin |
| 0024 | Request enabling / disabling plugins and its dependencies | 4 bytes representing ID of plugin, followed by 1 byte on whether to enable / disable it |
| 0025 | Request type of plugin needed (.dll, .dylib, .so) | - |
| 0024 | Request online plugin installation | URL of repository for plugin, or pointing towards a .dll, .dylib or .so file |
| 0025 | Request pysical plugin transfer | 4 bytes representing ID of plugin, 1 byte representing type of plugin, 1 byte representing hash type, remaining data is hash of resulting data |
| 0026 | Reserved | - |
| 0027 | Delete specific plugin | 4 bytes representing ID of plugin |
