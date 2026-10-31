# DHCP Deployment

## Overview

This project demonstrates the deployment of centralized Dynamic Host Configuration Protocol (DHCP) services in a small enterprise network using Cisco Packet Tracer.

A DHCP server located at the Head Office assigns IPv4 settings to local clients and, through DHCP relay, to a client at the Branch Office. The lab builds on the site-to-site routing architecture from Lab 04 and demonstrates DHCP pools, automatic IPv4 configuration, DHCP relay, static addressing for infrastructure devices, and end-to-end connectivity verification.

## Scenario

An organization operates from two locations:

- Head Office
- Branch Office

Both sites require consistent IPv4 configuration for client devices, while the network team wants to manage address allocation centrally.

The Head Office hosts the DHCP server. PC1 receives its address from the local DHCP pool. PC2 receives its address from a separate pool through DHCP relay on router R2. The two LANs remain connected using the existing point-to-point WAN link and static routes.

## Objectives

- Design a two-site network with centralized DHCP services.
- Configure a Cisco Server-PT device with two DHCP pools.
- Configure PC1 and PC2 to obtain IPv4 settings automatically.
- Configure DHCP relay on R2 for the Branch Office LAN.
- Preserve static IP addresses for routers, switch management interfaces, the server, and the printer.
- Verify DHCP leases, routing, and local/inter-site connectivity.
- Document the implementation with configuration files and screenshots.

## Requirements

- Cisco Packet Tracer 8.2.2
- Basic knowledge of IPv4 addressing and subnetting
- Basic understanding of DHCP, default gateways, and static routing
- 2 Cisco 1941 routers
- 2 Cisco 2960-24TT switches
- 1 Server-PT device
- 2 PC-PT devices
- 1 Printer-PT device

## Network Architecture

The network has two LANs connected by a point-to-point WAN-style Ethernet link.

```text
                         HEAD OFFICE

             PC1             SRV1 (DHCP)
              |                  |
              +-------- S1 ------+
                       |
                      R1
                       |
                WAN: 10.0.0.0/30
                       |
                      R2
                       |
                      S2
                     /  \
                   PC2  PRN1

                       BRANCH OFFICE
```

### Network Topology

![DHCP Deployment Network Topology](screenshots/network-topology.png)

### Head Office

The Head Office uses the network `192.168.10.0/24`.

Devices:
- R1 — Head Office router
- S1 — Head Office switch
- SRV1 — Central DHCP server
- PC1 — Head Office client

### Branch Office

The Branch Office uses the network `192.168.20.0/24`.

Devices:
- R2 — Branch Office router
- S2 — Branch Office switch
- PC2 — Branch Office client
- PRN1 — Network printer

### WAN Link

The routers are connected through the point-to-point network `10.0.0.0/30`.

- R1 GigabitEthernet0/1: `10.0.0.1/30`
- R2 GigabitEthernet0/1: `10.0.0.2/30`

## Device Inventory

| Device | Packet Tracer model | Role |
|---|---|---|
| R1 | Cisco 1941 | Head Office gateway and inter-site routing |
| R2 | Cisco 1941 | Branch gateway, inter-site routing, and DHCP relay |
| S1 | Cisco 2960-24TT | Head Office LAN connectivity |
| S2 | Cisco 2960-24TT | Branch Office LAN connectivity |
| SRV1 | Server-PT | Central DHCP server |
| PC1 | PC-PT | Head Office DHCP client |
| PC2 | PC-PT | Branch Office DHCP client |
| PRN1 | Printer-PT | Branch printer with static IPv4 address |

## IP Addressing Plan

| Device | Interface | IPv4 address | Subnet mask | Default gateway / next hop |
|---|---|---|---|---|
| R1 | GigabitEthernet0/0 | 192.168.10.1 | 255.255.255.0 | — |
| R1 | GigabitEthernet0/1 | 10.0.0.1 | 255.255.255.252 | — |
| S1 | VLAN 1 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| SRV1 | FastEthernet0 | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |
| PC1 | FastEthernet0 | Assigned by DHCP | 255.255.255.0 | 192.168.10.1 |
| R2 | GigabitEthernet0/0 | 192.168.20.1 | 255.255.255.0 | — |
| R2 | GigabitEthernet0/1 | 10.0.0.2 | 255.255.255.252 | — |
| S2 | VLAN 1 | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC2 | FastEthernet0 | Assigned by DHCP | 255.255.255.0 | 192.168.20.1 |
| PRN1 | FastEthernet0 | 192.168.20.20 | 255.255.255.0 | 192.168.20.1 |

## Port Assignment

### Head Office — S1

| Switch port | Connected device | Port mode |
|---|---|---|
| FastEthernet0/1 | PC1 | Access (default VLAN 1) |
| FastEthernet0/2 | SRV1 | Access (default VLAN 1) |
| FastEthernet0/24 | R1 GigabitEthernet0/0 | Access (default VLAN 1) |

### Branch Office — S2

| Switch port | Connected device | Port mode |
|---|---|---|
| FastEthernet0/1 | PC2 | Access (default VLAN 1) |
| FastEthernet0/2 | PRN1 | Access (default VLAN 1) |
| FastEthernet0/24 | R2 GigabitEthernet0/0 | Access (default VLAN 1) |

### WAN

| Device/interface | Connected to |
|---|---|
| R1 GigabitEthernet0/1 | R2 GigabitEthernet0/1 |

## DHCP Design

DHCP runs on Server-PT SRV1 at `192.168.10.20`. Two independent pools provide client addresses in the appropriate LAN.

### Pool 1 — HEAD-OFFICE

| Parameter | Value |
|---|---|
| Pool name | HEAD-OFFICE |
| Default gateway | 192.168.10.1 |
| DNS server | 0.0.0.0 if no DNS server is configured |
| Starting IP address | 192.168.10.100 |
| Subnet mask | 255.255.255.0 |
| Maximum users | 50 |

This pool serves clients in `192.168.10.0/24`, including PC1. The intended allocation range is `192.168.10.100`–`192.168.10.149`.

### Pool 2 — BRANCH-OFFICE

| Parameter | Value |
|---|---|
| Pool name | BRANCH-OFFICE |
| Default gateway | 192.168.20.1 |
| DNS server | 0.0.0.0 if no DNS server is configured |
| Starting IP address | 192.168.20.100 |
| Subnet mask | 255.255.255.0 |
| Maximum users | 50 |

This pool serves clients in `192.168.20.0/24`, including PC2. The intended allocation range is `192.168.20.100`–`192.168.20.149`.

The server, routers, switch management interfaces, and printer use static addresses outside the DHCP pools to avoid address conflicts.

## DHCP Relay

PC1 and SRV1 are on the same LAN, so PC1's DHCP broadcasts can reach the local server directly. PC2 is in a different IP network; routers do not forward DHCP broadcasts by default.

R2 therefore relays DHCP requests received on its Branch Office LAN interface to SRV1 using:

```text
interface GigabitEthernet0/0
 ip helper-address 192.168.10.20
```

The helper address belongs on R2's interface that receives the client's DHCP broadcast, not on the WAN interface. DHCP relay does not replace routing: R1 and R2 still need their static routes for return and inter-site traffic.

## Routing Plan

Static routing is used between the two LANs.

### R1

```text
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

R1 forwards traffic destined for `192.168.20.0/24` to R2 at `10.0.0.2`.

### R2

```text
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

R2 forwards traffic destined for `192.168.10.0/24` to R1 at `10.0.0.1`.

Both forward and return routes are required for successful end-to-end communication.

## Configuration Tasks

### Router R1

- Configure hostname R1.
- Configure GigabitEthernet0/0 as `192.168.10.1/24`.
- Configure GigabitEthernet0/1 as `10.0.0.1/30`.
- Enable both interfaces.
- Add a static route to the Branch Office LAN.
- Save the configuration.

Configuration file: [`configs/R1.txt`](configs/R1.txt)

### Router R2

- Configure hostname R2.
- Configure GigabitEthernet0/0 as `192.168.20.1/24`.
- Configure GigabitEthernet0/1 as `10.0.0.2/30`.
- Configure DHCP relay on GigabitEthernet0/0 using `ip helper-address 192.168.10.20`.
- Enable both interfaces.
- Add a static route to the Head Office LAN.
- Save the configuration.

Configuration file: [`configs/R2.txt`](configs/R2.txt)

### Switches S1 and S2

- Configure hostnames S1 and S2.
- Configure management addresses on VLAN 1.
- Configure the appropriate default gateways.
- Keep connected end-device and router ports in the default access VLAN.
- Save the configurations.

Configuration files: [`configs/S1.txt`](configs/S1.txt) and [`configs/S2.txt`](configs/S2.txt)

### Server SRV1

- Configure the static IPv4 address `192.168.10.20/24`.
- Set default gateway `192.168.10.1`.
- Enable the DHCP service.
- Create the `HEAD-OFFICE` and `BRANCH-OFFICE` pools with the parameters described above.

### PCs PC1 and PC2

- Select DHCP in Desktop > IP Configuration.
- Verify that each client receives an address from the correct pool.
- Verify the assigned subnet mask and default gateway.

### Printer PRN1

- Configure static address `192.168.20.20/24`.
- Set default gateway `192.168.20.1`.

## Configuration Evidence

### Network Topology

![Network Topology](screenshots/network-topology.png)

### R1 Configuration

![R1 Running Configuration](screenshots/r1-running-config.png)

### R2 Configuration

![R2 Running Configuration](screenshots/r2-running-config.png)

### R2 DHCP Relay

![R2 DHCP Relay Configuration](screenshots/r2-dhcp-relay-config.png)

### Switch Management Interfaces

#### S1

![S1 Interface Status](screenshots/s1-ip-interface-brief.png)

#### S2

![S2 Interface Status](screenshots/s2-ip-interface-brief.png)

### Routing Tables

#### R1

![R1 Routing Table](screenshots/routing-table-r1.png)

#### R2

![R2 Routing Table](screenshots/routing-table-r2.png)

### Printer Configuration

![Printer IP Configuration](screenshots/printer-ip-configuration.png)

## Verification

The following commands are useful for validating the configuration:

```text
show ip interface brief
show running-config
show ip route
show interfaces status
```

- `show ip interface brief` checks interface addresses and operational status.
- `show ip route` checks connected networks and static routes.
- `show running-config` checks router settings, including the DHCP relay configuration on R2.
- On each client, Desktop > IP Configuration confirms whether DHCP assigned an address, subnet mask, and gateway.
- On SRV1, Services > DHCP confirms that the DHCP service and pools are enabled.

## Expected Results

| Test | Expected result | What it validates |
|---|---|---|
| PC1 receives DHCP settings | Success | Local DHCP pool |
| PC2 receives DHCP settings | Success | DHCP relay and Branch Office pool |
| PC1 pings SRV1 | Success | Head Office LAN connectivity |
| PC2 pings PRN1 | Success | Branch Office LAN connectivity |
| PC1 pings PC2 | Success | Inter-site routing |
| PC2 pings SRV1 | Success | Remote access to the central server |

## Connectivity Verification

Connectivity is tested using ICMP Echo Requests. The following screenshot provides the available PC2-to-SRV1 connectivity evidence:

![PC2 to SRV1 Connectivity](screenshots/pc2-to-srv1-connectivity.png)

## Troubleshooting

### PC2 receives an APIPA address

If PC2 displays an address in the `169.254.0.0/16` range and reports that DHCP failed, it has not received a lease from the DHCP server.

Check the following in order:

1. Confirm that the DHCP service is enabled on SRV1.
2. Confirm that the `BRANCH-OFFICE` pool uses network `192.168.20.0/24`, mask `255.255.255.0`, and gateway `192.168.20.1`.
3. Confirm that R2 GigabitEthernet0/0 has `ip helper-address 192.168.10.20`.
4. Confirm that R1 and R2 have their correct interface addresses and are operational.
5. Confirm that both static routes exist and that SRV1 uses `192.168.10.1` as its default gateway.
6. On PC2, select Static and then DHCP again to request a new lease.

### DHCP works at the Head Office but fails at the Branch Office

A local DHCP client can reach a server on its own LAN using broadcasts. A remote client needs DHCP relay. Verify the helper address on R2's client-facing LAN interface and confirm bidirectional routing between the two sites.

### Incorrect gateway received by a client

Check the default-gateway field in the matching DHCP pool. The Head Office pool must advertise `192.168.10.1`; the Branch Office pool must advertise `192.168.20.1`.

## Security Considerations

DHCP automates address configuration; it does not provide network security by itself. In a production environment, consider DHCP snooping where supported, access controls, secure device management, firewall policies, monitoring, and a site-to-site VPN when confidentiality across an untrusted WAN is required.

## Lessons Learned

- DHCP centralizes automatic IPv4 configuration for clients.
- A DHCP pool must match the subnet in which the client resides.
- Network infrastructure and servers should use stable addresses where required.
- Routers do not forward DHCP broadcasts by default.
- DHCP relay allows a remote subnet to use a centralized DHCP server.
- The return path and static routes still matter when DHCP services are centralized.
- DHCP leases, routing tables, interface status, and ping tests provide complementary verification evidence.

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- DHCP
- DHCP relay (`ip helper-address`)
- IPv4
- Static routing
- Ethernet
- ICMP

## Skills Demonstrated

- Network design for a multi-site environment
- DHCP pool configuration
- Automatic IPv4 configuration
- DHCP relay troubleshooting
- Router and switch configuration
- Static routing
- Addressing and gateway verification
- End-to-end connectivity testing
- Technical documentation

## Project Structure

```text
05-DHCP-Deployment/
├── README.md
├── DHCP-Deployment.pkt
├── configs/
│   ├── R1.txt
│   ├── R2.txt
│   ├── S1.txt
│   ├── S2.txt
│   └── SRV1-DHCP-Settings.md
├── notes/
└── screenshots/
    ├── network-topology.png
    ├── r1-running-config.png
    ├── r2-running-config.png
    ├── r2-dhcp-relay-config.png
    ├── s1-ip-interface-brief.png
    ├── s2-ip-interface-brief.png
    ├── routing-table-r1.png
    ├── routing-table-r2.png
    ├── printer-ip-configuration.png
    └── pc2-to-srv1-connectivity.png
```

## Files

| File | Description |
|---|---|
| `DHCP-Deployment.pkt` | Cisco Packet Tracer project |
| `configs/R1.txt` | R1 configuration |
| `configs/R2.txt` | R2 configuration, including DHCP relay |
| `configs/S1.txt` | S1 management configuration |
| `configs/S2.txt` | S2 management configuration |
| `configs/SRV1-DHCP-Settings.md` | DHCP server pool settings |
| `notes/` | Project notes |
| `screenshots/` | Network topology, device configuration, routing, and connectivity evidence |

## Future Improvements

- DHCP snooping and other Layer 2 security controls
- High availability for DHCP services
- Dynamic routing with OSPF
- Site-to-site VPN
- ACLs and firewall integration
- DHCP options for additional services
- Network monitoring and centralized logging
- IPv6 address configuration using DHCPv6 or SLAAC

## Author

**Ziad ZARABI**

Networking Portfolio

GitHub Repository: **Networking-Labs**
