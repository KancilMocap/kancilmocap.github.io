# Connection Procedure

The proper procedures for connecting to a Kijang-compatible server:
1. Client connects to read port of server
2. Server sends back 6 byte response at read port; First 2 bytes represent write port of server, next 4 bytes represent ID of client
2a. If the server does not send the response within a specific interval (default is 5 seconds), client will automatically disconnect from server
3. Client connects to write port of server
4. Client sends 4 bytes representing ID of client
4a. If the client does not send the appropiate response within a specific interval (default is 5 seconds), server will kick write client off from server but read client would still be online
