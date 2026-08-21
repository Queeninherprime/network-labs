# Basic Inter-Subnet Connectivity Lab

## Objective
Build a simple topology with two separate subnets connected through a router, and verify that devices on different subnets can communicate with each other.



The lab consists of:
- 1 Router
- 2 Switches (Switch1, Switch2)
- 2 PCs (PC1, PC2)

**Layout:**
- Router G0/0 → Switch1 → PC1
- Router G0/1 → Switch2 → PC2

## IP Addressing Scheme

| Device  | Interface | IP Address     | Subnet Mask     | Gateway       |
|---------|-----------|-----------------|------------------|----------------|
| PC1     | Eth0      | 192.168.2.1     | 255.255.255.0    | 192.168.2.254 |
| PC2     | Eth0      | 192.168.1.10    | 255.255.255.0    | 192.168.1.254 |
| Router  | G0/0      | 192.168.2.254   | 255.255.255.0    | —              |
| Router  | G0/1      | 192.168.1.254   | 255.255.255.0    | —              |

> Note: PC1 sits on the 192.168.2.0/24 network, and PC2 sits on the 192.168.1.0/24 network. The router connects the two subnets and routes traffic between them.

## Configuration Steps
1. Assigned static IP addresses to PC1 and PC2 on their respective subnets.
2. Configured the router's G0/0 and G0/1 interfaces with the gateway IP for each subnet.
3. Brought up router interfaces with `no shutdown`.
4. Verified switches were passing traffic between connected devices (Layer 2, no VLAN config needed for this basic lab).

## Verification
- Pinged from PC1 to its default gateway (192.168.2.254) — **successful**.
- Pinged from PC2 to its default gateway (192.168.1.254) — **successful**.
- Pinged from PC1 to PC2 (192.168.1.10) across the router — **successful**, confirming inter-subnet routing is working.

## What This Demonstrates
- Basic static IP addressing across separate subnets
- Router acting as the default gateway for two networks
- End-to-end connectivity across a routed topology, verified with ICMP (ping)

## Tools Used
Cisco Modeling Labs (CML)
