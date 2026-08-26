# External Connector (NAT Mode) Lab — Outbound Internet Connectivity

## Objective
Enable outbound internet access for internal lab devices using an External Connector in NAT mode, and understand how DHCP, NAT, and DNS are automatically provided by the connector.



The lab extends the basic topology by adding an **External Connector (ext-conn-nat)** attached to Switch1, providing shared internet access to PC1 (and any other device on that switch).

- Router — G0/0 → Switch1, G0/1 → Switch2
- Switch1 → PC1, plus External Connector (NAT mode)
- Switch2 → PC2

## Initial State (Before External Connector)
- PC1 could ping its local gateway (10.0.1.254) successfully.
- PC1 **could not** ping PC2 (10.0.2.1) — different subnet, no default gateway configured on PC1.
- PC1 **could not** reach cisco.com — no external connectivity and no DNS configured.

## Configuration Steps
1. Added an **External Connector** node, set to **NAT mode** (default).
2. Renamed the node to `ext-conn-nat` for clarity.
3. Linked the external connector to **Switch1**, sharing external access with all devices on that switch.
4. Started the external connector node.
5. On PC1, requested a DHCP-derived IP address on eth0 alongside its existing static address.

## Verification
- PC1 received a second IP address via DHCP from the NAT pool (192.168.255.0/24), alongside its static address (10.0.1.1/24).
- A default route was automatically installed via the NAT connector.
- Pinged **cisco.com** from PC1 — **successful**, confirming outbound internet access.
- Checked DNS config (`/etc/resolv.conf`) — automatically populated with nameserver `192.168.255.1`, provided by the connector.

## What This Demonstrates
- How Cisco Modeling Labs' External Connector provides **NAT, DHCP, and DNS** automatically in NAT mode
- The difference between local subnet connectivity, inter-subnet connectivity (needs routing), and external/internet connectivity (needs an external connector)
- Attaching the connector to a switch (rather than a single PC) shares external access across the whole Layer 2 domain

## Tools Used
Cisco Modeling Labs (CML)
