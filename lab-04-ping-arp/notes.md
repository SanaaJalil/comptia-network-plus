# Lab 04 – Explore Network Layer Interaction with ping and arp

## Commands Used
| Command                  | Purpose                                      |
|--------------------------|----------------------------------------------|
| `arp -a`                 | Display all entries in the ARP cache         |
| `ip route show`          | Display the routing table / find gateway IP  |
| `ping -c 4 <gateway-ip>` | Send 4 packets to a local device             |
| `ping -c 4 google.com`   | Send 4 packets to an external host           |

## Key Concepts

### What is ARP?
- ARP = Address Resolution Protocol
- Maps Layer 3 (IP address) to Layer 2 (MAC address)
- Only works on the LOCAL network segment

### ARP Cache
- Stores known IP-to-MAC mappings to avoid repeated lookups
- Check it with: `arp -a`
- Format: `_gateway (172.16.50.253) at ee:ff:ff:ff:ff:ff [ether] on eth0`

### Local vs Remote Communication
| Destination | ARP Request? | Why?                              |
|-------------|-------------|-----------------------------------|
| Local (gateway) | Yes    | Needs MAC address directly        |
| Remote (google.com) | No | Sends to gateway MAC instead      |

## What I Learned
- ARP cache prevents redundant ARP requests
- For LOCAL traffic → system uses ARP to get MAC of destination
- For REMOTE traffic → system sends to gateway's MAC, not destination's
- Google's IP never appears in ARP cache — only the gateway does
- Default gateway is the intermediary for ALL external traffic
- `ip route show` reveals the gateway IP on the `default via` line
