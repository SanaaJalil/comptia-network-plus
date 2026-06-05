# Lab 05 – Simulate Network Layer Connectivity in Linux

## Commands Used
| Command                                        | Purpose                                      |
|------------------------------------------------|----------------------------------------------|
| `docker network create --subnet=192.168.56.0/24 lab_net` | Create a virtual network        |
| `docker run -d --name node1 --network lab_net --cap-add=NET_ADMIN ubuntu:22.04 sleep infinity` | Launch node1 |
| `docker exec node1 apt-get install -y iproute2 iputils-ping` | Install networking tools |
| `docker exec node1 ip addr show eth0`          | Show network config of node1                 |
| `docker exec node1 ip addr add 192.168.56.10/24 dev eth0` | Assign static IP to node1       |
| `docker exec node1 ping -c 4 192.168.56.11`   | Ping node2 from node1                        |
| `docker exec node2 ip addr flush dev eth0`     | Remove all IPs from node2                    |
| `docker exec node2 ip addr add 192.168.58.11/24 dev eth0` | Assign new subnet IP to node2   |

## Lab Setup
- Two Docker containers (node1, node2) simulating separate network nodes
- Connected via a custom Docker bridge network: `lab_net`
- `--cap-add=NET_ADMIN` required to modify network settings inside containers

## Key Concepts

### Same Subnet = Direct Communication
- node1: `192.168.56.10/24`
- node2: `192.168.56.11/24`
- Both on `192.168.56.0/24` → ping succeeds ✅

### Different Subnet = No Direct Communication
- node1: `192.168.56.10/24`
- node2: `192.168.58.11/24` (different subnet)
- ping fails ❌

## Two Types of Failure
| Direction         | Error                          | Why                                              |
|-------------------|--------------------------------|--------------------------------------------------|
| node1 → node2     | 100% packet loss (timeout)     | Packet sent but no route back for reply          |
| node2 → node1     | Network is unreachable         | OS checked routing table, found no path at all   |

## What I Learned
- Devices on the SAME subnet can communicate directly (no router needed)
- Devices on DIFFERENT subnets need a Layer 3 router to communicate
- `ip addr flush` removes ALL IPs and routes from an interface
- "Network is unreachable" = OS refused to send, no route exists
- "100% packet loss" = packet sent but no reply came back
- /24 = subnet mask 255.255.255.0 (third octet must match for same subnet)
