# Cosmos Micro

A lightweight health monitoring microservice for Cosmos-based blockchain nodes.

## Overview

Cosmos Micro is a FastAPI-based microservice designed to monitor the health and synchronization status of Cosmos blockchain nodes (with specific support for Cosmos Network nodes). It provides simple HTTP endpoints that can be integrated with monitoring systems, load balancers, or container orchestration platforms to ensure high availability of blockchain infrastructure.

## Features

- **Node Health Monitoring**: Checks if nodes are catching up and validates block time freshness
- **Version Reporting**: Reports the running version of the blockchain daemon (gaiad)
- **Response Caching**: Implements efficient caching to minimize load on the node
- **Configurable Thresholds**: Allows customization of acceptable synchronization delay
- **API-First Design**: RESTful API interface for easy integration with monitoring systems

## API Endpoints

### Health Check
```
GET /health_check
```
Returns a 200 status code if the node is healthy, or a 503 if the node is catching up or behind.

**Example Response (Healthy)**:
```json
{
  "status": "healthy",
  "catching_up": false,
  "latest_block_time": "2023-08-15T12:34:56.789012",
  "time_difference": 2.5,
  "is_healthy": true
}
```

### Version Information
```
GET /version
```
Returns the version of the gaiad daemon running on the host.

**Example Response**:
```json
{
  "version": "v1.9.0"
}
```

## Configuration

Cosmos Micro is configured via a `config.json` file with the following parameters:

```json
{
  "rpc_server": {
    "ip": "127.0.0.1",
    "port": 26657,
    "endpoint": "/status"
  },
  "microservice_port": 8080,
  "max_allowed_behind_seconds": 60
}
```

- `rpc_server`: Configuration for the node's RPC server
- `microservice_port`: Port on which the microservice will listen
- `max_allowed_behind_seconds`: Maximum allowed time difference (in seconds) between the latest block and current time

## Usage

### Running the Service

```bash
# Start the microservice
python3 cosmos_micro.py
```


### Integration with Monitoring Systems

Cosmos Micro can be integrated with monitoring systems like Prometheus, Grafana, or Kubernetes liveness probes to ensure high availability of your blockchain infrastructure.

## Dependencies

- FastAPI: Web framework for building APIs
- httpx: Asynchronous HTTP client
- gaiad: Gaiad (for version reporting)
