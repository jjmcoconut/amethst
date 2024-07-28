[[Computer Networking Quizzes & Exam]]

Lecture notes from Introduction to Computer Networking taught by  - KAIST
# Introduction
Internet: computer network that interconnects computing devices around the world
Protocol: Defines format and order of messages exchanged between multiple communication entities, as well as actions taken on the transmission
![[Pasted image 20240229140039.png|400]]

## 1.2 The Network Edge

__2 most common kinds of high-speed for hones__
- Digital Subscriber Line(DSL)
	- ![[Pasted image 20240412144002.png|300]]
	- From the same local telephone company that provides its wired local phone access
- Cable
	- ![[Pasted image 20240412144221.png|300]]
	- Uses cable television company's existing cable TV infastructure
	- Use hybrid fiber coax(HFC): fiber & coaxial cable
- Fiber To The Home(FTTH)
	- provides an optical fiber path from the CO(telco's local office) directly to the home

__Physical Medium__
- Guided media
	- Twisted-Pair Copper Wire
		- Data rates up to 10Gbps for up to 100 meters
		- Dominant solution of high-speed LAN
	- Coaxial Wire
		- [![Coaxial Cable - Write Short Note on Coaxial Cable - Computer Notes](https://ecomputernotes.com/images/Coaxial-Cable.jpg)
		- Consists of two copper conductors but concentric
	- Fiber Optics
		- Conducts pulses of light with each pulse representing a bit
- Unguided Media
	- Terrestrial Radio Channels
		- Normal radio
	- Satellite Radio Channels
		- Starlink

## 1.3 The Network Core
 Network core functions
 1. Forwarding: local action, moving packets from input to output (action)
 2. Routing: global action, determine packet destination (decision)

| Circuit switching                                            | Packet switching                    |
| ------------------------------------------------------------ | ----------------------------------- |
| resources are reserved for the duration of the communication | resource is not reserved            |
| reserves constant transmission rate                          | transmission rate is not gaurenteed |
| Traditional telephone network                                | Internet                            |

Packet switching is a winner?
Pros
- Great for bursty data (Sending is not constant)
	- Ex) 5 people, 1 line using 10% of time $\rightarrow$ Probability of 2 or more people trying to use the network at same time: 8.146%
	- Can handle more people than given line

Cons
- Packet delay & loss

If we need constant transmission rate function in packet switching: complicated & expensive

| Network End                                   | Network Core                                            |
| --------------------------------------------- | ------------------------------------------------------- |
| Device that uses the network(host=end system) | Interconnected routers                                  |
| enterprise network, home network, ...         | national, global, local, regional ISP(KT,SKT,LG U+,...) |
### 1.3.3 Network of Networks
![[Pasted image 20240305135554.png|500]]
Tier 1 ISP: ISP that has international coverage (AT&T, NTT, ...)
Regional ISP: ISP that has regional coverage (SKT, KT, LG U+, ...)
Content provider networks: Google, ...

KAIST: enterprise network
Data center networks: high-bandwith links(10-100Gbps)

Packet: segments of data with header bytes

## 1.4 Delay, Loss & Throughput in Packet-Switched Networks
Packet switching: store and forward
- Packets are transmitted after it is fully stored
- Does not send the packet data while receiving it

__Packet Queuing & loss__
Why do we need Queue?
- If packet arrival speed > output speed: the packets needs to be stored in the router

Package loss
- If queue is full we cannot store more packets $\rightarrow$ package disappears

__Delay__
- Processing Delay: time required to examine the packet's header and determine where to direct the packet
- Queuing Delay: Time required for waiting to be transmitted
- Transmission Delay: Time required to push all the packet's bits into the link: $\frac{\text{Packet size}}{\text{Transmission rate}}$
- Propagation Delay: Time required to get to the target router: $\frac{\text{Length}}{\text{Speed of light}}$

## 1.5 Protocol Layers and Their Service Models

### 1.5.1 Layered Architecture
![[Pasted image 20240412145750.png|300]]

### 1.5.2 Encapsulation
![[Pasted image 20240412145913.png|500]]
Packet has 2 types of fields:
- Header field: what the layer writes on the packet
- Payload field: packet from above

# 2. Application Layer
## 2.1 Principles of Network Application
Information in this subchapter is explained throughout the book.
Short summarization with graphs:
![[Pasted image 20240412150833.png|500]]
![[Pasted image 20240412150812.png|500]]

## 2.2 Web and HTTP

### 2.2.1 Overview of HTTP
__HyperText Transfer Protocol(HTTP)__
- Uses TCP
- Stateless protocol: HTTP server maintains no information about the clients
- Web browsers(Safari, Chrome) implement the client side of HTTP
- Web servers(Google, Naver) implement the server side of HTTP, addressable by URL

| Persistent Connection                                                                    | Non-persistent Connection                                       |
| ---------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Server leaves TCP connection open after sending message, closes connection after timeout | Each TCP connection is closed after the server sends the object |
| HTTP/1.1                                                                                 | HTTP/1.0                                                        |

### 2.2.3 HTTP Message Format
#### HTTP Request Message
```
GET /somedir/page.html HTTP/1.1 - request line
Host: www.someschool.edu.       - others: header line
Connection: close
User-agent: Mozilla/5.0
Accept-language: fr
```

- GET: when browser requests an object
- POST: when user fills out a form
- HEAD: responds with a HTTP message but it leaves out the requested object
- PUT: upload objects to Web servers
- DELETE: delete an object on a Web server

#### HTTP Response Message
```
HTTP/1.1 200 OK                               - status line
Connection: close                             - header lines
Date: Tue, 18 Aug 2015 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html

(data data data ...)                          - entire body 
```
- 400 Bad Request: Request could not be understood by server
- 404 Not Found: Requested document is not in server
- 505 HTTP Version Not Supported: requested HTTP protocol version is not supported by server
- 

### 2.2.4 User-Server Interaction: Cookies
![[Pasted image 20240412153955.png|500]]
- If Susan returns to Amazon's site -> her browser puts the header line `Cookie: 1678` in the request message
- Cookies can be used to identify users

### 2.2.5 Web Caching
![[Pasted image 20240412155239.png|400]]
__Web cache(Proxy server)__
- A network device that handles HTTP requests for a main web server
- Purchased & installed by an ISP

Advantages:
- Reduce the response time for a client request - especially when bottleneck exists
- Reduce traffic on an institution's access link to Internet - reduce costs of bandwidth

#### Conditional GET
Mechanism that allows a cache to verify objects are up to date
```
GET /fruit/kiwi.gif HTTP/1.1
Host: www.exotiquecuisine.com
If-modified-since: Wed, 9 Sept 2015 09:23:24
```
Then the response:
```
HTTP/1.1 304 Not Modified
Date: Sat, 10 Oct 2015 15:39:29
Server: Apache/1.3.0 (Unix)

(empty entity body)
```

### 2.2.6 HTTP/2
Goals:
- Reduce perceived latency by enabling request and response multiplexing over single TCP connection
- provide request prioritization and server push
- provide efficient compression of HTTP header fields

HTTP/2 changes how data is formatted and transported btw client, server. Does not change methods, status codes, URLs, header fields

__Head of Line(HOL) blocking__
- When small objects cannot be transmitted because of large objects(such as video)
- Happens when we try to connect web page over single TCP connection
- HTTP/1.1 makes multiple TCP connections to avoid this
- However HTTP/2 goal is to reduce of parallel TCP connections
	- Reduce sockets
	- Congestion control as intended
	- Method: Break each message into small frames & interleaving request, response message on same TCp connection

## 2.3 Electronic Mail in the Internet

### 2.3.1 Simple Mail Transfer Protocol(SMTP)
Problems
- Restricts the body(not just the headers) of all mail messages to simple 7-bit ASCII
- Requires binary multimedia encoded to ASCII then decode after SMTP transport

![[Pasted image 20240412162105.png|500]]
- Does not use intermediate mail servers for sending mail(direct connection)
- Persistent connection: It can send multiple messages over a single TCP connection
- Alice's user agent uses SMTP or HTTP to deliver email to Alice's mail server. Then Alice's mail server sends the email to Bob's mail server by SMTP. Why 2 steps?
	- Alice's user agent does not have any protocol when the Bob's server is unreachable
	- Alice's server can resend the email every 30 minutes until the Bob's server becomes operational
- Internet Mail Access Protocol(IMAP): how a user agent checks his/her email

## 2.4 DNS - Domain Name System
### 2.4.1 Services Provided by DNS
- Directory service that translates hostnames to IP addresses.
- Commonly employed by other application-layer protocols(HTTP, SMTP, ...)

Services
- Host aliasing: `relay.west-coast.abc.com`(canonical hostname) may have alias `www.abc.com`. DNS can obtain the canonical hostname
- Mail server aliasing: `bob@abc.com` to `bob@relay.west-coast.abc.com`
- Load distribution: `cnn.com` is replicated over multiple servers -> multiple IP address. DNS can distribute the load by rotating the returning IP address.

### 2.4.2 Overview of How DNS Works
Problems with centralized designed DNS
- Single point of failure: If DNS server crashes - Internet too.
- Traffic volume: single DNS has to handle all DNS queries
- Distant centralized database: Cities near the DNS server have faster connection to DNS
- Maintenance: DNS has to keep record of hosts and needed to be frequently updated

#### Distributed Hierarchical Database
![[Pasted image 20240412164047.png|500]]
- Root DNS servers: Provide IP addresses of TLD servers
- Top-level domain(TLD) servers: com, org, kr, ... - there is a TLD server
- Authoritative DNS servers: Every organization with publicly accessible hosts on the Internet must provide publicly accessible DNS records that map the names of those hosts to IP addresses. - (portal.)kaist.ac.kr
- ac.kr - also needs to fetch from authoritative DNS server(only .kr is in the TLD list)

__Local DNS server__
- Does not strictly belong to the hierarchy of servers.


| Iterative DNS quries                                             | Recursive DNS quries                                                                                |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![[Pasted image 20240412165502.png  ]]                           | ![[Pasted image 20240412165631.png]]                                                                |
| Root DNS sends only the IP address information of TLD DNS server | Root DNS needs to save of all queries from hosts until response from TLD DNS server - too much load |

#### DNS Caching
- Improve delay preformance
- Reduce number of DNS messages
- Mappings btw hostnames & IP address is not permanent -> discard cached information after period of time

### 2.4.3 DNS Records and Messages
DNS stores __resource records(RR)__ 
- `(Name, Value, Type, TTL)`
- `Name` and `Value` depends on `Type`

## 2.5 Peer-to-Peer File Distribution
- $N$ peers
- $F$: file size
- $u_s$: server upload speed
- $u_i$: client $i$ upload speed
- $d_{min} = min{d_1,d_2,\cdots,d_N}$

Server-client structure distribution time $D_{cs}$
$$D_{cs} \geq max(\frac{NF}{u_s},\frac{F}{d_{min}})$$

P2P distribution time $D_{P2P}$
$$D_{P2P} \geq max(\frac{NF}{u_s+\sum u_i},\frac{F}{d_{min}},\frac{F}{u_s})$$
![[Pasted image 20240412171110.png|500]]

#### BitTorrent

BitTorrent is a widely-used P2P protocol for file distribution. In BitTorrent, a group of peers involved in distributing a file is termed a torrent. Peers exchange equal-sized file chunks amongst each other, typically 256 KBytes in size. As peers join and leave the torrent, they download and upload chunks to one another. The protocol employs trackers to keep track of participating peers.

__Operation__
1. **Tracker Interaction:** Peers register with the tracker upon joining a torrent and periodically update their status.
2. **Peer Connection:** When a new peer joins, the tracker provides a subset of neighboring peers. Peers establish TCP connections with these neighbors.
3. **Chunk Exchange:** Peers exchange lists of chunks they possess and request missing ones from neighbors.
4. **Chunk Prioritization:** Peers utilize "rarest first" to request scarce chunks and prioritize trading with peers supplying data at the highest rate.
5. **Trading Algorithm:** Peers implement a trading algorithm where they prioritize peers providing them data at the highest rate. Additionally, they randomly select a peer every 30 seconds for trading, fostering new connections and allowing new peers to acquire chunks.
6. **Incentive Mechanism:** The protocol uses a tit-for-tat incentive scheme, encouraging peers to reciprocate data exchange. This mechanism fosters cooperation among peers.

__Significance__
- BitTorrent's success is attributed to its effective incentive mechanism, tit-for-tat, which encourages peer cooperation.
- Despite potential circumvention, BitTorrent remains highly successful, with millions of peers sharing files across hundreds of thousands of torrents.
- The protocol's design enables a thriving ecosystem of file sharing, preventing widespread free-riding behavior among users.

__Additional Applications__
- Distributed Hash Table (DHT): Utilized for decentralized database storage, widely implemented in P2P systems like BitTorrent, and subject to extensive research.

BitTorrent's robust design, driven by its incentive mechanism, has made it a cornerstone of P2P file sharing, facilitating efficient and widespread distribution of content.

## 2.6 Video Streaming and Content Distribution Networks
__Overview__
- Streaming video, including platforms like Netflix, YouTube, and Amazon Prime, dominates internet traffic, constituting about 80% in 2020.
- Prerecorded videos are stored on servers, and users request them on demand.
- Videos are sequences of images displayed at a constant rate, encoded into pixels represented by bits.
- Video compression allows trading off quality with bitrate, crucial due to high bitrate of internet video.

__HTTP Streaming and DASH__
- HTTP streaming delivers video stored on an HTTP server via HTTP GET requests.
- Dynamic Adaptive Streaming over HTTP (DASH) enables encoding videos into different versions with varying bitrates.
- Clients dynamically request video segments based on available bandwidth, ensuring smooth playback.
- DASH provides flexibility for clients to adapt to changing bandwidth conditions.

![[Pasted image 20240412172608.png|500]]

__Content Distribution Networks (CDNs)__
- CDNs distribute on-demand video streams to users worldwide efficiently.
- CDNs manage servers in multiple locations, storing copies of videos and directing user requests to the nearest server for optimal performance.
- CDNs may deploy servers deep within ISPs' networks or bring ISPs to centralized locations, each with its advantages and challenges.
- CDNs employ cluster selection strategies to direct clients to appropriate servers, considering factors like geographical proximity and real-time network conditions.
__Cluster Selection Strategies__
- CDNs use various strategies to select clusters for clients, including geographic proximity and real-time network measurements.
- Challenges include accurately determining the best cluster based on network conditions and dealing with unresponsive LDNSs.

Video streaming and CDNs play crucial roles in delivering high-quality video content to users worldwide, overcoming challenges of high bitrate and varying network conditions. Efficient server placement and intelligent cluster selection are key to ensuring optimal performance and user experience.

#### Google’s Network Infrastructure

Google has a vast array of services, requiring a complex network infrastructure. It includes:
- Nineteen mega data centers worldwide, each with around 100,000 servers, handling dynamic content like search results and Gmail messages.
- About 90 clusters in Internet Exchange Points (IXPs) globally, serving static content such as YouTube videos.
- Hundreds of "enter-deep" clusters within access ISPs, performing TCP splitting and serving static content like parts of web pages.
- All these data centers and clusters are interconnected with Google's private network, except for local ISPs.
- Google's services are largely provided by an independent network infrastructure, excluding local ISPs.

### 2.6.4 Case Studies: Netflix and YouTube
![[Pasted image 20240412172706.png|400]]
**Netflix:**
- Netflix uses Amazon servers for its website and backend databases, as well as for critical functions like content ingestion, processing, and uploading to its CDN.
- Initially, Netflix used third-party CDNs but later built its own private CDN, distributing videos via server racks in IXPs and ISPs worldwide.
- Netflix employs a proprietary version of DASH for video delivery, selecting servers based on client location and delivering content directly to clients.
- The CDN uses push caching, pushing content to servers during off-peak hours.

**YouTube:**
- YouTube, owned by Google, also utilizes a private CDN, distributing videos via server clusters in numerous IXPs and ISPs.
- Google employs pull caching and DNS redirect, directing clients to the closest or least loaded cluster.
- YouTube offers multiple versions of videos with different bit rates but lacks adaptive streaming like DASH.
- Video processing, including format conversion and bitrate variation, occurs within Google's data centers.


# 3. Transport Layer
- The transport layer is a crucial part of the network architecture, providing communication services directly to application processes.
- It alternates between discussing transport-layer principles and their implementation in existing protocols, with a focus on TCP and UDP.

## 3.1 Introduction & Transport-Layer Services
- Transport-layer protocols enable logical communication between application processes on different hosts, abstracting away the underlying physical infrastructure.
- Transport-layer protocols convert application messages into transport-layer segments, encapsulated within network-layer packets.
- Both TCP and UDP are available transport-layer protocols, offering different services to applications.

### 3.1.1 Relationship Between Transport and Network Layers
![[Pasted image 20240412173146.png|500]]
- The transport layer provides logical communication among processes, while the network layer provides logical communication among hosts.
- Transport-layer protocols operate within end systems and are not involved in the intermediate network core.
- Multiple transport protocols may offer different service models to applications, constrained by the service model of the underlying network-layer protocol.

### 3.1.2 Overview of Transport Layer in the Internet
- UDP provides an unreliable, connectionless service, extending IP's delivery service between processes.
- TCP offers reliable data transfer, congestion control, and error checking, converting IP's unreliable service into a reliable data transport service.
- TCP's congestion control aims to prevent excessive traffic and ensure fair bandwidth distribution among connections.

## 3.2 Multiplexing and Demultiplexing
- Discusses transport-layer multiplexing and demultiplexing, extending host-to-host delivery to process-to-process delivery.
- Provides concrete examples within the context of the Internet but applicable to all computer networks.

__Multiplexing and Demultiplexing Process__
- Transport layer receives segments from network layer and delivers data to appropriate application process.
- Each process has one or more sockets for data transmission.
- Sockets are identified by unique port numbers.
- Demultiplexing directs incoming segments to the correct socket based on destination port number.
- Multiplexing gathers data from sockets, encapsulates it into segments, and passes it to the network layer.

![[Pasted image 20240412174015.png|500]]
__Port Numbers__
- Port numbers range from 0 to 65535, with well-known port numbers reserved for specific protocols.
- UDP and TCP segments use source and destination port numbers for demultiplexing.
- UDP automatically assigns port numbers, but servers must specify well-known port numbers.
- Source port number serves as part of the return address for TCP segments.

__Connectionless Multiplexing and Demultiplexing (UDP)__
- UDP sockets are identified by a destination IP address and a destination port number.
- Incoming UDP segments are demultiplexed based on destination port number.
- A UDP socket may receive segments with different source IP addresses and source port numbers but the same destination IP address and port number.

![[Pasted image 20240412174141.png|500]]
__Connection-Oriented Multiplexing and Demultiplexing (TCP)__
- TCP sockets are identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).
- Incoming TCP segments are demultiplexed using all four values.
- TCP connection establishment involves exchanging segments with specific port numbers.
- Server supports multiple simultaneous TCP connection sockets, each identified by a unique four-tuple.

__Web Servers and TCP__
- Web servers use port numbers to distinguish segments from different clients.
- High-performing Web servers may use a single process with multiple connection sockets.
- Persistent HTTP connections use the same server socket for message exchange, while non-persistent connections create and close sockets for each request/response.

## 3.3 Connectionless Transport: UDP
- UDP (User Datagram Protocol) is a simple, connectionless transport protocol providing minimal functionality beyond multiplexing/demultiplexing and light error checking.
- It operates at the transport layer and is defined in [RFC 768].

__Design Philosophy__
- Designed to offer a bare-bones transport protocol.
- Provides multiplexing/demultiplexing service and basic error checking, adding little to IP.

![[Pasted image 20240412175917.png|500]]
__Functionality__
- **Application Interaction:** Takes messages from the application process, adds source and destination port numbers, and passes the segment to the network layer.
- **Connectionless:** No handshaking between sending and receiving entities before sending a segment.
- **Examples:** Often used for applications like DNS, where reliability isn't crucial.

__Why UDP?__
- **Application Control:** Allows finer control over data transmission compared to TCP.
- **No Connection Establishment:** No delay to establish a connection, suitable for real-time applications.
- **No Connection State:** Doesn't maintain connection state, allowing support for more active clients.
- **Lower Overhead:** Header overhead is smaller compared to TCP.

__Additional Considerations__
- **Applications:** Used for multimedia applications, network management, and DNS.
- **Reliability:** Reliability can be built into the application itself but requires careful implementation.
- **Error Detection:** Provides error detection through checksum, crucial for end-to-end reliability.

![[Pasted image 20240412175853.png|400]]
### 3.3.1 UDP Segment Structure
- Defined in RFC 768, consists of four fields: source port, destination port, length, and checksum.
- Application data occupies the data field, with length specifying the total bytes in the segment.
- Checksum ensures error detection by confirming the integrity of the segment.

### 3.3.2 UDP Checksum
UDP at the sender side performs the 1s complement of the sum of all the 16-bit words in the segment, with any overflow encountered during the sum being wrapped around. This result is put in the checksum field of the UDP segment.
- Suppose we have following 3 16-bit words
    0110011001100000
    0101010101010101
    1000111100001100
    The sum of these 3 is  0100101011000010. Taking 1's complement is 1011010100111101 which is the number that will be in the checksum field

__Significance__
- Provides a lightweight option for applications not requiring TCP's reliability.
- Offers flexibility and control to developers but requires careful consideration of reliability and error handling.

## 3.4 Principles of Reliable Data Transfer
![[Pasted image 20240412180126.png|500]]
- **Importance:** Reliable data transfer is crucial across different layers of networking.
- **Central Problem:** Implementing reliable data transfer across various layers of networking.
- **Significance:** TCP, a prominent protocol, utilizes these principles.
- **Service Abstraction:** Reliable channel ensuring data integrity, order, and no loss.
- **Protocol Responsibility:** Implementing the service abstraction despite unreliable underlying layers.

### 3.4.1 Building a Reliable Data Transfer Protocol
- **Incremental Approach:** Developing sender and receiver sides considering different channel models.
- **Terminology:** Usage of "packet" for generality across computer networks.
- **Unidirectional Focus:** Only unidirectional data transfer considered initially.
- **Interface Design:** Sender and receiver interfaces illustrated for data transfer protocol.
- **Protocol Naming:** Introduction of the name "rdt" for reliable data transfer protocol.

__Protocol Evolution__
1. **rdt1.0:** Simple protocol for perfectly reliable channels.
	- ![[Pasted image 20240412180153.png|400]]
2. **rdt2.0:** Handling bit errors with error detection, ACKs, and NAKs.
	- ![[Pasted image 20240412180213.png|500]]
3. **rdt2.1:** Enhanced version with sequence numbers to address corrupted ACKs or NAKs.
	- ![[Pasted image 20240412180236.png|500]]![[Pasted image 20240412180305.png|700]]
4. **rdt2.2:** NAK-free protocol with sequence numbers for packet acknowledgment.
	- ![[Pasted image 20240412180335.png|500]]![[Pasted image 20240412180356.png|600]]
5. **rdt3.0:** Addressing packet loss with time-based retransmission mechanism.
	- ![[Pasted image 20240412180418.png|600]]![[Pasted image 20240412180707.png|600]]

__Key Features__
- **Error Handling:** Error detection, ACKs, NAKs, sequence numbers, and retransmission.
- **Protocol Elements:** Checksums, sequence numbers, timers, and acknowledgment packets.

__Conclusion__
- **Achievement:** Development of a working reliable data transfer protocol.
- **Components:** Checksums, sequence numbers, timers, ACKs, and NAKs crucial for operation.
- **Protocol Robustness:** Gradual evolution addressing different channel challenges.
- **Protocol Name:** Adoption of "rdt" for future protocol references.
  
### 3.4.2 Pipelined Reliable Data Transfer Protocols
![[Pasted image 20240412181557.png|500]]
Protocol **rdt3.0** is functionally correct but suffers from poor performance due to its stop-and-wait nature. In a hypothetical scenario with coast-to-coast hosts, the stop-and-wait behavior severely limits sender utilization, causing inefficient use of available bandwidth.

**Solution:** Implement **pipelining** to allow the sender to transmit multiple packets without waiting for acknowledgments. This approach significantly improves sender utilization.

**Consequences:**
- **Sequence Number Range:** Must be increased to handle multiple unacknowledged packets.
- **Buffering:** Sender and receiver may need to buffer multiple packets.
- **Error Recovery Approaches:** Two basic methods are **Go-Back-N** and **Selective Repeat**.

### 3.4.3 Go-Back-N (GBN)
![[Pasted image 20240412181630.png|600]]
- Sender can transmit multiple packets without waiting for acknowledgments, constrained by a maximum allowable number (**N**) of unacknowledged packets.
- **Window Size:** Defines the range of permissible sequence numbers for transmitted but unacknowledged packets.
- **Implementation:** Includes sender and receiver FSM descriptions, event handling for invocation, ACK receipt, and timeouts.

**Receiver Actions:** Discards out-of-order packets, maintains expected sequence number, and delivers data to upper layer in order.

**Operation:** Sliding window mechanism controls packet transmission and acknowledgment.

**Implementation:** Likely resembles extended FSM with event-based programming for handling various events.

![[Pasted image 20240412181711.png|500]]![[Pasted image 20240412181737.png|500]]
**Conclusion:** GBN protocol encompasses techniques crucial for reliable data transfer, laying the foundation for further study of TCP's reliable data transfer components.

### 3.4.4 **Selective Repeat (SR)**
![[Pasted image 20240412182134.png|500]]
The **GBN protocol** aims to optimize channel utilization by filling the pipeline with packets, unlike stop-and-wait protocols. However, GBN can face performance issues, especially with large window sizes and bandwidth-delay products, leading to unnecessary retransmissions upon a single packet error.

**Selective-repeat protocols** address this by retransmitting only suspected erroneous packets, minimizing unnecessary retransmissions. The sender uses a window size to control the number of unacknowledged packets. Unlike GBN, the sender receives acknowledgments for some packets in the window.

The **SR receiver** acknowledges correctly received packets regardless of order and buffers out-of-order packets until missing ones are received. This allows delivering batches of packets in order to the upper layer.

**Important Considerations:**
- Lack of synchronization between sender and receiver windows can lead to retransmissions of already received packets.
- The sender and receiver may not have an identical view of received packets.
- A finite range of sequence numbers can affect protocol behavior, necessitating a careful choice of window size.

**Implications of Packet Reordering:**
- Packet reordering can occur in network channels, challenging the assumption of packet order preservation.
- Strategies like sequence number reuse prevention are employed to mitigate duplicate packet issues.
- Techniques like those described in [Sunshine 1978] help avoid reordering problems.

**Conclusion:**
Reliable data transfer protocols introduce various mechanisms to ensure data integrity and efficiency. Understanding these mechanisms is crucial for designing robust communication systems.

## 3.5 Connection-Oriented Transport: TCP
- **Transport-layer Protocol:** TCP (Transmission Control Protocol).
- **Connection-oriented & Reliable:** Utilizes principles of reliable data transfer, error detection, retransmissions, cumulative acknowledgments, timers, and header fields.
- **Defined in:** RFC 793, RFC 1122, RFC 2018, RFC 5681, and RFC 7323.

### 3.5.1 The TCP Connection
- **Connection Establishment:** Involves a handshake between communicating processes to establish parameters.
- **TCP Connection Nature:** Logical connection; resides only in communicating end systems.
- **Full-duplex Service:** Allows simultaneous data flow between sender and receiver.
- **Point-to-point:** Between single sender and receiver; multicast not supported.

__Establishing a TCP Connection__
- **Client-Server Interaction:** Client process initiates connection with server process.
- **Three-way Handshake:** Initiated by client, acknowledged by server, and finalized by client.

__Data Transmission__
- **Data Passing:** Client process sends data to TCP, directed to connection's send buffer.
- **Segment Formation:** Data paired with TCP header, forming TCP segments.
- **Buffer Management:** Segments received at the other end stored in connection's receive buffer.
- **No Intermediate Buffers:** Buffers and variables allocated only in end systems, not in network elements.

*Note: TCP ensures reliable and orderly data transmission between communicating processes, utilizing connection-oriented principles.*

### 3.5.2 **TCP Segment Structure**
![[Pasted image 20240412182757.png|400]]
The TCP segment comprises **header fields** and a **data field**, with the **Maximum Segment Size (MSS)** defining the maximum data field size. For large files, TCP divides data into MSS-sized chunks. Interactive apps often use smaller data chunks, e.g., Telnet and ssh typically use one-byte segments.

The TCP header, usually 20 bytes longer than UDP, contains:
- **Sequence number** and **acknowledgment number** fields for reliable data transfer.
- **Receive window** field for flow control.
- **Header length** field, variable due to TCP options.
- **Options field** for negotiation (e.g., MSS) and time-stamping.
- **Flag field** (6 bits), including ACK, SYN, FIN for connection setup/teardown, and PSH, URG for data handling.

**Sequence Numbers and Acknowledgment Numbers**
- TCP views data as an ordered byte stream.
- Sequence numbers mark byte positions in the stream.
- Acknowledgment numbers indicate the expected next byte.
- TCP offers cumulative acknowledgments.
- Handling out-of-order segments is at the discretion of TCP implementers.

![[Pasted image 20240412182820.png|400]]
**Telnet: A Case Study**
- Telnet, a remote login protocol, illustrates TCP sequence and acknowledgment numbers.
- Host A initiates a Telnet session with Host B.
- Each typed character undergoes a round trip between the client and server.
- Segments contain sequence numbers reflecting byte positions and acknowledgment numbers indicating the next expected byte.

*Note: Detailed examples and explanations were provided to elucidate TCP's functionality.*

### 3.5.3 **Round-Trip Time Estimation and Timeout in TCP**

- **Concept:** TCP implements a timeout/retransmit mechanism akin to the rdt protocol, aiming to recover from lost segments. This involves addressing various subtleties, particularly concerning timeout intervals.
- **Round-Trip Time (RTT) Estimation:** TCP estimates RTT between sender and receiver, crucial for setting timeout intervals. It measures SampleRTT, the time between segment transmission and acknowledgment receipt. TCP maintains an EstimatedRTT, an average of SampleRTT values, using an exponential weighted moving average (EWMA) formula.
	- `EstimatedRTT = (1 – α) * EstimatedRTT + α * SampleRTT`
- **RTT Variability:** DevRTT estimates the variability of RTT, providing insights into fluctuations in SampleRTT values. It also utilizes an EWMA formula to track deviations from EstimatedRTT.
	- `DevRTT = (1 – β) * DevRTT + β * | SampleRTT – EstimatedRTT |`
- **Setting Timeout Interval:** TCP determines the timeout interval (TimeoutInterval) based on EstimatedRTT and DevRTT. The interval should be greater than EstimatedRTT but not excessively so, considering DevRTT to avoid unnecessary retransmissions or delayed retransmissions.
	- `TimeoutInterval = EstimatedRTT + 4 * DevRTT`
- **Initial Timeout and Adjustment:** An initial TimeoutInterval value of 1 second is recommended, doubling upon timeout occurrence to prevent premature timeouts. Upon acknowledgment receipt, TimeoutInterval is recalculated using the formula.

**Vinton Cerf, Robert Kahn, and TCP/IP**

- **Origins:** In the early 1970s, Vinton Cerf and Robert Kahn envisioned interconnecting diverse packet-switched networks, leading to the development of TCP/IP (Transmission Control Protocol/Internet Protocol).
- **Protocol's Significance:** TCP/IP, devised before modern networking technologies and applications, laid the foundation for today's Internet. It aimed to support various applications while facilitating interoperability among different hosts and link-layer protocols.
- **Recognition:** In 2004, Cerf and Kahn were honored with the ACM Turing Award for their pioneering work on TCP/IP, recognized as fundamental to internetworking and basic communications protocols design.

### 3.5.4 **Reliable Data Transfer**

The Internet's IP service is **unreliable**, leading to issues like datagram loss, out-of-order delivery, and data corruption. TCP ensures **reliable data transfer** despite this. It guarantees uncorrupted, ordered, and gapless data streams.

- **Timer Management:** TCP uses a **single retransmission timer** to manage unacknowledged segments, reducing overhead.
- **Steps for Reliable Transfer:** TCP's process involves data reception, timeout, and acknowledgment receipt.
- **Timeout Handling:** TCP retransmits lost segments upon timeout and restarts the timer.
- **Acknowledgment Handling:** Upon ACK receipt, TCP updates its SendBase and potentially restarts the timer.

**Interesting Scenarios:**
- **Scenario 1:** A lost acknowledgment triggers retransmission, avoiding duplicate data at the receiver.
- **Scenario 2:** Back-to-back segments are sent; if one is lost, only it is retransmitted upon timeout.
- **Scenario 3:** If acknowledgment is received before timeout, no retransmission occurs.
![[Pasted image 20240412184204.png|700]]

**Timeout Interval Modification:**
- TCP employs an **exponential increase** in timeout intervals for retransmitted segments to mitigate congestion.
- This aids in **congestion control** by preventing persistent retransmissions during network congestion.
**Fast Retransmit:**
![[Pasted image 20240412184234.png|400]]
- Duplicate ACKs trigger **fast retransmit**, enabling prompt retransmission of lost segments.
- TCP reacts to **three duplicate ACKs** by retransmitting the missing segment.

**TCP Mechanism Analysis:**
- TCP's mechanism **evolves** based on extensive experience, addressing numerous subtle issues.
- TCP's error-recovery mechanism combines elements of both Go-Back-N and Selective Repeat protocols.
- **Selective acknowledgment** enhances TCP's error recovery, allowing for selective retransmission of out-of-order segments.

TCP's approach to reliable data transfer balances efficiency and robustness, evolving over decades of refinement.

### 3.5.5 **Flow Control**
![[Pasted image 20240412184307.png|400]]
In TCP connections, hosts allocate receive buffers to store incoming data, allowing application processes to read data at their own pace. However, if the sender transmits data faster than the receiver can process, buffer overflow can occur. TCP addresses this with **flow control**, ensuring the sender matches its transmission rate to the receiver's reading rate.

- **Flow Control vs. Congestion Control:** Flow control regulates sender speed to match receiver capacity, while congestion control throttles sender due to network congestion.
- **Receive Window:** TCP sender maintains a variable representing available buffer space at the receiver.
- **Dynamic Receive Window:** Adjusts based on buffer space availability.
- **TCP Operation:** Hosts exchange the current receive window value to regulate data transmission.
- **Buffer Full Issue:** When the receiver's buffer is full, TCP requires the sender to continue sending small segments to prevent blocking.
- **UDP Contrast:** UDP lacks flow control, leading to potential segment loss at the receiver due to buffer overflow.

TCP's flow control mechanism ensures efficient data transmission, contrasting with UDP's lack of control, which can lead to data loss under heavy load.
### 3.5.6 **TCP Connection Management**
![[Pasted image 20240412184337.png|300]]![[Pasted image 20240412184350.png|300]]
In TCP connection management, understanding how a connection is established and torn down is crucial. TCP connection establishment can contribute to perceived delays and is vulnerable to network attacks like SYN flood attacks. The process involves three steps:

1. **Connection Establishment:**
   - Client sends a SYN segment to the server, initiating the connection.
   - Server responds with a SYNACK segment, acknowledging and agreeing to the connection.
   - Client acknowledges the server's response, completing the three-way handshake.

2. **Connection Termination:**
   - Either party can initiate connection closure by sending a FIN segment.
   - After a series of acknowledgments, resources in both hosts are deallocated.

During a TCP connection's lifecycle, hosts transition through various states, starting from CLOSED to ESTABLISHED and ending in CLOSED again. The duration of these states varies based on implementation, typically involving states like FIN_WAIT_1, FIN_WAIT_2, and TIME_WAIT.

In cases where TCP segments with mismatched port numbers or source IP addresses are received, hosts respond with reset segments or ICMP datagrams, indicating a lack of matching sockets.

The nmap port-scanning tool utilizes TCP SYN segments to explore specific ports on a target host, determining whether they are open, blocked, or unresponsive. It aids in analyzing firewall configurations and detecting application versions and operating systems.

TCP connection management is essential for error control and flow control in TCP. In the next section, TCP congestion control will be explored in more detail, followed by a broader examination of congestion-control issues.

## 3.6 **Principles of Congestion Control**

In this section, we delve into **congestion control** principles and their application in TCP to ensure reliable data transfer amidst packet loss due to network congestion. While **packet retransmission** addresses the symptom of congestion, the underlying issue lies in the excessive data transmission rates.

### 3.6.1 Causes and Costs of Congestion
__Scenario 1: Two Senders, Infinite Buffer Router__
- As the sending rate approaches R/2, throughput at the receiver hits a ceiling.
- Congestion leads to unbounded queuing delays and infinite delays in extreme cases.

__Scenario 2: Two Senders, Finite Buffer Router__
- Packet loss occurs when buffers are full, triggering retransmissions.
- Throughput depends on retransmission strategies, with increased delays and wasted bandwidth due to unnecessary retransmissions.

__Scenario 3: Four Senders, Finite Buffer Routers, Multihop Paths__
- High traffic leads to buffer overflows, causing reduced throughput.
- Competition for buffer space results in decreased throughput for certain connections, leading to a tradeoff between offered load and throughput.

__Conclusion__
Congestion control mechanisms are crucial to ensure efficient network performance, mitigating the adverse effects of packet loss and optimizing resource utilization.

## **3.7 TCP Congestion Control**

**Overview:**
  - **Definition:** TCP provides reliable transport service.
  - **Focus:** Examines TCP congestion-control mechanisms.
  - **Approach:** Classic TCP uses end-to-end congestion control.
  - **Newer Flavors:** Explores TCP versions with explicit congestion indication.
  - **Challenge:** Achieving fairness among shared congested links.

### 3.7.1 Classic TCP Congestion Control
  - **Sender's Role:** Limits traffic based on perceived congestion.
  - **Variables:** Includes congestion window (cwnd), receive window (rwnd).
  - **Congestion Window:** Constraints sender's rate based on unacknowledged data.
  - **Congestion Detection:** Loss event triggers perception of congestion.
  - **Acknowledgments:** Indicate successful delivery, leading to rate increase.
  - **Guiding Principles:** Lost segment implies congestion, acknowledged segment indicates network health.

**TCP Congestion-Control Algorithm**
![[Pasted image 20240412185107.png|400]]
  - **Components:** Slow start, congestion avoidance, fast recovery.
  - **Slow Start:** Exponential growth of congestion window until loss event or threshold.
  - **Congestion Avoidance:** Linear increase in congestion window, cautious approach.
  - **Fast Recovery:** Increases congestion window based on duplicate ACKs, transitions based on loss events.

**TCP Cubic**
![[Pasted image 20240412185230.png|400]]
  - **Objective:** Probes for optimal sending rate more aggressively.
  - **Approach:** Increases congestion window as a function of time.
  - **Comparison:** Provides higher throughput than TCP Reno in certain scenarios.
  - **Deployment:** Widely adopted, especially in Linux operating system.

![[Pasted image 20240412185200.png|500]]
**Macroscopic Description of TCP Reno Throughput**
  - **Steady-State Behavior:** TCP's throughput ranges between minimum and maximum values.
  - **Average Throughput:** Calculated as 0.75 times the congestion window size divided by round-trip time.

This section delves into TCP's congestion-control mechanisms, focusing on classic approaches and newer flavors like TCP Cubic. It details algorithms like slow start, congestion avoidance, and fast recovery, explaining their roles in adjusting sending rates based on network conditions. Additionally, it provides insights into TCP Cubic's aggressive probing for optimal sending rates and offers a macroscopic description of TCP Reno's throughput behavior.

### 3.7.2 **Network-Assisted Explicit Congestion Notification and Delayed-based Congestion Control**

**Explicit Congestion Notification (ECN)**
![[Pasted image 20240412185558.png|500]]
- TCP's congestion control inferred congestion through observed packet loss.
- Extensions to IP and TCP [RFC 3168] allow explicit signaling of congestion.
- ECN involves TCP and IP, utilizing two bits in the Type of Service field of the IP datagram header.
- Routers signal congestion to TCP sender via marked IP datagram.
- TCP sender reacts to congestion by halving congestion window and setting Congestion Window Reduced (CWR) bit.
- Datagram Congestion Control Protocol (DCCP), DCTCP, and DCQCN utilize ECN.
- Increasing deployment of ECN capabilities observed in servers and routers.

**Delay-based Congestion Control**
- TCP Vegas measures Round-Trip Time (RTT) to detect congestion onset.
- Uncongested throughput rate calculated using RTTmin and congestion window size.
- TCP Vegas aims to keep the pipe just full, avoiding increased delay.
- BBR protocol builds on TCP Vegas ideas for fair competition with non-BBR TCP senders.
- Other delay-based TCP congestion control protocols include TIMELY, Compound TCP (CTPC), and FAST.

### 3.7.3 Fairness
- TCP's AIMD algorithm aims for equal sharing of link bandwidth among connections.
- TCP congestion control converges to provide an equal share of a bottleneck link’s bandwidth.
- Conditions such as RTT, multiple connections, and packet loss influence fairness.
- Multimedia applications over UDP may not cooperate with TCP's congestion control, impacting fairness.
- Parallel TCP connections in applications can lead to unfair bandwidth allocation, common in web traffic.
  
## 3.8 **Evolution of Transport-Layer Functionality**

- **TCP and UDP:** Dominant transport layer protocols with decades of experience.
- **TCP Evolution:** Numerous newer versions like TCP CUBIC, DCTCP, CTCP, BBR, tailored for diverse scenarios.
- **Diverse TCP Versions:** For wireless links, high-bandwidth paths, packet re-ordering, and data centers, among others.
- **QUIC (Quick UDP Internet Connections):**
    - **Purpose:** Designed to address needs between UDP and TCP.
    - **Deployment:** Widely used by Google, YouTube, Chrome, and Android.
    - **Features:** Combines speed and security, multiplexes streams, and ensures reliable, TCP-friendly congestion control.
    - **Design:** Built on UDP, interfaces with evolved HTTP/2, soon to be integrated with HTTP/3.
    - **Advantages:** Faster establishment, stream-based data delivery, and adaptable congestion control.
    - **Contribution:** Offers flexibility for application-layer updates at a faster pace than TCP or UDP.

*Note: QUIC represents a significant advancement in transport-layer protocols, offering enhanced performance and adaptability for modern internet applications.*


# 4. The Network Layer: Data Plane

## 4.2 What’s Inside a Router?

- **Router Components**:
  - **Input Ports**:
    - Functions include terminating incoming physical links, performing link-layer functions, and crucially, a lookup to consult the forwarding table to determine the output port for forwarding packets via the switching fabric.
    - Control packets are directed from the input port to the routing processor.
    - The number of ports in routers varies significantly, from a few in enterprise routers to hundreds in ISPs' routers, such as the Juniper MX2020, which supports up to 800 100 Gbps Ethernet ports.
  - **Switching Fabric**:
    - Connects the router’s input ports to its output ports, effectively acting as a network within a router.
  - **Output Ports**:
    - Store and transmit packets received from the switching fabric, handling necessary link-layer and physical-layer functions.
    - Typically paired with the corresponding input port on the same line card for bidirectional traffic.
  - **Routing Processor**:
    - Handles control-plane functions, executes routing protocols, maintains routing and forwarding tables, and in SDN routers, communicates with the remote controller to receive and install forwarding table entries.
    - Manages network functions and typically executes slower control activities, such as responding to changes in link states and managing the router.

- **Performance and Implementation**:
  - Hardware is often used for input ports, switching fabric, and output ports due to the high speed required for processing datagrams in large routers.
  - Control functions, which operate on a slower timescale (milliseconds to seconds), are typically implemented in software on the routing processor.

- **Analogy and Practical Considerations**:
  - Packet forwarding is likened to cars entering and exiting a roundabout, with the input port acting as the entry station where directions are given, the switching fabric as the roundabout itself, and the output port as the exit road.
  - Potential bottlenecks include rapid packet arrival rates and slow processing rates at the input ports, analogous to fast cars and a slow station attendant.
  - Router and switch designers must consider these dynamics to prevent backups and efficiently manage traffic prioritization and blocking.

### 4.2.1 Input Port Processing and Destination-Based Forwarding
- **Input Processing at Router Ports**: Critical for router operation, involving physical and link-layer processing.
- **Forwarding Table Lookup**:
  - Essential task performed at each router's input port.
  - Determines the output port for packet forwarding based on the packet’s destination address.
  - Forwarding tables are populated by routing processors or SDN controllers and are essential for making forwarding decisions locally at each input port.

- **Forwarding Mechanisms**:
  - **Destination-Based Forwarding**: Utilizes a forwarding table where packet forwarding is determined by matching the packet's destination IP address with table entries.
  - **Handling Large Address Spaces**: Instead of a direct one-to-one mapping, routers use prefix matching to efficiently manage and lookup addresses.
  - **Longest Prefix Matching Rule**: When multiple prefix matches occur, the router selects the entry with the longest matching prefix, critical for correct routing decisions.

- **Lookup Efficiency**:
  - **High-Speed Requirements**: Lookups need to be extremely fast, especially at gigabit transmission rates, necessitating hardware-based solutions.
  - **Advanced Lookup Technologies**:
    - Utilization of Ternary Content Addressable Memories (TCAMs) for rapid lookup processes.
    - TCAMs allow for quick searches through large forwarding tables by returning forwarding information almost instantaneously.

- **Packet Handling Post-Lookup**:
  - **Switching Fabric Entry**: Once the output port is determined, the packet is sent to the switching fabric for transfer to the correct output port.
  - **Queue Management**: Packets may be queued at the input port if the switching fabric is currently occupied by packets from other ports, with scheduling for later transmission.

- **Additional Input Port Actions**:
  - Verification and rewriting of packet fields such as version number, checksum, and time-to-live.
  - Updating counters for network management purposes.

- **General "Match Plus Action" Abstraction**:
  - Used across various network devices (routers, switches, firewalls, NAT devices) for a broad range of actions beyond mere packet forwarding.
  - Involves matching certain packet attributes and performing specified actions based on these matches, integral to modern network forwarding logic.


### 4.2.2 Switching
![[Pasted image 20240415211232.png|500]]
- **Switching Fabric in Routers**: Central to routers, enabling packet forwarding from input to output ports. Several methods are used:

  - **Switching via Memory**:
    - **Early Routers**: Functioned as computers with CPUs controlling switching. Packets from input ports are moved to processor memory, then to output after routing decisions.
    - **Limitations**: Forwarding throughput is limited to less than half the memory bandwidth due to read/write constraints.
    - **Modern Variants**: Similar to shared-memory multiprocessors, input line cards perform address lookup and direct memory writing, e.g., Cisco Catalyst 8500 series.

  - **Switching via a Bus**:
    - **Direct Transfer**: Input ports send packets with a local header across a shared bus to the designated output port, which strips the header.
    - **Limitations**: The speed is restricted to the bus’s capacity, making it suitable only for smaller networks, e.g., Cisco 6500 router.

  - **Switching via an Interconnection Network**:
    - **Crossbar Switch**: Utilizes a grid of buses allowing multiple simultaneous packet transfers without blocking, unless two packets target the same output port.
    - **Advanced Configurations**: Cisco 12000 series employs crossbar switching; Cisco 7600 series can use both bus and crossbar configurations.
    - **Multi-Stage and Parallel Switching**: Multi-stage networks handle concurrent transfers to the same output, and parallel fabrics increase capacity by distributing packet chunks, e.g., Cisco CRS.

- **Sophisticated Interconnection Networks**:
  - **Multi-Stage Switching**: Allows simultaneous routing to the same output port using a complex fabric setup.
  - **Parallel Switching Fabrics**: Enhances capacity by dividing a packet into chunks processed by multiple fabrics.

### 4.2.3 Output Port Processing
- **Functions of Output Ports**:
  - **Storage and Transmission**: Packets are stored in memory before being sent over the output link.
  - **Scheduling and De-Queuing**: Decides the order of packet transmission.
  - **Transmission Protocols**: Manages link-layer and physical-layer transmission functions, ensuring packets are correctly formatted and timed for sending.

### 4.2.4 Where Does Queuing Occur?

- **Packet Queuing Locations**: Occurs at both the input and output ports of a router, akin to traffic queues in a roundabout analogy. 
- **Queue Formation Factors**: Influenced by traffic load, the speed of the switching fabric, and line speed.
- **Queueing Implications**: Large queues can exhaust router memory leading to packet loss.

__Detailed Examination of Queues__
![[Pasted image 20240415211212.png|500]]
- **Input Queues**:
  - **Conditions for Input Queueing**: Occurs if the switching fabric's transfer rate (Rswitch) is slower than the input line speeds (Rline), causing packets to wait in input port queues.
  - **Head-of-the-Line (HOL) Blocking**: A packet at the front of the queue prevents other packets from being transferred even if their destination output port is free, potentially leading to unbounded queue lengths and significant packet loss under certain load conditions.

![[Pasted image 20240415211153.png|500]]
- **Output Queues**:
  - **Conditions for Output Queueing**: Even with a switching fabric speed of N times the line speed, simultaneous arrival of packets destined for the same output port leads to queuing.
  - **Queue Management Decisions**: Involves choosing to drop the arriving packet or remove queued packets to make room, utilizing strategies like drop-tail or proactive packet marking with Explicit Congestion Notification (ECN).

__Buffering Considerations__
- **How Much Buffering Is Enough?**:
  - **Traditional Rule of Thumb**: Buffer size should equal the round-trip time (RTT) multiplied by the link capacity (C).
  - **Recent Insights**: In core networks with many TCP flows, buffer requirements decrease significantly, making the need for large buffers less critical.
  - **Buffering Effects**: While buffering can reduce packet loss by absorbing traffic fluctuations, it also increases queuing delays, which can affect applications like gaming and teleconferencing by increasing the end-to-end delay.

- **Bufferbloat Issue**:
  - **Persistent Buffering**: Leads to consistent queuing delays despite no apparent network congestion, known as bufferbloat.
  - **Network Standard Measures**: The DOCSIS 3.1 standard includes AQM mechanisms specifically to address bufferbloat while maintaining throughput performance.

### 4.2.5 Packet Scheduling
Packet scheduling involves determining the order of packet transmission over an outgoing link, managing how queued packets are processed. Different queuing disciplines are used, each with its own methodology for handling packet transmission.

- **First-in-First-Out (FIFO) Discipline**:
  - FIFO, also known as first-come-first-served (FCFS), processes packets in the order they arrive. If the link is busy, packets wait in the queue until they can be transmitted. There is no preemption; once a packet transmission starts, it continues to completion. This method is straightforward but can lead to inefficiencies if the packet mix varies significantly in importance or size.

- **Priority Queuing**:
  - This method classifies incoming packets into priority classes at the queue. Packets from higher priority classes are transmitted first, regardless of their arrival time relative to packets in lower priority classes. This ensures critical information, such as network management or real-time packets (e.g., VoIP), is transmitted ahead of less critical data like emails.

- **Round Robin and Weighted Fair Queuing (WFQ)**:
  - Round Robin queuing alternates packet transmission between classes, ensuring no class dominates the transmission time. It’s a work-conserving discipline that continuously checks for packets in all classes, avoiding idle link time.
  - WFQ, an advanced form of Round Robin, assigns weights to each packet class, determining the fraction of bandwidth each class receives relative to others. This weighted approach allows for more nuanced control of transmission priorities, accommodating varying needs of packet classes efficiently.

## 4.3 The Internet Protocol (IP)
- **Context**: This section of the network layer includes data and control plane components, forwarding and routing, various network service models, and internal router operations without reference to any specific network architecture.
- **Focus**: Details the functioning of the Internet Protocol (IP) which is central to the Internet’s network layer.

### 4.3.1 IPv4 Datagram Format
![[Pasted image 20240415211124.png|400]]
- **IPv4**: The primary version of Internet Protocol in use, defined in RFC 791.
- **IPv6**: Proposed as a replacement for IPv4 to address its limitations, detailed in RFC 2460 and RFC 4291.
- **Datagram Structure**: Describes the anatomy of IPv4 datagrams:
  - **Version Number**: 4 bits indicating the IP protocol version, critical for routers to process the datagram correctly.
  - **Header Length**: 4 bits specifying the start of the payload, influenced by variable options included in the header.
  - **Type of Service (TOS)**: Distinguishes between types of traffic (e.g., real-time vs. non-real-time) and incorporates Explicit Congestion Notification.
  - **Datagram Length**: 16-bit field defining the total length of the datagram; typically does not exceed 1,500 bytes to fit within an Ethernet frame.
  - **Identifier, Flags, Fragmentation Offset**: Manage IP fragmentation for large datagrams which is not supported in IPv6.
  - **Time-to-Live (TTL)**: Ensures datagrams do not remain indefinitely in the network by decrementing this field at each router hop.
  - **Protocol**: Indicates the transport-layer protocol (e.g., TCP or UDP) to which the datagram’s data should be passed at the destination.
  - **Header Checksum**: Helps detect bit errors in the datagram at routers, recalculated at each hop due to changes in the TTL.
  - **Source and Destination IP Addresses**: Set by the source using DNS lookup, crucial for routing the datagram.
  - **Options**: Allows extension of the IP header; used rarely to avoid complexity and processing delays.
  - **Data (Payload)**: Carries the transport-layer segment or other data types like ICMP messages.

### 4.3.2 IPv4 Addressing
IPv4 addressing is a nuanced and critical aspect of Internet infrastructure, playing a central role in network communication.
![[Pasted image 20240415211104.png|500]]

- **Interfaces and IP Address Association**:
  - Devices (hosts and routers) connect to the Internet via interfaces.
  - Each interface has a unique IP address.
  - A router has multiple interfaces to manage data forwarding across different network links.

- **IP Address Structure**:
  - An IPv4 address is 32 bits long, divided into 4 bytes.
  - Expressed in dotted-decimal notation, e.g., 193.32.216.9.
  - Globally unique except when obscured by Network Address Translation (NAT).

- **Subnetting**:
  - IP addresses may share a common prefix indicating they belong to the same subnet.
  - Example: 223.1.1.xxx where xxx varies per device within the subnet.
  - A subnet can be an Ethernet LAN or connected via other technologies like wireless access points.

- **CIDR (Classless Interdomain Routing)**:
  - IP addresses are split into two parts; the network prefix and the host identifier.
  - CIDR uses notation like a.b.c.d/x to specify network size.
  - Helps reduce routing table size externally by using only the network prefix for routing decisions.
  
- **Subnet Structure**:
  - Within an organization, different subnets may exist, often with similar subnet addresses.
  - Subnets are defined by isolating network interfaces and recognizing them as distinct network segments.

- **Classful vs. Classless Addressing**:
  - Pre-CIDR, addressing was classful (Class A, B, C) with fixed subnet lengths of 8, 16, or 24 bits.
  - CIDR allows for variable length subnet masks, optimizing address allocation and usage.

- **IP Broadcast Address**:
  - The address 255.255.255.255 is used for broadcasting to all hosts on the same subnet.

- **Address Assignment**:
  - Organizations receive a block of addresses with a common prefix.
  - Devices within the organization are assigned addresses from this block, potentially using further subnetting within the organization.

![[Pasted image 20240415211028.png|500]]

__Obtaining a Block of Addresses__
- **Process of Acquiring IP Addresses**:
  - Organizations typically contact their ISP to obtain a block of IP addresses.
  - The ISP provides a subdivision of a larger block it owns, like dividing a 200.23.16.0/20 block into smaller /23 blocks for distribution among organizations.

- **Global IP Address Management**:
  - IP addresses are globally managed by the Internet Corporation for Assigned Names and Numbers (ICANN), which allocates blocks to regional Internet registries (e.g., ARIN, RIPE).
  - ICANN also manages DNS root servers and resolves domain name disputes.

__Dynamic Host Configuration Protocol (DHCP)__
![[Pasted image 20240415210931.png|350]]![[Pasted image 20240415210915.png|350]]
- **Functionality and Importance**:
  - DHCP allows automatic IP address assignment to hosts, making network configuration easier and supporting frequent network changes without manual setup.
  - It is essential in environments with high mobility, such as campuses where students move between multiple locations.

- **DHCP Operation**:
  - Consists of four main steps: Server Discovery, Server Offer(s), Request, and Acknowledgment (ACK).
  - A client first discovers servers via a broadcast message, receives offers, selects an offer, and finally receives an ACK to confirm the IP address configuration.

- **Benefits and Implementation**:
  - Reduces the administrative burden of manually configuring IP addresses.
  - Widely used in various network environments including residential, enterprise, and wireless networks due to its plug-and-play capability.

- **DHCP and Mobility**:
  - Although DHCP supports IP reassignment for mobile devices changing subnets, it does not maintain TCP connections during these transitions, which is a significant limitation for continuous connectivity.
  
- **Renewing and Managing Leases**:
  - DHCP allows for lease renewal, which lets a host extend its IP address allocation beyond the initial lease duration.
  - Provides a mechanism to manage network configurations over time efficiently.

- DHCP returns
	- The addressed IP, subnet mask, address of first-hop router

#### 4.3.3 Network Address Translation (NAT)
![[Pasted image 20240415210846.png|500]]
- **Context and Necessity**:
  - Every IP-capable device requires a unique IP address. Given the multitude of devices in small office, home office (SOHO) networks, this could mean a substantial block of IP addresses needed from ISPs. Address management by typical homeowners is impractical.

- **NAT Solution**:
  - **Network Address Translation (NAT)** simplifies IP address allocation for multiple devices within private networks like SOHOs, circumventing the need for extensive public IP address allocations from ISPs.

- **Private Network Addressing**:
  - Within a home network, devices use a common subnet address (e.g., 10.0.0.0/24). This address space is reserved for private networks and is meaningless outside of this local context.

- **Functionality of NAT**:
  - A NAT-enabled router presents itself to the internet with a single IP address. Internally, it manages a local network with private addresses, using a NAT translation table to map external connections back to the correct internal devices.

- **Operational Details**:
  - Devices within the NAT network communicate using private addresses, while external communication uses a translated public address provided by the NAT router.
  - The NAT router uses a translation table to track and map internal private addresses and port numbers to a single public address and corresponding ports.

- **Challenges and Criticisms**:
  - Technical: NAT can complicate server operations and peer-to-peer connections within the network because it alters address and port information.
  - Philosophical: NAT disrupts the architectural purity of network-layer operations by modifying packet data, which some argue should not happen in routers.

- **Technological Adaptations**:
  - **NAT Traversal Tools**: Developed to address connectivity issues caused by NAT, facilitating communications and services that require device discoverability and accessibility.

### 4.3.4 IPv6
![[Pasted image 20240415210828.png|400]]
- **Development and Motivation**: Initiated in the early 1990s by the Internet Engineering Task Force to address the limitations of the 32-bit address space of IPv4 which was rapidly depleting. This was due to the high rate of new subnets and IP nodes requiring unique IP addresses.
- **IPv6 Features**:
  - **Expanded Addressing Capabilities**: Increases IP address size from 32 to 128 bits, essentially ensuring an almost unlimited number of IP addresses.
  - **Simplified 40-byte Header**: Drops several IPv4 fields, making IPv6 headers streamlined for faster processing by routers.
  - **Flow Labeling**: Introduces the concept of flows, potentially allowing for differentiating service quality among different types of data traffic.
- **Key Fields in IPv6 Datagram**:
  - **Version**: Identifies the version of IP being used (6 for IPv6).
  - **Traffic Class**: Similar to the TOS field in IPv4, used for prioritizing datagrams.
  - **Flow Label**: Used to identify a flow of datagrams for special handling.
  - **Payload Length**: Indicates the size of the payload.
  - **Next Header**: Identifies the protocol for the payload.
  - **Hop Limit**: Replaces the TTL field from IPv4; decremented by routers to limit datagram lifetime.
  - **Source and Destination Addresses**: Now 128-bit, supporting a larger address space.
  - **Data**: The payload of the datagram.

![[Pasted image 20240415210807.png|500]]
- **Transition from IPv4 to IPv6**:
  - **Challenges**: IPv4 systems cannot inherently process IPv6 datagrams, complicating the transition.
  - **Tunneling Method**: Widely adopted method involving encapsulating IPv6 datagrams within IPv4 datagrams to bridge IPv4 and IPv6 systems.
- **Current Adoption and Future Outlook**:
  - Slow initial uptake, but increasing deployment driven by the proliferation of IP-enabled devices.
  - Future changes in the network layer are expected to occur at a slower pace compared to rapid developments at the application layer.

## 4.4 Generalized Forwarding and SDN
![[Pasted image 20240415210738.png|500]]
- **Match-plus-action paradigm**: This advanced forwarding approach extends beyond simple destination-based forwarding. It involves matching packets based on multiple header fields across various network layers and executing actions like forwarding, load balancing, rewriting headers (e.g., NAT), blocking/dropping packets (firewall actions), or sending packets for further processing (DPI).
- **Generalized forwarding devices**: Previously known as layer 3 routers or layer 2 switches, these are now referred to as packet switches in SDN contexts. They operate based on match-plus-action tables managed by a remote controller.

__OpenFlow Standard__
- **Introduction**: OpenFlow, a prominent standard in SDN, introduces the match-plus-action concept. It allows for extensive network programmability, changing the landscape of network management and operation.
- **Flow table components**:
  - **Header field values**: Incoming packets are matched to specified header field values.
  - **Counters**: Updated as packets match the entries, recording metrics like match frequency and last update time.
  - **Actions**: Defined per entry, actions may include forwarding packets to specific ports, dropping packets, or rewriting headers.

### 4.4.1 Match
![[Pasted image 20240415210715.png|500]]
- **OpenFlow 1.0 specifics**:
  - **Header fields for matching**: Up to 12 different values can be matched, covering multiple layers (link-layer, network-layer, and transport-layer). The specifications have expanded in later versions.
  - **Wildcard entries**: Support for broad matching criteria, such as an IP address with wildcard segments, enhancing flexibility.
  - **Priority settings**: Multiple matches are resolved by prioritizing entries, ensuring that the most critical rules are applied first.

### 4.4.2 Action
- **Flow Table Actions**:
  - **Forwarding**: Packets can be directed to specific ports, broadcasted, multicast, or sent to a remote controller which might alter flow table rules.
  - **Dropping**: Indicates packets that match this entry should be discarded.
  - **Modify-field**: Allows rewriting values in 10 packet-header fields before forwarding to the designated port.

### 4.4.3 OpenFlow Examples of Match-plus-action in Action
![[Pasted image 20240415210659.png|500]]
- **Network Configuration**:
  - **Network Components**: 6 hosts (h1 to h6) and 3 packet switches (s1, s2, s3) with 4 interfaces each.
- **OpenFlow Examples**:
  - **Example 1: Simple Forwarding**:
    - Packets from h5 and h6 to h3 and h4 are forwarded from s3 to s1, then from s1 to s2, avoiding the link between s3 and s2.
  - **Example 2: Load Balancing**:
    - Datagrams from h3 destined to 10.1.*.* are sent from s2 to s1 directly.
    - Datagrams from h4 destined to 10.1.*.* go from s2 to s3, then to s1.
    - Flow table entries are required at s1 and s3 to manage the forwarding paths.
  - **Example 3: Firewalling**:
    - s2 is configured to receive traffic only from hosts connected to s3.
    - Only traffic from 10.3.*.* would be allowed through to s2 if no other entries contradict this in s2’s flow table.
- **Versatility of Generalized Forwarding**:
  - Flow tables allow for the creation of various network behaviors such as virtual networks using the same physical infrastructure.
- **Flow Tables in SDN Controllers**:
  - Reviewed in context with SDN controllers that calculate and distribute flow tables and manage communications between switches and controllers.

## 4.5 **Middleboxes**

In the realm of networking, **routers** are fundamental for forwarding IP datagrams to their destinations. However, there are additional network devices termed **"middleboxes"** that perform functions beyond mere forwarding, encountered throughout various chapters.

Middleboxes encompass a range of equipment including **Web caches, TCP connection splitters, NAT, firewalls,** and **intrusion detection systems (IDS)**. These devices play roles in **NAT translation,** **security services,** and **performance enhancement.**

- **NAT Translation:** Middleboxes rewrite datagram header IP addresses and port numbers for private network addressing.
- **Security Services:** Firewalls block traffic based on header-field values or redirect packets for additional processing, such as deep packet inspection (DPI). IDS detect predetermined patterns and filter packets accordingly. Application-level e-mail filters combat junk, phishing, and security threats.
- **Performance Enhancement:** Middleboxes offer services like compression, content caching, and load balancing to improve service requests.

The rise of middleboxes poses challenges in terms of operation, management, and upgrade due to separate specialized hardware and software stacks, leading to significant costs. Consequently, **network function virtualization (NFV)** and outsourcing middlebox functionality to the cloud are explored as alternatives.

Middleboxes challenge the traditional separation between the network layer and the transport/application layers. While some view them as an architectural deviation, others argue for their necessity and anticipate their proliferation in the future.

This debate raises questions about the placement of service functionality in a network, touching upon the principles of the **"end-to-end argument."**


**Architectural Principles of the Internet**

The Internet's success prompts inquiry into its guiding architectural principles. RFC 1958 proposes minimal principles: connectivity as the goal, the Internet Protocol (IP) as the tool, and intelligence predominantly at the network edge.

**The IP Hourglass**

Illustrated by the "IP hourglass," the Internet's layered architecture focuses on IP as the singular network layer protocol. Its simplicity fosters the integration of diverse networks into the Internet, bridging varying link-layer technologies.

**The End-to-End Argument**

Echoing RFC 1958, functionality is primarily placed at endpoints rather than within the network. The "end-to-end argument" posits that certain functions require application-level knowledge for effective implementation, advocating for intelligence at endpoints. For instance, reliable data transfer necessitates end-to-end implementation due to potential packet loss within the network.

These principles, articulated in fundamental papers like [Saltzer 1984] and [Clark 1988], underpin Internet architecture. Follow-up discussions further explore these principles in the context of the evolving Internet landscape.


# 5. The Network Layer: Control Plane

## 5.1 Introduction

**Context and Components**:
  - **Forwarding and Flow Tables**: Central elements linking the network layer's data and control planes, guiding local data-plane forwarding actions in routers, including forwarding, dropping, replicating packets, and modifying packet headers.

**Computing, Maintaining, and Installing Tables**:
  - Explores methods to compute, maintain, and install forwarding and flow tables.

**Control Approaches**:
  - **Per-router Control**:
    - Each router runs a routing algorithm independently.
    - Routers communicate to compute forwarding table values.
    - Used for decades with protocols like OSPF and BGP 

  **Logically Centralized Control**:
-  A centralized controller computes and distributes forwarding tables.
- Enables traditional IP forwarding and additional functions like load sharing, firewalling, and NAT previously done by separate middleboxes.
- Routers interact with a central controller through a control agent (CA) which follows commands to manage the router’s flow table.
- Distinct from per-router control as CAs do not interact or compute tables themselves.

**Definition and Implementation**:
  - **Logically Centralized**: The control appears centralized for accessibility and management, though it is often implemented across multiple servers for fault tolerance and performance scalability.

**Real-world Applications**:
  - **Software-Defined Networking (SDN)**:
    - Increasingly used in production networks.
    - Examples include Google's B4 network, Microsoft's SWAN, Comcast's ActiveCore, and Deutsche Telecom’s Access 4.0.
    - Central to modern networking infrastructures like 4G/5G.
    - Notable usage by AT&T with plans for extensive network virtualization and software control.
    - Applied by China Telecom and China Unicom within and between data centers.

## 5.2 Routing Algorithms

__Overview of Routing Algorithms__
- **Purpose**: Determine optimal paths from senders to receivers through a network of routers.
- **Criteria for 'good' paths**: Typically, paths with the least cost, although real-world policies may affect routing decisions (e.g., organizational policies preventing routers from handling packets from certain networks).

__Graph Representation of Routing Problems__
- **Graph G = (N, E)**: Consists of nodes (N) representing routers and edges (E) representing physical links.
- **Edge Costs**: Reflect physical distance, link speed, or monetary costs. For any edge (x, y), cost is denoted as c(x, y), with c(x, y) = ∞ if (x, y) is not part of E.
- **Graph Type**: Discussion primarily around undirected graphs where edges do not have a specific direction, implying c(x, y) = c(y, x).

__Routing Algorithm Objectives__
- **Goal**: Identify the least costly paths between sources and destinations.
- **Path Cost Calculation**: The cost of a path is the sum of the costs of all edges it includes.
- **Example**: If all edges have equal cost, the least-cost path is also the shortest path in terms of the number of links.

__Types of Routing Algorithms__
- **Centralized Routing Algorithms**:
	- Compute paths using complete, global knowledge of the network.
	- Often referred to as link-state (LS) algorithms.
	- Example: Calculation can be done at a centralized controller.
- **Decentralized Routing Algorithms**:
	- Calculate paths in a distributed manner, starting with knowledge only of directly attached links.
	- Example: Distance-vector (DV) algorithms, where each router maintains a vector of cost estimates to all other nodes.
  
__Static vs. Dynamic Routing__
- **Static Routing**: Routes change slowly, often manually adjusted.
- **Dynamic Routing**: Paths adjust in response to changes in network traffic loads or topology, more responsive but can lead to routing loops and oscillations.
	- Used in network providers

__Load Sensitivity in Routing__
- **Load-sensitive**: Link costs vary to reflect current congestion levels, can reroute traffic around congested links.
- **Load-insensitive**: Costs do not reflect current congestion levels. Most modern Internet routing protocols (e.g., RIP, OSPF, BGP) are load-insensitive due to historical difficulties with load-sensitive routing.

### 5.2.1 The Link-State (LS) Routing Algorithm

__Overview of Link-State (LS) Routing Algorithm__
- **Fundamental Concept**: All nodes possess identical, complete knowledge of the network topology and link costs.
- **Implementation**: Nodes broadcast link-state packets containing the identity and costs of attached links to all other nodes in the network, achieving uniform awareness across the network.

__Key Algorithm: Dijkstra's Algorithm__
```
Initialization:
	N' = {u}
	for all nodes v
		if v is neighbor of u
			then D(v)=c(u,v)
		else D(v) = inf

Loop
	find w not in N' such that D(w) is minimum
	add w to N'
	update D(v) for each neighbor v of w and not in N':
		D(v) = min(D(v),D(w)+e(w,v))
until N'= N
```
- **Functionality**: Computes the least-cost path from a source node to all other nodes.
- **Iterative Process**:
	- **Initialization**: Begins with direct path costs to neighbors.
	- **Iteration Steps**: Sequentially adds nodes to the set $ N' $ (nodes with known least-cost paths) and updates path costs to other nodes.
- **Outcome**: At termination, provides the shortest paths from the source to all network nodes, forming the basis for constructing forwarding tables.

__Detailed Steps of Dijkstra's Algorithm__
- **Initialization**: Known costs to direct neighbors are set (e.g., to infinity if not directly connected).
- **First Iteration**: Identify the node with the smallest known cost not yet in $ N' $, update path costs based on this node.
- **Subsequent Iterations**: Continue adding nodes with the least cost to $ N' $ and update path costs.

__Example Calculation__
![[Pasted image 20240423133636.png|200]]![[Pasted image 20240423133652.png|400]]
- **Network Analysis**: From a given source node $ u $, detailed calculations show iterative updates of path costs to all destinations in the network, as visualized in a tabular format 
- __Result__:
  ![[Pasted image 20240423133801.png|450]]

__Computational Complexity__
- **Initial Complexity**: $ O(n^2) $ based on iterative node inclusion and path cost updates.
- **Optimization**: Using a heap data structure can reduce complexity by optimizing the search for the minimum cost node. O(n$\cdot$logn)

__Considerations and Pathologies__
- **Dynamic Link Costs**: If link costs reflect real-time traffic load, path costs may not be symmetric and can lead to oscillations in route determination.
- **Prevention of Oscillations**:
	- Staggering the execution of the LS algorithm across different nodes.
	- Randomizing times for sending link-state advertisements to prevent algorithm synchronization across routers.
- What about equal cost paths?
	- Use hashing to take care of it.

### 5.2.2 The Distance-Vector (DV) Routing Algorithm

__Overview of Distance-Vector Routing__
- **Nature**: Iterative, asynchronous, and distributed.
- **Process**:
	- Each node calculates the least-cost paths based on information from directly attached neighbors.
	- Nodes continuously exchange this information until no changes are detected (self-terminating).
- **Features**: Unlike centralized systems, the DV algorithm does not require nodes to operate synchronously.

__Bellman-Ford Equation__
- **Purpose**: Fundamental to the DV algorithm, providing a method to calculate least-cost paths.
- **Formula**: $d_x(y) = \min_{v}(c(x, v) + d_v(y))$
	- $d_x(y)$ represents the cost of the least-cost path from node $x$ to $y$.
	- The equation takes the minimum sum of costs to a neighbor $v$ and from $v$ to $y$.
  
__Practical Application of the Bellman-Ford Equation__
- **Routing Table Updates**:
	- The solution to the Bellman-Ford equation determines the entries in node $x$’s forwarding table.
	- For a packet destined for $y$, node $x$ forwards it to a neighbor $v^*$ that offers the minimal path cost.
  
__Mechanism of the DV Algorithm__
- **Initial Setup**:
	- Each node $x$ starts with $Dx(y)$, an estimate of the path cost from itself to all nodes $y$ in $N$.
- **Distance Vectors**:
	- $Dx = [Dx(y): y \in N]$: Node $x$’s vector of cost estimates to all nodes $y$.
	- $Dv = [Dv(y): y \in N]$ for each neighbor $v$: Neighbors’ cost estimates.
- **Asynchronous Updates**:
	- Nodes periodically send their distance vectors to neighbors.
	- Upon receiving a new distance vector from a neighbor $w$, node $x$ updates its distance vector using the Bellman-Ford equation: $Dx(y) = \min_{v}(c(x, v) + Dv(y))$.
	- If $Dx(y)$ changes, $x$ broadcasts its updated vector to its neighbors, triggering potential updates.

__Convergence__
- **Outcome**: As nodes exchange distance vectors asynchronously, each $Dx(y)$ converges to $dx(y)$, the actual cost of the least-cost path from node $x$ to node $y$, as proven by Bertsekas in 1991.

__Distance-Vector Algorithm Overview__
At each node, x:
```
Initialization:
	for all destinations y in N:  
		Dx(y) = c(x,y)/* if y is not a neighbor then c(x,y)= ∞ */
	
	for each neighbor w  
		Dw(y) = ? for all destinations y in N
	
	for each neighbor w  
		send distance vector Dx = [Dx(y): y in N] to w

loop  
	wait (until I see a link cost change to some neighbor w or
	           until I receive a distance vector from some neighbor w)
	           
	for each y in N:  
	Dx(y) = minv{c(x,v) + Dv(y)}

if Dx(y) changed for any destination y  
	send distance vector Dx = [Dx(y): y in N] to all neighbors

forever
```
- **Function**: Each node x calculates the shortest-path distance to all destinations within a network graph consisting of nodes and edges with associated costs.
- **Initialization**:
	- **For each destination y in N**: Set initial distance Dx(y) = c(x,y). If y is not a neighbor, c(x,y) = ∞.
	- **For each neighbor w**: Initialize distance vector Dw(y) for all destinations y in N as unknown.

__Operation Cycle__
- **Distance Vector Exchange**: Each node x sends its distance vector Dx = [Dx(y): y in N] to each neighbor w.
- **Update Cycle**:
	- Wait for a change in link cost or a new distance vector from any neighbor.
	- Update Dx(y) for each destination y by calculating the minimum cost through all possible paths via neighbors using Dx(y) = min{c(x,v) + Dv(y)}.
	- If Dx(y) changes, send the updated distance vector to all neighbors.

__Algorithm Details__
- **Next-Hop Determination**: Node x identifies the next-hop router v*(y) for each destination y, which is the neighbor that provides the minimum path cost in the updated Dx.
- **Continual Adjustment**: Nodes continuously receive and send updates, adjusting their routing tables based on the latest path costs until no further updates are necessary.

__Practical Implementation and Effects__
- **Real-world Use**: Employed in various routing protocols including RIP and BGP.
- **Behavior in Network Changes**:
	- **Decrease in Link Cost**: Quick propagation through the network, updating routing tables efficiently.
	- **Increase in Link Cost**: Potential slow updates and temporary routing loops, leading to the count-to-infinity problem.

__Advanced Techniques: Poisoned Reverse__
- **Purpose**: Mitigate routing loops by informing neighbors of infinite costs for certain routes.
- **Effectiveness**: Solves two-node loops but not more complex scenarios.

__Comparison with Link-State (LS) Algorithm__
- **Message Complexity**:
	- DV: Exchanges information only with directly connected neighbors, less initial traffic but potential delays in convergence.
	- LS: Requires global network knowledge, more initial messages but typically faster convergence.
- **Robustness**:
	- DV: Susceptible to propagation of incorrect routing information across the network.
	- LS: More contained impact of incorrect data due to localized computation.

## 5.3 Intra-AS Routing in the Internet: OSPF

__Overview of Intra-AS Routing Challenges__
- __INTRA__: inside AS
- **Scale and Administrative Autonomy**:
	- **Scale**: The Internet's vast number of routers leads to prohibitive overhead for storing, computing, and communicating routing information. 
	- **Administrative Autonomy**: ISPs desire to independently manage their network of routers while connecting to other networks.

__Autonomous Systems (AS)__
- **Definition**: A group of routers under the same administrative control within an ISP.
- **AS Number (ASN)**: Globally unique identifiers assigned by ICANN, essential for network management and operation.

__Open Shortest Path First (OSPF)__
- **Protocol Type**: OSPF is a link-state protocol widely used for intra-AS routing, distinguished by its public availability and comprehensive routing functionalities.
- **OSPF Version 2**: Defined in RFC 2328, it includes detailed specifications for link-state broadcasting and path calculation using Dijkstra’s algorithm.

__Key Features of OSPF__
- **Complete Topological Map**: Each router constructs and maintains a map of the AS, enabling precise routing decisions.
- **Link Costs**: Configured by network administrators, potentially based on link capacity to manage traffic flow.
- **Routing Information Broadcast**: Routers broadcast link-state information to all within the AS, ensuring up-to-date network status.

__Advanced OSPF Features__
- **Security**: Supports authentication (simple and MD5) to secure exchanges between routers within an AS.
- **Multiple Same-Cost Paths**: Allows the use of multiple equal-cost paths simultaneously, enhancing routing efficiency and load balancing.
- **Multicast Support**: Integrated support through Multicast OSPF (MOSPF), which extends OSPF capabilities to handle multicast routing effectively.
- **Hierarchical Organization**: OSPF can structure an AS into multiple areas to optimize routing; includes backbone areas for efficient inter-area routing
	- Each area runs its own OSPF link-state routing algorithm, with each router in an area broadcasting its link state to all other routers in that area.
	- Within each area, one or more area border routers are responsible for routing packets outside the area.
	- Exactly one OSPF area in the AS is configured to be the backbone area.
	- Primary role of the backbone area is to route traffic between the other areas in the AS.

__OSPF Operational Mechanisms__
- **Link-State Advertisements**: Periodic and event-driven updates that maintain routing accuracy and system robustness.
- **Area Border Routers**: Manage routing data across different OSPF areas, facilitating effective packet delivery across the network’s hierarchical structure.

## 5.4 Routing Among the ISPs: BGP
![[Pasted image 20240530133028.png|500]]
__Overview of BGP (Border Gateway Protocol)__
- **Protocol Type**: _Inter-autonomous system (inter-AS)_ routing protocol.
	- __INTER__: between AS
- **Importance**: Considered one of the most crucial Internet protocols, essential for interconnecting thousands of ISPs globally.
- **Functionality**: BGP manages how packets are routed across different autonomous systems (ASs) from source to destination across the internet.

### 5.4.1 The Role of BGP
- **Routing Across ASs**: BGP is responsible for determining the routes packets follow from one AS to another, crucial for global internet connectivity.
- **Prefix-based Routing**: Unlike routing within an AS, BGP routes packets to CIDRized prefixes representing subnets or groups of subnets (e.g., 138.16.68/22).
- **Primary Tasks of BGP**:
	1. **Prefix Reachability Information**: Allows subnets to advertise their presence across the internet, ensuring they are not isolated.
	2. **Best Route Determination**: Determines the optimal route to a prefix based on information received from neighboring ASs and local routing policies.

### 5.4.2 Advertising BGP Route Information
- **BGP Message Exchange**:
	- **External BGP (eBGP)**: Manages the exchange of routing information between ASs.
	- **Internal BGP (iBGP)**: Manages the distribution of routing information within an AS.
- **Routing Information Propagation**:
	- **Example**: A subnet with prefix x in AS3 advertises its reachability to AS2 and AS1 sequentially, informing them of a path through AS3 and AS2.
- **Connection Types**:
	- **eBGP Connections**: Between gateway routers in different ASs.
	- **iBGP Connections**: Between all routers within an AS, typically forming a mesh of TCP connections.
  
__BGP Session and Connection Overview__
- **BGP Sessions**: Conducted over semi-permanent TCP connections, crucial for the stability and reliability of internet routing.
- **Path Propagation**:
  - AS3 to AS2 via eBGP, then within AS2 via iBGP, and finally to AS1 via eBGP and iBGP, ensuring all routers know about subnet x and the path to reach it.

### 5.4.3 Determining the Best Routes

__BGP Routing: Determining Optimal Paths__
- **Context**: Routers often encounter multiple possible paths to destination subnets, necessitating a method to choose the optimal route.

__BGP Terminology and Attributes__
- **Route Definition**: In BGP, a route is defined as a prefix along with several BGP attributes.
- **Key Attributes**:
	- **AS-PATH**: Lists Autonomous Systems (AS) a route advertisement has passed through, used for loop prevention.
	- **NEXT-HOP**: IP address of the router interface starting the AS-PATH, crucial for linking inter-AS and intra-AS routing protocols.

__Hot Potato Routing__
- **Principle**: Choose the route that minimizes the cost to the NEXT-HOP router.
- **Method**: Router consults intra-AS routing information to determine the least-cost path to each NEXT-HOP and selects the route with the lowest cost.
- **Example**: Router 1b chooses the route via router 2a (least-cost path) and updates its forwarding table accordingly.
- **Concept**: Hot potato routing aims to expedite packet forwarding out of the AS with minimal concern for the subsequent path costs outside the AS.

__BGP Route-Selection Algorithm__
- **Overview**: More complex than hot potato routing, incorporates several selection criteria.
- **Selection Process**:
	1. **Local Preference**: Routes with higher local preference values are prioritized, reflecting policy decisions within the AS.
	2. **Shortest AS-PATH**: Among equally preferred routes, the route with the fewest AS hops is selected.
	3. **Hot Potato**: If routes still tie, the one with the closest NEXT-HOP is chosen.
	4. **BGP Identifiers**: Used as a last resort to break ties among routes.
- **Algorithm Behavior**: Transitions from purely self-interested routing (hot potato) to considering route efficiency and policy via AS-PATH length and local preferences.
- **Impact and Statistics**: BGP is the standard for inter-AS routing with vast routing tables in major ISPs, illustrating the global scale and complexity of Internet routing dynamics.

### 5.4.4 IP-Anycast
- **Context**: Utilized within DNS systems, IP-anycast allows users to access the nearest server hosting replicated content.
- **Implementation via BGP**:
	- **Setup**: CDNs assign the same IP address to multiple servers globally and advertise this via BGP.
	- **Operation**: BGP routers select the closest server based on the shortest AS-hop count, guiding user requests to the nearest server.
- **Use in DNS**: Extensively used to direct queries to the closest DNS root server among potentially hundreds worldwide.
- **Limitations**: Not typically used by CDNs for content delivery due to potential issues with TCP connections receiving packets from different server instances.

### 5.4.5 Routing Policy
- **Influence of AS Routing Policy**: Can override other routing considerations like shortest AS path or "hot potato" routing.
- **Example Scenario**:
	- **Network Setup**: Interconnected ASs, some acting as backbone providers and others as access ISPs.
	- **Routing Control**: Access ISPs like X advertise routes only for traffic originating or terminating within their network to prevent transit traffic, following a selective route advertisement policy.
- **Commercial Relationships and Routing**:
	- **Backbone Networks**: Prefer not to carry transit traffic for other networks to avoid additional costs.
	- **Peering Agreements**: Govern how ISPs manage routing among themselves, typically ensuring traffic either originates from or is destined to the ISP’s customers.

### 5.4.6 Obtaining Internet Presence
- **Steps for a New Company**:
	- **Internet Connectivity**: Contract with a local ISP, obtain a range of IP addresses.
	- **Domain Name and DNS Registration**: Register a domain and set up DNS entries for accessible servers.
	- **BGP Advertising**: The local ISP advertises the company’s IP prefix using BGP, enabling global routing to the company’s servers.

## 5.5 The SDN Control Plane

![[Pasted image 20240530133118.png|400]]
__Overview of the SDN Control Plane__
- **Purpose**: Control packet forwarding among SDN-enabled devices and manage device configuration and services.
- **Key Components**: Divided into the data plane (network switches) and the control plane (servers and software).

__Characteristics of SDN Architecture__
- **Flow-based Forwarding**: In SDN, packet switches forward packets based on multiple header field values across different layers, unlike traditional IP forwarding based only on destination addresses.
- **Separation of Data and Control Planes**: The data plane involves simple devices executing forwarding rules, while the control plane involves complex software managing these rules.
- **External Network Control Functions**: Implemented via software on servers separate from network switches, enhancing flexibility and control.
- **Programmable Network**: The network can be programmed through applications that interact with the SDN controller to manage and direct data plane behavior.

__SDN Control Plane Components__
- **SDN Controller**: Central or logically centralized server that maintains network state, informs control applications, and programs network devices.
- **Network-Control Applications**: Utilize APIs provided by the controller to implement network functionalities such as routing, access control, and load balancing.

### 5.5.1 The SDN Control Plane: SDN Controller and SDN Network-control Applications

__Controller's functionality in 3 layers__
![[Pasted image 20240530133257.png|300]]
- **Communication Layer**: Facilitates information transfer between the controller and network devices, including event notifications (known as the southbound interface).
- **Network-Wide State-Management Layer**: Maintains comprehensive state information necessary for configuring network-wide flow tables and other control functions.
- **Interface to Network-Control Applications**: Provides an API (northbound interface) for applications to interact with the network state and control decisions.

__SDN Protocols and Operations__
- **OpenFlow**: A protocol enabling communication between the SDN controller and network devices, foundational for most SDN operations.
- **Controller Operations**: Logically centralized but often physically distributed for resilience and performance, ensuring consistent and coordinated network functionality across different devices.

__Evolution of SDN__
- **Unbundling of Network Functions**: SDN separates network hardware and control logic, similar to the shift from mainframe to personal computers, fostering innovation in hardware, systems software, and applications.
- **Challenges and Questions**: Includes how flow tables are computed, updated, and synchronized across the network to ensure consistent and efficient operations.

### 5.5.2 OpenFlow Protocol

**Purpose**: Facilitates communication between an SDN controller and SDN-controlled devices using the OpenFlow API.
**Operation**: Utilizes TCP over default port 6653.
**Key Messages from Controller to Switch**:
- **Configuration**: Queries and sets switch configuration parameters.
- **Modify-State**: Adds, deletes, or modifies entries in the switch's flow table and port properties.
- **Read-State**: Gathers statistics and counter values from the switch's flow table and ports.
- **Send-Packet**: Sends specific packets out of designated ports on the switch.

**Key Messages from Switch to Controller**:
- **Flow-Removed**: Notifies the controller of flow table entry removals.
- **Port-Status**: Informs about changes in port status.
- **Packet-In**: Sends packets to the controller that do not match any flow table entries for further processing.

### 5.5.3 Data and Control Plane Interaction: An Example
![[Pasted image 20240530133347.png|300]]
**Scenario**: Utilizes Dijkstra’s algorithm for shortest path routing in an SDN environment.
**Process**:
1. **Link Failure Notification**: Switch s1 reports a failed link to s2 via OpenFlow port-status message to the SDN controller.
2. **Link-State Update**: SDN controller updates the link-state database upon receiving the notification.
3. **Routing Application Notification**: A network-control application registered for link-state updates receives notification and accesses updated link-state data.
4. **Path Recalculation**: Uses updated link-state to compute new least-cost paths.
5. **Flow Table Management**: The flow table manager determines necessary updates to flow tables based on new paths.
6. **Flow Table Updates**: OpenFlow protocol is used to update flow table entries at affected switches to reroute traffic accordingly.

### 5.5.4 SDN: Past and Future

**Origins and Evolution**:
- Early advocacy for separating data and control planes as seen in various projects and proposals from the early 2000s.
- The Ethane project evolved into the OpenFlow project, illustrating early practical implementations of flow-based control.
**Future Directions**:
- Ongoing research into SDN architectures and the extension of SDN principles to broader networking contexts including network functions virtualization (NFV) and inter-AS settings.
- Emphasis on replacing traditional networking components with simplified hardware managed by sophisticated software controls.

### SDN Controller Case Studies: The OpenDaylight and ONOS Controllers
___EXAM! 이 부분 퀴즈 시험예정(원래는 false 하지만 문제가 이상해서 paraphrase한 뒤 출제예정)___
**Context and Evolution**:
- Early SDN landscape featured limited protocols and controllers (e.g., OpenFlow, NOX).
- Growth in SDN controllers, moving from proprietary to more open-source models in collaboration with the Linux Foundation.

__OpenDaylight (ODL) Controller__
![[Pasted image 20240530133435.png|400]]
- **Basic Components and Structure**:
	- **Basic Network Functions**: Core of the controller, managing network-wide state.
	- **Service Abstraction Layer (SAL)**: Acts as the central hub for communication between controller components and external applications, providing a uniform interface to various protocols.
- **Protocols and Interfaces**:
	- Includes OpenFlow, SNMP, NETCONF, and OVSDB.
	- OVSDB is particularly used for data center switching management.
- **Operational Modes**:
	- **API-Driven (AD-SAL)**: Initial method using REST APIs for application-controller communication.
	- **Model-Driven (MD-SAL)**: Later approach using the YANG data modeling language for device and network management through NETCONF protocol.

__ONOS Controller__
![[Pasted image 20240530133506.png|400]]
- **Architectural Overview**:
	- Presented as a three-layer model:
	    1. **Northbound Abstractions and Protocols**: Includes an intent framework allowing applications to request high-level services without knowing underlying details.
	    2. **Distributed Core**: Maintains state of network elements like links and hosts; scales horizontally across servers.
	    3. **Southbound Abstractions and Protocols**: Provides device and protocol agnosticism, enabling a uniform interface across diverse network devices.
- **Unique Features**:
	- **Intent Framework**: Simplifies application requests for network services.
	- **Scalability and Redundancy**: Enhanced by a distributed deployment across multiple servers.
- **Comparison with ODL**:
	- ONOS offers a more scalable, distributed architecture.
	- Emphasizes high-level service requests through its intent framework, contrasting with ODL’s more direct device management approach.
- **Trends in SDN Controller Development**:
	- Shift from proprietary to open-source solutions.
	- Increased collaboration with larger foundations like the Linux Foundation.

**Challenges and Considerations**:
- Balancing between open-source flexibility and the need for secure, reliable network management.
- Integrating with existing and legacy network infrastructures.

**Future Directions**:
- Potential developments in controller technologies and the standardization of protocols.
- Enhancements in interoperability and ease of deployment for complex network environments.

## 5.6 ICMP: The Internet Control Message Protocol

__Overview__
**Internet Control Message Protocol (ICMP)**, defined in [RFC 792], is used to communicate network-layer information between hosts and routers, mainly for error reporting.

__Context__
- ICMP is part of, but architecturally above, IP, encapsulated within IP datagrams.
- Key use: Communicating errors like "Destination network unreachable."
- Unlike TCP/UDP, ICMP does not support user data transmission but manages error messages and operational information.

__Operation and Structure__
![[Pasted image 20240430135417.png|500]]
- **Demultiplexing**: ICMP messages are distinguished from other IP payloads (like TCP or UDP) by an upper-layer protocol number of 1.
- **Structure**: Each message contains a type and code field, along with the header and the first 8 bytes of the triggering IP datagram, allowing error diagnosis.
- ___TEST!___: destination network unreachable, what if we cannot reach using BGP routing?
- Nowadays ICMP is turned off in routers because of security issues(Hackers may do DDoS)

__Key ICMP Messages__
- **Echo Request and Reply**: Utilized by the ping program (type 8 code 0 for request, type 0 code 0 for reply).
- **Source Quench**: Intended for congestion control by instructing a host to reduce its transmission rate (seldom used).
- **Packet Too Big (IPv6)**: Indicates that a packet cannot be forwarded because it's too large to pass through a router without being fragmented (specific to ICMPv6).

__Utilities Utilizing ICMP__
- **Traceroute**:
	- Uses ICMP messages to trace the route from a host to any destination across routers.
	- Employs TTL (Time To Live) adjustments in IP headers to invoke time exceeded messages from each router (type 11 code 0).
	- Receives final destination unreachable messages (type 3 code 3) indicating the end of the trace.

__ICMP for IPv6 (RFC 4443)__
- **Enhancements in ICMPv6**:
	- Reorganized type and code definitions.
	- Added functionalities specific to IPv6 needs, like handling unrecognized IPv6 options.

__Practical Insights__
- **Implementation**: Most systems integrate ICMP functionality directly within the operating system kernel, not as a separate process.
- **Customization**: Developers can utilize ICMP's functionalities by coding at system level, as seen in the source code for the ping client in [Stevens 1990].



# 6. The Link Layer and LANs

## 6.1 Introduction to the Link Layer

__Introduction to Link Layer Concepts__
- **Nodes**: Devices that operate at the link layer, including hosts, routers, switches, and WiFi access points.
- **Links**: Communication channels connecting adjacent nodes; crucial for datagram transmission across the network path.

__Datagram Transmission Example__
- **Transmission Path**: A datagram may traverse multiple links such as WiFi, Ethernet, and router connections to reach its destination.
	- Example: Datagram from a wireless host to a server passes through six different links, including WiFi and multiple Ethernet connections.

__Link Layer and Network Layer Interaction__
- **Transportation Analogy**:
	- **Tourist**: Represents a datagram.
	- **Transportation Segments**: Different links each handled by different entities (e.g., limousine, airplane, train).
	- **Travel Agent**: Acts as a routing protocol arranging the segments.

### 6.1.1 Services Provided by the Link Layer
- **Framing**: Encapsulation of network-layer datagrams within a link-layer frame for transmission.
- **Link Access**: Medium Access Control (MAC) protocols dictate how frames are transmitted over a link. This is particularly complex in environments where multiple nodes share a single link.
- **Reliable Delivery**: Ensures error-free transmission across the link, particularly useful for error-prone links like wireless connections. Not typically used for low-error links like fiber or coaxial.
- **Error Detection and Correction**: Mechanisms to identify and correct bit errors in the frame, implemented in hardware for efficiency.

### 6.1.2 Implementation of the Link Layer
- **Implementation**: Primarily in hardware via a network adapter or network interface controller (NIC), which handles tasks such as framing and error detection.
- **Software Role**: Handles higher-level functionalities such as assembling addressing information and managing hardware activations.
- **Host Architecture**: Shows integration of Ethernet capabilities either directly on the motherboard or via a dedicated chip.
- **Operational Flow**:
	- **Sending Side**: Datagram is encapsulated in a link-layer frame and transmitted following the link-access protocol.
	- **Receiving Side**: Frame is received, errors are checked, and the datagram is extracted and passed up to the network layer.
.
## 6.2 Error-Detection and -Correction Techniques

__Overview of Error-Detection and Correction__
- **Purpose**: Detect and correct bit errors in data transmitted between nodes, commonly implemented in both link and transport layers.
- **Goal**: Develop an understanding of simple techniques used for error detection and correction in the link layer.

__Techniques for Error Detection and Correction__
- **Parity Checks**:
	- **Single-bit Parity**: Adds one bit to data to make the number of 1s even (even parity) or odd (odd parity). Simple but can miss errors if an even number of bits are flipped.
	  ![[Pasted image 20240530133916.png|200]]
	- **Two-dimensional Parity**: Organizes data into a matrix of rows and columns, computing parity for each, enhancing error detection and enabling correction of single-bit errors.
	  ![[Pasted image 20240530134003.png|300]]
- **Checksumming Methods**:
	- Data treated as sequence of k-bit integers; sum used for error detection.
	- **Internet checksum**: Based on 1s complement of sums; utilized in TCP, UDP, and IP for error detection.
- **Cyclic Redundancy Check (CRC)**:
  ![[Pasted image 20240530134036.png|400]]
	- Polynomial code-based technique where data is viewed as a polynomial.
	- Involves appending r bits to data so the combined data is divisible by a predefined polynomial (generator G) using modulo-2 arithmetic, enabling robust error detection.

__Practical Application and Importance__
- **Error Detection**: Critical for ensuring data integrity across transmissions; methods vary in complexity from simple parity checks to robust CRC.
- **Error Correction**: Two-dimensional parity allows for correction of single-bit errors, crucial for real-time applications or in environments with long propagation delays.
- **Forward Error Correction (FEC)**: Techniques that allow errors to be corrected at the receiver without needing retransmission, beneficial for real-time network applications and long-distance communications.

## 6.3 Multiple Access Links and Protocols

**Types of Network Links**:
- **Point-to-point Links**: Involves a single sender and a single receiver. Examples include PPP (Point-to-Point Protocol) and HDLC (High-level Data Link Control).
- **Broadcast Links**: Supports multiple senders and receivers using a shared channel, typical in local area networks (LANs).

__XCast__
- Unicast: point-to-point (usual connection)
- Multicast: multiple receivers (Use IP of 224.~(A), every packet sent to A will be sent to every device connected A)
- Broadcast: receiver is not limited. Everyone inside the subnet must receive it.
- Anycast: way of serving DNS servers

**Key Concept**:
- The main challenge in broadcast links is the **multiple access problem**, where multiple nodes must coordinate to share the same broadcast channel without interference.

**Analogy**:
- Compared to a cocktail party or a classroom where participants must follow social protocols to communicate effectively without talking over each other.

__The Multiple Access Problem__
- **Definition**:
	- Multiple nodes can transmit simultaneously on the same channel, which can lead to collisions, rendering the communication unintelligible.
- **Importance**:
	- Effective management of this access is crucial in networks, especially LANs, to maximize efficient use of bandwidth and minimize collisions.
- **Historical Context**:
	- Decades of research and development have led to the creation of numerous protocols to manage this problem, evidenced by numerous scholarly articles and PhD dissertations.
- **Types of Multiple Access Protocols**:
	- Broadly categorized into:
		1. **Channel Partitioning Protocols**
		2. **Random Access Protocols**
		3. **Taking Turns Protocols**
- **Desirable Characteristics of Protocols**:
	- 1. Full channel throughput when only one node is transmitting.
	- 2. Fair bandwidth distribution among multiple nodes.
	- 3. Decentralized control to avoid single points of failure.
	- 4. Simplicity and cost-effectiveness in implementation.

### 6.3.1 Channel Partitioning Protocols

**Concepts**:
- **Time-Division Multiplexing (TDM)**: Divides time into frames and slots, assigning slots to nodes.
- **Frequency-Division Multiplexing (FDM)**: Divides the channel into frequency bands assigned to nodes.
- **Code Division Multiple Access (CDMA)**: Assigns unique codes to each node allowing simultaneous transmissions.

**Illustration**:
![[Pasted image 20240530134507.png|300]]
- **TDM Example**: If N nodes are connected, each node gets one slot per frame to transmit, ensuring all have a chance without collision.
- **FDM and CDMA**: Similar in sharing but use frequencies and codes, respectively, for data transmission.

**Drawbacks**:
- **TDM and FDM**: Limit bandwidth per node, even if fewer nodes wish to transmit.
- **CDMA**: Technically complex but allows effective simultaneous transmissions.

**Usage**:
- TDM and FDM are used broadly in wired networks, while CDMA is prevalent in military and civilian wireless communications, such as cellular networks.2

### 6.3.2 Random Access Protocols

**Definition**: Random access protocols allow nodes to transmit at the full rate of the channel, R bps, and employ a collision resolution mechanism where each node involved in a collision retransmits its frame after a random delay.

__Slotted ALOHA__
![[Pasted image 20240530134528.png|400]]
- **Frame Size**: Frames are of size L bits.
- **Time Slots**: Transmission time is divided into slots of size L/R seconds.
- **Transmission Rules**:
	- Nodes transmit at the beginning of slots.
	- Nodes must be synchronized.
	- Collisions are detected before the slot ends.
- **Re-transmission Probability**: If a collision occurs, the node retransmits its frame in each subsequent slot with a probability p.
- **Efficiency**: When there are multiple active nodes, efficiency concerns arise due to collisions and empty slots. The maximum theoretical efficiency is 0.37 or 37% effective transmission rate.
	- prob given node has success in slot: $p(1-p)^{N-1}$
	- prob any node has success in slot: $Np(1-p)^{N-1}$
	- find p that maximizes $Np(1-p)^{N-1}$
	- $(1-p)^{N-1}-(N-1)p(1-p)^{N-2}=(1-p-(N-1)p)(1-p)^{N-2}=0$
	  $p=\frac{1}{N}$

__Pure ALOHA__
![[Pasted image 20240530134545.png|400]]
- **Decentralization**: Fully decentralized; nodes transmit immediately upon receiving a frame.
- **Collision Handling**: After a collision, a node retransmits the frame with a probability p after waiting for one frame transmission time.
- **Maximum Efficiency**: Half of slotted ALOHA, at 1/(2e) due to increased collision possibilities.

__Basic CSMA__
- **Carrier Sensing**: Nodes listen before transmitting. If the channel is busy, they wait until it becomes idle.
- **Collision Detection**: Nodes stop transmitting when they detect another transmission interfering.

__CSMA with Collision Detection (CSMA/CD)__
![[Pasted image 20240530134814.png|300]]
- **Operation**: Nodes perform carrier sensing and abort transmission immediately upon detecting a collision.
- **Binary Exponential Backoff**: Post-collision, nodes wait a random backoff time determined by the number of collisions encountered.
- **Efficiency Variables**:
	- **Propagation Delay (dprop)**: Time for a signal to reach from one node to another.
	- **Transmission Time (dtrans)**: Time to transmit the maximum-size frame.
- **Efficiency Formula**: Efficiency approximated as 1/(1 + 5(dprop/dtrans)), suggesting higher efficiency with lower propagation delay or longer transmission times.

__Real-world Applications__
- **Ethernet**: A popular CSMA/CD protocol used widely in local area networks.
- **Wireless Networks**: Adaptations of CSMA for managing airwave transmissions.

__Comparative Analysis__
- **Slotted vs. Pure ALOHA**:
	- Slotted ALOHA is more efficient due to synchronization and timed transmissions.
	- Pure ALOHA has higher flexibility but lower efficiency due to the continuous possibility of collisions.
- **CSMA/CD vs. ALOHA**:
	- CSMA/CD is generally more efficient than ALOHA due to the use of collision detection and carrier sensing, reducing the number of collisions and thus improving throughput.

### 6.3.3 Taking-Turns Protocols

**Desirable Properties of Multiple Access Protocols**:
- **Throughput for Single Active Node**: When only one node is active, it should achieve a throughput of R bps.
- **Throughput for Multiple Active Nodes**: When M nodes are active, each should have a throughput of nearly R/M bps.

ALOHA and CSMA protocols ensure high throughput for single active nodes but do not effectively manage multiple active nodes. This limitation has spurred the development of taking-turns protocols, which aim to balance throughput across multiple nodes.

__Polling Protocol__
- **Overview**:
	- **Master Node**: Designated to control the protocol, polls other nodes in a round-robin manner.
	- **Operation**: The master node invites each node sequentially to transmit a maximum number of frames. It monitors channel silence to determine the end of transmission before moving to the next node.
- **Advantages**:
	- Eliminates collisions and empty slots, common in random access protocols, thereby increasing efficiency.
- **Drawbacks**:
	- **Polling Delay**: Time taken to notify a node can decrease throughput, especially if fewer nodes are active.
	- **Single Point of Failure**: If the master node fails, the entire channel becomes inoperative.
- **Real-World Application**: The Bluetooth protocol is an example of a polling-based system.

__Token-Passing Protocol__
- **Overview**:
	- **Decentralized Operation**: No master node. A token circulates among nodes dictating the transmission rights.
	- **Token Mechanics**: Nodes transmit frames only when they possess the token. If no data needs to be sent, the token is immediately passed to the next node.
- **Efficiency**: Highly efficient due to decentralized management of transmission rights.
- **Challenges**:
	- **Node Failure**: Can disrupt the entire network if a node fails to pass the token.
	- **Token Management**: Lost or unpassed tokens require a recovery mechanism to maintain network functionality.
- **Notable Implementations**:
	- Fiber Distributed Data Interface (FDDI)
	- IEEE 802.5 Token Ring

### 6.3.4 DOCSIS: The Link-Layer Protocol for Cable Internet Access

![[Pasted image 20240530134856.png|500]]
**Cable Access Networks**:
- Connects thousands of residential modems to a Cable Modem Termination System (CMTS) using the DOCSIS standard.
- **Downstream and Upstream Channels**:
	- **Downstream**: High bandwidth (up to 1.6 Gbps), broadcast from CMTS to modems.
	- **Upstream**: Shared channel with potential for collisions, managed via time-division multiplexing (TDM).

__DOCSIS Specifications__
- **Frequency Division**:
	- **Downstream**: 24 MHz to 192 MHz channels.
	- **Upstream**: 6.4 MHz to 96 MHz channels, with a maximum throughput of 1 Gbps.
- **Transmission Management**:
	- **Mini-Slots**: Time intervals allocated by the CMTS for specific modems to avoid collisions.
	- **Control Messages (MAP)**: Direct which modem transmits in which mini-slot.

__Dynamic Slot Allocation__
- **Mini-Slot Requests**:
	- Modems request transmission slots in a random access method during designated intervals.
	- **Collision Handling**: Binary exponential backoff is used to manage collisions and retransmission attempts.

__Integration of Multiple Access Protocols__
- **Combination of Access Methods**:
	- **Frequency Division Multiplexing (FDM)**: Separates downstream and upstream channels by frequency.
	- **Time Division Multiplexing (TDM)**: Organizes transmission into timed mini-slots.
	- **Random Access**: Used for mini-slot requests, where collisions can occur.

## 6.4 Switched Local Area Networks

![[Pasted image 20240530134931.png|500]]
### 6.4.1 Link-Layer Addressing and ARP
![[Pasted image 20240530134957.png|250]]

__MAC Addresses__
- **Adapters have MAC addresses**: Hosts and routers use multiple network and MAC addresses; link-layer switches, however, do not have MAC addresses for interfaces connected to hosts and routers.
- **Permanent but changeable**: Traditionally fixed, MAC addresses can now be altered via software.
- **Uniqueness**: Managed by IEEE, ensuring no two adapters have the same MAC address globally.
- **Structure and notation**: Flat addressing structure; 6-byte long, expressed in hexadecimal format (e.g., AB-CD-EF-01-23-45).

__Address Resolution Protocol (ARP)__
![[Pasted image 20240530135022.png|400]]
- **Function**: Converts network-layer IP addresses to link-layer MAC addresses.
- **Scope**: Operates only within the same subnet; would error out if used for nodes on different subnets.
- **Mechanism**: 
	- Sends an ARP query in a broadcast frame to all on the subnet.
	- Receives the MAC address in a direct frame from the target device.
- **Automation**: ARP tables are built automatically, entries removed when devices disconnect.
- **Layer ambiguity**: ARP operates between the link and network layers, containing both MAC and IP addresses.

__Sending a Datagram off the Subnet__
- ![[Pasted image 20240509133712.png|500]]
	- MAC address changes every subnet
- **Process**:
	- **Internal Operation**: Host determines the MAC address of the router interface (first-hop router) using ARP for off-subnet communication.
	- **Routing**: The router uses its forwarding table to forward the datagram to the appropriate subnet.
- **Example**: A host on Subnet 1 sends a datagram to Subnet 2 by first sending it to its subnet's router interface, which forwards it further.
- **ARP's Role**: Essential in acquiring MAC addresses for routing datagrams to and through routers.

__ARP in Ethernet__
- **Specification**: Defined in RFC 826.
- **Tutorial**: Additional details in RFC 1180, which provides a foundational tutorial on ARP.

### 6.4.2 Ethernet

**Historical Dominance**:
- **Early Adoption**: Ethernet, first deployed in the mid-1970s, was the first widely adopted high-speed LAN technology.
- **Competitive Edge**: It maintained dominance over other LAN technologies like token ring and FDDI by being simpler and cheaper.
- **Adaptation and Growth**: Continuously evolved to match or exceed the data rates of competing technologies.

__Ethernet Evolution__
- **Initial Design and Topology**:
	- **Inventors**: Bob Metcalfe and David Boggs.
	- **Original Setup**: Utilized a coaxial bus topology.
	- **Broadcast Mechanism**: Frames are sent to all adapters on the bus, which could lead to collisions.
- **Technological Shifts**:
	- **1990s Shift**: Transition from bus topology to hub-based star topology using twisted-pair copper wire.
	- **2000s Development**: Replacement of hubs with switches, enhancing efficiency by eliminating collisions and enabling full-duplex communication.

__Ethernet Frame Structure:__ **Components of an Ethernet Frame**
- ![[Pasted image 20240509134111.png|400]]
- **Data Field**: Ranges from 46 to 1,500 bytes, carrying network-layer data like IP datagrams.
- **Addresses**: Includes 6-byte destination and source MAC addresses.
- **Type Field**: Identifies the network layer protocol being used.
- **Error Checking**: Uses a Cyclic Redundancy Check (CRC) to detect bit errors.
- **Preamble**: An 8-byte field used to synchronize the receiver's timing with the sender's.

__Ethernet Functionality__: **Service Characteristics**:
- **Connectionless and Unreliable**: Does not require handshaking between sending and receiving nodes; does not perform retransmissions at the Ethernet layer.
- **Layer Compatibility**: Operates up through layer 2, using simple link-layer mechanisms to support network-layer protocols.

__Ethernet Technologies__
- **Speed and Media Types**:
	- **Standard Evolution**: From 10 Mbps (10BASE-T) to 40 Gbps (40GBASE-T).
	- **Media Diversity**: Operates over coaxial cable, twisted-pair copper wire, and fiber optics.
	- **IEEE Standards**: Guided by IEEE 802.3 CSMA/CD protocols, accommodating a wide range of Ethernet configurations.
- **Modern Ethernet Usage**:
	- **Switch-Based Topologies**: Dominant use of switches in modern networks, which facilitate full-duplex and collision-less operations.
	- **Frame Consistency**: Despite significant changes in technology and topology, Ethernet’s frame format has remained consistent, illustrating its enduring legacy in network design.

### 6.4.3 Link-Layer Switches

__Role and Functionality of Link-Layer Switches__
**Function**: Switches at the link layer are responsible for receiving link-layer frames and forwarding them to the appropriate outgoing links. They operate transparently to hosts and routers, which continue to address frames directly to each other, oblivious to the switch's role in frame handling.

**Buffer Management**: To manage instances where incoming frame rates exceed an interface's capacity, switches are equipped with buffers similar to those in router interfaces, which temporarily store frames until they can be processed.

__Detailed Switch Operations: Forwarding and Filtering__
- **Switch Table Utilization**: 
	- Switch itself does not have a MAC address & IP address(Router does)
	- Switches use a dedicated table to manage frame forwarding and filtering.
	- **Table Contents**: Each entry includes a MAC address, the corresponding switch interface, and the timestamp marking the entry’s creation.
- **Operational Details**:
	- **Filtering**: Determines if incoming frames should be dropped or forwarded. If a frame's destination MAC address matches an interface from which the frame originated, the switch filters out the frame.
	- **Forwarding**: If the table points to a different interface than the incoming one for a given MAC address, the frame is forwarded to that interface. Frames with no specific table entry are broadcast to all interfaces except the source.

__Self-Learning Capabilities of Switches__
![[Pasted image 20240530135206.png|400]]
- **Automatic Table Configuration**: Switches autonomously populate their switch table based on incoming frames, which prevents the need for manual configuration:
	1. **Initial State**: The switch table starts empty.
	2. **Learning Process**: Each incoming frame leads to a new entry or updates an existing entry in the switch table with the frame's source MAC address, the receiving interface, and the time of reception.
		1. If there is a match with the output send it using the table
		2. If there is no match, flood(send it to all connected hosts)
	3. **Aging and Cleanup**: Entries in the switch table that do not see corresponding incoming frames within a specified aging time are automatically purged.
- **Example of Self-Learning**:
	- Suppose a frame from MAC address 01-12-23-34-45-56 arrives on interface 2 at 9:39. If this address is not already in the switch table, the switch adds it with the current timestamp.

__Benefits and Features of Link-Layer Switches
![[Pasted image 20240530135328.png|400]]__
- **Advantages**:
	- **Collision Avoidance**: By managing frame transmissions and buffering, switches eliminate collisions and maximize available bandwidth.
	- **Support for Diverse Link Types**: Switches can handle different speeds and types of media, enabling a mix of legacy and modern equipment within the same network.
	- **Enhanced Network Management**: Switches can autonomously manage issues such as faulty adapters and cable problems without manual intervention, significantly reducing network downtime and maintenance.

__Comparative Analysis: Switches vs. Routers__
![[Pasted image 20240530135359.png|500]]
- **Functional Differences**:
	- **Layer Operation**: Switches operate at Layer 2 using MAC addresses for decisions, whereas routers operate at Layer 3 and use IP addresses.
	- **Data Handling**: Switches perform store-and-forward packet switching up to Layer 2, whereas routers process up through Layer 3, adding more overhead.
- **Network Design Considerations**:
	- For smaller, simpler networks, switches are preferred due to their plug-and-play nature and local traffic management capabilities.
	- In larger or more complex networks, routers are employed alongside switches to provide enhanced traffic isolation, intelligent routing, and security against network-wide disruptions like broadcast storms.
- **Strategic Deployment**:
	- Smaller networks benefit from the high throughput and simplicity of switches.
	- Larger networks often require the robust traffic segmentation and advanced routing capabilities provided by routers, despite the need for more complex configuration and management. 

### 6.4.4 Virtual Local Area Networks (VLANs)

![[Pasted image 20240530135420.png|400]]
__Context and Network Challenges__
- **Hierarchical LAN Configuration**: Institutional LANs structured with departmental switched LANs linked via a switch hierarchy.
- **Identified Drawbacks**:
	1. **Lack of Traffic Isolation**: Broadcast traffic traverses entire network, impacting performance and potentially compromising security.
	2. **Inefficient Switch Use**: Requires multiple switches even for small groups, leading to underutilized resources.
	3. **Complex User Management**: Moving employees between groups necessitates physical cabling changes.

__VLAN Introduction and Benefits__
- **Definition**: Virtual networks configured over a single physical LAN infrastructure, isolating group communications.
- **Port-Based VLANs**: Switch ports are grouped, each group forming a separate broadcast domain.
	- **Example**: Ports 2-8 for EE VLAN; Ports 9-15 for CS VLAN (Figure 6.25).
	- **Advantages**:
		- Solves isolation issues by confining broadcast traffic within VLAN groups.
		- Reduces the need for multiple physical switches.
		- Simplifies management; reconfiguring a port's VLAN assignment is software-driven.

__VLAN Isolation and Inter-VLAN Communication__
- **Complete Isolation Issue**: VLANs initially prevent any inter-department communication.
- **Interconnection via Router**: A switch port (e.g., port 1 in Figure 6.25) can connect to a router to facilitate communication between VLANs.
- **Integrated Switch-Routers**: Modern solutions often include combined VLAN switch and router hardware for streamlined management.

__VLAN Extension and Management__
![[Pasted image 20240530135559.png|500]]
- **Extended VLANs**: Connecting remote users to their respective department VLANs.
- **Scalable Interconnection - VLAN Trunking**:
	- **Concept**: Use trunk ports to interconnect VLAN switches, carrying frames for all VLANs across a single port.
	- **IEEE 802.1Q Standard**: Frames tagged with VLAN identifiers to maintain separation across trunk links.
	    - **VLAN Tag Components**:
			- **TPID**: Tag Protocol Identifier, fixed hexadecimal (81-00).
			- **TCI**: Tag Control Information, includes a 12-bit VLAN ID and a 3-bit priority field.
- **Diverse VLAN Definitions**:
	- **MAC-Based VLANs**: Assign VLANs based on device MAC addresses.
	- **Protocol-Based VLANs**: Define VLANs through network layer protocols like IPv4 or IPv6.
	- **Global VLANs**: Potential for VLANs to span globally, connecting disparate LANs into a single VLAN network.

__Standards and Future Directions__
- **802.1Q Standard**: Provides detailed protocols for VLAN tagging and management.
- **Evolutionary Potential**: Continuous improvement in VLAN technology, aiming to simplify network management and enhance security and performance across institutional LANs.

## 6.5 Link Virtualization: A Network as a Link Layer

**Evolution of Link Definition**:
- Initially viewed as a physical wire connecting hosts.
- Expanded to include multiple hosts connected by shared media (e.g., radio spectra).
- Considered abstractly as a channel, not just a wire.
- Ethernet LANs: complex switched infrastructures seen as simple link-layer channels by hosts.
- Dialup modem connections: telephone network viewed as a simple "wire" by the Internet link-layer.
**Overlay Networks**:
- Internet virtualizes the telephone network, using it as a link-layer technology.
- Similar to how overlay networks use the Internet for connectivity.

## 6.5.1 Multiprotocol Label Switching (MPLS)

**Overview**:
- **Origins**: Evolved in the 1990s to improve IP router forwarding speeds using fixed-length labels.
- **Purpose**: Augment IP datagram-forwarding with fixed-length labels for faster processing.
- **Protocol**: Unified by IETF in MPLS protocol [RFC 3031, RFC 3032].

**MPLS Frame Structure**:
- **Format**: MPLS header added between layer-2 (e.g., Ethernet) and layer-3 (IP) headers.
- **Fields**:
  - Label
  - 3 experimental bits
  - S bit (end of MPLS header stack)
  - Time-to-live field

**Label-Switched Routers**:
- **Function**: Forward MPLS frames based on label lookups.
- **Requirement**: Both routers in the connection must be MPLS-capable.
- **Example**:
  - MPLS-capable routers (R1-R4) connect IP devices (R5, R6, A, D) without altering IP headers.

**Label Distribution and Path Computation**:
- **Label Distribution**: Managed by protocols like RSVP-TE [RFC 3209].
- **Path Computation**: Uses extended link-state routing algorithms (e.g., OSPF).
- **Vendor-Specific Algorithms**: Path computation methods are not standardized.

**Advantages of MPLS**:
- **Traffic Management**: Enables multiple paths to a destination, enhancing traffic engineering.
  - Example: Router R4 can use different MPLS paths to reach destination A.
- **Fast Restoration**: Precomputed failover paths for quick rerouting during link failures.
- **Virtual Private Networks (VPNs)**: MPLS isolates customer resources and addresses within an ISP’s network.

**Future of MPLS and SDN**:
- **Coexistence with SDN**: MPLS predated SDN but shares similar traffic engineering capabilities.
- **Potential for Replacement**: SDN may eventually replace MPLS, but both technologies currently coexist.

## 6.6 Data Center Networking

**Purpose and Functionality**:
- Serve as infrastructures for providing content, processing data tasks, and cloud computing.
- Major providers include Google, Microsoft, Amazon, and Alibaba.

**Services Provided**:
1. Content delivery (Web pages, search results, email, streaming video).
2. Massively-parallel computing for data processing (e.g., search engine index computations).
3. Cloud computing for external companies (e.g., AWS, Azure, Alibaba Cloud).

### 6.6.1 Data Center Architectures
![[Pasted image 20240530135714.png|400]]
**Design and Costs**:
- Designs are proprietary and costly (e.g., $12 million/month for a 100,000 host data center in 2009).
- Cost breakdown:
  - 45% for hosts (replaced every 3-4 years)
  - 25% for infrastructure (power supplies, generators, cooling)
  - 15% for electricity
  - 15% for networking (gear, external links, transit costs)

**Hosts and Networking**:
- Hosts (blades) are stacked in racks, each with 20-40 blades.
- Top of Rack (TOR) switches connect hosts within racks and to other switches.
- Ethernet connections (40 Gbps or 100 Gbps) between hosts and TOR switches.
- Hosts have data-center-internal IP addresses.

**Traffic Types**:
- External: Between external clients and internal hosts.
- Internal: Between internal hosts.

**Infrastructure**:
- Border routers connect the data center to the public Internet.
- Inter-rack and intra-rack connections facilitated by switches and routers.

__Load Balancing__
- **Functionality**:
	- Distributes external client requests to hosts based on load.
	- Multiple load balancers may be used for different applications.
	- Acts as "layer-4 switches" (decisions based on destination port and IP address).
- **Operations**:
	- Load balancers forward requests to hosts and translate between public and internal IP addresses.
	- Enhances security by hiding internal network structure from clients.

__Hierarchical Architecture__
- **Structure**:
	- Scales from thousands to hundreds of thousands of hosts using hierarchical tiers of routers and switches.
	- Example: Border routers → access routers → tier-1 switches → tier-2 switches → TOR switches.
	- Ethernet used for link-layer and physical-layer protocols, with a mix of copper and fiber cables.
- **Redundancy and Reliability**:
	- Redundant network equipment and links ensure high availability.
	- VLANs partition subnets to localize ARP broadcast traffic.
- **Scalability Challenges**:
	- Host-to-host capacity limits due to shared link capacities.
	- Example: 40 simultaneous flows between different racks can reduce individual flow rate significantly below the network interface rate.

__Solutions to Scalability Challenges__
- **Higher-rate Equipment**:
	- Deploying higher-rate switches and routers is costly.
- **Co-location**:
	- Placing related services and data close together to reduce inter-rack communication.
	- Limited by the need for flexibility in service placement.
- **Increased Connectivity**:
	- More links between TOR and tier-2 switches, and between tier-2 and tier-1 switches.
	- Benefits:
		- Increased capacity and reliability.
		- Supports multi-path routing (e.g., ECMP, finer-grained load balancing).
		- Multipath routing designs route packets across multiple paths for efficiency.
- **Case Example**:
	- Facebook’s data center connects each TOR to four tier-2 switches, and each tier-2 switch to four tier-1 switches, supporting multipath routing and high throughput.

### 6.6.2 Trends in Data Center Networking

**Cost Reduction**:
- Internet cloud giants deploy new data center network designs for cost reduction, improved delay, throughput, and ease of expansion.
- Designs can be proprietary or open, e.g., Google’s Jupiter, Facebook’s architecture.
- Trend towards hierarchical, tiered networks for multiple paths and increased capacity and reliability, akin to Clos networks.

**Centralized SDN Control and Management**:
- Large operators like Google, Microsoft, and Facebook adopt SDN-like centralized control.
- Clear separation of data plane (commodity switches) and control plane (software-based).
- Importance of automated configuration and state management.

**Virtualization**:
- Virtual Machines (VMs) enable decoupling of applications from physical hardware, allowing VM migration.
- Standard Ethernet and IP protocols have limitations; data center networks use a single, flat, layer-2 network to handle VM migrations.
- Modified ARP mechanisms and scalable schemes enhance VM management.

**Physical Constraints**:
- Data centers have high capacity (40-100 Gbps) and low delays (microseconds).
- Small buffer sizes and fast-reacting congestion control protocols are required.
- Solutions include data center-specific TCP variants and RDMA technologies, and decoupling flow scheduling from rate control.

**Hardware Modularity and Customization**:
- Modular data centers (MDCs) are built in shipping containers, each with thousands of hosts.
- Containers are designed for graceful performance degradation and easy replacement.
- Networking challenges include container-internal and core networks, with hybrid electrical/optical switch architectures.
- Large providers customize network components and use availability zones for reliability.

## 6.7 Retrospective: A Day in the Life of a Web Page Request

Before diving into the topical chapters in the second part of this book, we take an integrated view of the protocols involved in satisfying a simple request: downloading a web page. 

**Scenario**: Bob connects his laptop to his school's Ethernet switch and downloads a web page from www.google.com. This process involves multiple protocols working together.

### 6.7.1 Getting Started: DHCP, UDP, IP, and Ethernet
![[Pasted image 20240530135940.png|400]]
**Initial Setup**:
- Bob connects his laptop to an Ethernet cable linked to the school’s Ethernet switch.
- The switch connects to the school’s router, which connects to an ISP (comcast.net).
- Comcast.net provides DNS service for the school.
- The DHCP server runs within the router.

**Obtaining an IP Address via DHCP**:
1. **DHCP Request Creation**:
	- Bob’s laptop creates a DHCP request message.
	- The message is placed within a UDP segment (dest port 67, source port 68).
	- The UDP segment is encapsulated in an IP datagram with a broadcast destination IP (255.255.255.255) and a source IP of 0.0.0.0.
2. **Encapsulation in Ethernet Frame**:
	- The IP datagram is placed within an Ethernet frame.
	- The frame has a destination MAC address of FF:FF:FF:FF:FF:FF (broadcast) and a source MAC address of Bob’s laptop (00:16:D3:23:68:8A).
3. **Broadcast by Switch**:
	- The Ethernet frame is sent by Bob’s laptop to the Ethernet switch.
	- The switch broadcasts the frame on all outgoing ports, including the one connected to the router.
4. **Router Processing**:
	- The router receives the Ethernet frame on its interface (MAC: 00:22:6B:45:1F:1B).
	- The IP datagram is extracted and processed, leading to the DHCP request being handled by the router’s DHCP server.
5. **DHCP Server Response**:
	- The DHCP server allocates an IP address (68.85.2.101) to Bob’s laptop.
	- It creates a DHCP ACK message containing this IP address, the DNS server IP (68.87.71.226), the default gateway IP (68.85.2.1), and the subnet block (68.85.2.0/24).
	- The DHCP ACK message is encapsulated in a UDP segment, then an IP datagram, and finally an Ethernet frame with the router’s MAC address as the source and Bob’s laptop’s MAC address as the destination.
6. **Unicast to Laptop**:
	- The Ethernet frame is sent by the router to the switch.
	- The switch, using its self-learning capability, forwards the frame directly to Bob’s laptop.
7. **Final Steps on Laptop**:
	- Bob’s laptop receives the frame, extracts the IP datagram, then the UDP segment, and finally the DHCP ACK message.
	- The laptop records its IP address and the DNS server IP.
	- It installs the default gateway’s address into its IP forwarding table.
	- Now, Bob’s laptop is ready to process the web page fetch.

### 6.7.2 Still Getting Started: DNS and ARP

**DNS Query Process**:
8. **Creating DNS Query**:
	- The OS creates a DNS query message with "www.google.com" in the question section.
	- The message is placed in a UDP segment (destination port 53).
	- The UDP segment is placed in an IP datagram with the DNS server’s IP (68.87.71.226) and the source IP (68.85.2.101).
9. **Encapsulation in Ethernet Frame**:
	- The datagram is placed in an Ethernet frame.
	- The frame needs to be sent to the gateway router, but the MAC address of the gateway router (68.85.2.1) is unknown.

**ARP Protocol for MAC Address**:
10. **Creating ARP Query**:
	- An ARP query message is created with the target IP address (68.85.2.1).
	- The ARP message is placed in an Ethernet frame with a broadcast destination address (FF:FF:FF:FF:FF:FF).
	- The frame is sent to the switch, which delivers it to all devices, including the gateway router.
11. **Gateway Router Response**:
	- The gateway router receives the frame, identifies the matching IP, and prepares an ARP reply with its MAC address (00:22:6B:45:1F:1B).
	- The ARP reply is placed in an Ethernet frame with the destination address of Bob’s laptop (00:16:D3:23:68:8A) and sent back through the switch.
12. **Receiving ARP Reply**:
	- Bob’s laptop receives the frame, extracts the MAC address of the gateway router.
	- The Ethernet frame containing the DNS query is now addressed to the gateway router’s MAC address.
	- The frame is sent to the switch, which delivers it to the gateway router.

### 6.7.3 Still Getting Started: Intra-Domain Routing to the DNS Server

**Forwarding DNS Query**:
13. **Gateway Router Processing**:
	- The gateway router receives the frame and extracts the IP datagram.
	- The destination address (68.87.71.226) is looked up in the forwarding table, directing the datagram to the Comcast router.
	- The datagram is placed in a link-layer frame appropriate for the school-Comcast link and sent.
14. **Comcast Network Processing**:
	- The Comcast router receives the frame, extracts the IP datagram, and forwards it based on intra-domain and inter-domain routing protocols (RIP, OSPF, IS-IS, BGP).
	- The datagram eventually reaches the DNS server.
15. **DNS Server Response**:
	- The DNS server extracts the DNS query, looks up "www.google.com", and finds the corresponding IP address (64.233.169.105).
	- A DNS reply message with the IP address is created and placed in a UDP segment, which is then placed in an IP datagram addressed to Bob’s laptop.
	- The datagram is sent back through the Comcast and school networks to Bob’s laptop.
16. **Receiving DNS Reply**:
	- Bob’s laptop receives the DNS reply, extracts the IP address of www.google.com, and is now ready to contact the server.

### 6.7.4 Web Client-Server Interaction: TCP and HTTP

**Establishing TCP Connection**:
17. **Creating TCP Socket**:
    - Bob’s laptop creates a TCP SYN segment (dest port 80) to establish a connection with www.google.com.
    - The TCP segment is placed in an IP datagram (dest IP 64.233.169.105) and then in an Ethernet frame (dest MAC 00:22:6B:45:1F:1B) and sent to the switch.
18. **Routing TCP SYN**:
    - The datagram is forwarded through the school, Comcast, and Google networks to www.google.com.
19. **Receiving TCP SYN at Google**:
    - Google’s server extracts the TCP SYN, creates a connection socket, and generates a TCP SYNACK segment.
    - The TCP SYNACK is placed in a datagram addressed to Bob’s laptop and sent back.
20. **Receiving TCP SYNACK**:
    - Bob’s laptop receives the TCP SYNACK, completing the three-way handshake, and the TCP socket enters the connected state.

**HTTP Request and Response**:
21. **Sending HTTP GET**:
    - Bob’s browser creates an HTTP GET message with the URL.
    - The GET message is placed in a TCP segment, then in a datagram, and sent to www.google.com.
22. **Processing HTTP GET**:
    - Google’s server reads the GET message, creates an HTTP response with the requested web page content, and sends it back to Bob’s laptop.
23. **Receiving HTTP Response**:
    - Bob’s laptop receives the HTTP response, extracts the HTML content, and displays the web page.

# 7. Wireless and Mobile Networks

## 7.2 Wireless Links and Network Characteristics

**Differences from Wired Links**:
- **Decreasing Signal Strength**:
	- Electromagnetic radiation attenuates through matter (e.g., walls).
	- Signal disperses in free space, decreasing strength (path loss) with distance.
- **Interference from Other Sources**:
	- Radio sources in the same frequency band interfere (e.g., 2.4 GHz phones and 802.11b LANs).
	- Electromagnetic noise (e.g., motors, microwaves) also causes interference.
	- Newer 802.11 standards use the 5GHz band to mitigate interference.
- **Multipath Propagation**:
	- Electromagnetic waves reflect off objects, taking different paths.
	- Causes signal blurring at the receiver.
	- Moving objects can change multipath propagation over time.

**Impacts on Wireless Communication**:
![[Pasted image 20240521140853.png|300]]
- **Bit Errors**:
	- More common in wireless links.
	- Wireless protocols (e.g., 802.11) use CRC error detection and reliable-data-transfer protocols for retransmitting corrupted frames.
- **Signal-to-Noise Ratio (SNR)**:
	- Measure of received signal strength relative to background noise.
	- Measured in decibels (dB).
	- Larger SNR makes it easier to extract the transmitted signal from noise.
- **Bit Error Rate (BER) vs. SNR**:
	- **Modulation Techniques**:
		- Higher SNR results in lower BER for a given modulation scheme.
		- Increasing transmission power can reduce BER but has diminishing returns and potential downsides (e.g., energy consumption, interference).
			- Also transmission power is fixed for most cases, standardized by the government.
	- **BER and Transmission Rate**:
		- Higher bit transmission rate increases BER for a given SNR.
		- Example: BPSK at 1 Mbps has lower BER than QAM16 at 4 Mbps with the same SNR.
		- Adaptive modulation can optimize transmission rate and BER based on channel conditions (used in 802.11 WiFi, 4G, 5G).

**Challenges in Wireless Networks**:
- **Hidden Terminal Problem**:
	- Physical obstructions prevent nodes from hearing each other's transmissions, causing interference at the receiver.
- **Signal Fading**:
	- Signal strength fades with distance, leading to undetectable collisions at the receiver.
- **Complexity in Multiple Access**:
	- Hidden terminal problem and signal fading make wireless multiple access more complex than in wired networks.

### 7.2.1 CDMA
**Introduction to CDMA**:
- CDMA (Code Division Multiple Access) is a channel partitioning protocol.
- Used in wireless LAN and cellular technologies.
- Encodes each bit by multiplying it by a fast-changing signal (the code).

**CDMA Encoding and Decoding**:
![[Pasted image 20240530140407.png|400]]
- **Encoding**: Each bit is multiplied by a sequence of values (the code) that changes faster than the data bits.
- **Decoding**: The receiver recovers the original data by multiplying the received encoded bits by the same code.

**Mathematical Representation**:
- Each data bit, \(d_i\), is multiplied by the corresponding code bit $c_m$ for each mini-slot $m$: $Z_{i,m} = d_i \times c_m$
- The receiver computes the original data bit by summing the product of the received encoded bits $Z_{i,m}$ and the code bits $c_m$:  $d_i = \frac{1}{M} \sum_{m=1}^{M} Z_{i,m} \times c_m$

**Interference Handling**:
- **Additive Signal**: Interference from multiple senders is additive.
- Example: If three senders send a 1 and a fourth sends a -1, the received signal is 2 (1 + 1 + 1 - 1 = 2).
- **Receiver Decoding**: Even with multiple senders, the receiver can recover the data using the sender's unique code.

**Example**:
- Two senders using different CDMA codes:
  ![[Pasted image 20240530140436.png|400]] 
	- Sender 1: Code (1, 1, 1, -1, 1, -1, -1, -1)
	- Sender 2: Code (1, -1, 1, 1, 1, -1, 1, 1)
- The receiver can decode the data from sender 1 despite the interference from sender 2.

**Analogy**:
- CDMA is like partygoers speaking different languages; each person can filter out the conversations in languages they don't understand, similar to how a CDMA receiver isolates the signal using the specific code.

**Practical Considerations**:
- **Code Selection**: CDMA codes must be carefully chosen for effective communication.
- **Signal Strength**: Assumes equal signal strengths from all senders, which can be challenging in practice.

## 7.3 WiFi: 802.11 Wireless LANs

![[Pasted image 20240530140517.png|500]]
**Pervasiveness**:
  - Widely used in workplaces, homes, educational institutions, cafés, airports, and public places.
  - Crucial access network technology in today's Internet.

**Dominant Standard**:
  - **IEEE 802.11 (WiFi)**: The leading standard for wireless LANs developed in the 1990s.

__802.11 Standards Overview__
- **Generations**:
  - **802.11 b, g, n, ac, ax**: Successive generations for WLANs, typically under 70m range.
  - **Branding**:
    - **WiFi 4**: 802.11n
    - **WiFi 5**: 802.11ac
    - **WiFi 6**: 802.11ax
  - **Special Standards**:
    - **802.11 af, ah**: For Internet of Things, sensor networks, and metering applications.
- **Common Characteristics**:
  - **Frame Format**: Shared across all 802.11 standards.
  - **Backward Compatibility**: Older devices (e.g., 802.11g) can interact with newer base stations (e.g., 802.11ac, 802.11ax).
  - **Medium Access Protocol**:
    - **CSMA/CA**: Used by all standards.
    - **802.11ax**: Also supports centralized scheduling by the base station.

__Physical Layer Differences__
 - **Frequency Ranges**:
  - **2.4–2.485 GHz (2.4 GHz range)**:
    - Unlicensed frequency band.
    - Competes with devices like 2.4 GHz phones and microwave ovens.
  - **5.1–5.8 GHz (5 GHz range)**:
    - Shorter transmission distance for a given power level.
    - More affected by multipath propagation.
- **Advanced Technologies**:
	- **MIMO Antennas**:
	    - Used in 802.11n, 802.11ac, and 802.11ax.
	    - Multiple antennas on sending and receiving sides for different signals.
  - **Smart Antennas**:
    - In 802.11ac and 802.11ax base stations.
    - Enable simultaneous transmission to multiple stations.
    - Adaptive beamforming to target specific receivers, reducing interference and increasing range at a given data rate.
- **Performance**:
	- **Data Rates**: Ideal rates shown in Table 7.1 assume optimal conditions (e.g., close proximity to base station, no interference).
	- **Real-World Variability**: Actual data rates may vary due to environmental factors.
- **Note**: 
	- YMMV (Your Mileage May Vary) highlights the variability in real-world wireless data rates compared to ideal scenarios.

### 7.3.1 The 802.11 Wireless LAN Architecture

![[Pasted image 20240530140554.png|400]]
**Principal Components**:
- **Basic Service Set (BSS)**: Fundamental building block containing wireless stations and a central base station (Access Point, AP).
- **Access Point (AP)**: Connects BSS to the Internet via interconnection devices (e.g., switch or router).
- **MAC Addresses**: Each 802.11 wireless station and AP have a unique 6-byte MAC address administered by IEEE.

**Infrastructure Wireless LANs**:
- **Infrastructure**: Comprises APs and wired Ethernet infrastructure connecting APs and a router.
- **Ad Hoc Networks**: Formed without central control, no external connections, created by devices in proximity needing communication.

__Channels and Association__
- **Association Process**:
	- Wireless stations must associate with an AP to send/receive data.
	- **SSID**: Assigned by the network administrator to identify the AP.
	- **Channel Numbers**: APs operate in 2.4 GHz to 2.4835 GHz range with 11 partially overlapping channels. Channels 1, 6, and 11 are non-overlapping.\
- **WiFi Jungle**:
	- **Definition**: Location where a device receives signals from multiple APs.
	- **Association**: Device must join one subnet by associating with one AP.
	- **Beacon Frames**: APs send periodic frames with SSID and MAC address, scanned by devices for association.
- **AP Selection**:
	- Devices typically select the AP with the highest signal strength, though signal strength isn’t the only performance factor.
	- **Alternative Selection Methods**: Various algorithms exist to choose APs based on factors beyond signal strength.

__Scanning Methods__
![[Pasted image 20240530140625.png|500]]
- **Passive Scanning**:
	- Devices scan channels and listen for beacon frames.
- **Active Scanning**:
	- Devices broadcast a probe frame, APs respond with a probe response frame.
	- Device sends an association request frame, AP responds with an association response frame.
- **IP Address Assignment**:
	- After association, device sends a DHCP discovery message to obtain an IP address from the subnet.

__Authentication__
- **Authentication Methods**:
	- **MAC Address-Based**: Common in company networks.
	- **Username and Password**: Common in public networks like cafés.
	- **Authentication Servers**: APs communicate with servers using protocols like RADIUS or DIAMETER for authentication.
- **Security**:
	- **Centralized Authentication**: Reduces AP complexity and centralizes sensitive decisions.
	- **IEEE 802.11i**: New protocol defining security aspects, follows centralized authentication approach.

### 7.3.2 The 802.11 MAC Protocol
![[Pasted image 20240530140710.png|200]]
__Association with AP__
- **Process**: Wireless device associates with an Access Point (AP).
- **Multiple Access Protocol**: Needed to coordinate transmissions from multiple devices/APs over the same channel.

__CSMA/CA Protocol__
- **Choice**: Random access protocol inspired by Ethernet.
- **Definition**: Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA).

__Key Differences from Ethernet__
- **Collision Avoidance**: Instead of collision detection.
- **Link-layer Acknowledgment**: Due to high bit error rates in wireless channels.

__Collision Detection Challenges__
- **Hardware Limitation**: Difficult to detect collisions due to signal strength differences.
- **Hidden Terminal Problem**: Not all collisions can be detected.

__Collision Avoidance Techniques__
- **Transmission Protocol**:
	1. **Sense Channel Idle**: If idle, transmit after Distributed Inter-frame Space (DIFS).
	2. **Backoff**: If busy, choose a random backoff value using binary exponential backoff.
	3. **Transmit Frame**: When counter reaches zero and channel is idle.
	4. **Acknowledgment**: Wait for acknowledgment; if received, proceed; otherwise, reenter backoff.

__Hidden Terminals: RTS/CTS Scheme__
![[Pasted image 20240530140746.png|300]]
- **Purpose**: To avoid collisions in the presence of hidden terminals.
- **Process**:
	1. **RTS Frame**: Sender requests to send data.
	2. **CTS Frame**: AP grants permission and notifies other stations.
- **Advantages**:
	- Mitigates hidden station problem.
	- Reduces collision duration.
- **Usage**: Typically for long data frames due to introduced delay and resource consumption.
  ![[Pasted image 20240530140839.png|400]]

__Point-to-Point Link__
- **Directional Antennas**: Can use 802.11 protocol over a point-to-point link.
- **Applications**: Inexpensive wireless point-to-point connections over long distances.

__Detailed Process Breakdown__
1. **Channel Sensing and Idle Detection**:
	- Station senses the channel.
	- If idle, waits DIFS then transmits.
2. **Backoff Mechanism**:
	- If busy, station waits using binary exponential backoff.
	- Countdown starts when channel is idle.
	- Transmits when countdown reaches zero.
3. **Frame Transmission**:
	- Transmit entire frame without collision detection.
	- Wait for acknowledgment from receiver.
4. **Acknowledgment Handling**:
	- If acknowledgment received, proceed to next frame.
	- If not, retransmit using backoff.
5. **RTS/CTS for Collision Avoidance**:
	- Sender sends RTS to AP.
	- AP responds with CTS.
	- Other stations defer transmission upon receiving CTS.
6. **Point-to-Point 802.11 Links**:
	- Directional antennas create a point-to-point connection.
	- Enables long-distance, low-cost wireless connections.

### 7.3.3 The IEEE 802.11 Frame

![[Pasted image 20240530140909.png|400]]
**Overview**:
- Similar to Ethernet frames, but with additional fields for wireless links.
- Frame fields include payload, CRC, address fields, sequence number, duration, and frame control.

**Payload and CRC Fields**:
- **Payload**: Contains an IP datagram or ARP packet, typically fewer than 1,500 bytes, but can be up to 2,312 bytes.
- **CRC**: 32-bit cyclic redundancy check to detect bit errors, more crucial in wireless LANs.

**Address Fields**:
- **Four address fields**: Each holds a 6-byte MAC address.
	- **Address 2**: MAC address of the transmitting station (wireless station or AP).
	- **Address 1**: MAC address of the receiving station (destination AP or wireless station).
	- **Address 3**: MAC address of the router interface connecting subnets.
	- **Address 4**: Used in ad hoc mode (not discussed here).

**Internetworking Example**:
1. **Router to Station H1**:
	- Router R1 uses ARP to find H1's MAC address, encapsulates the datagram in an Ethernet frame.
	- AP converts the Ethernet frame to an 802.11 frame, setting Address 1 (H1’s MAC), Address 2 (AP’s MAC), and Address 3 (R1’s MAC).
1. **Station H1 to Router R1**:
	- H1 creates an 802.11 frame, setting Address 1 (AP’s MAC), Address 2 (H1’s MAC), and Address 3 (R1’s MAC).
	- AP converts the 802.11 frame back to an Ethernet frame for transmission to R1.

**Sequence Number, Duration, and Frame Control Fields**:
- **Sequence Number**: Distinguishes between new transmissions and retransmissions.
- **Duration**: Indicates the time required to transmit the frame and its acknowledgment.
- **Frame Control Field**:
	- **Type and Subtype**: Identify the frame type (association, RTS, CTS, ACK, data).
	- **To and From Fields**: Define the meanings of address fields, varying by mode and sender.
	- **WEP Field**: Indicates whether encryption is used (discussed in Chapter 8).

### 7.3.4 Mobility in the Same IP Subnet

**Increasing Wireless LAN Range**:
- Multiple BSSs are deployed within the same IP subnet to extend physical range.
- Key issue: Seamless mobility among BSSs while maintaining ongoing TCP sessions.

**Example of Mobility Between BSSs**:
- **Scenario**: Host H1 moves from BSS1 to BSS2 (Fig. 7.15).
- **Same Subnet**: Interconnection device is not a router; all stations and APs share the same IP subnet.
	- **Result**: H1 keeps its IP address and TCP connections when moving between BSSs.
- **Router Scenario**: If the interconnection device were a router, H1 would need a new IP address, disrupting TCP connections.

**Movement Process**:
- **Detecting Signal Weakening**: H1 detects weakening signal from AP1.
- **Scanning for Stronger Signal**: H1 scans and finds stronger signal from AP2.
- **Association Change**: 
	- H1 disassociates from AP1.
	- H1 associates with AP2.
	- Maintains IP address and ongoing TCP sessions.

**Switch Considerations**:
- **Self-Learning Switches**:
	- Switches build forwarding tables automatically (self-learning).
	- Suitable for occasional moves but not highly mobile users with ongoing TCP sessions.
- **Forwarding Table Issue**:
	- Before the move: Switch pairs H1’s MAC address with AP1’s interface.
	- After the move: Frames should be directed to AP2.
- **Solution**:
	- AP2 sends a broadcast Ethernet frame with H1’s source address to the switch.
	- Switch updates its forwarding table to direct frames to AP2.
	- 802.11f standards group developing inter-AP protocol for these issues.

**VLANs and Mobility**:
- **VLAN Connectivity**: VLANs can connect islands of LANs into a large virtual LAN spanning a wide region.
- **Handling Mobility**: Mobility among base stations within a VLAN handled similarly to the process above.

### 7.3.5 Advanced Features in 802.11

__802.11 Rate Adaptation__
- **Concept**:
	- Different modulation techniques are appropriate for different Signal-to-Noise Ratio (SNR) scenarios.
	- Modulation technique should adapt as SNR changes due to user mobility to maintain low Bit Error Rate (BER).
- **Mechanism**:
	- Adaptive selection of physical-layer modulation based on channel characteristics.
	- **Fallback**: If two consecutive frames are not acknowledged (indicating bit errors), the transmission rate decreases.
	- **Increase**: If 10 consecutive frames are acknowledged, or a timer expires, the transmission rate increases.

__Power Management__
- **Importance**:
	- Critical for conserving power in mobile devices.
- **Operation**:
	- **Sleep/Wake States**: Nodes can alternate between sleep and wake states.
	- **Sleep Notification**: Node sets the power-management bit in the frame header to 1 to notify the AP it’s going to sleep.
	- **Beacon Frame Timing**: Node sets a timer to wake up just before the AP sends its beacon frame (typically every 100 msec).
- **AP Role**:
	- **Frame Buffering**: AP buffers frames for the sleeping node and avoids sending frames to it during sleep.
	- **Beacon Frames**: Contain a list of nodes with buffered frames.
- **Node Actions**:
	- **Wake Up**: Just before the beacon, enter fully active state quickly (250 microseconds).
	- **Check for Buffered Frames**: If no frames are buffered, node goes back to sleep. Otherwise, it requests buffered frames by sending a polling message.
- **Efficiency**:
	- With a wakeup time of 250 microseconds and minimal time to receive and check the beacon frame, nodes can be asleep 99% of the time if there are no frames to send or receive, leading to significant energy savings.

### 7.3.6 Personal Area Networks: Bluetooth

**Everyday Use**:
  - Cable replacement technology for peripherals (keyboard, mouse, earbuds, speakers, watches, health bands).
  - Connects smartphones to car audio systems.
  - Operates over short ranges (tens of meters), at low power, and low cost.
  - Known as Wireless Personal Area Networks (WPANs) or piconets.

**Technical Details**:
  - **Link-Level Techniques**: Includes TDM, frequency division, randomized backoff, polling, error detection/correction, and reliable data transfer via ACKs/NAKs.
  - **Frequency Band**: Operates in the unlicensed 2.4 GHz ISM band with devices like microwaves, garage door openers, and cordless phones.
  - **Noise and Interference**: Designed to handle noise/interference with Frequency-Hopping Spread Spectrum (FHSS).
  - **Data Rates**: Can reach up to 3 Mbps.

**Ad Hoc Network Structure**:
  - No network infrastructure needed.
  - Devices form a piconet with up to eight active devices.
  - **Master Node**: Controls the piconet, including clock, frequency hopping, client entry, transmission power, and polling.
  - **Client Devices**: Can be active or parked (up to 255 parked devices).
  - **Parked Devices**: Sleep mode to conserve energy, wake periodically to receive beacon messages, must be activated by the master to communicate.

**Network Formation (Bootstrap Process)**:
  - **Neighbor Discovery**: Master broadcasts 32 inquiry messages on different frequencies, repeated up to 128 times.
    - Clients listen for inquiry messages, back off randomly to avoid collisions, and respond with device ID.
  - **Paging Process**: Master invites discovered clients to join the piconet.
    - Master sends 32 identical paging invitations on different frequencies.
    - Clients respond with ACK, receive frequency-hopping info, clock sync, and active member address.
    - Master polls the client to ensure connection.

**Higher-Level Protocols**:
  - Provide reliable data transfer, circuit-like streaming for audio/video.
  - Allow changes in transmission power levels and device states (active/parked).
  - Address low energy and security considerations in newer versions.

## 7.4 Cellular Networks: 4G and 5G

__Ubiquity and Performance of 4G__
- **Coverage**:
	- 4G network access is pervasive.
	- Over 90% coverage in the US with download speeds of 20 Mbps and higher.
	- Korea’s major carriers provide 95-99.5% coverage.
- **Applications**:
	- Streaming HD videos, videoconferences while on the move.
	- Enabled new IoT applications: Internet-connected bikes, scooters.
	- Smartphone applications: Mobile payments, Internet messaging (WeChat, WhatsApp).

__Cellular Network Structure__
- **Cells**:
	- Region covered by a cellular network is divided into cells.
	- Each cell has a base station for signal transmission and reception.
	- Coverage area depends on:
		- Transmitting power of base station and devices.
		- Obstructing buildings.
		- Height and type of base station antennas.

__Overview of 4G and 5G Networks__
- **Wireless First Hop**:
	- Connection between the mobile device and the base station.
- **All-IP Core Network**:
	- Connects the wireless first hop to the carrier’s network.
	- Links to other carrier networks and the larger Internet.

__Architectural Principles in 4G Networks__
- **Protocol Layering**:
	- Similar to Internet-focused architectures.
- **Edge/Core Distinction**:
	- Clear separation of data and control planes.
	- Logically centralized control.
- **Global Network Interconnection**:
	- Multiple provider networks form a global "network of networks."
- **Internet Protocols**:
	- Many Internet protocols are used in the all-IP core of 4G networks.0

### 7.4.1 4G LTE Cellular Networks: Architecture and Elements

![[Pasted image 20240530141018.png|500]]
__Mobile Device (User Equipment, UE)__
- **Function**: Connects to the cellular carrier’s network.
- **Applications**: Web browsers, map apps, voice/video apps, mobile payment apps.
- **Network Endpoint**: Implements full 5-layer Internet protocol stack.
- **Identification**: 
	- IP address (via NAT).
	- International Mobile Subscriber Identity (IMSI) stored on SIM card.
	- IMSI is globally unique and analogous to a MAC address.
- **Role**: Stores subscriber services and encryption key information.

__Base Station (eNode-B)__
- **Function**: Manages wireless radio resources and mobile devices within its coverage area.
- **Roles**:
	- Device authentication and resource allocation.
	- Creates device-specific IP tunnels.
	- Coordinates with nearby base stations to manage radio spectrum.
- **Comparison**: Similar to APs in wireless LANs but with additional responsibilities.

__Home Subscriber Server (HSS)__
- **Role**: Control-plane element.
- **Function**: Stores information about mobile devices in its home network.
- **Usage**: Works with MME for device authentication.

__Serving Gateway (S-GW) and Packet Data Network Gateway (P-GW)__
- **Function**: Routers on the data path between mobile device and Internet.
- **P-GW Specific Roles**:
	- Provides NAT IP addresses.
	- Performs NAT functions.
	- Last LTE element before Internet.
- **Network Role**: Hides mobility of mobile nodes from the outside world.

![[Pasted image 20240530141228.png|400]]
__Mobility Management Entity (MME)__
- **Role**: Control-plane element.
- **Functions**:
	- Device authentication with HSS.
	- Sets up IP tunnels on data paths.
	- Maintains active device’s cell location.
- **Not In Data Path**: Does not forward datagrams.

__Authentication Process__
- **Importance**: Network and mobile device must authenticate each other.
- **Process**: 
	- MME acts as a middleman between mobile device and HSS.
	- MME contacts HSS in the mobile’s home network after an attach request.
	- HSS provides encrypted information for mutual authentication.

__Path Setup__
- **Data Path Components**:
	- Wireless first hop (mobile device to base station).
	- IP tunnels (base station to S-GW, S-GW to P-GW).
- **Tunnels**: Controlled by MME to facilitate mobility; endpoint changes with device movement.

__Cell Location Tracking__
- **Movement**: Base stations update MME on device’s location.
- **Sleep Mode**: MME locates device through paging when moving between cells.

### 7.4.2 LTE Protocols Stacks

**Overview**:
- Focus on link and physical layers, and mobility management due to LTE's all-IP architecture.
- Higher-layer protocols (IP, TCP, UDP) are already familiar from previous chapters.

**User-Plane Protocol Stacks**:
- **Figure 7.21**: Shows stacks at LTE mobile node, base station, and serving gateway.
- **Control-Plane Protocols**: Discussed later in mobility management (Section 7.6) and security (Section 8.8).

**Link Layer Sublayers**:
1. **Packet Data Convergence Protocol (PDCP)**:
	- Sits below IP.
	- Performs IP header compression to reduce bits over the wireless link.
	- Handles encryption/decryption using keys established via signaling messages between the LTE mobile device and the Mobility Management Entity (MME).
2. **Radio Link Control (RLC) Protocol**:
	- Fragmentation and reassembly of IP datagrams too large for link-layer frames.
	- Provides link-layer reliable data transfer using an ACK/NAK-based ARQ protocol.
3. **Medium Access Control (MAC)**:
	- Performs transmission scheduling.
	- Handles error detection/correction with redundant bit transmission as a forward error-correction technique.
	- Adapts redundancy based on channel conditions.

**Tunnels in User Data Path**:
- Established under MME control when the device first attaches to the network.
- Unique tunnel endpoint identifier (TEID) for each tunnel.
- Base station encapsulates datagrams using the GPRS Tunneling Protocol (GTP), sends them in UDP segments to the Serving Gateway, and decapsulates them for the mobile device.

### 7.4.3 LTE Radio Access Network

![[Pasted image 20240530141347.png|400]]
**Orthogonal Frequency Division Multiplexing (OFDM)**:
- Uses frequency division and time division multiplexing on the downstream channel.
- Allocates 0.5 ms time slots in one or more channel frequencies to mobile devices.
- **Figure 7.22**: Illustrates allocation of eight time slots over four frequencies.

**Time Slot Allocation**:
- Not mandated by LTE standard.
- Determined by LTE equipment vendor or network operator using scheduling algorithms.
- Opportunistic scheduling optimizes the use of the wireless medium based on channel conditions.
- User priorities and service levels (silver, gold, platinum) influence scheduling.

**LTE-Advanced**:
- Allows for downstream bandwidths of hundreds of Mbps by allocating aggregated channels to a mobile device.

### 7.4.4 Additional LTE Functions: Network Attachment and Power Management

__Network Attachment__
- **Process Phases**:
	1. **Attachment to a Base Station**:
		- Similar to 802.11 association but different in practice.
		- Mobile device searches for a primary synchronization signal broadcast by a base station.
		- Locates secondary synchronization signal for additional information like channel bandwidth and carrier information.
		- Establishes control-plane signaling connection with the base station.
	2. **Mutual Authentication**:
		- Base station contacts local MME for mutual authentication.
		- Ensures the device is associated with a given IMSI and the network is a legitimate carrier.
		- MME configures the Mobile-device-to-PDN-gateway data path.
	3. **Data Path Configuration**:
		- MME establishes tunnels between the mobile device, Serving Gateway, and base station.
		- Mobile device can send/receive IP datagrams via these tunnels to/from the Internet.

__Power Management: Sleep Modes__
- **Sleep States**:
	1. **Discontinuous Reception State**:
		- Entered after several hundred milliseconds of inactivity.
		- Mobile device schedules periodic wake-up times to monitor the channel for transmissions.
	2. **Idle State**:
		- Entered after 5 to 10 seconds of inactivity.
		- Mobile device wakes up less frequently.
		- No need to inform previous base station if moving to a new cell.
		- Mobile device re-establishes association with a base station to check for paging messages broadcast by the MME.

### 7.4.5 The Global Cellular Network: A Network of Networks

![[Pasted image 20240530141639.png|400]]
**Overview**:
  - The global cellular network is a "network of networks" similar to the Internet.
  - A user’s mobile device connects via a 4G base station to the home network, operated by carriers like Verizon, AT&T, T-Mobile, etc.
  - The home network connects to other cellular networks and the global Internet through gateway routers.
  - Mobile networks interconnect via the public Internet or an Internet Protocol Packet eXchange (IPX) Network.
  - 4G networks can also peer with 3G and earlier networks.

**Future Topics**:
  - Mobility management in Section 7.6.
  - 4G security in Section 8.8.2.
  - Emerging 5G networks.

### 7.4.6 5G Cellular Networks

**Ultimate Wide-Area Data Service**:
  - Goal: Gigabit connection speeds, low latency, unlimited users/devices.
  - Applications: Augmented reality, virtual reality, autonomous vehicles, factory robots, fixed wireless Internet services.

**5G Advancements**:
  - Expected improvements: 10x increase in peak bitrate, 10x decrease in latency, 100x increase in traffic capacity over 4G.
  - 5G NR (New Radio): Standard adopted by 3GPP.
  - Other technologies: Verizon’s 5G TF network on 28 and 39 GHz for fixed wireless Internet.

**Frequency Groups**:
  - FR1: 450 MHz–6 GHz.
  - FR2: 24 GHz–52 GHz (millimeter wave frequencies).

**Drawbacks of Millimeter Wave**:
  - Shorter range, requiring denser base station deployment.
  - Susceptible to atmospheric interference (foliage, rain).

**Three Co-existing Standards**:
  - **eMBB (Enhanced Mobile Broadband)**:
    - Increased bandwidth, higher speeds, moderate latency reduction.
    - Supports rich media applications (AR, VR, 4K video).
  - **URLLC (Ultra Reliable Low-Latency Communications)**:
    - Targeted at latency-sensitive applications (factory automation, autonomous driving).
    - Aims for latencies of 1ms.
  - **mMTC (Massive Machine Type Communications)**:
    - Narrowband for IoT applications (sensing, metering, monitoring).
    - Focus on reducing power requirements and latency for IoT devices.

**5G and Millimeter Wave Frequencies**:
  - Potential for 100x increase in capacity over 4G.
  - **Capacity Equation**: 
    - Capacity = cell density * available spectrum * spectral efficiency.
    - Increased cell density due to shorter range.
    - Larger available spectrum in FR2 band.
    - Improved spectral efficiency using MIMO technology (multiple antennas and beamforming).

**Challenges**:
  - Millimeter wave signals blocked by buildings and trees.
  - Need for small cell stations in populous regions (10 to 100 meters apart).

**5G Core Network**:
  - Redesigned for better integration with Internet and cloud services.
  - Includes distributed servers and caches to reduce latency.
  - Utilizes network function virtualization and network slicing.

**New 5G Core Network Functions**:
  - **User-Plane Function (UPF)**: Distributes packet processing to the network edge.
  - **Access and Mobility Management Function (AMF)**: Manages connection and mobility tasks.
  - **Session Management Function (SMF)**: Handles session management, IP address management, and acts as DHCP.

**Current Status**:
  - Early stages of deployment with ongoing standardization.
  - Future impact on broadband wireless service, indoor wireless service competition, factory automation, autonomous vehicles, and wide-area wireless service.

## 7.5 Mobility Management: Principles

### 7.5.1 Device Mobility: a Network-layer Perspective

**Forms of Mobility**:
- A mobile device changes its point of attachment to the network over time.
- Different challenges arise depending on device activity and mobility.

**Scenarios**:
- **Scenario (a)**:
	- User physically moves between networks, powering down the device during moves.
	- Device associates and disassociates from networks serially.
	- Handled by existing networking mechanisms (Sections 7.3 and 7.4).
- **Scenario (b)**:
	- Device remains attached to the same access network despite physical movement.
	- Not considered mobile from a network-layer perspective.
	- No link-layer mobility if the device remains associated with the same AP or base station.
- **Scenario (c)**:
	- Device changes its access network while sending/receiving IP datagrams and maintaining connections.
	- Requires handover for datagram forwarding between APs or base stations.
	- Handover can be managed by a single provider or coordinated between multiple providers.
- **Scenario (d)**:
	- Device roams between multiple provider networks.
	- Complicated handover process due to inter-provider coordination.

### 7.5.2 Home Networks and Roaming on Visited Networks

**Home Networks**:
- Each cellular subscriber has a home network storing subscriber information in the Home Subscriber Service (HSS).
- HSS includes device ID, service information, cryptographic keys, and billing data.

**Roaming**:
- When a device connects to a network other than its home network, it roams on a visited network.
- Coordination is needed between home and visited networks.

**Internet Context**:
- No strong notion of home/visited networks in the Internet.
- Examples: student’s home network might be their school network; mobile professional’s home network might be their company network.

**Mobile IP Protocol**:
- Proposed to incorporate the notion of home/visited networks.
- Limited deployment/use in practice.

**Eduroam**:
- Provides authenticated network access across visited IP networks, built on existing IP infrastructure.

**Advantages of Home Networks**:
- Single location for device information.
- Serves as a coordination point for communication to/from roaming devices.

**Analogy**:
- Bob, a mobile adult, registers his current address with his family.
- Friends contact the family home to find Bob's current address.
- Communication can be indirect (forwarded mail) or direct (using the updated address).

### 7.5.3 Direct and Indirect Routing to/from a Mobile Device

__Introduction__
- **Scenario**: A correspondent wants to communicate with a mobile device in its home network or a visited network.
- **Context**: Discusses 4G/5G cellular networks, with principles applicable to both cellular networks and the Internet.
- **Identifiers**: Mobile devices have globally unique identifiers (IMSI in 4G, permanent IP address in Mobile IP architecture).

__Approaches to Routing in Mobile Networks__
1. **Leveraging Existing IP Address Infrastructure**:
	- **Method**: Use BGP to advertise routes to mobile devices by their specific IP addresses.
	- **Process**: Visited network advertises the mobile device’s IP address. Other networks propagate this information, directing datagrams to the visited network.
	- **Drawback**: Scalability issues due to the need for routers to maintain entries for potentially billions of mobile devices and frequent updates as devices roam.

2. **Using Mobile Device’s Home Network**:
	- **Method**: Push mobility functionality to the network edge via the home network.
	- **Components**:
		- **MME and HSS**: Track mobile device location within the home network.
		- **Database Updates**: Visited network updates home network’s HSS with device location.
	- **Addressing**:
		- Mobile device may use a permanent address, a new address from the visited network, or a NAT address.
		- **NAT**: Visited network gateway router performs NAT translation.

__Routing Approaches__
1. **Indirect Routing to a Mobile Device**:
   ![[Pasted image 20240530145950.png|400]]
	- **Process**:
		- Correspondent sends a datagram to the mobile device’s permanent address.
		- Home network’s gateway intercepts and forwards the datagram to the visited network.
		- Visited network forwards it to the mobile device, performing NAT if necessary.
		- Encapsulation/decapsulation is used (tunneling).
	- **Sending from Mobile Device**:
		- Datagrams are sent through the visited network gateway.
		- Options:
			- Tunnel back to the home gateway (4a).
			- Transmit directly to the correspondent (local breakout) (4b).
	- **New Functionalities**:
		- Mobile-device-to-visited-network association protocol.
		- Visited-network-to-home-network-HSS registration protocol.
		- Datagram tunneling protocol.
	- **Continuity**:
		- Update home network HSS and tunnel endpoint when the device moves to a new network.
		- Minimal datagram loss if the transition time between networks is small.
2. **Direct Routing to a Mobile Device**:
   ![[Pasted image 20240530150005.png|400]]
	   - **Process**:
	     - Correspondent queries HSS to find the mobile device’s visited network.
	     - Correspondent tunnels datagrams directly to the visited network.
	   - **Challenges**:
	     - Requires a mobile-user location protocol for querying HSS.
	     - Protocols needed to update the correspondent when the mobile device moves between visited networks.
	   - **Advantage**: Avoids the triangle routing problem, providing a more efficient route.

## 7.6 Mobility Management in Practice

**Introduction**:
- Key challenges and solutions for device mobility:
	- Home and visited networks
	- Home network as central information and control hub
	- Control-plane functions for tracking roaming devices
	- Data-plane approaches: direct and indirect routing

**Focus**:
- Mobility management in 4G/5G networks
- Mobile IP for Internet mobility

### 7.6.1 Mobility Management in 4G/5G Networks

**Background**:
- 4G/5G networks build on 3G and 2G networks
- Focus on interoperability of network elements for mobility services

![[Pasted image 20240530150037.png|400]]
**Scenario**: Mobile user moving between 4G/5G base stations while streaming HD video.
__Steps in Mobility Management:__
1. **Mobile device and base station association**:
	- Device listens to base station signals and selects one
	- Provides base station with IMSI for identification
2. **Control-plane configuration**:
	- MME in visited network contacts home network
	- Retrieves authentication and network service information
	- Mutual authentication ensures device and network verification
	- HSS in home network updates database with device’s location
	- Establishes control-plane state and parameters for data-plane channel
3. **Data-plane configuration**:
	- MME configures two tunnels:
	     - Base station to Serving Gateway in visited network
	     - Serving Gateway to PDN Gateway in home network
	- Uses GTP protocol for tunneling
	- Compares with mobility within home network:
	     - Both use Serving Gateway in device’s network
	     - Indirect routing through home network
	- Local breakout (alternative) is rarely used
4. **Mobile device handover**:
	- Handover between base stations involves:
	     - Selection of target base station
	     - Pre-allocation of resources by target base station
	     - Informing mobile device of target base station
	     - Stopping and reconfiguring tunnel datagram forwarding
	- Involves local changes if base stations are near each other
	- Reasons for handover:
	     - Signal deterioration
	     - Cell congestion
	     - Mobile measures signals and reports to source base station
	- Source base station initiates handover based on measurements and other factors

**Handover Process**:
1. Source base station selects target base station, sends Handover Request.
2. Target base station pre-allocates resources, sends Handover Request Acknowledge.
3. Source base station informs mobile device about target base station.
4. Source base station forwards datagrams to target base station.
5. Target base station informs MME, which reconfigures tunnel to terminate at target base station.
6. Target base station confirms tunnel reconfiguration, source base station releases resources.
7. Target base station begins delivering datagrams to mobile device.

**Future of 5G Mobility**:
- 5G networks will be denser with smaller cell sizes
- Handover will be critical for real-time applications
- Migration of control plane to SDN for higher capacity and lower latency
- Ongoing research into SDN applications in 5G networks

### 7.6.2 Mobile IP

**Context and Deployment**:
- The Internet lacks widely deployed infrastructure for "on the go" mobile users, unlike 4G/5G networks.
- **Mobile IP** architecture and protocols [RFC 5944] have been standardized for over 20 years.
- **Lack of Deployment**: Due to lack of motivating business/use cases and the rise of alternative cellular network solutions.
- **Historical Context**: 2G networks provided mobile voice services; 3G networks supported voice and data, addressing mobile user needs through dual technology solutions (cellular for mobility, 802.11 for local/stationary use).

**Importance of Mobile IP**:
- Mobile IP offers similar services and mobility principles as cellular networks.
- Defined primarily in **RFC 5944 for IPv4**.
- Similar architecture to cellular networks with home and foreign networks and the use of indirect routing.

**Mobile IP Architecture**:
- **Home Network**: Mobile device has a permanent IP address.
- **Foreign Networks**: Mobile device receives a care-of-address.
- **Home Agent**: Tracks location updates from foreign agents.
- **Indirect Routing**: Uses tunnels to connect home and foreign network routers.

**Main Components of Mobile IP**:
1. **Agent Discovery**:
	- Foreign agents advertise mobility services to mobile devices.
	- Includes care-of-address allocation, registration with the home agent, and datagram forwarding.
2. **Registration with Home Agent**:
	- Protocols for mobile devices/foreign agents to register and deregister care-of-addresses with the home agent.
3. **Indirect Routing of Datagrams**:
	- Defines forwarding of datagrams to mobile devices by the home agent.
	- Includes rules for forwarding, handling errors, and tunneling [RFC 2003, RFC 2004].

## 7.7 Wireless and Mobility: Impact on Higher-Layer Protocols

__Introduction__
- **Wireless Networks vs. Wired Networks**:
	- Wireless networks differ significantly from wired networks at both the link layer and network layer.
	- Despite similar network-layer best-effort delivery models, transport and application layers can experience different performance in wireless networks.

__Transport Layer Protocols in Wireless Networks__
- **TCP Performance**:
	- TCP retransmits segments lost or corrupted due to network congestion or handover delays.
	- TCP’s ACK mechanism does not distinguish the cause of segment loss.
	- TCP's congestion-control decreases the congestion window uniformly, assuming congestion as the cause of loss, which is not always accurate in wireless networks.
	- Wireless networks have higher bit error rates, making TCP’s congestion control less effective.
- **TCP Challenges and Solutions**:
	- Researchers identified issues with TCP’s congestion control in wireless settings in the early to mid-1990s.
	- Three broad classes of approaches were proposed:
		- **Local Recovery**:
		    - Protocols recover from bit errors locally, such as the 802.11 ARQ protocol or combinations of ARQ and FEC in 4G/5G networks.
		- **TCP Sender Awareness of Wireless Links**:
		    - TCP sender and receiver become aware of the wireless link.
		    - Distinguish between congestion losses and corruption/loss on wireless links.
		    - Invoke congestion control only for congestive wired-network losses.
		    - Research includes [Liu 2003] and [Huang 2013] for more LTE-friendly transport mechanisms.
		- **Split-Connection Approaches**:
			- End-to-end connection split into two transport-layer connections:
				- One from the mobile host to the wireless access point.
				- One from the wireless access point to the wired host.
			- Can use standard TCP or specialized error recovery protocols.
			- Studies such as [Bakre 1995], [Yavatkar 1994], and [Wei 2006] show significant improvements with split connections.

__Application Layer Protocols in Wireless Networks__
- **Bandwidth Considerations**:
	- Bandwidth is a scarce commodity in wireless links, especially cellular links.
	- Applications must adapt content delivery (e.g., image-rich content) to the available bandwidth on wireless connections.
- **Opportunities in Mobility**:
	- Mobility enables location-aware and context-aware applications.
	- Rich potential for future ubiquitous computing environments.
	- Research and potential developments are still in early stages, indicating much more impact to come.

# Security in Computer Networks
## 8.1 What Is Network Security?

__Introduction__
- **Scenario**: Alice and Bob want to communicate securely over an insecure medium.
- **Threat**: Intruder (Trudy) may intercept communications.
- **Goals**:
	- Ensure only Bob can understand Alice's message.
	- Bob verifies the message is from Alice.
	- Messages are not altered in transit.
	- Ensure communication resources are accessible.

__Desirable Properties of Secure Communication__
- **Confidentiality**:
	- Only sender and receiver understand the message.
	- Messages are encrypted to prevent eavesdropping.
	- Focus on cryptographic techniques (Section 8.2).
- **Message Integrity**:
	- Ensure communication is not altered maliciously or accidentally.
	- Uses checksumming techniques (Section 8.3).
- **End-point Authentication**:
	- Confirm identities of communicating parties.
	- Example: Verifying user identity when accessing an inbox (Section 8.4).
- **Operational Security**:
	- Protect organizational networks connected to the public Internet.
	- Counter threats like worms, data theft, network mapping, and DoS attacks.
	- Use of firewalls and intrusion detection systems (Section 8.9).

__Intruder Capabilities and Threats__
- **Intruder Actions**:
	- **Eavesdropping**: Sniffing and recording control/data messages.
	- **Modification**: Inserting, altering, or deleting messages.
- **Potential Attacks**:
	- **Snooping**: Stealing passwords and data.
	- **Impersonation**: Pretending to be another entity.
	- **Session Hijacking**: Taking over an ongoing session.
	- **Denial of Service (DoS)**: Overloading system resources to deny service.
- **Real-world Threats**:
	- **Reported Attacks**: Maintained at the CERT Coordination Center.

__Real-world Examples of Secure Communication Needs__
- **Human Users**: Secure email between real individuals.
- **E-commerce**: Secure credit card transactions.
- **Online Banking**: Secure interactions with banks.
- **Network Infrastructure**: Secure DNS lookups, routing information exchange, network management.

__Importance of Cryptography__
- **Central Role**:
	- Provides confidentiality, end-point authentication, and message integrity.
	- Essential to network security.

## 8.2 Principles of Cryptography

**Historical Context**:
  - Cryptography dates back to Julius Caesar.
  - Modern techniques have advanced significantly in the past 30 years.
  - For detailed history, see Kahn’s "The Codebreakers" [Kahn 1967] and Singh’s "The Code Book" [Singh 1999].
  - Comprehensive discussions on cryptography can be found in [Bishop 2003; Kaufman 2002; Schneier 2015].

**Scope**:
  - Focuses on essential aspects of cryptography as practiced on the Internet.
  - Cryptographic techniques are integral to confidentiality, authentication, message integrity, nonrepudiation, etc.

**Basic Concepts**:
  - **Purpose**: Allows a sender to disguise data to prevent information interception by intruders.
  - **Receiver's Role**: Must be able to recover original data from the disguised data.
  - **Terminology**:
    - **Plaintext/Cleartext**: Original message (e.g., “Bob, I love you. Alice”).
    - **Ciphertext**: Encrypted, unintelligible message to intruders.
    - **Encryption Algorithm**: The known, published method for encoding data (e.g., [RFC 1321; RFC 3447; RFC 2420; NIST 2001]).
    - **Keys**: Secret information preventing intruders from decrypting data.

**Encryption and Decryption Process**:
  - **Encryption**:
    - Sender (Alice) provides a key (KA) to the encryption algorithm.
    - Algorithm takes the key and plaintext message (m) to produce ciphertext (KA(m)).
  - **Decryption**:
    - Receiver (Bob) provides a key (KB) to the decryption algorithm.
    - Algorithm takes the ciphertext and Bob’s key to produce the original plaintext (KB(KA(m)) = m).

**Key Systems**:
  - **Symmetric Key Systems**:
    - Both Alice and Bob use identical, secret keys.
  - **Public Key Systems**:
    - Uses a pair of keys: one public (known to everyone) and one private (known only to the owner).

### 8.2.1 Symmetric Key Cryptography

__Overview__
- **Cryptographic Algorithms**: Substitute plaintext with ciphertext to create encrypted messages.
- **Caesar Cipher**: Substitutes each letter in plaintext with a letter k positions later in the alphabet. Example: For k = 3, "bob, i love you. Alice" becomes "ere, l oryh brx. dolfh". Limited security with only 25 possible keys.
- **Monoalphabetic Cipher**: Each letter is uniquely substituted with another letter. More secure than Caesar cipher with 26! (≈10^26) possible pairings. Vulnerable to statistical analysis of letter frequency.
  ![[Pasted image 20240530151949.png|400]]

__Attack Scenarios__
1. **Ciphertext-only attack**: Intruder has only the ciphertext.
	- Uses statistical analysis to deduce plaintext.
2. **Known-plaintext attack**: Intruder knows some plaintext-ciphertext pairs.
	- Example: Knowing "bob" and "alice" appear in the text helps break the code.
3. **Chosen-plaintext attack**: Intruder can choose plaintext and obtain ciphertext.
	- Example: Encrypting "The quick brown fox jumps over the lazy dog" can break simple encryption schemes.

__Polyalphabetic Encryption__
- **Improvement**: Uses multiple monoalphabetic ciphers.
- **Example**: Alternates between two Caesar ciphers (k=5 and k=19) in a pattern. Example: "bob, i love you." becomes "ghu, n etox dhz".
  ![[Pasted image 20240530152017.png|400]]
- **Key**: Knowledge of the specific ciphers and the pattern used.

__Modern Symmetric Key Encryption__
__Block Ciphers__
- **Definition**: Encrypts message in k-bit blocks independently.
- **Example**: For k=3, maps 3-bit cleartext to 3-bit ciphertext.
  ![[Pasted image 20240530152038.png|400]]
- **Key Space**: For k=3, 8 possible inputs can be permuted in 8! (40,320) ways.
- **Brute-force Attack**: Feasible for small k but infeasible for larger k like 64 bits due to 2^k! possible mappings.

__Practical Block Ciphers__
- **Function**: Simulate randomly permuted tables using manageable size tables and permutations.
- **Example**: 64-bit block cipher breaks block into 8-bit chunks, processes each with a table, scrambles positions, and repeats.
- **Popular Ciphers**: DES (64-bit block, 56-bit key), AES (128-bit block, 128/192/256-bit keys).
- **Brute-force Attack**: Infeasible for large keys (e.g., 128-bit AES key).

__Cipher-Block Chaining (CBC)__
- **Problem**: Identical plaintext blocks produce identical ciphertext blocks.
- **Solution**: Introduce randomness to ensure different ciphertext blocks.
- **Example**: Using a random k-bit number r(i) for each block.
	- Encrypt: c(i) = KS(m(i) ⊕ r(i))
	- Decrypt: m(i) = KS(c(i)) ⊕ r(i)
- **Bandwidth Issue**: Transmitting random bits doubles required bandwidth.
- **CBC Mechanism**:
	1. Generate and send a random Initialization Vector (IV) in cleartext.
	2. Calculate c(1) = KS(m(1) ⊕ IV).
	3. For subsequent blocks, c(i) = KS(m(i) ⊕ c(i-1)).
- **Advantages**: Different ciphertext for identical plaintext blocks, minimal bandwidth overhead.
- **Example**: For a 3-bit block cipher, plaintext "010010010" and IV="001" produce ciphertext blocks "100", "000", and "101".

__Implications for Secure Protocols__
- Need a mechanism to distribute the IV from sender to receiver.
- Essential for protocols like PGP, TLS, and IPsec.

### 8.2.2 Public Key Encryption

![[Pasted image 20240530152105.png|500]]
__Introduction to Public Key Encryption__
- **Historical Context**:
	- Encrypted communication traditionally required a shared symmetric key.
	- Challenges included securely agreeing on the key, especially over a network.
	- Diffie-Hellman Key Exchange (1976) revolutionized secure communication, leading to public key cryptography.

__Concept of Public Key Cryptography__
- **Key Elements**:
  - Each party has a public key (KB+) available to everyone and a private key (KB-) known only to the owner.
  - Example: Alice encrypts a message (m) to Bob using Bob’s public key: KB+(m). Bob decrypts it with his private key: KB-(KB+(m)) = m.
  - Remarkable property: KB-(KB+(m)) = m and KB+(KB-(m)) = m.

__Authentication Concern__
- **Issue**: Public key cryptography does not inherently verify the sender's identity.
- **Solution**: Digital signatures bind the sender to the message (explored in Section 8.3).

__RSA Algorithm__
- **Founders**: Ron Rivest, Adi Shamir, Leonard Adleman.
- **Modular Arithmetic**:
	- Operations involve addition, multiplication, and exponentiation modulo-n.
	- Important identities: (a mod n)d mod n = ad mod n.

__RSA Key Generation__
1. **Choose Two Primes**: p and q.
2. **Compute**: n = pq and z = (p - 1)(q - 1).
3. **Select e**: A number less than n, relatively prime to z.
4. **Find d**: Such that ed mod z = 1.
5. **Public Key**: (n, e).
6. **Private Key**: (n, d).

__RSA Encryption/Decryption__
- **Encryption**: c = me mod n (Alice to Bob).
- **Decryption**: m = cd mod n (Bob decrypts).
  ![[Pasted image 20240530152146.png|400]]
  ![[Pasted image 20240530152202.png|400]]


__RSA Example__
- **Example Values**: p = 5, q = 7, n = 35, z = 24, e = 5, d = 29.
- **Message Encryption**: Example of letters 'l', 'o', 'v', 'e' encrypted and decrypted using RSA.

__Practical Considerations__
- **Large Primes**: Needed for security, e.g., product of p and q ~ 1024 bits.
- **Exponentiation**: Time-consuming, hence often used with symmetric key cryptography for large data.

__Session Keys__
- **Usage**: RSA used to encrypt a session key (KS), which is then used for symmetric key encryption of data.

__Why RSA Works__
- **Mathematical Basis**:
	- Encryption: c = me mod n.
	- Decryption: m = cd mod n.
	- Fundamental property: med mod n = m.
	- Proof: Uses modular arithmetic properties and the relationship ed mod z = 1.

__Security of RSA__
- **Basis**: Difficulty of factoring n into p and q.
- **Concerns**: Quantum computing may threaten RSA's security in the future, but practical implementation is still distant.

__Diffie-Hellman Algorithm__
- **Overview**: Another public-key algorithm used to establish symmetric session keys.
- **Limitation**: Cannot encrypt messages of arbitrary length, used for key exchange.

## 8.3 Message Integrity and Digital Signatures

**Overview**
- Focus on message integrity (message authentication), digital signatures, and end-point authentication.
- Importance: Verifying the sender and ensuring no tampering of messages.

**Message Integrity Problem**
- Example: Bob receives a message believed to be from Alice.
- Goals:
	1. Verify the message originated from Alice.
	2. Ensure the message was not tampered with.

### 8.3.1 Cryptographic Hash Functions

**Definition and Properties**
- Hash function: Computes a fixed-size string H(m) from input m.
- Required property: It is computationally infeasible to find two different messages x and y such that H(x) = H(y).

**Example and Limitations**
- Internet checksum and CRCs are simple but not suitable for security.
- Example: Simple checksums can lead to collisions (e.g., “IOU100.99BOB” and “IOU900.19BOB” have the same checksum).

**Advanced Hash Algorithms**
- **MD5**: Computes a 128-bit hash; involves padding, appending message length, initialization, and looping steps.
- **SHA-1**: Computes a 160-bit message digest; more secure due to longer output length.

### 8.3.2 Message Authentication Code (MAC)

**Concept**
- Combines message m with a shared secret s to create a MAC: H(m + s).
- Ensures message integrity without requiring encryption.

**Procedure**
1. Alice creates message m, concatenates s, and computes H(m + s).
2. Alice sends (m, H(m + s)) to Bob.
3. Bob computes H(m + s) and verifies it matches the received MAC.

**Standards**
- **HMAC**: Popular standard, uses MD5 or SHA-1, processes data and key twice through the hash function.

**Key Distribution**
- Shared authentication key distribution methods:
	- Physically visiting each router.
	- Encrypting the key with each router’s public key and sending it over the network.

### 8.3.3 Digital Signatures

**Purpose**
- Signatures authenticate the creator of a document and signify agreement with its contents.

**Mechanism**
- Uses public-key cryptography.
- Bob signs a document m using his private key: KB-(m).
- Verification: Alice uses Bob’s public key to check the signature.

**Efficiency**
- Signing the hash of a message (H(m)) rather than the entire message to reduce computational effort.

**Comparison with MACs**
- MACs: Use shared secret keys, no encryption.
- Digital signatures: Use private/public key pairs, more secure, involve PKI (Public Key Infrastructure).

**Public Key Certification**
- **Purpose**: Verify public key ownership.
- **Certification Authority (CA)** roles:
	1. Verify the entity’s identity.
	2. Issue a certificate binding the entity's identity to its public key.
- **Standards**: ITU X.509 and IETF RFC 1422.

**Example Scenario**
- **Pizza Prank**:
	- Trudy pretends to be Bob, uses her public key, and signs a message.
	- Alice mistakenly verifies the signature with Trudy’s public key.
	- Solution: Use CA-signed certificates to verify true public keys.

**Operational Procedure**
- Bob sends CA-signed certificate with his order.
- Alice verifies the certificate using the CA’s public key and extracts Bob’s true public key.

## 8.4 End-Point Authentication

**Definition**:
- End-point authentication: Process of one entity proving its identity to another over a network, e.g., a user to an e-mail server.
- Human analogy: Recognizing faces, voices, or customs officials checking passports.

**Purpose**:
- Authenticate a “live” party during communication.
- Different from verifying a message received in the past.

**Challenges**:
- Cannot rely on biometric information (visual appearance, voiceprint).
- Authentication relies on exchanged messages and data in an authentication protocol.
- Typically, an authentication protocol runs before other protocols (data transfer, routing, e-mail).

**Development of Authentication Protocols**:
- Stepwise development similar to reliable data transfer protocol development.
- Identifying and addressing flaws in successive versions.

__Authentication Protocol ap2.0__
**Scenario**:
- Alice authenticates herself to Bob.
- Simple method: Alice sends a message saying, “I am Alice”.

**Flaw**:
- No way for Bob to verify the sender’s true identity.
- Trudy (intruder) could impersonate Alice.

**Improvement**:
- Verify the source address on the IP datagram matches Alice’s well-known address.

**Flaw**:
- IP spoofing: Creating an IP datagram with Alice’s IP address is easy.
- Reliance on first-hop router configurations to prevent spoofing (not universally enforced).

__Authentication Protocol ap3.0__
**Classic Approach**:
- Use a secret password shared between Alice and Bob.
- Widely used in services like Gmail, Facebook, Telnet, FTP.

**Flaw**:
- Password sent unencrypted can be intercepted (e.g., on a LAN during Telnet login).
- Eavesdropping threat is real.

__Authentication Protocol ap3.1__

**Improvement**:
- Encrypt the password using a symmetric secret key (KA-B).
- Alice sends an encrypted password and “I am Alice” message to Bob.

**Flaw**:
- Vulnerable to playback attack: Trudy can record and replay the encrypted password.
- Encryption does not prevent reuse of the recorded message.

__Authentication Protocol ap4.0__

**Solution**:
- Use a nonce (a number used only once).
- Steps:
  1. Alice sends “I am Alice” to Bob.
  2. Bob sends a nonce, R, to Alice.
  3. Alice encrypts the nonce with the symmetric key (KA-B) and sends it back.
  4. Bob decrypts and verifies the nonce.

**Benefit**:
- Ensures Alice is live and knows the secret key.
- Nonce prevents replay attacks.

## 8.6 Securing TCP Connections: TLS

**TLS (Transport Layer Security)**:
  - Enhances TCP with security services: confidentiality, data integrity, and end-point authentication.
  - Standardized by IETF [RFC 4346].
  - Successor to SSL (Secure Sockets Layer) version 3, originally designed by Netscape.

**Importance and Usage**:
  - Broadly deployed, supported by all popular Web browsers and servers.
  - Used by major services like Gmail, Amazon, eBay, TaoBao.
  - Facilitates secure Internet commerce, handling transactions worth hundreds of billions of dollars annually.
  - Identified by URLs beginning with "https" instead of "http".

**Example**:
  - Bob visits Alice Incorporated’s site to buy perfume.
  - Bob enters personal information and payment details.
  - Risks without TLS:
    - **No confidentiality**: Intruder intercepts and uses Bob’s payment information.
    - **No data integrity**: Intruder alters the order details.
    - **No server authentication**: Bob could be tricked by a fraudulent site (e.g., Trudy masquerading as Alice Inc.).

**Provides**:
  - **Confidentiality**: Encrypts data to prevent interception.
  - **Data Integrity**: Ensures data has not been tampered with.
  - **Server Authentication**: Verifies the server’s identity to prevent impersonation.
  - **Client Authentication**: Verifies the client’s identity.

**Usage**:
  - Secures transactions over HTTP and other applications running over TCP.
  - Provides an API similar to TCP’s, enabling easy integration with applications.

**Developer's Perspective**:
  - Technically resides in the application layer.
  - Seen as a transport protocol that enhances TCP with security services.
  - Requires inclusion of SSL classes/libraries in the application.

### 8.6.1 The Big Picture

**Simplified Version of TLS ("almost-TLS")**:
- **Phases**: Handshake, Key Derivation, Data Transfer.
- **Participants**: Client (Bob) and Server (Alice), with Alice having a private/public key pair and a certificate.

__Handshake__
- **Steps**:
	1. Establish TCP connection.
	2. Verify Alice's identity.
	3. Send a master secret key to Alice.
- **Process**:
	- Bob sends a hello message after establishing a TCP connection.
	- Alice responds with her certificate containing her public key.
	- Bob generates a Master Secret (MS), encrypts it with Alice’s public key, and sends the Encrypted Master Secret (EMS) to Alice.
	- Alice decrypts the EMS with her private key to obtain the MS.
- **Outcome**: Both Bob and Alice know the master secret for this TLS session.

__Key Derivation__
- **Purpose**: Generate different cryptographic keys for encryption and integrity checking.
- **Keys Derived**:
	- **EB**: Session encryption key for Bob to Alice.
	- **MB**: Session HMAC key for Bob to Alice.
	- **EA**: Session encryption key for Alice to Bob.
	- **MA**: Session HMAC key for Alice to Bob.
- **Process**: Both Alice and Bob generate these keys from the MS.

__Data Transfer__
- **Purpose**: Secure data transfer using the derived keys.
- **Process**:
	- Data is broken into records.
	- HMAC is appended to each record for integrity checking.
	- Record + HMAC is encrypted and sent over TCP.
- **Integrity Check**:
	- Use of sequence numbers in HMAC calculations to prevent reordering or replaying segments.
- **Potential Issues**: Without sequence numbers, a woman-in-the-middle attack could reorder segments, affecting the data integrity.

**TLS Record Structure**:
- **Fields**:
	- **Type Field**: Indicates if the record is a handshake message or application data.
	- **Version Field**: Specifies the version of TLS.
	- **Length Field**: Used to extract TLS records from the TCP byte stream.
	- **Data Field**: Contains the actual data.
	- **HMAC Field**: Ensures the integrity of the record.

**Sequence Numbers in TLS**:
- **Function**: Prevent attacks by ensuring the correct order of records.
- **Process**:
	- Sequence numbers are not included in the record but are used in HMAC calculations.
	- Bob maintains a sequence number counter and includes the sequence number in the HMAC calculation.
	- Alice tracks the sequence numbers to verify the data integrity.

### 8.6.2 A More Complete Picture

__TLS Handshake__
- **Overview**:
	- TLS allows Alice and Bob to agree on cryptographic algorithms at the start of the session during the handshake phase.
	- Nonces are exchanged to create session keys.
- **Steps**:
	1. **Client Sends**:
		- List of supported cryptographic algorithms.
		- Client nonce.
	2. **Server Chooses and Sends**:
		- Chosen symmetric algorithm (e.g., AES), public key algorithm (e.g., RSA), HMAC algorithm (e.g., MD5 or SHA-1).
		- Certificate and server nonce.
	3. **Client Verifies and Sends**:
		- Verifies the server’s certificate.
		- Extracts server’s public key.
		- Generates Pre-Master Secret (PMS).
		- Encrypts PMS with server’s public key and sends it to the server.
	4. **Both Compute Master Secret (MS)**:
		- Independently compute MS from PMS and nonces.
		- MS is used to generate encryption and HMAC keys, and Initialization Vectors (IVs) for CBC mode.
		- All subsequent messages are encrypted and authenticated.
	5. **Client Sends**:
		- HMAC of all handshake messages.
	6. **Server Sends**:
		- HMAC of all handshake messages.
- **Tampering Protection**:
	- Steps 5 and 6 prevent tampering with the handshake process.
	- Ensures the integrity of the algorithm selection process by comparing HMACs.
- **Nonce Use**:
	- Prevents "connection replay attack" where an attacker replays a previous session's messages.
	- Ensures different encryption keys for each session.

__Connection Closure__
- **Issue**:
	- Terminating the session with a simple TCP FIN could allow a truncation attack, ending the session prematurely.
- **Solution**:
	- Use a TLS type field to indicate session termination.
	- Authenticated by HMAC to ensure the closure message is legitimate.
	- Alerts the receiver to suspicious activity if a TCP FIN is received before a closure record.

