# Inter-VLAN Setup for IT, Sales, and HR

![Inter-VLAN Network Diagram](Inter-VLAN-Routing/Images/VLAN_Topology.PNG)

**Project Description**:  
This project demonstrates the configuration and management of Inter-VLAN Routing (IVR) between three VLANs: IT, Sales, and HR, using a Cisco router. The router performs the routing between VLANs, allowing devices on different VLANs to communicate with each other.


**Technologies Used**:  
- Cisco Packet Tracer
- Cisco Routers (Router-on-a-Stick Configuration)
- VLAN Configuration
- Routing Configuration

## Project Overview

This project adds **Inter-VLAN Routing (IVR)** functionality to a network with the following VLANs:

- **VLAN 10 (IT)**: Used for IT-related devices.
- **VLAN 20 (Sales)**: Used for Sales-related devices.
- **VLAN 30 (HR)**: Used for HR-related devices.

The router-on-a-stick method is used to enable inter-VLAN routing, where a router connects to a switch via a single trunk link and uses sub-interfaces for each VLAN. This configuration allows devices in different VLANs to communicate with each other.

### **Network Design**

- **Router**: The router will have sub-interfaces for each VLAN.
- **Switch**: The switch will have trunk ports connecting to the router to allow traffic from multiple VLANs.


## CLI Commands
Configuring VLANs on the switch:

- VLAN 10 for IT
- VLAN 20 for Sales
- VLAN 30 for HR

```bash
SW1(config)# vlan 10
SW1(config-vlan)# name IT
SW1(config)# vlan 20
SW1(config-vlan)# name Sales
SW1(config)# vlan 30
SW1(config-vlan)# name HR

SW1(config)# interface range fa0/1-2
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 10

SW1(config)# interface range fa0/3-4
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 20

SW1(config)# interface range fa0/5-6
SW1(config-if-range)# switchport mode access
SW1(config-if-range)# switchport access vlan 30
```
- Configuring the trunk port:
```bash
SW1(config)# interface fa0/24
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,20,30
```
- Router Configurations
```bash
R1(config)# interface gig0/0.10
R1(config-if)# encapsulation dot1Q 10
R1(config-if)# ip address 192.168.10.254 255.255.255.0

R1(config)# interface gig0/0.20
R1(config-if)# encapsulation dot1Q 20
R1(config-if)# ip address 192.168.20.254 255.255.255.0

R1(config)# interface gig0/0.30
R1(config-if)# encapsulation dot1Q 30
R1(config-if)# ip address 192.168.30.254 255.255.255.0
```
## Testing and Verification
```bash
R1# show ip route
R1# show ip interface brief
R1# show interfaces gig0/0.10
R1# show interfaces gig0/0.20
R1# show interfaces gig0/0.30
```
Ping Test:
- Every PC in every VLAN should be able to ping eachother.
