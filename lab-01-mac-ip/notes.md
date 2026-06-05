# Lab 01 – Identify MAC and IP Addresses in Linux

## Commands Used
| Command                  | Purpose                              |
|--------------------------|--------------------------------------|
| `ip a`                   | Display all network interfaces       |
| `ip a | grep "link/ether"` | Filter and show only MAC addresses |
| `ip a | grep "inet "`    | Filter and show only IPv4 addresses  |
| `ip a | grep "inet6"`    | Filter and show only IPv6 addresses  |

## Network Interfaces
- `lo`      – loopback interface, system talks to itself (127.0.0.1)
- `eth0`    – primary Ethernet interface, connects to external network
- `docker0` – virtual bridge created by Docker for containers

## How to Read ip a Output
- `link/ether` → MAC address (unique hardware identifier, 12 hex digits)
- `inet`       → IPv4 address (e.g. 172.16.50.202/24)
- `inet6`      → IPv6 address (e.g. fe80::216:3eff:fe0e:d83c/64)

## Key Concepts
- MAC address = physical/hardware address, unique per NIC
- IPv4 = 4 numbers separated by dots (e.g. 192.168.1.10)
- IPv6 = 128-bit address in hex separated by colons
- /24 and /64 = CIDR notation defining the subnet
- Link-local IPv6 (fe80::) = only works on local network segment
- `ip a` is modern replacement for `ifconfig`
- Use `grep` with a space ("inet ") to avoid matching inet6 results

## What I Learned
- Every interface has a MAC address on the link/ether line
- loopback (lo) has no MAC address
- One interface can have both IPv4 and IPv6 addresses
- grep can filter ip a output to find specific address types quickly
