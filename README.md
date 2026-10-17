# Ethernet Switching, MAC Address Learning, and VLAN Segmentation Lab/Project

## Objective

This lab/project aims to develop practical skills in Ethernet switching, MAC address learning, VLAN segmentation, broadcast domains, trunking, inter-VLAN routing, and Layer 2 network troubleshooting. In this lab, I used a multi-VM VirtualBox homelab consisting of Windows and Linux systems to examine Ethernet frames, MAC addresses, ARP traffic, and network communication using Wireshark. I also explored how switches learn MAC addresses, forward unicast traffic, flood unknown-destination frames, and handle broadcast and multicast communication.

To gain hands-on experience with enterprise networking concepts, I analyzed Ethernet frame headers, captured ARP requests and replies, simulated switch MAC address learning and aging, and examined the differences between collision domains and broadcast domains. I also studied how VLANs logically segment networks, how access ports and IEEE 802.1Q trunk ports operate, and how Layer 3 routing enables communication between separate VLANs. Building on my existing homelab, I designed a proposed enterprise network consisting of five VLANs for management, servers, clients, security, and testing, including subnet assignments, switch port configurations, and planned OPNsense firewall routing. Finally, I completed network troubleshooting scenarios involving incorrect VLAN assignments, MAC address aging, trunk misconfigurations, and inter-VLAN connectivity issues, while updating my network diagrams and IPAM documentation. This project strengthened my understanding of Layer 2 switching, Ethernet communication, VLAN architecture, network segmentation, and enterprise network troubleshooting while establishing a foundation for future network infrastructure and security implementations.

### Skills Learned

This project provided hands-on experience with the following Ethernet switching, VLAN segmentation, enterprise networking, and Layer 2 troubleshooting skills:

- Ethernet and OSI Layer 2 concepts, including Ethernet frame structure, encapsulation, MAC addressing, and the relationship between Ethernet frames and IP packets
- MAC address learning and switch forwarding behavior, including source MAC learning, MAC address tables, known and unknown unicast forwarding, frame flooding, and MAC address aging
- ARP and Ethernet traffic analysis using Wireshark to capture and inspect Ethernet frames, ARP requests and replies, ICMP traffic, and unicast, broadcast, and multicast MAC addresses
- VLAN segmentation and enterprise network design, including creating logical network boundaries for management, servers, clients, security infrastructure, and testing environments
- Access and trunk port configuration concepts, including VLAN membership, IEEE 802.1Q tagging, and carrying multiple VLANs across trunk connections
- IPv4 subnet planning and VLAN-to-subnet mapping, including calculating network addresses, usable host ranges, broadcast addresses, subnet masks, and default gateways
- Network documentation and IP address management (IPAM), including updating homelab network diagrams, creating VLAN assignment tables, documenting switch port configurations, and maintaining current and proposed network architectures

### Tools Used

- Oracle VirtualBox
- Wireshark
- Windows 10
- Ubuntu Linux
- Windows Command Prompt
- Linux Terminal
- Windows networking utilities (`ipconfig`, `arp`, `ping`)
- Linux networking utilities (`ip addr`, `ip link`, `ip neigh`, `ip route`, `ping`)
- Wireshark display filters (`arp`, `icmp`, `eth.addr`, `eth.dst`)
- Python 3 (`ipaddress` module for subnet verification)
- Ethernet switching and MAC address table simulations
- VLAN and IEEE 802.1Q trunking design exercises
- Cisco IOS-style switch commands (conceptual troubleshooting and configuration examples)
- OPNsense Firewall (proposed inter-VLAN routing and firewall architecture)

## Current Lab Environment Architecture/Setup

Below is a screenshot of my current lab architecture before and after this weeks Lab/Project (IM1&2). This week was more practice than real hands-on work. 

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/4a9a0c08-1a45-487f-baec-3188b8babfd4" />
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/c36009df-d9cf-4517-ad32-abd8a84bfdfe" />

IM1&2: Current Lab Environment/Architecture before and after this weeks lab/project















































