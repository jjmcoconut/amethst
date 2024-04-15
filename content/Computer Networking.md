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

### 4.4 Generalized Forwarding and SDN
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