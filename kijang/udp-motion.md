# UDP Motion Protocol (KijangMotion)

This page describe the streaming format that is used to transmit motion data between Kijang and its clients. It is primarily designed to transmit humanoid motion data, but it is also compatible with non-humanoid motion data as well. No timestamps would be provided as the timestamps on the client side would be used when each packet is received.

The coordinates and units system follows that of glTF (See https://www.khronos.org/registry/glTF/specs/2.0/glTF-2.0.html#coordinate-system-and-units):
- +Y is up, +Z is forward, -X is right
- The front of the object faces +Z
- All distance units are in metres
- All angles are in radians
- Positive rotation is counterclockwise

| Starting Byte | Ending Byte | Contents |
|-|-|-|
| 1 | 4 | Identity of bone |
