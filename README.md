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

## Steps/Procedure

### Part 1: Baseline and Adapter Identification

Before starting the lab, I wanted to get a baseline of my VMs, specifically the Windows 10 VM and Ubuntu Server. I got the VMs adapters, IP and MAC information, as well as ARP info. I also mapped them as well (IM3-10).

<img width="835" height="107" alt="Screenshot 2026-10-12 171756" src="https://github.com/user-attachments/assets/1f3a0745-3c4e-4b9d-913e-37dd08524d42" />
<img width="606" height="693" alt="Screenshot 2026-10-12 171912" src="https://github.com/user-attachments/assets/0dd3cccb-db0b-4341-ba32-ada91b876dfc" />
<img width="391" height="139" alt="Screenshot 2026-10-12 172144" src="https://github.com/user-attachments/assets/df9ebd25-79e9-46f8-8be9-2baad448a718" />
<img width="694" height="106" alt="Screenshot 2026-10-12 172240" src="https://github.com/user-attachments/assets/db65cd04-2a4d-4572-aa76-cc641a9a452b" />
<img width="923" height="110" alt="Screenshot 2026-10-12 172330" src="https://github.com/user-attachments/assets/82e6a4da-2fba-4c0e-8c16-b5a0bf41b1e9" />
<img width="961" height="65" alt="Screenshot 2026-10-12 172405" src="https://github.com/user-attachments/assets/e74018d7-05d0-48a2-86ff-8e521dd9ff47" />
<img width="520" height="360" alt="Screenshot 2026-10-12 172758" src="https://github.com/user-attachments/assets/7b550548-0a9b-40f0-8ed0-6e653e0418a3" />
<img width="523" height="360" alt="Screenshot 2026-10-12 172933" src="https://github.com/user-attachments/assets/a6120185-a2ad-4684-9101-52333a564aa3" />

IM3-10: Windows 10 and Ubuntu Server IP and MAC Info

### Part 2: Ethernet Header Inspection

Next I wanted to inspect some packets in Wireshark and see the ethernet header. I started a new capture and did a ping from the Windows 10 VM to the Ubuntu VM to generate ICMP packets. I used the "icmp" filter (IM11) and looked at one of the Echo Request packets. Inside the packet, I saw the source and destination MAC Addresses as well as source and destination IP addresses (IM11&12)

<img width="816" height="85" alt="Screenshot 2026-10-12 173431" src="https://github.com/user-attachments/assets/244a845d-233b-42c3-bc25-2e2a405a2c89" />
<img width="525" height="252" alt="Screenshot 2026-10-12 173608" src="https://github.com/user-attachments/assets/aa6c63b0-06a4-40a2-9f14-cb0623baae91" />

IM11&12: MAC and IP Headers in ICMP Echo Request Packet

### Part 3: Broadcast ARP vs Unicast Traffic

Now I specifically wanted to see Broadcast vs unicast packets. I started a fresh packet capture and removed Ubuntu from Window's arp cache so it could be re-added and activity could be generated in Wireshark. I started a fresh capture, pinged again, then filtered for arp packets. I looked at the packet for Windows looking for Ubuntu's MAC and looked at the Ethernet header. The destination MAC was "ff-ff-ff-ff-ff-ff. (IM13)" This is because since Windows doesn't know Ubuntu's MAC address, it broadcasts to the rest of the network waiting for a response. Then for the response, Ubuntu tells Windows where its MAC address is (IM14). I also filtered for broadcast addresses only (IM15). 

<img width="940" height="86" alt="Screenshot 2026-10-12 174651" src="https://github.com/user-attachments/assets/8ec46468-7ce3-422e-9aef-9a408730fcb2" />

IM13: Arp Packet with Broadcast Address

<img width="777" height="100" alt="Screenshot 2026-10-12 174819" src="https://github.com/user-attachments/assets/5dbea6e1-25aa-46b9-ba44-0c1186dcf4c3" />

IM14: Response from Ubuntu with MAC Address

<img width="845" height="239" alt="Screenshot 2026-10-12 174920" src="https://github.com/user-attachments/assets/22444d65-04c4-423e-8f1c-de8ef91bab66" />

IM15: Using Broadcast Filter in Wireshark

### Part 4: VLAN Practice

The rest of this weeks lab was mostly theory and practice with learning VLANs. I created a proposed future Lab plan and what it could look like with VLANs in the future (IM16). 

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/b2b38cde-97b5-4391-94b8-48c08a0c0b34" />

IM16: Future Proposed Network Design

## Conclusion

This lab successfully demonstrated the core concepts of Ethernet switching, MAC address learning, VLAN segmentation, broadcast domains, trunking, inter-VLAN routing, and Layer 2 network troubleshooting. Throughout the project, I used Windows and Linux systems within my VirtualBox homelab to examine network interfaces, MAC addresses, ARP tables, and Ethernet communication. I also used Wireshark to capture and analyze Ethernet frames, ARP requests and replies, and ICMP traffic, allowing me to observe how devices communicate within a local network. Additionally, I simulated switch MAC address learning, explored access and trunk port behavior, and designed a proposed enterprise network consisting of five VLANs with dedicated subnets, switch port assignments, and planned inter-VLAN routing through an OPNsense firewall.

Overall, this project strengthened my understanding of Ethernet frames, MAC addressing, switch forwarding decisions, unicast and broadcast traffic, collision and broadcast domains, VLAN isolation, IEEE 802.1Q tagging, and Layer 2 versus Layer 3 communication. I also gained experience designing a segmented enterprise network, planning VLAN addressing through IPAM, troubleshooting common switching and VLAN connectivity issues, and updating my homelab network diagrams to document both the existing environment and proposed infrastructure. The hands-on experience and network design skills gained from this lab provide a strong foundation for future work in network administration, enterprise infrastructure management, firewall configuration, network segmentation, security monitoring, and cybersecurity.
























































