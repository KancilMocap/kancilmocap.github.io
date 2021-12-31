# Connection Procedure

The proper procedures for connecting to a Kijang-compatible server are as follows:
1. The client would connect to the read port of the server.
2. The server would send back a 6 byte response at the read port; The first 2 bytes represent the uint16 write port of server (Big Endian), the next 4 bytes would represent the ID of the client.
2a. If the server does not send the response within a specific interval (default is 5 seconds), the client will automatically disconnect from the server.
3. The client would connect to the write port of the server.
4. The client sends 4 bytes representing its ID to the write port of the server.
4a. If the client does not send the appropiate response within a specific interval (default is 5 seconds), the server will kick the client off the write port but the client at the read port would still be online. The client may choose to disconnect or try to connect to the write server again. In Pilandok and KancilMocap, the client would disconnect once the write client has been terminated.

Note: Appropiate measures should be taken to ensure that the read and write client are from the same device. Currently, the server would check if the IP address of the read and write client matches.
