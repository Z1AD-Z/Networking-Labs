# Learning Resources

This document contains the learning resources used throughout the **Networking-Labs** project.

The objective is to document the official references, study materials, and tools that support each lab. The list will continue to grow as new networking concepts are introduced.

---

# Primary Learning Platform

## Cisco Networking Academy (NetAcad)

The majority of the networking concepts implemented in this repository are based on Cisco Networking Academy courses.

Topics include:

- Networking Fundamentals
- Ethernet
- IPv4
- IPv6
- Switching
- Routing
- VLANs
- Inter-VLAN Routing
- STP
- EtherChannel
- ACLs
- NAT
- DHCP
- OSPF
- WAN Technologies
- Network Security

---

# Books

## CCNA 200-301 Official Cert Guide

Author:

- Wendell Odom

Purpose:

Primary theoretical reference for CCNA concepts and Cisco IOS configuration.

Status:

Ongoing reference.

---

## 31 Days Before Your CCNA Exam

Author:

- Allan Johnson

Purpose:

Concept review and exam preparation.

Status:

Future reference.

---

# Documentation

## Cisco Documentation

Official Cisco technical documentation for Cisco IOS commands and networking technologies.

Used for:

- IOS commands
- Routing
- Switching
- Network services
- Configuration verification

---

# Software

## Cisco Packet Tracer

Purpose:

Network simulation and laboratory implementation.

Used in every project contained in this repository.

---

## Visual Studio Code

Purpose:

Documentation and Markdown editing.

---

## Git

Purpose:

Version control.

---

## GitHub

Purpose:

Project hosting and portfolio management.

---


# Labs

## Lab 01 — Small Office Network

Topics Covered

- Network Topology Design
- Ethernet
- IPv4 Addressing
- Cisco IOS
- Router Configuration
- Layer 2 Switching
- Switch Management Interface
- Static Host Configuration
- ICMP Connectivity Verification
- Network Documentation

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer
- Cisco IOS CLI

Status

Completed

---

## Lab 02 — Two LANs with Static Routing

Topics Covered

- Multi-site Network Design
- Point-to-Point WAN Links
- Static Routing
- Routing Tables
- Default Gateway Configuration
- Router-to-Router Communication
- End-to-End Connectivity
- ICMP Verification

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer
- Cisco IOS CLI

Status

Completed

---

## Lab 03 — Small Business VLANs

Topics Covered

- Virtual Local Area Networks (VLANs)
- VLAN Fundamentals
- VLAN Creation and Naming
- VLAN Assignment
- Access Port Configuration
- VLAN Segmentation
- Broadcast Domains
- Ethernet Switching
- Trunking Fundamentals
- Switch-to-Switch Connectivity
- VLAN Verification
- Cisco IOS Switching Commands
- Network Troubleshooting

Implementation Focus

- Designing a small-business network using multiple VLANs.
- Creating and configuring VLANs on Cisco switches.
- Assigning switch ports to their corresponding VLANs.
- Configuring access ports.
- Understanding the role of trunk links in carrying multiple VLANs.
- Verifying VLAN membership and switch port assignments.
- Testing connectivity within the configured network.
- Troubleshooting VLAN and switching configuration issues.

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer 8.2.2
- Cisco IOS CLI
- Cisco Switching Documentation

Status

Completed

---

## Lab 04 — Branch Office Connectivity

Topics Covered

- Branch Office Network Design
- Multi-Device Network Topology
- IPv4 Addressing and Subnetting
- Router Interface Configuration
- LAN Connectivity
- WAN Connectivity
- Inter-Router Links
- Default Gateway Configuration
- Routing Fundamentals
- Routing Table Verification
- Inter-Network Communication
- ICMP Connectivity Testing
- Network Troubleshooting

Implementation Focus

- Designing a network connecting separate office locations.
- Organizing routers, switches, and end devices.
- Configuring IPv4 addresses on the required network interfaces.
- Establishing connectivity between the network devices.
- Configuring the required network paths between the connected segments.
- Verifying interface addressing and operational status.
- Inspecting routing information and connectivity.
- Testing communication between devices across the network.
- Identifying and resolving network configuration issues.

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer 8.2.2
- Cisco IOS CLI
- Cisco Routing Documentation

Status

Completed

---

## Lab 05 — DHCP Deployment

Topics Covered

- Dynamic Host Configuration Protocol (DHCP)
- DHCP Client and Server Roles
- DHCP Server Configuration
- Dynamic IPv4 Address Assignment
- DHCP Address Pools
- Address Allocation
- DHCP Lease Management
- Default Gateway Distribution
- Network Parameter Assignment
- Client Address Acquisition
- DHCP Verification
- Network Services Troubleshooting

Implementation Focus

- Designing a small-business network with centralized DHCP services.
- Configuring the designated DHCP server.
- Defining the IPv4 addressing parameters for DHCP clients.
- Configuring DHCP address allocation.
- Providing network configuration information to end devices.
- Configuring clients to obtain their IPv4 addresses automatically.
- Verifying dynamically assigned IP addresses.
- Inspecting client network configuration.
- Testing network connectivity after DHCP address assignment.
- Troubleshooting DHCP configuration and address allocation issues.

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer 8.2.2
- Cisco IOS CLI
- Packet Tracer Server Configuration Tools
- Cisco Networking Documentation

Status

Completed

---

## Lab 06 — OSPF Single-Area

Topics Covered

- Dynamic Routing Fundamentals
- Open Shortest Path First (OSPFv2)
- Link-State Routing
- OSPF Process Configuration
- OSPF Router ID Assignment
- OSPF Area 0
- Neighbor Discovery
- OSPF Adjacency Formation
- Network Advertisement
- Wildcard Masks
- Passive Interfaces
- OSPF Routing Tables
- Administrative Distance
- OSPF Interface Cost
- Routing Metrics
- End-to-End Connectivity Verification
- Network Troubleshooting

Implementation Focus

- Designing a three-router linear network topology.
- Configuring IPv4 addresses on router interfaces.
- Assigning unique OSPF Router IDs.
- Enabling OSPF process 1 on all three routers.
- Advertising LAN and transit networks within Area 0.
- Configuring passive interfaces on LAN-facing interfaces.
- Establishing OSPF neighbor relationships between adjacent routers.
- Verifying OSPF adjacency states.
- Inspecting dynamically learned routes.
- Analyzing OSPF interface costs and routing metrics.
- Testing bidirectional connectivity between the Head Office and Branch Office LANs.

Verification Results

- R1 successfully established an adjacency with R2.
- R2 successfully established adjacencies with R1 and R3.
- R3 successfully established an adjacency with R2.
- All expected OSPF adjacencies reached the FULL state.
- Remote networks were successfully learned through OSPF.
- Inspected transit interfaces reported an OSPF cost of 1.
- PC1 successfully communicated with PC2.
- PC2 successfully communicated with PC1.
- Both final connectivity tests completed with 0% packet loss.

Resources Used

- Cisco Networking Academy
- Cisco Packet Tracer 8.2.2
- Cisco IOS CLI
- Cisco OSPF Documentation
- IPv4 and Routing References

Status

Completed

---

## Upcoming Labs

The following laboratories are planned for future development. They will extend the networking concepts and practical experience gained from the first six projects.

### Lab 07 — EtherChannel

Topics

- EtherChannel Fundamentals
- Link Aggregation
- Port Aggregation Protocol (PAgP)
- Link Aggregation Control Protocol (LACP)
- Interface Bundling
- Load Balancing
- Redundant Network Links
- EtherChannel Configuration and Verification

Status

Planned

---

### Lab 08 — Advanced DHCP Deployment

Topics

- Advanced DHCP Configuration
- DHCP Relay Agent
- Multiple DHCP Scopes
- DHCP Across Multiple Networks
- Address Reservation
- DHCP Exclusions
- DHCP Troubleshooting
- DHCP Service Optimization

Status

Planned

---

### Lab 09 — Network Address Translation (NAT)

Topics

- NAT Fundamentals
- Static NAT
- Dynamic NAT
- Port Address Translation (PAT)
- Inside and Outside Interfaces
- Private and Public IPv4 Addressing
- Address Translation Configuration
- NAT Verification

Status

Planned

---

### Lab 10 — Access Control Lists (ACLs)

Topics

- Access Control Lists
- Standard ACLs
- Extended ACLs
- Traffic Filtering
- Inbound and Outbound Rules
- Access Control Verification
- Network Traffic Restrictions
- Basic Network Security Policies

Status

Planned

---

### Lab 11 — Advanced OSPF and Multi-Area Routing

Topics

- Advanced OSPF Configuration
- Multi-Area OSPF
- Backbone and Non-Backbone Areas
- Inter-Area Routing
- OSPF Area Border Routers (ABR)
- Route Summarization
- OSPF Cost Manipulation
- OSPF Authentication
- OSPF Convergence and Verification

Status

Planned

---

### Lab 12 — IPv6

Topics

- IPv6 Addressing
- IPv6 Address Types
- Prefix Lengths
- Stateless Address Autoconfiguration
- DHCPv6 Fundamentals
- IPv6 Routing
- ICMPv6
- IPv6 Connectivity Verification
- IPv4 and IPv6 Coexistence

Status

Planned

---

### Lab 13 — Network Services

Topics

- Domain Name System (DNS)
- Network Time Protocol (NTP)
- Network Services Configuration
- Client and Server Communication
- Name Resolution
- Service Management
- Network Service Verification
- Infrastructure Troubleshooting

Status

Planned

---

### Lab 14 — Network Security

Topics

- Network Security Fundamentals
- Secure Device Management
- Secure Shell (SSH)
- Authentication and Authorization
- Password Security
- Switch Port Security
- Network Segmentation
- Infrastructure Hardening
- Basic Network Security Monitoring

Status

Planned

---

### Lab 15 — Enterprise Network

Topics

- Enterprise Network Architecture
- Hierarchical Network Design
- Core, Distribution, and Access Layers
- VLAN Segmentation
- Inter-VLAN Routing
- Dynamic Routing Integration
- Network Redundancy
- High Availability Fundamentals
- Enterprise Network Scalability
- End-to-End Network Verification

Status

Planned

---

# Laboratory Progress Summary

| Lab | Project | Status |
|---|---|---|
| 01 | Small Office Network | Completed |
| 02 | Two LANs with Static Routing | Completed |
| 03 | Small Business VLANs | Completed |
| 04 | Branch Office Connectivity | Completed |
| 05 | DHCP Deployment | Completed |
| 06 | OSPF Single-Area | Completed |
| 07 | EtherChannel | Planned |
| 08 | Advanced DHCP Deployment | Planned |
| 09 | Network Address Translation | Planned |
| 10 | Access Control Lists | Planned |
| 11 | Advanced OSPF and Multi-Area Routing | Planned |
| 12 | IPv6 | Planned |
| 13 | Network Services | Planned |
| 14 | Network Security | Planned |
| 15 | Enterprise Network | Planned |

**Completed Laboratories:** 6  
**Planned Laboratories:** 9  
**Total Laboratories:** 15

# Repository Goal

This repository is intended to document the practical progression from fundamental networking concepts to enterprise-level network implementation.

Every lab focuses on:

- Planning
- Configuration
- Verification
- Troubleshooting
- Documentation

Each completed lab builds upon concepts introduced in previous labs, creating a structured and progressive learning path toward CCNA-level networking skills.