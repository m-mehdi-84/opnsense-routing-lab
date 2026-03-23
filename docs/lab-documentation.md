# Lab Documentation – OPNsense Routing Lab

## Overview

This document provides the **technical implementation details** of the OPNsense Routing Lab.

While the README presents a high-level overview, this document focuses on:

- routing configuration  
- protocol behavior  
- troubleshooting scenarios  
- validation and analysis  

---

## Lab Objective

The objective of this lab was to explore how routing works in a segmented network environment.

Key goals:

- configure static routing between subnets  
- analyze route selection using metrics  
- implement dynamic routing using OSPF (FRR)  
- understand routing behavior in OPNsense  
- troubleshoot routing conflicts and connectivity issues  

---

## Environment Setup

### Platform

- Microsoft Hyper-V  
- OPNsense firewall (router)  

### Networks

- LAN → 192.168.10.0/24  
- LAN2 → 192.168.20.0/24  

### Systems

- Ubuntu (LAN)  
- Windows 11 (LAN2)  

---

## Network Context

Both networks are directly connected to OPNsense:

- LAN → interface 192.168.10.1  
- LAN2 → interface 192.168.20.1  

This setup allows testing of routing behavior within a single router environment.

---

## Static Routing

### Configuration

A static route was manually configured in OPNsense.

- Destination: 192.168.20.0/24  
- Gateway: 192.168.20.1  

### Purpose

- simulate routing behavior  
- understand how manual routes are applied  

### Result

- communication between LAN and LAN2 successful  

### Observation

Static routes are not required in directly connected networks, but were configured to demonstrate routing behavior.

---

## Routing Metrics

### Configuration

Two routes were configured with different metric values:

- primary route → metric 0  
- secondary route → metric 10  

### Testing Procedure

- removed primary route  
- tested connectivity again  

### Result

- traffic automatically used secondary route  
- confirmed that lower metric is preferred  
- demonstrated how routers prioritize paths based on cost  

---

## Dynamic Routing – OSPF (FRR)

### Installation

FRR plugin installed in OPNsense.

### Configuration Steps

- enabled FRR service  
- enabled OSPF  
- added LAN interface  
- added LAN2 interface  
- defined OSPF networks  

---

### Observation

- OSPF configured successfully  
- no route exchange occurred  

### Explanation

- only one router exists in the lab  
- OSPF requires multiple routers to exchange routes  
- therefore, no dynamic routing behavior was observed  

---

## Connectivity Testing

### Commands

```
ping 192.168.10.1
ping 192.168.20.1
ping <target-host>
```

### Result

- successful communication between subnets  
- routing verified through OPNsense  

---

## Routing Table Verification

Routing behavior was validated by inspecting routing tables.

### On OPNsense (Shell)

```
netstat -rn
```

### On Linux (Ubuntu)

```
ip route
```

### On Windows

```
route print
```

### Purpose

- verify active routes  
- confirm gateway selection  
- analyze path changes during testing  

---

## Troubleshooting & Issues Encountered

### 1. Firewall Blocking Traffic

#### Issue

- communication between LAN and LAN2 failed  

#### Cause

- missing allow rule on LAN2 interface  

#### Resolution

- added allow rule on LAN2 interface  

#### Result

- traffic allowed between networks  

---

### 2. Windows ICMP Blocking

#### Issue

- ping from Ubuntu to Windows failed  

#### Cause

- Windows Firewall blocks ICMP  

#### Resolution (PowerShell)

```
Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"
```

#### Result

- ICMP allowed  
- connectivity restored  

---

### 3. FRR Not Visible in GUI

#### Issue

- FRR plugin not visible under Services  

#### Cause

- newer OPNsense versions place FRR under Routing menu  

#### Resolution

- accessed FRR via:
  - Routing → General  
  - Routing → OSPF  

---

### 4. Routing Loop (TTL Exceeded)

#### Issue

```
TTL exceeded
```

#### Cause

- conflict between static routes, custom gateway and OSPF  

#### Resolution

- removed static routes  
- removed custom gateway  
- disabled OSPF  
- rebooted OPNsense  

#### Result

- routing table reset  
- normal connectivity restored  

---

## Technical Observations

- static routing is unnecessary for directly connected networks  
- routing metrics determine path preference  
- OSPF requires multiple routers to exchange routes  
- firewall rules directly impact routing behavior  
- routing misconfiguration can cause loops  
- system reboot may be required to clear routing state  
- routing tables are essential for validation and troubleshooting  

---

## Conclusion

This lab demonstrates how routing behaves in a segmented network environment using OPNsense.

It highlights:

- differences between static and dynamic routing  
- how routing decisions are made  
- how misconfigurations affect connectivity  
- how to troubleshoot routing issues effectively  

The lab provides practical insight into routing concepts used in real-world network environments.

---
