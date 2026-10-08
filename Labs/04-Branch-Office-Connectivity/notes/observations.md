# Observations

## 1. Network Architecture

The network was designed as a two-site architecture consisting of:

- Head Office
- Branch Office

The two locations are connected through a point-to-point WAN-style
link between routers R1 and R2.

The Head Office uses the `192.168.10.0/24` network, while the Branch
Office uses the `192.168.20.0/24` network.

The WAN link uses the `10.0.0.0/30` network.

## 2. Head Office

The Head Office consists of:

- Router R1
- Switch S1
- PC1
- SRV1

The Head Office LAN uses:

```text
192.168.10.0/24

R1 provides the default gateway:

192.168.10.1

S1 was configured with the management address:

192.168.10.2/24
3. Branch Office

The Branch Office consists of:

Router R2
Switch S2
PC2
PRN1

The Branch Office LAN uses:

192.168.20.0/24

R2 provides the default gateway:

192.168.20.1

S2 was configured with the management address:

192.168.20.2/24
4. WAN Connectivity

R1 and R2 were connected using a point-to-point WAN-style link.

The addressing used on the WAN link is:

R1 Gi0/1 → 10.0.0.1/30
R2 Gi0/1 → 10.0.0.2/30

Connectivity between the two router interfaces was successfully verified
using ICMP Echo Requests.

5. IPv4 Addressing

Static IPv4 addressing was configured as follows:

Device	IP Address	Subnet Mask	Default Gateway
PC1	192.168.10.10	255.255.255.0	192.168.10.1
SRV1	192.168.10.20	255.255.255.0	192.168.10.1
PC2	192.168.20.10	255.255.255.0	192.168.20.1
PRN1	192.168.20.20	255.255.255.0	192.168.20.1
6. Static Routing

Static routes were configured on both routers to provide reachability
between the two remote LANs.

R1
ip route 192.168.20.0 255.255.255.0 10.0.0.2
R2
ip route 192.168.10.0 255.255.255.0 10.0.0.1

The routing tables were verified using:

show ip route

The static routes appeared in the routing tables with the S route
code.

7. Local Connectivity Verification

Head Office connectivity was verified between:

PC1 → R1
PC1 → SRV1

Branch Office connectivity was verified between:

PC2 → R2
PC2 → PRN1

The local connectivity tests were successful.

8. Inter-Site Connectivity Verification

End-to-end connectivity was verified between the two sites using ICMP.

The following tests were successfully completed:

PC1 → PC2
PC1 → PRN1
PC2 → PC1
PC2 → SRV1

These tests confirmed that traffic could travel from one local network
through R1, across the WAN link, through R2, and reach the remote
destination network.

9. Routing Verification

The following commands were used during verification:

show ip interface brief
show ip route
show running-config
show interfaces status

show ip interface brief was used to verify interface IP addresses
and interface status.

show ip route was used to verify directly connected networks and
static routes.

show interfaces status was used to verify switch port status.

10. Observations

The WAN link between R1 and R2 became operational after both router
interfaces were configured and enabled.

The initial state of R1 Gi0/1 was up/down before R2 was configured.
After configuring R2 Gi0/1 with 10.0.0.2/30 and enabling the
interface, the WAN link became up/up.

The static routes were required because each router initially knew only
its directly connected networks.

Both forward and return routes were required for successful end-to-end
communication between the two sites.

11. Security Considerations

The current lab demonstrates connectivity and routing between two sites.
Static routing itself does not provide traffic filtering or
confidentiality.

Additional security controls would be required in a real deployment,
such as:

Site-to-site VPN
ACLs
Firewall policies
Secure device management
Network monitoring and logging
12. Lessons Learned
A multi-site network requires separate IP networks for each location.
Routers provide Layer 3 communication between different networks.
A point-to-point link can be used to connect two routers.
Static routes can provide communication between remote networks.
Both routers must have appropriate forward and return routes.
show ip route is essential for verifying routing decisions.
show ip interface brief is useful for validating interface state
and addressing.
End-to-end ICMP testing validates the complete path between sites.
WAN connectivity and routing should be verified separately before
troubleshooting end-to-end communication.

## Pourquoi ce fichier est adapté

Il documente ce qu’on a réellement fait :

```text
2 sites
↓
2 LANs
↓
WAN /30
↓
R1 + R2
↓
Static routes
↓
Verification
↓
Inter-site connectivity

Je n’ai pas ajouté d’OSPF, VPN, ACL ou autre technologie comme si elle avait été réalisée ; elles restent dans les considérations/futures extensions.