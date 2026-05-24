# OPNsense Routing Lab

A hands-on **networking lab** built using **Microsoft Hyper-V** and **OPNsense firewall** to explore routing concepts in a segmented network environment.

This project focuses on **static routing, routing metrics, FRR (Free Range Routing) and OSPF**, including real-world troubleshooting of routing issues and connectivity problems.

The lab is designed as a **follow-up project** to a foundational network lab, with emphasis on routing behavior and traffic flow analysis.

---

## Lab Overview

This lab extends a segmented network environment to analyze how routing decisions are made and how traffic flows between networks.

Key focus areas:

- Static routing configuration
- Route selection using metrics
- Dynamic routing with OSPF (FRR)
- Troubleshooting routing conflicts
- Connectivity validation between subnets

---

## Network Topology

```
                         INTERNET
                             |
                            WAN
                             |
                    +------------------+
                    |     OPNsense     |
                    |  Firewall/Router |
                    +--------+---------+
                             |
               -----------------------------
               |                           |
      +------------------+       +------------------+
      |       LAN        |       |       LAN2       |
      | 192.168.10.0/24 |       | 192.168.20.0/24 |
      +--------+---------+       +--------+---------+
               |                           |
            Ubuntu                     Windows 11
         (Routing Node)             (Client LAN2)
```

---

## Network Configuration

| Network | Subnet            | Gateway        |
|--------|------------------|---------------|
| LAN    | 192.168.10.0/24  | 192.168.10.1  |
| LAN2   | 192.168.20.0/24  | 192.168.20.1  |

---

## Routing Scenarios

### Static Routing Analysis

- reviewed static route configuration in OPNsense
- analyzed why additional static routes are unnecessary for directly connected networks
- identified how incorrect route configuration can create routing conflicts and loops

---

### Routing Metrics Analysis

- configured route metric values to study path preference
- analyzed how lower metric values influence route selection
- observed how incorrect or conflicting route configuration can affect connectivity

---

### OSPF Configuration Study

- installed the FRR plugin in OPNsense
- enabled and configured OSPF for LAN and LAN2
- confirmed that no route exchange occurred because the lab contained only one router
- documented that multiple routers are required to validate real OSPF neighbor relationships and dynamic route exchange

---

## Troubleshooting

This lab includes real-world troubleshooting scenarios:

- connectivity failures between LAN and LAN2  
- firewall rules blocking traffic  
- Windows ICMP blocking  
- routing conflicts and misconfigurations  
- TTL exceeded errors caused by routing loops  

---

## Validation

### Connectivity Testing

```
ping 192.168.10.1
ping 192.168.20.1
ping <target-host>
```

### Routing Verification

- verified traffic flow between subnets  
- analyzed routing table behavior  
- confirmed route selection based on metrics  

---

## Key Learning Outcomes

- understanding static vs dynamic routing  
- configuring and analyzing routing metrics  
- working with FRR and OSPF in OPNsense  
- troubleshooting routing and connectivity issues  
- understanding traffic flow between segmented networks  
- identifying and resolving routing loops  

---

## Documentation

Detailed step-by-step guide is available in:

[Lab Documentation](docs/lab-documentation.md)

---

## Conclusion

This project builds on foundational networking knowledge and introduces advanced routing concepts.

It demonstrates how routing decisions are made, how protocols behave and how misconfigurations can impact network connectivity.

---

## Author

**Muhammad Mehdi**  
IT Security Developer Student  
 
---
