# Lab 01 – Identify MAC and IP Addresses in Linux

## Summary
Used the `ip a` command to identify network addresses in Linux.

## Commands Used
| Command | Purpose |
|---------|---------|
| `ip a`  | Display all network interfaces and their addresses |

## Key Concepts
- `ip a` is the modern preferred tool over `ifconfig`
- **Loopback interface** (`lo`) – internal system communication
- **Ethernet interface** (`eth0`) – primary network interface

## How to Read the Output
- `link/ether` → MAC address (hardware address)
- `inet`       → IPv4 address
- `inet6`      → IPv6 address

## What I Learned
- Every network interface has a unique MAC address
- A single interface can have both IPv4 and IPv6 addresses
- `ip a` shows a complete overview of all interfaces at once
