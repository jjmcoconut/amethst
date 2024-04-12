
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