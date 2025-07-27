# Simple Network Topology in Cisco Packet Tracer

This repository showcases a fundamental network setup designed and implemented using Cisco Packet Tracer. The project aims to demonstrate core networking concepts including IP addressing, subnetting, and enabling communication between different network segments via a router.

## Project Goal

The primary objective was to establish a functional network where devices (PCs) located in distinct IP subnets can successfully communicate with each other, leveraging a central router for inter-subnet routing.

## Network Topology Overview

The setup includes:

* **4 End Devices (PCs):** Logically grouped into two separate IP subnets.
* **2 Layer 2 Switches:** Each serving as the local connectivity point for one IP subnet.
* **1 Router:** Acting as the gateway between the two subnets, enabling cross-subnet communication.

## IP Addressing Scheme

The following IP addressing plan was used for the devices:

| Device           | IP Address    | Subnet Mask     | Default Gateway (for PCs) | Connected To |
| :--------------- | :------------ | :-------------- | :------------------------ | :----------- |
| PC0              | 192.168.1.10  | 255.255.255.0   | 192.168.1.1               | Switch 1     |
| PC1              | 192.168.1.11  | 255.255.255.0   | 192.168.1.1               | Switch 1     |
| PC2              | 192.168.2.10  | 255.255.255.0   | 192.168.2.1               | Switch 2     |
| PC3              | 192.168.2.11  | 255.255.255.0   | 192.168.2.1               | Switch 2     |
| Router (Gi0/0)   | 192.168.1.1   | 255.255.255.0   | N/A                       | Switch 1     |
| Router (Gi0/1)   | 192.168.2.1   | 255.255.255.0   | N/A                       | Switch 2     |

## Key Configurations

### Router Configuration (Cisco IOS CLI commands):

The router was configured with two interfaces, each acting as the default gateway for its respective subnet.

```cli
enable
configure terminal
! Interface connected to 192.168.1.0/24 network (Switch 1)
interface GigabitEthernet0/0   # IMPORTANT: Adjust this interface name if yours is different (e.g., FastEthernet0/0)
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

! Interface connected to 192.168.2.0/24 network (Switch 2)
interface GigabitEthernet0/1   # IMPORTANT: Adjust this interface name if yours is different (e.g., FastEthernet0/1)
 ip address 192.168.2.1 255.255.255.0
 no shutdown
 exit

end
copy running-config startup-config

**## PC Configuration:**
Each PC was statically configured with its IP address, subnet mask, and the appropriate default gateway (the router's interface IP for its subnet). Screenshots of the PC configurations are available in the images/ folder (if you upload them).

**Verification**
Connectivity was thoroughly verified using the ping command from various PCs:

Intra-subnet communication: Pinging between PCs within the same subnet (e.g., PC0 to PC1) was successful.

Gateway reachability: Each PC could successfully ping its designated default gateway (the router's interface).

Inter-subnet communication: Crucially, PCs in different subnets could successfully ping each other (e.g., PC0 to PC2), confirming the router's proper function in routing traffic between segments.

**How to Use This Project**
Download: Download the [YourFileName].pkt file (e.g., Cisco-Simple-LAN.pkt) from this repository.

Open in Packet Tracer: Open the downloaded .pkt file using Cisco Packet Tracer.

Explore and Test: You can then examine the topology, review device configurations, and conduct your own ping tests from the PCs' "Desktop" -> "Command Prompt" to observe the network's behavior.
