# My Personal Notes: Network Communication and TCP Foundations

## Introduction

These are my personal notes on the network communication and TCP concepts I have studied so far.

I wrote them in simple first-person language so that when I return to them in the future, I can understand what I was learning without having to go through the original lessons again.

These notes cover what I have studied from the fundamentals of communication up to the TCP three-way handshake.

---

# 1. Fundamentals of Communication

## What communication means

I understand communication in networking as the transfer of information from one point to another.

The simplest communication model is:

**Sender → Channel → Receiver**

A more detailed model is:

**Source → Transmitter → Channel → Receiver → Destination**

The important thing for me to remember is that information does not travel through a network as an abstract idea. It has to be represented in some physical form.

For example:

- Copper uses electrical signals.
- Fiber uses optical signals.
- Wireless networks use electromagnetic radio signals.

## Data and signals

I need to keep **data** and **signals** separate.

Data is the information being communicated.

A signal is the physical representation used to carry that information.

A bit is not a physical object travelling through a cable or through the air. Bits are represented using physical signals.

My basic mental model is:

**Information → Data → Bits → Physical Signal**

At the receiving side, the process is reversed:

**Physical Signal → Bits → Data → Information**

## The complete communication path

A useful way for me to visualize networking is:

**Application data → TCP segment → IP packet → Ethernet/Wi-Fi frame → Physical signal**

At the receiving side, the process is reversed:

**Physical signal → Frame → IP packet → TCP segment → Application data**

This is one of the most important ideas I have learned.

## TCP and physical transmission

TCP does not directly transmit radio waves, electrical signals, or light.

TCP is a Transport Layer protocol.

The physical technology underneath TCP determines how the bits are actually transmitted.

Therefore, TCP itself does not have a specific operating frequency.

TCP traffic can travel over:

- 2.4 GHz Wi-Fi
- 5 GHz Wi-Fi
- 6 GHz Wi-Fi
- Cellular radio
- Ethernet
- Fiber

The frequency belongs to the underlying physical communication technology, not to TCP.

---

# 2. Frequency and the Electromagnetic Spectrum

## What frequency means

Frequency tells me how many cycles occur in one second.

The unit is Hertz, written as Hz.

**1 Hz = 1 cycle per second**

Common units are:

- kHz = thousands of cycles per second
- MHz = millions of cycles per second
- GHz = billions of cycles per second

For example:

**2.4 GHz = 2.4 billion cycles per second**

This does not mean 2.4 Gbit/s.

Frequency and bit rate are different measurements.

## Frequency and period

Frequency and period are related by:

**T = 1 / f**

Where:

- T = period
- f = frequency

Therefore, when frequency increases, the period becomes shorter.

## Frequency and wavelength

Frequency is also related to wavelength:

**λ = c / f**

Where:

- λ = wavelength
- c = speed of light
- f = frequency

Some approximate examples are:

| Frequency | Approximate wavelength |
|---|---:|
| 100 MHz | 3 m |
| 1 GHz | 30 cm |
| 2.4 GHz | 12.5 cm |
| 5 GHz | 6 cm |
| 6 GHz | 5 cm |

The basic relationship I need to remember is:

**Higher frequency → shorter wavelength**

## Electromagnetic spectrum

The electromagnetic spectrum can be viewed broadly as:

**Radio → Microwave → Infrared → Visible → Ultraviolet → X-ray → Gamma**

Networking technologies use particular portions of this spectrum.

Wi-Fi commonly uses the 2.4 GHz, 5 GHz, and 6 GHz ranges, subject to channel and regulatory requirements.

## Frequency band and bandwidth

I need to distinguish frequency from bandwidth.

A frequency identifies a particular rate of oscillation.

A frequency band is a range of frequencies.

For example:

**2.400 GHz to 2.420 GHz**

has a bandwidth of:

**20 MHz**

So I can think about it as:

**Frequency = where I am operating**

**Bandwidth = how wide the frequency range is**

Bandwidth can also be used in networking to describe communication capacity, so I need to pay attention to the context.

## Modulation

Bits need to be represented using a physical signal.

Modulation is the process of encoding information onto a carrier signal.

Modern wireless technologies use sophisticated modulation techniques, including QAM.

The important idea for me is:

**Bits are encoded onto a physical carrier so they can be transmitted through the communication medium.**

## Effects on wireless signals

Wireless signals can be affected by the environment.

Important effects include:

- Reflection
- Refraction
- Diffraction
- Absorption
- Scattering
- Attenuation
- Interference

These effects can influence signal quality and network performance.

I should avoid simplistic statements such as "2.4 GHz is always better than 5 GHz." Actual performance depends on factors such as distance, obstacles, interference, antennas, and the technology being used.

---

# 3. Bandwidth, Bit Rate and Network Performance

## Bandwidth

Bandwidth can have more than one meaning.

In the frequency-domain sense, bandwidth is the width of a frequency range.

In common networking discussions, bandwidth often refers to the capacity or maximum data rate of a connection.

I need to understand the context in which the word is being used.

## Bit rate

Bit rate tells me how many bits are transmitted per second.

For example:

**100 Mb/s = 100,000,000 bits per second**

Converting this to bytes:

**100,000,000 ÷ 8 = 12,500,000 bytes per second**

That is approximately:

**12.5 MB/s**

This is a theoretical rate. Actual application performance is usually lower because of overhead and network conditions.

## Throughput

Throughput is the actual rate at which data is successfully delivered.

So I distinguish:

**Bit rate = transmission rate**

**Throughput = actual successful delivery rate**

## Goodput

Goodput focuses on useful application-level data delivered.

Conceptually, it excludes protocol overhead and retransmitted data.

This explains why the useful rate experienced by an application can be lower than the advertised link rate.

---

# 4. Latency, RTT, Jitter and Packet Loss

## Latency

Latency is the delay involved in communication.

It can come from several sources:

- Propagation delay
- Transmission delay
- Processing delay
- Queuing delay

## Round-trip time

RTT means Round-Trip Time.

It is the time taken for communication to travel to the destination and for the corresponding response to return.

RTT is important when studying TCP because TCP operates across networks where communication takes time.

## Jitter

Jitter is variation in delay.

If packets experience different delays, the variation between those delays is jitter.

Jitter is especially important for applications that are sensitive to timing.

## Packet loss

Packet loss occurs when transmitted packets do not successfully reach their destination.

Possible causes include:

- Congestion
- Wireless interference
- Signal degradation
- Hardware problems
- Buffer overflow
- Routing problems

TCP has mechanisms for responding to problems such as loss. I have not yet studied those mechanisms in detail, so at this stage my main understanding is:

**Network problems → packet loss or delay → TCP observes the effects and reacts**

---

# 5. Shannon Channel Capacity

I learned the Shannon channel-capacity formula:

**C = B log₂(1 + S/N)**

Where:

- C = theoretical channel capacity
- B = bandwidth
- S = signal power
- N = noise power
- S/N = signal-to-noise ratio

The basic idea is that the theoretical capacity of a communication channel depends on both its bandwidth and its signal-to-noise conditions.

This helps me understand why increasing bandwidth is not the only factor that matters.

Signal quality also matters.

---

# 6. Bandwidth-Delay Product

The Bandwidth-Delay Product, or BDP, estimates how much data can be in transit on a network path at one time.

The formula is:

**BDP = Bandwidth × RTT**

Example:

**100 Mb/s × 0.1 seconds**

First:

**100 Mb/s = 100,000,000 bits/s**

Then:

**100,000,000 × 0.1 = 10,000,000 bits**

Converting to bytes:

**10,000,000 ÷ 8 = 1,250,000 bytes**

So the BDP is approximately:

**1.25 MB**

My simple mental model is:

**BDP ≈ amount of data that can be in flight across the path**

---

# 7. Networking Models

## Why networking uses layers

Networking is complicated, so responsibilities are divided into layers.

Each layer has its own responsibilities and interacts with the layers above and below it.

This makes networking easier to design, understand, troubleshoot, and standardize.

## OSI model

The OSI model has seven layers:

| Layer | Name |
|---:|---|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

The most important point for my TCP studies is:

**TCP operates at Layer 4, the Transport Layer.**

## Important layers

### Layer 4: Transport

TCP operates here.

TCP provides transport functions such as:

- Connection management
- Reliable delivery
- Ordered delivery
- Flow control
- Congestion control

### Layer 3: Network

IP operates here.

IP deals with logical addressing and routing packets between networks.

### Layer 2: Data Link

Ethernet and Wi-Fi operate at the data-link level.

This layer handles local-link communication and MAC addressing.

### Layer 1: Physical

The physical layer deals with the physical representation and transmission of bits.

Examples include:

- Electrical signals on copper
- Optical signals in fiber
- Radio signals in wireless networks

## TCP/IP model

A simplified TCP/IP model has four layers:

1. Application
2. Transport
3. Internet
4. Network Access

The rough mapping is:

**OSI Application + Presentation + Session → TCP/IP Application**

**OSI Transport → TCP/IP Transport**

**OSI Network → TCP/IP Internet**

**OSI Data Link + Physical → TCP/IP Network Access**

## Protocol stack example

A traditional HTTPS communication can be represented as:

**HTTPS → TCP → IP → Wi-Fi → Radio**

This shows that several protocols and technologies work together to move application data.

---

# 8. Encapsulation and Decapsulation

## Encapsulation

Encapsulation happens as data moves down the protocol stack.

Each layer adds information needed by that layer.

The simplified process is:

**Application data**

↓

**TCP header + application data = TCP segment**

↓

**IP header + TCP segment = IP packet**

↓

**Link header/trailer + IP packet = frame**

↓

**Physical layer = physical signal**

This is encapsulation.

## Decapsulation

At the destination, the reverse process occurs.

The physical signal is received and converted into bits.

The frame is processed.

The IP packet is processed.

The TCP segment is processed.

Eventually the application receives the relevant data.

This reverse process is called decapsulation.

## Segment, packet and frame

I need to remember:

**TCP → Segment**

**IP → Packet**

**Ethernet/Wi-Fi → Frame**

These terms describe data at different layers.

## Port, IP address and MAC address

These identify different things at different layers.

**Port**

Identifies a transport-layer endpoint or service.

**IP address**

Identifies a logical network endpoint.

**MAC address**

Is used for local link delivery.

I should not treat these as interchangeable.

## What happens across routers?

A Layer 2 frame is normally specific to a local link.

When traffic crosses a router, the Layer 2 frame is replaced for the next link.

The IP packet continues to be forwarded across the network, although some IP fields can change. For example, the IPv4 TTL is decremented, and NAT can alter addressing information.

The important idea is:

**The frame is local to a link, while the IP packet is used for communication across networks.**

## Wireshark and encapsulation

Wireshark can display the protocol layers of a captured packet.

A simplified view can look like:

**Frame → Ethernet II → IPv4 → TCP → TLS/Application Data**

This gives me a practical way to see encapsulation.

---

# 9. Introduction to TCP

## What TCP is

TCP means Transmission Control Protocol.

It is a transport-layer protocol that provides reliable and ordered communication between application endpoints across IP networks.

A definition I want to remember is:

> TCP is an end-to-end transport protocol that provides a controlled, ordered byte stream between application endpoints over an IP network using sequence numbers, acknowledgments, retransmissions, flow control and congestion control.

## Why TCP exists

IP does not guarantee that packets will arrive correctly.

Packets can potentially be:

- Lost
- Duplicated
- Reordered
- Delayed

TCP provides mechanisms above IP to deal with these problems.

## Main TCP responsibilities

The major responsibilities I have studied are:

1. Connection management
2. Reliable delivery
3. Ordered delivery
4. Flow control
5. Congestion control

I have not yet studied all of these mechanisms in detail.

## TCP is connection-oriented

TCP establishes a connection before normal application data exchange.

The basic connection-establishment process is:

**SYN → SYN-ACK → ACK**

This is the TCP three-way handshake.

## TCP is full-duplex

Once established, a TCP connection can carry data in both directions.

Each direction has its own sequence-number space.

## TCP is byte-stream oriented

TCP provides an ordered byte stream rather than preserving application messages as individual network messages.

This is why TCP sequence numbers relate to byte positions.

## TCP and IP are different

I need to keep this distinction clear:

**IP = logical addressing and packet forwarding**

**TCP = transport communication, reliability, ordering, flow control and congestion control**

TCP does not decide the network route.

## TCP is not encryption

TCP provides transport functions.

It does not automatically encrypt application data.

For example, HTTPS normally combines HTTP with TLS, while TLS provides cryptographic protection.

## Examples of TCP-based applications

Examples include:

- SSH
- HTTP
- HTTPS in traditional TCP-based deployments
- FTP
- SMTP
- IMAP
- POP3

---

# 10. TCP Ports, Sockets and Connections

## TCP ports

TCP ports are 16-bit numbers.

Therefore, the numerical range is:

**0 to 65535**

Traditional categories are:

| Range | Traditional category |
|---|---|
| 0–1023 | Well-known |
| 1024–49151 | Registered |
| 49152–65535 | Dynamic/private |

The exact ephemeral-port range can vary by operating system.

## Common TCP ports

| Port | Common association |
|---:|---|
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |

These are conventions.

A port number alone does not prove the application running on that port.

For example, port 443 is commonly associated with HTTPS, but another service could use it.

Therefore:

**Port number = clue, not absolute proof of application identity.**

## Client and server ports

A server normally listens on a known service port.

A client normally receives an ephemeral source port.

Example:

**192.168.1.20:52341 → 142.250.10.10:443**

Here:

- Client IP = 192.168.1.20
- Client port = 52341
- Server IP = 142.250.10.10
- Server port = 443

## Socket

A socket is an operating-system networking abstraction associated with a network endpoint, protocol, and connection state.

A useful simplified way for me to think about an endpoint is:

**IP address + port + transport protocol**

The exact meaning of "socket" depends somewhat on context, but it is more than simply a port number.

## TCP four-tuple

A TCP connection can be identified using four values:

**Source IP + Source Port + Destination IP + Destination Port**

Example:

**192.168.1.20:52341 → 142.250.10.10:443**

This allows many clients to connect to the same server port.

Thousands of clients can use server port 443 because their source IP addresses and/or source ports are different.

## Listening socket versus established connection

A server can have a listening socket on port 443 while also having many established TCP connections using destination port 443.

The listening socket waits for new connections.

Each established connection has its own connection context.

## NAT

Network Address Translation can change private IP addresses and port numbers as traffic passes through a NAT device.

Because of this, network investigations can sometimes require NAT translation logs to connect internal and external traffic.

## Open port does not automatically mean vulnerable

A scan can show that a port is reachable.

That does not automatically mean that the service is vulnerable.

The service, version, configuration, and security state still need to be investigated.

---

# 11. TCP Segment and Header

## TCP segment

A TCP segment consists of:

**TCP header + optional TCP payload**

The minimum TCP header is 20 bytes.

TCP options can make the header larger.

## Main TCP header fields

The fields I have studied include:

- Source Port
- Destination Port
- Sequence Number
- Acknowledgment Number
- Data Offset
- Reserved
- TCP Flags
- Window Size
- Checksum
- Urgent Pointer
- Options
- Padding

## Source and destination ports

These identify the TCP endpoints involved in the communication.

Example:

**Source Port = 52341**

**Destination Port = 443**

## Sequence number

The sequence number tracks the position of bytes in the TCP byte stream.

For example, if a segment starts at sequence number 1000 and carries 500 bytes, the next sequence position is:

**1500**

## Acknowledgment number

The acknowledgment number indicates the next byte expected by the receiver.

For example:

**ACK = 1500**

Conceptually means bytes through 1499 have been received in order and byte 1500 is the next expected byte.

## ACK flag versus acknowledgment number

I need to keep these separate.

The ACK flag indicates that the acknowledgment field is significant.

The acknowledgment number contains the actual value.

## Window size

The TCP window relates to flow control.

The receiver advertises how much data it can currently accept.

Two important concepts are:

**rwnd = receiver's advertised receive window**

**cwnd = sender's congestion window**

A simplified view of the sender's effective sending limit is:

**min(rwnd, cwnd)**

I have not yet studied the detailed congestion-control algorithms.

## Checksum

The TCP checksum is used to detect corruption.

It does not provide encryption.

Therefore:

**Checksum ≠ encryption**

## Data Offset

The Data Offset field tells TCP how large the TCP header is.

It is measured in 32-bit words.

This is necessary because TCP options can make the header larger than the basic 20-byte header.

---

# 12. TCP Options and MSS

TCP can include options in its header.

Examples include:

- MSS
- Window Scale
- SACK Permitted
- SACK
- Timestamps

I have encountered these options as part of understanding the TCP header and handshake, but I have not yet studied their mechanisms in depth.

## Maximum Segment Size

MSS means Maximum Segment Size.

It refers to the maximum amount of TCP payload that can normally be carried in one TCP segment.

MSS is different from MTU.

For example, with:

**IPv4 MTU = 1500 bytes**

and:

**IPv4 header = 20 bytes**

**TCP header = 20 bytes**

then:

**MSS = 1500 - 20 - 20 = 1460 bytes**

For IPv6 with a 1500-byte MTU and the basic 40-byte IPv6 header plus a 20-byte TCP header:

**MSS = 1500 - 40 - 20 = 1440 bytes**

These examples assume no additional headers affecting the calculation.

## MTU versus MSS

I need to remember:

**MTU = maximum IP packet size supported by a link**

**MSS = maximum TCP payload size in a segment**

They are related, but they are not the same measurement.

---

# 13. TCP Flags

TCP flags are control bits in the TCP header.

The important flags I have studied are:

- SYN
- ACK
- FIN
- RST
- PSH
- URG
- ECE
- CWR
- NS

## SYN

SYN means Synchronize.

It is used during TCP connection establishment and is associated with synchronizing sequence-number state.

## ACK

ACK indicates that the acknowledgment field is meaningful.

The actual acknowledgment value is stored in the acknowledgment-number field.

## FIN

FIN means Finish.

It indicates that one side has finished sending data in one direction.

It does not necessarily mean that the entire full-duplex connection immediately disappears.

## RST

RST means Reset.

It is associated with an abrupt termination or rejection of a connection.

A useful distinction is:

**FIN = graceful closing**

**RST = abrupt reset**

## PSH

PSH means Push.

It is associated with making received data available to the application promptly.

I should not remember it simply as "important data," because that is an oversimplification.

## URG

URG relates to the TCP urgent-pointer mechanism.

It is uncommon in modern application use.

## ECE and CWR

These flags are related to Explicit Congestion Notification, or ECN.

**ECE = ECN Echo**

**CWR = Congestion Window Reduced**

ECN can allow congestion information to be signaled using packet marking rather than relying only on packet loss.

## NS

NS is an older and less commonly encountered ECN-related flag.

## Multiple flags

TCP flags are not limited to one flag at a time.

Examples include:

**SYN**

**SYN + ACK**

**FIN + ACK**

**PSH + ACK**

**RST + ACK**

The combination of flags helps describe what is happening in the TCP communication.

## Flags and network analysis

Flags can provide useful evidence during traffic analysis.

However, I should not automatically interpret one flag pattern as proof of an attack or problem.

For example, repeated SYN packets could have several explanations:

- Normal retransmission
- Packet loss
- Network problems
- Scanning
- Service problems
- Firewall behavior
- SYN flooding

A flag is evidence that needs context.

---

# 14. TCP Three-Way Handshake

## Why the handshake exists

TCP establishes a connection before normal application data exchange.

The connection-establishment process uses three segments:

**SYN → SYN-ACK → ACK**

This is the TCP three-way handshake.

## Example

I can use this example:

**Client: 192.168.1.20:52341**

**Server: 192.168.1.10:443**

### Step 1: Client sends SYN

The client sends a TCP segment with:

**SYN**

**SEQ = 1000**

The client is requesting a TCP connection and is starting its sequence-number space at 1000 in this example.

### Step 2: Server sends SYN-ACK

The server responds with:

**SYN + ACK**

**SEQ = 5000**

**ACK = 1001**

The server is doing two things at the same time.

It is acknowledging the client's SYN and sending its own SYN.

The acknowledgment is 1001 because the SYN consumes one sequence number.

### Step 3: Client sends ACK

The client responds with:

**ACK**

**SEQ = 1001**

**ACK = 5001**

The client is acknowledging the server's SYN.

At this point, the TCP connection is established.

## Why SYN consumes one sequence number

A SYN represents connection-establishment state and consumes one sequence number.

Therefore:

**Client SYN at SEQ 1000 → next client sequence position = 1001**

Similarly:

**Server SYN at SEQ 5000 → next server sequence position = 5001**

A pure ACK normally does not consume a sequence number.

TCP data consumes sequence numbers according to the number of payload bytes.

FIN also consumes one sequence number.

## Handshake and TCP options

TCP options can be negotiated during the SYN exchange.

Examples include:

- MSS
- Window Scale
- SACK Permitted
- Timestamps

This means the handshake is not only about the SYN, SYN-ACK and ACK flags. It can also carry information used to establish characteristics of the TCP session.

---

# 15. Handshake Problems

## Lost SYN

If the client's SYN does not reach the server, the client can retransmit the SYN.

## Lost SYN-ACK

If the server's SYN-ACK does not successfully reach the client, the server can retransmit its SYN-ACK.

The important idea is that networks are not perfect, so TCP has mechanisms for dealing with communication problems.

I have not yet studied TCP retransmission mechanisms in depth.

## Connecting to a closed port

If a SYN reaches a host where no service is listening on the requested port, the host may respond with an RST instead of a SYN-ACK.

This tells the sender that the connection request was rejected or reset rather than established.

An RST should not automatically be interpreted as evidence of an attack.

---

# 16. Basic TCP States

I have learned a simplified view of the states involved in establishing a TCP connection.

For the client:

**CLOSED → SYN-SENT → ESTABLISHED**

For the server:

**LISTEN → SYN-RECEIVED → ESTABLISHED**

The client begins by sending a SYN and enters SYN-SENT.

The server is normally listening for incoming connections.

After receiving the SYN, the server responds with SYN-ACK and enters SYN-RECEIVED.

After the final ACK is received, the connection reaches ESTABLISHED.

I will study the complete TCP state machine later.

---

# 17. Viewing the Handshake in Wireshark

Wireshark can make the three-way handshake visible.

A basic handshake can appear as:

**[SYN]**

**[SYN, ACK]**

**[ACK]**

This gives me a practical way to connect the theory to actual network traffic.

When examining a capture, I can look at:

- Source IP
- Destination IP
- Source port
- Destination port
- Sequence number
- Acknowledgment number
- TCP flags
- TCP options

The important lesson is that Wireshark shows the actual protocol fields I have been studying theoretically.

---

# 18. Putting Everything Together

The concepts I have studied are connected.

A user starts with information in an application.

That information becomes application data.

TCP can process that data and add a TCP header.

The result is a TCP segment.

IP then adds its own information, producing an IP packet.

The link layer adds its own information, producing a frame.

The physical layer converts the bits into physical signals.

Depending on the technology, those signals may be:

- Electrical signals
- Optical signals
- Radio signals

In a Wi-Fi network, physical transmission can occur in a radio band such as 2.4 GHz, 5 GHz, or 6 GHz.

This is where the frequency concept connects to TCP.

The relationship is:

**Application data**

↓

**TCP**

↓

**IP**

↓

**Ethernet / Wi-Fi**

↓

**Physical transmission**

TCP is part of the communication stack, but it is not the physical radio technology.

## My complete mental model

The most useful mental model I have developed is:

**Information → Data → Protocol processing → Bits → Encoding/modulation → Physical signal → Medium → Physical signal → Decoding → Bits → Protocol processing → Data → Information**

This connects the physical networking concepts with the transport-layer concepts.

---

# 19. Important Distinctions I Need to Remember

## Frequency vs bandwidth

**Frequency** tells me how many cycles occur per second.

**Bandwidth** can describe the width of a frequency range or, in common networking usage, the capacity of a connection.

## Frequency vs bit rate

**Frequency ≠ bit rate**

2.4 GHz does not mean 2.4 Gbit/s.

## Bit rate vs throughput

**Bit rate** is a transmission rate.

**Throughput** is the actual successful delivery rate.

## Latency vs throughput

**Latency** is delay.

**Throughput** is the amount of data successfully delivered over time.

A network can have high throughput and high latency at the same time.

## TCP vs IP

**IP handles logical addressing and packet forwarding.**

**TCP handles transport-level communication and provides mechanisms for reliability, ordering, flow control and congestion control.**

## Port vs IP address

An IP address identifies a logical network endpoint.

A port identifies a transport-layer service or endpoint.

## Port vs socket

A port is a number.

A socket is an operating-system networking abstraction associated with an endpoint and connection context.

## Segment vs packet vs frame

**TCP → Segment**

**IP → Packet**

**Ethernet/Wi-Fi → Frame**

## MTU vs MSS

**MTU = maximum IP packet size on a link**

**MSS = maximum TCP payload size in a segment**

## ACK flag vs acknowledgment number

The ACK flag says that the acknowledgment field is meaningful.

The acknowledgment number contains the actual acknowledgment value.

## FIN vs RST

**FIN = graceful completion of sending in one direction**

**RST = abrupt reset**

## TCP and frequency

**TCP does not have a specific operating frequency.**

The underlying physical communication technology determines the frequency or physical transmission method.

---

# 20. My Current Understanding

At this stage, I understand TCP as one part of a much larger communication system.

I should not think about TCP as if it directly sends data through radio waves or cables.

I should think in layers.

The application creates information.

Protocols represent and process that information.

TCP provides transport-layer communication.

IP provides logical addressing and forwarding.

Ethernet or Wi-Fi handles local-link communication.

The physical layer carries the bits using electrical, optical, or electromagnetic signals.

This also explains why frequency is connected to TCP without frequency being a property of TCP itself.

For example, a TCP connection can travel over 5 GHz Wi-Fi.

The Wi-Fi transmission uses the 5 GHz radio band.

TCP is still operating at the Transport Layer.

The concepts are connected because TCP data is carried by the lower layers, but they are not the same thing.

---

# 21. Quick Review Questions

When I return to these notes later, I should be able to answer these questions without immediately looking at the answers.

## Communication

1. What is the difference between data and a signal?
2. How does information move from an application to a physical medium?
3. Why are bits not physical objects travelling through a network?

## Frequency

4. What is frequency?
5. What does 2.4 GHz mean?
6. How is frequency related to wavelength?
7. What is the difference between frequency and bandwidth?
8. What is modulation?
9. What physical effects can affect wireless signals?

## Network performance

10. What is the difference between bit rate and throughput?
11. What is latency?
12. What is RTT?
13. What is jitter?
14. What causes packet loss?
15. What does the Shannon capacity formula describe?
16. What is the Bandwidth-Delay Product?

## Networking models

17. What are the seven OSI layers?
18. Which OSI layer does TCP operate at?
19. Which layer does IP operate at?
20. What are Ethernet and Wi-Fi responsible for?
21. What is the TCP/IP model?

## Encapsulation

22. What is a TCP segment?
23. What is an IP packet?
24. What is a frame?
25. What happens during encapsulation?
26. What happens during decapsulation?
27. What is the difference between a port, IP address and MAC address?

## TCP

28. What does TCP provide?
29. Why is TCP connection-oriented?
30. What does full-duplex mean?
31. What does it mean that TCP is byte-stream oriented?
32. What is the TCP four-tuple?
33. What is a TCP port?
34. What is a socket?
35. Why does an open port not automatically mean that a service is vulnerable?

## TCP header

36. What is the purpose of the sequence number?
37. What is the purpose of the acknowledgment number?
38. What does the ACK flag mean?
39. What does the window field represent?
40. What does the TCP checksum do?
41. What is the Data Offset field?
42. What is MSS?
43. How is MSS different from MTU?

## TCP flags

44. What does SYN mean?
45. What does ACK mean?
46. What does FIN mean?
47. What does RST mean?
48. What are PSH and URG?
49. What are ECE and CWR related to?
50. Why can multiple TCP flags appear together?
51. Why should I avoid drawing conclusions from one flag pattern without context?

## Three-way handshake

52. What are the three steps of the TCP handshake?
53. Why does SYN consume one sequence number?
54. Why is the server's ACK number 1001 in my example?
55. Why does the client's final ACK acknowledge 5001?
56. What happens if the SYN is lost?
57. What happens if the SYN-ACK is lost?
58. What can happen when a SYN reaches a closed port?
59. What TCP options can appear during the handshake?
60. What basic TCP states are involved in establishing a connection?

## The most important question

**Does TCP have a specific operating frequency?**

My answer should be:

**No. TCP is a Transport Layer protocol. The underlying physical communication technology determines the frequency or physical transmission method.**

---

# Final Mental Picture

The simplest picture I want to remember is:

**Application**

↓

**TCP**

↓

**IP**

↓

**Ethernet / Wi-Fi**

↓

**Physical medium**

For wireless communication:

**TCP data → IP packet → Wi-Fi frame → Radio signal → Air**

And at the receiving side:

**Radio signal → Wi-Fi frame → IP packet → TCP segment → Application data**

TCP is therefore part of the transport process, while frequency belongs to the underlying physical communication technology.

The most important distinction for me is:

> **TCP does not operate at a particular frequency. TCP operates at the Transport Layer, while the underlying physical technology determines how the bits are physically transmitted.**

These notes represent my current understanding through the TCP three-way handshake.
