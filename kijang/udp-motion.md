# UDP Motion Protocol (KijangMotion)

This page describe the streaming format that is used to transmit motion data between Kijang and its clients. It is primarily designed to transmit humanoid motion data, but it is also compatible with non-humanoid motion data as well. No timestamps would be provided as the timestamps on the client side would be used when each packet is received.

The coordinates and units system follows that of glTF (See https://www.khronos.org/registry/glTF/specs/2.0/glTF-2.0.html#coordinate-system-and-units):
- +Y is up, +Z is forward, -X is right
- The front of the object faces +Z
- All distance units are in metres
- All angles are in radians
- Positive rotation is counterclockwise

Each UDP packet consist of multiple segments of data points, with each data point consisting of 3 IEEE-754 floats representing the absolute X, Y and Z coordinate of the data point. The float values can either be binary32 or binary64, which should be agreed upon between the client and server via an external method (eg. TCP status server)
The absolute zero point (0, 0, 0) within the tracking system is determined by the server.

For example, tracking an object with 3 data points using binary64 would result in the following UDP packet being sent:

| Starting byte | Ending byte | Description |
|-|-|-|
| 1 | 8 | Data Point 1, X coordinate |
| 9 | 16 | Data Point 1, Y coordinate |
| 17 | 24 | Data Point 1, Z coordinate |
| 25 | 32 | Data Point 2, X coordinate |
| 33 | 40 | Data Point 2, Y coordinate |
| 41 | 48 | Data Point 2, Z coordinate |
| 49 | 56 | Data Point 3, X coordinate |
| 57 | 64 | Data Point 3, Y coordinate |
| 65 | 72 | Data Point 3, Z coordinate |

Tracking another object with 2 data points using binary32 would result in the following TCP packet being sent:

| Starting byte | Ending byte | Description |
|-|-|-|
| 1 | 4 | Data Point 1, X coordinate |
| 5 | 8 | Data Point 1, Y coordinate |
| 9 | 12 | Data Point 1, Z coordinate |
| 13 | 16 | Data Point 2, X coordinate |
| 17 | 20 | Data Point 2, Y coordinate |
| 21 | 24 | Data Point 2, Z coordinate |

A calculator to calculate the required ethernet capacity as well as the maximum possible sample rate could be found [here](./motion-calculator.html).

The order of the data points and their corresponding meaning shoould be agreed upon by the client and server externally. In Kijang, motion presets identified by a 4 byte unsigned integer (quint32) are used to represent a set of data points.
