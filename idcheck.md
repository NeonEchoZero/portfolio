# Ethereum Network Identifier

A lightweight Go tool for identifying which Ethereum network a node is operating on by performing P2P protocol handshakes.

## Overview

This tool connects to any Ethereum node via its enode URL and determines which network (Mainnet, Sepolia, Holesky, etc.) it belongs to. It works by:

1. Establishing a TCP connection to the target node
2. Performing an RLPx cryptographic handshake
3. Negotiating the highest supported Ethereum protocol version
4. Exchanging protocol status messages to retrieve the network ID
5. Mapping the network ID to a human-readable network name

## Features

- Implements the complete Ethereum P2P protocol handshake sequence
- Supports all major Ethereum networks (Mainnet, Sepolia, Holesky, etc.)
- Handles protocol negotiation with nodes supporting multiple versions
- Provides detailed connection and handshake information
- Gracefully handles disconnect messages with human-readable reasons

## Usage

```
go run idcheck.go <enode URL>
```

The enode URL format follows the Ethereum node discovery protocol specification:
```
enode://<node-id-hex>@<ip-address>:<port>
```

## Dependencies

- github.com/ethereum/go-ethereum: For the core P2P protocol implementation

## Technical Details

The tool implements several key components of the Ethereum P2P protocol:

1. **RLPx Transport Layer** - Secure encrypted communication channel
2. **Node Discovery Protocol** - For parsing enode URLs
3. **DevP2P Wire Protocol** - Base protocol for peer-to-peer communication
4. **Ethereum Protocol (eth)** - Application-specific protocol for blockchain data


## Example Output

Holesky
```
go run idcheck.go enode://a3435a0155a3e837c02f5e7f5662a2f1fbc25b48e4dc232016e1c51b544cb5b4510ef633ea3278c0e970fa8ad8141e2d4d0f9f95456c537ff05fdf9b31c15072@178.128.136.233:30303
Starting Ethereum network identifier
Connecting to node: ab8122385d3dd781c9d46b19e9da50835f85b512c87ecef985703ca34cc2d250 (178.128.136.233:30303)
TCP connection established
RLPx handshake completed
Protocol handshake sent
Protocol handshake received
Negotiated eth protocol version: 68
Status message sent
Received status with Network ID: 17000
Network: Holesky
```

Holesky
```
go run idcheck.go enode://ac906289e4b7f12df423d654c5a962b6ebe5b3a74cc9e06292a85221f9a64a6f1cfdd6b714ed6dacef51578f92b34c60ee91e9ede9c7f8fadc4d347326d95e2b@146.190.13.128:30303
Starting Ethereum network identifier
Connecting to node: 0db44877fbd32648b5556377f37b8ef9b98b03c5ae287b2c9a06cecd637a628a (146.190.13.128:30303)
TCP connection established
RLPx handshake completed
Protocol handshake sent
Protocol handshake received
Negotiated eth protocol version: 68
Status message sent
Received status with Network ID: 17000
Network: Holesky
```

Hoodi
```
go run idcheck.go enode://8ae4a48101b2299597341263da0deb47cc38aa4d3ef4b7430b897d49bfa10eb1ccfe1655679b1ed46928ef177fbf21b86837bd724400196c508427a6f41602cd@134.199.184.23:30303
Starting Ethereum network identifier
Connecting to node: 903a2b76436a55a0665d3ef337f41e8ed3e4d66ffe3a0f40b444234e96d20e55 (134.199.184.23:30303)
TCP connection established
RLPx handshake completed
Protocol handshake sent
Protocol handshake received
Negotiated eth protocol version: 68
Status message sent
Received status with Network ID: 560048
Network: Unknown (Network ID: 560048)
```

Sepolia
```
go run idcheck.go enode://9e9492e2e8836114cc75f5b929784f4f46c324ad01daf87d956f98b3b6c5fcba95524d6e5cf9861dc96a2c8a171ea7105bb554a197455058de185fa870970c7c@138.68.123.152:30303
Starting Ethereum network identifier
Connecting to node: 21956df73984224e0e9eaf23adc4917813f08bd50be12a91dcfd6664f953e85a (138.68.123.152:30303)
TCP connection established
RLPx handshake completed
Protocol handshake sent
Protocol handshake received
Negotiated eth protocol version: 68
Status message sent
Received status with Network ID: 11155111
Network: Sepolia
```

Mainnet example (too many peers)
```
go run idcheck.go enode://22a8232c3abc76a16ae9d6c3b164f98775fe226f0917b0ca871128a74a8e9630b458460865bab457221f1d448dd9791d24c4e5d88786180ac185df813a68d4de@3.209.45.79:30303
Starting Ethereum network identifier
Connecting to node: f23ac6da7c02f84a425a47414be12dc2f62172cd16bd4c7e7efa02ebaa045605 (3.209.45.79:30303)
TCP connection established
RLPx handshake completed
Protocol handshake sent
Received disconnect message. Raw payload (2 bytes): c104
Error: peer disconnected: Too many peers (code 4)
exit status 1
```
