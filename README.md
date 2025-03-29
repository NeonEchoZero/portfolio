# Blockchain Infrastructure Monitoring Portfolio

This repository contains a suite of some of my custom-built tools designed to solve specific challenges in blockchain infrastructure monitoring.

### 🛠️ Tools Collection

| Tool | Ecosystem | Language | Description |
|------|-----------|----------|-------------|
| [Ethereum Network Identifier](#ethereum-network-identifier) | Ethereum | Go | Identifies Ethereum networks via P2P protocol handshakes |
| [Ethereum Bootstrap Monitor](#ethereum-bootstrap-monitor) | Ethereum | Go | Monitors Ethereum bootnode peer discovery |
| [Node Uptime & Health Checker](#node-uptime--health-checker) | Cosmos | Python | Comprehensive node monitoring with alerting |
| [Node Health Dashboard](#node-health-dashboard) | Cosmos | React/JavaScript | Frontend dashboard for the Node Uptime & Health Checker |
| [Cosmos Micro](#cosmos-micro) | Cosmos | Python | Lightweight node health monitoring microservice |
| [BitcoinEVM](#bitcoinevm) | Bitcoin/EVM | Go | Secure Bitcoin asset management for EVM chain validators |

## Ethereum Network Identifier

A lightweight Go tool for identifying which Ethereum network a node is operating on by performing P2P protocol handshakes.

### Key Features
- Implements complete Ethereum P2P protocol handshake sequence
- Supports all major Ethereum networks (Mainnet, Sepolia, Holesky, etc.)
- Handles protocol negotiation with nodes supporting multiple versions
- Provides detailed connection and handshake information

### Use Cases
- Verify network identity of peer nodes before connecting
- Troubleshoot connectivity issues between networks
- Validate correct network deployment

[View Project Details](./idcheck.md)

## Ethereum Bootstrap Monitor

A specialized Go tool for monitoring Ethereum bootnode peer discovery and network health through Discv4 protocol interactions.

### Key Features
- Tracks peer discovery across Kademlia buckets
- Monitors bootnode responsiveness and peer availability
- Exports comprehensive Prometheus metrics
- Tracks specific IP addresses for network monitoring
- Configurable discovery parameters

### Use Cases
- Bootnode health monitoring
- Network connectivity validation
- Peer discovery troubleshooting
- Network growth analysis

[View Project Details](./EthereumBootstrapMonitor.md)

## Node Uptime & Health Checker

A comprehensive monitoring solution for Cosmos-based blockchain nodes with integrated alerting, metrics, and status dashboard capabilities.

### Key Features
- Multi-node monitoring across different networks
- Real-time status dashboard via API endpoints
- Intelligent alerting via Telegram and Pushover
- Alert aggregation for node groups
- Prometheus metrics integration
- Configurable thresholds and maintenance mode

### Use Cases
- Production node infrastructure monitoring
- DevOps integrations for high availability
- Network status visualization
- Alert management for operations teams

[View Project Details](./Node_Uptime_and_Health_Checker.md)

## Node Health Dashboard

A modern React-based frontend for the Node Uptime & Health Checker service, providing a real-time visual interface to monitor blockchain node health across multiple networks.

### Key Features
- Real-time node status monitoring with auto-refresh
- Multi-network support with organized display
- Status visualization with color-coded indicators
- Version tracking across node infrastructure
- Alert management with pause functionality
- Responsive design for desktop and mobile

### Use Cases
- Operations center monitoring displays
- DevOps team status monitoring
- Quick health assessment during incidents
- Remote node monitoring from any device

[View Project Details](./Node_Uptime_and_Health_Checker-frontend.md)

## Cosmos Micro

A lightweight health monitoring microservice for Cosmos-based blockchain nodes, designed for integration with container orchestration and load balancers.

### Key Features
- Node health monitoring with sync status checking
- Version reporting of blockchain daemon
- Response caching for efficiency
- Configurable synchronization thresholds
- RESTful API for monitoring integration

### Use Cases
- Kubernetes liveness/readiness probes
- Load balancer health checks
- Microservice architecture integration
- Simple health monitoring

[View Project Details](./cosmosmicro.md)

## BitcoinEVM

A sophisticated system designed to allow validators on a custom EVM chain to securely control Bitcoin assets using Intel SGX enclaves.

### Key Features
- Secure key management using SGX enclaves
- Threshold cryptography with n-of-m signing
- Transaction signing for Bitcoin triggered by EVM smart contracts
- Cryptographic attestation of enclave integrity
- Phased implementation approach from testnet to multi-node mainnet

### Use Cases
- Cross-chain asset management
- Trustless Bitcoin bridging to EVM chains
- Secure multi-party transaction signing
- Decentralized custody solutions

[View Project Details](./BitcoinEVM.md)

## 💻 Technology Stack

These projects covers proficiency with the following technologies:

- **Languages**: Go, Python, JavaScript/React
- **Blockchain Ecosystems**: Ethereum, Cosmos, Bitcoin
- **Monitoring Tools**: Prometheus, Grafana
- **Alerting Systems**: Telegram, Pushover
- **Web Frameworks**: FastAPI, React
- **Security Technologies**: Intel SGX, Threshold Cryptography
- **Protocols**: Ethereum P2P, DevP2P, RLPx, Discv4, Cosmos RPC, Bitcoin transactions
- **Deployment**: Systemd, Ansible, Docker
