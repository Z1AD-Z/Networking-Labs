<div align="center">

#  NETWORKING LABS

### Practical Networking Foundations for Cybersecurity

**Routing • Switching • Security • Troubleshooting • Automation**

[About](#-about) • [Learning Objectives](#-learning-objectives) • [Lab Roadmap](#-lab-roadmap) • [Lab Architecture](#-core-networking-concepts) • [Skills](#-skills-developed) • [Tools](#-tools--technologies) • [Repository Structure](#-repository-structure) • [Portfolio Integration](#-relationship-with-cybersecurity-portfolio)

![Level](https://img.shields.io/badge/Level-Beginner%20→%20Intermediate-0A66C2?style=for-the-badge)
![Networking](https://img.shields.io/badge/Focus-Networking-1E3A8A?style=for-the-badge)
![Cisco](https://img.shields.io/badge/Cisco-IOS-00BCF2?style=for-the-badge&logo=cisco&logoColor=white)
![Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-003D82?style=for-the-badge)
![Network Security](https://img.shields.io/badge/Network-Security-0F172A?style=for-the-badge)
![Automation](https://img.shields.io/badge/Network-Automation-1D4ED8?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-12-2563EB?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-38BDF8?style=for-the-badge)

</div>

---

##  About

**Networking-Labs** is a structured collection of hands-on networking exercises designed to build **real understanding**, not memorization. It starts with foundational network configuration and progressively moves toward multi-LAN architectures, VLANs, routing, DHCP, OSPF, ACLs, NAT, enterprise topology design, troubleshooting, traffic analysis, and network automation.

This repository is **not** simply a folder of Cisco Packet Tracer files. It is a practical networking foundation built to support future work in cybersecurity, network security, SOC operations, network administration, penetration testing, cloud security, infrastructure security, firewall administration, security monitoring, and network automation.

> **"Strong cybersecurity begins with strong networking fundamentals."**

Before securing a network, you must understand how the network works. That principle drives the structure of every lab in this repository.

**Target level:** Beginner → Intermediate
**Target audience:** Networking students, cybersecurity students, CCNA learners, junior network engineers, and anyone building a technical foundation for advanced security and infrastructure work.

---

##  Why Networking Matters for Cybersecurity

Cybersecurity professionals cannot secure what they do not understand. Effective defense, detection, and response all depend on a solid grasp of IP addressing, subnets, routing, switching, VLANs, ports, protocols, NAT, ACLs, DNS, DHCP, network traffic, and network segmentation.

```
Networking
   ↓
Network Visibility
   ↓
Network Security
   ↓
Traffic Analysis
   ↓
Threat Detection
   ↓
Incident Response
   ↓
Cybersecurity
```

This progression connects directly to tools and concepts used across the security field:

- **Firewalls** — enforce boundaries defined by network segmentation
- **IDS/IPS** — depend on understanding normal vs. abnormal traffic
- **VPNs** — rely on routing and addressing fundamentals
- **SIEM** — ingests and correlates the same traffic you learn to read here
- **Wireshark** — turns raw packets into actionable intelligence
- **Network monitoring** — built on visibility established through solid design
- **Penetration testing** — requires fluency in how networks actually behave
- **Cloud networking & Zero Trust** — modern extensions of the same core principles

---

##  Learning Objectives

By working through this repository, the goal is to:

- Build strong networking fundamentals
- Understand IPv4 addressing
- Master subnetting
- Configure switches and routers
- Configure VLANs and trunking
- Configure DHCP
- Configure NAT
- Configure ACLs
- Understand routing protocols and configure OSPF
- Troubleshoot network issues methodically
- Analyze network traffic with Wireshark
- Understand enterprise network architecture
- Practice foundational network security
- Learn basic network automation concepts
- Build a solid foundation for CCNA and broader cybersecurity work

---

##  Learning Philosophy

```
UNDERSTAND
   ↓
CONFIGURE
   ↓
VERIFY
   ↓
TROUBLESHOOT
   ↓
SECURE
   ↓
AUTOMATE
   ↓
DOCUMENT
```

- Understand the network before securing it.
- Build configurations yourself instead of copying them blindly.
- Use troubleshooting as part of the learning process, not a failure state.
- Analyze packets and behavior — not only CLI output.
- Document the reasoning behind each configuration decision.
- Connect every networking concept back to its cybersecurity relevance.

Every lab in this repository is ideally documented with an **Objective, Topology, Requirements, Addressing Plan, Configuration, Validation, Troubleshooting, Security Considerations,** and **Lessons Learned.**

---

##  Lab Roadmap

| # | Lab | Main Skills | Level |
|---|---|---|---|
| 01 | [Small Office Network](#lab-01--small-office-network) | Basic topology, IPv4, connectivity | 🟢 Beginner |
| 02 | [Two LANs — Static Routing](#lab-02--two-lans--static-routing) | Static routes, routing table | 🟢 Beginner |
| 03 | [Small Business VLANs](#lab-03--small-business-vlans) | VLANs, trunking, segmentation | 🟢 Beginner |
| 04 | [Branch Office Connectivity](#lab-04--branch-office-connectivity) | Site-to-site, WAN-style design | 🟢 Beginner / 🟡 Intermediate |
| 05 | [DHCP Deployment](#lab-05--dhcp-deployment) | DHCP pools, leases, DNS config | 🟢 Beginner / 🟡 Intermediate |
| 06 | [OSPF Single-Area](#lab-06--ospf-single-area) | Dynamic routing, neighbors, Area 0 | 🟡 Intermediate |
| 07 | [Network Access Control](#lab-07--network-access-control) | ACLs, allow/deny logic | 🟡 Intermediate |
| 08 | [Internet Access with NAT](#lab-08--internet-access-with-nat) | NAT, PAT, inside/outside interfaces | 🟡 Intermediate |
| 09 | [Enterprise Campus Network](#lab-09--enterprise-campus-network) | Core/distribution/access design | 🟡 Intermediate |
| 10 | [Network Troubleshooting](#lab-10--network-troubleshooting) | Layered troubleshooting methodology | 🟡 Intermediate |
| 11 | [Wireshark Traffic Analysis](#lab-11--wireshark-traffic-analysis) | Packet capture & protocol analysis | 🟡 Intermediate |
| 12 | [Network Automation](#lab-12--network-automation) | Python, APIs, reporting | 🟡 Intermediate |

---

##  Lab Details

### Lab 01 — Small Office Network

The foundation lab. Establishes the baseline concepts every later lab builds on.

**Concepts:** Basic topology, IPv4 addressing, end devices, switch, router, default gateway, connectivity testing.

```
PCs
 ↓
Switch
 ↓
Router
 ↓
Network
```

**Security relevance:** Understanding network boundaries, basic segmentation, default gateway behavior, connectivity validation.

---

### Lab 02 — Two LANs — Static Routing

**Concepts:** Two separate LANs, router-to-router communication, static routes, routing tables, end-to-end connectivity.

```
LAN A
  │
Router A
  │
Router B
  │
LAN B
```

**Security relevance:** Routing visibility, network boundaries, inter-network communication, basic route control.

---

### Lab 03 — Small Business VLANs

**Concepts:** VLANs, access ports, trunking, department segmentation, inter-VLAN communication concepts.

```
VLAN 10 → ADMIN
VLAN 20 → SALES
VLAN 30 → SERVICES
```

**Security relevance:** Broadcast separation, segmentation, reduced lateral communication, security policy enforcement.

---

### Lab 04 — Branch Office Connectivity

**Concepts:** Site-to-site connectivity, branch architecture, inter-location routing, WAN-style connectivity, network design.

```
Head Office
    │
    │ WAN
    │
Branch Office
```

Branch connectivity is foundational to any enterprise network — most real-world organizations operate across multiple physical sites that must communicate securely and reliably.

---

### Lab 05 — DHCP Deployment

**Concepts:** DHCP server configuration, address pools, default gateway and DNS options, leases, automatic IP assignment.

**Security relevance:** Centralized network configuration, controlled device onboarding, address management, and the ability to spot rogue or unexpected configurations on the network.

---

### Lab 06 — OSPF Single-Area

An intermediate dynamic routing lab.

**Concepts:** OSPF fundamentals, router IDs, neighbor relationships, route advertisement, cost, single-area design, routing table verification.

```
Router A
   ↕
Router B
   ↕
Router C

  (all in Area 0)
```

**Security relevance:** Dynamic routing understanding, infrastructure resilience, routing visibility, and the ability to detect unexpected route changes.

---

### Lab 07 — Network Access Control

A security-focused networking lab.

**Concepts:** ACLs, source/destination addresses, protocols, ports, allow/deny logic, rule ordering.

```
Users
   ↓
ACL
   ↓
Allowed Services
   ↓
Servers
```

> Access control should be based on business and security requirements — not random filtering.

**Security relevance:** Network segmentation, least privilege, traffic control, attack surface reduction.

---

### Lab 08 — Internet Access with NAT

**Concepts:** NAT, PAT, private vs. public addressing, inside/outside interfaces, internet connectivity.

```
LAN
 ↓
Router
 ↓
NAT
 ↓
Internet
```

**Security relevance:** Address translation, egress control, private address architecture, internet boundary awareness.

> NAT provides address translation and a degree of obscurity — it is **not** a complete security control on its own.

---

### Lab 09 — Enterprise Campus Network

The major infrastructure lab of this repository.

**Concepts:** Enterprise topology, VLANs, routing, distribution/access design concepts, segmentation, scalability, redundancy concepts, addressing plans.

```
                 Core
              /        \
        Distribution  Distribution
          /   \          /   \
       Access Access   Access Access
         │      │        │      │
       Users  Servers  Users  Services
```

**Security relevance:** Segmentation, network architecture, centralized control, reduced broadcast domains, scalable security design.

---

### Lab 10 — Network Troubleshooting

A dedicated troubleshooting methodology lab.

```
IDENTIFY
  ↓
COLLECT EVIDENCE
  ↓
CHECK LAYER 1
  ↓
CHECK LAYER 2
  ↓
CHECK LAYER 3
  ↓
CHECK SERVICES
  ↓
TEST
  ↓
FIX
  ↓
VALIDATE
  ↓
DOCUMENT
```

**Troubleshooting areas:** Physical connectivity, VLAN configuration, trunking, IP addressing, default gateway, routing, DNS, DHCP, ACLs, NAT.

**Useful tools:** `ping`, `traceroute`, `ipconfig`, `show` commands, `arp`, `nslookup`, Wireshark.

---

### Lab 11 — Wireshark Traffic Analysis

A cybersecurity-focused traffic analysis lab.

**Concepts:** Packet capture, frames, Ethernet, ARP, IPv4, TCP, UDP, ICMP, DNS, HTTP, the TCP three-way handshake.

```
Capture
   ↓
Filter
   ↓
Inspect
   ↓
Interpret
   ↓
Document
```

**Analysis goals:** Identify protocols, identify source/destination, understand ports, analyze the TCP handshake, observe DNS resolution, troubleshoot network behavior, identify unusual traffic patterns.

**Security relevance:** Network visibility, incident investigation, traffic analysis, threat detection.

---

### Lab 12 — Network Automation

Connects directly with the [`Python-for-IT`](https://github.com/Z1AD-Z/Python-for-IT), [`Automation`](https://github.com/Z1AD-Z/Automation), and future `Network-Automation` repositories.

**Concepts (covered conceptually):** Python, APIs, configuration automation, device inventory, repetitive task automation, reporting.

```
Network Devices
      ↓
Automation Script
      ↓
API / SSH
      ↓
Collect Data
      ↓
Process
      ↓
Generate Report
```

> This lab focuses on operational and administrative automation — not offensive tooling.

---

##  Core Networking Concepts

**Layer 1** — Physical media, interfaces, cabling
**Layer 2** — Ethernet, MAC addresses, switching, VLANs, trunking, STP fundamentals
**Layer 3** — IPv4, subnetting, routing, static routing, OSPF, NAT
**Layer 4** — TCP, UDP, ports
**Network Services** — DHCP, DNS
**Security** — ACLs, segmentation, firewalls, traffic analysis

---

##  IP Addressing & Subnetting

Addressing plans are essential to good network architecture. Core concepts covered: IPv4, network address, broadcast address, host range, CIDR, subnet masks, FLSM, VLSM, private addressing, public addressing.

**Example:**

```
192.168.10.0/24

Network:    192.168.10.0
Usable:     192.168.10.1 – 192.168.10.254
Broadcast:  192.168.10.255
```

---

##  Switching Fundamentals

MAC address table, access ports, trunk ports, VLANs, broadcast domains, collision domains, basic STP concepts.

Switching knowledge matters in security because Layer 2 is where segmentation begins — VLANs and trunk boundaries directly shape what traffic can reach what, long before a firewall rule is ever evaluated.

---

##  Routing Fundamentals

Routing tables, next-hop, default route, static routes, dynamic routing, OSPF.

```
Network A
   ↓
Router
   ↓
Routing Table
   ↓
Network B
```

---

##  Network Services

**DHCP** — Automatic IP addressing and configuration distribution.
**DNS** — Name resolution between hostnames and IP addresses.

Both services interact heavily with normal enterprise network operation — and both are common pivot points for troubleshooting and security monitoring alike.

---

##  Network Security Foundations

Network segmentation, ACLs, firewalls, NAT, VPN concepts, IDS/IPS concepts, secure protocols, monitoring, traffic analysis.

```
Security controls
      ↓
Reduce attack surface
      ↓
Improve visibility
      ↓
Support detection
```

---

##  Enterprise Network Design Principles

Layered architecture, modularity, scalability, redundancy, segmentation, documentation, secure management, monitoring.

```
Access Layer
    ↓
Distribution
    ↓
Core
    ↓
WAN / Internet
```

This repository teaches these principles through simplified, hands-on labs — not production-scale deployments.

---

##  Tools & Technologies

| Tool / Technology | Role |
|---|---|
| Cisco Packet Tracer | Primary network simulation environment |
| Wireshark | Packet capture and traffic analysis |
| Cisco IOS | Router and switch configuration |
| Python | Scripting and automation |
| Bash | Linux-side automation and scripting |
| PowerShell | Windows-side automation and scripting |
| Git | Version control |
| GitHub | Repository hosting and documentation |
| `ipconfig` | Local IP configuration inspection |
| `ping` | Connectivity testing |
| `traceroute` | Path/hop analysis |
| `nslookup` | DNS resolution testing |
| `arp` | Layer 2 address resolution inspection |
| SSH | Secure remote device access |
| APIs | Automation and integration |

**Future expansion:** GNS3, EVE-NG (for more advanced, scalable lab environments).

---

##  Lab Environment

Labs may use virtualized or simulated networking environments for safe, isolated practice.

```
Host Machine
      ↓
Networking Simulator / Virtualization
      ↓
Routers / Switches / Hosts
      ↓
Controlled Lab Environment
```

**Possible platforms:** Cisco Packet Tracer, GNS3, EVE-NG, VirtualBox, VMware, Proxmox.

---

##  Lab Documentation Standard

Every lab ideally follows this structure:

```markdown
# Lab Title

## Objective
## Scenario
## Topology
## Requirements
## Addressing Table
## Configuration
## Verification
## Troubleshooting
## Security Considerations
## Lessons Learned
## Future Improvements
```

Documentation is strengthened with network diagrams, IP addressing tables, CLI output, screenshots, and test results.

> ⚠️ Real credentials or sensitive network information are never included in lab documentation.

---

##  Network Configuration Examples

Small, safe Cisco IOS syntax examples used for demonstration purposes only:

```
hostname R1

interface gigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown
```

Conceptually demonstrated across labs: interface configuration, VLAN configuration, static routes, OSPF, ACLs.

> These examples are for syntax demonstration only. No destructive or unauthorized attack configurations are included in this repository.

---

##  Networking Cheat Sheet

| Task | Command / Concept | Purpose |
|---|---|---|
| Show interfaces | `show ip interface brief` | Interface status and IPs |
| Show IP configuration | `ipconfig` / `show running-config` | Verify addressing |
| Show VLANs | `show vlan brief` | VLAN membership overview |
| Show MAC address table | `show mac address-table` | Layer 2 learning table |
| Show routing table | `show ip route` | Verify routes |
| Show OSPF neighbors | `show ip ospf neighbor` | Verify OSPF adjacency |
| Ping | `ping <ip>` | Basic connectivity test |
| Traceroute | `tracert` / `traceroute` | Path/hop analysis |
| DNS lookup | `nslookup <domain>` | Name resolution test |
| ARP | `arp -a` | Layer 2 address resolution |
| Packet capture | Wireshark | Deep traffic inspection |

---

##  Roadmap

###  Beginner
- [ ] Small Office Network
- [ ] Two LANs — Static Routing
- [ ] Small Business VLANs
- [ ] Branch Office Connectivity
- [ ] DHCP Deployment

###  Intermediate
- [ ] OSPF Single-Area
- [ ] Network Access Control
- [ ] Internet Access with NAT
- [ ] Enterprise Campus Network
- [ ] Network Troubleshooting
- [ ] Wireshark Traffic Analysis
- [ ] Network Automation

###  Next Level 
- [ ] STP / RSTP
- [ ] EtherChannel
- [ ] Advanced OSPF
- [ ] EIGRP concepts
- [ ] IPv6
- [ ] VPNs
- [ ] IDS/IPS
- [ ] Network segmentation (advanced)
- [ ] Zero Trust networking
- [ ] SDN concepts
- [ ] Advanced network automation
- [ ] Network security monitoring

---

##  Skills Developed

**Networking:** IPv4, subnetting, routing, switching, VLANs, trunking, DHCP, DNS, NAT, OSPF
**Security:** ACLs, segmentation, traffic analysis, network visibility, security architecture
**Operations:** Troubleshooting, monitoring, documentation
**Automation:** Python, APIs, network automation

---

##  Relationship with Cybersecurity Portfolio

Networking-Labs is one of the **foundational repositories** of the broader cybersecurity portfolio. Every other repository that touches infrastructure, security, or automation builds on the concepts practiced here.

```
Networking-Labs
      │
      ├── Network-Security-Labs
      │
      ├── PfSense
      │
      ├── Monitoring
      │
      ├── Network-Automation
      │
      ├── Linux-Administration-Labs
      │
      ├── Windows-Server-Labs
      │
      ├── Virtualization
      │
      └── Home-Lab-Projects
```

```
Networking
    ↓
Infrastructure
    ↓
Network Security
    ↓
Monitoring
    ↓
Cybersecurity
```

---

##  Relationship with Home-Lab-Projects

Networking-Labs teaches networking components **independently**. Home-Lab-Projects integrates those same components into larger, cohesive environments.

```
Networking-Labs
    ↓
Routing / VLANs / ACLs / NAT / OSPF
    ↓
Home-Lab-Projects
    ↓
Integrated Secure Network
```

---

##  Portfolio Value

This repository demonstrates practical capability in network design, network configuration, troubleshooting, security thinking, documentation, packet analysis, and automation.

> "The repository demonstrates practical networking experience developed through structured laboratory environments and documented technical exercises."

These labs are educational and lab-based — they are not presented as production enterprise experience.

---

##  Project / Lab Status

| Lab | Status | Level |
|---|---|---|
| 01 — Small Office Network | 🟢 Planned | Beginner |
| 02 — Two LANs — Static Routing | 🟢 Planned | Beginner |
| 03 — Small Business VLANs | 🟡 Planned | Beginner |
| 04 — Branch Office Connectivity | 🔵 Planned | Beginner / Intermediate |
| 05 — DHCP Deployment | 🔵 Planned | Beginner / Intermediate |
| 06 — OSPF Single-Area | 🔵 Planned | Intermediate |
| 07 — Network Access Control | 🔵 Planned | Intermediate |
| 08 — Internet Access with NAT | 🔵 Planned | Intermediate |
| 09 — Enterprise Campus Network | 🔵 Planned | Intermediate |
| 10 — Network Troubleshooting | 🔵 Planned | Intermediate |
| 11 — Wireshark Traffic Analysis | 🔵 Planned | Intermediate |
| 12 — Network Automation | 🔵 Planned | Intermediate |

*Update statuses (🟢 Completed / 🟡 In Progress / 🔵 Planned) as labs are finished.*

---

##  Repository Structure

```
Networking-Labs/
│
├── Labs/
│   ├── 01-Small-Office-Network/
│   ├── 02-Two-LANs-Static-Routing/
│   ├── 03-Small-Business-VLANs/
│   ├── 04-Branch-Office-Connectivity/
│   ├── 05-DHCP-Deployment/
│   ├── 06-OSPF-Single-Area/
│   ├── 07-Network-Access-Control/
│   ├── 08-Internet-Access-with-NAT/
│   ├── 09-Enterprise-Campus-Network/
│   ├── 10-Network-Troubleshooting/
│   ├── 11-Wireshark-Traffic-Analysis/
│   └── 12-Network-Automation/
│
├── docs/
│   ├── resources.md
│   └── roadmap.md
│
├── .gitignore
├── LICENSE
└── README.md
```

<details>
<summary><strong> Future Expansion (planned structure)</strong></summary>

```
Networking-Labs/
│
├── Labs/
├── docs/
│   ├── resources.md
│   ├── roadmap.md
│   └── addressing-plans/
├── diagrams/
├── configs/
├── .gitignore
├── LICENSE
└── README.md
```

</details>

---

##  Learning Philosophy (Applied)

```
LEARN
  ↓
CONFIGURE
  ↓
TEST
  ↓
BREAK
  ↓
TROUBLESHOOT
  ↓
SECURE
  ↓
DOCUMENT
```

Learning by doing drives this repository. Breaking a configuration on purpose and troubleshooting it back to health teaches more than a perfect, untouched config ever could.

---

##  Security & Ethical Guidelines

- Labs are performed in controlled or authorized environments only.
- Do not scan or modify networks without explicit permission.
- Do not use these exercises against public or third-party infrastructure.
- Do not expose intentionally vulnerable labs to the public internet.
- Sanitize screenshots, IP addresses, credentials, and logs before publishing.
- Use this repository for education, administration, defense, and authorized testing only.

---

##  Resources

- [Cisco Networking Academy](https://www.netacad.com/)
- [Cisco Documentation](https://www.cisco.com/c/en/us/support/index.html)
- [RFC Editor](https://www.rfc-editor.org/)
- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [NIST](https://www.nist.gov/)
- [CISA](https://www.cisa.gov/)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [OWASP](https://owasp.org/)
- [Python Documentation](https://docs.python.org/3/)

---

##  Contribution

```bash
git clone https://github.com/Z1AD-Z/Networking-Labs.git
git checkout -b feature/your-improvement
git add .
git commit -m "Add: description of your change"
git push origin feature/your-improvement
```

Contributions can include new networking labs, topology improvements, documentation updates, troubleshooting scenarios, security considerations, automation examples, packet analysis exercises, and general corrections.

---

##  Repository Status

```
Level:    Beginner → Intermediate
Focus:    Networking Foundations for Cybersecurity
Type:     Educational & Practical
Platform: Cisco Packet Tracer / Virtual Labs
Status:   🚧 Actively Developed
```

---

##  License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">

##  NETWORKING LABS

**Practical Networking Foundations for Cybersecurity**

Routing • Switching • Security • Troubleshooting • Automation

*"Understand the network. Secure the infrastructure. Analyze the traffic."*

[ Repository](https://github.com/Z1AD-Z/Networking-Labs) • [👤 GitHub Profile](https://github.com/Z1AD-Z)

</div>
