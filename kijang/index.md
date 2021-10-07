# Kijang

Kijang is the main backend that would be use to process all the sensory inputs and convert them into motion outputs.

## TCP Protocol

The following pages contain information about the protocol for packets that are used to transfer information between Kijang and other application in the communication port.

- [Protocol](./tcp-protocol)
- [Modules](./tcp-modules)

## Sensory Protocols

The following pages contain information about the protocols that are used to transmit sensory data from the server to the client or vice versa.

- [Audio](./udp-audio)
- [Video](./udp-video)
- [Motion](./udp-motion)

## Warning: Usage of Protocol Across Internet

Although it is technically possible to use the protocol across the public internet, do note that the protocol by itself does not come with any form of encryption. Thus, any data sent via the protocol could be intercepted and monitored.
