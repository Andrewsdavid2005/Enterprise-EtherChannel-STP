# Enterprise EtherChannel & STP Redundancy

## Project Overview

This project demonstrates an enterprise network switching environment designed using Cisco Packet Tracer.

It implements VLAN segmentation, LACP EtherChannel, and Rapid Spanning Tree Protocol (Rapid PVST+) to improve network availability, prevent switching loops, and provide link redundancy.

## Project Objectives

- Configure VLAN 10 (HR) and VLAN 20 (Finance).
- Implement LACP EtherChannel between switches.
- Configure trunk links for VLAN traffic.
- Enable Rapid PVST+ to prevent Layer 2 loops.
- Configure STP root and secondary root bridges.
- Test EtherChannel member-link failure.
- Verify network connectivity and redundancy.

## Network Topology

**Devices used:**
- 3 × Cisco 2960 switches
- 6 × PCs
- Cisco Packet Tracer

### Switch Configuration

| Switch | Role |
|---|---|
| SW1 | Core Switch / STP Root Bridge |
| SW2 | HR Department Switch / Secondary Root |
| SW3 | Finance Department Switch |

### VLAN Configuration

| VLAN ID | Department | Network |
|---|---|---|
| 10 | HR | 192.168.10.0/24 |
| 20 | Finance | 192.168.20.0/24 |

### PC Addressing

| PC | VLAN | IP Address |
|---|---|---|
| PC1 | 10 | 192.168.10.10 |
| PC2 | 10 | 192.168.10.11 |
| PC3 | 10 | 192.168.10.12 |
| PC4 | 10 | 192.168.10.13 |
| PC5 | 20 | 192.168.20.10 |
| PC6 | 20 | 192.168.20.11 |

## EtherChannel Configuration

LACP (Link Aggregation Control Protocol) was used to combine multiple physical links into logical Port-channel interfaces.

| EtherChannel | Switches | Ports |
|---|---|---|
| Port-channel 1 | SW1–SW2 | Fa0/21–22 |
| Port-channel 2 | SW1–SW3 | Fa0/23–24 |

### LACP Example

```cisco
interface range fa0/21-22
switchport mode trunk
channel-group 1 mode active
```

## Spanning Tree Protocol

Rapid PVST+ was enabled on all switches.

```cisco
spanning-tree mode rapid-pvst
```

SW1 was configured as the primary root bridge:

```cisco
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root primary
```

SW2 was configured as the secondary root bridge:

```cisco
spanning-tree vlan 10 root secondary
spanning-tree vlan 20 root secondary
```

## Verification Commands

```cisco
show vlan brief
show interfaces trunk
show etherchannel summary
show spanning-tree
show spanning-tree vlan 10
show spanning-tree vlan 20
```

## Testing

The following tests were performed or planned:

1. Same-VLAN connectivity between PCs.
2. EtherChannel operational status.
3. Failure of one EtherChannel member link.
4. STP loop prevention on the redundant SW2–SW3 link.
5. Network recovery after restoring links.

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS
- VLAN
- LACP EtherChannel
- Rapid PVST+
- Spanning Tree Protocol
- Layer 2 Switching

## Learning Outcomes

- Understanding enterprise switching architecture.
- Implementing link aggregation using LACP.
- Configuring VLANs and trunk links.
- Understanding STP root bridge elections.
- Troubleshooting switching loops.
- Testing network redundancy and failover.

## Author

Andrews GnanaSelvin D

GitHub: https://github.com/Andrewsdavid2005

LinkedIn: https://www.linkedin.com/in/andrews-gnana-selvin-d

## Project Status

Configuration and testing documentation prepared. Update the testing section with verified results before publishing.
