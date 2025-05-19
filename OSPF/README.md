# OSPF Lab

- This is a practical OSPF lab designed to demonstrate basic OSPF configuration, neighbor formation, and route advertisement across four routers whilst 
also connecting 2 end hosts (PCs) on different networks that are connected through the routers. 
- The end goal is for the 2 end hosts to be able to communicate with eachother.

## Network Topology & Addressing

| Device   | Interface | IP Address        | Notes             |
|----------|-----------|-------------------|-------------------|
| **Router 1** | G0/0      | 10.0.11.1/30      | Link to Router 2  |
|          | G0/1      | 10.0.14.1/30      | Link to Router 4  |
|          | G0/2      | 192.168.1.1/24    | LAN, Passive Interface |
|          | Router ID | 1.1.1.1           |                   |
| **Router 2** | G0/0      | 10.0.11.2/30      | Link to Router 1  |
|          | G0/1      | 10.0.12.2/30      | Link to Router 3  |
|          | Router ID | 2.2.2.2           |                   |
| **Router 3** | G0/0      | 10.0.12.1/30      | Link to Router 2  |
|          | G0/1      | 10.0.13.1/30      | Link to Router 4  |
|          | G0/2      | 192.168.4.1/24    | LAN, Passive Interface |
|          | Router ID | 3.3.3.3           |                   |
| **Router 4** | G0/0      | 10.0.14.2/30      | Link to Router 1  |
|          | G0/1      | 10.0.13.2/30      | Link to Router 3  |
|          | Router ID | 4.4.4.4           |                   |
| **PC1**  | FA0/1       | 192.168.1.10/24   | Default Gateway: 192.168.1.1 |
| **PC2**  | FA0/1       | 192.168.4.10/24   | Default Gateway: 192.168.4.1 |


##  Configuration Highlights

- OSPF is configured on all routers with router IDs set explicitly.
- Point-to-point links use /30 subnets between routers.
- LAN interfaces (`G0/2` on Router 1 and Router 3) are configured as **passive interfaces** to prevent OSPF neighbor formation on those LAN ports while still advertising the connected networks.
- PCs connected to the LAN subnets can ping across the network through OSPF routing.
