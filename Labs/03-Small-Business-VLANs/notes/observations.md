# Observations

## 1. VLAN Segmentation

The network was segmented into three VLANs:

- VLAN 10 — ADMIN
- VLAN 20 — SALES
- VLAN 30 — SERVICES

PC1 was assigned to VLAN 10, PC2 to VLAN 20, while SRV1 and PRN1
were assigned to VLAN 30.

This segmentation creates separate Layer 2 broadcast domains.

## 2. Access Port Configuration

The end devices were connected using access ports:

- Fa0/1 → PC1 → VLAN 10
- Fa0/2 → PC2 → VLAN 20
- Fa0/3 → SRV1 → VLAN 30
- Fa0/4 → PRN1 → VLAN 30

Multiple access ports can belong to the same VLAN, as demonstrated
by Fa0/3 and Fa0/4 in VLAN 30.

## 3. Router Configuration

R1 was configured with:

- Hostname: R1
- GigabitEthernet0/0: enabled
- No IP address configured on Gi0/0

The router link is reserved for a future Router-on-a-Stick /
Inter-VLAN Routing implementation.

## 4. IPv4 Addressing

Static IPv4 addressing was configured as follows:

| Device | IP Address | Subnet Mask | VLAN |
|---|---|---|---|
| PC1 | 192.168.10.10 | 255.255.255.0 | 10 |
| PC2 | 192.168.20.10 | 255.255.255.0 | 20 |
| SRV1 | 192.168.30.5 | 255.255.255.0 | 30 |
| PRN1 | 192.168.30.20 | 255.255.255.0 | 30 |

Default gateways were intentionally left unconfigured because
Inter-VLAN Routing is not implemented in this lab.

## 5. Verification

The following commands were used to verify the network configuration:

```text
show vlan brief
show interfaces status
show mac address-table
show running-config
show ip interface brief
VLAN Verification

show vlan brief was used to verify VLAN creation and access-port
membership.

The final VLAN assignments were verified as follows:

Fa0/1 → VLAN 10
Fa0/2 → VLAN 20
Fa0/3 → VLAN 30
Fa0/4 → VLAN 30
Interface Verification

show interfaces status was used to verify port status, port mode,
and VLAN assignment.

The end-device ports were verified as access ports.

MAC Address Verification

show mac address-table was used to verify dynamic MAC address
learning on the switch.

The switch learned the MAC addresses of devices that generated
traffic during the verification process.

6. Troubleshooting
Issue: End-device ports were operating in trunk mode

During the initial verification, the ports connected to the end
devices were found to be operating in trunk mode.

Detection

The following command was used:

show interfaces trunk

The command showed Fa0/1 through Fa0/4 operating as trunk ports.

Resolution

The ports were explicitly changed to access mode:

interface range FastEthernet0/1 - 4
 switchport mode access

Fa0/24 was also explicitly configured as an access port for the
current lab design.

Validation

The final port configuration was verified using:

show interfaces status

The end-device ports were then confirmed to operate as access ports
with the expected VLAN assignments.

7. Connectivity

SRV1 and PRN1 were assigned to VLAN 30 and are expected to communicate
within the same Layer 2 network.

Devices assigned to different VLANs are expected to remain isolated
because no Layer 3 Inter-VLAN Routing is configured in this lab.

Connectivity was verified using ICMP Echo Requests.

8. Security Considerations

VLAN segmentation provides logical separation between the business
departments and separates their Layer 2 broadcast domains.

However, VLAN segmentation alone is not a complete security control.
Controlled communication between VLANs would require Layer 3 routing
combined with appropriate security policies such as ACLs.

9. Lessons Learned
VLANs provide logical network segmentation on a Layer 2 switch.
Access ports are used to connect end devices to a specific VLAN.
Multiple access ports can belong to the same VLAN.
Trunk ports are used when a single link must carry multiple VLANs.
VLAN membership can be verified using show vlan brief.
Interface status and VLAN assignments can be verified using
show interfaces status.
MAC address learning can be verified using show mac address-table.
Devices in different VLANs cannot communicate directly at Layer 2.
Inter-VLAN communication requires a Layer 3 routing mechanism.
Verification commands are essential for validating network configuration.
Troubleshooting helps identify configuration errors before final
validation.