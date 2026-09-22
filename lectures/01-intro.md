# Introduction

## The Internet: Nuts and Bolts

The internet consists of billions of connected computing devices:

* Hosts are end systems (any end user device), running network apps at the "edge" of the internet.

Packet switches are devices that forward **packets** (chunks of data):

* Routers
* Switches (L2 switches)

Communication links:

* fiber, copper, radio, satellite
* *transmission rate*: bandwidth

Networks are collections of devices, L2 switches, routers, and/or links that are **managed by an organization**.

The internet can be thought of as a "network of networks", with interconnected ISPs (internet service providers).

Protocols are communication rules, which are **everywhere**:

* Responsible for the sending and receiving of messages.
* ex: HTTP, TCP, IP, WiFi, 4G, Ethernet

## The Internet: Services

The internet:

* is **infrastructure** that provides services to applications
  * Web, streaming video, email, social media, etc.
* provides **programming interfaces** to distributed applications
  * "hooks" that allow sending/receiving apps to "connect" to
  * provide service options analagous to postal service

## Protocols

> Protocols define the format of messages, order of messages sent and received among network entities, and actions taken on message transmission and receipt.

A protocol is a set of communication rules. Two entities communicate by exchanging messages.

Network protocols govern all communication activites in the internet.

## Internet Structure

### Network Edge

* Hosts: clients and servers.
* Servers often in data centers.

### Access Networks and Physical Media

* The "front portion" of the network that connects the user with the Internet: links, switches, routers.
* Wired and wireless communication links.

### Network Core

* Interconnected routers.
* Network of networks.

## Host

A **packet** is a fundamental concept on the internet.

A host sending function:

* Takes an application message ($M$).
* Breaks $M$ into packets (structured sequence of bits) of length $L$ bits.
* Transmits a packet (bit-by-bit) into access network (the first link) at transmission rate $R$ (also known as link capacity or link bandwidth).

The process of packet transmission incurs some delay, known as **packet transmission delay**.

$$
\text{Packet transmission delay = time needed to transmit L-bit packet into link = } \frac{L}{R}
$$

## Links

* Bit: propogates between transmitter(Tx)/receiver(Rx) pairs.
* Physical link: what lies between transmitter and receiver.
* Guided media: signals propogate in solid media (copper, fiber, coax).
* Unguided media: signals propogate freely (radio).
* Twisted pair: two insulated copper wires.

### Coaxial Cable

* Two concentric copper conductors.
* Bidirectional.
* Broadband:
  * Multiple frequencies on cable.
  * Hundreds of Mbps per channel.

### Fiber Optic Cable

* Glass fiber carrying light pulses, each pulse a bit.
* High-speed operation:
  * High-speed point-to-point transmission (tens to hundreds of Gbps).
* Low bit error rate, therefore repeaters spaced far apart (~100 km).
* Immune to electromagnetic noise.

Bit errors occur if a received bit has been flipped.

$$
\text{Bit Error Rate} = \frac{\text{\# of bit errors at receiver}}{\text{\# of bits transmitted}}
$$

### Wireless Radio

* Signal carried in various "bands" in electomagnetic spectrum (900 Mhz, 1800 Mhz, 2.4 GHz, etc.).
* No physical "wire".
* Broadcast, "half-duplex" (can't transmit AND receive at the same time).
* Propagation environment effects:
  * Reflection.
  * Obstruction by objects.
  * Interference or noise.

### Radio Link Types

* Wireless LAN (WiFi):
  * Tens to hundreds of Mbps over tens of meters.
* Wide-area (4G Cellular):
  * Tens of Mbps over tens of kilometers.
* Bluetooth:
  * short distances and limited rates.
* Terrestrial Microwave:
  * Point-to-point, 45 Mbps channels.
* Satellite:
  * Up to 45 Mbps per channel.
  * 270 ms end-to-end delay.

## Network Core: Packet Switching

The network core is a mesh of interconnected routers.

Packet-switching is the process by which hosts break application-layer messages into independent packets.

The network forwards packets from one router to the next, across links on path from source to destination.

There are **two key** network core functions:

* **Forwarding**: move an arriving packet from a router's input link to an appropriate output link (local action).
* **Routing**: determine source-destination paths taken by packets (global action).
  * Routing algorithms create forwarding tables (routing tables).

A router continuously updates its routing table. When the router receives a packet, it forwards the packet based on the current routing table.

## Packet Switching

Store-and-forward refers to the idea that an entire packet must arrive at a router before it can be transmitted on the next link.

Queueing occurs when work arrives faster than it can be serviced. In the case of packets, this occurs when arrival rate (bps) exceeds transmission rate (bps) for some period of time.

In this case, packets will queue for transmission, and they can be dropped (packet loss) if memory (buffer) in a router fills up.

## Circuit Switching

Circuit switching is an alternative to packet switching. End-to-end resources are allocated to and reserved for a "call" between a source and destination.

* Resources can include buffer space, link bandwidth, and processing power.
* Each link is divided into separate circuits (channels).
* Dedicated resources provide circuit-like, guaranteed performance.
* A circuit segment is idle when it is not being used by the call; resources are not shared.
* Circuit switching was commonly used in traditional telephone networks.

### Frequency Division Multiplexing

In **frequency division multiplexing (FDM)**, optical or electromagnetic frequencies are divided into narrow frequency bands.

* Each call is allocated its own band.
* A call can transmit at the maximum rate of its allocated band.

### Time Division Multiplexing

In **time division multiplexing (TDM)**, time is divided into slots.

* Each call is allocated one or more periodic slots.
* During its slot, a call can transmit at the maximum rate of the wider frequency band.

GSM (Global System for Mobile Communications) networks use a combination of FDM and TDM.

## Packet Switching versus Circuit Switching

Consider a $1$ Gb/s link with $N$ users. Each user:

* accesses the network at $100$ Mb/s when active;
* is active $10\%$ of the time.

With circuit switching, the link supports:

$$
\frac{1\text{ Gb/s}}{100\text{ Mb/s}} = 10 \text{ users}
$$

With packet switching, the link can support many more than $10$ users because users do not transmit continuously. For example, with $35$ users, the probability that more than $10$ are active at the same time is less than $0.0004$.

Packet switching is well suited to **bursty data**:

* Resource sharing allows users to share buffer space and link capacity.
* There is no call setup, so no extra messages are exchanged before data transfer.

However:

* Excessive congestion can cause packet delay and loss due to buffer overflow.
* Protocols are needed for reliable data transfer and congestion control.

## Internet Structure: A Network of Networks

Hosts connect to the Internet through access ISPs. Access ISPs must themselves be interconnected so that any two hosts, anywhere, can send packets to one another.

Connecting every access ISP directly to every other access ISP does not scale because it requires $O(N^2)$ connections.

### Global Transit ISPs

One option is to connect each access ISP to a global transit ISP.

* Access ISPs are customer ISPs.
* The global ISP is a provider ISP.
* Customer and provider ISPs have an economic agreement.

If one global ISP is a viable business, competitors will also want to be connected. ISPs can connect through:

* **Internet exchange points (IXPs)**;
* **peering links**, which directly connect networks.

Regional networks may arise to connect access networks to larger ISPs. Content provider networks, such as Google, Microsoft, or Akamai, may also run their own networks to bring services and content close to end users.

At the center of the Internet are a small number of well-connected large networks:

* Tier-1 commercial ISPs provide national and international coverage.
* Content provider networks connect their data centers to the Internet, often bypassing tier-1 and regional ISPs.

## Packet Delay and Loss

Packets queue in router buffers while waiting for their turn to be transmitted.

* Queue length grows when the arrival rate temporarily exceeds the output link capacity.
* Packet loss occurs when the memory available for queued packets fills up.
* A lost packet may be retransmitted by the previous node, by the source end system, or not at all.
* Retransmission decisions are protocol specific.

### Four Sources of Packet Delay

The total nodal delay is:

$$
d_{\text{nodal}} = d_{\text{proc}} + d_{\text{queue}} + d_{\text{trans}} + d_{\text{prop}}
$$

* $d_{\text{proc}}$: nodal processing delay
  * checks for bit errors;
  * determines the output link;
  * is typically less than a few microseconds.
* $d_{\text{queue}}$: queueing delay
  * time waiting at the output link for transmission;
  * depends on the congestion level of the router.
* $d_{\text{trans}}$: transmission delay
  * time required to push the packet into the link.
* $d_{\text{prop}}$: propagation delay
  * time required for a bit to propagate across the physical link.

The transmission delay is:

$$
d_{\text{trans}} = \frac{L}{R}
$$

where $L$ is the packet length in bits and $R$ is the link transmission rate in bits per second.

The propagation delay is:

$$
d_{\text{prop}} = \frac{d}{s}
$$

where $d$ is the physical link length and $s$ is the propagation speed, approximately $2 \times 10^8$ m/s.

Transmission delay and propagation delay are different: transmission delay depends on packet length and link rate, while propagation delay depends on link length and signal propagation speed.

### Propagation Delay Examples

For a $100$ m campus link:

$$
d_{\text{prop}} = \frac{100}{2 \times 10^8} = 0.5\ \mu\text{s}
$$

For a $500$ km national link:

$$
d_{\text{prop}} = \frac{500 \times 10^3}{2 \times 10^8} = 2.5\ \text{ms}
$$

For a roughly $12{,}000$ km international link:

$$
d_{\text{prop}} = \frac{12{,}000 \times 10^3}{2 \times 10^8} = 60\ \text{ms}
$$

### Queueing Delay and Traffic Intensity

Let:

* $a$ be the average packet arrival rate;
* $L$ be the packet length in bits;
* $R$ be the link bandwidth in bits per second.

The traffic intensity is:

$$
\frac{La}{R}
$$

* If $La/R \approx 0$, average queueing delay is small.
* As $La/R \to 1$, average queueing delay becomes very large.
* If $La/R > 1$, work arrives faster than it can be serviced, so the average delay becomes infinite.

### Traceroute

The `traceroute` program measures delay from a source to each router along an end-to-end path toward a destination.

For router $i$:

1. The sender transmits three probes with the IP packet TTL field set to $i$.
2. Router $i$ returns the probes to the sender.
3. The sender measures the interval between transmission and reply, $t_2 - t_1$.

This measured interval is the round-trip delay. A `*` means that a probe received no response because the probe was lost or the router did not reply.

## Throughput

**Throughput** is the rate, in bits per unit time, at which bits are received by a destination from a sender.

* Instantaneous throughput is measured over a small period of time.
* Average throughput is measured over a longer period of time.

For a server-to-client path with server access rate $R_s$ and client access rate $R_c$:

* If $R_s < R_c$, the average end-to-end throughput is $R_s$.
* If $R_s > R_c$, the average end-to-end throughput is $R_c$.

The **bottleneck link** is the link on an end-to-end path that constrains end-to-end throughput.

If $10$ connections fairly share a backbone link with capacity $R$, the per-connection end-to-end throughput is:

$$
\min\left(R_c, R_s, \frac{R}{10}\right)
$$

In practice, $R_c$ or $R_s$ is often the bottleneck.

## Protocol Layers

Networks are complex systems containing hosts, routers, links with different media, applications, protocols, hardware, and software. Layering organizes these pieces into a structured reference model.

An analogy is air travel. An end-to-end trip involves several services:

* ticketing;
* baggage handling;
* gates;
* runways;
* airplane routing.

Each layer implements a service through its own internal actions and relies on services provided by the layer below.

Layering helps support:

* explicit identification of system components and their relationships;
* seamless evolution, such as IPv4 to IPv6;
* scalability, such as adding a new tier-1 network;
* maintenance and updating, because changes within one layer can be transparent to the rest of the system.

## Layered Internet Protocol Stack

### Application Layer

Supports network applications.

* HTTP
* IMAP (Internet Message Access Protocol)
* SMTP (Simple Mail Transfer Protocol)
* DNS (Domain Name System)

### Transport Layer

Provides process-to-process data transfer.

* TCP (Transmission Control Protocol)
* UDP (User Datagram Protocol)

### Network Layer

Routes IP packets, or datagrams, from source to destination machines.

* IP
* Routing protocols

### Link Layer

Transfers data between neighboring network elements, such as hosts and switches.

* Ethernet
* 802.11 (WiFi)
* PPP (Point-to-Point Protocol)

### Physical Layer

Moves individual bits "on the wire".

## Encapsulation

Each layer adds its own header to the data received from the layer above.

1. The application layer creates a message $M$.
2. The transport layer encapsulates $M$ with transport header $H_t$ to create a segment:

   $$
   [H_t \mid M]
   $$

   The transport header can contain sequence numbers, acknowledgements, and error-checking information.
3. The network layer encapsulates the segment with network header $H_n$ to create a datagram (IP packet):

   $$
   [H_n \mid H_t \mid M]
   $$

   The network header can contain source and destination IP addresses, an error-checking code, and the time-to-live (TTL) field.
4. The link layer encapsulates the datagram with link header $H_l$ to create a frame:

   $$
   [H_l \mid H_n \mid H_t \mid M]
   $$

The physical layer transmits the frame as bits. At the destination, headers are processed and removed in the reverse order until the original message $M$ reaches the application.

Switches are transparent to the source host and router in this end-to-end view. Routers process the network-layer datagram and create new link-layer frames for the next hop.

Encapsulation provides modularity and protects data using layer-specific control information, but every header adds overhead. Example header sizes include:

* TCP header: $20+$ bytes;
* IP header: $20+$ bytes;
* Ethernet header: $14+$ bytes.
