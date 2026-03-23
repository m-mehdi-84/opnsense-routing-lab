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

### Static Routing

- configured static routes between LAN and LAN2  
- tested communication across segmented networks  
- analyzed routing behavior in directly connected networks  

---

### Routing Metrics

- configured multiple routes with different metrics  
- observed route preference based on metric values  
- tested failover by removing primary route  

---

### Dynamic Routing (OSPF)

- installed FRR plugin in OPNsense  
- enabled OSPF  
- configured LAN and LAN2 interfaces  
- defined OSPF networks  

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

## Project Structure

```
opnsense-routing-lab/
│
├── README.md
├── docs/
│   └── lab-documentation.md
└── images/
```

---

## Conclusion

This project builds on foundational networking knowledge and introduces advanced routing concepts.

It demonstrates how routing decisions are made, how protocols behave and how misconfigurations can impact network connectivity.

---

## Author

**Muhammad Mehdi**  
IT Security Developer Student  
 
---
