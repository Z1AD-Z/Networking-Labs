
# Lab 06 — OSPF Single-Area
# Laboratory Observations and Technical Analysis

## 1. Document Purpose

This document records the technical observations, verification results, and conclusions obtained during the implementation of the OSPF Single-Area laboratory.

It complements the main project documentation by providing a structured record of the network behavior observed in Cisco Packet Tracer.

The observations are based on the actual router outputs, routing tables, OSPF interface information, and end-to-end connectivity tests performed during the laboratory.

---

## 2. Laboratory Environment

| Parameter | Description |
|---|---|
| Laboratory | Lab 06 — OSPF Single-Area |
| Simulation Platform | Cisco Packet Tracer 8.2.2 |
| Routing Protocol | OSPFv2 |
| OSPF Process ID | 1 |
| OSPF Area | 0 |
| Router Count | 3 |
| Switch Count | 2 |
| End Devices | 2 |
| Topology | Linear, three-router topology |

### Network Components

The simulated network consists of two user LANs connected through an intermediate OSPF router.

- R1 acts as the Head Office gateway.
- R2 provides transit connectivity between the two edge routers.
- R3 acts as the Branch Office gateway.
- S1 and S2 provide Layer 2 connectivity within their respective LANs.
- PC1 and PC2 are used to validate end-to-end communication.

---

## 3. Initial Network Observations

### 3.1 IPv4 Addressing

The following addressing scheme was implemented:

| Device | Interface | IPv4 Address | Network |
|---|---|---|---|
| R1 | GigabitEthernet0/0 | 192.168.10.1/24 | Head Office LAN |
| R1 | GigabitEthernet0/1 | 10.0.0.1/30 | R1–R2 Transit |
| R2 | GigabitEthernet0/0 | 10.0.0.2/30 | R1–R2 Transit |
| R2 | GigabitEthernet0/1 | 10.0.0.5/30 | R2–R3 Transit |
| R3 | GigabitEthernet0/0 | 192.168.30.1/24 | Branch Office LAN |
| R3 | GigabitEthernet0/1 | 10.0.0.6/30 | R2–R3 Transit |

End-device addressing:

| Device | IPv4 Address | Default Gateway |
|---|---|---|
| PC1 | 192.168.10.10/24 | 192.168.10.1 |
| PC2 | 192.168.30.10/24 | 192.168.30.1 |

Two /30 subnets were used for the router transit links:

- R1–R2: 10.0.0.0/30
- R2–R3: 10.0.0.4/30

This addressing design provides two usable host addresses per transit network.

### 3.2 OSPF Router IDs

Unique Router IDs were manually assigned to the three routers.

| Router | Router ID | OSPF Process |
|---|---|---|
| R1 | 1.1.1.1 | 1 |
| R2 | 2.2.2.2 | 1 |
| R3 | 3.3.3.3 | 1 |

Using explicit Router IDs makes router identification predictable during OSPF neighbor verification and troubleshooting.

---

## 4. OSPF Neighbor Observations

The expected OSPF adjacencies were:

| Local Router | Expected Neighbor | Neighbor Router ID |
|---|---|---|
| R1 | R2 | 2.2.2.2 |
| R2 | R1 | 1.1.1.1 |
| R2 | R3 | 3.3.3.3 |
| R3 | R2 | 2.2.2.2 |

All expected adjacencies reached the `FULL` state during verification.

### Observations

- R1 successfully established an adjacency with R2.
- R2 successfully established adjacencies with both R1 and R3.
- R3 successfully established an adjacency with R2.
- No direct OSPF adjacency was expected between R1 and R3 because they are not directly connected.

The `FULL` state confirms that the neighboring routers completed adjacency formation and synchronized their link-state databases.

### Conclusion

The observed neighbor relationships matched the designed linear topology.

R2 successfully operated as the central OSPF transit router.

---

## 5. Routing Table Analysis

The `show ip route ospf` command was executed on all three routers to inspect dynamically learned OSPF routes.

### 5.1 R1 — Routing Information

Observed OSPF routes:

| Destination Network | Next Hop | OSPF Metric |
|---|---|---:|
| 10.0.0.4/30 | 10.0.0.2 | 2 |
| 192.168.30.0/24 | 10.0.0.2 | 3 |

R1 learned the R2–R3 transit network and the remote Branch Office LAN through R2.

The Branch Office LAN is reachable through the next-hop address `10.0.0.2`.

### 5.2 R2 — Routing Information

Observed OSPF routes:

| Destination Network | Next Hop | OSPF Metric |
|---|---|---:|
| 192.168.10.0/24 | 10.0.0.1 | 2 |
| 192.168.30.0/24 | 10.0.0.6 | 2 |

R2 learned both user LAN networks through their respective edge routers.

This confirms that the intermediate router has routing information for both remote LANs.

### 5.3 R3 — Routing Information

Observed OSPF routes:

| Destination Network | Next Hop | OSPF Metric |
|---|---|---:|
| 10.0.0.0/30 | 10.0.0.5 | 2 |
| 192.168.10.0/24 | 10.0.0.5 | 3 |

R3 learned the R1–R2 transit network and the remote Head Office LAN through R2.

### 5.4 Routing Analysis Summary

| Router | Remote Networks Learned | Verification |
|---|---:|---|
| R1 | 2 | Successful |
| R2 | 2 | Successful |
| R3 | 2 | Successful |

All expected remote networks appeared in the routing tables with the OSPF route code `O`.

### Technical Interpretation

The routing information confirms that OSPF successfully distributed network reachability throughout Area 0.

The route metrics represent the accumulated OSPF path costs. They are not manually configured static route values.

The observed metrics are consistent with the linear topology and the interface costs inspected during the laboratory.

---

## 6. OSPF Interface Cost Observations

The command `show ip ospf interface` was used to inspect the transit interfaces participating in OSPF.

The following values were observed:

| Router | Interface | OSPF Cost | Network Type |
|---|---|---:|---|
| R1 | GigabitEthernet0/1 | 1 | BROADCAST |
| R2 | GigabitEthernet0/0 | 1 | BROADCAST |
| R3 | GigabitEthernet0/1 | 1 | BROADCAST |

### Observations

- Each inspected transit interface reported an OSPF cost of 1.
- The inspected interfaces reported the OSPF network type `BROADCAST`.
- OSPF uses interface costs to calculate the total path metric.
- The accumulated metric increases as the path crosses additional OSPF-enabled interfaces.

### Technical Interpretation

OSPF selects routes according to their total path cost.

A lower total cost is preferred when multiple paths to the same destination are available.

This laboratory uses a linear topology with only one path between the two user LANs. Therefore, it demonstrates interface-cost inspection and metric accumulation, but does not demonstrate a comparison between competing paths.

No explicit interface-cost modification was performed as part of the recorded experiment.

---

## 7. Passive Interface Observations

The LAN-facing interfaces were configured as passive on R1 and R3.

| Router | Passive Interface | Advertised Network |
|---|---|---|
| R1 | GigabitEthernet0/0 | 192.168.10.0/24 |
| R3 | GigabitEthernet0/0 | 192.168.30.0/24 |

### Technical Interpretation

A passive OSPF interface allows the associated network to be advertised while preventing OSPF Hello packets and neighbor formation on that interface.

This is appropriate for user-facing LAN interfaces where end devices do not participate in OSPF.

The transit interfaces remained active to establish adjacencies between routers.

---

## 8. End-to-End Connectivity Observations

Bidirectional ICMP tests were performed between PC1 and PC2.

### 8.1 PC1 to PC2

Source: `192.168.10.10`

Destination: `192.168.30.10`

The initial ping attempt produced:

| Parameter | Result |
|---|---:|
| Packets Sent | 4 |
| Packets Received | 3 |
| Packets Lost | 1 |
| Packet Loss | 25% |

A second ping test was performed immediately afterward.

Observed result:

| Parameter | Result |
|---|---:|
| Packets Sent | 4 |
| Packets Received | 4 |
| Packets Lost | 0 |
| Packet Loss | 0% |
| Average Round-Trip Time | 0 ms |

The repeated test confirmed successful communication from PC1 to PC2.

### 8.2 PC2 to PC1

Source: `192.168.30.10`

Destination: `192.168.10.10`

Observed result:

| Parameter | Result |
|---|---:|
| Packets Sent | 4 |
| Packets Received | 4 |
| Packets Lost | 0 |
| Packet Loss | 0% |
| Average Round-Trip Time | 2 ms |

Communication from PC2 to PC1 was successful.

### 8.3 Connectivity Summary

| Test | Packet Loss | Result |
|---|---:|---|
| PC1 → PC2 | 0% on repeated test | PASS |
| PC2 → PC1 | 0% | PASS |

### Technical Interpretation

Both end devices successfully exchanged ICMP packets across the routed network.

The results confirm:

- Correct end-device IPv4 addressing.
- Correct default gateway configuration.
- Successful OSPF route advertisement.
- Availability of forward and return routing paths.
- End-to-end reachability between the two LANs.

The initial timeout during the first PC1-to-PC2 test may have been associated with initial ARP resolution or address learning. The exact cause was not independently verified. The successful repeated test confirmed normal connectivity.

---

## 9. Overall Verification Summary

| Verification Area | Expected Result | Observed Result | Status |
|---|---|---|---|
| Router IPv4 addressing | Correct interface addressing | Verified | PASS |
| OSPF Router IDs | Unique Router IDs | Verified | PASS |
| R1–R2 adjacency | FULL | FULL | PASS |
| R2–R3 adjacency | FULL | FULL | PASS |
| R1 remote routes | OSPF routes installed | Verified | PASS |
| R2 remote routes | OSPF routes installed | Verified | PASS |
| R3 remote routes | OSPF routes installed | Verified | PASS |
| OSPF interface costs | Inspect interface metrics | Cost 1 observed | PASS |
| PC1 to PC2 | Successful communication | 0% loss on repeated test | PASS |
| PC2 to PC1 | Successful communication | 0% loss | PASS |

---

## 10. Technical Lessons and Conclusions

The implementation provided practical experience with OSPFv2 configuration and verification in a small enterprise network.

The main technical observations were:

1. **Router Identification:** Manually assigning unique Router IDs provides predictable identification of OSPF routers.

2. **Neighbor Formation:** OSPF routers must establish neighbor adjacencies before exchanging link-state information.

3. **Area Design:** Area 0 provides the shared OSPF backbone for all participating routers in this topology.

4. **Dynamic Routing:** OSPF automatically distributes remote network reachability, removing the need to configure individual static routes between the two LANs.

5. **Passive Interfaces:** Passive interfaces allow user LANs to be advertised without attempting to establish OSPF adjacencies with end devices.

6. **Metric Analysis:** Interface costs contribute to the total OSPF route metric and influence path selection.

7. **Routing Verification:** The `show ip route ospf` command provides a focused view of dynamically learned OSPF routes.

8. **End-to-End Testing:** Bidirectional ICMP testing confirms that routing information is usable for actual communication between remote LANs.

### Final Conclusion

The OSPF Single-Area laboratory was successfully implemented and verified.

The three routers established the expected OSPF adjacencies, learned the required remote networks, and maintained the routing information necessary for communication between the Head Office and Branch Office.

Both end-to-end connectivity tests completed successfully with zero packet loss on the final tests.

The project demonstrates a practical understanding of dynamic routing, OSPF operation, route verification, interface metrics, and basic network troubleshooting.

---

## 11. Evidence References

The following screenshots provide supporting evidence for the observations documented above.

| Evidence | File |
|---|---|
| Network topology | `../screenshots/network-topology.png` |
| R2 OSPF neighbors | `../screenshots/ospf-neighbors-r2.png` |
| R3 OSPF neighbors | `../screenshots/ospf-neighbors-r3.png` |
| R1 OSPF routing table | `../screenshots/ospf-routing-table-r1.png` |
| R2 OSPF routing table | `../screenshots/ospf-routing-table-r2.png` |
| R3 OSPF routing table | `../screenshots/ospf-routing-table-r3.png` |
| R1 final OSPF routes | `../screenshots/ospf-final-routes-r1.png` |
| R2 final OSPF routes | `../screenshots/ospf-final-routes-r2.png` |
| R3 final OSPF routes | `../screenshots/ospf-final-routes-r3.png` |
| R1 OSPF cost | `../screenshots/ospf-cost-analysis-r1.png` |
| R2 OSPF cost | `../screenshots/ospf-cost-analysis-r2.png` |
| R3 OSPF cost | `../screenshots/ospf-cost-analysis-r3.png` |
| PC1 to PC2 connectivity | `../screenshots/connectivity-ping-pc1-to-pc2.png` |
| PC2 to PC1 connectivity | `../screenshots/connectivity-ping-pc2-to-pc1.png` |

---

**Laboratory:** 06 — OSPF Single-Area  
**Platform:** Cisco Packet Tracer 8.2.2  
**Routing Protocol:** OSPFv2  
**OSPF Process ID:** 1  
**OSPF Area:** 0  
**Documentation:** Laboratory observations and technical analysis
