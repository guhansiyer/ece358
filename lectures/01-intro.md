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

## Network Core

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
