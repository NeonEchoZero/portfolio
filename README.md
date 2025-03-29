# Blockchain Infrastructure Monitoring Portfolio

This repository contains a suite of some of my custom-built tools designed to solve specific challenges in blockchain infrastructure monitoring.

### 🛠️ Tools Collection

| Tool | Ecosystem | Language | Description |
|------|-----------|----------|-------------|
| [Ethereum Network Identifier](#ethereum-network-identifier) | Ethereum | Go | Identifies Ethereum networks via P2P protocol handshakes |
| [Ethereum Bootstrap Monitor](#ethereum-bootstrap-monitor) | Ethereum | Go | Monitors Ethereum bootnode peer discovery |
| [Node Uptime & Health Checker](#node-uptime--health-checker) | Cosmos | Python | Comprehensive node monitoring with alerting |
| [Cosmos Micro](#cosmos-micro) | Cosmos | Python | Lightweight node health monitoring microservice |

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

## 💻 Technology Stack

These projects covers proficiency with the following technologies:

- **Languages**: Go, Python
- **Blockchain Ecosystems**: Ethereum, Cosmos
- **Monitoring Tools**: Prometheus, Grafana
- **Alerting Systems**: Telegram, Pushover
- **Web Frameworks**: FastAPI
- **Protocols**: Ethereum P2P, DevP2P, RLPx, Discv4, Cosmos RPC
- **Deployment**: Systemd, Ansible, Docker
