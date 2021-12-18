# KancilMocap Modules

The following modules are used in KancilMocap applications, such as Kijang, Pilandok and KancilMocap.

| Module code | Designation |
|-|-|
| 7FFE | KancilMocap / Pilandok |
| FFFE | Kijang |

## Kijang - FFFE

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Output IO devices |
| 0010 | 001F | Input IO devices |
| 0020 | 002F | Plugin management |
| F000 | F0FF | Generic Error |
| F100 | F1FF | Plugin System Errors |

### Output IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0000 | Reserved | - |
| 0001 | Reserved | - |
| 0002 | Returns all available audio, video and motion devices | See below |
| 0003 | Returns all available audio devices | Multiple 4+n bytes sequence, first 4 bytes is audio device ID, next n bytes is audio device preset |
| 0004 | Returns all available video devices | Multiple 4+n bytes sequence, first 4 bytes is video device ID, next n bytes is video device preset |
| 0005 | Returns all available motion devices | Multiple 8 bytes sequence, first 4 bytes is motion device ID, next 4 bytes is motion device preset |
| 0006 | Start streaming audio device request acknowledged | - |
| 0007 | Start streaming video device request acknowledged | - |
| 0008 | Start streaming motion device request acknowledged | - |
| 0009 | Stop streaming audio device request acknowledged | - |
| 000A | Stop streaming video device request acknowledged | - |
| 000B | Stop streaming motion device request acknowledged | - |

n is currently TBD.

### 0002 Response

When providing all available audio, video and motion devices, the response consist of 3 main segments for the response of 0003, 0004 and 0005 respectively. Each segment would be prefixed by a 8 byte header representing the byte size of the response for that specific segment.

For instance, the response would start with the byte size of response 0003 followed by the entirety of response 0003; then the byte size of response 0004 followed by the entirety of response 0004; then the byte size of response 0005 followed by the entirety of response 0005.

### Input IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Returns of the block of codes is blocked | [Auth requirement](./tcp-module-auth) |
| 0011 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0012 | Reserved | - |
| 0013 | Audio device addition acknowledged | 2 bytes representing uint16 receiving port number, 4 bytes representing audio device ID |
| 0014 | Video device addition acknowledged | 2 bytes representing uint16 receiving port number, 4 bytes representing video device ID |
| 0015 | Motion device addition acknowledged | 2 bytes representing uint16 receiving port number, 4 bytes representing motion device ID |
| 0016 | Audio device removal acknowledged | - |
| 0017 | Video device removal acknowledged | - |
| 0018 | Motion device removal acknowledged | - |

### Plugin Management

| Byte | Designation | Contents |
|-|-|-|
| 0020 | Returns of the block of codes is blocked | [Auth requirement](./tcp-module-auth) |
| 0021 | Returns whether the block access is granted | 1 byte response on whether access has been granted for the block |
| 0022 | Returns all plugins on Kijang as JSON | A JSON file containing the metadata of all plugins currently installed on the server |
| 0023 | Returns all plugins on Kijang as hex string | Multiple 4 bytes sequence representing ID of plugins |
| 0024 | Returns metadata on the specified plugin on Kijang | A JSON file containing the metadata of the plugin specified, returns nothing if the plugin is not installed |

### Generic Error

| Byte | Designation | Contents |
|-|-|-|
| F000 | Request denied by server | - |
| F001 | Unauthorized client | - |
| F002 | Unable to access port specified by client | - |
| F003 | No data received from port specified by client | - |
| F004 | Max outgoing connections reached for server | - |

### Plugin System Errors

| Byte | Designation | Contents |
|-|-|-|
| F100 | Plugin not found | 4 bytes representing ID of plugin |

## KancilMocap / Pilandok - 7FFE

| Start | End | Designation |
|-|-|-|
| 0000 | 000F | Output IO devices |
| 0010 | 001F | Input IO devices |
| 0020 | 002F | Plugin management |

### Output IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0000 | Reserved | - |
| 0001 | Reserved | - |
| 0002 | Request all available audio, video and motion devices | TBD |
| 0003 | Request all available audio devices | - |
| 0004 | Request all available video devices | - |
| 0005 | Request all available motion devices | - |
| 0006 | Request to stream data for specific audio device | 2 bytes representing uint16 receiving port number, 4 bytes representing audio device ID |
| 0007 | Request to stream data for specific video device | 2 bytes representing uint16 receiving port number, 4 bytes representing video device ID |
| 0008 | Request to stream data for specific motion device | 2 bytes representing uint16 receiving port number, 4 bytes representing motion device ID |
| 0009 | Request to stop streaming data for specific audio device | 4 bytes representing audio device ID |
| 000A | Request to stop streaming data for specific video device | 4 bytes representing video device ID |
| 000B | Request to stop streaming data for specific motion device | 4 bytes representing motion device ID |

### Input IO Devices

| Byte | Designation | Contents |
|-|-|-|
| 0010 | Request whether the block of codes is blocked | - |
| 0011 | Request access to block | [Auth request](./tcp-module-auth) |
| 0012 | Reserved | - |
| 0013 | Request to add audio device | n bytes representing audio device preset |
| 0014 | Request to add video device | n bytes representing video device preset |
| 0015 | Request to add motion device | 4 bytes representing motion device preset |
| 0016 | Request to remove audio device | 4 bytes representing audio device ID |
| 0017 | Request to remove video device | 4 bytes representing video device ID |
| 0018 | Request to remove motion device | 4 bytes representing motion device ID |

n is TBD.

### Plugin Management

| Byte | Designation | Contents |
|-|-|-|
| 0020 | Request whether the block of codes is blocked | - |
| 0021 | Request access to block | [Auth response](./tcp-module-auth) |
| 0022 | Request all plugins on Kijang as JSON | - |
| 0023 | Request all plugins on Kijang as hex list | - |
| 0024 | Request metadata on the specified plugin on Kijang | 4 bytes representing ID of plugin |
