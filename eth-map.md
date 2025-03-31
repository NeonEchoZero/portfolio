# P2P Network Visualizer

A modern React-based visualization tool for Ethereum P2P network metrics with interactive network topology graphs and geographic distribution maps. This deploys automatically to cloudflare pages from a github repo.

![Status](https://img.shields.io/badge/status-active-success.svg)
![React](https://img.shields.io/badge/React-18.2.0-blue.svg)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.3.2-38B2AC.svg)

## Screenshots

![image](https://github.com/user-attachments/assets/3a48f88f-7a0a-4e35-b2e7-9c7a64097af9)
![image](https://github.com/user-attachments/assets/1e545cc5-7124-4d65-b120-1d0245be5927)
![image](https://github.com/user-attachments/assets/620d24eb-b5b7-4544-9d05-8e5ea2f853aa)

## Overview

P2P Network Visualizer🛰️ is a comprehensive dashboard for visualizing and analyzing peer-to-peer network data from Ethereum nodes. It consumes Prometheus metrics to create interactive visualizations that help operators and researchers understand network topology, peer distribution, and health metrics.

## Features

- **Network Topology Visualization**: Interactive force-directed graph showing bootnode, Kademlia buckets, and peer connections
- **Geographic Distribution**: World map showing peer density across regions with detailed country-level statistics
- **Real-time Metrics**: Dashboard of network health stats including peer counts, reachability, and poll status
- **Historical Trends**: Time-series graphs tracking metrics over time to identify patterns and issues
- **Peer Analysis**: Detailed breakdowns of peer types, connection reliability, and regional distribution
- **Interactive Controls**: Zoom, pan, and filter capabilities for exploring complex network data

## Technology Stack

- **React 18**: Modern component-based architecture
- **TailwindCSS**: Utility-first CSS framework for responsive design
- **Recharts**: Composable charting library for React
- **React Simple Maps**: React components for geographic visualizations
- **D3 Scale**: Scale functions from D3.js for data visualization
- **Vite**: Next-generation frontend tooling for fast development

## Key Visualizations

### Network Graph

The network graph provides a force-directed visualization of the P2P network structure:

- **Bootnode**: Central star-shaped node representing the monitored Ethereum bootnode
- **Kademlia Buckets**: Diamond-shaped nodes representing Kademlia k-buckets
- **Peers**: Circle nodes color-coded by type (reachable, unreachable, known)
- **Connections**: Lines connecting peers to their respective buckets with animated particles for active connections
- **Interactive Elements**: Hover for details, zoom and pan for navigation, physics simulation for natural layout

### Geographic Map

The geographic distribution view offers insights into the global spread of peers:

- **Peer Density**: Color-coded countries showing peer concentration
- **Regional Details**: Country-level statistics including peer counts and reachability
- **Interactive Regions**: Click on countries to view detailed peer listings
- **Custom Navigation**: Region-specific focus options for exploring key areas

### Analytics Panels

Comprehensive analytics panels provide detailed network insights:

- **Peer Type Distribution**: Pie chart showing breakdown of peer types
- **Time Series Analysis**: Line charts tracking key metrics over time
- **Regional Trends**: Area charts showing peer growth across top regions
- **Bucket Distribution**: Bar charts showing peer distribution across Kademlia buckets

## Integration with Ethereum Bootstrap Monitor

This visualization tool is designed to work with the [Ethereum Bootstrap Monitor](./EthereumBootstrapMonitor.md) backend, consuming its Prometheus metrics to generate visualizations. The metrics endpoint provides detailed peer data including:

- Peer counts per Kademlia bucket
- Reachability statistics for all discovered peers 
- Detailed peer metadata including IP addresses and connection history
- Bucket-level discovery statistics
- Monitoring status and health metrics

## Usage

### Configuration

1. Set the Prometheus metrics endpoint URL (default: `https://eth-map.deltaflyer.llc`)
2. Configure the polling interval for real-time updates
3. Select visualization mode (Network Graph or Geographic Map)

### Exploration

- Use zoom and pan controls to navigate visualizations
- Hover over elements to see detailed tooltips
- Toggle between visualization modes for different perspectives
- Check historical trends to identify patterns over time

## Development

### Prerequisites

- Node.js 16.x or higher
- NPM 8.x or higher

## Architecture

The application is organized around these key components:

- **P2PVisualizer**: Main component orchestrating the dashboard
- **GeographicMap**: World map visualization of peer distribution
- **PeerTypeDistribution**: Pie chart showing peer type breakdown
- **TimeSeriesGraph**: Historical trend visualization
- **RegionalTrends**: Geographic distribution trends over time

The network graph visualization uses a custom force simulation to create a natural layout of nodes representing the network topology, while the geographic map leverages React Simple Maps to show global peer distribution.

## Future Enhancements

- Enhanced filtering capabilities for large networks
- Additional visualization modes for specific network characteristics
- Export functionality for reports and sharing
- Real-time alerts for network anomalies
- Extended historical data storage and analysis

## Related Projects

- [Ethereum Bootstrap Monitor](./EthereumBootstrapMonitor.md): Backend service that provides the metrics for this visualization
- [Ethereum Network Identifier](./idcheck.md): Tool for identifying Ethereum networks via P2P handshakes
