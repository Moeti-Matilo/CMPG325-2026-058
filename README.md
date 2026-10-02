CMPG325 Individual Semester Project

Project ID: CMPG325-2026-058
Client ID: CLI-058
Organisation: Botshelo Safari Adventures
Industry: Tourism
Location: Rustenburg

Project Overview

This repository contains the portfolio of evidence for my CMPG325 Computer Networks individual semester project. The project involves designing, implementing, testing and documenting a network solution for Botshelo Safari Adventures using Cisco Packet Tracer.

Milestone 1

The initial design stage includes:
- Client requirements analysis
- Physical network topology
- Logical network topology
- IP addressing plan
- Initial Packet Tracer topology

Assigned Technical Challenge

NAT (inside/outside address translation)

Design Constraint

Remote management of network devices for an off-site IT contractor.

Change Request CR15

A second Internet connection must be integrated to provide resilience.




Milestone 2 – Client Implementation Review

Assigned Feature: NAT and ISP Failover

The assigned network feature for Milestone 2 was implemented on the edge router.

Implemented Features
* Network Address Translation (NAT) for internal VLAN networks.
* Primary ISP NAT using GigabitEthernet0/1.
* Secondary ISP NAT using GigabitEthernet0/2.
* NAT overload (PAT) for internal private IP addresses.
* Primary default route through the primary ISP.
* Floating secondary default route for ISP resilience.
* CR15 second-ISP failover implemented and tested.
* Remote-management network infrastructure retained from the original design.

NAT Configuration
Primary NAT:
* ACL 101
* Outside interface: GigabitEthernet0/1
* Simulated external destination: 203.0.113.1

Secondary NAT:
* ACL 102
* Outside interface: GigabitEthernet0/2
* Simulated external destination: 198.51.100.1

Internal VLAN interfaces are configured as NAT inside interfaces, while both WAN interfaces are configured as NAT outside interfaces.

Testing Evidence

Primary ISP and NAT

PC-ADMIN1 successfully reached the simulated primary ISP destination:
`203.0.113.1`

Test result:
* 3 successful replies out of 4 packets after the primary WAN interface was restored.

Secondary ISP and NAT

The primary WAN connection was intentionally shut down to simulate an ISP failure.

The routing table changed from:
`0.0.0.0/0 via 10.0.0.2`

to the floating backup route:
`0.0.0.0/0 via 10.0.0.6`

PC-ADMIN1 then successfully reached the simulated secondary ISP destination:
`198.51.100.1`

Test result:
* 4 successful replies out of 4 packets.

NAT Verification

NAT statistics recorded successful NAT processing, including:
* NAT hits: 22
* NAT outside interfaces: GigabitEthernet0/1 and GigabitEthernet0/2
* NAT inside interfaces: all eight VLAN subinterfaces

Evidence Files

The following evidence was captured during implementation:

* NAT configuration evidence
* NAT statistics evidence
* Primary routing evidence
* Secondary failover routing evidence
* Packet Tracer topology/configuration

Final Deliverable
The final Packet Tracer project file contains the implemented NAT configuration, primary/secondary ISP connections, and CR15 failover configuration.
