# Node Uptime & Health Checker

A comprehensive monitoring solution for Cosmos-based blockchain nodes with integrated alerting, metrics, and status dashboard capabilities.

## Overview

Node Uptime & Health Checker is a FastAPI-based service designed to monitor the health and synchronization status of multiple Cosmos blockchain nodes across different networks. It provides real-time monitoring, configurable alerting via Telegram and Pushover, and Prometheus metrics integration.

## Features

- **Multi-Node Monitoring**: Monitor multiple nodes across different networks or node groups
- **Real-Time Status Dashboard**: View the current status of all monitored nodes via API endpoints
- **Intelligent Alerting**: Receive notifications when nodes fall behind or encounter issues
- **Alert Aggregation**: Consolidated status updates for node groups via Telegram
- **Multiple Alert Channels**: Support for Telegram and Pushover notifications
- **Prometheus Integration**: Expose metrics for integration with Prometheus and Grafana
- **Configurable Thresholds**: Customize acceptable block time differences
- **Alert Pause Functionality**: Temporarily pause alerts during maintenance
- **Version Reporting**: Track software versions across your node infrastructure

## API Endpoints

### Node Status
```
GET /api/nodes/statuses
```
Returns the current status of all monitored nodes, grouped by node group.

### Alert Management
```
POST /api/pause
```
Pause alerts for a specified duration during maintenance.

```
GET /api/pause/status
```
Check the current pause status and remaining pause duration.

### Metrics
```
GET /metrics
```
Prometheus-compatible metrics endpoint for integration with monitoring stacks.

## Configuration

The service is configured using a `config.toml` file with the following structure:

```toml
[settings]
max_allowed_behind_seconds = 60
check_interval_seconds = 30

[telegram]
api_key = "your-telegram-bot-api-key"
chat_id = "your-chat-id"
alert_interval_seconds = 300

[telegram_testnet_api]
api_key = "your-testnet-api-telegram-bot-key"
chat_id = "your-testnet-api-chat-id"

[pushover]
api_token = "your-pushover-api-token"
user_key = "your-pushover-user-key"
priority = 1

[pause]
password = "your-secure-password"

[node_groups.mainnet]
alert_types = ["telegram", "pushover"]

[[node_groups.mainnet.nodes]]
name = "Mainnet Node 1"
ip = "123.456.789.0"
port = 26657
endpoint = "/status"

[node_groups.testnet_api]
alert_types = ["telegram"]
great_threshold = 60
good_threshold = 30
telegram_alert_interval_seconds = 1800
rpc = "https://testnet.rpc.example.com"
lcd = "https://testnet.lcd.example.com"
grpc = "https://testnet.grpc.example.com"

[[node_groups.testnet_api.nodes]]
name = "Testnet API Node 1"
ip = "123.456.789.1"
port = 26657
endpoint = "/status"
```

## Background Tasks

The service runs two background tasks:

1. **Periodic Health Check**: Regularly checks the health of all configured nodes
2. **Aggregated Telegram Alerts**: For node groups like `testnet_api`, sends consolidated status updates

## Usage

### Running the Service

```bash
# Start the service
python3 node_monitor.py
```

## Integration

### Prometheus & Grafana
The `/metrics` endpoint provides the following metrics:
- `node_time_difference_seconds`: Time difference between now and the latest block
- `node_health_status`: Node health (1 for healthy, 0 for unhealthy)

### Load Balancers
Use the `/api/nodes/statuses` endpoint to check node health before routing traffic.
