# Lab Observation: Centralized DHCP with Relay Across a Routed WAN

**Platform:** Cisco Packet Tracer
**Topic:** DHCP server, multiple pools, DHCP relay (`ip helper-address`), static routing
**Builds on:** Previous branch connectivity lab (static routing between sites)

---

## 1. Objective

Provide automatic IPv4 configuration to clients at two sites from a single DHCP server located in the Head Office, and confirm that clients in the remote Branch Office can obtain leases across the WAN by using DHCP relay.

---

## 2. Network Architecture

| Item | Head Office | Branch Office |
|---|---|---|
| Router | R1 | R2 |
| LAN subnet | 192.168.10.0/24 | 192.168.20.0/24 |
| LAN gateway | 192.168.10.1 (R1 Gi0/0) | 192.168.20.1 (R2 Gi0/0) |
| Key devices | SRV1 (DHCP), PC1 | PC2, PRN1 |

**WAN link (R1 to R2):** 10.0.0.0/30, point-to-point (R1 = 10.0.0.1, R2 = 10.0.0.2, as used by the static routes in section 7).

```
 [PC1]--[SW]--(Gi0/0) R1 (Se/Gi)---10.0.0.0/30---(Se/Gi) R2 (Gi0/0)--[SW]--[PC2][PRN1]
         |      192.168.10.1                          192.168.20.1
       [SRV1]
   192.168.10.20
```

---

## 3. DHCP Server (SRV1)

SRV1 provides centralized DHCP for both sites and uses a **static** IPv4 configuration so it is always reachable at a predictable address.

| Parameter | Value |
|---|---|
| IP address | 192.168.10.20 |
| Subnet mask | 255.255.255.0 |
| Default gateway | 192.168.10.1 |

---

## 4. DHCP Pools

Two pools are configured on SRV1 (Services > DHCP).

| Setting | HEAD-OFFICE | BRANCH-OFFICE |
|---|---|---|
| Network | 192.168.10.0/24 | 192.168.20.0/24 |
| Default gateway | 192.168.10.1 | 192.168.20.1 |
| Subnet mask | 255.255.255.0 | 255.255.255.0 |
| Start IP | 192.168.10.100 | 192.168.20.100 |
| Max users | 50 | 50 |
| Resulting range | 192.168.10.100 - .149 | 192.168.20.100 - .149 |

Both ranges start at .100, which keeps them clear of the static addresses used by routers, switches, the server and the printer.

> **Important:** the pool is selected by the subnet of the request. For relayed requests, the router's relay interface address (giaddr) tells SRV1 which pool to use. This is why the BRANCH-OFFICE pool is matched when the request comes through R2 (192.168.20.1).

---

## 5. DHCP Clients

PC1 and PC2 are set to obtain IPv4 settings automatically (DHCP).

| Client | Expected pool | Leased IP | Mask | Gateway |
|---|---|---|---|---|
| PC1 | HEAD-OFFICE | *record from IP Configuration* | *record* | *record* |
| PC2 | BRANCH-OFFICE | *record from IP Configuration* | *record* | *record* |

Values must be taken from the actual leases shown in Packet Tracer, not assumed.

---

## 6. DHCP Relay

**Why it is needed:** a DHCP Discover is a broadcast, and routers do not forward broadcasts. SRV1 is in the Head Office, so PC2 in the Branch Office cannot reach it without help.

**How it works:**

1. PC2 broadcasts a DHCP Discover on 192.168.20.0/24.
2. R2, with a helper address configured, converts it into a unicast packet to 192.168.10.20 and records its own receiving interface address (192.168.20.1) as the relay agent address.
3. SRV1 uses that address to choose the BRANCH-OFFICE pool and sends the offer back to the relay agent.
4. R2 delivers the offer to PC2. The same relay path handles Request and Acknowledgement.

**Configuration on R2:**

```
interface GigabitEthernet0/0
 ip helper-address 192.168.10.20
```

The command belongs on the interface that **receives the client broadcasts** (the Branch LAN interface), pointing to the DHCP server.

---

## 7. Routing

Static routing is retained from the previous lab.

**R1**
```
ip route 192.168.20.0 255.255.255.0 10.0.0.2
```

**R2**
```
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

DHCP relay does not replace routing. The relayed request travels R2 to R1 to SRV1, and the reply travels back to 192.168.20.1. Both routers therefore need valid routes in both directions.

---

## 8. Troubleshooting

### Issue: PC2 did not obtain a DHCP lease

| | |
|---|---|
| **Symptom** | PC2 showed an address in 169.254.0.0/16 (APIPA) instead of a Branch Office address. |
| **Meaning** | PC2 sent DHCP requests but received no usable reply and self-assigned a link-local address. |
| **Cause** | DHCP relay on R2 was missing or incorrect, so PC2's broadcast never reached SRV1. |
| **Fix** | Checked and corrected the relay command on R2 Gi0/0: `ip helper-address 192.168.10.20` |
| **Re-test** | Set PC2 back to DHCP to request a new lease. |
| **Result** | PC2 obtained a valid configuration from the BRANCH-OFFICE pool. Confirm the exact values from the saved lease screenshot. |

### General checklist for a failed relay lease

1. Does the client show 169.254.x.x? The lease failed.
2. Is `ip helper-address` on the correct (client-facing) interface and does it point to 192.168.10.20?
3. Can R2 reach 192.168.10.20? Ping from R2.
4. Does SRV1 have a route or gateway back to 192.168.20.0/24 (via 192.168.10.1)?
5. Is the DHCP service **On** in SRV1 and does a pool match the relay interface subnet?
6. Is the pool exhausted or do its ranges conflict with static addresses?
7. Are the interfaces up/up (`show ip interface brief`) and are the routes present (`show ip route`)?

---

## 9. Verification Commands

| Command / location | Purpose |
|---|---|
| `show ip interface brief` | Interface status and addresses |
| `show ip route` | Confirm static and connected routes |
| `show running-config` | Confirm `ip helper-address` and routes |
| `show interfaces status` | Switch port status |
| End device > IP Configuration | Confirm leased address, mask, gateway |
| SRV1 > Services > DHCP | Confirm pool settings |

---

## 10. Connectivity Verification

Record only results actually observed in Packet Tracer.

| # | Test | Result | Notes |
|---|---|---|---|
| 1 | PC1 to Head Office gateway (192.168.10.1) | *Pass / Fail* | |
| 2 | PC2 to Branch Office gateway (192.168.20.1) | *Pass / Fail* | |
| 3 | PC1 to SRV1 (192.168.10.20) | *Pass / Fail* | |
| 4 | PC2 to PRN1 | *Pass / Fail* | |
| 5 | PC1 to PC2 | *Pass / Fail* | |
| 6 | PC2 to SRV1 | *Pass / Fail* | Validates the relay and WAN path |

Note: the first ping in Packet Tracer may time out while ARP resolves, so repeat before recording a failure.

---

## 11. Security Considerations

DHCP automates addressing but provides no access control or confidentiality. Any device that connects can request a lease, and a rogue DHCP server could hand out false gateway settings.

Production protections to consider:

- **DHCP snooping** to block rogue servers
- **Dynamic ARP inspection** and **IP source guard**
- **Port security** to limit devices per port
- **ACLs** and firewall policies to restrict who can reach SRV1
- Secure device management (SSH, strong credentials)
- Network monitoring and logging of DHCP activity
- Lease reservations for devices that must keep a fixed address

---

## 12. Lessons Learned

- DHCP automates IPv4 configuration for clients.
- Pools define the address ranges and parameters handed out, and a pool matches the subnet of the request.
- Infrastructure devices (routers, switches, servers, printers) keep static addresses outside the pool ranges.
- Routers do not forward DHCP broadcasts, so a remote server needs a relay agent.
- `ip helper-address` goes on the interface that receives the client broadcasts.
- Relay does not replace routing; both directions must be routable.
- A 169.254.0.0/16 address indicates the client failed to obtain a lease.
- Verify with real device output and document only confirmed results.

---

## 13. Possible Improvements

- Add DNS server settings to the pools.
- Add excluded or reserved addresses explicitly.
- Replace static routes with a dynamic routing protocol (e.g. OSPF).
- Test lease renewal and pool exhaustion.
- Add screenshots of leases, pool configuration and ping results.