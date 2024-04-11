
Lecture notes from Introduction to Computer Networking taught by  - KAIST

### Introduction - 29 Feb 24
Internet: computer network that interconnects computing devices around the world
![[Pasted image 20240229140039.png|400]]

| Network End                           | Network Core                                            |
| ------------------------------------- | ------------------------------------------------------- |
| Device that uses the network          | Interconnected routers                                  |
| enterprise network, home network, ... | national, global, local, regional ISP(KT,SKT,LG U+,...) |

KAIST: enterprise network
Data center networks: high-bandwith links(10-100Gbps)

Packet: segments of data with header bytes
Protocol: Format and order of messages exchanged between multiple network entities and action taken on transmission or receipt

#### 05 Mar 24
 Network core functions
 1. Forwarding: local action, moving packets from input to output (action)
 2. Routing: global action, determine packet destination (decision)

Packet switching: store and forward
- Packets are transmitted after it is fully stored
- Does not send the packet data while receiving it

Packet Queuing & loss
Why do we need Queue?
- If packet arrival speed > output speed: the packets needs to be stored in the router
Package loss
- If queue is full we cannot store more packets $\rightarrow$ package disappears

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

__Network of Networks__
![[Pasted image 20240305135554.png|500]]
Tier 1 ISP: ISP that has international coverage (AT&T, NTT, ...)
Regional ISP: ISP that has regional coverage (SKT, KT, LG U+, ...)
Content provider networks: Google, ...

__Delay__
- Processing Delay: time required to examine the packet's header and determine where to direct the packet
- Queuing Delay: Time required for waiting to be transmitted
- Transmission Delay: Time required to push all the packet's bits into the link: $\frac{\text{Packet size}}{\text{Transmission rate}}$
- Propagation Delay: Time required to get to the target router: $\frac{\text{Length}}{\text{Speed of light}}$
