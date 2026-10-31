# MikroTik ISP-Style Access Network (On Going)

**PPPoE Server | NAT | Per-Subscriber Bandwidth Management | Multi-WAN Load Balancing | Automatic Failover**

## Overview

Designed and simulated an ISP-style access network using MikroTik RouterOS v7 and GNS3. Project demonstrates core ISP infrastructure, including PPPoE subscriber authentication, centralized bandwidth management, NAT, PCC-based multi-WAN load balancing, and automatic gateway failover.

Built modular network architecture separating ISP Core Router and PPPoE Access Concentrator to simulate real-world ISP operations.

## Network Architecture

```text
                 INTERNET SIMULATION
                         |
             +-----------+-----------+
             |           |           |
           ISP-A       ISP-B       ISP-C
             |           |           |
             +-----------+-----------+
                         |
                  CORE ROUTER
                   (CORE-R1)
                         |
                  ACCESS NETWORK
                         |
                 PPPoE CONCENTRATOR
                   (ACCESS-R1)
                         |
                  SUBSCRIBER LAN
                         |
             +-----------+-----------+
             |           |           |
          CLIENT-01   CLIENT-02   CLIENT-03
           BASIC      STANDARD     PREMIUM
```

## Technologies & Tools

- **MikroTik RouterOS v7** – Routing, PPPoE, NAT, firewall and bandwidth management.
- **MikroTik CHR** – Virtual router infrastructure.
- **GNS3** – Network topology design and simulation.
- **WinBox** – Router configuration and administration.
- **PCC (Per Connection Classifier)** – Multi-WAN load balancing.
- **PCQ (Per Connection Queue)** – Fair bandwidth distribution.
- **RADIUS** – Centralized subscriber authentication architecture.
- **SNMP / Zabbix** – Network monitoring architecture.

## Key Features

### 1. PPPoE Subscriber Management
- Configured MikroTik PPPoE Access Concentrator.
- Implemented individual subscriber authentication using username and password.
- Created dynamic IP address pools and PPP profiles.
- Supported multiple subscriber service packages.
- Managed active sessions and subscriber account status.

### 2. Multi-WAN Load Balancing
- Integrated three simulated upstream ISP gateways.
- Implemented PCC-based connection distribution.
- Distributed new subscriber connections across available WAN links.
- Used connection marking and policy-based routing to maintain connection symmetry.

### 3. Automatic Gateway Failover
- Configured primary and backup routes for each WAN routing table.
- Implemented gateway reachability monitoring.
- Tested automatic traffic redirection during upstream gateway failures.
- Validated route recovery after gateway restoration.

### 4. NAT & Routing
- Configured source NAT using masquerade.
- Implemented inter-router routing between Core and Access routers.
- Established subscriber connectivity through multiple upstream gateways.

### 5. Bandwidth Management
- Created BASIC, STANDARD and PREMIUM subscriber packages.
- Applied individual upload/download limits through PPP profiles.
- Implemented dynamic Simple Queues.
- Explored PCQ-based bandwidth distribution.

### 6. Network Security
- Configured firewall input and forward chains.
- Restricted administrative access to management network.
- Disabled unnecessary RouterOS services.
- Implemented internal network traffic exclusions from PCC classification.

### 7. Network Monitoring
- Monitored PPPoE sessions and subscriber traffic.
- Inspected WAN utilization and connection tracking.
- Configured RouterOS logging and SNMP monitoring foundations.
- Used CLI tools for troubleshooting and performance validation.

## IP Addressing Plan

| Network | Address |
|---|---|
| ISP-A WAN | 172.16.1.0/24 |
| ISP-B WAN | 172.16.2.0/24 |
| ISP-C WAN | 172.16.3.0/24 |
| Core-to-Access | 10.10.10.0/24 |
| PPPoE Subscribers | 10.20.0.0/24 |
| Management | 192.168.100.0/24 |

## Subscriber Packages

| Package | Upload | Download |
|---|---:|---:|
| BASIC | 2 Mbps | 5 Mbps |
| STANDARD | 5 Mbps | 10 Mbps |
| PREMIUM | 10 Mbps | 25 Mbps |

## Repository Structure

```text
mikrotik-isp-access-network/
│
├── README.md
│
├── topology/
│   ├── network-topology.png
│   ├── ip-addressing-plan.md
│   └── interface-mapping.md
│
├── configurations/
│   ├── core-router.rsc
│   ├── access-router.rsc
│   ├── isp-a.rsc
│   ├── isp-b.rsc
│   └── isp-c.rsc
│
├── pppoe/
│   ├── subscriber-profiles.rsc
│   ├── subscriber-accounts.rsc
│   └── authentication.md
│
├── routing/
│   ├── pcc-load-balancing.rsc
│   ├── failover.rsc
│   └── routing-explanation.md
│
├── firewall/
│   ├── nat.rsc
│   └── firewall-rules.rsc
│
├── qos/
│   ├── bandwidth-management.rsc
│   └── pcq.rsc
│
├── testing/
│   ├── test-cases.md
│   ├── failover-results.md
│   └── bandwidth-results.md
│
└── screenshots/
    ├── network-topology.png
    ├── pppoe-sessions.png
    ├── pcc-distribution.png
    └── failover-testing.png
```

## Testing & Validation

Performed or planned validation scenarios:

- PPPoE authentication with valid and invalid credentials.
- Dynamic subscriber IP assignment.
- Individual upload/download bandwidth enforcement.
- NAT connectivity through upstream gateways.
- PCC connection distribution across three WAN links.
- Individual WAN gateway failure and recovery.
- Firewall access restrictions.
- Subscriber session and traffic monitoring.

## Deployment Notes

1. Install MikroTik CHR on GNS3 or another supported virtualization platform.
2. Create virtual routers and connect interfaces according to topology.
3. Configure ISP gateways and IP addressing.
4. Configure Core and Access routers.
5. Import RouterOS configuration scripts.
6. Establish PPPoE subscriber sessions.
7. Configure NAT, PCC, routing and failover.
8. Execute connectivity, bandwidth and failure tests.

**Important:** This project uses simulated upstream gateways. Production deployment requires independent upstream connectivity, end-to-end WAN health monitoring, secure management, and validated routing policies.

## Learning Outcomes

- ISP network architecture and subscriber access design.
- MikroTik RouterOS v7 configuration and administration.
- PPPoE authentication and subscriber management.
- Policy-based routing and PCC load balancing.
- Multi-WAN failover and redundancy.
- NAT, firewall and network security.
- QoS and per-subscriber bandwidth enforcement.
- Network monitoring and troubleshooting.

## References

- [MikroTik Official Documentation](https://manual.mikrotik.com/docs/)
- [PPPoE Configuration](https://help.mikrotik.com/docs/spaces/ROS/pages/2031625/PPPoE)
- [Load Balancing](https://help.mikrotik.com/docs/spaces/ROS/pages/4390920/Load+Balancing)
- [Firewall Mangle](https://help.mikrotik.com/docs/spaces/ROS/pages/48660587/Mangle)
- [NAT](https://help.mikrotik.com/docs/spaces/ROS/pages/3211299/NAT)

---

**Project Type:** Network Engineering / ISP Infrastructure Simulation  
**Platform:** GNS3 + MikroTik CHR  
**RouterOS:** Version 7  
**Status:** Lab implementation and validation
