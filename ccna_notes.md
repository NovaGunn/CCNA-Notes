  ------------------------------------------------------------------------
  TCP:               Port:             UDP:            Port:
  ------------------ ----------------- --------------- -------------------
  FTP                21                TFTP            69

  SSH                22                SNMP            161

  Telnet             23                                

  HTTP               80                                

  HTTPS              443               **TCP & UDP**:  **Port:**

                                       DNS             53
  ------------------------------------------------------------------------

# Layer 4: Transport

# Layer 3: Network Layer

-   routing traffic through the network (destination) and quality of
    service (QoS).

-   ICMP = internet control message protocol; think of the command
    \[ping\]

# Decimal to Binary: IPv4

  -------------------------------------------------------------------------
  256      128      64      32      16      8       4       2       1
  -------- -------- ------- ------- ------- ------- ------- ------- -------
  1        0        0       0       1       0       1       0       0

  -------------------------------------------------------------------------

(The binary table above is wrong by one. Suppose to be 8 across not 9).

\(236\) = 100010100 ? Instructor led has an additional column (256) to
what Cisco teaches and the below answer is the correct answer.

  -----------------------------------------------------------------------
  128      64       32       16       8        4        2        1
  -------- -------- -------- -------- -------- -------- -------- --------
  1        1        1        0        1        1        0        0

  -----------------------------------------------------------------------

\(236\) = 11101100

-(108)

-(44)

-(12)

  -----------------------------------------------------------------------
  128      64       32       16       8        4        2        1
  -------- -------- -------- -------- -------- -------- -------- --------
  1        0        1        1        0        0        1        1

  -----------------------------------------------------------------------

\(179\) = 10110011

179 -- 128 = 51-32 = 19

# Wild mask: 

  -------------------------------------------------------------------------
  Standard mask 255:           255:           255:           255:
  ------------- -------------- -------------- -------------- --------------
  Subnet mask   255            255            255            000

  Wild mask     000            000            000            255
  -------------------------------------------------------------------------

Essentially the wild mask is the opposite of the subnet mask, meaning
its octets must add up to 255. Think of sudoku, when the numbers have to
add up to 10 in this scenario its 255 in each column.

# Class A addresses: 

Are always assigned as a 0 in the first octet. For example:

  -----------------------------------------------------------------------
  128      64       32       16       8        4        2        1
  -------- -------- -------- -------- -------- -------- -------- --------
  0        0        0        0        1        0        0        1

  -----------------------------------------------------------------------

What this means is that the address pool for class A addresses can be up
to 126.0.0.0 /8 With 127 reserved. A key feature of a class A address is
the subnet mask is always a

255.0.0.0 (/8)

127.0.0.1 reserved class A address = loopback address

You would use to test the device you are on. The local tcp/ip stack.

# Class B Addresses: 

Class B is one binary number along in the first octet. The example above
is a class A this one is class B. For example:

  -----------------------------------------------------------------------
  128      64       32       16       8        4        2        1
  -------- -------- -------- -------- -------- -------- -------- --------
  1        0        0        0        1        0        0        1

  -----------------------------------------------------------------------

Which allows the address to range from 128.0.0.0 to 191.0.0.0 /16

  -----------------------------------------------------------------------
  Class             First Octet       Slash             Dotted Decimal
  ----------------- ----------------- ----------------- -----------------
  A                 1-126             /8                255.0.0.0

  B                 128-191           /16               255.255.0.0

  C                 192-223           /24               255.255.255.0

  D                 224-239           Broadcast         

  E                 240-255           Experimental      
  -----------------------------------------------------------------------

# CIDR: Class inter-domain routing (1993)

This method replaced the older class-based (Class A, B, C) addressing
system and introduced more efficient IP address allocation and routing.

CIDR allows routers to advertise summarised address ranges, which helps
reduce the size of routing tables by consolidating multiple networks
into a single router entry. For example:

192.168.10.X/24\
10.15.0.0/16\
\
in CIDR notation, the number after the slash (/) represents the subnet
mask's bit length, indicating how many bits are used for the network
portion. The "X" signifies the start of the subnet and implies multiple
addresses within that range.\
\
This route aggregation conserves space in the routing table and improves
overall routing efficiency.\
\
Stops the table from having every single IP address entry being listed
individually in the table. With some networks consisting of hundreds of
IP addresses, this protocol really helps.

# Subnetting: 

To calculate the number of subnets available:

The formula is 2 to the power of number of subnet-bits.

2 to the power of number of bits we borrowed. For example, we been
assigned a class c address /24. We borrowed 4 bits from the /24 to make
a /28 subnet.

This becomes 2 to the power of 4 = 16 available subnets.

Hosts = 2 the power of host-bits minus 2:

FLM -- Fixed length subnet mask -- rip 1 (old protocol) essentially
forces all subnets to have the same amount of users.

What are the network address, broadcast address, and valid addresses for
the IP addresses 198.22.45.173 /26 ?

What is the subnet mask in dotted notation?

/26 =

11111111.11111111.11111111.11000000 =

255.255.255.192

+-----------------+-----------------+-----------------+-----------------+
| Subnet mask:    | Network         | Broadcast       | Valid host:     |
|                 | address:        | address:        |                 |
+=================+=================+=================+=================+
| 255.255.255.192 | 198.22.45.128   | 63 needed to    | 62 61           |
|                 |                 | add that to the |                 |
|                 | Needed to have  | network         | The full valid  |
|                 | laid out the    | address.        | host addresses: |
|                 | entire address  |                 |                 |
|                 | in binary.      | Only would have | 198.22.45.129   |
|                 |                 | known to do     | to              |
|                 | (slow way)      | this if I did   |                 |
|                 |                 | the network     | 198.22.45.190   |
|                 | Then added each | address first.  |                 |
|                 | octet in binary |                 | As the first    |
|                 | to have given   | 128+63 = 191    | number can only |
|                 | me the network  |                 | be 1 number     |
|                 | address         | 198.22.45.191   | above the       |
|                 |                 |                 | network address |
|                 |                 |                 | and below the   |
|                 |                 |                 | broadcast       |
|                 |                 |                 | address.        |
+-----------------+-----------------+-----------------+-----------------+

VLSM: Variable Length Subnet Masks

192.168.1. /27

8 subnets & 32 -2 =30 hosts

/27

Subnet mask binary: last octet

  -----------------------------------------------------------------------
  128      64       32       16       8        4        2        1
  -------- -------- -------- -------- -------- -------- -------- --------
  1        1        1        0        0        0        0        0

  -----------------------------------------------------------------------

128+64+32 = 224

11111111.11111111.11111111.11100000

255.255.255.224

198.168.1. 0 /27

NEED TO WORK ON MY NETWORK ADDRESSING & BROADCASTING

Allocated 200.15.10.0 /24

Engineering Department:

Already has 200.15.10.0 to 200.15.10.64

New York Sales Department:

+-----------+-------------+-------------+--------------+-------------+
| De        | Network     | Broadcast   | Subnet mask: | Valid host: |
| partment: | address:    |             |              |             |
+===========+=============+=============+==============+=============+
| En        | 200.15.10.0 |             |              |             |
| gineering | to          |             |              |             |
|           |             |             |              |             |
|           | 2           |             |              |             |
|           | 00.15.10.63 |             |              |             |
+-----------+-------------+-------------+--------------+-------------+
| New York  | 2           | 2           | 255          | 2           |
| Sales     | 00.15.10.64 | 00.15.10.79 | .255.255.240 | 00.15.10.65 |
|           | to          |             |              | to          |
|           |             | One less    | /28 = 14     | 2           |
|           | 2           | than the    | hosts        | 00.15.10.78 |
|           | 00.15.20.80 | network     |              |             |
|           |             | address.    |              |             |
+-----------+-------------+-------------+--------------+-------------+
| Boston    | 2           | 2           | 255          | 2           |
| Sales     | 00.15.10.81 | 00.15.10.88 | .255.255.248 | 00.15.10.82 |
|           | to          |             |              | to          |
|           |             |             | /29 = wrong  |             |
|           | 2           |             |              | 2           |
|           | 00.15.10.89 |             |              | 00.15.10.87 |
+-----------+-------------+-------------+--------------+-------------+

7 hosts

Subnet = /29 forgot to subtract the 2 in the calculation.

What I've done though with the subnet mask of 29 is correct though, for
the network address, broadcast and valid host. So, some improvement?

# Spanning tree Protocol: (STP)

Is a network protocol designed to prevent broadcast loops in ethernet
networks that have multiple interconnected switches. These loops can
lead to network congestion and failure due to the continuous circulation
of broadcast packets.

## How STP works: 

**Loop prevent:**

STP Identifies redundant paths within the network and places some of
these connections into a *Blocking state* to prevent loops. It
dynamically recalculates paths when there is a change in the network
topology (e.g., a link failure), enabling traffic to reroute through an
alternative path when needed.

**Root bridge selection:**

STP elects a *root bridge* (the central switch) to serve as the
reference point for all path calculations. All other switches find the
shortest path to the root bridge.

### Port states: 

**Blocking** -- the port does not forward frames and only listens for
BPDU (Bridge protocol data unit) frames to prevent loops.

**Listening** -- the port listens for BODU to determine if it should
move to the forwarding state.

**Learning** -- the port learns MAC addresses but does not forward
frames yet,

**Forwarding** -- The port forwards frames and processes incoming data.

**Disabled** -- the port is administratively shut down.

  -----------------------------------------------------------------------
  **State:**        **Forward         **Learn MAC       **Duration:**
                    Frames:**         addresses:**      
  ----------------- ----------------- ----------------- -----------------
  Blocking          No                No                20 seconds

  Listening         No                No                15 seconds

  Learning          No                Yes               15 seconds

  Forwarding        Yes               Yes               \-
  -----------------------------------------------------------------------

### Clarification on my points: 

ARP Broadcasts:

While ARP broadcast is used to find MAC addresses for a known IP
address, broadcast storms and loops are a broader issue. They occur when
any broadcast frame (not just ARP) loops indefinitely due to redundant
paths in the network.

Role of STP:

STP Doesn't simply turn interfaces on and off but calculates which ports
need to be in a ***blocking state*** to break the loops. It selectively
places interfaces in blocking or forwarding states based on the
network's topology and BDPUs exchanged between the switches.

### Example of Broadcast Loops: 

In a network with multiple interconnected switches forming a loop, a
broadcast packet sent from one device could be replicated across all
connected switches endlessly.\
\
![A diagram of a computer network Description automatically
generated](media/image1.png){width="6.268055555555556in"
height="4.352083333333334in"}

This replication creates a broadcast storm that consumes bandwidth and
CPU resources, ultimately leading to network failure. STP stops this by
blocking redundant paths.

<https://www.youtube.com/watch?v=6MW5P6Ci7lw>

# Line Types

  -----------------------------------------------------------------------
  Line Type:              Description             Command
  ----------------------- ----------------------- -----------------------
  Console                 Physical port that      Line con 0
                          provides the initial    
                          CLI access; used for    
                          troubleshooting when    
                          remote access to the    
                          IOS device isn't        
                          functioning; only one   
                          is supported on a       
                          device. (console port)  

  Auxiliary               Backup physical port    Line aux 0
                          typically used for      
                          dialup into the IOS     
                          device; not all devices 
                          have an auxiliary port  
                          and only one is         
                          supported per device.   

  Visual Type Terminal    Logical port that       Line vty 0 4
  (VTY)                   allows for remote       
                          access connection such  
                          as telnet and SSH to    
                          gain access to the CLI; 
                          many VTYs are supported 
                          on an ISO device, and   
                          the number is dependent 
                          on t he device, model,  
                          and software version.   

  Teletype Terminal (TTY) Physical port used for  Line tty 0 31
                          connecting to a modem   
                          for a terminal service  
                          or for access to the    
                          console ports of other  
                          devices. These ports    
                          are found only on       
                          routers and the number  
                          supported depends on    
                          the router model.       
  -----------------------------------------------------------------------

# Introduction IPv4:

Characteristics of IPv4 --

-   Operates at network layer (layer 3)

-   32-bit long and consists of 2 parts.

    -   Network part and the host part

    -   192.168.1.10 /24

    -   Network portion/host/network mask.

    -   Network mask determines the network portion of the IP address.

-   IPv4 is decimal based

Maximum hosts per network = 2^n^-2

(n = the number of host bits)

To find the network portion, remove the -2.

192.168.1.10 /24 = as there is 8 spare bits 2^8^ = 256

The /24 of the IP address is the subnet mask which represents 24 bits
out of 32-bit long IP address (IPv4) the 192.168.1 is our network
portion. As each octet (192) (168) (1) represents 8 bits each. Three
octets added together equals 24.

# IP Packet Diagram: 

+--------+-----------+---+---------+------+--------+--------------------+---+
| V      | Header    | T |         |      | Packet |                    |   |
| ersion | length    | y |         |      | Length |                    |   |
|        | (IHL)     | p |         |      |        |                    |   |
|        |           | e |         |      |        |                    |   |
|        |           | o |         |      |        |                    |   |
|        |           | f |         |      |        |                    |   |
|        |           | s |         |      |        |                    |   |
|        |           | e |         |      |        |                    |   |
|        |           | r |         |      |        |                    |   |
|        |           | v |         |      |        |                    |   |
|        |           | i |         |      |        |                    |   |
|        |           | c |         |      |        |                    |   |
|        |           | e |         |      |        |                    |   |
|        |           |   |         |      |        |                    |   |
|        |           | ( |         |      |        |                    |   |
|        |           | T |         |      |        |                    |   |
|        |           | O |         |      |        |                    |   |
|        |           | S |         |      |        |                    |   |
|        |           | ) |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| Id     |           |   |         |      | Flags  | Fragment offset    |   |
| entifi |           |   |         |      |        |                    |   |
| cation |           |   |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| Time   |           |   | P       |      | Header |                    |   |
| to     |           |   | rotocol |      | ch     |                    |   |
| live   |           |   |         |      | ecksum |                    |   |
| (TTL)  |           |   |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| Source |           |   |         |      |        |                    |   |
| a      |           |   |         |      |        |                    |   |
| ddress |           |   |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| Desti  |           |   |         |      |        |                    |   |
| nation |           |   |         |      |        |                    |   |
| a      |           |   |         |      |        |                    |   |
| ddress |           |   |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| O      |           |   |         | Pad  |        |                    |   |
| ptions |           |   |         | ding |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+
| Data   |           |   |         |      |        |                    |   |
+--------+-----------+---+---------+------+--------+--------------------+---+

# OSI Model:

  -------------------------------------------------------------------------
  OSI Model:      TCP/IP:         Protocol:        Hardware:       Num:
  --------------- --------------- ---------------- --------------- --------
  Application     Application                                      7

  Presentation    Application                                      6

  Session         Application                                      5

  Transport       internet        TCP/UDP                          4

  Network         Network         IP addresses     Routers         3

  Data Link       Network Access  Mac Addresses    Switches        2

  Physical        Network Access  Cables/NIC                       1
  -------------------------------------------------------------------------

# Practical Knowledge:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image2.png){width="5.208333333333333in"
height="5.625in"}

# LANs:

LANs = Local Area Network

The dominant protocol we use In LANs is "Ethernet" which is governed by
the IEEE (Institute of Electrical and Electronics Engineers).

IEEE are an institution who describe protocols, cabling, connectors,
etc.

## SOHO LAN: (Small Office Home Office) 

This "type" of LAN is something we should all be familiar with, as it's
the most common amongst them. These a small group of devices, in its
simplest form 2 computers and a switch.

This will allow the two computers to communicate to each other and share
folders + printing etc.

## Enterprise LAN: 

# IEEE standards: 

  --------------------------------------------------------------------------
  Bandwidth:     Common Name:   Informal Name: IEEE Name:     Cable Type:
  -------------- -------------- -------------- -------------- --------------
  10 Mbps        Ethernet       10BASE-T       802.3          UTP 100m

  100 Mbps       Fast Ethernet  100BASE-T      802.3u         UTP 100m

  1000 Mbps      Gigabit        1000BASE-LX    802.3z         Fiber 5000m
                 Ethernet                                     

  1000Mbps       Gigabit        1000BASE-T     802.3ab        UTP 100m
                 Ethernet                                     

  10 Gbps        10 Gigabit     10GBASE-T      802.3an        UTP 100m
                 Ethernet                                     
  --------------------------------------------------------------------------

# Firewalls: 

There three types of Firewalls:

1.  Firewalls

2.  Circuit-level Firewall

3.  Application layer firewall, aka proxy servers/reverse proxy servers.

<https://www.youtube.com/watch?v=FhLC11J8K1o>

# Collision Domain:

Collision domains are too many packets being sent at the time, causing a
collision.

Think of car traffic moving from a 2-lane road into a single road, the
bottle neck can cause a car crash (collision). Similarly, to road
traffic it causes a jam; this jam causes slowdowns, affecting overall
performance.

Modern switches and full duplex resolve this issue. Bit like building
more roads or overpasses to prevent this issue from happening.

![A diagram of a computer software Description automatically
generated](media/image3.png){width="6.268055555555556in"
height="2.9006944444444445in"}

Before modern switches and having cables, which can do full duplex. Half
duplex was used, meaning network equipment could not send and receive at
the same time. Bit like traffic lights on a two-way single lane allowing
traffic to flow one way, whilst the other lane pauses.

This doesn't mean collisions still didn't happen. Just like in the car
analogy, computers can decide the "line (lane) is free" causing a
collision.

This issue was resolved using a protocol called CSMA/CD:

-   CS = Carrier sense

-   MA = Multi Access

-   CD = Collision Detection

Carrier sense means each device listens to the network to check if it's
clear before transmitting.

Multi access means multiple devices share the same transmission medium.
(Multiple devices connected to the same \*hub\*)

Collision detection means devices detect if a collision has occurred and
takes steps to retransmit after a random back-off time.

Need to preference this with it being old technology, today we don't
worry about collisions. However, when we did, it was because we used a
network equipment called a "Hub" which is a repeater.

What this means, is any electrical signal being sent to the hub, for
example, an email. Would be sent to hub and replicated across all
interfaces apart from the one it was received on.

# Campus Network (Three-Layer): 

## Core layer: 

Role: High-speed backbone of the network, ensuring efficient data
transfer between distribution layers.

### Advantages:

Provides high-speed switching and low latency for data transport.

Ensures network availability by routing traffic quickly across the
network.

## Distribution Layer: 

Role: Aggregates data from the access layer and forwards it to the core
layer. It also enforces policies, such as filtering, routing, etc.

### Advantages: 

Enhances network scalability by managing traffic flows and polices.

Offers redundancy and load balancing for reliability.

## Access Layer:

Role: Connects end-user devices like computers, printers, and IP phones
to the network.

Advantage: Provides many ports and easy access for users.

# Spine and Leaf Architecture: 

vPC = Virtual port channel

We use vPC instead of spanning tree protocol (STP) in this type of
topology due to the limitations of STP. These limitations are the
inability to utilise all the physical connected lines between the
switches.

A data centre where you will most likely see Spine and Leaf architecture
being used, a vPC allows the network to utilise all its connected
interfaces.

![A diagram of a network Description automatically
generated](media/image4.png){width="4.198502843394576in"
height="2.0315332458442694in"}

Can be a layer 2 or layer 3. If it's a layer 2 design, we don't use
spanning tree protocol. We use transparent interconnection of lost of
links or TRILL for short. This allows all links to be used
simultaneously.

## Advantages: 

-   Improved redundancy

-   Increased bandwidth

-   Improved scalability

-   Lower cost

-   Lower latency and delay

-   Power consumption

## Disadvantages: 

-   Cabling requirement

-   Limited number of hosts -- By which we mean the spine switch can
    only connect to 48 leaves (hosts) if it's a 48 a port switch.

# DHCP: 

# Software Defined Networking (SDN)

To understand SDN we need to look at traditional networking and the
issues SDN was designed to resolve.

Traditional networking is your networking equipment. Router, switches,
and firewalls. It has been like this for many years. Companies like
Cisco, Palo Alto, Juniper and Ubiquiti sell these devices and are often
proprietary.

Meaning, they are enclosed within their own ecosystem. Think of Apple
and their products, or if you have experience with Ubiquiti; the network
management system (NMS) they have built is fantastic with their own
products, however, plug in any other networking equipment and you don't
know what you have apart from the MAC address.

As for Cisco, they use software (GUI) products like CCP (Cisco
Configuration Protocol) for routers or ASDM for the Cisco ASA firewalls.

To take another step deeper, a router has different functions that it
must perform to forward a packet. For example:

-   Check the destination IP address within it's routing table to figure
    out where to forward the IP packet to.

-   It has routing protocols like OSPF, EIGRP or BGP to learn networks
    which are installed in the routing table.

-   Address resolution protocol (ARP) to figure out MAC address of the
    next hop or destination and change the destination MAC address in
    the ethernet frame.

-   Time to live in the IP Packet must be decreased by 1 and the IP
    header \[checksum\] must be recalculated,

These different tasks are separated into three different planes:

1.  **Control plane**

2.  **Data plane**

3.  **Management plane**

# Lab:

Here\'s a set of networking labs for CCNA practice, progressing from
easy to hard:

## Beginner Labs

1.  **Basic Router Configuration**

    -   Set up hostname, passwords, and basic security settings on a
        Cisco router.

    -   Configure an IP address on an interface and enable it.

    -   Test connectivity between two routers using static routes.

2.  **Basic Switch Configuration**

    -   Set up the switch hostname, passwords, and enable port security.

    -   Configure VLANs and assign switch ports to specific VLANs.

    -   Verify VLAN configuration and test inter-VLAN communication
        using a router-on-a-stick setup.

> <https://networklessons.com/ip-routing/how-to-configure-router-on-a-stick>

Note: the reason why it wasn't working, was because I was setting the Ip
addresses of the computers to the VLAN interface and not the computers.\
\
Corrected issue and set the default gateway to the IP address set to the
sub interfaces of the router.

The port connected to the router is put into trunk mode by enabling the
port to be in encapsulated in dot1q. Using this command:\
\
conf t

Inteface \-\-\--

Switchport trunk encapsulation dot1q

Switchport mode trunk

No shutdown

Additional command to learn if the trunk is working:\
\
show interface \-\-\-\-- trunk

3.  **Subnetting Practice**

    -   Create subnetting schemes for given IP address spaces.

    -   Assign subnets to different interfaces and test connectivity
        between hosts in different subnets.

![A computer diagram with text and numbers Description automatically
generated with medium
confidence](media/image5.png){width="6.268055555555556in"
height="3.8243055555555556in"}

Keep a track of the interfaces and Ip addresses. Script for this lab is
in the notes.

UPDATE: 27/02/2025

This lab is asking for a router on a stick. You will find the notes in
the Network Lessons -- notes folder in the One Drive.

Also known as Inter-VLAN communication.

## Intermediate Labs

4.  **Routing Protocols (RIP, OSPF)**

    -   Configure RIP version 2 on multiple routers and test route
        propagation.

![A diagram of a computer Description automatically
generated](media/image6.png){width="6.268055555555556in"
height="2.673611111111111in"}

Note: Issue I had here was not configuring the interfaces with the IP
addresses. Being lazy and blindly following. Otherwise very simple to
set up. This one was done through:

<https://networklessons.com/rip/rip-default-route>

-   Set up single-area OSPF and understand OSPF neighbour relationships.

-   Modify OSPF priority to influence designated router elections.

![A computer screen shot of a network Description automatically
generated](media/image7.png){width="6.268055555555556in"
height="7.784027777777778in"}

![A diagram of a diagram Description automatically generated with medium
confidence](media/image8.png){width="6.268055555555556in"
height="7.454166666666667in"}

5.  **DHCP Configuration**

    -   Configure a router to act as a DHCP server for different
        subnets.

    -   Set up DHCP relay agents and test IP address allocation across
        subnets.

6.  **Access Control Lists (ACLs)**

    -   Create and apply standard and extended ACLs to control traffic
        between different network segments.

    -   Test traffic filtering with pings and TCP connections to verify
        ACL behaviour.

## Advanced Labs

7.  **Inter-VLAN Routing with Layer 3 Switch**

    -   Configure and verify inter-VLAN routing on a Layer 3 switch.

    -   Implement routing using SVI (Switched Virtual Interfaces).

8.  **Advanced OSPF (Multi-area OSPF)**

    -   Configure and verify multi-area OSPF with multiple routers.

    -   Understand LSA types and how OSPF converges across areas.

9.  **EIGRP Configuration**

    -   Set up and optimize EIGRP with manual and automatic
        summarization.

    -   Test failover scenarios by manipulating route metrics and
        bandwidth.

10. **NAT (Network Address Translation)**

    -   Configure static, dynamic, and PAT (Port Address Translation) on
        a router.

    -   Test NAT configuration with external traffic simulation.

11. **WAN Technologies**

    -   Set up and test PPP with CHAP authentication.

    -   Configure GRE tunnels between routers and verify connectivity.

12. **BGP (Border Gateway Protocol) Basics**

    -   Set up a simple BGP configuration between two routers.

    -   Introduce basic BGP attributes and test route advertisements.

These labs will give you a comprehensive practice experience, covering
key CCNA topics and preparing you for real-world network scenarios

# PVST -- Per Vlan spanning tree: 

Designated roots.

Blocked ports.

<https://networklessons.com/cisco/ccna-200-301/per-vlan-spanning-tree-pvst>

![A diagram of a network Description automatically
generated](media/image9.png){width="6.268055555555556in"
height="4.819444444444445in"}

# Virtual local area network (VLAN): 

# Network addressing and Basic Troubleshooting

**Purpose of the Physical Layer:**

Whenever the physical layer is mentioned, we are referring to a couple
of things. The OSI model and the physical connection (wired connection)
between device to device.

Before any network communication can occur, a physical connection must
be established.

This also includes wireless connections. A different type of physical
connection but still bound to the rule of needing a "connection" before
network communication can occur. In wireless this means electromagnetic
waves (Radio Frequency).

**How do we connect?**

Many devices use a computer component called a Network Interface
Controller (NIC).

![A close-up of a computer chip AI-generated content may be
incorrect.](media/image10.jpeg){width="6.268055555555556in"
height="3.5229166666666667in"}

This is what it looks like, outside of the computer. However, there are
other variants such as:

![A diagram of different types of electronic devices AI-generated
content may be
incorrect.](media/image11.png){width="6.268055555555556in"
height="3.5256944444444445in"}

![A hand holding a cable to a computer AI-generated content may be
incorrect.](media/image12.jpeg){width="6.268055555555556in"
height="4.1722222222222225in"}

The physical layer provides the means to transport bits over the network
whether the network is wired or wireless.

# Ethernet

Ethernet is a collection of network protocols and standards.

Ethernet Standards: (copper)

  -----------------------------------------------------------------------
  Speed:        Common Name:     IEEE         Informal      Maximum
                                 Standard:    Name:         Length:
  ------------- ---------------- ------------ ------------- -------------
  10 Mbps       Ethernet         802.3i       10BASE-T      100 m

  100 Mbps      Fast Ethernet    802.3u       100BASE-T     100 m

  1 Gbps        Gigabit Ethernet 802.3ab      1000BASE-T    100 m

  10 Gbps       10 Gig Ethernet  802.3an      10GBASE-T     100 m
  -----------------------------------------------------------------------

UTP = Unshielded Twisted Pair

![Close-up of several wires AI-generated content may be
incorrect.](media/image13.jpeg){width="3.129861111111111in"
height="2.467361111111111in"}

The most common type of cables used in networking. The twisted cables
help protect against electromagnetic interference (EMI).

**Straight-through cable**

![A screenshot of a computer AI-generated content may be
incorrect.](media/image14.png){width="6.268055555555556in"
height="1.7055555555555555in"}

Here you can see the diagram above, highlighting two pairs of the cables
found inside of a UTP.

The 1^st^ pair, 1 and 2 are used by the PC to transmit data and the
switch receives the data on the same pair.

The 2^nd^ pair, 3 and 6 are used by the switch to send data to the PC.

This means that the cable is a full-duplex cable. Meaning both devices
can transmit and receive data at the simultaneous, so no collisions will
occur.

![A black screen with white text AI-generated content may be
incorrect.](media/image15.png){width="6.268055555555556in"
height="1.49375in"}

This is the same grouping between a router and switch. As both devices
are receiving and transmitting on opposite pairs, so no collisions
should occur.

What happens between a router and router?

![A screen shot of a computer AI-generated content may be
incorrect.](media/image16.png){width="6.268055555555556in"
height="1.488888888888889in"}

It doesn't work. As the router is only set to transmit data on pins 1 &
2 not receive them.

This applies to two switches as well. For example:

![A screen shot of a computer AI-generated content may be
incorrect.](media/image17.png){width="6.268055555555556in"
height="1.4722222222222223in"}

To solve this issue, we have another cable called a cross-over cable.
Here:

![A diagram of a network AI-generated content may be
incorrect.](media/image18.png){width="6.268055555555556in"
height="1.4777777777777779in"}

Notice the difference between crossover and straight through?

  -----------------------------------------------------------------------
  Device type:        Transmit (Tx) Pins:      Receive (Rx) Pins:
  ------------------- ------------------------ --------------------------
  Router              1 and 2                  3 and 6

  Firewall            1 and 2                  3 and 6

  PC                  1 and 2                  3 and 6

  Switch              3 and 6                  1 and 2
  -----------------------------------------------------------------------

Overall, these issues are not a common occurrence in modern networks as
network devices uses a feature called Auto-MDIX which will detect which
pins are being used for what and will appropriately switch the pins
accordingly.

Within the 1000BASE-T and 10GBASE-T, the gigabits per second speed
cables are **bidirectional** pairs. Meaning each pair can be either a
transmit or receive, why these are so much faster than the previous
examples.\
\
![A screen shot of a black screen AI-generated content may be
incorrect.](media/image19.png){width="6.268055555555556in"
height="2.2083333333333335in"}

Fibre-Optic Cable Standards

  -----------------------------------------------------------------------
  Speed:        Cable type:      IEEE         Informal      Maximum
                                 Standard:    Name:         Length:
  ------------- ---------------- ------------ ------------- -------------
  1 Gbps        Ethernet         802.3i       10BASE-T      100 m

  100 Mbps      Fast Ethernet    802.3u       100BASE-T     100 m

  1 Gbps        Gigabit Ethernet 802.3ab      1000BASE-T    100 m

  10 Gbps       10 Gig Ethernet  802.3an      10GBASE-T     100 m
  -----------------------------------------------------------------------

# Protocols: 

Networking models categorise and provide a structure for networking
protocols and standards.

A Networking protocol is a set of rules defining how network devices and
software should work.

Protocols are a set of Logical rules, on how to communicate. Not
physical.

# CLI password: 

In global configuration mode, you can use this command:

service password-encryption

This will encrypt the password we set to deny/allow users to get into
the CLI on a switch/router.

However not the most secure encryption algorithm, as you can search for
a password cracking tool to undo this.

To help circumvent this we can use another command:

Enable secret ....

Instead of the:

Enable password

Command, as this will give us a level 5 secure encryption (MD5) which is
more secure than the level 7 "service password-encryption".

To check this, we do can look at the "show run" command to see if the
password is in plain text or encrypted with different numbers and
letters.

"do" is a shorthand command which allows us to execute commands at conf
t level instead of needing to repeatedly exit/end to privilege (#) mode
to do the commands.

What happens when you use the enable service password-encryption?

When the command is entered, it will encrypt all current passwords and
future passwords. The "enable secret" command will not be affected as it
is its own separate thing.

When disabling the "service password-encryption" with "no service
password-encryption" the current passwords will not be decrypted but
future passwords will not be encrypted. Same again for the "enable
secret" command, it will not be changed.

However, we try and avoid using this command as it's the least secure.

# CTRL + SHIFT 6 to cancel current command

# MAC Address = 24 bits

The mac address is represented like AA:BB:CC:00:11:22 or AABB.CC00.1122
the first half is the OUI (AABB.CC). A unique number which is set by the
manufacturer. This is sometimes called the Burn in Address (BIA).

OUI = Organisational Unique Identifier

Payload of a packet is 46 bytes in length and is padded out when the
frame is less than that.

# Binary Numbering table

![A table of numbers with numbers AI-generated content may be
incorrect.](media/image20.png){width="4.170138888888889in"
height="4.51875in"}

# Packet Information on a Switch interface: 

![A screenshot of a computer AI-generated content may be
incorrect.](media/image21.png){width="6.268055555555556in"
height="4.561111111111111in"}

Highlighted in red, we can see packet information being received on the
switch 1 interface (fa0/3).

**Frame Size Limits:**

64 bytes -- Minimum frame size

1518 bytes - Maximum frame size

**Error types & Frame Issues:**

Runts = Frames smaller than 64 bytes (often due to collisions or
errors).

> Giants = Frames larger than 1518 bytes (can be caused by
> misconfiguration or jumbo frames without support).
>
> Throttle = frames which are intentionally dropped due to: Network
> congestion, Flow Control, Rate limiting, Overloaded network
> interfaces.

**CRC & Frame check Sequence (FCS):**

CRC (Cyclical Redundancy Check) detects transmission errors.

> The sender calculates a CRC number on the frame's data and attaches it
> to the frame as an FCS (frame check sequence).
>
> When the switch (or receiving device) gets the frame, it recalculates
> the CRC:
>
> If it matches the FCS, the frame is assumed to be error-free and
> processed.
>
> If it doesn't match, the frame is corrupted and discarded.

Think of this process a red light/green light system:

Green light (Go): If the received frame's CRC matches the expected
value.

Red Light (Stop): If it doesn't match, meaning data Is corrupt.

**Other Frame Errors:**

Frame = Frames which have incorrect format (due to an error)

> Input errors = Total count of the various incoming frame issues (e.g.,
> CRC errors, runts, giants).

Output errors = Frames the switch attempted to send but failed due to an
error.

# Routing Fundamentals: 

**What is routing?**

Routing is the process that routers use to determine the path that IP
packets should take over a network to reach their destination.

Routers store routes to all their known destinations in a routing table.

> For example, switches keep a mac-address table. Routers keep a routing
> table.
>
> When routers receive packets, they look in the routing table to find
> the best route to forward the packet.

There are three main routing methods (methods that router user to learn
routes):

> Dynamic routing: Routers use dynamic routing protocols such as OSPF,
> to share information with each other automatically and build their
> routing tables.
>
> Static routing: A route which has been manually set by a network
> engineer.
>
> Third option: Directly connected to the router.

**What is a route?**

A route is an instruction that tells a router where to send a packet to
reach its destination.

> It defines the next hop (next router or device) or the exit interface
> the packet should take.

For example:

192.168.1.0/24 via 10.0.0.1

This means:

Any packet for 192.168.1.x should be sent to the next hop 10.0.0.1

## Example **Static route:** 

To configure a static route on a Cisco router:

Go to global configuration mode -

Ip route 0.0.0.0 0.0.0.0 10.0.0.1

**What does this mean?**

1.  0.0.0.0 = Matches any destination (default route)

10.0.0.1 = The next hop (where the router sends packets if no other
specific route exists).

This is commonly used in network with firewalls, internet gateways, or
edge routers, where all unspecified traffic is forwarded to a specific
exit point (e.g., the internet or another network segment).

**Analogy**

Think of routing like a motorway junction:

> If it has a specific route (e.g., a static or dynamic router to a
> known network), it will send traffic down that road.
>
> If it doesn't have a specific route, it follows the default route
> (0.0.0.0 0.0.0.0)- like a slip road leading all unknown traffic to
> 10.0.0.1 (which could be a firewall, ISP router, or gateway to another
> network).

It's like saying "all traffic, use this road" unless another road is
clearly marked.

# Life a Packet:

How a packet travels from a pc to a remote pc.

The layer 3 headers stay the same in the frame: Source and Destination
IP addresses

The layer 2 headers changes when it reaches each hop. For example, PC 1
sends a packet to PC4:

Source IP address is its own and destination is where it wants to
reach.\
\
To send it outside its own network (LAN) it needs to learn the mac
address of the device which will be forwarding it to remote site. This
is the Router's internal interface.

It does an ARP request, which asks for the MAC address from the router.
A switch will simply flood it out all interfaces apart from the one it
was received on.

The switch updates its own MAC address table with PC1s and once it
receives an ARP reply from the router it passes it back to the PC (1)
and updates it MAC address with the routers internal interface as well.

The PC updates it ARP table and changes the destination MAC address to
the Routers and passes the packet on to it.

The layer 2 process between the PC and the Router within the Network
(LAN) happens at hop, once the packet leaves the LAN and enters WAN
(Router to Router).

Best way to think about this is the life a letter being posted and the
process you must do to get the right address and then trust the
postmen/postal service to send it to where you need it to.

# Subnetting-2:

+-----+----------+------------+-------------+---------+--------------+
| Cl  | First    | Prefix     | Dotted      | Num     | Addresses    |
| ass | Octet    | Length     | Decimal     | N       | per network  |
|     | range    |            |             | etworks |              |
+=====+==========+============+=============+=========+==============+
| A   | 0-127    | /8         | 255.0.0.0   | 128     | 16,777,216   |
|     |          |            |             | (2^7^)  | (2^24^)      |
+-----+----------+------------+-------------+---------+--------------+
| B   | 128-191  | /16        | 255.255.0.0 | 16,384  | 65,536       |
|     |          |            |             | (2^14^) | (2^16^)      |
+-----+----------+------------+-------------+---------+--------------+
| C   | 192-223  | /24        | 25          | 2,      | 256 (2^8^)   |
|     |          |            | 5.255.255.0 | 097,152 |              |
|     |          |            |             |         |              |
|     |          |            |             | (2^21^) |              |
+-----+----------+------------+-------------+---------+--------------+
| D   | 224-239  | Broadcast  |             |         |              |
+-----+----------+------------+-------------+---------+--------------+
| E   | 240-255  | Ex         |             |         |              |
|     |          | perimental |             |         |              |
+-----+----------+------------+-------------+---------+--------------+

## Binary Table: 

  ------------------------------------------------------------------------
  128       64       32       16       8        4        2        1
  --------- -------- -------- -------- -------- -------- -------- --------
                                                                  

  ------------------------------------------------------------------------

## Class C CIDR: /24

  ------------------------------------------------------------------------
  Dotted Decimal:   CIDR          Usable        Block Size        subnet
                    Notation:     addresses                       
  ----------------- ------------- ------------- ----------------- --------
  255.255.255.128   /25           2^7^ - 2 =    256 -- 128 = 128  2
                                  126                             

  255.255.255.192   /26           2^6^ -- 2 =   256 -- 192 = 64   4
                                  62                              

  255.255.255.224   /27           2^5^ -- 2 =   256 -- 224 = 32   8
                                  30                              

  255.255.255.240   /28           2^4^ -- 2 =   256 -- 240 = 16   16
                                  14                              

  255.255.255.248   /29           2^3^ -- 2 = 6 256 -- 248 = 8    32

  255.255.255.252   /30           2^2^ -- 2 = 2 256 -- 252 = 4    64

  255.255.255.254   /31           2^1^ -- 2 = 0 256 -- 254 = 2    128

  255.255.255.255   /32           2^0^ -- 2 =   256 -- 255 = 1    256
                                  -1                              
  ------------------------------------------------------------------------

## Example 1:

<https://www.youtube.com/watch?v=bQ8sdpGQu8c&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=26>

It was this video from Jeremy's IT lab YouTube which gives us the task.

The answer is:

  ------------------------------------------------------------------------
  Network Address:   Broadcast:        First usable:     Last usable:
  ------------------ ----------------- ----------------- -----------------
  192.168.1.0/26     192.168.1.63      192.168.1.1       192.168.1.62

  192.168.1.64/26    192.168.1.127     192.168.1.65      192.168.1.126

  192.168.1.128/26   192.168.1.191     192.168.1.129     192.168.1.190

  192.168.1.192/26   192.168.1.255     192.168.1.193     192.168.1.254
  ------------------------------------------------------------------------

## Example 2:

Second Question:

162.168.255.0/24 split into 5 subnets

we have 8 spare bits to play with. We need to split this into 5 subnets.

a /25 will give us 126 usable addresses with 128 networks. Too many. Is
this right?

A /26 like we did before gave us 4 subnets with 64 usable addresses.

let\'s rethink this. 8 spare bits. How many subnets does each one give
us.

2 to the power of 1 = 2

4

8

16

32

etc

In between 4 and 8. Seeing we need 5, 8 is the closest. Which is 2 to
the power of 3. We borrowed 3 bits. Add 3 bits to /24 = /27 with 6
usable addresses in each subnet.

usable addresses is wrong, we are just calculating the subnets. We do
the usable addresses after.

So, we know we need /27 which leaves 5 spare bits. 2 to the power of 5 -
2 = 30 usable addresses in each subnet.

  --------------------------------------------------------------------------------
  Net   Network Address:     Broadcast:        First usable:     Last usable:
  ----- -------------------- ----------------- ----------------- -----------------
  1     192.168.255.0/27     192.168.255.31    192.168.255.1     192.168.255.30

  2     192.168.255.32/27    192.168.255.63    192.168.255.33    192.168.255.62

  3     192.168.255.64/27    192.168.255.95    192.168.255.65    192.168.255.94

  4     192.168.255.96/27    192.168.255.127   192.168.255.97    192.168.255.126

  5     192.168.255.128/27   192.168.255.59    192.168.255.129   192.168.255.158
  --------------------------------------------------------------------------------

Spare networks & address:

  --------------------------------------------------------------------------------
  Net   Network Address:     Broadcast:        First usable:     Last usable:
  ----- -------------------- ----------------- ----------------- -----------------
  6     192.168.255.160/27   192.168.255.191   192.168.255.161   192.168.255.190

  7     192.168.255.192/27   192.168.255.223   192.168.255.193   192.168.255.222

  8     192.168.255.224/27   192.168.255.255   192.168.255.225   192.168.255.254
  --------------------------------------------------------------------------------

## Class B:

172.16.0.0 /16

You have been given the network above. You are asked to create 80
subnets for your company's various LANs. What prefix length should you
use?

A /16 gives me 16 spare bits to use.

The company wants 80 subnets.

To find how many subnets we must use this formula:

2^x^ = 2^16^ =

Off the top of my head, 2^10^ = 1024 times that by 2 6 more times

2048

4096

8192

16384

32768

65536 = How many subnets we have currently.

We need to borrow enough spare bits then to reduce it down to roughly
80.

2^6^ = 64

2^7^ = 128 /our closest to the 80 subnets. So, we need to borrow 7 bits.

172.16.0.0/23

Second Question:

You have been given the 172.22.0.0 /16 network. You are required to
divide the network into 500 separate subnets. What prefix length should
you use?

Based on the previous answer with 7 bits borrowed, I know we need to
borrow 9.

172.22.0.0/25

255.255.255.128 which leaves 254 host addresses?

10101100.0001100.00000000.00000000

Q3:

What subnet does host 172.25.217.192/21 belong to?\
\
11011001

256-217 = 39

172.25.0.0 /21

172.25.39.0 -

127.25.78.0 -

172.25.117.0 -

172.25.156.0 -

172.25.195.0 -

172.25.234.0 --

WRONG! Find the block size by converting the /21 into binary! In the
third octet = 248

256 -- 248 = 8

172.25.200.0/21

172.25.208.0/21

172.25.216.0/21

172.25.224.0/21

Answer is 172.25.216.0/21

## Class A:

You have been given the 10.0.0.0/8 network. You must create 2000 subnets
which will be distributed to various enterprises.

What prefix length must you use?

How many host addresses (usable addresses) will be in each subnet?

10.0.0.0/8 gives us 24 spare bits to play with.

From the 24 we need work out how many subnets we need make to create
2000.

The formula to do this is 2^x^

2^10^ =1024

2^11^ = 2048

So, we need to borrow 11 bits which equals to 10.0.0.0/19

Now we can work out how many host addresses this will give us.

Which is 2^13^ as we have 13 bits left over, -2.

We know that 2^11^ is 2048, next in line is 4096 (2^12^) next number is
8192 (2^13^) -- 2 = 8190 usable addresses.

Answer is:

10.0.0.0/19

8190 addresses.

Correct

PC1 has an IP address of 10.217.182.223/11

Identify the following the PC1's subnet:

1\) Network address:

2\) Broadcast address:

3\) First usable address:

4\) Last usable address:

5\) Number of host (usable) addresses:

10.217.182.223/11

So, we have a subnet of /11 so we know the first octet stays the same
with the 2^nd^ octet being the split point.

255.11011001.

So its 255.110 000..... = 10.192.0.0 /11

Now we know that we can find the block size. 256 -- 192 = 64

Network Address is 10.192.0.0 /11 correct

Broadcast address is = 10.255.254.254 wrong

First usable Address = 10.192.0.1 wrong

Last usable Address = 10.255.254.253 /11 wrong\
Number of hosts equates to 2^21^ -2 = 2,097,150 correct

To work this out properly:

We got the network address right with 10.192.0.0 /11

We worked this out by converting the ip address to a binary address and
finding the split which equates to 1111 1111.110 using the rule of
turning all bits to 0 apart from the ones which fall in the /11 range.

256 -- 192 = 64 as our block size

But adding 64 to 192 makes the block size push into the next octet/bit

1111 1111.110 \-\-\-\-\--

So, we flip the 0 in the /11 to 1

1111 111.111 \-\-\-- = 10.224 as we added 1 bit 192+32 = 224

Making the block size 256 -224 = 32

Note:

It's a class A network, meaning that we already borrowed 3 bits to make
/11 which equates to 2^3^ = 8 subnets. The block is 32 as 8x32 = 256

The first subnet with /11 is 10.0.0.0 /11

Then 10.32.0.0/11

And so on.

You\'re very close! Your explanation is solid, but I see a couple of
things that might need slight clarification. Here\'s a cleaned-up and
slightly refined version of your breakdown:

**Step-by-Step Explanation**

We need to determine the subnet for **10.217.182.223/11**

1.  **Find the network address:**

    -   **/11** means the first **11 bits** are the network portion.

    -   The first octet (10) remains the same.

    -   The second octet (217 in decimal) needs to be analysed in
        binary.

**Convert to binary:**

-   **217 (decimal) = 1101 1001 (binary)**

-   **/11** means the first **3 bits** of the second octet belong to the
    network.

-   Keeping only the first **3 bits** of the second octet and setting
    the remaining bits to **0**, we get:

    -   **1100 0000 (192 in decimal)**

So, the **network address = 10.192.0.0/11**

2.  **Find the block size:**

    -   The **/11** subnet mask is **255.224.0.0**, where the second
        octet uses 3 bits for subnetting.

    -   The **block size** in the second octet is **256 - 224 = 32**

    -   This means our subnet ranges are:

        -   **10.192.0.0/11**

        -   **10.224.0.0/11** (next subnet)

        -   **10.256.0.0 → Invalid (out of range for IPv4)**

3.  **Verify the broadcast address:**

    -   The next subnet **starts at 10.224.0.0**, so the **last IP of
        10.192.0.0/11** is one before that:

    -   **Broadcast address = 10.223.255.255**

4.  **First & Last Usable IPs:**

    -   **First usable IP =** **10.192.0.1**

    -   **Last usable IP =** **10.223.255.254**

5.  **Number of usable hosts:**

    -   Since we have **21 bits** for host addresses:

    -   **2²¹ - 2 = 2,097,150 usable hosts**

**Corrections & Adjustments to Your Explanation:**

-   You correctly identified that 192 is valid, but instead of flipping
    the **third octet\'s bit** manually, the better way to approach it
    is:

    -   Find the **block size (32)** in the second octet.

    -   Step through **192 → 224**, which confirms **10.224.0.0** is the
        next network.

-   **The first subnet in a /11 is NOT 10.0.0.0**; it actually starts
    from **10.0.0.0/11 → 10.32.0.0/11 → 10.64.0.0/11, etc.**

    -   So **10.192.0.0/11 is not the first subnet in a Class A /11
        network**, but just the one that contains **10.217.182.223**.

Your explanation was very close! Just refine the thought process
slightly, and you\'re golden. 🔥🚀

<https://www.youtube.com/watch?v=z-JqCedc9EI&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=27>

Answer is:

Network Address: 10.192.0.0/11

Broadcast address: 10.223.255.255

First usable address: 10.192.0.1

Last usable address: 10.223.255.254

Number of hosts: 2,097,150

# Variable-Length Subnet Masks (VLSM): 

What we have been using in the previous pages is FLSM, Fixed-Length
Subnet Masks.

Meaning, all the subnets use the same prefix length, for example the
recent /11,

225.223.0.0

VLSM is the process of creating subnets of different sizes, to make your
use of network addresses more efficient.

Note to self: I think this is splitting the bits more. For example, you
get a class A network address /8 we have 24 spare bits to play. As for
the /11 we did earlier, we borrowed 3 bits to make the /11 which still
leaves us 21 bits to use.

So, we can split it again.

VLSM Steps:

1.  Assign the largest subnet at the start of the address space

2.  Assign the second-largest subnet after it.

3.  Repeat the process until all subnets have been assigned.

For this next question, we are given the address 192.168.1.0 /24 we need
to split up for 5 networks with Tokyo LAN A having 110 hosts, Tokyo LAN
B 8 hosts, Toronto LAN A 29 hosts, Toronto LAN B 45 hosts. Then a
point-to-point connection between routers connecting the two sites,

  -----------------------------------------------------------------------------------
  Name:     Network:         Broadcast:      First:          Last:           Total
                                                                             hosts:
  --------- ---------------- --------------- --------------- --------------- --------
  Tokyo LAN 192.168.1.0/25   192.168.1.255   192.168.1.129   192.168.1.254   126
  A                                                                          

  Toronto   192.168.1.0/26   192.168.1.255   192.168.1.193   192.168.1.254   62
  LAN A                                                                      

  Toronto   192.168.1.0/27   192.168.1.255   192.168.1.225   192.168.1.254   30
  LAN B                                                                      

  Tokyo LAN 192.168.1.0/29   192.168.1.255   192.168.1.241   192.168.1.254   14
  B                                                                          

  PTP       192.168.1.0/30   192.168.1.255   192.168.1.251   192.168.1.254   2
  -----------------------------------------------------------------------------------

Wrong -- but right logic.

Correct versions (Answer):

  ---------------------------------------------------------------------------------------------
  Name:     Network:        Broadcast:      First:          Last:           Subnet     Total
                                                                            mask       usable
                                                                            (Prefix    hosts:
                                                                            Length):   
  --------- --------------- --------------- --------------- --------------- ---------- --------
  Tokyo LAN 192.168.1.0     192.168.1.127   192.168.1.1     192.168.1.126   /25        126
  A                                                                                    

  Toronto   192.168.1.128   192.168.1.191   192.168.1.129   192.168.1.190   /26        62
  LAN B                                                                                

  Toronto   192.168.1.192   192.168.1.223   192.168.1.193   192.168.1.222   /27        30
  LAN A                                                                                

  Tokyo LAN 192.168.1.240   192.168.1.255   192.168.1.241   192.168.1.254   /28        14
  B                                                                                    

  PTP       192.168.1.252   192.168.1.255   192.168.1.253   192.168.1.254   /30        2
  ---------------------------------------------------------------------------------------------

Not wrong but not the next available address in the address schema:
Below is the correct alteration.

  --------------------------------------------------------------------------------------------
  Name:    Network:        Broadcast:      First:          Last:           Subnet     Total
                                                                           mask       usable
                                                                           (Prefix    hosts:
                                                                           Length):   
  -------- --------------- --------------- --------------- --------------- ---------- --------
  Tokyo    192.168.1.224   192.168.1.239   192.168.1.225   192.168.1.238   /28        14
  LAN B                                                                               

  PTP      192.168.1.240   192.168.1.243   192.168.2.241   192.168.1.242   /30        2
  --------------------------------------------------------------------------------------------

Packet Tracer Lab: 192.168.5.0/24

  ------------------------------------------------------------------------------------------------
  Name:      Network:        Broadcast:      First:          Last:           Subnet mask  Total
                                                                             (Prefix      usable
                                                                             Length):     hosts:
  ---------- --------------- --------------- --------------- --------------- ------------ --------
  LAN 2 (64  192.168.5.0     192.168.5.127   192.168.5.1     192.168.5.126   /25          126
  hosts)                                                                                  

  LAN 1 (45  192.168.5.128   192.168.5.191   192.168.5.129   192.168.5.190   /26          62
  hosts)                                                                                  

  LAN 3 (14  192.168.5.192   192.168.5.207   192.168.5.193   192.168.5.206   /28          14
  hosts)                                                                                  

  LAN 4 (9   192.168.5.208   192.168.5.223   192.168.5.209   192.168.5.222   /28          14
  hosts)                                                                                  

  PTP        192.168.5.252   192.168.5.255   192.168.5.253   192.168.5.254   /30          2
  ------------------------------------------------------------------------------------------------

Correct: find the number of hosts (2^n^ -2) needed first, then worked
out the rest from there.

Need to trust the binary conversion.

# VLANS:

<https://www.youtube.com/watch?v=cjFzOnm6u1g&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=29>

Virtual Local Area Network

What is a LAN?

We understand a LAN is a group of devices located in a single location,
such as an office, home etc. To be more specific, a LAN is a single
broadcast domain including all devices in that broadcast domain.

Think of it like a post code which highlights the street but not
necessarily the specific house number.

A broadcast domain is the group of devices which will receive a
broadcast frame (destination MAC FFFF.FFFF.FFFF) sent by any one of the
members. Members being the other users/devices within the same bubble.

Bubble meaning LAN.

Additionally, without VLANs all devices connected to the switch are in
the same broadcast domain, which can lead to congestion.

For example, in this diagram:

![A diagram of a computer network AI-generated content may be
incorrect.](media/image22.png){width="6.268055555555556in"
height="6.357638888888889in"}

We can see there are three broadcast domains. When a PC sends a
broadcast frame, a mac address with all Fs (FFFF.FFFF.FFFF) is sent to
the switch within that domain (LAN) also known as ARP (Address
resolution protocol) which floods it out of all interfaces except from
the one it was received on.

The switch will update its MAC address table with the senders (source)
MAC address for 5 minutes. This is to allow smooth transition of
communication and reduce resource overhead by not keeping the address in
its memory permanently.

Once the broadcast frame reaches the Router, it will be dropped by the
router as routers do not forward/send broadcast frames.

![A computer diagram of a computer network AI-generated content may be
incorrect.](media/image23.png){width="6.268055555555556in"
height="6.366666666666666in"}

This diagram is to highlight the different broadcast domains. Equalling
to 4 total domains.

VLANs are configured on the switches interface per-host.

Logically separate end hosts at layer 2

VLANs Part 1 lab:

  ---------------------------------------------------------------------------------------
  Name:         Network:     Broadcast:   First:       Last:        Subnet mask  Total
                                                                    (Prefix      usable
                                                                    Length):     hosts:
  ------------- ------------ ------------ ------------ ------------ ------------ --------
  Engineering   10.0.0.0     10.0.0.63    10.0.0.1     10.0.0.62    /26          62

  HR            10.0.0.64    10.0.0.127   10.0.0.65    10.0.0.126   /26          62

  Sales         10.0.0.128   10.0.0.191   10.0.0.129   10.0.0.190   /26          62

  Unknown       10.0.0.192   10.0.0.255   10.0.0.193   10.0.0.254   /26          62

                                                                                 
  ---------------------------------------------------------------------------------------

  -----------------------------------------------------------------------
  Name:              VLAN:             Switch:             Router:
  ------------------ ----------------- ------------------- --------------
  Engineering        10                F3/1 -- F4/1 --     G0/0
                                       G0/1                

  HR                 20                F5/1 -- F6/1 --     G0/1
                                       G1/1                

  Sales              30                F7/1 -- F8/1 --     G0/2
                                       G2/1                

  Unknown            40                                    

                                                           
  -----------------------------------------------------------------------

## VLANs part 2: 

<https://www.youtube.com/watch?v=Jl9OOzNaBDU&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=31>

What is a trunk port:

Trunk ports are a switch interface which carries traffic over multiple
VLANs.

What are trunk ports for:

It allows switches to forward traffic from multiple VLANs over a single
physical interface. Instead of having to use a separate physical
interface for every single VLAN.

Router on a stick: (ROAS)

Requires 802.1Q encapsulation between the switch and routers connected
interfaces. Depending on the age of the switch it will need to be
specified what encapsulation to use as there are two:

802.1Q -- standard

ISL -- Cisco Propriety

To enable encapsulation on an interface --

Switchport trunk encapsulation dot1q

Is the command

What this means is a tag is attached to the Ethernet frame, which is
used to identify the VLAN frame sent over the trunk port.

Note:

A trunk port allows all VLANs (1-4094) by default.

> If you manually limit the VLANs, you can reset the trunk to its
> default behaviour by using:

Switchport trunk allowed all.

To limit the trunk port to certain VLANs by using:\
\
Switchport trunk allowed \<vlan\>

Which field of the 802.1Q tag identifies the VLAN ID of the frame?

VID ✓

VID means VLAN ID

## VLANs Part 3:

Native VLAN on Router (ROAS)

We want to use an unused VLAN number as our Native VLAN as having it as
Native VLAN 1 can cause some security issues.

There are 2 methods of configuring the native VLAN on a router:

> Use the command encapsulation dot1q *vlan-id* native on the router
> sub-interface.
>
> Configure the IP address for the native VLAN on the router's physical
> interface (the encapsulation dot1q vlan-id command is not necessary).

Setting Native VLANs assume any traffic which isn't VLAN tagged goes
through here.

SVI = Switch Virtual Interface

Rewatch --

<https://www.youtube.com/watch?v=OkPB028l2eE&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=34>

# DTP & VTP:

Cisco propriety

DTP stands for Dynamic Trunking Protocol --

> Allows switches to negotiate the status of their switchports, to be
> access port or trunk ports, without manually configuring them.
>
> DTP is enabled by default on all Cisco switch interfaces.
>
> We have been using "switchport mode access or switchport mode trunk"
> to enable our switch ports. With DTP, now we don't.
>
> It is recommended for security purposes; DTP should be disabled on all
> interfaces.

VTP stands for VLAN Trunking Protocol --

> Allows you configure VLANs on a central switch, which then acts as a
> server, that other switches can synchronised to. So, you don't have to
> configure VLANs on every switch.

What does auto and desirable do: switchport mode dynamic?

A switchport in dynamic desirable mode will actively try to form a trunk
with other Cisco switches. It will form a trunk if connected to another
switchport in the following modes:

Switchport mode trunk

Switchport mode dynamic desirable

Switchport mode auto

Command:

Show interfaces \<interface\> switchport

Dynamic: Desirable

When an interface is configured with dynamic desirable mode it will
actively want to create a trunk with any other cisco switch it is
connected to. However, is the other switch is configured with access
mode the connected will form an access link.

A switchport in dynamic desirable mode will actively try to form a trunk
with other Cisco Switches. It will form a trunk if connected to another
switchport in the following modes:

Switchport mode trunk

switchport mode dynamic desirable

switchport mode dynamic auto

Dynamic: Auto

A switchport in dynamic auto mode will NOT actively try to form a trunk
with other cisco switches, however, it will form a trunk if the switch
connected to it is actively trying to from a trunk. It will form a trunk
with a switchport in the following mode:

Switchport mode trunk

Switchport mode dynamic desirable

For example, if two switches are connected with each having an interface
configured with dynamic auto mode, they will form an "static access"
link not a Trunk. As Auto does not actively seek to create a trunk.

If a switch is manually configured with switchport mode trunk and the
other with switchport mode access, they will mismatch and will result in
an error and not pass traffic.

  ----------------------------------------------------------------------------
  Administrative   Trunk:         Dynamic        Access:        Dynamic Auto:
  mode:                           Desirable:                    
  ---------------- -------------- -------------- -------------- --------------
  Trunk            Trunk          Trunk          X              Trunk

  Dynamic          Trunk          Trunk          Access         Trunk
  Desirable                                                     

  Access           X              Access         Access         Access

  Dynamic Auto     Trunk          Trunk          Access         Access
  ----------------------------------------------------------------------------

Important note:

DTP will not form a Trunk with a Router, PC, etc. The switchport will be
in access mode.

If you wanted to configure a router on a stick for example, you will
need to manually configure the interface as a trunk.

Older switches dynamic desirable is the default administrative mode

Newer switches, dynamic mode auto is the default administrative mode

To disable an interface with DTP use this command: switchport
nonegotiate

Switches that support both 802.1Q and ISL trunk encapsulations can use
DTP to negotiate the encapsulation they will use.

This negotiation is enabled by default, as the default trunk
encapsulation mode is:

Switchport trunk encapsulation negotiate

## VTP: 

VTP stands for VLAN Trunking Protocol --

> Allows you configure VLANs on a central switch, which then acts as a
> server, that other switches can synchronised to. So, you don't have to
> configure VLANs on every switch.

Designed for large networks with many VLANs, so that you don't have to
configure each VLAN on every switch.

Like DTP, it is recommended that you do not use it. Disable it on all
interfaces.

There are three versions of VTP: 1,2, & 3

New switches support all three, whereas older switches might only
support 1 & 2.

Three modes that VTP operate in: Server. Client, and Transparent.

Cisco Switches operate in VTP server mode by default.

Which can add/modify/delete VLANs.

Store the VLAN database in non-volatile RAM (NVRAM)

Will increase the revision number every time a VLAN is
added/modified/deleted.

VTP server will advertise the latest version of the VLAN database on
trunk interfaces, and the VTP clients will synchronize their VLAN
database to it.

VTP advertisements only sent on trunk ports, not access ports.

VTP Servers also function as VTP Clients, therefore, a VTP server will
synchronize to another VTP server with a higher revision number.

VTP Clients:

Cannot add/modify/delete VLANs.

Do not store the VLAN database in NVRAM. (in VTPv3, they do)

> Will synchronize their VLAN database to the server with the highest
> revision number in their VTP domain.
>
> Will advertise their VLAN database, and forward VTP advertisements to
> other clients over their trunk ports.

VTPv1/v2 do not support the extended VLAN range (1006-4094). Only VTPv3
supports them.

If a switch with no VTP domain (domain NULL) receives a VTP
advertisement with a VTP domain name, it will automatically join that
VTP domain.

DANGER!!!!!!!

If you connect an old switch with a higher revision number to your
network (and the VTP domain name matches), all switches in the domain
will sync their VLAN database to switch.

VTP Transparent mode:

Does not participate in the VTP domain (does not sync its VLAN database)

Maintains its own VLAN database in NVRAM.

> It can add/modify or delete VLANS, but they won't be advertised to
> other switches.
>
> Will forward VTP advertisements that are in the same domain as it.
> Will not advertise it's own database.

Instructions:

Select the VLAN trunking operational modes from the left and drag them
to the resulting configuration. VLAN Trunking operational modes can be
used more than once:

Access \| Misconfig \| Trunk

  ----------------------------------------------------------------------------
  Administrative   Access:        Dynamic auto:  Dynamic        Trunk:
  mode:                                          desirable:     
  ---------------- -------------- -------------- -------------- --------------
  Access           Access ✓       access✓        access✓        Misconfig✓

  Dynamic auto     access✓        Trunk x        Trunk✓         Trunk✓
                                  (access)                      

  Dynamic          access✓        Trunk✓         Trunk✓         Trunk✓
  desirable                                                     

  Trunk            Misconfig✓     Trunk✓         Trunk✓         Trunk✓
  ----------------------------------------------------------------------------

# Spanning Tree Protocol: (STP)

'Classic Spanning Tree Protocol' is IEEE 802.1D

STP prevents layer loops by placing redundant ports in a blocking state,
essentially disabling the interface.

These interfaces act as backups that can enter a forwarding state if an
active (=currently forwarding) interface fails. Interfaces in a
forwarding state behave normally. They send and receive all normal
traffic.

Interfaces in a blocking state only send or receive STP messages (called
BPDUs = Bridge Protocol Data Units).

**How does it work?**

There is a set process that STP uses to determine which ports should be
forwarding and which should be blocking.

It works by selecting ports to be in a forwarding state and which ports
are blocking, STP creates a single path to/from each point in the
network. This prevents layer 2 loops.

STP-enabled switches send/receive "Hello BPDUs" out of all interfaces,
the default timer is 2 seconds (the switch will send a Hello BDPU out of
every interface, once every 2 seconds).

If a switch receives a Hello BDPU on an interface. It knows that
interface is connected to another switch (router, PCs, etc. Do not use
STP, so they do not send Hello BPDUs).

**Identifying STP:**

Switches use one field in the STP BPDU, the Bridge ID field, to elect a
root bridge for the network. The switch with the lowest Bridge ID
becomes the root bridge.

All ports on the root bridge are put in a forwarding state, and other
switches in the topology must have a path to reach the root bridge.

+--------------+-------------------------------------------------------+
| Bridge ID    |                                                       |
+--------------+-------------------------------------------------------+
| Bridge       | MAC Address                                           |
| Priority     |                                                       |
|              | (48 Bits)                                             |
| (16 bits)    |                                                       |
+--------------+-------------------------------------------------------+

The default bridge priority is **32768** on all switches, so by default
the MAC address is used as the tiebreaker (lowest MAC address becomes
the root bridge).

Note: The Bridge Priority is compared first. If they tie, the MAC
address is then compared.

+--------------+-------------------------------------------------------+
| Bridge ID    |                                                       |
+--------------+-------------------------------------------------------+
| Bridge       | MAC Address                                           |
| Priority     |                                                       |
|              | (48 Bits)                                             |
| (16 bits)    |                                                       |
+--------------+-------------------------------------------------------+

+----------------------+-----------------------------------------------+
| Bridge Priority (16  | Extended System ID (=VLAN ID)                 |
| Bits)                |                                               |
|                      | (12 bits)                                     |
+======================+===============================================+
+----------------------+-----------------------------------------------+

With Cisco switches they use an alternative/additional STP protocol
called PVST (Per-VLAN Spanning Tree). PVST runs a separate STP
'instance' in each VLAN, so in each VLAN different interfaces can be
forwarding/blocking.

For example, an interface could be forwarding in VLAN 1 but blocking in
VLAN 2. Each VLAN will have a different Bridge ID.

**PVST:**

To have a deeper look, here is the table which determines the number for
the bridge priority:

  ----------------------------------------------------------------------------------------------------
  Bridge                           Extended                                                       
  Priority                         System ID                                                      
                                   (VLAN ID)                                                      
  ---------- ------- ------ ------ ---------- ------ ----- ----- ----- ---- ---- ---- --- --- --- ----
  32768      16384   8192   4096   2048       1024   512   256   128   64   32   16   8   4   2   1

  1          0       0      0      0          0      0     0     0     0    0    0    0   0   0   1
  ----------------------------------------------------------------------------------------------------

As you can see, the table follows the binary same as the IP addressing
schema. As it's 16 bits in length, we draw a binary table with 16
columns.

The bridge priority was the default number of 32768, but with the
addition of PVST you can see it adds 1 more to the number. Equalling to
**32769**.

The default of PVST is VLAN 1, as you can see in the table above.

The bridge priority + extended system ID is a single field of the bridge
ID, however the extended system ID is set and cannot be changed (because
it is determined by the VLAN ID). Therefore, you can only change the
total bridge priority (bridge priority + extended system ID) in units of
4096, the value of the least significant bit of the bridge priority.

For example, lets reduce the current Bridge ID of 32769.

As we can only change the Bridge priority number, we can only add or
minus it by 4096.

Meaning the formula will be:

32769 -- 4096 = 28673

This equates to 16384 + 8192 + 4096 + 1 (VLAN ID) = 28673

**Further notes:**

The STP bridge priority can only be changed units of 4096.

The valid values you can configure are:

0, 4096, 8192, 12288, 16384, 20480, 24572, 28672, 32786, 36864, 40960,
45056, 49152, 53248, 57344, or 61440.

The extended System ID will then be added to this number to make the
total bridge priority.

**STP:**

When a switch is powered on, it assumes it is the root bridge; it will
only give up its position if it receives a 'superior' BPDU, meaning a
**lower bridge ID.** Once the topology has converged and all switches
agree on the root bridge, only the root bridge sends BPDUs.

Other switches in the network will forward these BPDUs but will not
generate their own original BPDUs.

The switch with the lowest bridge ID is elected as the root bridge. All
ports on the root bridge are designated ports (forwarding state). Each
remaining switch will select ONE of its interfaces to be its root port.

The interface with the lowest ROOT cost will be the root port. Root
ports are also in a forwarding state.

## What is the root COST: 

  -----------------------------------------------------------------------
  Speed:                                 STP Cost:
  -------------------------------------- --------------------------------
  10 Mbps                                100

  100 Mbps                               19

  1 Gbps                                 4

  10 Gbps                                2
  -----------------------------------------------------------------------

The root cost is the total cost of the outgoing interfaces path to the
root bridge.

Think of it like planning your route to somewhere on holiday with the
different road names and junctions etc. In networking these are the
interfaces, each interface might be different speeds which correlates to
cost in the table above.

The switches determine (STP) which is the lowest cost to the bridge;
quickest path forwards to reach the destination based on the total cost
of those interfaces.

The designated root bridge interfaces are all set to 0 cost.

Recap:

One switch is elected as the root bridge. All ports on the root bridge
are designated ports (forwarding state). Root bridge selection:

Lowest bridge ID

Each remaining switch will select ONE of its interfaces to be its root
port (forwarding state). Ports across from the root port are always
designated ports.

Root port selection:

Lowest root cost.

However, what happens when there are multiple ports with the same root
cost?

The switch will then select the neighbour with the **lowest bridge ID**

**Diagram: Example**

![A computer screen shot of a diagram AI-generated content may be
incorrect.](media/image26.png){width="6.072916666666667in"
height="2.7604166666666665in"}

In this diagram, SW1 has been elected as the Root Bridge, which means
all its ports are designated ports (since the Root Bridge never has
block ports).

**How was SW1 chosen as the Root Bridge?**

STP (Spanning Tree Protocol) selects the Root Bridge based on the Bridge
ID (BID).

The bridge ID consists of:

Bridge priority (16 bits) -- Default value is 32768 unless manually
changed.

Mac address (48 bits) -- Used as a tiebreaker if priorities are equal.

The switch with the lowest bridge ID (smallest priority, or lowest MAC
if priorities match, becomes the Root Bridge.

**Why does STP use 32768?**

32768 is the default bridge priority assigned by most switches. Since
STP uses binary calculations, priorities are in multiples of 4096 (e.g.,
4096, 8192...,61440) to align with VLAN-based STP (PVST+ or MST).

**Election Process:**

1.  All switches initially assume they are the Root Bridge and send BPDU
    (Bridge Protocol Data Unit) packets.

2.  They compare Bridge IDs:

    a.  If a switch receives a BPDU with a lower Bridge ID, it stops
        advertising itself as the Root and forwards the superior BPDU.

    b.  This process continues until all switches agree on the lowest
        Bridge ID, which becomes the Root Bridge.

Since SW1 had the lowest Bridge ID, it was elected as the Root Bridge.

**How do other Switches Determine their root port?**

Once the Root Bridge is elected, all non-root switches must determine
their Root Port. The Root Port (RP) is the port on a switch that has the
lowest path cost to the Root Bridge.

**STP Path Cost Calculation**

The cost of a link is based on its bandwidth. Here are the standard STP
path costs:

  -----------------------------------------------------------------------
  Speed:                                 STP Cost:
  -------------------------------------- --------------------------------
  10 Mbps                                100

  100 Mbps                               19

  1 Gbps                                 4

  10 Gbps                                2
  -----------------------------------------------------------------------

**Root Port Selection Process**

1.  Each switch receives BPDUs from neighbouring switches. These BPDUs
    contain the Root Bridge ID and the total path cost to reach the
    root.

2.  Each switch adds the cost of the incoming port to the BPDU and
    forwards it to the next switch.

3.  The switch selects the lowest cost path as it Root Port.

4.  If there's a tie in cost, the switch selects the port that received
    the BPDU from the switch with:

    a.  The lowest Bridge ID.

    b.  If the Bridge ID is the same, the lowest Port ID Is used as a
        tiebreaker.

**Example:**

If SW2 is connected to the Root Bridge SW1 via two links:

-   1 Gbps link (cost = 4)

-   100 Mbps (cost = 19)

-   SW2 will select the 1 Gbps link as its Root Port because it has the
    lowest cost.

If SW3 is two hops away from the Root Bridge:

-   It receives the BPDUs from SW2 with a cost of 4 (1 Gbps link).

-   If SW3 is connected to SW2 with another 1 Gbps link, the total cost
    to the Root is 4 + 4 =8.

-   If SW3 is also connected to SW1 directly via a 100Mbps link (cost
    19), it will prefer the 1Gbps path through SW2 (cost 8) since it has
    the lowest cost.

**Final STP Role Assignments:**

The root bridge (SW1) has only Designated Ports.

Each non-root switch:

Selects one Root Port (RP) (lowest-cost path to the Root Bridge).

> Blocks one or more ports to prevents loops, leaving only one active
> path to the Root.

![A computer screen shot of a diagram AI-generated content may be
incorrect.](media/image26.png){width="6.072916666666667in"
height="2.7604166666666665in"}

**Key Takeaways:**

-   The Root Bridge is selected based on the lowest Bridge ID.

-   Each non-root switch determines its Root Port based on the lowest
    cost path.

-   Path cost is calculated based on interface Bandwidth.

-   Tiebreakers include the lowest Bridge ID and Port ID.

## Port ID Structure:

**The port ID consist of two parts:**

1.  Port Priority (8 bits) -- Default is 128 (lower values are
    preferred)

2.  Port Number (8 bits) -- The actual interface number (e.g.,
    FastEthernet 0/1, GigabitEthernet 1/1).

So, Port ID = Port Priority + Port number

**How is Port ID Used in STP?**

If a switch has multiple ports with equal path cost to the Root Bridge,
it chooses the Root Port based on the lowest Port ID.

**Example Scenario:**

Let's say SW2 has two equal-cost paths to the Root Bridge SW1:

Port Gi1/0/1 (Port ID = 128.2)

Port Gi1/0/2 (Port ID = 128.3)

Since both ports have the same total STP cost, SW2 chooses Gi1/0/1 as
the Root Port because 128.1 \< 128.2.

Another example:

Port Gi1/0/0 (Port ID = 128.1)

Port Gi1/0/24 (Port ID = 128.25)

**Key Takeaways:**

Port ID = Port Priority (default 128) + Port Number.

Lower Port Id is preferred when there's a tie in cost.

Port Priority can be manually changed to influence STP decisions
(*spanning tree port-priority \<value\>*).

This process of the STP protocol is only ever used when the path cost is
the same.

## Port Selection Process: 

It will use this process in a hierarchical manner:

1.  **Lowest root cost (path Cost)**

    a.  The switch selects the port that receives the BPDU with the
        lowest total cost to the Root Bridge.

2.  **Lowest Sender (Neighbour) bridge ID**

    a.  If multiple ports have the same Root Cost, the switch prefers
        the BPDU from the switch neighbour with the lowest Bridge ID.

3.  **Lowest Sender (Neighbour) Port ID** -- rare cases

    a.  If all the previous values are still equal, the switch selects
        the local port with the lowest port ID.

## STP States/Timers: 

  -----------------------------------------------------------------------
  STP Port State:                  Stable/Transitional:
  -------------------------------- --------------------------------------
  **Blocking**                     Stable

  **Listening**                    Transitional

  **Learning**                     Transitional

  **Forwarding**                   Stable
  -----------------------------------------------------------------------

Root/Designated ports remain stable in a Forwarding State

Non-designated ports remain stable in a Blocking State

Listening and Learning are transitional states which are passed through
when an interface is activated, or when a Blocking port must transition
to a Forwarding state due to a change in the network topology.

Think of it like a traffic light system, where Listening and Learning
are always in yellow between go and stop.

When an interface changes, new hardware or something else changes in the
network topology, these transitional (Listening/Learning) interfaces
will change in accordance.

![](media/image27.png){width="3.4171434820647417in"
height="0.46881561679790024in"}

Non-designated ports are in a blocking state.

Interfaces in a Blocking State are effectively disabled to prevent
loops.

Interfaces in a Blocking State do not send/receive regular network
traffic.

Interfaces in a Blocking State do receive STP BPDUs.

Otherwise, it wouldn't know what state to be in, however, blocking state
does not forward STP BPDUs.

Interfaces in a blocking state do NOT learn MAC addresses.

Any traffic which goes to the blocking port simple drops the traffic and
does not learn the MAC address of the traffic.

![A white background with black text AI-generated content may be
incorrect.](media/image28.png){width="3.4588156167979003in"
height="0.7501049868766404in"}

After the blocking state, interfaces with the Designated or Root role
enter the Listening state.

Only Designated or Root ports enter the Listening state (non-designated
ports are always Blocking).

The listening state is 15 seconds long by default. This is determined by
the **Forward Delay** timer.

An interface in the listening state Only sends/receives STP BPDUs.

An interface in the listening state does not send/receive regular
traffic.

An interface in the listening state does not learn MAC addresses from
regular traffic that arrives on the interface.

STP - Listening state: 

 

"When a frame arrives on a switch interface, the switch uses the
'source' MAC address to learn the MAC address, and it updates the MAC
address table. However, if an interface is in spanning tree listening
state, it will not do this. The traffic is simply dropped, and the MAC
address learning process do not occur."

Additional context:

> While an interface is in the listening state, it is actively
> processing BPDUs to determine the network topology.
>
> This phase lasts 15 seconds by default (part of the Forward Delay
> Timer).
>
> Once the topology is understood, the interface transitions to the
> learning state and then forwarding state if no loops are detected.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image29.png){width="3.3858891076115487in"
height="0.9793033683289589in"}

After the Listening state, a Designated or Root port will enter the
Learning state. The learning state is 15 seconds long by default. This
is determined by the Forward Delay timer (the same timer is used for
both the Listening and Learning states).

Meaning by default it takes a total of 30 seconds to move through both
states to enter the forwarding state.

An interface in the Learning state Only send/receives STP BPDUs.

An interface in the Learning state does NOT send/receive regular
traffic.

An interface in the Learning state **[Learns]{.underline}** MAC
Addresses from regular traffic that arrives on the interface.

  -----------------------------------------------------------------------
  STP Port State:                  Stable/Transitional:
  -------------------------------- --------------------------------------
  **Blocking**                     Stable

  **Listening**                    Transitional

  **Learning**                     Transitional

  **Forwarding**                   Stable
  -----------------------------------------------------------------------

Root and Designated ports are in a Forwarding state (stable).

A port in the forwarding state operates as normal.

A port in the forwarding state sends/receives BPDUs.

A port in the forwarding state sends/receives normal traffic.

A port in the forwarding state learns MAC addresses.

A switch port operating as normal.

### Summary:

  ---------------------------------------------------------------------------------
  STP Port State Send/Receive   Frame          MAC address    Stable/Transitional
                 BPDUs          Forwarding     learning       
                                (regular                      
                                traffic)                      
  -------------- -------------- -------------- -------------- ---------------------
  Blocking       NO/YES         NO             NO             Stable

  Listening      YES/YES        NO             NO             Transitional

  Learning       YES/YES        NO             YES            Transitional

  Forwarding     YES/YES        YES            YES            Stable

  Disabled       NO/NO          NO             NO             Stable
  ---------------------------------------------------------------------------------

  -----------------------------------------------------------------------
  STP Timer               Purpose                 Duration
  ----------------------- ----------------------- -----------------------
  Hello                   How often the root      2sec
                          bridge sends "Hello     
                          BPDUs" -- hello is it   
                          me you're looking for!  

  Forward Delay           How long the switch     15sec
                          will stay in the        
                          Listening and Learning  
                          states (each state 15   
                          seconds = total 30      
                          seconds).               

  Max Age                 How long an interface   20sec (10^\*^ hello)
                          will wait [after        
                          ceasing to receive      
                          Hello                   
                          BDPUs]{.underline} to   
                          change the STP          
                          topology.               
  -----------------------------------------------------------------------

Switches will only forward BPDUs on its designated ports. For example,
in this image:

![A computer screen shot of a computer AI-generated content may be
incorrect.](media/image30.png){width="4.583333333333333in"
height="3.4375in"}

PVST is the old protocol and only supports Cisco's old technology ISL
trunk encapsulation. When someone refers to PVST, they most likely mean
PVST+ which supports 802.1Q encapsulation.

Normal STP not the PVST+ uses a MAC address of 0180.c200.0000

PVST+ MAC address is 01:00:0c:cc:cc:cd

  ---------------------------------------------------------------------------
  Name:       VLAN:     Port:     STP:     Port:     STP:     Port:    STP:
  ----------- --------- --------- -------- --------- -------- -------- ------
  SW1         1         F0/1      B        F0/2      D        F0/3     R

              2         F0/1      B        F0/2      D        F0/3     R

                                                                       

  SW2: RB     1         F0/1      D        F0/2      D        F0/3     D

              2         F0/1      D        F0/2      D        F0/3     D

                                                                       

  SW3         1         F0/1      D        F0/2      R        F0/3     D

              2         F0/1      D        F0/2      R        F0/3     

                                                                       

  SW4         1         Fa0/1     R        Fa0/2     B        Fa0/3    

              2         Fa0/1     R        Fa0/2     B        Fa0/3    D
  ---------------------------------------------------------------------------

Lab-config STP 1

## LAB Exercise

  ---------------------------------------------------------------------------
  Name:       VLAN:     Port:     STP:     Port:     STP:     Port:    STP:
  ----------- --------- --------- -------- --------- -------- -------- ------
  SW1: RB     1         F0/1      D        F0/2      D        F0/3     D

              2         F0/1      D        F0/2      D        F0/3     R

                                                                       

  SW2         1         F0/1      D        F0/2      D        F0/3     R

              2         F0/1      D        F0/2      D        F0/3     D

                                                                       

  SW3         1         F0/1      R        F0/2      B        F0/3     D

              2         F0/1      B        F0/2      R        F0/3     

                                                                       

  SW4         1         Fa0/1     B        Fa0/2     R        Fa0/3    

              2         Fa0/1     R        Fa0/2     B        Fa0/3    D
  ---------------------------------------------------------------------------

Lab-Config STP 2 after changing VLAN priorities

## Port fast: 

Portfast allows a port to move immediately to the Forwarding state,
bypassing the Listening and Learning state. Since we are connecting end
devices to these ports, it safe enable portfast on these ports; making
it immediate to forwarding state than weighting when you plug in a
device.

## STP Toolkit:

**PortFast:**

> Allows switch ports connected to end hosts to immediately enter the
> STP Forwarding state, bypassing Listening and Learning.
>
> You can configure PortFast in two ways:

1.  Interface config mode:

> SW1(config-if)# **spanning-tree portfast**
>
> This enables Portfast only on the individual interface.

2.  Global config mode:

> SW1(config)# **spanning-tree portfast default**
>
> This enables Portfat on [all access ports.]{.underline}
>
> Connections between switches are almost always trunk links
>
> Connections to end hosts are almost always access links.

In some cases, you might want to enable PortFast on a trunk port:

> A port connected to a virtualisation server with virtual machines
> (VMs) in different VLANs.
>
> A port connected to a router via router-on-a-stick (ROAS).

This can only be configured per-point in interface config mode:

SW1(config-if)# **spanning-tree portfast trunk**

**There is two Portfast Modes:**

Portfast Network & Portfast edge.

In modern Cisco switches, if you used the commands above, the device
will automatically add **edge** keyword to the configuration.

For example:

SW1(config-if)# **spanning-tree portfast** In the running-config:
**spanning-tree portfast edge**

SW1(config-if)# **spanning-tree portfast trunk** In the running-config:
**spanning-tree portfast edge trunk**

SW1(config)# **spanning-tree portfast default** in the running-config:
**spanning-tree** **portfast** **edge** **default**

You can use either version of the commands when configuring PortFast.

The result is the same: edge will always be added in the configuration.

**BPDU Guard:**

> Automatically disables a port if it receives a BPDU, protecting the
> STP topology by preventing unauthorized devices from becoming part of
> the network.

**BPDU Filter:**

Stops a port from sending BPDUs or processing received BPDUs.

**Root Guard:**

> Prevents a port from becoming a Root Port by disabling it if superior
> BPDUs (BPDUs with a lower bridge ID) are received. This enforces the
> current Root Bridge as the authoritative Root.
>
> It's a protection mechanism to prevent misconfigured switches from
> trying to become the Root Bridge, causing STP instability or network
> loops.

**Where to Apply Root Guard:**

> On ports that connect to access switches or other switches that should
> never become the Root Bridge.
>
> This is commonly done on distribution and access layer switches
> connected to the Root Bridge (or upstream switches) to ensure they
> don't accidentally or maliciously try to take over the Root Bridge
> role.

**Example Use Case:**

> Preventing rogue switches: If someone plugs in a switch with a lower
> Bridge ID (like a misconfigured switch), it might send superior BPDUs.
> Root Guard blocks the port, preventing this switch from becoming the
> Root Bridge, thereby maintaining network stability.
>
> Or if connecting a switch to a clients' network and you don't want to
> ruin your clients' network.
>
> **Key Note:**
>
> Root Guard only works on ports where you don't want the Root Bridge
> role to change; typically, access ports and uplinks.

**Loop Guard:**

> Protects the network from loops y disabling a port if it unexpectedly
> stops receiving BPDUs, ensuring it does not mistakenly enter the
> Forwarding state.

**Summary:**

When selecting a LAN's root bridge, you should consider the following:

Optimal traffic flow:

Minimizing latency

Minimize congestion

Stability and reliability

Within your own LAN, you can easily control the root bridge by setting
its priority to 0. There are cases where you might connect your switches
to other switches outside of your control (e.g. service provider +
client).

Which is very unlikely, unless you work in an ISP. Even then, it will
most likely be an edge router using MPLS. So, STP isn't an issue. Since
we would be dealing with layer 3 routing and not layer 2 switching
protocols.

Root Guard can be configured on specific ports to prevent them from
accepting superior BPDUs from switches outside of your control.

# RSTP (Rapid Spanning-Tree Protocol)

+-----------------------------------+-----------------------------------+
| Industry Standard (IEEE):         | Cisco Versions:                   |
+===================================+===================================+
| Classic -- Spanning Tree Protocol | **Per-VLAN Spanning Tree Plus     |
| (802.1D):                         | (PVST+):**                        |
|                                   |                                   |
| 1.  All VLANs share one STP       | 1.  Cisco's upgrade to 802.1D     |
|     instance                      |                                   |
|                                   | 2.  Each VLAN has its own STP     |
| 2.  Therefore, cannot load        |     instance.                     |
|     balance.                      |                                   |
|                                   | 3.  Can load balance by blocking  |
| 3.  The original STP              |     different ports each VLAN.    |
+-----------------------------------+-----------------------------------+
| Rapid Spanning Tree Protocol      | **Rapid Per-VLAN Spanning Tree    |
| (802.1w):                         | Plus (Rapid PVST+):**             |
|                                   |                                   |
| 1.  Much faster at                | 1.  Cisco's upgrade to 802.1w     |
|     converging/adapting to        |                                   |
|     network changes than 802.1D   | 2.  Each VLAN has its own STP     |
|                                   |     instance.                     |
| 2.  All VLANs share one STP       |                                   |
|     instance                      | 3.  Can load balance by blocking  |
|                                   |     different ports in each VLAN. |
| 3.  Therefore, cannot load        |                                   |
|     balance.                      |                                   |
+-----------------------------------+-----------------------------------+
| Multiple Spanning Tree Protocol   |                                   |
| (802.1s)                          |                                   |
|                                   |                                   |
| 1.  Uses modified RSTP mechanics. |                                   |
|                                   |                                   |
| 2.  Can group multiple VLANs into |                                   |
|     different instances (ie.      |                                   |
|     VLANs 1-5 in instance 1,      |                                   |
|     VLANs 6-10 in instance 2) to  |                                   |
|     perform load balancing.       |                                   |
+-----------------------------------+-----------------------------------+

**CISCO's summary:**

"RSTP is not a timer-based spanning tree algorithm like 802.1D.
Therefore, RSTP offers an improvement over the 30 seconds or more that
802.1D takes to move a link to forwarding. The heart of the protocol is
a new bridge-bridge handshake mechanism, which allows ports to move
directly to forwarding."

Updated STP costs to include the newer and faster speeds:

  ------------------------------------------------------------------------
  Speed:                 STP Cost:               RSTP Cost:
  ---------------------- ----------------------- -------------------------
  10 Mbps                100                     2,000,000

  100 Mbps               19                      200,000

  1 Gbps                 4                       20,000

  10 Gbps                2                       2000

  100 Gbps               X                       200

  1 Tbps                 X                       20
  ------------------------------------------------------------------------

Rapid Spanning Tree Port States:

  ---------------------------------------------------------------------------------
  STP Port State Send/Receive   Frame          MAC address    Stable/Transitional
                 BPDUs          Forwarding     learning       
                                (regular                      
                                traffic)                      
  -------------- -------------- -------------- -------------- ---------------------
  Discarding     NO/YES         NO             NO             Stable

  Learning       YES/YES        NO             YES            Transitional

  Forwarding     YES/YES        YES            YES            Stable
  ---------------------------------------------------------------------------------

If a port is administratively disabled (shutdown command) = discarding
state

If a port is enabled but blocking traffic to prevent layer 2 loops =
discarding state

# EtherChannel: 

There are three methods of EtherChannel configuration on Cisco Switches:

1.  PAgP (Port Aggregation Protocol)

    1.  Cisco proprietary protocol

    2.  Dynamically negotiates the creation/maintenance of the
        EtherChannel

2.  LACP (Link Aggregation Control Protocol)

    1.  Industry Standard protocol (IEEE 802.3ad)

    2.  Dynamically negotiates the creation/maintenance of the
        EtherChannel. (like DTP does for Trunk)

3.  Static EtherChannel

    1.  A protocol isn't used to determine if an EtherChannel should be
        formed.

    2.  Interfaces are statically configured to form an EtherChannel.

        1.  However, it is recommended that this is not done. As having
            issues appear, be resolved automatically by using the other
            protocols makes life easier and trouble shooting.

Up to 8 interfaces can be formed into a single EtherChannel (LACP allows
up to 16, but only 8 will be active, the other will be in standby mode,
waiting for an active interface to fail).

# Dynamic Routing Protocols: 

Routers can use dynamic routing protocols to advertise information about
the routes they know to other routers. They form 'adjacencies' /
'neighbour relationships' / 'neighborships' with adjacent routers to
exchange this information.

If multiple routes to a destination are learn, the router determines
which route is superior and adds it to the routing table. It uses
'metric' of the route to decide which is superior (lower
metric=superior), think back to the spanning tree protocol (STP) and how
it decides which path is a designated/root/block etc.

Types of dynamic routing protocols:

IGP -- Interior Gateway Protocol

IGP = used to share routes within a single autonomous system (AS), which
is a single organisation (i.e., company).

EGP -- Exterior Gateway Protocol

EGP = used to share routes between different autonomous systems.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image31.png){width="6.268055555555556in"
height="2.7111111111111112in"}

![](media/image32.png){width="6.268055555555556in" height="3.5125in"}

## Distance Vector: 

Distance Vector protocols operate by sending the following to their
directly connected neighbours:

Their known destination networks

Their metric to reach their known destination networks

This method of sharing route information is often called "**routing by
rumour**".

This is because the router doesn't know about the network beyond its
neighbours. It only knows the information that its neighbours tell it.

Distance Vector = Metric \| Direction (Next hop)

For example, a router will advertise it's IP address (hey, I'm here)
with a metric number (here's how you can get to me) to its connected
neighbour. The next-door neighbour will be a metric of 1, the neighbour
(router) will advertise the same IP address but with a metric of 2 to
its neighbour and so on.

![A diagram of a computer AI-generated content may be
incorrect.](media/image32.png){width="6.268055555555556in"
height="3.5125in"}

## Link State Protocol: 

When using a link state routing protocol, every router creates a
'connectivity map' of the network. To allow this, each router advertises
information about its interfaces (connected networks) to its neighbours.
These advertisements are passed along to other routers, until all router
in the network develop the same map of the network.

To further explain:

-   Each router running a link-state protocol discovers it directly
    connected networks and neighbours.

-   It then creates a Link-State Advertisement (LSA) -- A kind of
    "network postcard", but to every router in the area.

-   Every router stores these LSA in a Link-state database (LSDB),
    building a topological map of the entire network.

-   Once they all have the same map, they independently run Dijkstra's
    algorithm (SPF algorithm) to calculate the shortest path to every
    destination.

Think of it like a road map zoomed in, then slowly zooming out as new
routing information is learnt till you see multiple connected towns etc.

Each router first sees only its street (local interfaces), then its
neighbourhood (neighbouring routers), and eventually gets the full map
showing all routes, paths, and towns (entire network topology).

To further visualize, it's like a puzzle being solved -- each LSA is a
piece, and once every router has the full puzzle, they all know the best
way to reach any destination.

-   Lowest route cost (metric) is considered best.

> ![A close-up of a sign AI-generated content may be
> incorrect.](media/image33.png){width="4.594444444444444in"
> height="1.2638888888888888in"}

![A black text on a white background AI-generated content may be
incorrect.](media/image34.png){width="4.072916666666667in"
height="0.53125in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image35.png){width="6.268055555555556in"
height="2.1326388888888888in"}

When this happens in the routing table of a router, this is called
**ECMP**.

## Dynamic Routing Protocol Metrics:

  -----------------------------------------------------------------------
  IGP:                    Metric:                 Explanation:
  ----------------------- ----------------------- -----------------------
  RIP                     Hop count               Each router in the path
                                                  counts as one 'hop'.
                                                  The total metric is
                                                  that total number of
                                                  hops to the
                                                  destination. **Links of
                                                  all speeds are equal**

  EIGRP                   Metric based on         Complex formula that
                          Bandwidth & delay (by   can take into account
                          default)                many values. By
                                                  default, the bandwidth
                                                  of the **slowest link
                                                  in the route** and the
                                                  total delay of all
                                                  links in the route are
                                                  used.

  OSPF                    Cost                    The cost of each link
                                                  is calculated based on
                                                  bandwidth. The total
                                                  metric is the total
                                                  cost of each link in
                                                  the route.

  IS-IS                   Cost                    The total metric is the
                                                  total cost of each link
                                                  in the route. The cost
                                                  of each link is **not**
                                                  automatically
                                                  calculated by default.
                                                  All links have a cost
                                                  of 10 by default.
  -----------------------------------------------------------------------

## Administrative Distance:

In most cases a company will only use a single IGP -- usually OSPF or
EIGRP. However, in some rare cases they might use two. For example, if a
two company connect their networks to share information, two different
routing protocols might be in use.

When this happens, the two routing protocols cannot determine which
metric to use. This is where the administrative distance (AD) is used to
determine which routing protocol is preferred.

In this scenario, the lower AD is preferred.

  -----------------------------------------------------------------------
  Route protocol/type                                AD
  -------------------------------------------------- --------------------
  Directly connected                                 0

  Static                                             1

  External BGP (eBGP)                                20

  EIGRP                                              90

  IGRP                                               100

  OSPF                                               110

  IS-IS                                              115

  RIP                                                120

  EIGRP (External)                                   170

  Internal BGP (iBGP)                                200

  Unusable                                           255
  -----------------------------------------------------------------------

By changing the AD of a static route, you can make it less preferred
than routes learned by a dynamic routing protocol to the same
destination (make sure the AD is higher than the routing protocol's
AD!).

This is called a 'floating static route'.

The route will be inactive (not in the routing table) unless the route
learned by the dynamic routing protocol is removed (for example, the
remote router stops advertising it for some reason, or an interface
failure causes an adjacency with a neighbour to be lost).

## RIP & EIGRP:

For RIP anything over the maximum number of hops (15) will be considered
unreachable.

RIP has three versions:

**RIPv1** and **RIPv2**, used for IPv4

**RIPng** (RIP Next Generation), used for IPv6

RIP uses two message type:

**Request:** To ask RIP-enabled neighbour to routers to send their
routing table

**Response:** To send the local router's routing table to neighbouring
routers

By default, RIP enabled routers will share their routing table every 30
seconds. In larger networks this can cause bandwidth issues.

**RIPv1**: No longer used in modern networking.

-   Only supports classful addresses

-   Doesn't support VLSM and CIDR

-   Doesn't include subnet mask information in advertisements (Response
    messages)

-   Message are broadcast to 255.255.255.255

**RIPv2**:

-   Supports VLSM and CIDR

-   Includes subnet mask information in advertisements

-   Messages are **multicast** to 224.0.0.9

**Broadcast** messages are delivered to all devices on the local
network.

**Multicas**t messages are delivered only to devices that joined that
specific multicast group.

![A computer diagram with text and symbols AI-generated content may be
incorrect.](media/image36.png){width="6.268055555555556in"
height="3.1243055555555554in"}

Although there is no RIP neighbours connected to G2/0. R1 will
continuously send RIP advertisements out of G2/0. This is unnecessary
traffic, so G2/0 should be configured as a **passive interface**.

The **network** commands tell the router to:

-   Look for interfaces with an IP address that is in the specified
    range

-   Active RIP on the interfaces that all in the range

-   Form adjacencies to connected RIP Neighbours

-   Advertise the **network prefix of the interface** (NOT the prefix in
    the network command)

    -   You're setting the rule with a known network, and when the
        router matches an interface to it, it advertises the interface's
        real IP and Subnet.

OSPF and EIGRP network commands operate in the same way

### Summary note: 

You're setting the rule with a network range that the router knows, and
when it finds an interface whose IP address falls within that range, it:

1.  "Enables the routing protocol on that interface"

2.  "Advertise the real network prefix (IP + Subnet) of that interface
    to other routers"

Using RIP as an example:

Router RIP

Network 10.0.0.0 = classful addressing (Class A) in RIPv1

Let's say:\
\
G0/0 = 10.1.1.1 /24

G0/1 = 192.168.1.1 /24

Only **G0/0** matches the 10.0.0.0 range.

So, rip is enabled on G0/0.

The router advertises **10.1.1.1 /24** to neighbours and starts sending
and receiving RIP updates on that interface.

It does not advertise 10.0.0.0 /8 -- that's just what you typed in the
command to match interfaces, not what gets shared.

This is how **EIGRP** is configured too; however, EIGRP supports
wildcard masks, while RIP does not.

A wildcard mask is essentially the inverse of a subnet mask. For
example:

-   Subnet mask: 255.255.255.0 = /24

-   Wildcard: 0.0.0.255 = /24

Wildcards are used in EIGRP when you want to specify exactly which
subnet(s) to match.

If you don't include a wildcard in EIGRP, it behaves like RIP:

It assumes a classful boundary -- so typing "network 10.0.0.0" is
treated as /8 (with a wildcard of 0.255.255.255), and the router matches
any interface with an IP in the 10.0.0.0/8 range.

But with EIGRP, you can be more precise using a wildcard, e.g.:

Network: **10.1.1.0 0.0.0.255**

This would activate EIGRP only on interfaces in the 10.1.1.X subnet.

TL; DR:

  -----------------------------------------------------------------------
  Feature:                RIP:                    EIGRP:
  ----------------------- ----------------------- -----------------------
  Uses Wildcards          X No                    ✓ Yes

  Classful matching       ✓ Yes                   ✓ (if no wildcard)

  VLSM/CIDR support       X (RIPv1), ✓ (RIPv2)    ✓ Yes

  Precision control       X                       ✓ Yes
  -----------------------------------------------------------------------

### Further note: 

In RIP interface, using the command:\
\
**default-information originate**

Will advertise a default route (0.0.0.0/0) to RIP neighbours -- but only
if the router already has a default route in its routing table (e.g., a
static route like ip route 0.0.0.0 0.0.0.0 \<next0hop\>).

This tells other routers:

"Hey! You can send unknown traffic to me -- I've got a way out to the
internet (or somewhere beyond our RIP domain)."

This command only works for RIP and OSPF; not EIGRP.

-   For EIGRP you simply put the default route in EIGRP:

    -   **Network 0.0.0.0**

    -   Alternatively: **redistribute static**

    -   Or -- **redistribute static route-map DEFAULT_ONLY**

RIP treats all connections equally as one hop: so if two routes to the
same destination in the routing table are shown, with the same number of
**hops**, it will be treated equally and will load balance between the
two routes, whether one connection a gigabit and other is a fast
ethernet connection.

### Command: show ip protocols 

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image37.png){width="6.268055555555556in"
height="3.527083333333333in"}

### EIGRP: 

-   Stands for Enhance interior gateway protocol.

-   Does not have the 15 'hop-count' limit of RIP.

-   Sends messages using multicast address 224.0.0.10

-   Is the only IGP that can perform unequal-cost load-balancing (by
    default it performs ECMP load-balancing over 4 paths like RIP).

  -----------------------------------------------------------------------
  Protocol:               Multicast Address:      Purpose:
  ----------------------- ----------------------- -----------------------
  RIP                     224.0.0.9               RIP routers send
                                                  updates here (RIPv2
                                                  only)

  EIGRP                   224.0.0.10              EIGRP routers use this
                                                  to talk to each other.
  -----------------------------------------------------------------------

**Think of it like a private radio channel**

What multicast means here:

-   These addresses are like special radio frequencies that only routers
    in that protocol group "tune in" to.

-   Devices on the same subnet will ignore these multicast packets
    unless they're configured to participate in that routing protocol.

-   RIP and EIGRP separate their traffic from:

    -   Other routing protocols

    -   End-user devices (like PCs, printers, etc.)

    -   Even each other.

**"Think of RIP routers chatting on channel 9, and EIGRP router on
channel 10 -- and only routers "subscribed" to that channel can hear and
respond."**

Router ID priority:

Manual Configuration -- Highest Loopback interface address -- Highest
Physical Interface address

**EIGRP metric**:

By default, EIGRP uses bandwidth and delay to calculate metric.

Formula can be simplified to:

**Metric = bandwidth + Delay**

Bandwidth of the **slowest link** + the delay **of all links**

-   **Feasible Distance** = this router's metric value to the route's
    destination

    -   The entire length of the route to reach the destination.

-   **Report Distance** (aka Advertised Distance) = The neighbours
    metric value to the route's destination.

![A computer screen shot of a router diagram AI-generated content may be
incorrect.](media/image38.png){width="6.268055555555556in"
height="3.5284722222222222in"}

Via 10.0.12.2:

In red is R1's feasible distance

In blue is R2's reported distance

And the same for the route underneath via 10.0.13.2

As you can see the metric for it is higher, why traffic will be sent to
R2 over the gigabit link and to R3 on Fast ethernet link.

#### EIGRP Terminology: 

-   **Feasible Distance** = this router's metric value to the route's
    destination

    -   The entire length of the route to reach the destination.

-   **Report Distance** (aka Advertised Distance) = The neighbours
    metric value to the route's destination.

-   **Successor** = The route with the lowest metric to the destination
    (the best route)

-   **Feasible Successor** = An alternate route to the destination (not
    the best route) *[Which meets the feasibility
    condition]{.underline}*

    -   *Feasibility condition: A route is considered **a feasible
        successor** if its **reported distance** is lower than the
        successor route's **feasible distance**.*

*[Key Concepts in EIGRP:]{.underline}*

-   Successor:

    -   The best path to the destination (lowest feasible distance). It
        goes straight into the routing table.

-   Feasible Successor:

    -   A backup path -- not used immediately, but ready to go instantly
        if the successor fails.

*[Feasibility Condition:]{.underline}*

A route is considered a **feasible successor** only its **reported
distance** is less than the **feasible distance** of the **successor**.

-   Feasible Distance (FD): Total cost from this router to the
    destination via the successor.

-   Reported Distance (RD): Cost from the neighbour (who's offering the
    route) to the destination.

Basically:\
\
"I will accept your route as a safe backup only if you are closer to the
destination than I am."

This prevents loops -- the neighbour must be closer to the destination
than you are (according to their own view).

![A computer screen shot of a computer AI-generated content may be
incorrect.](media/image39.png){width="6.268055555555556in"
height="3.463888888888889in"}

#### EIGRP Unequal-Cost Load-balancing

By default, EIGRP does not do unequal load-balancing.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image40.png){width="6.268055555555556in"
height="3.5180555555555557in"}

To add this feature to EIGRP, in the EIGRP interface:\
\
R1 (config-router)#variance ?

\<1-128\> Metric variance Multiplier

R1 (config-router)#variance 2

Variance 2 = feasible successor routes with an FD up to 2x the successor
route's FD can be used to load-balance.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image41.png){width="6.268055555555556in"
height="2.94375in"}

As you can see, highlighted in red. I changed the variance to 2 and it
has 2 successors rather than the 1 like all the others. This means
traffic will be load balanced between the two routes even though one is
fast ethernet and the other is gigabit.

(You will see another route with 2 successors to 4.4.4.4 loopback
address, as that is the destination \*router\* as the 192.168.4.0/24
one)

How it does this:

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image42.png){width="6.268055555555556in"
height="2.94375in"}

Because I set the variance to 2 it will use the same process as if it
was 1 by default but use the FD number highlighted in red and times (\*)
it by 2 making the actual FD = 28672\*2 = 57344

Reminder:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image43.png){width="6.268055555555556in"
height="2.94375in"}

In EIGRP:

-   FD (Feasible Distance):

    -   The total metric from this router (R1) to the destination
        network.

        -   This is what's highlighted in red

-   RD (Reported Distance):

    -   The metric the neighbour is reporting to reach the destination
        (how far the neighbour thinks it is).

        -   This Is what's highlighted in yellow

-   Highlighted in Blue is the same as the FD of that route through
    10.0.12.2 -- router's total cost via that next hop.

EIGRP will only perform unequal-cost load-balancing over feasible
successor routes. If a route does not meet the feasibility requirement,
it will NEVER be selected for load-balancing, regardless of the
variance.

# OSPF: Part 1

Brief overview:

![A diagram of a computer AI-generated content may be
incorrect.](media/image32.png){width="6.268055555555556in"
height="3.5125in"}

When using a Link State routing protocol, every router creates a
'connectivity map' of the network.

To allow this, each router advertises information about its interfaces
(connected networks) to its neighbours. These advertisements are passed
along to other routers, until all routers in the network develop the
same map of the network.

Each router independently uses this map to calculate the best routes to
each destination.

Link state protocols use more resources (CPU) on the router, because
more information is shared. However, link state protocols tend to be
faster in reacting to changes in the network than distance vector
protocols.

## Acronyms: 

**ASBR** = Autonomous System Boundary Router:

-   A router that **redistributes external routes** into an OSPF domain

    -   This typically includes:

        -   A connection to the internet, or

        -   A connection to another routing protocol (e.g., EIGRP, BGP,
            RIP), or

        -   A static router (e.g., a default route like 0.0.0.0/0)

-   Think of it as the router that advertises "way out" of the OSPF
    domain.

To advertise a default route from an ASBR (e.g., a static 0.0.0.0/0):

-   In OSPF configuration mode, use this command:

    -   **Default-information originate**

    -   This tells the ASBR to send out an LSA advertising that "this
        router has the default route out of our domain"

-   If the default route (0.0.0.0/0) exists in the routing table, OSPF
    will advertise it.

<https://notes.networklessons.com/ospf-autonomous-system-boundary-router-asbr>

**IR** = Internal Routers

-   Routers with all interfaces in the same area are called **internal
    routers.**

-   It does not connect to other OSPF areas.

-   These routers participate in in OSPF within a single area and do not
    perform inter-area routing.

**ABRs** = Area Border Routers

-   Router that has interfaces in two or more OSPF areas.

-   One of those areas must be Area 0 (the backbone area) to allow
    proper OSPF routing.

-   It connects different areas and performs inter-area route
    summarisation and translation.

**DR** = Designated Router

**BDR** = Backup Designated Router

## 1.1

OSPF stands for Open Shortest Path First/Forward.

It uses the Shortest Path First algorithm of Dutch computer scientist
Edsger Dijkstra. (aka Dijkstra's algorithm, remember this name!)

OSPF has three versions:

-   OSPFv1 (1989): OLD, not in use anymore

-   OSPFv2 (1998): Used for IPv4 -- exam topic

-   OSPFv3 (2008): Used for IPv6 (can also be used for IPv3, but usually
    v2 is used)

## 1.1.0

To further explain:

-   Each router running a link-state protocol discovers it directly
    connected networks and neighbours.

-   It then creates a Link-State Advertisement (LSA) -- A kind of
    "network postcard", but to every router in the area. "flood".

-   Every router stores these LSA in a Link-state database (LSDB),
    building a topological map of the entire network.

-   Once they all have the same map, they independently run Dijkstra's
    algorithm (SPF algorithm) to calculate the shortest path to every
    destination.

Think of it like a road map zoomed in, then slowly zooming out as new
routing information is learnt till you see multiple connected towns etc.

Each router first sees only its street (local interfaces), then its
neighbourhood (neighbouring routers), and eventually gets the full map
showing all routes, paths, and towns (entire network topology).

To further visualize, it's like a puzzle being solved -- each LSA is a
piece, and once every router has the full puzzle, they all know the best
way to reach any destination.

## OSPF -- LSA Basics:

An LSA (**Link-State Advertisement**) is the core unit of information
OSPF routers use to share routing information. Each LSA contains key
data that help build the **OSPF link-state database**, which is then
used to calculate the shortest path tree.

### Key information inside an LSA: 

Each LSA contains, at minimum:

-   Router ID -- The unique identifier of the router generating the LSA

-   Advertised Network Prefix -- The IP network/subnet the router wants
    to advertise.

-   Cost -- The OSPF metric (based on interface bandwidth) to r each the
    network from the advertising router.

**How does a router generate a unique Identifier?**

For routers, they use a type 1 LSA:

The router ID (RID) of the router creating the LSA is used as the unique
identifier.

This router ID is usually:

-   Manually configured (router-id 1.1.1.1), or

-   If not set manually, it's the highest IP address of any active
    loopback interface, or

-   If no loopbacks exist, it defaults to the highest IP address of any
    active physical interface.

    -   For example, G0/0 = 192.168.1.1 or G0/1 = 10.10.10.10

This ID ensures that LSA are uniquely identified across routers.

  -----------------------------------------------------------------------
  LSA Type                Identifier field        Explanation
  ----------------------- ----------------------- -----------------------
  Type 1 (router)         Router ID               Who originated it

  Type 2 (network)        DR's Router ID          The Designated Router
                                                  for that segment.

  Type ¾ (Summary)        Advertised network ID   The subnet being
                                                  summarised into another
                                                  area.

  Type 5 (External)       External route prefix   The external network
                                                  being advertised (e.g.,
                                                  from redistribution).
  -----------------------------------------------------------------------

To add further information into the LSA, they also include:

-   A sequence number (to track newer versions of an LSA).

-   Checksum (to validate integrity).

-   Age (helps with LSA expiration and flooding behaviour).

**For Type 1 LSAs, the unique identifier is the router ID of the router
generating it. For other types, it's specific to the kind of info being
advertised.**

The process of LSA to LSDB:

-   OSPF is enable on a router's interface. G1/0

-   The router creates an LSA to tell its neighbours about the network
    in G1/0

-   The LSA is flooded throughout the network until all routers have
    received it.

-   This result in all routers sharing the same LSDB -- Link State Data
    Base

-   Each router then uses the SPF algorithm (Dijkstra's algorithm) to
    calculate its best route to G1/0 (IP address).

-   There is expiration timer too, which is by default 30 mins before
    sending another LSA.

![A blue square with black text AI-generated content may be
incorrect.](media/image44.png){width="4.90625in"
height="1.3645833333333333in"}

Essentially there is three main steps for OSPF to function:

1.  **Become neighbours** with other routers connected to the same
    segment

2.  **Exchange LSAs** with the neighbour router

3.  **Calculate the best routes** to each destination, and insert the,
    into the routing table.

## OSPF Areas: 

OSPF uses **areas** to divide up the network. Think back to basic
routing with the New York and London setup. In OSPF, we could set New
York as area 1 and London as Area 2.

These two areas don't directly exchange all their LSA -- instead, they
communicate through Area 0, the backbone area, which is required for
inter-area communication.

Routers in each area build an LSDB (Link State Database) based on the
LSAs they receive, allowing them to learn about routes dynamically
without needing to manually configure static routes to every network at
each location.

**Areas:**

Let's break it down:

-   Small network can be ***single-area*** without any negative effects
    on performance.

-   In larger networks, a single-area design can have negative effects:

    -   The SPF algorithm takes more time to calculate routes

    -   The SPF algorithm requires exponentially more processing power
        on the routers.

    -   The larger LSDB takes up more memory on the routers

    -   Any small change in the network causes every router to flood
        LSAs and run the SPF algorithm again.

-   By dividing a large OSPF network into several smaller areas, you can
    avoid the above negative effects.

![A diagram of a diagram of areas AI-generated content may be
incorrect.](media/image45.png){width="6.268055555555556in"
height="3.511111111111111in"}

-   An **Area** is a set of routers and links that share the same LSBD

-   The **Backbone area** (area 0) is an area that all other areas must
    connect to.

-   Routers with all interfaces in the same area are called **internal
    routers.**

-   Router with interfaces in multiple areas are called **area border
    routers** (ABRs)

-   Routers connected to the backbone area (area 0) are called
    **backbone routers**.

    -   This includes ABRs.

-   An **intra-area route** is a route to a destination inside the same
    OSPF area.

-   An **interarea route** is a route to a destination in a different
    OSPF area.

> For example, these routers are ABRs:\
> \
> ![A screenshot of a computer screen AI-generated content may be
> incorrect.](media/image46.png){width="6.268055555555556in"
> height="3.511111111111111in"}

As they have an interface(s) point the internal routers and interface(s)
pointing to the external.

ABRs maintain a separate LSDB for each area they are connected to. It is
recommended that you connect an ABR to a maximum of 2 areas. Connecting
an ABR to 3 + areas can overburden the router.

### Further rules: 

-   OSPF areas should be *contiguous*.

    -   Meaning that each individual area should be connect, not divided
        up.

This is an example of a non-contiguous area and is not allowed in OSPF:

![A diagram of a network AI-generated content may be
incorrect.](media/image47.png){width="6.268055555555556in"
height="3.4854166666666666in"}

A contiguous area looks like this:

![A diagram of a diagram of areas AI-generated content may be
incorrect.](media/image48.png){width="6.268055555555556in"
height="3.511111111111111in"}

See area 1 isn't split up.

-   All OSPF areas must have at least one ABR connected to the backbone
    area.

-   OSPF interfaces in the same subnet must be in the same area.

    -   Think back to EIGRP (AS) number, the channel they're tuning
        into.

<https://www.youtube.com/watch?v=pvuaoJ9YzoI&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=53>

# OSPF Part 2: 

-   OSPF's metric is called **cost.** It is automatically calculated
    based on the bandwidth (speed) of the interface.

-   It is calculated by dividing a reference bandwidth value by the
    interface's bandwidth.

-   The default reference bandwidth is 100 Mbps.

    -   For example:

        -   **Reference**: 100 Mbps / interface: 10 Mbps = cost of 10

        -   **Reference**: 100 Mbps / interface: 100 Mbps = cost of 1

        -   **Reference:** 100 Mbps / interface: 1000 Mbps = cost of 1??

        -   **Reference:** 100 Mbps / interface: 10,000 Mbps = cost of
            1??

-   All value less than 1 will be converted to 1.

-   Therefore, Fast Ethernet, Gigabit Ethernet, 10 Gig Ethernet, etc.
    Are equal and all have a cost of 1 by default.

You can and SHOULD! Change the reference bandwidth with this command:

R1(config-router)# **auto-cost reference-bandwidth**
\<*megabits-per-second*\>

![A screenshot of a computer AI-generated content may be
incorrect.](media/image49.png){width="6.268055555555556in"
height="3.5006944444444446in"}

When setting the reference-bandwidth on a OSPF network, all OSPF routers
across the entire OSPF domain (not just the same area) should use the
same reference bandwidth.

Why?

-   OSPF uses **cost = reference bandwidth / interface bandwidth**

-   If routers have different reference bandwidth values, they'll
    calculate different OSPF costs for the same links, which leads to
    inconsistent routing decisions.

-   That breaks OSPF's goal of having synchronized link-state database
    across all routers.

OSPF cost:

-   One more option to change the OSPF cost of an interface is to change
    the bandwidth of the interface with the bandwidth command.

-   Changing the interface speed (bandwidth) does not actually change
    the speed of the interface it can physically operate at. It just
    changes the stated speed for OSPF cost purposes -- by default OSPF
    matches the speed.

    -   The bandwidth is just a value that is used to calculate OSPF
        cost, EIGRP metric, etc.

-   To change the speed at the interface operates, use the SPEED
    command.

Three ways to modify the OSPF cost:

1.  Change the reference bandwidth:

    a.  R1(config-router)# auto-cost reference-bandwidth
        *megabits-per-second*

2.  Manual configuration:

    a.  R1(config-router)# ip ospf cost *cost*

3.  Change the interface bandwidth:

    a.  R1(config-if)# bandwidth *kilobits-per-second*

        i.  Although not recommended

**Command:**

R1# show ip ospf interface bri

## OSPF Neighbours: 

Makin sure that routers successfully become OSPF neighbours is the main
task in configuring and troubleshooting OSPF. Once routers become OSPF
neighbours, they automatically do the work of sharing network
information, calculating routes, etc.

When OSPF is activated on a interface, the router starts sending OSPF
**hello** messages out of the interface at regular intervals (determined
by the **hello timer**). These are used to introduce the router to
potential OSPF neighbours.

-   The default **hello timer is 10 seconds** on an ethernet connection.

-   Hello messages are multicast to 224.0.0.5 (multicast address for all
    OSPF routers)

    -   A separate "channel" so the routers can talk to each other
        without "clogging" up the network we use to send and receive
        traffic.

        -   While not literally a "separate channel" the hello timers
            are dropped by non-OSPF routers/devices.

-   OSPF messages are encapsulated in an IP header, with a value of 89
    in the Protocol field.

### Down State: 

Scenario: state 1 - **down**

![A screenshot of a computer AI-generated content may be
incorrect.](media/image50.png){width="6.268055555555556in"
height="3.533333333333333in"}

We have two routers: R1 and R2. R1 has an interface with OSPF enable.

-   It sends a Hello packet:

    -   With it's RID (router ID) 1.1.1.1 with the neighbours RID.

        -   R1 does not know of R2 yet, so the Neighbours RID is set to
            0.0.0.0

![A screenshot of a computer AI-generated content may be
incorrect.](media/image51.png){width="6.268055555555556in"
height="3.5541666666666667in"}

State 2 -- **init state** (receiving the hello packet)

When R2 receives the Hello packet, it will add an entry for R1 to its
OSPF neighbour table.

-   In R2s neighbour table, the relationship with R1 is now in the
    **Init state**.

    -   **Init** state: Hello packet received, but own router ID is not
        in the Hello packet.

State 3: **2-way state**

![A screenshot of a computer AI-generated content may be
incorrect.](media/image52.png){width="6.268055555555556in"
height="3.5229166666666667in"}

![A screenshot of a message AI-generated content may be
incorrect.](media/image53.png){width="6.268055555555556in"
height="3.5409722222222224in"}

The **2-way state** means that:

-   the router has received a Hello packet with its own RID in it.

-   If both routers reach the 2-way state, it means that all the
    conditions have been met for them to become OSPF neighbours.

    -   They are now ready to share LSAs to build a common LSDB

Note: Think of it like the 3-way handshake process:

Synchronisation -- Synchronisation /Acknowledgement -- Acknowledgement

But as:

-   The routers see each other's Hello packet

-   They acknowledge that they can communicate

-   If eligible, they move forward to exchange LSAs and form an
    adjacency

Hello -- Hello back -- Let's talk

![A screenshot of a computer AI-generated content may be
incorrect.](media/image54.png){width="6.268055555555556in"
height="3.522222222222222in"}

DBD state -- who is the master and slave based on the RID of the routers

-   The Router with the greater RID (lowest) is the master.

Once this is done

### OSPF Neighbour State process: 

OSPF has been activated on a Router, it follows these next steps to
establish automatic routing:

-   1: **Down State**

    -   No Hello packets have been received yet.

    -   Router starts sending Hello packets to discover neighbours.

-   2: **init State**

    -   Hello packet received **without** the local router's RID in it.

    -   This means the neighbour is aware of you, but you're not listed
        yet as their neighbor

-   3: **2-way State**

    -   Hello packet received **with your own** **RID** include --
        neighbour recognises you.

    -   Bidirectional communication established.

    -   **DR/BDR** election happens here (in broadcast/multicast
        network).

    -   Routers that aren't DR/DBR stops here (non-adjacent neighbours).

-   4: **Exstart State**

    -   Routers negotiate Master/Slave roles (Based on highest RID).

    -   Begin forming adjacency

-   5: **Exchange State**

    -   Exchange **DBD (Databased Description)** packets.

    -   Summary of LSAs in the LSDB -- kind of like "Here's what I know,
        what do you have?"

-   6: **Loading State**

    -   Routers request missing LSA using **LSR (Link State Request)**

    -   Respond with **LSU (Link State Update)**

    -   Acknowledge using **LSAck.**

-   7: **Full State**

    -   LSDB fully synchronised

    -   Routers are now fully adjacent and can route based on complete
        OSPF topology

![A screenshot of a computer AI-generated content may be
incorrect.](media/image55.png){width="6.268055555555556in"
height="3.50625in"}

Essentially there is three main steps for OSPF to function:

1.  **Become neighbours** with other routers connected to the same
    segment

2.  **Exchange LSAs** with the neighbour router

3.  **Calculate the best routes** to each destination, and insert the,
    into the routing table.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image56.png){width="6.268055555555556in"
height="3.5236111111111112in"}

+----------------------+----------------------+-----------------------+
| Type:                | Name:                | Purpose:              |
+======================+======================+=======================+
| 1                    | **Hello**            | Neighbour discovery   |
|                      |                      | and maintenance.      |
+----------------------+----------------------+-----------------------+
| 2                    | **Database           | Summary of the LSDB   |
|                      | Description**        | of the router. Used   |
|                      |                      | to check if the LSDB  |
|                      | **(DBD)**            | of each router is the |
|                      |                      | same.                 |
+----------------------+----------------------+-----------------------+
| 3                    | **Link-State         | Request specific LSAs |
|                      | Request**            | from the neighbour    |
|                      |                      |                       |
|                      | **(LSR)**            |                       |
+----------------------+----------------------+-----------------------+
| 4                    | **Link-State         | Send specific LSAs to |
|                      | Update**             | the neighbour         |
|                      |                      |                       |
|                      | **(LSU)**            |                       |
+----------------------+----------------------+-----------------------+
| 5                    | **Link-State         | Used to acknowledge   |
|                      | Acknowledgement**    | that the router       |
|                      |                      | received a message.   |
+----------------------+----------------------+-----------------------+

### Recap:

-   Reference bandwidth / interface bandwidth = cost (values less than 1
    are converted to 1)

-   Default reference bandwidth = 100 Mbps

-   Modify the reference bandwidth:

    -   R1(config-if)# **auto-cost reference-bandwidth**
        *megabits-per-second*

-   Manually configure the cost of an interface:

    -   R1(config-if)# **ip ospf cost** *cost*

-   Modify the interface bandwidth:

    -   R1(config-if)# **bandwidth** *kilobits-per-second*

-   Total cost of *outgoing* interfaces = metric of the route

Becoming OSPF neighbours:\
\
![A screenshot of a computer AI-generated content may be
incorrect.](media/image55.png){width="6.268055555555556in"
height="3.50625in"}

More OSPF configurations:

-   Activate OSPF directly on an interface:

    -   R1(config-if)# **ip ospf** *process-id* **area** *area-id*

        -   Int g0/0

        -   Ip ospf 1 area 0

-   Configure all interfaces as passive interfaces by default:

    -   R1(config-router)# **passive-interface default**

    -   Then make specific interfaces non-passive by:

        -   **No** passive-interface ***interface***

# OSPF Part 3: 

**Purpose of Loopback Interfaces in OSPF:**

-   it's not reliant on a physical interface.

1.  *[Ensures a Stable Router ID (RID):]{.underline}*

    a.  OSPF uses the **highest IP address of a loopback** **interface**
        as the router ID by default.

    b.  If no Loopback is present, it uses the **highest IP of a
        physical interface** -- but physical interfaces can go down.

    c.  A loopback interface is **logical** and doesn't go down unless
        manually shut -- making the **RID stable and always reachable**.

2.  *[It's not exactly a Failover path, but More of an
    identifier:]{.underline}*

    a.  The **loopback IP isn't used as a destination in routing**
        unless you specifically advertise it into OSPF.

    b.  It doesn't help **route failover** between physical interfaces
        directly.

    c.  Hower, by advertising the loopback into OSPF, it gives a
        **reliable address to reach the router** itself (for things like
        router management, tunnel endpoints, iBGP neighbour
        relationships, etc).

## The Journey Analogy: 

-   **Loopback as a Signpost:**

    -   The loopback address is like a checkpoint or signpost that says,
        "I'm here. This is a stable place you can always find me."

    -   It's always up, regardless of the physical interfaces, like a
        reliable stop-off point on a long journey.

-   **Router ID as the "Destination":**

    -   In OSPF, when router use the loopback address, it's like saying,
        "here's my final destination point." This is where packets
        should be sent to reach the router.

    -   It's like knowing that the stop sign in the countryside will be
        there -- even if the other roads or routes may change or close
        due to traffic (e.g., physical interfaces going down).

-   **Physical Interfaces as Roads Along the journey:**

    -   The physical interfaces are like the roads you travel on -- they
        can go up or down, change, or even be closed temporarily.

    -   But as long as you pass through the "stop" sign (loopback) and
        know where it leads, you're still on the right path, even if
        road changes or is rerouted.

-   **Other Routers (Drivers) Following the Path:**

    -   Other routers will see the loopback address as the stable
        identifier for your router (the stop sign).

    -   They know that his is the reliable point in your network, and
        they will forward traffic accordingly, just like you'd follow
        signs on your journey even if some roads change.

## OSPF Network Types: 

The OSPF 'network types' refers to the type of connection between OSPF
neighbours (Ethernet, etc). There are three main OSPF network types:

-   **Broadcast:**

    -   Enabled by default on **Ethernet** and **FDDI** (Fiber
        Distributed Data Interfaces) interfaces.

-   **Point to Point:**

    -   Enabled by default on **PPP** (Point-to-Point Protocol) and
        **HDLC** (High-level Data Link Control) interfaces.

-   **Non-broadcast:**

    -   Enabled by default on **Frame Relay** and **X.25** interfaces

### Broadcast

![A diagram of a network AI-generated content may be
incorrect.](media/image57.png){width="6.268055555555556in"
height="2.046527777777778in"}

Example of a DR/BDR image - \[OSPF area 0\]

A DR (designated router) and BDR (backup designated router) must be
elected on each subnet (only DR if there are no OSPF neighbours, i.e.
R1's G1/0 interface)

Routers which aren't the **DR** or **BDR** become **DROther.**

**The multicast address for broadcast:** 224.0.0.5

Priority Process:

The DR/BDR election order of priority:

-   **1:** The highest ***OSPF interface priority***

    -   *However, all interfaces have the same priority by default.
        Priority is 1.*

-   **2:** The highest OSPF Router ID

'First Place' becomes the DR for the subnet, 'Second Place' becomes the
BDR

To change a routers priority in OSPF is:

Router(config)# int \<number\>

Router(config-if)# ip ospf priority ?

\<0-255\> Priority

Router(config-if)#**ip ospf priority 255**

If you set the OSPF interface priority to 0, the router CANNOT be the DR
or DBR for the subnet, no matter what.

-   If you change the priority to the highest priority after OSPF has
    already been established; the old roles which have been elected,
    keep them. Until OSPF is reset (the interface fails/is shut down,
    etc).

    -   This is because DR/BDR election is 'non-pre-emptive'.

To BE CONTINUED....

### Point-to-Point

![A diagram of a network AI-generated content may be
incorrect.](media/image58.png){width="6.268055555555556in"
height="2.042361111111111in"}

Example of a DR/BDR image - \[OSPF area 0\]

-   Enabled on **serial** interfaces using the **PPP** or **HDLC**
    encapsulations by default.

    -   PPP and HDLC are layer 2 encapsulations -- like ethernet but are
        used in serial connections.

-   Routers dynamically discover neighbours by sending/listening for
    OSPF Hello messages using **multicast address 224.0.0.5.**

-   A DR and BDR are not elected

-   These encapsulations are used for 'point-to-point' connections.

    -   Therefore, there is no point In electing a DR and BDR

-   The two routers will form a full adjacency with each other.

  -----------------------------------------------------------------------
  Broadcast:                          Point-to-Point:
  ----------------------------------- -----------------------------------
  Default on Ethernet, FDDI           Default on HDLC, PPP (Serial)
  interfaces                          interfaces

  DR/DBR elected                      No DR/DBR

  Neighbours dynamically discovered   Neighbours dynamically discovered

  Default timers: Hello 10, Dead 40   Default timers: Hello 10, Dead 40
  -----------------------------------------------------------------------

(non-broadcast network type default timers = Hello 30, dead 120)

### Common Issues: 

<https://www.youtube.com/watch?v=3ew26ujkiDI&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=57>

![A table with numbers and symbols AI-generated content may be
incorrect.](media/image59.jpeg){width="6.268055555555556in"
height="2.4125in"}

# First Hop Redundancy Protocols:

## Overview

Is a name given to a group (type) of protocols which makes up FHRP,
which are:

-   HSRP (Hot Standby Router Protocol)

-   VRRP (Virtual Router Redundancy Protocol)

-   GLBP (Gateway Load Balancing Protocol)

"A first hop redundancy protocol (FHRP) is a computer networking
protocol which is designed to protect the default gateway used on a
subnetwork by allowing two or more routers to provide backup for that
address; in the event of a failure of an active router, the backup
router will take over the address, usually within a few seconds." --
Wikipedia

The reason behind "First Hop" is it's normally the first hop (Default
Gateway) in the chain, traffic is being sent to.

How FHRP does this is, is through a Virtual IP (VIP) an IP address which
is shared between the two routers.

![A diagram of a network AI-generated content may be
incorrect.](media/image60.png){width="6.268055555555556in"
height="3.5215277777777776in"}

Then you set the default gateway on end devices, here the PC's to that
VIP.

The two routers negotiate the roles between each other through hello
(multicast) packets.

For example, R1 will become Active and R2 becomes Standby.

![A diagram of a network AI-generated content may be
incorrect.](media/image61.png){width="6.268055555555556in"
height="3.515972222222222in"}

Note: The Active and Standby terminology is specific to which FHRP is
being used.

When an end device sends an ARP request to find the MAC address of its
default gateway to send traffic outbound. R1 (active) will reply with a
unicast frame with the 'virtual MAC Address'; side note, each FHRP uses
a different virtual mac address.

What happens when R1 goes down?

R2 will stop receiving hello packets and assume R1 has gone down, then
elect itself as the active router. R2 will then send a broadcast:\
\
Gratuitous ARP -- ARP replies sent without being requested. (no ARP
request message was received)

Note: Normally an ARP reply (Router) is a unicast when received a
broadcast (PC) ARP Request. In Gratuitous ARP it is a broadcast.

This will make the switches update its mac address table to the "new"
backup router.

What's confusing me here is, why does this Gratuitous ARP broadcast
needs happen when both routers share the VIP and VMAC?

To answer this, the Switches map the VMAC to the port they are
forwarding traffic out of. So, the Gratuitous ARP broadcast is letting
the switches know which port to send traffic out of when traffic needs
to be outbound. Otherwise, they will send traffic to the router
associated with VMAC and port

![A diagram of a computer network AI-generated content may be
incorrect.](media/image62.png){width="6.268055555555556in"
height="3.509027777777778in"}

### Summary: 

-   A **virtual IP** is configured on the two routers, and a **virtual
    MAC** is generated for the virtual IP. (Each FHRP uses a different
    format for the virtual MAC)

-   An **active** router and a **standby** router are elected.
    (different FHRPs use different terms)

-   End hosts in the network are configured to use the virtual IP as
    their default gateway.

-   The active router replies to ARP requests using the virtual MAC
    address, so traffic destined for other networks will be sent to it.

-   If the active router fails, the standby becomes the next active
    router.

-   The new active router will send gratuitous ARP messages so that
    switches will update their MAC address tables. It now functions as
    the default gateway.

-   If the old active router comes back online, by default it won't take
    back its role as the active router. It will become the standby
    router.

-   You can configure 'pre-emption', so that the old active router does
    take back its old role.

## Hot Standby Router Protocol (HSRP)

-   It's Cisco Proprietary

-   An **active** and **standby** router are elected.

-   There are two versions: version 1 and version 2:

    -   Version 2 adds IPv6 support and increases the number of *groups*
        that can be configured.

-   Multicast IPv4 address:

    -   V1 = 224.0.0.2

    -   V2 = 224.0.0.102

-   Virtual MAC address:

    -   V1 = 0000.0c07.acXX (XX = HSRP group number)

    -   V2 = 0000.0c9f.fXXX (XXX = HRSP group number)

-   In a situation with multiple subnets/VLANs, you can configure a
    different active router in each subnet/VLAN to load balance.

![A diagram of a network AI-generated content may be
incorrect.](media/image63.png){width="6.268055555555556in"
height="3.5180555555555557in"}

### Command: 

Enabled on the interface.

**Standby**

## Virtual Router Redundancy Protocol (VRRP)

-   Open standard

-   A **master** and **backup** router are elected.

-   Multicast IPv4: 224.0.0.18

-   Virtual MAC address: 0000.5e00.01XX (XX = VVRP group number)

-   In a situation with multiple subnet/VLANs, you can configure a
    different master router in each subnet/VLAN to load balance.

![A diagram of a network AI-generated content may be
incorrect.](media/image64.png){width="6.268055555555556in"
height="3.545138888888889in"}

## Comparison Table

+-------------+-------------+-------------+-------------+-------------+
| FHRP:       | T           | Multicast   | Virtual     | Cisco       |
|             | erminology: | IP:         | MAC:        | P           |
|             |             |             |             | roprietary? |
+=============+=============+=============+=============+=============+
| HSRP        | Act         | V1:         | V1:         | Yes         |
|             | ive/Standby | 224.0.0.2   |             |             |
|             |             |             | 000         |             |
|             |             | V2:         | 0.0c07.acXX |             |
|             |             | 224.0.0.102 |             |             |
|             |             |             | V2:\        |             |
|             |             |             | 000         |             |
|             |             |             | 0.0c9f.fXXX |             |
+-------------+-------------+-------------+-------------+-------------+
| VRRP        | Ma          | 224.0.0.18  | 000         | No          |
|             | ster/Backup |             | 0.5e00.01XX |             |
+-------------+-------------+-------------+-------------+-------------+
| GLBP        | AVG / AVF   | 224.0.0.102 | 000         | Yes         |
|             |             |             | 7.b400.XXYY |             |
+-------------+-------------+-------------+-------------+-------------+

## Gateway Load Balancing Protocol (GLBP)

-   Cisco proprietary

-   Load balances among multiple routers [within a single
    subnet.]{.underline}

-   An AVG (Active Virtual Gateway) is elected.

-   Up to four AVFs (Active Virtual Forwarders) are assigned by the AVG
    (the AVG itself can be an AVF, too).

-   Each AVF acts as the default gateway for a portion of the hosts in
    the subnet.

-   Multicast IPv4: 224.0.0.102

-   Virtual MAC Address: 0007.b400.XXYY (XX = GLBP group number, YY =
    AVF number)

# TCP & UDP:

Functions of the layer 4: Transport in the OSI Model.

-   Provides transparent transfer of data between end hosts.

-   Provides (or doesn't provide) various services to applications:

    -   Reliable data transfer

    -   Error recovery

    -   Data sequencing

    -   Flow control

-   Provides layer 4 addressing (port numbers).

    -   Not the physical interfaces/ports on network devices.

    ```{=html}
    <!-- -->
    ```
    -   Identify the Application Layer protocol

    -   Provides session multiplexing

[Port Numbers / Session Multiplexing:]{.underline}

What is a session:

A session is an exchange of data between two or more communicating
devices.

For example, in your daily use of your computer it needs to be able to
handle multiple communication sessions at once. Perhaps you have
multiple internet tabs open, accessing different services over the
internet.

![A screen shot of a computer AI-generated content may be
incorrect.](media/image65.png){width="6.268055555555556in"
height="3.1243055555555554in"}

![A diagram of a cloud AI-generated content may be
incorrect.](media/image66.png){width="6.268055555555556in"
height="3.14375in"}

**Well-Known:** Port numbers 0 -- 1023 (services)

**Registered:** Port numbers 1024 -- 49151 (end hosts)

Although this is for the CCNA -- additional information regarding port
numbers for other systems still use port numbers but might allocate
their range of port numbers differently to what CISCO uses.

These are called ephemeral port numbers.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image67.png){width="6.268055555555556in"
height="3.107638888888889in"}

**<https://en.wikipedia.org/wiki/Ephemeral_port>**

**<https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers>**

**Ephemeral/private/dynamic:** port numbers 49152 -- 65535

## The Three-way handshake: 

**SYN -- SYN/ACK -- ACK**

## The Four-way handshake: 

While the three-way handshake is used to establish a TCP connection, the
four-way handshake is used to terminate it.

**FIN -- ACK - FIN -- ACK**

Port numbers:

  -----------------------------------------------------------------------
  TCP:                    UDP:                    TCP & UDP:
  ----------------------- ----------------------- -----------------------
  FTP data (20)           DHCP server (67)        DNS (53)

  FTP control (21)        DHCP client (68)        

  SSH (22)                TFTP (69)               

  Telnet (23)             SNMP agent (161)        

  SMTP (25)               SNMP manager (162)      

  HTTP (80)               Syslog (514)            

  POP3 (110)                                      

  HTTPS (443)                                     
  -----------------------------------------------------------------------

# IPv6: 

  -----------------------------------------------------------------------
  Decimal (IPv4)           Binary         Hexadecimal (IPv6)
  ------------------------ -------------- -------------------------------
  0                        **0000**       0

  1                        **0001**       1

  2                        **0010**       2

  3                        **0011**       3

  4                        **0100**       4

  5                        **0101**       5

  6                        **0110**       6

  7                        **0111**       7

  8                        **1000**       8

  9                        **1001**       9

  10                       **1010**       A

  11                       **1011**       B

  12                       **1100**       C

  13                       **1101**       D

  14                       **1110**       E

  15                       **1111**       F
  -----------------------------------------------------------------------

### Decimal to Hexadecimal: 

0b00101111 =

0b0010 -- 0b1111

0d2 -- 0d15

0x2 -- 0xF

0x2F

0b10000001 =

0b1000 -- 0b0001

0d8 -- 0d1

0x8 -- 0x1

0x81

### Hexadecimal to Binary:

0xEC =

0xE -- 0xC

0d14 -- 0d12

0b1110 -- 0b1100

0xEC = 0b11101100

0x2B =

0x2 -- 0xB

0d2 -- 0d11

0b0010 -- 0b1011

0x2b = 0b00101011

0xD7 =

0xD -- 0x7

0d13 -- 0d7

0b1101 -- 0b0111

0xD7 = 0b11010111

### Shortening IPv6 addresses:

  ---------------------------------------------------------------------------
  Full IPv6 Address:                        Shortened IPv6 Address:
  ----------------------------------------- ---------------------------------
  2000:AB78:0020:01BF:ED89:0000:0000:0001   2000:AB78: 20:1BF:ED89::1

  FE80:0000:0000:0000:0002:0000:0000:FBE8   FE80::2:0:0:FBE8

  AE89:2100:01AC:00F0:0000:0000:0000:020F   AE89:2100:1AC:F0::20F

  2001:0DB8:8B00:1000:0002:0BC0:0D07:0099   2001:DB8:8B00:1000:2:BC0:D07:99

  2001:0DB8:0000:0000:0000:0000:0000:1000   2001:DB8::1000
  ---------------------------------------------------------------------------

### Expanding shortened IPv6 addresses: 

  --------------------------------------------------------------------------
  Shortened IPv6 Address:          Full IPv6 Address:
  -------------------------------- -----------------------------------------
  FE80::1010:2FC:0:9               FE80:0000:0000:0000:1010:02FC:0000:0009

  2001:DB8:1:B23:2309::C1          2001:0DB8:0001:0B23:2309:0000:0000:00C1

  FD00::1000:689:9000:CDF          FD00:0000:0000:0000:1000:0689:9000:0CDF

  FF02::2                          FF02:0000:0000:0000:0000:0000:0000:0002

  ::1                              0000:0000:0000:0000:0000:0000:0000:0001
  --------------------------------------------------------------------------

## IPv6 (global unicast addresses) 

Most IPv6 networks use a /64 prefix, meaning:

-   The first 64 bits are the network portion

-   The last 64 bits are the interface identifier (like a host address)

Example:\
\
**2001:0DB8:8B00:1000:0002:0BC0:0D07:0099 /64**

Enterprises typically receive a /48 block (prefix) from their ISP:

-   This means the first 48 bits are fixed (the global routing prefix).

-   The next 16 bits (49-64) are yours to use for subnetting --
    highlight purple

**2001:0DB8:8B00:1000:0002:0BC0:0D07:0099 /64**

Which leaves a 16 bit "gap" to use to make subnets with. Highlighted
purple

Each Octet in an IPv6 address is 16 bits adding up to 128 bits total.

8 octets = 16x8 = 128 bits

Whereas IPv4 octets equate to 8 bits over 4 octets

4 octets = 8x4 = 32 bits

### Finding the IPv6 Prefix: 

2001:0DB8:8B00:0001:0000:0000:0000:0001 /64 -

2001:DB8:8B00:1:: /64

300D:00F2:0B34:2100:0000:1200:0001 /56 --

300D:00F2:0B34:2100:: /56 -- CANNOT REMOVE THOSE ZERO'S

2001:0DB8:8B00:0001:FB89:017B:0020:0011 /93

2001:0DB8:8B00:0001:FB89:017 = /92

B = 0D11

0d11

0b1011

0b1011

0b1000 -- change all host bits to 0 like in IPv4

0b1000 = 0b8

0d8

0x8

2001:0DB8:8B00:0001:FB89:0178 /93

2001:DB8:8B00:1:FB89:0178:: /93

Finding the IPv6 Prefix:

  -----------------------------------------------------------------------
  Host address:                             Prefix:
  ----------------------------------------- -----------------------------
  FE80:0000:0000:0000:4C2C:E2ED:6A89:2A27   FE80:: /9
  /9                                        

  -----------------------------------------------------------------------

FE (8)

8 = 0d8

0b1000

  -----------------------------------------------------------------------
  Host address:                              Prefix:
  ------------------------------------------ ----------------------------
  2001:0DB8:0001:0B23:BA89:0020:0000:00C1    2001:DB8:1:B23:: /64
  /64                                        

  -----------------------------------------------------------------------

  -----------------------------------------------------------------------
  Host address:                               Prefix:
  ------------------------------------------- ---------------------------
  2001:0DB8:0BAD:CAFÉ:1300:0689:9000:0CDF /71 2001:DB8:BAD:CAFÉ:1000::
                                              /71

  -----------------------------------------------------------------------

2001:0DB8:0BAD:CAFÉ:1 /70

:1300 =

0d3

0b0011

0b0000

0d0

0x0

2001:0DB8:0BAD:CAFÉ:1000 /71

Note: The reason I got it wrong, is I needed to have converted the whole
octet into binary to find the correct number. It wasn't 1000 it was
1200:: /71

  -----------------------------------------------------------------------
  Host address:                               Prefix:
  ------------------------------------------- ---------------------------
  2001:0DB8:0000:FEED:0DAD:018F:6001:0DA3 /62 2001:DB8::FEEC:: /62

  -----------------------------------------------------------------------

2001:0DB8:0000:FEE - /60

FEE (D) = 0d13

0b1101

0b1100

0d12

0xC

  -----------------------------------------------------------------------
  Host address:                                Prefix:
  -------------------------------------------- --------------------------
  2001:0DB8:9BAD:BABE:0DE8:AB78:2301:0010 /63  2001:DB8:9BAD:BABE:: /63

  -----------------------------------------------------------------------

2001:0DB8:9BAD:BAB /60

BAB (E)

0d14

0b1110

0d14

0xE

## Configuring IPv6 addresses:

2001:db8:0:0:: /64

![A screenshot of a computer AI-generated content may be
incorrect.](media/image68.png){width="4.625645231846019in"
height="5.156969597550306in"}

This IPv6 address range has been reserved for documentation and
examples.

They should never actually be used in real networks, but you're free to
use them in examples like in the image above.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image69.png){width="6.268055555555556in"
height="3.1375in"}

Link-Local Addresses start with FE80::

A Link-Local address is like the IPv4 LAN address.

# IPv6 Part 2:

Modified EUI-64 (technical term)

EUI = Extended Unique Identifier

What is (modified) EUI-64?

It's a method of converting a MAC address (48 bits) into a 64-bit
interface identifier. This interface identifier can then become the
'host portion' of a /64 IPv6 address.

How to convert the MAC address:

1.  Divide the MAC address in half:

    a.  For example, 1234 5678 90AB -- 1234 56 \| 78 90AB

2.  Insert FFFE in the middle:

    a.  1234 56FF \| FE78 90AB

3.  Invert the 7^th^ bit:

    a.  If the 7^th^ bit is a 0 convert it to a 1

    b.  if the 7^th^ bit is a 1 convert it to a 0.

4.  Where is the 7^th^ bit in this address:

    a.  1234 56FF FE78 90AB

        i.  Clue: Remember each letter/number represents 4 bits, which
            each octet totalling to 16 bits.

        ii. Before 1234 5678 90AB = 48 bits

        iii. After 1234 56FF FE78 90AB = 64 bits

    b.  7^th^ bit is: 1234 56FF FE78 90AB

        i.  In binary is: 0010

        ii. It's a 1, so convert it to a 0 = 0000

    c.  Convert the address back with the modified bit:

        i.  1034 56FF FE78 90AB

## Practice table:

+-----------------------------------+-----------------------------------+
| MAC Address:                      | EUI-64 Interface identifier:      |
+===================================+===================================+
| 782B CBAC 0867                    | 782B CBFF FEAC 0867:              |
|                                   |                                   |
|                                   | 0b1000 = 0b1010                   |
|                                   |                                   |
|                                   | 0b1010 = 0d10                     |
|                                   |                                   |
|                                   | 0d10 = 0xA                        |
|                                   |                                   |
|                                   | 7A2B CBFF FEAC 0867               |
+-----------------------------------+-----------------------------------+
| 0200 4C4F 4F50                    | 0200 4CFF FE4F 4F50:              |
|                                   |                                   |
|                                   | 0b0010 = 0b0000                   |
|                                   |                                   |
|                                   | 0b0000 = 0d0                      |
|                                   |                                   |
|                                   | 0d0 = 0x0                         |
|                                   |                                   |
|                                   | 0000 4CFF FE4F 4F50               |
+-----------------------------------+-----------------------------------+
| 0500 56C0 0001                    | 0500 56FF FEC0 0001               |
|                                   |                                   |
| Wrong MAC address from the video  | 0b0101 = 0b0111                   |
| but still got correct answer.     |                                   |
|                                   | 0b0111 = od7                      |
|                                   |                                   |
|                                   | 0d7 = 0x7                         |
|                                   |                                   |
|                                   | 0700 56FF FEC0 0001               |
+-----------------------------------+-----------------------------------+
| 00FF 6BA6 F456                    | 00FF 6BFF FEA6 F456               |
|                                   |                                   |
|                                   | 0b0000 = 0b0010                   |
|                                   |                                   |
|                                   | 0b0010 = 0b2                      |
|                                   |                                   |
|                                   | 0b2 = 0x2                         |
|                                   |                                   |
|                                   | 02FF 6BFF FEA6 F456               |
+-----------------------------------+-----------------------------------+
| 96AB 6D6B 98AE                    | 96AB 6DFF FE6B 98AE               |
|                                   |                                   |
|                                   | 0b0110 = 0b0101                   |
|                                   |                                   |
|                                   | 0b0101 = 0d5                      |
|                                   |                                   |
|                                   | 0d5 = 0x5                         |
|                                   |                                   |
|                                   | 95AB 6DFF FE6B 98AE               |
+-----------------------------------+-----------------------------------+

![](media/image70.png){width="6.268055555555556in"
height="3.5256944444444445in"}

![](media/image71.png){width="6.268055555555556in"
height="3.502083333333333in"}

## Why invert the 7^th^ bit? 

Mac addresses can be divided into two types:

-   UAA (Universally Administered Address)

    -   Uniquely assigned to the device by the manufacturer

-   LAA (Locally Administered Address)

    -   Manually assigned by an admin (with the mac-address command on
        the interface) or protocol. Doesn't have to be globally unique.

You can identify a UAA or LAA by the 7^th^ bit of the MAC address,
called the U/L bit (Universal/Local bit):

-   U/L bit set to 0 = UAA

-   U/L bit set to 1 = LAA

In the context of IPv6 addresses/EUI-64, the meaning of the U/L bit is
reversed:

-   U/L bit set to 0 = The MAC address the EUI-64 interface ID was made
    from was an LAA

-   U/L bit set to 1 = The MAC address the EUI-64 interface ID was made
    from was an UAA

## Global Unicast addresses: 

Global unicast IPv6 addresses are public addresses which can be used
over the internet. Which must be registered to be able to use them over
the internet, because they are public addresses, it is expected that
they are globally unique.

Like two homes, having the exact same address.

The range of addresses to be used for global unicast addresses,
originally defined as the 2000::/3 block (2000:: to
3FFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF).

Now defined as all addresses which aren't reserved for other purposes.
For example:

2001:0DB8:8B00:0001:0000:0000:0000:0001 /64

NETWORK/SUBNET/HOST PORTION

2001:0DB8:8B00: 48-bit 'global routing prefix' assigned by the ISP

0001: 16-bit 'subnet identifier', used by the enterprise to make various
subnets

-   These 16 bits allows for over 65,000 subnets to use -- more than
    enough for any enterprise.

2001:0DB8:8B00:0001 \| these two parts together make up the IPv6 network
prefix (/64)

:0000:0000:0000:0001 \| The host portion -- called the 'interface
identifier' in IPv6. This can be generated with EUI-64 as shown before,
or manually configured however you want.

1.  Global routing prefix : 2001:0DB8:8B00

2.  Subnet Identifier : 0001

3.  Interface identifier : 0000:0000:0000:0001

## Unique Local addresses: 

**Unique local** IPv6 addresses are private addresses which **cannot be
used over the internet.** You do not need to register to use them. They
can be used freely within internal networks and don't need to be
globally unique (\*). Can't be routed over the internet.

The address block used in unique local addresses is:

FC00::/7 (FC00:: to FDFF: FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF).

However, a later updated requires the 8^th^ bit to be set to 1, so the
first digits must be FD.

An example of a unique local address:

FD45:93AC:8A8F:0001:0000:0000:0000:0001 /64

FD = indicates a unique local address

45:93AC:8A8F = 40-bit 'global ID', which should be randomly generated.

-   Reason why randomly generated:

    -   Is when a company merges with another company, having a randomly
        generated 'unique' global ID means theirs less likely to cause
        issues in the network when they merge.

0001 = 16-bit 'subnet identifier', used by the enterprise to make
various subnets.

## Link Local Address: 

Link local IPv6 addresses are automatically generated on IPv6-enabled
interfaces.

Can use this command:

R1(config-if)# **ipv6 enable**

On an interface to enable IPv6 on that interface, which will
automatically generate a Link-Local address for that interface and be
the only address associated with that interface.

The address block used in link local addresses is:

FE80::/10 (FE80:: to FEBF: FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF).

However, the standard states that the 54 bits after FE80/10 should be
all 0s, so you won't see link addresses beginning with FE9, FEA, or FEB.
**Only FE8.**

![](media/image72.png){width="6.268055555555556in"
height="3.0458333333333334in"}

The interface ID is generated using the EUI-64 rules.

Link-Local means that these addresses are used for communication within
a single link (subnet). Routers WILL NOT route packets with a link-local
destination IPv6 address.

Common uses of link-local addresses:

-   Routing protocol peerings (OSPFv4 uses link-local addresses for
    neighbour adjacencies).

-   Next-hop addresses for static routes.

-   Neighbour Discovery Protocol (NDP, IPv6's replacement for ARP) uses
    Link-local addresses to function.

## Multicast Addresses: 

For review:

-   **Unicast** addresses are one-to-one

    -   One source to one destination

-   **Broadcast** addresses are one-to-all

    -   One source to all destination (within the subnet)

-   **Multicast** addresses are one-to-many

    -   One source to multiple destinations (that have joined the
        specific multicast group)

        -   Think of the OSPF protocol when routers share LSAs and
            LSDBs.

-   IPv6 uses range FF00::/8 for multicast (FF00:: to
    FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF).

-   **IPv6 doesn't use broadcast** (there is no 'broadcast address' in
    IPv6!)

  -----------------------------------------------------------------------
  Purpose:                IPv6 Address            IPv4 Address:
  ----------------------- ----------------------- -----------------------
  All nodes/hosts         FF02::1                 224.0.0.1
  (functions like                                 
  broadcast)                                      

  All routers             FF02::2                 224.0.0.2

  All OSPF routers        FF02::5                 224.0.0.5

  All OSPF DRs/BDRs       FF02::6                 224.0.0.6

  All RIP routers         FF02::9                 224.0.0.9

  All EIGRP routers       FF02::A                 224.0.0.10
  -----------------------------------------------------------------------

[Multicast address scopes:]{.underline}

IPv6 defines multiple multicast 'scopes' which indicate how far the
packet should be forwarded. The addresses in the table ab5ove all use
the 'link-local' scope (FF02), which stays in the local subnet.

This a different concept to IPv6 link-local address which begins with
FE80; these are IPv6 'multicast' addresses with a link-local scope:

IPv6 Multicast scopes

-   **Interface-local** (FF01): The packet doesn't leave the local
    device. Can be used to send traffic to a service within the local
    device.

    -   Meaning it can be used to send traffic to a service running
        within the local device, but the router won't send traffic out
        of a physical interface also known as 'node-local'.

-   **Link-local** (FF02): The packet remains in the local subnet.
    Routers will not route the packet between subnets.

-   **Site-local** (FF05): The packet can be forwarded by routers.
    Should be limited to a single physical location (not forwarded over
    WAN).

-   **Organisation-local** (FF08): Wider in scape than site-local (an
    entire company/organisation).

-   **Global** (FF0E): No boundaries. Possible to be routed over the
    internet.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image73.png){width="6.268055555555556in"
height="3.1909722222222223in"}

## Anycast Address:

Anycast Address is a 'one-to-one-of-many'

![A diagram of a network AI-generated content may be
incorrect.](media/image74.png){width="6.268055555555556in"
height="6.111805555555556in"}

**How does this work**?

Multiple routers are configured with the same IPv6 address.

They use a routing protocol to advertise the address.

When hosts send packets to that destination address, routers will
forward it to the nearest router configured with that IP address (based
on routing metric).

There is no specific address range for anycast addresses. Use a regular
unicast address (global unicast, unique local) and specify it as an
anycast address:

R1(config-if)#**ipv6 address 2001:db8:1:1::99/128 anycast**

What it looks like in the CLI:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image75.png){width="6.268055555555556in"
height="3.529861111111111in"}

## Other IPv6 Addresses: 

**::** = The unspecified IPv6 address

This means the address is all 0s and this syntax can be used when a
device doesn't yet know it's IPv6 address.

IPv6 default routes are configured with **::/0** which is the same as
IPv4s 0.0.0.0

**::1** = The loopback address

This the IPv6 loopback address. Used to test the protocol stack on the
local device.

Messages sent to this address are processed within the local device but
not sent to other devices.

IPv4 equivalent is 127.0.0.0/8 address range

# Day 32 IPv6 Part 2 configuration lab: 

We used the Link-Local address which found in the IP configuration of
PC1, alternatively could go to the command prompt and run ipconfig /all
to find it as well.

interface ID is:

260:70FF:FE35:C92E

Prefix is:

FE80::

So we need reverse engineer the engineer the interface ID:

260:70FF:FE35:C92E

0260:70FF:FE35:C92E becomes:

02:60:70:35:C9:2E or 0260:7035:C92E

We need to reverse the 7th bit to complete the process.

0260 is the first 16 bits.

02 = 8 bits

so, it sits in between the two numbers, meaning we need to convert this
decimal number into a binary number =

00000010

we can ignore the first 4 bits (0000) leaving us with:

0010

the 7th bit is the 1 in the binary. We flip it back to 0 becoming

0000

with this we can add this all back together to get the original MAC
address:

0060:7035:C92E

Long winded process to find the original MAC address, when I could have
done what I said at the top. Ipconfig /all would have given me the MAC
address.

To make a global-unicast address. Just replace the prefix (FE80::)with
the correct alternative prefix (2001:DB8::/64).

So, the prefix is 2001:DB8:: add 1 (2001:DB8::1/64) to the end of it to
be in the same subnet. If you do 2001:db8:0:1:..... that is a different
subnet.

## Note: 

Make sure to enable IPv6 routing in global config before doing the IPv6
on the interfaces, using this command:\
\
**ipv6 unicast-routing**

# IPv6 part 3: 

IPv6 Address Representation (correction)

RFC = Request for Comments

Is a publication from the ISOC (Internet Society) and associated
organisations like the IETF (internet Engineering Task Force), and are
the official documents of internet specifications, protocols,
procedures, etc.

RFC 5925 is a 'A recommendation for IPv6 Address Text Representation'.

## Solicited-Node Multicast Address: 

An IPv6 solicited-node multicast address is calculated from a unicast
address.

Ff02:0000:0000:0000:0000:0001:ff + Last 6 hex digits of unicast address.

For example:

2001:0db8:0000:0001:0f2a:4fff:fea3:00b1

Becomes ff02::1:ffa3:b1

This how you create a solicited-node multicast address.

Another example:\
\
2001:0db8:0000:0001:0489:4eda:073a:12ba

Becomes ff02::1:ff3a:12ba

![A screenshot of a computer AI-generated content may be
incorrect.](media/image76.png){width="6.268055555555556in"
height="3.5236111111111112in"}

## Neighbour Discovery Protocol: (NDP)

IPv6s version of IPv4s ARP.

The ARP-like function of NDP uses ICMPv6 and solicited-node multicast
addresses to learn the MAC address of other hosts. (ARP in IPv4 uses
broadcast messages)

In IPv6 version, there are two message types:

1.  Neighbour Solicitation (NS) = ICMPv6 type 135

2.  Neighbour Advertisement (NA) = ICMPv6 type 136 (equivalent to IPv4s
    ARP reply)

### Neighbour Solicitation (NS): 

![A screenshot of a computer AI-generated content may be
incorrect.](media/image77.png){width="6.268055555555556in"
height="3.5076388888888888in"}

Main difference to understand is the ARP request is a broadcast message,
whereas, an IPv6 NS is a multicast.

### Neighbour Advertisement (NA):

![A screenshot of a computer AI-generated content may be
incorrect.](media/image78.png){width="6.268055555555556in"
height="3.535416666666667in"}

The ARP table for IPv6 is called the IPv6 Neighbour Table:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image79.png){width="6.268055555555556in"
height="3.5083333333333333in"}

Another type of message which is allowed in Neighbour Discovery Protocol
(NDP) is routers automatically discover each other on the local network
using two messages:

**Router Solicitation (RS)** = ICMPv6 type 133

Sent to multicast address FF02::2 (all router).

Asks all router on the local link to identify themselves.

Sent when an interface is enable/host is connected to the network

**Router Advertisement (RA)** = ICMPv6 type 134

Sent to multicast address FF02::1 (all nodes)

The router announces its presence, as well as other information about
the link.

These messages are sent in response to RS messages.

They are also sent periodically, even if the router hasn't received a
RS.

![A black red and blue rectangle AI-generated content may be
incorrect.](media/image80.png){width="6.268055555555556in"
height="0.8138888888888889in"}

## SLAAC \| Stateless Address Auto-configuration

Hosts use the RS/RA messages to learn the IPv6 prefix of the local link
(i.e. 2001:db8::/64), and then automatically generate an IPv6 address.

When using the IPv6 address /eui-64 command, you need to manually enter
the prefix, but with **ipv6 address auto-config** command you don't need
to enter the prefix. The device will use NDP to learn the prefix used on
the local link via the RS and RA messaging.

### DAD \| Duplicate Address Detection 

Part of the NDP process.

Allows hosts to check if other devices on the local link are using the
same IPv6 address. Anytime an IPv6-enabled interface initialises (no
shutdown command), or an IPv6 address is configured on an interface.

It performs DAD. DAD uses two messages we learned earlier, NS and NA.
The host will send an NS to its own IPv6 address. If it doesn't get a
reply, it knows the address is unique. If it gets a reply, it means
another host on the network is already using the address.

For example, you might a see a message like this:\
![](media/image81.png){width="6.268055555555556in" height="0.16875in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image82.png){width="6.268055555555556in"
height="3.520138888888889in"}

# Security Fundamentals 

## Access control lists: 

What are ACLs?

As the name suggests it prevents or allows access to certain resources.
For example. Host A can access Server A but Host B cannot access Server
A.

A more technical explanation is: ACLs functions as a packet filer,
instructing the router to permit or discard specific traffic. Even if
the router has a route to the destination, the packet might be discarded
if the ACL tells router to do so.

ACLs can filter traffic based on source/destination IP addresses,
source/destination Layer 4 ports, etc.

![A computer screen shot of a diagram AI-generated content may be
incorrect.](media/image83.png){width="6.268055555555556in"
height="3.5319444444444446in"}

The order the ACLs are list are important -- think of firewall rules.
Top to bottom.

Configuring an ACL in global config mode will not make the ACL take
effect. It must be applied to an interface. Like how VLANs work.

Important note to add, is ACLs are applied either inbound or outbound.
Meaning traffic coming in or going out.

The best way to understand how the inbound and outbound rules on the
interfaces of the diagram above, is to think of the routers like a train
station.

**✅ Visualizing Inbound/Outbound ACLs: Train Station Analogy**

**Imagine each router interface as a gate at a train station.**

Let's say:

-   **PC1** (from subnet 192.168.2.0/24) wants to ping

-   **SRV1** (in subnet 10.0.0.0/24)

-   The packet goes through **R1** → **R2**

**🛤 R1 Interfaces**

-   G0/2 is connected to PC1\'s network

-   G0/0 leads toward R2

**🚦 What happens?**

1.  **PC1 sends a ping** --- the packet enters R1 through interface
    **G0/2**\
    → This is **inbound** on G0/2

2.  Router R1 **routes** the packet\
    → Then sends it out of interface **G0/0**\
    → This is **outbound** on G0/0

So, if you:

-   Apply an **inbound ACL** on G0/2 denying ICMP → the ping is blocked
    right at entry

-   Apply an **outbound ACL** on G0/0 denying ICMP → the ping is blocked
    as it\'s about to leave

Think of it like:

-   **Inbound = entering the station**

-   **Outbound = boarding the train to leave**

Important note to add: ACLs act like static routes, as in, if you
configure an ACL on one side you must do so for the other side as well.

For example:

You permit PC1 (192.168.1.10) to access Server1 (10.0.0.5) on R1's
**outbound** ACL:

access-list 100 permit Ip host 192.168.1.10 host 10.0.0.5

But the **return traffic** from Server1 → PC1 must also be allowed on
the **inbound** interface where the reply comes in, **if** there\'s an
ACL there.

If not:

-   The reply gets dropped

-   And it seems like the original request \"didn't work\"

## ACL types: 

Standard ACLs: Match based on **Source IP address** [only.]{.underline}

-   Standard Numbered ACLs

-   Standard Named ACLs

Extended ACLs: Match based on **Source/Destination IP,
Source/Destination port**, etc.

-   Extended Numbered ACLs

-   Extended Named ACLs

  -----------------------------------------------------------------------
  IPv4 ACL Type:                      Number Range / Identifier
  ----------------------------------- -----------------------------------
  Numbered Standard                   1-99, 1300-1999

  Numbered Extended                   100-199, 2000-2699

  Named (Standard & Extended)         Name
  -----------------------------------------------------------------------

<https://www.learncisco.net/courses/icnd-1/acls-and-nat/type-of-acls.html>

Command to configure a standard numbered ACL is:\
\
Name(Config)# **access-list** *number* **\[deny \| permit\]** *ip
wildcard-mask*

![A black rectangular sign with yellow text AI-generated content may be
incorrect.](media/image84.png){width="6.268055555555556in"
height="0.8569444444444444in"}

Different configuration options when setting a /32 subnet.

When configuring permit ACLs:

![](media/image85.png){width="6.268055555555556in"
height="0.5666666666666667in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image86.png){width="6.268055555555556in"
height="3.515277777777778in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image87.png){width="6.268055555555556in"
height="3.5430555555555556in"}

## Standard Named ACLs:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image88.png){width="6.268055555555556in"
height="3.5118055555555556in"}

![A computer screen shot of a computer diagram AI-generated content may
be incorrect.](media/image89.png){width="6.268055555555556in"
height="3.5548611111111112in"}

## Extended ACLs:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image90.png){width="6.268055555555556in"
height="3.540277777777778in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image91.png){width="6.268055555555556in"
height="3.5541666666666667in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image92.png){width="6.268055555555556in"
height="3.525in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image93.png){width="6.268055555555556in"
height="3.4833333333333334in"}

**Important note:** for extended ACLs the rule of thumb is the opposite
of standard ACLs.

Instead of placing the ACL as close to the target as possible, it
applying the ACL closest to the source.

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image94.png){width="6.268055555555556in"
height="3.4763888888888888in"}

**Rule of Thumb Recap:**

**Standard ACLs**

-   **Filter by source IP only**

-   **Place them close to the *destination***

-   Why: You can\'t specify what they\'re trying to reach, so placing it
    near the destination minimizes accidental overblocking

**Extended ACLs**

-   **Filter by source, destination, and protocol (ports)**

-   **Place them close to the *source***

-   Why: You can tightly control what\'s being blocked (e.g., HTTP to
    one server), and by placing it near the source, you avoid wasting
    bandwidth routing unwanted traffic across the network

**Example:**

You want to block **HTTP/HTTPS from 172.16.2.0/24 to SRV2
(192.168.2.100)**:

-   **Use an extended ACL** on **R2 Serial0/0/0 inbound** --- close to
    the source

-   That way only **those specific packets** are filtered, and other
    traffic can still flow freely

# CDP & LLDP

Cisco Discovery Protocol & Link Layer Discovery Protocol

CDP & LLDP are protocols which operate at layer 2, where they share
information with and discover information about neighbouring (connected)
devices.

This shared information includes host names, IP addresses, device type,
etc. This is a security risk and many network engineers decide to
disable it.

CDP is a cisco proprietary protocol.

LLDP is an industry standard protocol (IEEE 802.1AB).

CDP is enabled by default on cisco devices. These messages are
periodically sent to multicast MAC address **0100.0CCC.CCCC**. By
default message are sent every 60 seconds.

This message is held for 180 seconds, if a message is not received from
a neighbour within that time, the neighbour is removed from the CDP
neighbour table.

CDPv2 messages are sent by default.

There are 2 versions of CDP: CDPv1 & CDPv2

CDPv1 is old and will likely never be needed.

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image95.png){width="6.268055555555556in"
height="3.5104166666666665in"}

![A white and blue text on a white background AI-generated content may
be incorrect.](media/image96.png){width="6.268055555555556in"
height="3.561111111111111in"}

Additional commands:\
\
To enable/run CDP on a device, use these commands:\
\
To enable/disable CDP globally: \[no\] **cdp run**

To enable/disable CDP on specific interfaces: \[no\] **cdp enable**

Configure CDP timer: **cdp timer** *seconds*

Configure CDP holdtime: **cdp holdtime** *seconds*

Enable/disable CDPv2: \[no\] **cdp advertise-v2**

## LLDP:

LLDP is usually disabled on Cisco devices by default, so it must be
manually enabled.

A device can run CDP and LLDP at the same time.

LLDP messages are periodically sent to multicast MAC address
**0180.C200.000E.**

Same as CDP, the device receives an LLDP message and it processes, then
discards the message. It doe does not forward it to other devices. So,
only directly connected devices can become neighbours.

By default, LLDP message are sent once every 30 seconds. Faster than
CDP.

By default, the LLDP message hold time is 120 seconds.

**Configuration Commands:**

To enable it globally: **lldp run**

To enable it on specific interface (tx): **lldp transmit**

To enable it on specific interface (rx): **lldp receive**

Configure the LLDP timer: **lldp timer**

Configure the LLDP holdtime: **lldp holdtime**

Configure the LLDP reinit timer**: lldp reinit**

Pretty similar to CDP configuration, apart from the Interface commands.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image97.png){width="6.268055555555556in"
height="3.5305555555555554in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image98.png){width="6.268055555555556in"
height="3.515972222222222in"}

# Network Time Protocol (NTP)

![A screenshot of a computer AI-generated content may be
incorrect.](media/image99.png){width="6.268055555555556in"
height="3.527083333333333in"}

**Syslog**, the protocol used to keep device logs, will be covered
later.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image100.png){width="6.268055555555556in"
height="3.504861111111111in"}

Although the hardware calendar (built-in-clock) is the default
time-source, the hardware clock and software clock are separate and can
be configured separately.

## Hardware clock (calendar) Configuration: 

You can manually configure the hardware clock with the **calendar set**
command.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image101.png){width="6.268055555555556in"
height="3.53125in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image102.png){width="6.268055555555556in"
height="3.4833333333333334in"}

## Configuring Time Zone: 

![A screenshot of a computer AI-generated content may be
incorrect.](media/image103.png){width="6.268055555555556in"
height="3.5118055555555556in"}

## Summertime (Daylight Saving Time): 

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image104.png){width="6.268055555555556in"
height="3.50625in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image105.png){width="6.268055555555556in"
height="3.504861111111111in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image106.png){width="6.268055555555556in"
height="3.5in"}

## NTP:

Manually configuring the time on devices is not scalable. The manually
configured clocks will drift, resulting n inaccurate time. To fix this,
NTP allows automatic syncing of time over a network.\
\
NTP client requests the time from NTP servers. A device can be an NTP
server and an NTP client at the same time. NTP allows accuracy of time
within \~1 millisecond if the NTP server is in the same LAN, or with
\~50 milliseconds if connecting to the NTP server over a WAN/the
internet.

Some NTP servers are 'better' than others. The 'distance' of an NTP
server from the original **reference clock** is called **stratum**.

If the stratum is high, it is considered less accurate. NTP uses UDP
port 123 to communicate.

Reference Clocks:

A reference clock is usually a very accurate time device like an atomic
clock or a GPS clock. Reference clocks are **stratum 0** within the NTP
hierarchy.\
\
NTP servers directly connected to reference clocks are **stratum 1**.

![A diagram of a computer server AI-generated content may be
incorrect.](media/image107.png){width="6.268055555555556in"
height="3.484722222222222in"}\
Devices can also 'peer' with devices at the same stratum to provide more
accurate time. This also acts as a backup in case loose access to a
lower stratum NTP server. This mode is called 'symmetric active' mode.

Cisco devices can operate in three NTP modes:

-   Server mode

-   Client mode

-   Symmetric mode

They can be in all three of those modes at the same time. Additionally,
an NTP client can sync to multiple NTP servers.

![A diagram of a diagram AI-generated content may be
incorrect.](media/image108.png){width="6.268055555555556in"
height="3.5215277777777776in"}

## Configuration: Lab 37

To configure a router to reach out to an NTP server the command is:

**Ntp server** \<ip address\> in global config mode.

To see if it worked:\
\
**sh ntp status\
\
**To make R1 an NTP server for the 'internal network' for R2 and R3:\
\
global config mode

**Ntp master \<number\>**

![A screenshot of a computer AI-generated content may be
incorrect.](media/image109.png){width="6.268055555555556in"
height="3.5076388888888888in"}**\
\
**![A screenshot of a computer AI-generated content may be
incorrect.](media/image110.png){width="6.268055555555556in"
height="3.5083333333333333in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image111.png){width="6.268055555555556in"
height="3.563888888888889in"}

# Domain Name Service (DNS):

![A screenshot of a computer AI-generated content may be
incorrect.](media/image112.png){width="6.268055555555556in"
height="3.5444444444444443in"}

![A computer screen shot of a computer AI-generated content may be
incorrect.](media/image113.png){width="6.268055555555556in"
height="3.532638888888889in"}

![A screenshot of a computer command AI-generated content may be
incorrect.](media/image114.png){width="6.268055555555556in"
height="3.5125in"}

# Dynamic Host Configuration Protocol (DHCP)

Maybe I'll fill this out later.

## DHCP Relay: 

# Simple Network Management Protocol (SNMP)

+----------------------+----------------------+-----------------------+
| Message Class:       | Description:         | Messages:             |
+======================+======================+=======================+
| Read                 | Messages sent by the | Get\                  |
|                      | NMS to read the      | GetNext\              |
|                      | managed devices.     | GetBulk               |
|                      | (Ie. What's your     |                       |
|                      | current CPU usage    |                       |
|                      | %?)                  |                       |
+----------------------+----------------------+-----------------------+
| Write                | Messages sent by the | Set                   |
|                      | NMS to change        |                       |
|                      | information on the   |                       |
|                      | managed devices.     |                       |
|                      | (ie. Change an IP    |                       |
|                      | address)             |                       |
+----------------------+----------------------+-----------------------+
| Notification         | Messages sent by the | Trap                  |
|                      | managed devices to   |                       |
|                      | alert the NMS of a   | Inform                |
|                      | particular event.    |                       |
|                      | (ie. Interface going |                       |
|                      | down)                |                       |
+----------------------+----------------------+-----------------------+
| Response             | Messages sent in     | Response              |
|                      | responses to a       |                       |
|                      | previous             |                       |
|                      | message/request      |                       |
+----------------------+----------------------+-----------------------+

SNMP Agent = UDP 161

SNMP Manager = UDP162\
\
![A screenshot of a computer AI-generated content may be
incorrect.](media/image115.png){width="6.268055555555556in"
height="3.1368055555555556in"}

# Syslog:

## Syslog severity Levels:

  ----------------------------------------------------------------------------
  **Level:**   **Keyword:**            **Description:**
  ------------ ----------------------- ---------------------------------------
  **0**        **Emergency**           System is unusable

  **1**        **Alert**               Action must be taken immediately

  **2**        **Critical**            Critical conditions

  **3**        **Error**               Error Conditions

  **4**        **Warning**             Warning conditions

  **5**        **Notice**              Normal but significant
                                       **(Notification)**

  **6**        **Informational**       Information messages

  **7**        **Debugging**           Debug-level messages
  ----------------------------------------------------------------------------

Destination port for syslog messages is **UDP 514**

![A screen shot of a computer AI-generated content may be
incorrect.](media/image116.png){width="6.268055555555556in"
height="3.4965277777777777in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image117.png){width="6.268055555555556in"
height="3.511111111111111in"}

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image118.png){width="6.268055555555556in"
height="3.5083333333333333in"}

**Syslog** is used for message logging.

> Events that occur within the system are categorised based on
> facility/severity and logged.\
> Used for system management, analysis, and troubleshooting.
>
> Messages are sent from the devices to the server. The server can't
> actively pull information from the device (like SNMP Get) or modify
> variables (like SNMP Set).

**SNMP** is used to retrieve and organise information about the SNMP
managed devices.

IP addresses, current interface status, temperature, CPU usage, etc.

SNMP server can use **Get** to query the clients and **Set** to modify
variables on the clients.

# Telnet & SSH:

On a Cisco device, whether it's a switch or a router; there is a
**console port** that allows direct physical access to configure the
device without needing a network connection.

Without console port security, anyone with physical access (such as
opportunistic or disgruntled staff) could connect to the device and
potentially make unauthorized changes. To prevent this, you can
configure **console login security** by setting a password and enabling
login on the console line.

You can also create **local user accounts** for added security, which is
a better practice than using just a simple line password.

**To configure basic console port security:**

conf t

line console 0

password \<your_password\>

login

exit

-   password \<your_password\> sets the password.

-   login tells the device to require a password on the console line.

After this, test the configuration by disconnecting and reconnecting via
the console port. If prompted for a password and access is granted, save
the configuration:

write memory

or

copy running-config startup-config

**For stronger security:**

Instead of using just a line password, you can configure a **local user
account** and force the console line to use **local authentication**:

username admin secret \<strong_password\>

line console 0

login local

-   login local tells the console line to use the local user database
    (instead of just the line password).

-   secret is encrypted in the config, unlike password.

For added security you can add:\
\
exec-timeout 0 0\
\
the first 0 represents minutes and the second 0 represents seconds.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image119.png){width="6.268055555555556in"
height="3.172222222222222in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image120.png){width="6.268055555555556in"
height="3.517361111111111in"}

![](media/image121.png){width="6.268055555555556in"
height="0.46805555555555556in"}

FQDN = Fully Qualified Domain Name (host name + domain name)

![A screenshot of a computer AI-generated content may be
incorrect.](media/image122.png){width="6.268055555555556in"
height="3.5166666666666666in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image123.png){width="6.268055555555556in"
height="3.535416666666667in"}

# FTP & TFTP:

File transfer Protocol & Trivial File transfer Protocol:

The main function of these protocols is to transfer files over a
network.

They both use a client-server model:

-   Clients can use FTP or TFTP to copy files from a server.

-   Clients can use FTP or TFTP to copy files to a server.

As a network engineer, the most common use for FTP/TFTP is in the
process of upgrading the operating system of a network device.

TFTP servers listen on **UDP port 69.**

Although UDP is not a reliable protocol to transfer files, however,
within the TFTP protocol there are built-in features which makes it more
reliable than standard.

TFTP Process:

Every TFTP data message is acknowledged.

-   If the client is transferring a file to the server, the server will
    send Ack messages.

-   If the server is transferring a file to the client, the client will
    send Ack messages.

Timers are used, and if an expected message isn't received in time, the
waiting device will resend its previous message.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image124.png){width="6.268055555555556in"
height="2.678472222222222in"}

TFTP file transfers have three phases:

-   1: Connection: TFPT client sends a request to the server, and the
    server responds back, initialising the connection.

-   2: Data Transfer: The client and server exchange TFTP messages. One
    send data and the other send acknowledgments.

-   3: Connection Termination After the last data message has been sent,
    a final acknowledgement Is sent to terminate the connection.

TFTP TID:

When the client sends the first message to the server, the destination
port is UDP 69 and the source is an ephemeral port.

This random port is called a "Transfer Identifier" (TID) and identifies
the data transfer.

The server then also selects a random TID to use as the source port when
it replies, not 69.

When the client sends the next message, the destination port will be the
server's TID, not 69.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image125.png){width="6.268055555555556in"
height="2.847916666666667in"}

FTP:

i.  FTP used TCP ports 20 and 21

ii. Usernames and passwords are used for authentication, however there
    is no encryption.

iii. For greater security, FTPS (FTP over SSL/TLS) can be used.

iv. SSH file transfer protocol (SFTP) can also be used for greater
    security

v.  FTP is more complex than TFTP and allows not only file transfers,
    but clients can also navigate file directories, add and remove
    directories, list files, etc.

vi. The client sends FTP commands to the server to perform these
    functions.

FTP uses two types of connections:

-   An FTP control connection (TCP 21) is established and used to send
    FTP commands and replies.

-   When files or data are to be transferred, a separate FTP data
    (TCP 20) connections are established and terminated as needed.

![A close-up of a computer screen AI-generated content may be
incorrect.](media/image126.png){width="6.268055555555556in"
height="2.767361111111111in"}

The default method of establishing FTP data connections is active mode,
In which the server initiates the TCP connection.

![A close-up of a data connection AI-generated content may be
incorrect.](media/image127.png){width="6.268055555555556in"
height="2.5659722222222223in"}

Both connections are active without terminating the other.

FTP Passive mode:

In FTP passive mode, the client initiates the data connection. This is
often necessary when the client is behind a firewall, which could block
the incoming connection from the server.

![A close-up of a computer screen AI-generated content may be
incorrect.](media/image128.png){width="6.268055555555556in"
height="3.3340277777777776in"}

  -----------------------------------------------------------------------
  FTP                                 TFPT
  ----------------------------------- -----------------------------------
  Users TCP (20 for data, 21 for      Uses UDP (69) for connectionless
  control) for connection-based       communication (although a basic
  communication                       form of 'connection' is used within
                                      the protocol itself)

  Clients' ca use FTP commands to     Clients can only copy files to or
  perform various actions, not just   from the server.
  copy files.                         

  Username/Password authentication    No authentication

  More complex                        Simpler
  -----------------------------------------------------------------------

![A screenshot of a computer program AI-generated content may be
incorrect.](media/image129.png){width="6.268055555555556in"
height="3.5381944444444446in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image130.png){width="6.268055555555556in"
height="3.5368055555555555in"}

![A screen shot of a computer AI-generated content may be
incorrect.](media/image131.png){width="6.268055555555556in"
height="3.504166666666667in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image132.png){width="6.268055555555556in"
height="3.4875in"}

# NAT: Part 1

NAT is used to translate the source and/or destination IP address of a
packet to a different IP address.

-   Private IPv4 addresses

-   Intro to NAT

-   Static NAT

-   Static NAT Configuration

Private IPv4: (RFC 1918)\
\
There isn't enough IPv4 address for all device that need an IP address
in the modern world. The long-term solution is to switch to IPv6;
although IPv6 is not widely adopted to date, and IPv4 is still used in
most networks.

There are three main short-term solutions:

-   CIDR: Classless inter-domain routing

-   Private IPv4 addresses

-   NAT

RFC (Request for Comment) 1918 specifies the following IPv4 ranges as
private:

-   10.0.0.0/8 (10.0.0.0 to 10.255.255.255)

-   172.16.0.0/12 (172.16.0.0 to 172.31.255.255)

-   192.168.0.0/16 (192.168.0.0 to 192.168.255.255)

These, if you remember are from the class-based system:

-   Class A

-   Class B

-   Class C

One thing you may notice about the IP addresses above, is the /subnet
masks for each class looks odd. The answer for this, is they are simply
address "ranges" -- from & to.

You are free to use these addresses in your networks. They don't have to
be globally unique.

You test this by using ipconfig on your PC.

These are private IP addresses for a reason and cannot access the
internet. This Is why we use NAT which translates internal private IP
addresses to a globally unique IPv4 address. This unique address is a
shared address used for all internal end devices.

## Network Address Translation (NAT) 

Network Address Translation is used to modify the source and/or
destination IP addresses of packets.\
\
There are various reasons to use NAT, but the common reason is to allow
host with private IP addresses to communicate with other hosts over the
internet.

For the CCNA you must understand **source NAT** and how to configure it
on Cisco routers.\
\
\
![A screenshot of a computer AI-generated content may be
incorrect.](media/image133.png){width="6.268055555555556in"
height="1.895138888888889in"}\
\
Static NAT involves statically configuring one-to-one mappings of
private IP addresses to public IP addresses *--*

*an inside local IP address is mapped to an inside global IP address.*

![A close-up of a number AI-generated content may be
incorrect.](media/image134.png){width="6.268055555555556in"
height="1.0347222222222223in"}

![A screenshot of a computer AI-generated content may be
incorrect.](media/image135.png){width="6.268055555555556in"
height="2.6819444444444445in"}

## Static NAT configuration:

Static NAT allows devices with private IP addresses to communicate over
the internet. However, because it requires a one-to-one IP address
mapping, it doesn't help preserve IP addresses.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image136.png){width="6.268055555555556in"
height="3.51875in"}

Remember you cannot use any public IP address like you can with private
IP addresses, you must own the public IP address.

**Inside local:** The IP address of the inside host, from the
perspective of the local network \*the IP address configured on the
inside host, usually a private address.

**Inside global:** The IP address of the inside host, from the
perspective of outside hosts \*the IP address of the inside host after
NAT, usually a public address.

**Outside local:** The IP address of the outside host, from the
perspective of the local network.

**Outside global:** The IP address of the outside host, from the
perspective of the outside network.

**Inside/Outside** = Location of the host

**Local/Global** = Perspective

![A screenshot of a computer screen AI-generated content may be
incorrect.](media/image137.png){width="6.268055555555556in"
height="1.6458333333333333in"}

![A screenshot of a computer screen AI-generated content may be
incorrect.](media/image138.png){width="6.268055555555556in"
height="2.1590277777777778in"}

![A screen shot of a computer AI-generated content may be
incorrect.](media/image139.png){width="6.268055555555556in"
height="1.6256944444444446in"}

# NAT: Part 2

Things we'll cover:

-   More about static NAT

-   Dynamic NAT

-   Dynamic PAT

![A screenshot of a computer AI-generated content may be
incorrect.](media/image140.png){width="6.268055555555556in"
height="3.527083333333333in"}

**Inside - outside**

This one-to-one mapping of the internal IP to a global IP isn't just for
inside to outside, this allows external hosts to also gain access to the
internal via the inside global address.

**Note:** A good example to remember is when I did the NAT on the
fortigate, which allowed specific external hosts to RDP into internal
resources (servers). I have a 100+ page training document I did as well,
showing every step.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image141.png){width="6.026529965004374in"
height="3.3644674103237096in"}

**Outside -- Inside**

## Dynamic NAT:

In dynamic NAT, the router dynamically maps *inside local addresses* to
*inside global addresses* as needed.

The router makes those mappings automatically and then clears the
mapping when its no longer needed. How it works in Cisco IOS. An ACL us
used to identify which traffic should be translated.

This part is important, as this not your typical use of an ACL.

ACLs can be used to indicate which traffic should be forwarded and which
should be blocked. While this is their primary function, ACLs can also
be used to identify traffic.\
\
If the source IP of a packet is permitted by the ACL, the source IP will
be translated by NAT.

If the source IP of a packet is denied by the ACL, the source IP will
NOT be translated. However, this does not mean the traffic will be
dropped.

A NAT pool is used to define the available inside global addresses. For
example:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image142.png){width="5.677876202974629in"
height="1.6460629921259842in"}

Although they are dynamically assigned, the mappings are still
one-to-one (*one **inside** local IP address* per *inside **global** IP
address*).

If there are not enough inside global IP addresses available; meaning
all are being currently used, it is called '**NAT pool exhaustion**'.

What happens if another inside IP address needs translated?

Due to the pool exhaustion, the traffic will be dropped until one
becomes available.\
\
Further detail:\
\
Meaning the dynamic NAT pool will automatically time out entries if not
used, or you can clear them manually.

![A screenshot of a computer screen AI-generated content may be
incorrect.](media/image143.png){width="6.268055555555556in"
height="3.5in"}

First entry timed out:\
![A screenshot of a computer AI-generated content may be
incorrect.](media/image144.png){width="6.268055555555556in"
height="3.4930555555555554in"}

## Dynamic NAT configuration:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image145.png){width="6.268055555555556in"
height="3.5083333333333333in"}

Dynamic NAT mappings have a default timer of 24 hours and each time a
translation is made the timer resets.

## PAT (NAT Overload)

**PAT** translates both the IP address and, if necessary, the port
number.\
The purpose of using unique port numbers is to allow a single public IP
address to be shared by many internal hosts.\
\
it's like **apartment numbers in the same building**.

![A diagram of a cloud computing system AI-generated content may be
incorrect.](media/image146.png){width="6.268055555555556in"
height="2.3402777777777777in"}

## PAT configuration:

![A screenshot of a computer AI-generated content may be
incorrect.](media/image147.png){width="6.268055555555556in"
height="3.5208333333333335in"}

## PAT configuration (interface)

The difference with this configuration compared with the previous
configuration is you use the interface rather than specifying a pool.\
\
![A screenshot of a computer AI-generated content may be
incorrect.](media/image148.png){width="6.268055555555556in"
height="3.5180555555555557in"}\
\
![A computer screen shot of a diagram AI-generated content may be
incorrect.](media/image149.png){width="6.268055555555556in"
height="3.5381944444444446in"}

## Command Review:  ![A screenshot of a computer command AI-generated content may be incorrect.](media/image150.png){width="6.268055555555556in" height="3.5069444444444446in"}

# Quality of Server (QoS):
