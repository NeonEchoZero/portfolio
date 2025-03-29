# Node Health Dashboard

A modern React-based frontend for the Node Uptime & Health Checker service, providing a real-time visual interface to monitor blockchain node health across multiple networks.

## Overview

Node Health Dashboard is a responsive web application that connects to the Node Uptime & Health Checker backend API to display the current status and health metrics of Cosmos-based blockchain nodes. The dashboard offers a clean, intuitive interface for monitoring node performance, with support for alert management and real-time status updates.

## Features

- **Real-time Node Status Monitoring**: View the status of all monitored nodes with automatic refresh every 10 seconds
- **Multi-network Support**: Organized display of nodes grouped by network (mainnet, testnet, etc.)
- **Status Visualization**: Color-coded status indicators for quick health assessment
- **Version Tracking**: Display current software versions across your node infrastructure
- **Alert Management**: Pause notifications during scheduled maintenance
- **Countdown Timer**: Real-time display of remaining time when alerts are paused
- **Responsive Design**: Optimized layout for both desktop and mobile viewing
- **Error Handling**: Graceful degradation when backend services are unavailable

## Technology Stack

- **React 18**: Modern component-based UI architecture
- **Tailwind CSS**: Utility-first CSS framework for responsive design
- **Lucide Icons**: Lightweight icon library for UI elements
- **Fetch API**: For communication with the backend service

## Getting Started

### Prerequisites

- Node.js 16.x or higher
- NPM 8.x or higher
- Backend API (Node Uptime & Health Checker) running and accessible


## Usage

### Viewing Node Status

The dashboard automatically displays all node groups and their respective nodes with the following information:
- Node name
- Software version
- Current status (healthy, unhealthy, or error)
- Latest block time
- Time difference between latest block and current time

### Managing Alerts

To pause alerts during scheduled maintenance:

1. Click the "Pause Alerts" button
2. Enter your pause password when prompted
3. Specify the duration (in seconds) for the pause
4. A countdown timer will appear showing the remaining pause time

## Integration with Backend

This dashboard is designed to work with the Node Uptime & Health Checker backend. It interacts with the following API endpoints:

- `GET /api/nodes/statuses`: Retrieves the current status of all monitored nodes
- `GET /api/pause/status`: Checks if alerts are currently paused and the remaining duration
- `POST /api/pause`: Pauses alerts for a specified duration

For full backend documentation, see [Node Uptime & Health Checker](./Node_Uptime_and_Health_Checker.md).

## Customization

### Styling

The application uses Tailwind CSS for styling. To customize the appearance:

1. Modify the color scheme in `tailwind.config.js`
2. Update class names in `App.js` to change the layout and styling

### Adding Features

The codebase is organized to make feature additions straightforward:

- Add new components in the `src` directory
- Extend the main `App.js` file to include new functionality
- Update the state management as needed for additional data requirements
