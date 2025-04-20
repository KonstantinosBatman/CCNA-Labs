# Static Routing in Cisco Packet Tracer

## Project Overview

This project demonstrates how to configure **static routing** in a network using **Cisco Packet Tracer**. The network consists of 3 routers, 2 switches, and 2 PCs that are in different networks. The goal of the project is to configure static routes between the routers to enable communication between the two PCs.

The network topology is as follows:

- **PC1** is on the **192.168.1.0/24** network.
- **PC2** is on the **192.168.4.0/24** network.
- The routers are configured to route traffic between the two different networks using static routes.

## Network Topology

The network consists of the following devices:

- **PC1** (IP: 192.168.1.10/24, Gateway: 192.168.1.1)
- **PC2** (IP: 192.168.4.10/24, Gateway: 192.168.4.1)
- **Router1** (G0/0/0 IP: 192.168.1.1, G0/0/1 IP: 192.168.30.1)
- **Router2** (G0/0/0 IP: 192.168.30.4, G0/0/1 IP: 192.168.20.1)
- **Router3** (G0/0/0 IP: 192.168.20.5, G0/0/1 IP: 192.168.4.1)

The routers are connected as follows:

- **Router1** is connected to **Router2** via **G0/0/1** (IP: 192.168.30.1).
- **Router2** is connected to **Router1** via **G0/0/0** (IP: 192.168.30.2) and **Router3** via **G0/0/1** (IP: 192.168.20.1).
- **Router3** is connected to **Router2** via **G0/0/0** (IP: 192.168.20.5) and to **PC2** via **G0/0/1** (IP: 192.168.4.1).

## Static Routing Configuration

### Router1 Configuration
Router1 has two interfaces:
- **G0/0/0** connected to PC1 (IP: 192.168.1.1).
- **G0/0/1** connected to Router2 (IP: 192.168.30.1).

**Static Route Configuration:**
Router1 needs to know how to reach **PC2’s network (192.168.4.0/24)** via Router2. The static route is added as:

```
ip route 192.168.4.0 255.255.255.0 192.168.30.4
```


### Router2 Configuration
Router2 has two interfaces:
- **G0/0/0** connected to Router1 (IP: 192.168.30.4).
- **G0/0/1** connected to Router3 (IP: 192.168.20.1).

**Static Route Configuration:**
Router2 needs to know how to reach **PC1’s network (192.168.1.0/24)** via Router1 and how to reach **PC2’s network (192.168.4.0/24)** via Router3. The static routes are added as:

```
ip route 192.168.1.0 255.255.255.0 192.168.30.1 
ip route 192.168.4.0 255.255.255.0 192.168.20.5
```
### Router3 Configuration
Router3 has two interfaces:
- **G0/0/0** connected to Router2 (IP: 192.168.20.5).
- **G0/0/1** connected to PC2 (IP: 192.168.4.1).

**Static Route Configuration:**
Router3 needs to know how to reach **PC1’s network (192.168.1.0/24)** via Router2. The static route is added as:

```
ip route 192.168.1.0 255.255.255.0 192.168.20.1
```


## Configuration Steps

1. **Set up the PCs:**
   - Configure the IP addresses, subnet masks, and default gateways on **PC1** and **PC2**.
   - PC1: IP 192.168.1.10, Gateway 192.168.1.1
   - PC2: IP 192.168.4.10, Gateway 192.168.4.1

2. **Configure Router1:**
   - Assign IP addresses to interfaces G0/0/0 (192.168.1.1) and G0/0/1 (192.168.30.1).
   - Add a static route to Router2’s G0/0/0 interface for PC2’s network:
     ```
     ip route 192.168.4.0 255.255.255.0 192.168.30.2
     ```

3. **Configure Router2:**
   - Assign IP addresses to interfaces G0/0/0 (192.168.30.2) and G0/0/1 (192.168.20.1).
   - Add static routes to Router1 and Router3 for communication between networks:
     ```
     ip route 192.168.1.0 255.255.255.0 192.168.30.1
     ip route 192.168.4.0 255.255.255.0 192.168.20.5
     ```

4. **Configure Router3:**
   - Assign IP addresses to interfaces G0/0/0 (192.168.20.5) and G0/0/1 (192.168.4.1).
   - Add a static route to Router2’s G0/0/1 interface for PC1’s network:
     ```
     ip route 192.168.1.0 255.255.255.0 192.168.20.1
     ```

5. **Verify Connectivity:**
   - Once the static routes are configured, use the `ping` command from **PC1** to **PC2** and vice versa to verify that the routing is set up correctly.

## Troubleshooting

- **If the ping fails:** Check the routing tables on each router using the `show ip route` command to ensure the static routes are properly added.
- **Check interface statuses:** Make sure all router interfaces are up and that there are no issues with the physical layer (e.g., cables or switches).
- **Verify IP configurations:** Ensure that the PCs and routers have the correct IP addresses and subnet masks configured.

## Conclusion

This project demonstrates how to configure static routing between multiple routers to allow communication between PCs on different networks. By using static routes, we can control the path that packets take through the network, which is an important concept in networking.

