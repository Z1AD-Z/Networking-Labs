# Lab Observations

## Lab Information

**Lab Name:** Two LANs with Static Routing

**Objective:**
Design, configure, and validate communication between two independent Local Area Networks (LANs) interconnected through a Wide Area Network (WAN) using static routing.

---

## Network Summary

The network consists of two geographically separated LANs connected by two Cisco routers over a point-to-point WAN link.

Each LAN contains a Layer 2 switch and end devices configured with static IPv4 addresses. Static routes were manually configured on both routers to enable communication between remote networks.

### LAN 1

- Network: 192.168.10.0/24
- Default Gateway: 192.168.10.1
- Devices:
  - R1
  - S1
  - PC1
  - SRV1

### LAN 2

- Network: 192.168.20.0/24
- Default Gateway: 192.168.20.1
- Devices:
  - R2
  - S2
  - PC2
  - PRN1

### WAN

- Network: 10.0.0.0/30
- R1: 10.0.0.1
- R2: 10.0.0.2

---

## Configuration Summary

The following components were successfully configured:

### Routers

- Hostnames configured.
- LAN interfaces configured.
- WAN interfaces configured.
- Interfaces activated using `no shutdown`.
- Static routes configured on both routers.
- Running configurations saved to startup configuration.

### Switches

- Hostnames configured.
- VLAN 1 management interfaces configured.
- Default gateways configured.
- Running configurations saved.

### End Devices

- Static IPv4 addresses assigned.
- Subnet masks configured.
- Default gateways configured.
- Network connectivity verified.

---

## Static Routing

Static routes were manually configured to enable communication between both LANs.

### R1

Destination Network:

- 192.168.20.0/24

Next Hop:

- 10.0.0.2

### R2

Destination Network:

- 192.168.10.0/24

Next Hop:

- 10.0.0.1

Routing tables were verified using:

```text
show ip route
```

The routing tables correctly displayed both directly connected and static routes.

---

## Connectivity Verification

Successful ICMP Echo Request and Echo Reply messages were verified between:

- R1 and R2 across the WAN link.
- PC1 and PC2.
- PC1 and PRN1.
- PC2 and SRV1.

These successful tests confirmed:

- Correct interface configuration.
- Proper default gateway configuration.
- Successful static routing.
- End-to-end communication between both LANs.

---

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- Ethernet
- IPv4
- Static Routing
- ICMP

---

## Skills Demonstrated

- Network topology design
- IPv4 addressing
- WAN configuration
- Point-to-point networking
- Cisco IOS configuration
- Router configuration
- Layer 2 switch configuration
- Static route implementation
- Routing table verification
- End-to-end connectivity testing
- Basic network troubleshooting
- Technical documentation

---

## Lessons Learned

This lab reinforced several fundamental networking concepts.

- Static routes must be configured on every router participating in the communication path.
- Each end device requires a correctly configured default gateway to communicate with remote networks.
- Routing tables should always be verified after adding static routes.
- Successful routing depends on correct interface addressing and operational interface status.
- Systematic verification significantly simplifies network troubleshooting.

---

## Conclusion

The objectives of this lab were successfully achieved.

Two independent LANs were interconnected through a point-to-point WAN link using static routing. All network devices were successfully configured, routing tables were validated, and end-to-end connectivity was confirmed through ICMP testing.

This lab provides a solid foundation for future routing technologies such as RIP, OSPF, and EIGRP, where static routing is replaced by dynamic routing protocols.