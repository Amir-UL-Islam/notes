Network protocols are sets of rules or standards used by devices to communicate with each other over a network.
- HTTP, used for web browsing
- SMTP, used for email
- FTP, used for file transfers


Network protocols can be broadly categorized into "layers". Each layer relies on the layer below it and provides services to the layer above it.
![[Screenshot 2025-03-01 at 3.59.41 PM.png]]
**Link Layer:**
It is responsible for sending data over a physical medium, such as a cable or a wireless connection. Like:
- Bluetooth
- Wifi
- Entranet

**Internet Layer**
It is responsible for routing data across different networks to get it to the right destination.
The Internet Layer relies on services provided by the Link Layer.

The fundamental protocol in **Internet Layer** is the Internet Protocol (IP). But there are others too:
- ICMP, used by programs like **`ping`** to test connectivity
- ARP, used to map IP addresses to MAC addresses

**Transport Layer**
This layer's job is to provide reliable data transfer between two devices.
The Transport Layer relies on services provided by the Internet Layer.

The most commonly used Transport Layer protocols are:
- TCP, for reliable delivery of data
- UDP, for fast but less reliable delivery.(It doesn't try to retransmit lost packets like TCP, which could cause delays.)
There are a few other not so popular ones too (like RUDP, DCCP etc.), but TCP & UDP are the most common ones.

**Application Layer**
This is the top-most layer, where most of the actual applications that we use live.
The Application Layer relies on protocols like TCP/UDP in the Transport Layer.
HTTP, SMTP, FTP etc. are all Application Layer protocols.

### **TCP An Overview**
TCP is a widely used network protocol. It's a "reliable" protocol that runs on top of an unreliable protocol: IP, short for Internet Protocol.

Before TCP was invented, the **Transport Layer** relied on simpler protocols, mainly **NCP (Network Control Program)** in the ARPANET, and **raw IP (Internet Protocol)**. Here’s how it worked and how you can simulate it:

**IP - The Internet's postal service**
When a program sends data over the network using IP, the data is broken up and sent as multiple "packets".

Each packet contains:

- a header section
- a data section

The header contains a source and destination address, much like an envelope that you send through your local postal service.

The important similarity between IP and a postal service is that packets are **not guaranteed** to arrive at the destination. Although every effort is made to get it there, sometimes packets get lost in transit.

Furthermore, if you send 5 packets at once, there's no guarantee that they'll arrive at their destination at the same time or in the same order.

## TCP's Guarantees

Primarily, TCP offers two guarantees: **(a)** Reliable delivery of packets and **(b)** In-order delivery of packets.

**Guarantee #1 - Reliable Delivery**
TCP ensures that no packets are lost in transit. It does this by asking the receiver to acknowledge all sent packets, and re-transmitting any packets if an acknowledgement isn't received.![[Screenshot 2025-03-05 at 11.39.07 PM.png]]
**Guarantee #2 - Ordered Delivery**
In addition to guaranteeing packets reach their destination, TCP also guarantees that the packets are delivered in order. **It does this by labelling each packet with a sequence number.** The receiver tracks these numbers and reorders out-of-sequence packets. If a packet is missing, the receiver waits for it to be re-transmitted.![[Screenshot 2025-03-05 at 11.44.15 PM.png]]
 **TCP Connections**
 TCP is a connection-oriented protocol, which means that to interact over TCP a program must first "establish a connection". To do this, one program takes the role of a "server", and the other program takes the role of a "client".
![[Screenshot 2025-03-07 at 11.32.50 PM.png]]
 Once a connection is established, the client & server can both receive and send data (it's a two-way channel).

**Why is TCP bidirectional?**
- TCP uses **separate send (TX) and receive (RX) buffers** to handle data flow in both directions.
- Each side of the connection can send packets independently, and **TCP ensures reliable delivery using sequence numbers and acknowledgments**

A TCP connection is identified using a unique combination of four values:

- destination IP address
- destination port number
- source IP address
- source port number

If your browser opens multiple connections to Google's server, only the "source port number" will change, the rest will remain the same.

 **TCP Handshake**
The TCP handshake is how clients establish connections with servers. This is a 3-step process.

**Step 1: SYN**
First, the client initiates the connection by sending a SYN (synchronize) packet to the server, indicating a request to establish a connection. This packet also contains a sequence number to maintain the order of the packets being sent.

**Step 2: SYN-ACK**
The server, upon receiving this SYN packet, sends back a SYN-ACK (synchronize-acknowledge) packet.

**Step 3: ACK**
In the final step of this three-way handshake, the client acknowledges the server's SYN-ACK packet by sending an ACK (acknowledge) packet. The connection is considered established once this last packet is received by the server.