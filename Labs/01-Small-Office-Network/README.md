# Small Office Network

## Overview

This project simulates the design and deployment of a small office network using Cisco Packet Tracer. The objective is to build a reliable and scalable local area network (LAN) that provides connectivity between end devices while following networking best practices.

The project demonstrates the implementation of fundamental networking concepts, including IPv4 addressing, router and switch configuration, network verification, and documentation.

---

## Scenario

A small technology company has recently established a new office and requires a functional network infrastructure for its daily operations.

As the network engineer, the objective is to design, configure, and validate a wired network that enables communication between all connected devices while providing a foundation for future network expansion.

---

## Objectives

- Design a small office network topology.
- Configure a Cisco router.
- Configure a Cisco Layer 2 switch.
- Configure end devices with static IPv4 addressing.
- Configure a switch management interface.
- Verify end-to-end connectivity.
- Document the network implementation.

---

## Network Topology

The network consists of the following devices:

| Device          | Quantity |
|-----------------|---------:|
| Cisco Router    | 1        |
| Cisco Switch    | 1        |
| PCs             | 2        |
| Network Printer | 1        |
| Server          | 1        |

The following diagram illustrates the physical topology of the network.

![Small Office Network Topology](topology.png)

---

## IP Addressing Plan

| Device  | Interface            | IP Address     | Subnet Mask   | Default Gateway |
|---------|----------------------|----------------|---------------|-----------------|
| R1      | GigabitEthernet0/0   | 192.168.10.1   | 255.255.255.0 | N/A             |
| S1      | VLAN 1               | 192.168.10.2   | 255.255.255.0 | 192.168.10.1    |
| Server  | NIC                  | 192.168.10.5   | 255.255.255.0 | 192.168.10.1    |
| PC1     | NIC                  | 192.168.10.10  | 255.255.255.0 | 192.168.10.1    |
| PC2     | NIC                  | 192.168.10.11  | 255.255.255.0 | 192.168.10.1    |
| Printer | NIC                  | 192.168.10.20  | 255.255.255.0 | 192.168.10.1    |

---

## Project Structure

```text
01-Small-Office-Network/
│
├── README.md
├── Small-Office-Network.pkt
├── topology.png
│
├── configs/
│   ├── R1.txt
│   └── S1.txt
│
├── screenshots/
│   ├── topology.png
│   ├── ping-tests.png
│   ├── router-config.png
│   └── switch-config.png
│
└── notes/
    └── observations.md
```

---

## Configuration Tasks

### Router

- Configure the hostname.
- Configure the GigabitEthernet interface.
- Assign the IPv4 address.
- Enable the interface.
- Save the running configuration.

### Switch

- Configure the hostname.
- Configure the management interface.
- Configure the default gateway.
- Save the running configuration.

### End Devices

- Configure static IPv4 addressing.
- Configure the subnet mask.
- Configure the default gateway.

---

## Verification

The following connectivity tests were successfully completed:

- PC1 to PC2
- PC1 to Server
- PC1 to Printer
- PC2 to Router
- Server to Printer

All devices successfully exchanged ICMP echo requests and replies.

---

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- Ethernet
- IPv4
- ICMP

---

## Skills Demonstrated

- Network topology design
- IPv4 addressing
- Cisco IOS configuration
- Router configuration
- Switch configuration
- Switch management
- Network verification
- Basic network troubleshooting
- Network documentation

---

## Files

| File                     | Description                                |
|--------------------------|--------------------------------------------|
| Small-Office-Network.pkt | Cisco Packet Tracer project                |
| topology.png             | Network topology diagram                   |
| configs/                 | Router and switch configurations           |
| screenshots/             | Configuration and verification screenshots |
| notes/                   | Additional project notes                   |

---

## Future Improvements

This network can be extended by implementing:

- Dynamic Host Configuration Protocol (DHCP)
- Virtual Local Area Networks (VLANs)
- Inter-VLAN Routing
- Access Control Lists (ACLs)
- Network Address Translation (NAT)
- Dynamic Routing Protocols
- Network Monitoring
- Internet Connectivity

---

## Author

**Ziad ZARABI**

Networking Portfolio

GitHub Repository: Networking-Labs