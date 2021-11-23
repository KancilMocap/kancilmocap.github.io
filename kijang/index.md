# Kijang

Kijang is the main backend that would be use to process all the sensory inputs and convert them into motion outputs.

## Modular TCP Information Transfer Protocol

The following pages contain information about the protocol for packets that are used to transfer information via a single TCP port.

- [Protocol](./tcp-protocol)
- [Connection Procedures](./connection-procedure)
- [System Modules](./tcp-module-system)
- [KancilMocap Modules](./tcp-module-kancilmocap)
- [Module Authentication](./tcp-module-auth)
- [Module Implementation](https://docs.google.com/spreadsheets/d/1Sq6EpBsYsZIn28BhSFvsJMJmWTyCYuu_7-Skr5m-gWw/edit?usp=sharing).

All servers that use the TCP protocol are expected to handle requests from clients for codes in the system module and respond accordingly. Similarly, this protocol is not limited in its usage within the KancilMocap system, and can be used to transfer data between other applications on the same server and client.

## Sensory Protocols

The following pages contain information about the protocols that are used to transmit sensory data from the server to the client or vice versa.

- [Audio](./udp-audio)
- [Video](./udp-video)
- [Motion](./udp-motion)

## ⚠ Usage of Protocol Across Internet ⚠

Although it is technically possible to use the protocol across the public internet, do note that the protocols by themselves does not come with any form of encryption. Thus, any data sent via the protocol could be intercepted and monitored. Similarly, the audio and video codec are not encrypted by default.
