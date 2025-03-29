## Approach for "EthereumBootstrapMonitor" in Go

This tool leans on Go’s Discv4 library to query the bootnode for peers with FINDNODE packets and can optionally explore further with random targets. Using Go because of its Discv4/5 library, seems like the path of least resistance.

## Configuration Strategy

Has two configuration files: `config.json` and `ip_list.json`.

### Core Objectives

- Track whether any peer with an IP from the ip list has ever been known to the bootnode
- Expose Prometheus gauges: query success (1/0), peer count, IP presence (per-IP labels)
- IP List: Reads ip list at startup.
- Prometheus Metrics: Indicate if the bootnode query succeeded (1) or failed (0). Show if a peer with a specific IP has ever been known to the bootnode (per-IP labels)
- Ansible Deployment: Use a playbook to automate setup—compiling the Go binary (if not already compiled), copying files, and configuring a systemd service. To ensure repeatability and easy adjustment for similar tools

### How It Works

1. **Startup**:
   - Loads configuration from `config.json` or command-line flags.
   - Loads custom list of IPs, to indicates whether a peer with IP from said Configurable List has been “Known” to the bootnode.
   - Starts a Prometheus metrics server on the specified port (e.g., `9090`).

2. **Monitoring Loop** (Every `interval` Seconds, e.g., 300):
   - Performs peer discovery using enabled methods:
     - Always: Direct lookup of the bootnode with *custom* FINDNODE packets to grab its known peers.
     - Optional: Lookup using random public keys to explore the network further (configurable).
     - Combines all peers found, weeds out duplicates, and pings them to see who’s alive.
   - Updates metrics with:
     - `bootnode_known_peers`: Total unique peers found in the last poll.
     - `bootnode_unreachable_peers`: Number of peers that didn’t respond to pings.
     - `bootnode_last_poll_timestamp`: When the last poll happened (Unix timestamp).
     - `bootnode_poll_duration_seconds`: How long the last poll took.
     - `bootnode_poll_count`: How many polls have run total.
     - `bootnode_poll_success`: Was the last poll successful?
     - `bootnode_total_unique_peers`: Total number of unique peers seen since service start.
     - `bootnode_peers_from_bootnode_lookup`: Number of peers discovered from direct bootnode lookup in the last poll.
     - `bootnode_peers_from_random_targets`: Number of peers discovered from random target lookups in the last poll.
     - `bootnode_discovery_method_success`: Success count of different discovery methods (labels: "method").
     - `bootnode_known_peer_by_ip`: Indicates whether a peer with the specified IP has ever been known to the bootnode (1 = yes, 0 = no)—tracks this across all polls, not just the last one.
     - `bootnode_peers_per_bucket`: Number of new peers discovered in each Kademlia bucket (not the cumulative total across all polls) during the last poll (labels: "bucket").

3. **Error Handling**:
   - If bootnode lookup fails (e.g., it’s down or unreachable), logs the error and aborts the poll. Other errors are logged and ignored.
   - If no peers are found, logs the result and updates metrics with `0` peers.

### Go Application Code (`main.go`)

See `EthereumBootstrapMonitor/main.go`

### Example Config File

Setting `random_targets_per_poll=0`, `concurrent_discovery_limit=0`, and `enable_random_targets=false` makes the tool only talk to bootstrap nodes (so no crawling). These same options `random_targets_per_poll`, `concurrent_discovery_limit`, and `enable_random_targets` control the random target feature which enables crawling the broader network beyond the bootstrap node.

Save this as `config.json`— or run `go run main.go -generate-config config.json`:

For all buckets.
```json
{
    "bootnode_address": "enode://22a8232c3abc76a16ae9d6c3b164f98775fe226f0917b0ca871128a74a8e9630b458460865bab457221f1d448dd9791d24c4e5d88786180ac185df813a68d4de@3.209.45.79:30303",
    "poll_interval": "2h",
    "prometheus_port": 9090,
    "random_targets_per_poll": 0,
    "concurrent_discovery_limit": 0,
    "enable_random_targets": false,
    "target_buckets": [
        255, 254, 253, 252, 251, 250, 249, 248, 247, 246, 245, 244, 243, 242, 241, 240,
        239, 238, 237, 236, 235, 234, 233, 232, 231, 230, 229, 228, 227, 226, 225, 224,
        223, 222, 221, 220, 219, 218, 217, 216, 215, 214, 213, 212, 211, 210, 209, 208,
        207, 206, 205, 204, 203, 202, 201, 200, 199, 198, 197, 196, 195, 194, 193, 192,
        191, 190, 189, 188, 187, 186, 185, 184, 183, 182, 181, 180, 179, 178, 177, 176,
        175, 174, 173, 172, 171, 170, 169, 168, 167, 166, 165, 164, 163, 162, 161, 160,
        159, 158, 157, 156, 155, 154, 153, 152, 151, 150, 149, 148, 147, 146, 145, 144,
        143, 142, 141, 140, 139, 138, 137, 136, 135, 134, 133, 132, 131, 130, 129, 128,
        127, 126, 125, 124, 123, 122, 121, 120, 119, 118, 117, 116, 115, 114, 113, 112,
        111, 110, 109, 108, 107, 106, 105, 104, 103, 102, 101, 100, 99, 98, 97, 96,
        95, 94, 93, 92, 91, 90, 89, 88, 87, 86, 85, 84, 83, 82, 81, 80,
        79, 78, 77, 76, 75, 74, 73, 72, 71, 70, 69, 68, 67, 66, 65, 64,
        63, 62, 61, 60, 59, 58, 57, 56, 55, 54, 53, 52, 51, 50, 49, 48,
        47, 46, 45, 44, 43, 42, 41, 40, 39, 38, 37, 36, 35, 34, 33, 32,
        31, 30, 29, 28, 27, 26, 25, 24, 23, 22, 21, 20, 19, 18, 17, 16,
        15, 14, 13, 12, 11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0
    ]
}
```

For several buckets (e.g 0 - 8)
```json
{
    "bootnode_address": "enode://22a8232c3abc76a16ae9d6c3b164f98775fe226f0917b0ca871128a74a8e9630b458460865bab457221f1d448dd9791d24c4e5d88786180ac185df813a68d4de@3.209.45.79:30303",
    "poll_interval": "2h",
    "prometheus_port": 9090,
    "random_targets_per_poll": 0,
    "concurrent_discovery_limit": 0,
    "enable_random_targets": false,
    "target_buckets": [
        0, 1, 2, 2, 4, 5, 6, 7, 8
    ]
}
```

### Example IP List

Save this as `ip_list.json`
```json
["71.163.116.174", "5.9.138.178", "135.148.20.58", "135.181.235.137", "82.25.56.60", "185.141.166.77", "47.252.1.1", "148.251.216.1", "42.3.104.159", "42.3.104.159", "3.12.28.21", "135.181.65.227", "82.25.58.43", "43.131.14.27", "62.92.48.118", "135.148.20.99", "148.251.216.4", "34.121.115.125", "148.251.216.1", "86.109.2.93", "138.201.38.33"]
```

### Run it manually

Init:
```bash
go mod init EthereumBootstrapMonitor
go mod tidy
```

Run it manually to test:
```bash
go run main.go -bootnode "enode://22a8232c3abc76a16ae9d6c3b164f98775fe226f0917b0ca871128a74a8e9630b458460865bab457221f1d448dd9791d24c4e5d88786180ac185df813a68d4de@3.209.45.79:30303"
```

### Ansible Playbook for Deployment

This playbook automates - building the app, replace the config.json & ip_list.json in the /etc/Ethereum Bootstrap Monitor directory with the ones from the directory the playbook runs from, deploys it to the target server (default is `localhost`), and sets it up as a systemd service.

#### Playbook

see `deploy_EthereumBootstrapMonitor.yml`

#### Inventory (`inventory.ini`)
```ini
[local]
localhost ansible_connection=local
```

#### Running the Playbook
With Ansible installed, you can run:
```bash
ansible-playbook -i inventory.ini deploy_EthereumBootstrapMonitor.yml --ask-become-pass
```

This sets up everything—binary, configs, and service—on `localhost`.

### Systemd Service

The playbook creates `/etc/systemd/system/Ethereum Bootstrap Monitor.service` with:
- **Description**: Ethereum EthereumBootstrapMonitor Monitor
- **Runs After**: `network.target` (waits for network to be up)
- **Executes**: `/usr/local/bin/Ethereum_Bootstrap_Monitor -config /etc/Ethereum_Bootstrap_Monitor/config.json`
- **User**: Runs as `Ethereum Bootstrap Monitor`.
- **Restart Policy**: Restarts on failure.
- **Startup**: Enabled at boot via `multi-user.target`

### Prometheus Metrics

Grep `http://localhost:9090/metrics` (or whatever port you set):

```
curl -s http://localhost:9090/metrics | grep "bootnode_"
# HELP bootnode_discovery_method_success Success count of different discovery methods
# TYPE bootnode_discovery_method_success counter
bootnode_discovery_method_success{method="direct_bootnode_findnode"} 1
# HELP bootnode_known_peer_by_ip Indicates whether a peer with the specified IP has ever been known to the bootnode (1 = yes, 0 = no)
# TYPE bootnode_known_peer_by_ip gauge
bootnode_known_peer_by_ip{ip="135.148.20.58"} 1
bootnode_known_peer_by_ip{ip="135.148.20.99"} 1
bootnode_known_peer_by_ip{ip="135.181.235.137"} 1
bootnode_known_peer_by_ip{ip="135.181.65.227"} 1
bootnode_known_peer_by_ip{ip="138.201.38.33"} 1
bootnode_known_peer_by_ip{ip="148.251.216.1"} 0
bootnode_known_peer_by_ip{ip="148.251.216.4"} 0
bootnode_known_peer_by_ip{ip="185.141.166.77"} 0
bootnode_known_peer_by_ip{ip="3.12.28.21"} 1
bootnode_known_peer_by_ip{ip="34.121.115.125"} 0
bootnode_known_peer_by_ip{ip="42.3.104.159"} 1
bootnode_known_peer_by_ip{ip="43.131.14.27"} 1
bootnode_known_peer_by_ip{ip="47.252.1.1"} 0
bootnode_known_peer_by_ip{ip="5.9.138.178"} 0
bootnode_known_peer_by_ip{ip="62.92.48.118"} 0
bootnode_known_peer_by_ip{ip="71.163.116.174"} 0
bootnode_known_peer_by_ip{ip="82.25.56.60"} 0
bootnode_known_peer_by_ip{ip="82.25.58.43"} 1
bootnode_known_peer_by_ip{ip="86.109.2.93"} 0
# HELP bootnode_known_peers Number of peers known to the monitored bootnode (last poll)
# TYPE bootnode_known_peers gauge
bootnode_known_peers 64
# HELP bootnode_last_poll_timestamp Timestamp of the last successful poll
# TYPE bootnode_last_poll_timestamp gauge
bootnode_last_poll_timestamp 1.743265407e+09
# HELP bootnode_peers_from_bootnode_lookup Number of peers discovered from direct bootnode lookup
# TYPE bootnode_peers_from_bootnode_lookup gauge
bootnode_peers_from_bootnode_lookup 64
# HELP bootnode_peers_from_random_targets Number of peers discovered from random target lookups
# TYPE bootnode_peers_from_random_targets gauge
bootnode_peers_from_random_targets 0
# HELP bootnode_peers_per_bucket Number of peers discovered in each Kademlia bucket
# TYPE bootnode_peers_per_bucket gauge
bootnode_peers_per_bucket{bucket="0"} 16
bootnode_peers_per_bucket{bucket="1"} 16
bootnode_peers_per_bucket{bucket="2"} 16
bootnode_peers_per_bucket{bucket="3"} 16
# HELP bootnode_poll_count Total number of polling operations performed
# TYPE bootnode_poll_count counter
bootnode_poll_count 1
# HELP bootnode_poll_duration_seconds Duration of the last polling operation in seconds
# TYPE bootnode_poll_duration_seconds gauge
bootnode_poll_duration_seconds 35.846901127
# HELP bootnode_poll_success 1 if the last poll was successful, 0 otherwise
# TYPE bootnode_poll_success gauge
bootnode_poll_success 1
# HELP bootnode_total_unique_peers Total number of unique peers seen since service start
# TYPE bootnode_total_unique_peers gauge
bootnode_total_unique_peers 64
# HELP bootnode_unreachable_peers Number of unreachable peers from the last poll
# TYPE bootnode_unreachable_peers gauge
bootnode_unreachable_peers 3
```
