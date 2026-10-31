SRV1 DHCP Settings
Overview
SRV1 is the central DHCP server for the Head Office and Branch Office networks in Lab 05 — DHCP Deployment.
Server IPv4 Configuration
Configure the server under Desktop → IP Configuration → Static.
Parameter	Value
Device name	SRV1
IPv4 address	192.168.10.20
Subnet mask	255.255.255.0
Default gateway	192.168.10.1
DNS server	Leave blank if no DNS service is configured; otherwise use the actual DNS server address


DHCP Service
In Packet Tracer, open Services → DHCP and set the DHCP service to On.
Pool 1 — HEAD-OFFICE
Parameter	Value
Pool name	HEAD-OFFICE
Default gateway	192.168.10.1
Start IP address	192.168.10.100
Subnet mask	255.255.255.0
Maximum number of users	50
DNS server	Leave blank if no DNS service is configured; otherwise use the actual DNS server address


Expected allocation range: 192.168.10.100–`192.168.10.149`.
Pool 2 — BRANCH-OFFICE
Parameter	Value
Pool name	BRANCH-OFFICE
Default gateway	192.168.20.1
Start IP address	192.168.20.100
Subnet mask	255.255.255.0
Maximum number of users	50
DNS server	Leave blank if no DNS service is configured; otherwise use the actual DNS server address


Expected allocation range: 192.168.20.100–`192.168.20.149`.
DHCP Relay
The Branch Office client PC2 is in a different subnet from SRV1. On R2, the DHCP relay command must be configured on the LAN interface that receives PC2's DHCP broadcasts:
interface GigabitEthernet0/0
 ip helper-address 192.168.10.20
R2 must also have a route to the Head Office network, and R1 must have a return route to the Branch Office network.
Client Configuration
Set PC1 and PC2 to Desktop → IP Configuration → DHCP. Verify that each receives an address from its own site's pool, the correct /24 subnet mask, and the correct default gateway.