# QUIZ

What is not in the network edge? 
End-systems
Access networks
Routers
Tier-1 ISPs

True or false? Propagation delay is a function of the distance and the medium.

True or false? Propagation delay is a function of the distance and the medium.

What is the most popular physical medium used in access networks?
Coaxial cable
Twisted pair
Fiber optic cable
Wireless

True or false? Transmission delay is a function of the distance.

True or false? Queueing delay is a function of the distance.

True or false? A bottleneck link on the path from a sender to a receiver is fixed, regardless of the time of the day or cross traffic.

True or false? On a path from a sender to a receiver, a bottleneck link refers to the most constrained link and may change over time.

With whom did Vint Cerf win the Turing Award?
Robert Kahn
Jeffrey Hinton
David Patterson
Robert Metcalfe

Please sort the following events in a correct chronological order.
The first TCP/IP connection was established between a PDP-11 at Seoul National University and a VAX11/780 at ETRI in Gumi via a 1200bps modem?
KT (Korea Telecom) was first established.
The Telecommunications Act of 1996 in the US added the Internet to American regulation of broadcasting and telephony.
Jun Murai established the first TCP/IP connection in Japan.

What does an application-layer protocol define? Mark all that apply.
Sender
Types of messages exchanged
Message syntax
Message semantics
Rules
Receiver

What is used to identify a process in an end host in networking applications? Mark all that apply.
IP address
Port number
PID
Ethernet address

What does RTT stand for?

Is HTTP stateless?Yes or No?

Persistent HTTP saves on TCP connection setup overhead over non-persistent HTTP. Yes or no?

Who sets the HTTP cookie?
Web server
Client's browser
Router
Switch

Where are your cookies on your smartphone saved?

What is the MX type in a DNS RR for?
Mail server
IP address
Name server
Canonical name

Yes or no? KAIST runs the authoritative name server and the local DNS server on separate machines.

Yes or no. DNS has a hierarchy of two layers: root servers and TLD servers.

Yes or no? Hostname to IP address mappings are cached at the local DNS servers with TTLs.

In BitTorrent, a file is chopped into chunks and a peer may receive chunks from multiple peers. In order to prevent selfish peers from leaving after only receiving from other peers and not sending any chunk out, what policy does BitTorrent employ?
Tit-for-tat; a peer unchoke only those top peers that are sending chunks at highest rates.
A peer must serve twice or more chunks as it has received so far before leaving.
Peers choose other peers randomly to download chunks from.

What does TTL stand for?

Name a non-electronic item that comes with a TTL.

If the .com TLD server address has a TTL value of 24hrs and there are 10 million DNS queries for .com domain per hour, then how many DNS queries should the local DNS server send to the .com TLD server in a day?
1
24
10 million
10 million x 24

At the receiver, the UDP layer uses only the destination port number for demultiplexing. Yes or no?

A UDP socket receives packets from not only a single IP address and a port number pair, but multiple pairs of IP addresses and port numbers. Yes or no?

In the UDP header, there is a sequence number field. Yes or no? 

In the UDP header, there is a checksum field. Yes or no?

In the UDP header, there is a length field. Yes or no?

In rdt 1.0 to 3.0 we have relaxed assumptions about the underlying channel from fully reliable to unreliable, step by step. First, we relaxed the assumption that the channel has no bit errors. In order to deal with bit errors in the forward data channel, what mechanism is added? Mark all that apply.
Checksum
ACK/NACK
Sequence Number
Timer

In rdt 3.0 we relaxed yet another assumption about packet loss and the underlying channel would lose packets. It is the role of the sender to figure out if the packet has been lost or not in transit. What mechanism does the sender use to detect a packet loss?
Checksum
ACK/NACK
Sequence Number
Timer

At the receiver, the TCP layer uses both the source and the destination IP addresses and the source and destination port numbers for demultiplexing. Yes or no?

What is the meaning of ack # of N in TCP?
Packets up to sequence number N have been received at the receiver.
Packets up to N have been sent out at the sender.
Packets up to sequence number N-1 have been received at the receiver and the
receiver is expecting a packet w/ sequence number of N.

When does the sender receive duplicate ACKs? Mark all the applies.
When the receiver receives packets with a gap in the sequence number.
When a timer goes off at the receiver for the next packet.
When a timer goes off at the sender and the sender retransmits only a single packet.

Yes or no. The rwnd field in the TCP header is for flow control.

How does a TCP sender infer packet loss? Mark all that apply.
Timer expiration
Multiple duplicate acks
Increased RTT measurement
Decreased RTT measurement

Yes or no. TCP RTT is fixed as a constant of the initial 3-way handshake RTT.

Yes or no. TCP's timeout value is based on RTT estimates. 

Yes or no. The rwnd field in the TCP header is for flow control.

How does TCP achieve fairness among sessions through a common bottleneck?
AIMD
AIAD
MIAD
MIMD

Yes or no? QUIC runs on top of TCP.

Strict AIMD has a long lead time to reach the maximum available bandwidth of today's high-speed Internet. What are _not_ the mechanisms that different flavors of TCP have adopted to improve performance over AIMD.
Slow start
Fast retransmit
Flow control
3-way handshake

Yes or no. QUIC multiplexes several different application-level "streams" into a single QUIC connection.

Yes or no. QUIC runs its own reliable data transfer on top of TCP. This way, QUIC data transfer is super reliable.

Yes or no. Microsoft and Google run different flavors of TCP within their datacenters.

What is not a function of input ports at a router?
line termination
link layer protocol implementation
forwarding table lookup
switching

Where can queueing take place at a router? Mark all that apply.
Input port
Switching fabric
Output port

If the forwarding table is as below, which entry will the IP address 11001000 00010111 00011001 10101010 match to?
11001000 00010111 00010*** ********
11001000 00010111 00011*** ********
11001000 00010111 00011000 ********
11001000 00010111 00011001 ********
11001000 00010111 00010001 10*******

Name at least two scheduling policies used at routers.

Can a router interface support both IPv4 and IPv6? Yes or No?

When a IPv6 tunnel is set up in an IPv4 network, IPv6 packets are encapsulated in IPv4 datagrams and travel the IPv4 network. Yes or No?

The first DHCP discover message is broadcast to the subnet with the source IP address of 255.255.255.255 and the destination IP address of 255.255.255.255. Yes or No?

What is the IP address that is used in broadcast?
0.0.0.0
8.8.8.8
143.248.255.255
255.255.255.255

What is the scope of an IP packet with a broadcast destination address?
Internet
AS (Autonomous System)
subnet
neighbor hosts

## Quiz Answers

**What is not in the network edge?**
- **Routers** - Routers are typically considered part of the network core, not the edge. The network edge generally includes hosts and end-systems like PCs, smartphones, and local networks, rather than the routing centers of the internet.

**True or false? Propagation delay is a function of the distance and the medium.**
- **True** - Propagation delay is influenced by the length of the path the signal must travel and the propagation speed of the medium (such as copper wire, fiber optic cable, or air).

**What is the most popular physical medium used in access networks?**
- **Twisted pair** - Historically and currently, twisted pair cables are widely used in access networks, especially for telephone and Ethernet networks, due to their cost-effectiveness and sufficient performance for broad ranges of applications.

**True or false? Transmission delay is a function of the distance.**
- **False** - Transmission delay depends on the data rate of the link and the size of the data being transmitted, not the distance over which the data travels.

**True or false? Queueing delay is a function of the distance.**
- **False** - Queueing delay is influenced by the traffic load and the capacity of the links, not directly by the distance.

**True or false? A bottleneck link on the path from a sender to a receiver is fixed, regardless of the time of the day or cross traffic.**
- **False** - Bottleneck links can vary depending on the volume of traffic and the network conditions at different times, making them dynamic rather than fixed.

**True or false? On a path from a sender to a receiver, a bottleneck link refers to the most constrained link and may change over time.**
- **True** - A bottleneck link is the link with the lowest capacity along a path and can indeed change over time due to varying network conditions and traffic patterns.

**With whom did Vint Cerf win the Turing Award?**
- **Robert Kahn** - Vint Cerf, along with Robert Kahn, won the Turing Award for their pioneering work on the design and implementation of the Internet’s basic communications protocols, TCP/IP.

**Please sort the following events in a correct chronological order.**
1. **KT (Korea Telecom) was first established.**
2. **The first TCP/IP connection was established between a PDP-11 at Seoul National University and a VAX11/780 at ETRI in Gumi via a 1200bps modem.**
3. **Jun Murai established the first TCP/IP connection in Japan.**
4. **The Telecommunications Act of 1996 in the US added the Internet to American regulation of broadcasting and telephony.**
- The chronological order reflects the sequence of developments, starting with foundational establishments, initial connections, and leading up to broader regulatory changes.

**What does an application-layer protocol define? Mark all that apply.**
- **Types of messages exchanged**
- **Message syntax**
- **Message semantics**
- **Rules**
- Application-layer protocols define how data is structured (message syntax), what the data means (message semantics), the types of messages that can be sent and received, and the rules for managing communication.

**What is used to identify a process in an end host in networking applications? Mark all that apply.**
- **Port number**
- **PID**
- In networking, a process is typically identified by a port number which is used alongside an IP address to direct network traffic to specific applications. The PID (Process ID) is also used internally within an operating system to identify processes.

**What does RTT stand for?**
- RTT stands for **Round-Trip Time**, which is the time it takes for a signal to travel from the source to a destination plus the time it takes for an acknowledgment of that signal to return to the source.

**Is HTTP stateless?**
- **Yes**, HTTP is stateless, meaning each request from a client to server is treated as new, with no memory of past interactions.

**Persistent HTTP saves on TCP connection setup overhead over non-persistent HTTP. Yes or no?**
- **Yes**, persistent HTTP saves on TCP connection setup overhead because it reuses the same connection for multiple requests and responses, rather than establishing a new connection for each request.

**Who sets the HTTP cookie?**
- **Web server**
- A web server sets an HTTP cookie, which is then stored on the client's browser.

**Where are your cookies on your smartphone saved?**
- Cookies on a smartphone are saved in the device's internal memory within the specific browser's storage used to access websites.

**What is the MX type in a DNS RR for?**
- **Mail server**
- MX records in DNS (Domain Name System) are used to specify mail servers responsible for receiving email messages on behalf of a domain.

**Yes or no? KAIST runs the authoritative name server and the local DNS server on separate machines.**
- Without specific information on KAIST’s DNS infrastructure, I can’t confirm whether they run the authoritative and local DNS servers on separate machines, but it is common practice to do so for reasons of load management and security.

**Yes or no. DNS has a hierarchy of two layers: root servers and TLD servers.**
- **No**, DNS hierarchy includes more than just root servers and TLD (Top-Level Domain) servers; it also includes authoritative name servers, making it more than a two-layer hierarchy.

**Yes or no? Hostname to IP address mappings are cached at the local DNS servers with TTLs.**
- **Yes**, local DNS servers cache mappings of hostnames to IP addresses with Time To Live (TTL) values, which dictate how long the information should be stored before being refreshed.

**In BitTorrent, a file is chopped into chunks and a peer may receive chunks from multiple peers. In order to prevent selfish peers from leaving after only receiving from other peers and not sending any chunk out, what policy does BitTorrent employ?**
- **Tit-for-tat; a peer unchoke only those top peers that are sending chunks at highest rates.**
- BitTorrent employs a tit-for-tat strategy to encourage cooperation among peers by favoring those who contribute more to the network.

**What does TTL stand for?**
- TTL stands for **Time To Live**, a mechanism that limits the lifespan or the number of hops that data packets can take before they are discarded by a network router.

**Name a non-electronic item that comes with a TTL.**
- A non-electronic example of TTL can be seen in perishable goods such as food items which have a "best before" date.

**If the .com TLD server address has a TTL value of 24hrs and there are 10 million DNS queries for .com domain per hour, then how many DNS queries should the local DNS server send to the .com TLD server in a day?**
- **1**
- Only one query per day needs to be sent to the TLD server if the TTL is set for 24 hours, assuming the data does not change.

**At the receiver, the UDP layer uses only the destination port number for demultiplexing. Yes or no?**
- **Yes**, UDP uses the destination port number to determine which application process should receive incoming packets.

**A UDP socket receives packets from not only a single IP address and a port number pair, but multiple pairs of IP addresses and port numbers. Yes or no?**
- **Yes**, UDP sockets can receive packets from multiple pairs of IP addresses and port numbers, as UDP is connectionless and does not maintain a dedicated connection state.

**In the UDP header, there is a sequence number field. Yes or no?**
- **No**, there is no sequence number field in the UDP header.

**In the UDP header, there is a checksum field. Yes or no?**
- **Yes**, the UDP header does include a checksum field.

**In the UDP header, there is a length field. Yes or no?**
- **Yes**, the UDP header includes a length field, which specifies the length of the UDP header plus the UDP data.

**In rdt 1.0 to 3.0 we have relaxed assumptions about the underlying channel from fully reliable to unreliable, step by step. First, we relaxed the assumption that the channel has no bit errors. In order to deal with bit errors in the forward data channel, what mechanism is added? Mark all that apply.**
- **Checksum**
- **ACK/NACK**

Checksums are used to detect errors in data, and ACK/NACK messages are used to indicate whether data was received correctly or needs to be resent.

**In rdt 3.0 we relaxed yet another assumption about packet loss and the underlying channel would lose packets. It is the role of the sender to figure out if the packet has been lost or not in transit. What mechanism does the sender use to detect a packet loss?**
- **Timer**

In rdt 3.0, timers are used to detect packet loss. If an ACK is not received within a certain time frame, the packet is assumed lost and resent.

**At the receiver, the TCP layer uses both the source and the destination IP addresses and the source and destination port numbers for demultiplexing. Yes or no?**
- **Yes**, TCP uses both source and destination IP addresses and port numbers to correctly route and deliver data to the appropriate application.

**What is the meaning of ack # of N in TCP?**
- **Packets up to sequence number N-1 have been received at the receiver and the receiver is expecting a packet with sequence number N.**

**When does the sender receive duplicate ACKs? Mark all that applies.**
- **When the receiver receives packets with a gap in the sequence number.**

**Yes or no. The rwnd field in the TCP header is for flow control.**
- **Yes**, the rwnd (receive window) field in the TCP header is used for flow control, indicating how much more data the receiver can handle.

**How does a TCP sender infer packet loss? Mark all that apply.**
- **Timer expiration**
- **Multiple duplicate acks**
- These mechanisms help infer packet loss by signaling that a packet has not been acknowledged within the expected time, or when multiple duplicate ACKs are received for the same data.

**Yes or no. TCP RTT is fixed as a constant of the initial 3-way handshake RTT.**
- **No**, TCP's RTT is not fixed but dynamically calculated based on ongoing measurements as data packets are sent and acknowledgments are received.

**Yes or no. TCP's timeout value is based on RTT estimates.**
- **Yes**, TCP’s timeout value for retransmissions is dynamically calculated based on RTT estimates to adapt to network conditions.

**How does TCP achieve fairness among sessions through a common bottleneck?**
- **AIMD (Additive Increase Multiplicative Decrease)**
- AIMD is a congestion control algorithm used by TCP to ensure fairness and efficient use of network resources.

**Yes or no? QUIC runs on top of TCP.**
- **No**, QUIC runs on top of UDP, not TCP.

**Strict AIMD has a long lead time to reach the maximum available bandwidth of today's high-speed Internet. What are _not_ the mechanisms that different flavors of TCP have adopted to improve performance over AIMD.**
- **3-way handshake**

**Yes or no. QUIC multiplexes several different application-level "streams" into a single QUIC connection.**
- **Yes**, QUIC supports multiplexing multiple streams over a single connection.

**Yes or no. QUIC runs its own reliable data transfer on top of TCP. This way, QUIC data transfer is super reliable.**
- **No**, QUIC provides its own reliability mechanisms but runs on top of UDP, not TCP.

**Yes or no. Microsoft and Google run different flavors of TCP within their datacenters.**
- **Yes**, large tech companies often use custom or modified TCP implementations to optimize performance within their datacenters.

**What is not a function of input ports at a router?**
- **forwarding table lookup**
- Forwarding table lookup is typically a function of the routing processor, not the input ports.

**Where can queueing take place at a router? Mark all that apply.**
- **Input port**
- **Switching fabric**
- **Output port**
- Queueing can occur at all these locations within a router.

**If the forwarding table is as below, which entry will the IP address 11001000 00010111 00011001 10101010 match to?**
- **11001000 00010111 00011001 **********
- This entry matches the given IP address because it matches the most specific prefix.

**Name at least two scheduling policies used at routers.**
- **Round-robin**
- **Weighted fair queuing**

**Can a router interface support both IPv4 and IPv6? Yes or No?**
- **Yes**, modern router interfaces can support both IPv4 and IPv6.

**When an IPv6 tunnel is set up in an IPv4 network, IPv6 packets are encapsulated in IPv4 datagrams and travel the IPv4 network. Yes or No?**
- **Yes**, this describes the process of IPv6 tunneling over an IPv4 network.

**The first DHCP discover message is broadcast to the subnet with the source IP address of 255.255.255.255 and the destination IP address of 255.255.255.255. Yes or No?**
- **Yes**, the DHCP discover message is broadcast using the IP address 255.255.255.255.

**What is the IP address that is used in broadcast?**
- **255.255.255.255**

**What is the scope of an IP packet with a broadcast destination address?**
- **subnet**
- Broadcasts are typically confined to a single subnet to limit network congestion.