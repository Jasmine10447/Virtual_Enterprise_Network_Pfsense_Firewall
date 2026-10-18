<h1 align=center>🌐 Virtual Firewall Deployment & Policy Configuration </h1>

<p align="center">
  <strong>A Virtualized Enterprise Network Security Project Using pfSense and Oracle VirtualBox</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Virtualization-Oracle%20VirtualBox-183A61" alt="Oracle VirtualBox">
  <img src="https://img.shields.io/badge/Firewall-pfSense%20CE-212121" alt="pfSense CE">
  <img src="https://img.shields.io/badge/Networking-Implementation-F59E0B" alt="Networking Implementation">
  <img src="https://img.shields.io/badge/Virtual%20Machines-Deployment-6366F1" alt="Virtual Machines">
  <img src="https://img.shields.io/badge/WAN%2FLAN-Segmentation-0EA5E9" alt="WAN LAN Segmentation">
  <img src="https://img.shields.io/badge/IPv4-Addressing-8B5CF6" alt="IPv4 Addressing">
  <img src="https://img.shields.io/badge/Subnetting-Network%20Design-14B8A6" alt="Subnetting">
  <img src="https://img.shields.io/badge/NAT-Internet%20Connectivity-10B981" alt="NAT">
  <img src="https://img.shields.io/badge/Firewall-Rules-EF4444" alt="Firewall Rules">
  <img src="https://img.shields.io/badge/IP-Aliases-EC4899" alt="IP Aliases">
  <img src="https://img.shields.io/badge/DNS-Resolution-3B82F6" alt="DNS Resolution">
  <img src="https://img.shields.io/badge/Ubuntu-Desktop-E95420" alt="Ubuntu Desktop">
  <img src="https://img.shields.io/badge/Lubuntu-24.04%20LTS-0068C8" alt="Lubuntu 24.04 LTS">
  <img src="https://img.shields.io/badge/Static-IP%20Configuration-7C3AED" alt="Static IP Configuration">
  <img src="https://img.shields.io/badge/Client--Specific-Access%20Control-DC2626" alt="Client-Specific Access Control">
  <img src="https://img.shields.io/badge/Network-Troubleshooting-F97316" alt="Network Troubleshooting">
  <img src="https://img.shields.io/badge/Connectivity-Testing-059669" alt="Connectivity Testing">
</p>


---

## 📌 Project Overview

This project demonstrates the design, deployment, configuration, and testing of a virtualized enterprise network environment using **Oracle VirtualBox and pfSense CE**.

The network uses pfSense as the centralized firewall and router, connecting two Linux-based client machines to an external internet connection provided through a mobile hotspot.

The internal network is isolated using a VirtualBox Internal Network named `LAN NET`. Both client machines communicate with external networks through the pfSense firewall, enabling centralized traffic routing, Network Address Translation (NAT), and client-specific firewall policy enforcement.

The project also demonstrates how different internet access restrictions can be applied to individual workstations using pfSense firewall rules and IP aliases.

### 🎯 Key Implementation Results

- Deployed pfSense CE as the centralized firewall and gateway.
- Configured separate WAN and LAN network interfaces.
- Connected Ubuntu and Lubuntu client machines to an isolated internal network.
- Established internet connectivity through pfSense and NAT.
- Implemented client-specific service restrictions using firewall rules and IP aliases.
- Tested connectivity and access policies across both client machines.
- Troubleshot virtual machine, network configuration, and DNS filtering issues.

---

## 🌐 Network Architecture

### 🖧 Network Topology

The network follows a centralized firewall architecture in which pfSense manages communication between the internal LAN and the external internet connection.

The WAN interface connects to the mobile hotspot through a VirtualBox Bridged Adapter, while the LAN interface connects to the internal network shared by both client machines.

**Network flow:** : `Mobile Hotspot → pfSense WAN → pfSense Firewall/NAT → pfSense LAN → Ubuntu PC1 & Lubuntu PC2`

The internal clients use pfSense as their default gateway, ensuring that their external traffic passes through the firewall.

![Virtual Enterprise Design Blueprint](Virtual%20Enterprise%20Design/Design%20Blueprint.png)

---

## 🗺️ Network Addressing Plan

The internal LAN uses the private IPv4 subnet `192.168.1.0/24`. Static IP addresses were assigned to both client machines to support consistent identification and client-specific firewall rules.

| Device | Interface | IP Address | Role |
|---|---|---|---|
| pfSense WAN | `em0` | `10.22.154.3/24` | External connectivity |
| pfSense LAN | `em1` | `192.168.1.1/24` | Default gateway |
| PC1 – Ubuntu | `enp0s3` | `192.168.1.20/24` | Client workstation 1 |
| PC2 – Lubuntu | `enp0s3` | `192.168.1.40/24` | Client workstation 2 |

**Default gateway for both clients:** `192.168.1.1`

**Internal network:** `LAN NET`

> The WAN address shown above is the address recorded during the implementation. As it is assigned by the mobile hotspot through DHCP, it may change in another environment.

---

## 🔧 Technologies & Networking Concepts

| Infrastructure & Tools | Networking & Security |
|---|---|
| 🖥️ Oracle VirtualBox | 🌐 IPv4 Addressing |
| 🛡️ pfSense CE | 🔀 WAN/LAN Segmentation |
| 🐧 Ubuntu Desktop | 🔄 Network Address Translation (NAT) |
| 🐧 Lubuntu 24.04 LTS | 📋 Firewall Rule Configuration |
| 📡 Mobile Hotspot | 🎯 Client-Specific Access Control |
| 🖧 Virtual Internal Networks | 🧪 Connectivity Verification |
| ⚙️ Linux Network Manager | 🔍 Troubleshooting & Diagnostics |
| 🗂️ pfSense IP Aliases | 🔐 Network Traffic Filtering |

---

## 🎯 Project Objectives

The primary objectives of this project were to:

- Deploy a virtual firewall environment using Oracle VirtualBox.
- Install and configure pfSense as the central router and firewall.
- Create an isolated internal network for client workstations.
- Configure WAN and LAN interfaces with appropriate IP addressing.
- Connect two Linux client systems to the internal LAN.
- Establish internet access through pfSense using NAT.
- Apply different firewall policies to individual client machines.
- Block YouTube access for Ubuntu PC1 while retaining WhatsApp access.
- Block WhatsApp access for Lubuntu PC2 while retaining YouTube access.
- Verify connectivity and troubleshoot configuration issues.

---

## 🛡️ Firewall Policy Configuration

A key feature of this project is the implementation of different internet access policies for the two client machines.

The final configuration used pfSense firewall rules and destination IP aliases to apply restrictions based on each client's source IP address.

### 🔒 Client-Specific Access Policies

| Client | IP Address | Restricted Service | Expected Policy |
|---|---|---|---|
| PC1 – Ubuntu | `192.168.1.20` | YouTube | Block |
| PC1 – Ubuntu | `192.168.1.20` | WhatsApp | Allow |
| PC2 – Lubuntu | `192.168.1.40` | WhatsApp | Block |
| PC2 – Lubuntu | `192.168.1.40` | YouTube | Allow |

The firewall rules were designed to restrict the selected services without applying the same policy to both clients.

### 📋 IP Alias Management

Two pfSense firewall aliases were created to group destination networks associated with the selected services.

| Alias | Purpose |
|---|---|
| `YouTube_IPs` | Groups selected Google and YouTube-related IP ranges |
| `WhatsApp_IPs` | Groups selected Meta and WhatsApp-related IP ranges |

Using aliases simplifies firewall rule management by allowing multiple destination networks to be referenced through a single configuration object.

> **Implementation note:** The aliases contain selected IP ranges, not a guaranteed complete list of all service infrastructure. Large services use changing and shared IP addresses, so the results may vary over time. The project demonstrates IP-based filtering rather than comprehensive application-layer identification.

---

## 🔄 Network Connectivity & NAT

Both client machines use the pfSense LAN interface as their default gateway.

The pfSense firewall provides outbound connectivity by translating private LAN traffic to the WAN address using Network Address Translation.

### Connectivity Path

1. Ubuntu or Lubuntu generates outbound network traffic.
2. Traffic is sent to the default gateway at `192.168.1.1`.
3. pfSense applies the configured firewall policies.
4. Permitted traffic is routed through the WAN interface.
5. NAT allows the internal client to communicate with external networks through the mobile hotspot connection.

This configuration simulates a basic enterprise network in which workstations share a centrally managed internet gateway.

---

## 🧪 Implementation & Testing

The project was completed through four main implementation tasks.

### Task 01 — Virtual Environment Setup

- Installed Oracle VirtualBox.
- Deployed pfSense CE.
- Installed Ubuntu Desktop as PC1.
- Installed Lubuntu 24.04 LTS as PC2.
- Completed the initial pfSense web-based configuration.

### Task 02 — Virtual Network Configuration

- Configured the pfSense WAN adapter using Bridged Adapter mode.
- Configured the pfSense LAN adapter using the `LAN NET` Internal Network.
- Connected both client machines to the same internal network.
- Assigned static IP addresses to the clients.
- Verified interface assignments and client network settings.

### Task 03 — Internet Connectivity

- Verified the pfSense WAN connection.
- Configured both clients to use `192.168.1.1` as the default gateway.
- Tested external network connectivity.
- Verified DNS resolution.
- Confirmed internet connectivity on both Ubuntu and Lubuntu.

### Task 04 — Client-Specific Service Blocking

- Removed previous global DNS Resolver filtering configurations.
- Created the `YouTube_IPs` and `WhatsApp_IPs` aliases.
- Configured firewall rules for each client.
- Applied the firewall changes.
- Flushed DNS caches on both clients.
- Tested restricted and permitted service access.

### 📊 Expected Verification Results

| Test | PC1 – Ubuntu | PC2 – Lubuntu |
|---|---|---|
| Internet connectivity | Successful | Successful |
| YouTube access | Blocked | Allowed |
| WhatsApp access | Allowed | Blocked |

These are the intended and reported test outcomes of the implementation. Actual results can vary if service IP addresses change or traffic uses an unfiltered endpoint.

---

## 🔍 Challenges & Troubleshooting

Several practical challenges were encountered during the implementation.

| Challenge | Resolution |
|---|---|
| High resource consumption from Linux Mint Cinnamon | Replaced it with Lubuntu 24.04 LTS |
| Linux Mint MATE installer becoming unresponsive | Tested alternative settings and selected Lubuntu |
| Incorrect client network adapter configuration | Connected both clients to `LAN NET` |
| Outdated DHCP address on Lubuntu | Configured the intended static IP address |
| Multiple IP addresses on the Lubuntu interface | Removed the outdated address and restored the intended configuration |
| DNS Resolver rules affecting both clients | Removed global DNS filtering and implemented client-specific firewall rules |
| Inconsistent results with a hybrid DNS/firewall approach | Rebuilt the filtering configuration using firewall rules and aliases |

These troubleshooting activities provided practical experience in virtual machine resource management, IP addressing, interface configuration, and firewall policy design.

---

## 📁 Repository Structure

The following is a suggested structure for publishing the project documentation and supporting materials.

```text
Virtual-Firewall-Deployment/
│
├── README.md
│
├── Network-Design/
│   └── Logical-Network-Topology.png
│
├── Screenshots/
│   ├── pfSense-Dashboard.png
│   ├── Network-Adapter-Configuration.png
│   ├── IP-Address-Verification.png
│   ├── Firewall-Aliases.png
│   ├── Firewall-Rules.png
│   └── Connectivity-Tests.png
│
├── Documentation/
│   └── Virtual-Firewall-Deployment-Report.pdf
│
└── LICENSE
```
---

## 📚 Skills Demonstrated

- Virtual machine deployment and resource allocation.
- pfSense firewall installation and administration.
- WAN/LAN network segmentation.
- IPv4 subnetting and static addressing.
- NAT-based internet connectivity.
- Firewall rule configuration and access control.
- IP alias management.
- DNS configuration and troubleshooting.
- Linux network configuration.
- Connectivity testing and problem-solving.
- Technical documentation and network design.

---

## 🚀 Project Scope & Future Improvements

The implementation provides a foundation for further exploration of virtualized network security.

Possible future improvements include:

- Introducing separate VLANs or additional internal network segments.
- Implementing DHCP reservations and centralized address management.
- Exploring domain-based filtering and more comprehensive application controls.
- Configuring firewall logging and traffic monitoring.
- Testing DNS-over-HTTPS and other filtering bypass scenarios.
- Expanding the environment with additional clients and security policies.

These are potential extensions, not features claimed as part of the completed implementation.

---

## 🔒 Copyright & Usage Policy

### © 2026 Yesmin Jalaldeen. All Rights Reserved.

This repository documents an educational project involving virtual firewall deployment, enterprise-style network configuration, and client-specific access control.

The author's original project documentation, network diagrams, screenshots, and project-specific materials are protected by the author's stated usage policy, subject to applicable third-party and institutional rights.

**No permission is granted to reproduce, modify, redistribute, republish, or submit the author's original project materials as another person's work without prior written permission.**

This notice applies to original project materials, including:

- Network diagrams and topology designs.
- Original screenshots and documentation.
- Project-specific firewall configurations.
- Original implementation notes and reports.

Public repository access does not, by itself, grant permission to reuse the author's original materials. Third-party software and tools remain subject to their respective licenses and terms.

### 📩 Permission Requests

Requests to reuse or redistribute protected original materials should be directed to the author for written permission.

---

<div align="center">

### ✍️ Yesmin Jalaldeen

*Virtual Firewall Deployment & Policy Configuration*

**BIT (Hons) Specialized in Computer Networks**  
**BCS HEQ PGD in Computer Networks**

*“Building Practical Network Security Through Virtualization.”*

**© 2026 Yesmin Jalaldeen — All Rights Reserved.**

</div>
