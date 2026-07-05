# Small Business VLANs

## Overview

This project simulates the design and deployment of a segmented Local Area Network (LAN) for a small business using Cisco Packet Tracer. The objective is to improve network organization and security by separating departments into different Virtual Local Area Networks (VLANs) while following networking best practices.

The project demonstrates the implementation of VLAN technology, including VLAN creation, port assignment, Layer 2 switch configuration, IPv4 addressing, network verification, and technical documentation.

---

## Scenario

A growing small business has expanded its internal departments and requires logical network segmentation to improve security, performance, and administration.

As the network engineer, the objective is to configure VLANs for each department, assign switch ports accordingly, and validate that devices within the same VLAN can communicate while communication between different VLANs remains isolated.

---

## Objectives

- Design a segmented small business network.
- Configure a Cisco Layer 2 switch.
- Create multiple VLANs.
- Assign switch ports to VLANs.
- Configure end devices with static IPv4 addressing.
- Verify VLAN membership.
- Validate Layer 2 communication.
- Document the complete network implementation.

---

## Network Topology

The network consists of the following devices:

|      Device     |  Quantity |
|-----------------|----------:|
| Cisco Router    |      1    |
| Cisco Switch    |      1    |
|      PCs        |      2    |
|      Server     |      1    |
| Network Printer |      1    |

The following diagram illustrates the physical topology of the network.

![Small Business VLAN Topology](screenshots/network-topology.png)

---

## VLAN Plan

| VLAN ID | VLAN Name |    Devices       |
|---------|-----------|------------------|
|    10   |    ADMIN  |      PC1         |
|    20   |   SALES   |      PC2         |
|    30   | SERVICES  | Server, Printer  |

---

## Port Assignment

| Switch Port      | Connected Device |                 VLAN                   |
|------------------|------------------|----------------------------------------|
| FastEthernet0/1  |       PC1        |                  10                    |
| FastEthernet0/2  |       PC2        |                  20                    |
| FastEthernet0/3  |      Server      |                  30                    |
| FastEthernet0/4  |      Printer     |                  30                    |
| FastEthernet0/24 |      Router R1   | Reserved for future Inter-VLAN Routing |

---

## IP Addressing Plan

| Device |   Interface   |   IP Address  | Subnet Mask   | Default Gateway |
|--------|---------------|---------------|---------------|-----------------|
|   PC1  | FastEthernet0 | 192.168.10.10 | 255.255.255.0 |      N/A        |
|   PC2  | FastEthernet0 | 192.168.20.10 | 255.255.255.0 |      N/A        |
|  SRV1  | FastEthernet0 | 192.168.30.5  | 255.255.255.0 |      N/A        |
|  PRN1  | FastEthernet0 | 192.168.30.20 | 255.255.255.0 |      N/A        |

> **Note:** Default gateways are intentionally not configured because inter-VLAN routing is not implemented in this lab. Communication between VLANs will be introduced in **Lab 05 – Branch Office Connectivity**.

---

## Project Structure

```text
03-Small-Business-VLANs/
│
├── README.md
├── Small-Business-VLANs.pkt
│
├── configs/
│   ├── R1.txt
│   └── S1.txt
│
├── screenshots/
│   ├── network-topology.png
│   ├── switch-running-config.png
│   ├── show-vlan-brief.png
│   ├── mac-address-table.png
│   ├── pc1-ip-configuration.png
│   ├── pc2-ip-configuration.png
│   ├── server-ip-configuration.png
│   ├── printer-ip-configuration.png
│   ├── ping-server-to-printer.png
│   ├── ping-pc1-to-pc2-failed.png
│   └── ping-pc1-to-server-failed.png
│
└── notes/
    └── observations.md
```

---

## Configuration Tasks

### Router R1

- Configure the hostname.
- Reserve the physical interface for future Router-on-a-Stick implementation.
- Save the running configuration.

Configuration file:

```text
configs/R1.txt
```

### Switch S1

- Configure the hostname.
- Create VLAN 10.
- Create VLAN 20.
- Create VLAN 30.
- Assign VLAN names.
- Configure access ports.
- Verify VLAN membership.
- Save the running configuration.

Configuration file:

```text
configs/S1.txt
```

### End Devices

- Configure static IPv4 addresses.
- Configure subnet masks.
- Verify communication within the same VLAN.
- Verify isolation between different VLANs.

---

## Configuration Evidence

### Switch Running Configuration

![Switch Running Configuration](screenshots/switch-running-config.png)

### VLAN Configuration

![Show VLAN Brief](screenshots/show-vlan-brief.png)

### MAC Address Table

![MAC Address Table](screenshots/mac-address-table.png)

### PC1 IP Configuration

![PC1 IP Configuration](screenshots/pc1-ip-configuration.png)

### PC2 IP Configuration

![PC2 IP Configuration](screenshots/pc2-ip-configuration.png)

### Server IP Configuration

![Server IP Configuration](screenshots/server-ip-configuration.png)

### Printer IP Configuration

![Printer IP Configuration](screenshots/printer-ip-configuration.png)

---

## Connectivity Verification

Connectivity was verified using ICMP Echo Requests after completing the configuration.

### Server to Printer (Same VLAN)

![Server to Printer](screenshots/ping-server-to-printer.png)

Communication was successful because both devices belong to **VLAN 30**.

### PC1 to PC2 (Different VLANs)

![PC1 to PC2 Failed](screenshots/ping-pc1-to-pc2-failed.png)

Communication failed because **inter-VLAN routing is not configured**.

### PC1 to Server (Different VLANs)

![PC1 to Server Failed](screenshots/ping-pc1-to-server-failed.png)

Communication failed because devices are located in different VLANs.

---

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- Ethernet
- IPv4
- VLANs
- Layer 2 Switching
- ICMP

---

## Skills Demonstrated

- VLAN design
- VLAN creation
- VLAN port assignment
- Layer 2 switch configuration
- IPv4 addressing
- Broadcast domain segmentation
- VLAN verification
- MAC address table verification
- Network verification using ICMP
- Technical documentation

---

## Files

|             File         | Description                                                |
|--------------------------|------------------------------------------------------------|
| Small-Business-VLANs.pkt | Cisco Packet Tracer project                                |
| configs/                 | Router and switch configuration files                      |
| screenshots/             | Topology, VLAN configuration, and verification screenshots |
| notes/                   | Project observations and documentation                     |

---

## Future Improvements

This network can be extended by implementing:

- Router-on-a-Stick
- Inter-VLAN Routing
- Dynamic Host Configuration Protocol (DHCP)
- Access Control Lists (ACLs)
- Network Address Translation (NAT)
- Dynamic Routing Protocols (OSPF)
- Internet connectivity
- Network monitoring and management

---

## Author

**Ziad ZARABI**

Networking Portfolio

GitHub Repository: **Networking-Labs**