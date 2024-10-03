# External BGP Connecting 3 Autonomous Systems

## Autonomous Systems (AS) each running a different IGP, OSPF, EIRGP, RIP
The internet is a collection of autonomous systems, or networks controlled by different organizations. To facilitate routing between each system, an external gateway protocol is used. The most common protocol used today is BGP, or border gateway protocol. autonomous systems form a "neighborship", establishing a TCP connection and exchanging routes. The process of connecting two BGP routes is called peering. Anyone facilitating such a router in a real-world autonomous system connected to the internet can expect more than 50,000 routes to be added through BGP.  

This lab is an extremely simplified model of the internet, 3 autonomous systems each running their own internal gateway protocol (IGP) are connected and configured to advertise all routes to each other. This results in any device being able to ping every address in the network. 

## Topology
<p align="center">
    <img src="./images/Topology.svg" width="75%">
</p>

## IP Address Configuration

| Device | Interface  | IPv4         | IPv6        |
|:-------|:-----------|:------------:|:-----------:|
| R1     | Loopback 0 | 11.0.0.1/24  | 11::1/64    |
|        | S0/1/0     | 10.0.0.1/24  | 1::1/64     |
| R2     | S0/1/0     | 10.0.0.2/24  | 1::2/64     |
|        | G0/0/0     | 9.1.0.1/24   | 9::1/64     |
|        | G0/0/1     | 9.3.0.1/24   | 9:3::1/64   |
| R3     | S0/1/0     | 20.0.0.1/24  | 2::1/64     |
|        | G0/0/0     | 9.1.0.2/24   | 9::2/64     |
| R4     | S0/1/0     | 20.0.0.2/24  | 2::2/64     |
|        | G0/0/0     | 9.2.0.1/24   | 9:2::1/64   |
| R5     | S0/1/0     | 30.0.0.1/24  | 3::1/64     |
|        | G0/0/0     | 9.2.0.2/24   | 9:2::2/64   |
|        | G0/0/1     | 9.3.0.2/24   | 9:3::2/64   |
| R6     | Loopback 0 | 33.0.0.1/24  | 33::1/64    |
|        | S0/1/0     | 30.0.0.2/24  | 3::2/64     |

## Device Overview
### Routers
* 6 Cisco 4321 ISRs running Cisco IOS XE Software, Version 16.09.08 Universal K9

### ICMPv4 Ping Across Network
```
Sending 5, 100-byte ICMP Echos to 33.0.0.1, timeout is 2 seconds:
Packet sent with a source address of 11.0.0.1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/3 ms
```
### ICMPv6 Ping Across Network
```
Sending 5, 100-byte ICMP Echos to 33::1, timeout is 2 seconds:
Packet sent with a source address of 11::1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/2/3 ms
``` 
