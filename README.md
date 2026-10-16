CMPG325 Computer Networks Project

Botshelo Safari Adventures — Network Design and Implementation

Project ID: CMPG325-2026-058  
Client ID: CLI-058  
Client: Botshelo Safari Adventures  
Location: Rustenburg, South Africa  
Industry: Tourism  
Simulation Software: Cisco Packet Tracer  
Assigned IPv4 Address Block: 172.30.34.0/23

1. Project Overview

This project involves designing, implementing and testing a computer network for Botshelo Safari Adventures. The network is designed to provide structured connectivity between business departments, servers, management workstations and guest devices.

The project addresses network segmentation, inter-VLAN routing, Network Address Translation (NAT), secure remote management and the addition of a secondary ISP connection for improved connectivity resilience.

The network is implemented and documented using Cisco Packet Tracer, with supporting evidence provided in this GitHub portfolio.

2. Project Objectives

The main objectives are to:

- Design a logical and physical network topology.
- Divide the network into VLANs for departments and services.
- Implement an IPv4 addressing plan using the allocated address block.
- Configure inter-VLAN routing.
- Implement NAT for internal network traffic.
- Configure primary and secondary ISP connections.
- Configure secure remote management using SSH.
- Test network connectivity and document implementation evidence.

3. Network Segmentation and IP Addressing

The network uses eight VLANs to separate departments, services and management traffic.

| VLAN | Name | Network | Subnet Mask | Default Gateway |
|---:|---|---|---|---|
| 10 | ADMIN | `172.30.34.0/26` | `255.255.255.192` | `172.30.34.1` |
| 20 | BOOKINGS | `172.30.34.64/26` | `255.255.255.192` | `172.30.34.65` |
| 30 | FINANCE | `172.30.35.0/27` | `255.255.255.224` | `172.30.35.1` |
| 40 | MANAGEMENT | `172.30.35.32/27` | `255.255.255.224` | `172.30.35.33` |
| 50 | OPERATIONS | `172.30.34.128/26` | `255.255.255.192` | `172.30.34.129` |
| 60 | SERVERS | `172.30.35.64/27` | `255.255.255.224` | `172.30.35.65` |
| 70 | NET-MGMT | `172.30.35.96/27` | `255.255.255.224` | `172.30.35.97` |
| 80 | GUEST | `172.30.34.192/26` | `255.255.255.192` | `172.30.34.193` |

VLAN segmentation creates separate broadcast domains and provides a foundation for controlling communication between departments and services.

4. Network Infrastructure

The simulated network includes:

- **SW-CORE:** Central switching infrastructure.
- **SW-ACCESS1, SW-ACCESS2 and SW-ACCESS3:** Access switches for connected devices.
- **R-EDGE:** Router providing inter-VLAN routing and external network connectivity.
- **SRV-1:** Server connected through the server VLAN.
- **Primary ISP:** Primary external network connection.
- **Secondary ISP:** Additional connection intended to improve resilience.
- **End devices:** Departmental PCs and management workstations.

The core and access switches use trunk links to carry the configured VLAN traffic. Router subinterfaces provide the default gateways for the VLANs.

5. Network Address Translation (NAT)

NAT was configured on R-EDGE to support translation of internal network traffic at the network edge.

The configuration includes NAT inside settings on the internal VLAN subinterfaces and NAT outside settings on the two ISP-facing interfaces. NAT access control lists and overload rules were also configured.

The final NAT assessment should be supported by translation-table output and connectivity tests demonstrating the intended translations. The presence of NAT commands alone does not establish that all required translations have been verified.

6. Dual ISP Connectivity and Resilience

The network includes two external connections:

| Connection | R-EDGE Interface | R-EDGE Address | ISP Address |
|---|---|---|---|
| Primary ISP | GigabitEthernet0/1 | `10.0.0.1/30` | `10.0.0.2/30` |
| Secondary ISP | GigabitEthernet0/2 | `10.0.0.5/30` | `10.0.0.6/30` |

A primary default route points to `10.0.0.2`. A floating static default route points to `10.0.0.6` with an administrative distance of 10.

This configuration is intended to provide a backup route if the primary route becomes unavailable. Automatic failover should be confirmed by testing the loss of the primary path and verifying that traffic can use the secondary path.

7. Remote Network Management

SSH version 2 was configured on R-EDGE to provide encrypted remote command-line access.

The configuration includes:

- Router hostname and domain name.
- A local administrator account.
- 1024-bit RSA keys.
- SSH version 2.
- Local authentication on the VTY lines.
- SSH-only remote terminal access.

The SSH status was verified using `show ip ssh`, and the configuration was saved to startup configuration.

A remote SSH session was successfully established from MGMT-PC1 in VLAN 40 (MANAGEMENT), using IP address `172.30.35.40` to access the router at `172.30.35.33`.

VLAN 70 (NET-MGMT) is configured in the addressing plan, but remote access through that dedicated VLAN still requires separate verification.

8. Testing and Verification

The following results were recorded during implementation:

| Test | Recorded Result |
|---|---|
| Router interface status | Configured VLAN subinterfaces and both ISP interfaces reported up/up |
| MGMT-PC1 to VLAN 40 gateway | Four ping replies received |
| Primary ISP gateway `10.0.0.2` | Four replies from five attempts in the recorded test |
| Secondary ISP gateway `10.0.0.6` | Five replies from five attempts in the recorded test |
| SSH status | SSH version 2 confirmed enabled |
| Remote SSH access | Successful session from MGMT-PC1 to R-EDGE |

These results verify selected aspects of the implementation. Full NAT functionality, automatic ISP failover, connectivity across all VLANs, and dedicated management access through VLAN 70 should only be reported as verified when their corresponding tests and evidence are available.

9. Evidence Portfolio

The repository includes supporting implementation evidence. The following screenshots were previously reported as uploaded:

- `NAT_Configuration_Evidence.png`
- `NAT_Statistics_Evidence.png`
- `ISP_Failover_Evidence.png`

Additional evidence should include the logical topology, VLAN and trunk configuration, router interface status, successful connectivity tests and SSH remote-management session.

10. Project Deliverables

The final project submission consists of:

1. Cisco Packet Tracer project file (`.pkt`).
2. GitHub portfolio of evidence.
3. Technical report.
4. 15–20-minute demonstration video.
5. Any additional files required by the project brief or assessment rubric.

The Packet Tracer file and technical report should reflect the actual implemented configuration and distinguish verified results from features that still require testing.

11. Conclusion

The project demonstrates the design and implementation of a segmented business network using Cisco Packet Tracer. It incorporates VLANs, inter-VLAN routing, NAT configuration, dual ISP connectivity and SSH-based remote management.

The GitHub repository serves as the portfolio of evidence for the network design, implementation and testing. Final submission should include the working `.pkt` file, completed technical report, supporting screenshots and the required demonstration video.

