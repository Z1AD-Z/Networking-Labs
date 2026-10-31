# Observations

## 1. Network Architecture

The network consists of two sites:

- Head Office
- Branch Office

The sites are connected through a point-to-point WAN link between R1
and R2.

The Head Office LAN uses `192.168.10.0/24`, while the Branch Office
LAN uses `192.168.20.0/24`.

The WAN link uses `10.0.0.0/30`.

## 2. DHCP Server

SRV1 provides centralized DHCP services for both sites.

The server uses a static IPv4 configuration:

- IP address: `192.168.10.20`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.10.1`

A static address ensures that the server remains reachable at a
predictable address.

## 3. DHCP Pools

Two DHCP pools were configured on SRV1.

### HEAD-OFFICE

- Network: `192.168.10.0/24`
- Starting IP address: `192.168.10.100`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.10.1`
- Maximum users: 50

### BRANCH-OFFICE

- Network: `192.168.20.0/24`
- Starting IP address: `192.168.20.100`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.20.1`
- Maximum users: 50

The configured pool ranges avoid the static addresses assigned to
the routers, switches, server, and printer.

## 4. DHCP Clients

PC1 and PC2 are configured to obtain their IPv4 settings automatically.

- PC1 receives its configuration from the HEAD-OFFICE pool.
- PC2 receives its configuration from the BRANCH-OFFICE pool.

The assigned IP addresses should be recorded from the actual DHCP
leases displayed in Packet Tracer.

## 5. DHCP Relay

The DHCP server is located in the Head Office, while PC2 is located
in the Branch Office.

DHCP client discovery messages are broadcasts and are not normally
forwarded by routers.

To allow PC2 to obtain its configuration from SRV1, DHCP relay was
configured on R2's LAN interface:

```text
interface GigabitEthernet0/0
 ip helper-address 192.168.10.20


This command relays eligible client broadcast requests to the
central DHCP server at 192.168.10.20.

## 6. Troubleshooting

Issue: PC2 did not receive a DHCP lease
During the initial test, PC2 displayed an automatic address in the
169.254.0.0/16 range instead of an address from the Branch Office
DHCP pool.

This indicated that PC2 had not successfully obtained a DHCP lease.
Resolution
The DHCP relay configuration on R2 was checked and corrected.

The following command was configured on R2 GigabitEthernet0/0:
ip helper-address 192.168.10.20


PC2 was then switched back to DHCP to request its configuration again.
Result
PC2 subsequently obtained a DHCP configuration successfully.

The assigned address, subnet mask, and default gateway should be
confirmed using the saved PC2 DHCP lease screenshot.

## 7. Routing

Static routing is retained from the previous branch connectivity lab.
R1
ip route 192.168.20.0 255.255.255.0 10.0.0.2


R2
ip route 192.168.10.0 255.255.255.0 10.0.0.1


These routes provide reachability between the two LANs.

DHCP relay does not replace routing. The routers must still have
valid routes for the DHCP request and response traffic.

## 8. Verification Commands

The following commands are used to verify the network configuration:
show ip interface brief
show ip route
show running-config
show interfaces status


The DHCP client settings are verified through the end-device
IP Configuration window.

The DHCP pools are verified through:

SRV1 > Services > DHCP

## 9. Connectivity Verification

Connectivity tests should be documented using the actual results
observed in Packet Tracer.

The planned tests include:
- PC1 to the Head Office gateway
- PC2 to the Branch Office gateway
- PC1 to SRV1
- PC2 to PRN1
- PC1 to PC2
- PC2 to SRV1
Only tests that have been performed successfully should be recorded
as confirmed results.

## 10. Security Considerations

DHCP automates IP configuration but does not, by itself, provide
network access control or confidentiality.

In a production environment, additional protections may include:
- DHCP snooping
- Port security
- Access Control Lists (ACLs)
- Firewall policies
- Secure device management
- Network monitoring

## 11. Lessons Learned

- DHCP automates IPv4 address configuration for clients.
- DHCP pools define the address ranges and network parameters
  distributed to clients.
- Infrastructure devices can retain static IP addresses.
- DHCP requests from another subnet require a relay mechanism when
  the DHCP server is not on the local network.
- ip helper-address must be configured on the router interface
  receiving the client broadcasts.
- DHCP relay does not replace routing between network sites.
- An automatic 169.254.0.0/16 address can indicate that a client
  failed to obtain a DHCP lease.
- Verification and troubleshooting are essential when deploying
  centralized network services.