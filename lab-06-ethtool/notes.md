# Lab 06 – Examine Network Interface Settings with ethtool

## Commands Used
| Command                                      | Purpose                                      |
|----------------------------------------------|----------------------------------------------|
| `sudo apt install ethtool -y`                | Install ethtool                              |
| `ip a`                                       | List all interfaces, find primary one        |
| `ethtool eth0`                               | View speed
# Lab 06 – Examine Network Interface Settings with ethtool

## Commands Used
| Command                                      | Purpose                                      |
|----------------------------------------------|----------------------------------------------|
| `sudo apt install ethtool -y`                | Install ethtool                              |
| `ip a`                                       | List all interfaces, find primary one        |
| `ethtool eth0`                               | View speed, duplex, auto-negotiation         |
| `sudo ethtool -s eth0 speed 10 duplex half`  | Manually set speed to 10Mbps half-duplex     |
| `ethtool -k eth0`                            | View hardware offload features               |
| `sudo ethtool -K eth0 tx-checksumming off`   | Disable TX checksumming                      |
| `sudo ethtool -K eth0 tx-checksumming on`    | Re-enable TX checksumming                    |
| `ethtool -S eth0`                            | View interface statistics (packets/bytes)    |

## Key Concepts

### Speed & Duplex
- **Half-duplex** = send OR receive at a time, not both
- **Full-duplex** = send AND receive simultaneously (modern standard)
- **Auto-negotiation** = NIC and switch agree on best speed/duplex automatically
- Forcing wrong settings = duplex mismatch = degraded performance

### Hardware Offload Features (-k / -K)
- Offload = NIC handles tasks instead of CPU (improves performance)
- `[fixed]` = cannot be changed by user
- Disabling one feature may auto-disable dependent features
- Common offload features: rx/tx checksumming, TCP segmentation, scatter-gather

### Interface Statistics (-S)
- Shows per-queue packet and byte counters
- `rx_queue_*` = received traffic
- `tx_queue_*` = transmitted traffic
- Error counters increasing = sign of a problem
- Use to verify link health during troubleshooting

## What I Learned
- ethtool operates at Layer 1 (Physical layer)
- `Link detected: yes` confirms physical cable/connection is active
- Manual speed/duplex only needed for legacy hardware or troubleshooting
- `netlink error: Operation not permitted` is normal in virtual environments
- Statistics change after generating traffic (e.g. ping)
- Always re-enable offload features after testing to restore performance
