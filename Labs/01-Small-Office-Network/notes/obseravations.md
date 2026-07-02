# Observations

## Summary

This lab demonstrates the successful deployment of a basic small office Local Area Network (LAN) using Cisco Packet Tracer.

The network was designed to provide reliable communication between multiple end devices through a Cisco router and a Cisco Layer 2 switch while following fundamental networking best practices.

---

## Network Components

The network consists of:

- 1 Cisco 1941 Router (R1)
- 1 Cisco Catalyst 2960 Switch (S1)
- 2 Workstations (PC1 and PC2)
- 1 Server (SRV1)
- 1 Network Printer (PRN1)

All devices are connected using Ethernet and belong to the same IPv4 subnet.

---

## Configuration Summary

The following configuration tasks were completed successfully:

- Assigned hostnames to the router and switch.
- Configured the router's LAN interface with a static IPv4 address.
- Configured the switch management interface (VLAN 1).
- Configured the switch default gateway.
- Assigned static IPv4 addresses to all end devices.
- Verified physical connectivity.
- Saved the running configurations to startup configurations.

---

## Verification Results

Network connectivity was successfully verified using ICMP Echo Requests (ping).

The following tests completed successfully:

- PC1 → Router
- PC1 → PC2
- PC1 → Server
- PC1 → Printer
- Router → All End Devices

All devices responded successfully without packet loss.

---

## Key Concepts Practiced

- IPv4 addressing
- Ethernet LAN design
- Cisco IOS navigation
- Router configuration
- Layer 2 switch configuration
- Switch management interface configuration
- Static IP addressing
- Basic network verification
- Configuration management

---

## Lessons Learned

This lab reinforced the importance of:

- Proper IP address planning before deployment.
- Maintaining consistent device naming conventions.
- Saving device configurations after completing changes.
- Verifying network connectivity after every configuration step.
- Organizing project documentation to improve maintainability.

---

## Future Improvements

The current network serves as the foundation for more advanced networking scenarios.

Future enhancements may include:

- DHCP deployment
- VLAN implementation
- Inter-VLAN Routing
- Access Control Lists (ACLs)
- Network Address Translation (NAT)
- Dynamic Routing Protocols (OSPF)
- Internet connectivity
- Network monitoring

---

## Conclusion

The objectives of this lab were successfully achieved.

A functional small office LAN was designed, configured, verified, and documented. This project establishes a solid foundation for subsequent networking labs and demonstrates practical experience with Cisco networking fundamentals.