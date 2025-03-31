# Infrastructure Portfolio

A suite of custom-built tools designed to solve specific challenges in infrastructure monitoring and management.

## 🛠️ Tools Collection

| Tool | Ecosystem | Language | Description |
|------|-----------|----------|-------------|
| [Ethereum Network Identifier](./idcheck.md) | Ethereum | Go | Identifies Ethereum networks via P2P protocol handshakes |
| [Ethereum Bootstrap Monitor](./EthereumBootstrapMonitor.md) | Ethereum | Go | Monitors Ethereum bootnode peer discovery |
| [Node Uptime & Health Checker](./Node_Uptime_and_Health_Checker.md) | Cosmos | Python | Comprehensive node monitoring with alerting |
| [Node Health Dashboard](./Node_Uptime_and_Health_Checker-frontend.md) | Cosmos | React/JavaScript | Frontend dashboard for the Node Uptime & Health Checker |
| [Cosmos Micro](./cosmosmicro.md) | Cosmos | Python | Lightweight node health monitoring microservice |
| [P2P Network Visualizer](./eth-map.md) | Ethereum | React/JavaScript | Interactive visualization of P2P network metrics |

## 🌟 Featured Projects

### Ethereum Network Identifier

A lightweight Go tool for identifying which Ethereum network a node is operating on by performing P2P protocol handshakes. Implements the complete Ethereum P2P protocol handshake sequence to determine if a node belongs to Mainnet, Sepolia, Holesky, or other networks.

**Key Features:**
- Implements complete Ethereum P2P protocol handshake sequence
- Supports all major Ethereum networks (Mainnet, Sepolia, Holesky, etc.)
- Handles protocol negotiation with nodes supporting multiple versions
- Provides detailed connection and handshake information

[View Details](./idcheck.md)

### Ethereum Bootstrap Monitor

A specialized Go tool for monitoring Ethereum bootnode peer discovery and network health through Discv4 protocol interactions. Tracks peer discovery across Kademlia buckets, monitors bootnode responsiveness, and exports comprehensive Prometheus metrics.

**Key Features:**
- Tracks peer discovery across Kademlia buckets
- Monitors bootnode responsiveness and peer availability
- Exports comprehensive Prometheus metrics
- Tracks specific IP addresses for network monitoring
- Configurable discovery parameters

[View Details](./EthereumBootstrapMonitor.md)

### Node Uptime & Health Checker

A comprehensive monitoring solution for Cosmos-based blockchain nodes with integrated alerting, metrics, and status dashboard capabilities.

**Key Features:**
- Multi-node monitoring across different networks
- Real-time status dashboard via API endpoints
- Intelligent alerting via Telegram and Pushover
- Alert aggregation for node groups
- Prometheus metrics integration
- Configurable thresholds and maintenance mode

[View Details](./Node_Uptime_and_Health_Checker.md)

### Node Health Dashboard

A modern React-based frontend for the Node Uptime & Health Checker service, providing a real-time visual interface to monitor blockchain node health across multiple networks.

**Key Features:**
- Real-time node status monitoring with auto-refresh
- Multi-network support with organized display
- Status visualization with color-coded indicators
- Version tracking across node infrastructure
- Alert management with pause functionality
- Responsive design for desktop and mobile

[View Details](./Node_Uptime_and_Health_Checker-frontend.md)

### Cosmos Micro

A lightweight health monitoring microservice for Cosmos-based blockchain nodes, designed for integration with container orchestration and load balancers.

**Key Features:**
- Node health monitoring with sync status checking
- Version reporting of blockchain daemon
- Response caching for efficiency
- Configurable synchronization thresholds
- RESTful API for monitoring integration

[View Details](./cosmosmicro.md)

### P2P Network Visualizer

An interactive React-based visualization tool for Ethereum P2P network metrics. Provides real-time network topology visualization, geographic distribution maps, and comprehensive analytics for peer discovery and network health monitoring.

**Key Features:**
- Interactive network topology graph with force-directed simulation
- Geographic map showing global peer distribution
- Time-series analysis of network performance metrics
- Peer type distribution and reliability statistics
- Integration with Ethereum Bootstrap Monitor metrics

[View Details](./eth-map.md)


## 💻 Technology Stack

This portfolio leverages the following technologies:

- **Languages**: Go, Python, JavaScript/React
- **Blockchain Ecosystems**: Ethereum, Cosmos, Bitcoin
- **Monitoring Tools**: Prometheus, Grafana
- **Visualization**: React, D3.js, Recharts, React Simple Maps
- **Alerting Systems**: Telegram, Pushover
- **Web Frameworks**: FastAPI, React
- **Security Technologies**: Intel SGX, Threshold Cryptography
- **Protocols**: Ethereum P2P, DevP2P, RLPx, Discv4, Cosmos RPC, Bitcoin transactions
- **Deployment**: Systemd, Ansible, Docker

## 📊 Use Cases

These tools are designed for infrastructure operators, developers, and researchers who need:

- Network health monitoring and alerting for validators and nodes
- Peer discovery and network topology analysis
- Cross-chain communication and asset management
- Visual insights into distributed network behavior
- Integration with existing monitoring stacks (Prometheus/Grafana)
- Secure cross-chain asset management
