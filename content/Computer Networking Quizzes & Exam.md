
**1. Yes or no? According to the Dijkstra's link state algorithm, individual routers have the complete topology of the network for shortest-path computation.**
- **Answer:** Yes
- **Explanation:** Dijkstra의 링크 상태 알고리즘에 따르면 개별 라우터는 최단 경로 계산을 위해 네트워크의 전체 토폴로지를 갖고 있습니다.

**2. Yes or no? In a distance vector routing algorithm, individual routers compute paths to the rest of the network via updates from neighboring routers.**
- **Answer:** Yes
- **Explanation:** 거리 벡터 라우팅 알고리즘에서는 개별 라우터가 인접 라우터로부터 받은 업데이트를 통해 네트워크의 나머지 부분으로의 경로를 계산합니다.

**3. Yes or no? Routing protocols based on shortest-path algorithms run between ASes (Autonomous Systems).**
- **Answer:** No
- **Explanation:** 최단 경로 알고리즘에 기반한 라우팅 프로토콜은 주로 AS 내부에서 사용됩니다. AS 간에는 BGP와 같은 프로토콜이 사용됩니다.

**4. Yes or no? The KAIST network shares one AS number with a couple of neighboring institutions.**
- **Answer:** No
- **Explanation:** KAIST 네트워크는 인접 기관들과 AS 번호를 공유하지 않습니다.

**5. Yes or no? KAIST has only one routable prefix 143.248.0.0/16.**
- **Answer:** Yes
- **Explanation:** KAIST는 143.248.0.0/16의 하나의 라우터 가능한 프리픽스를 갖고 있습니다.

**6. Yes or no? OSPF is an intra-domain routing protocol.**
- **Answer:** Yes
- **Explanation:** OSPF는 내부 도메인 라우팅 프로토콜입니다.

**7. Yes or no? BGP is an inter-domain routing protocol.**
- **Answer:** Yes
- **Explanation:** BGP는 도메인 간 라우팅 프로토콜입니다.

**8. Yes or no? Routers within an AS use only intra-domain routing protocols between themselves.**
- **Answer:** No
- **Explanation:** AS 내부의 라우터는 iBGP를 포함하여 내부 및 외부 라우팅 프로토콜을 모두 사용할 수 있습니다.

**9. Yes or no? iBGP is used to disseminate BGP routes learned from peer ASes.**
- **Answer:** Yes
- **Explanation:** iBGP는 피어 AS에서 학습한 BGP 경로를 전파하는 데 사용됩니다.

**10. What protocol do gateway routers directly connected between two different ASes use to exchange BGP route info?**
- **Answer:** BGP (Border Gateway Protocol)
- **Explanation:** 두 다른 AS에 직접 연결된 게이트웨이 라우터는 BGP를 사용하여 BGP 경로 정보를 교환합니다.

**11. Yes or no? End-to-end Internet paths are always symmetric; forward and reverse paths go through the same routers.**
- **Answer:** No
- **Explanation:** 종단 간 인터넷 경로는 항상 대칭적이지 않으며, 순방향 및 역방향 경로는 다른 라우터를 통해 갈 수 있습니다.

**12. Which ICMP message type the routers use to reply to packets sent out by traceroute?
	Type = 3, code = 1; destination host unreachable
	Type = 3, code = 3; destination port unreachable
	Type = 11, code = 0; TTL expired
	Type = 12, code = 0; bad IP header**
- **Answer:** Type 11, code 0; TTL expired
- **Explanation:** 트레이스루트가 보낸 패킷에 라우터는 "TTL 만료" 메시지 (Type 11, code 0)로 응답합니다.

**13. Yes or no? If an AS adopts an SDN control plane, routers delegate intra-domain shortest path computation to the centralized SDN controller.**
- **Answer:** Yes
- **Explanation:** SDN 제어 평면을 채택한 AS에서는 라우터가 내부 도메인의 최단 경로 계산을 중앙 집중식 SDN 컨트롤러에 위임합니다.

**14. Yes or no? An SDN switch communicates with an ONOS controller via OpenFlow and with an OpenDaylight (ODL) controller via SNMP.**
- **Answer:** No
- **Explanation:** SDN 스위치는 ONOS 및 OpenDaylight 컨트롤러와 모두 OpenFlow를 통해 통신합니다.

**15. What type of errors does Cyclic Redundancy Check (CRC) with d data bits and r CRC bits detect? Mark all that applies
	A single bit error
	A burst of errors up to (r+1) bits
	Any combination of errors up to r bits
	Any odd number of r-bit errors**
- **Answer:**
  - A single bit error
  - A burst of errors up to (r+1) bits
- **Explanation:** CRC는 단일 비트 오류와 최대 (r+1) 비트의 오류 묶음을 감지할 수 있습니다.

**16. Mark all the protocols that have some form of error detection.
	HTTP
	TCP
	IP
	Ethernet**
- **Answer:**
  - TCP
  - IP
  - Ethernet
- **Explanation:** TCP, IP, Ethernet 프로토콜은 모두 오류 검출 메커니즘을 포함하고 있습니다.

**17. Yes or no? Slotted ALOHA has better efficiency than pure ALOHA.**
- **Answer:** Yes
- **Explanation:** 슬롯 ALOHA는 순수 ALOHA보다 효율성이 더 높습니다.

**18. In Ethernet CSMA/CD, what is the next action that a host takes after detecting a collision?
	A host stops transmitting and wait for a random amount of time.
	A host sends out a jamming signal.
	A host finishes transmissing a frame and when waits for a random amount of time.
	A host stops transmitting and waits for a constant amount of time.
- **Answer:** A host sends out a jamming signal.
- **Explanation:** 충돌을 감지한 후 호스트는 간섭 신호를 보냅니다.

**19. Which of the following protocols does not "take turn"?
	Bluetooth
	FDDI
	token ring
	Ethernet**
- **Answer:** Ethernet
- **Explanation:** Ethernet은 'turn-taking' 메커니즘을 사용하지 않습니다.

**20. Mark all use cases of VLAN.
	Partition a subnet into smaller groups of administrative domains.
	Limit the scope of IP broadcast.
	Limit the size of routing tables.
	Limit the scope of routing protocol reachability.**
- **Answer:**
  - Partition a subnet into smaller groups of administrative domains.
  - Limit the scope of IP broadcast.
- **Explanation:** VLAN은 서브넷을 더 작은 관리 도메인으로 분할하고 IP 브로드캐스트의 범위를 제한하는 데 사용됩니다.

**21. What action does a switch take when it receives a frame of which MAC address is not in the switching table?
	It drops the frame and replies "destination unreachable" via ICMP .
	It broadcasts an ARP request on all ports but for the incoming port.
	It simply broadcasts the frame to all ports but for the incoming port.
	It simply sends it back on the incoming port.**
- **Answer:** It simply broadcasts the frame to all ports but for the incoming port.
- **Explanation:** 스위치는 MAC 주소가 스위칭 테이블에 없을 때 프레임을 들어오는 포트를 제외한 모든 포트에 브로드캐스트합니다.

**22. How long is the MPLS label?**
- **Answer:** 20 bits
- **Explanation:** MPLS 레이블은 20비트입니다.

**23. Now that you have covered the Internet protocol stack from the application layer down to the Ethernet layer. What will you do when your web search does not go thru?**
- **Answer:** Check network connectivity, DNS settings, or firewall configurations.
- **Explanation:** 웹 검색이 되지 않으면 네트워크 연결, DNS 설정 또는 방화벽 구성을 확인합니다.

**24. Which of the medium access classes does CDMA (Code Division Multiple Access) belong to?
	Channel partitioning
	Random access
	Taking turns**
- **Answer:** Channel partitioning
- **Explanation:** CDMA는 채널 분할에 속합니다.

**25. Yes or no? CDMA allows multiple stations to transmit and receive at the same time.**
- **Answer:** Yes
- **Explanation:** CDMA는 여러 스테이션이 동시에 전송하고 수신할 수 있도록 합니다.

**26. Yes or no? When you connect to the Internet via an AP (Access Point), you are using the infrastructure mode of WiFi technology.**
- **Answer:** Yes
- **Explanation:** AP를 통해 인터넷에 연결할 때 WiFi 기술의 인프라 모드를 사용하고 있습니다.

**27. Yes or no? MANET and VANET rely on ad-hoc mode of WiFi technology.**
- **Answer:** Yes
- **Explanation:** MANET 및 VANET은 WiFi 기술의 애드혹 모드에 의존합니다.

**28. Yes or no? Base stations and mobile hosts both adjust rates dynamically as SNR changes.**
- **Answer:** Yes
- **Explanation:** 기지국과 모바일 호스트 모두 SNR(신호 대 잡음비)의 변화에 따라 동적으로 속도를 조정합니다.

**29. Yes or no? In the 802.11 header frame, the MAC address of the AP is included.**
- **Answer:** Yes
- **Explanation:** 802.11 헤더 프레임에는 AP의 MAC 주소가 포함됩니다.

**30. Yes or no? RTS-CTS is a collision detection mechanism.**
- **Answer:** No
- **Explanation:** RTS-CTS는 충돌 회피 메커니즘입니다.

**31. Yes or no? 5G base stations cover a shorter range of distance than 4G one.**
- **Answer:** Yes
- **Explanation:** 5G 기지국은 4G 기지국보다 더 짧은 범위를 커버합니다.

**32. Yes or no? When you travel abroad and start roaming, the visited network abroad has to contact your home network for authorization to network access.**
- **Answer:** Yes
- **Explanation:** 해외로 로밍할 때 방문한 네트워크는 네트워크 접근 권한을 얻기 위해 귀하의 홈 네트워크에 연락해야 합니다.

**33. Yes or no? In 4G/5G your roaming phone's data goes thru a tunnel between the visited network and your home network for eventual Internet access.**
- **Answer:** Yes
- **Explanation:** 4G/5G에서는 로밍 전화의 데이터가 방문 네트워크와 홈 네트워크 사이의 터널을 통해 최종적으로 인터넷에 접근합니다.


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


# Answers for Exams
## 2017 Spring
Here are the answers for the PDF you provided:

1. **True or False?**
   - (a) **False** - Transmission delay is not proportional to the propagation delay but rather depends on the data size and the data rate of the transmission link.
   - (b) **False** - Queueing delay is not proportional to propagation delay; it depends on the traffic load and the performance of the queuing strategies at routers.
   - (c) **True** - Cross traffic can cause additional data packets in the queue, increasing queueing delay.
   - (d) **False** - With nonpersistent connections, each TCP segment carries exactly one HTTP request; a new connection is needed for each new request.
   - (e) **False** - HTTP response messages can have an empty message body, particularly in responses like 204 No Content.
   - (f) **False** - Circuit switching uses dedicated circuit paths and not statistical multiplexing, which is associated with packet-switched networks.
   - (g) **False** - TCP does have mechanisms like ACKs and retransmissions to notify the sender of packet loss implicitly.
   - (h) **False** - HTTP by itself is stateless; cookies are used by websites to maintain state, making it behave in a stateful manner when cookies are used.

2. **Delay Components in End-to-End Delay**
   - The main delay components include processing delay, queueing delay, transmission delay, and propagation delay. 
   - **Constant Delays**: Propagation delay tends to be constant as it is based on the physical distance and medium.
   - **Variable Delays**: Queueing delay is highly variable depending on the network traffic; transmission delay can vary with the size of the packet and the network's capacity.

3. **Time Elapsed for VoIP Communication**
   - (a) Total time = Processing delay + Queueing delay (if any) + Transmission delay + Propagation delay. With a transmission rate of 256 Kbps and a 56-byte packet, the transmission delay = (56 bytes * 8 bits/byte) / 256,000 bits/second ≈ 1.75 ms. Adding the propagation delay of 10 ms, the total time from creation to decoding is approximately **11.75 ms**.
   - (b) For a 100 Mbps transmission rate and a 100 ms propagation delay, the transmission delay becomes significantly shorter, approximately 0.00448 ms. Thus, the total time from creation to decoding is about **100.00448 ms**.

4. **Fields in the TCP Header**
   - Source Port, Destination Port, Sequence Number, Acknowledgment Number, Data Offset, Reserved, Control Bits (e.g., SYN, ACK), Window Size, Checksum, Urgent Pointer, Options (if any).

5. **TCP Congestion Control without Slow Start**
   - (a) Time to increase cwnd from 6 MSS to 12 MSS: Assuming AIMD increases cwnd linearly without loss, it would take 6 RTTs to double the cwnd from 6 to 12 MSS.
   - (b) Average throughput up to 6 RTTs: The average throughput can be calculated as the total segments sent divided by the total time. Over 6 RTTs, starting from 1 MSS and doubling, the average throughput is approximately **4 MSS/RTT** (since the sum of the series from 1 to 6 divided by 6 gives an average window size of 4).

6. **Advantages and Disadvantages of CDNs and P2P**
   - **CDNs**: Advantages include high availability and high performance due to distributed nature. Disadvantages include higher cost and potentially less privacy.
   - **P2P**: Advantages include lower cost and scalability. Disadvantages include inconsistent performance and potential security vulnerabilities.

## 2018 Spring
Here are the answers to the questions from the PDF you uploaded:

1. **Which technology delivers the highest bandwidth for Internet access?**
   - **FTTH (Fiber to the Home)** delivers the highest bandwidth for Internet access among the options listed .

2. **Which of the following does not belong to guided media?**
   - **Digital satellite channel** does not belong to guided media; it is an example of unguided media as it uses wireless communication through space .

3. **What do the following acronyms stand for?**
   - **DDoS**: Distributed Denial of Service
   - **AIMD**: Additive Increase Multiplicative Decrease
   - **MTU**: Maximum Transmission Unit
   - **CIDR**: Classless Inter-Domain Routing 

4. **True or False?**
   - (a) **True** - The fiber-optic cable is guided media.
   - (b) **True** - The goal of persistent HTTP connections is to avoid TCP 3-way handshake delay overhead per object.
   - (c) **False** - The unit of the TTL field in the IP header is not in seconds; it's in hops (the maximum number of hops that packets are allowed to travel through routers).
   - (d) **False** - The destination addresses of DHCP messages can vary; not all are 255.255.255.255, particularly in later stages of the DHCP process .

5. **What is the source IP address of a DHCP discover message that a host sends out when it arrives at a network?**
   - The source IP address is typically **0.0.0.0** when the host does not yet have an assigned IP .

6. **End-to-End Delays in a Datacenter Scenario**
   - (a) Without queueing or processing delays, the end-to-end delay would be dominated by **propagation delay**, though minimal given the short distances and high speed of light in the medium.
   - (b) With maximum queueing, the dominant delay component would likely be **queueing delay** due to the filled buffers at each router.
   - (c) Increasing the length of the links to 10 km significantly increases the **propagation delay**, making it the dominant component.
   - (d) Changing both the link length to 10 km and packet size to 10 Kbits would make **transmission delay** significant, potentially dominating due to the larger packet size over higher distances .

7. **Distribution Schemes in Networking**
   - (a) To minimize inter-ISP bandwidth, all hosts should ideally be within the same ISP as host s or directly connected ISPs to minimize crossing to other ISPs.
   - (b) To maximize inter-ISP bandwidth consumption, the hosts should be distributed across multiple different ISPs that require crossing multiple ISP networks, thereby increasing inter-ISP traffic .

8. **TCP Throughput Description**
   - The loss rate \( L \) can be mathematically derived based on the formula and TCP throughput considerations. The average throughput of TCP is not directly proportional to RTT; it generally decreases as RTT increases because the window size is limited by the delay-bandwidth product .

9. **Maximum Window Size for a TCP (Reno) Connection**
   - Considering the link speed, segment size, and RTT, the maximum window size can be calculated based on the congestion avoidance algorithm where it grows until loss occurs, dictated by the bandwidth-delay product .

10. **Network Addresses for Subnets**
   - Each subnet needs a specific prefix and enough addresses to support the required number of interfaces. Network addresses must conform to subnetting rules that allow for the required number of hosts, given as /24 for about 254 hosts, adjusted as needed .

11. **Impact of NATs on P2P Applications**
   - Establishing a TCP connection between two peers behind NATs can be achieved using techniques like NAT traversal, which may involve methods such as UPnP, NAT-PMP, or hole punching, depending on the NAT configuration and type .

12. **Packet Loss at Input Ports**
   - Packet loss at input ports can occur due to buffer overflow, when incoming packets arrive at a rate exceeding the processing capacity of the port or its buffer space .

13. **Overhead in Data Transmission**
   - Calculating the overhead involves considering the size of the TCP and IP headers relative to the data size of 40 bytes. Given typical header sizes, the percentage of overhead versus application data can be calculated .

14. **Worst Startup Time for Loading a Web Page**
   - **DNS Resolution**: In the worst case, if the DNS server is slow to respond or if the domain is not cached locally.

## 2021 Fall

Here are the answers to the questions from the 2021 Fall CS341 Midterm PDF:

**P1: Finite State Machine (FSM) of rdt 3.0 receiver**
- Unfortunately, without seeing the specific FSM diagram with its empty phrases, I can't accurately fill in the blanks. This would typically involve understanding the specific actions and responses of the receiver in various states of packet reception, including acknowledgment and handling of duplicate or corrupt packets.

**P2: Effects of DHCP and DNS server downtime while surfing the web**
- a. **DHCP server down:** Your current web surfing session will not be immediately affected because your device has already obtained an IP address. However, you might not be able to renew the IP lease or get a new IP address if needed. A solution other than waiting could be to manually configure a static IP address, if possible, within the same subnet.
- b. **DNS server down:** You won't be able to resolve domain names to IP addresses, which means new websites might not load. Cached DNS entries will still work. Alternatives include switching to a public DNS server like Google DNS (8.8.8.8 and 8.8.4.4) or Cloudflare DNS (1.1.1.1).

**P3: Non-compliance with TCP congestion control**
- If other hosts do not use congestion control and send packets aggressively, it can lead to network congestion, increased packet loss, and unfair bandwidth distribution. This can degrade overall network performance and particularly impact compliant hosts, which might experience reduced throughput as a consequence.

**P4: Time to download a document calculation**
- Given \( S/R + T > 4 \cdot S/R \), you can estimate the time to download a document of size \( 13 \cdot S \) as follows:
  - The total time \( T_{total} \) to download the document would be the sum of the transmission times and the round-trip times involved. Since \( S/R \) is the time to send one segment and there are 13 segments, the naive calculation would be \( 13 \cdot S/R \) for transmission plus round-trip times. However, the comparison provided suggests there's more waiting involved due to the round-trip time, making \( T \) a significant factor. Thus, a more accurate estimate might involve multiple of \( T \), suggesting \( T_{total} \approx 13 \cdot S/R + multiple \cdot T \).

**P5: Number of datagrams to send a 1GB file**
- A 1GB file is \( 1 \times 10^9 \) bytes. Each datagram can carry \( 1500 - 20 = 1480 \) bytes of data. Therefore, the number of datagrams required would be:
  $\text{Number of Datagrams} = \lceil \frac{1 \times 10^9 \text{ bytes}}{1480 \text{ bytes}} \rceil$
  This results in approximately 675,676 datagrams needed to send the file. The calculation divides the total file size by the payload capacity of each datagram, considering the IP header size, and uses the ceiling function to account for any remaining partial datagram.

## 2022 Spring
Here are the responses to the questions from the 2022 Spring CS341 Midterm PDF:

1. **True or False Answers:**
   - (1) **True** - Propagation delay is indeed a function of the distance and the medium through which data travels.
   - (2) **True** - Transmission delay depends on the link capacity (or bandwidth) and the packet length.
   - (3) **False** - Queueing delay is generally a function of the traffic load and the link capacity, not directly the packet length.
   - (4) **False** - In a client-server paradigm, clients do not typically communicate directly with each other; they interact through the server.
   - (5) **False** - In a peer-to-peer paradigm, peers are not necessarily expected to be always on; they can join and leave the network as needed.
   - (6) **False** - HTTP cookies are stored at the client's browser, not on the server-side database, although servers may store session identifiers linked to those cookies.
   - (7) **False** - The DNS root servers, including m.root-servers.net, do not serve as authoritative servers for specific domains like kaist.ac.kr.
   - (8) **True** - Both TCP and UDP headers include a checksum field.
   - (9) **False** - Only the TCP header has a length field (as part of the data offset field); the UDP header does not.
   - (10) **True** - Both IP and UDP headers include a length field.
   - (11) **False** - TCP and UDP headers contain port numbers but IP addresses are in the IP header, not TCP or UDP headers.
   - (12) **False** - The rwnd field in the TCP header is for flow control, not congestion control.
   - (13) **True** - The IPv6 header has a fixed length of 40 bytes.
   - (14) **False** - TCP receivers do not start a timer every time a packet is received; timers are generally started to manage packet loss and retransmissions.
   - (15) **True** - Queueing can occur at both the input and output ports of a router.
   - (16) **True** - Faster transmission speeds generally result in faster arrival of packets at the destination assuming all other factors are constant.

2. **Subnet and Forwarding Table Questions:**
   - Without specific diagrams (Figures 1 and 2) showing the subnet addresses, it's impossible to determine the number of subnets or construct a forwarding table.

3. **DHCP Transactions:**
   - Filling in the addresses in a DHCP transaction diagram requires specific details from the diagram which are not available in this text format.

4. **NAT Translation Table:**
   - Similar to the DHCP transactions, constructing a NAT translation table needs specific transaction details from the diagrams.

5. **IPv6 Tunneling:**
   - Specific source and destination addresses for IPv6 tunneling over IPv4 nodes would require more details from the provided diagram.

6. **TCP Segment Exchange:**
   - Correct sequence and acknowledgment numbers would need the specific states and actions from the TCP segment exchange diagram.

7. **DNS Query Calculations:**
   - Assuming each DNS query for www.mit.edu results in one query to the .edu TLD server per day due to the 24-hour TTL, and each query to the mit.edu authoritative server 4 times a day due to the 6-hour TTL, approximately 1 query to the .edu TLD server and 4 queries to the mit.edu server per day would be needed.

8. **External Web Site Access Detection:**
   - Without administrative access to the DNS server logs or network monitoring tools, an ordinary user cannot determine if an external website was accessed from within the department recently.

9. **Transmission and Propagation Delay Calculations:**
   - These calculations would require the specific formulae for transmission and propagation delays, which depend on link capacity, packet size, and the speed of signal propagation.

10. **Users in a Shared Link Scenario:**
   - Calculating the number of users supported under circuit switching, the probability of transmission under packet switching, and the probabilities involving binomial distributions would require detailed calculations based on provided formulas and values.
