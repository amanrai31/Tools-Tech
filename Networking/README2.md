# OSI Model

**Purpose of Networking :** Allow 2 hosts to share data with one another. OSI or TCP/IP models are Internet communication model.

**Host must follow a set of rules like any language has some set of rules while communicating**

Like Human body is made up of various systems (Skeletal, Respiratory, Nervous, Cardiovascular, Muscular etc.), similarly OSI model divides rules of networking into 7 **LAYERS** (if all layers are functioning, host can share data)

### 1. Physical Layer (Transporting bits)

Computer data exists in form of Bits(1's & 0's), something has to transport those bits between hosts. E.G. Ethernet cable, coaxial cable, fiber cable, WiFi, Repeaters, Hub.

### 2. Data Link Layer (Hop to Hop delivery)

It interacts with the wire (Puts bits on the wire || retrive bits from wire). E.G. => NIC(Network interface Card), Wi-Fi access cards, Switches 

NIC to NIC (Hop to Hop) communication is enables using **MAC Address** of computer's NIC

**MAC Address :** It is 48 bits, represented as 12hex digits.

Here is same MAC addr which is displayed in 2 diff ways => 94-65-9C-3B-8A-E5(Window) || 94:65:9C:3B:8A:E5(Linux) || 9465.9C3B.8AE5(CISCO- router & switches)

=> When data is transferred from one Host to another Host, it goes through various routers in between, so the data contains IP of source & Destination Hosts(for End2End comm via IP) & data has also info of source Hop & next immediate destination Hop(Hop to Hop comm via MAC). When data packet reach from source hop to 1st router in the way, it drops the source's MAC & carry Router1 MAC(as source) & next router's MAC(as destination). 

### 3. Network Layer (End to End delivery)

Addressing Scheme - IP addresses(32 bits). L3 Technologies: Routers, Hosts(Anything with an IP)

**NOTE :** Both IP & MAC addresses servers diff purposes, but they work together to move data across internet so L2(Data Link) & L3(Network) is combinely called - **ARP(Address Resolution Protocol)**

### 4. Transport Layer (Service to service delivery)

1. Distinguish data stream - We might be using browser, a chat application & a game on a host at the same time. L4 Makes sure that right program/application recives right data).

2. Addressing Scheme - PORTS. [0-65535 - for TCP] || [0-65535 - for UDP]. **TCP & UDP are 2 diff strategies to distinguish data Streams**

- TCP favors reliability - (Transmission Control Protocol)
- UDP favours efficiency - (User Datagram Protocol)

 **So every dataPacket/request append this information of PORTS too along with MAC & IP**

3. Servers listen for request to pre-defined Ports. (10.134.45.9:8000)- (IP+PORT)

4. Clients select **RANDOM PORT** (outbound intial packect) for each connection & response traffic will arrive on this exact same port. Client(1.1.1.1: 1000) ---> Server (10.134.45.9:8000), server will send response on client's PORT 1000


### 5. Session Layer, Presentation Layer, Application Layer

In modern evolution of OSI model, the distinction between these layers is somewhat vague
- Other networking models(like TCP/IP) combine these into one layer

-----

**Encapsulation start from Layer4 to Layer1 :** 
- At Layer4 PORT is added - Data + TCP/UDP PORT = Segment 
- At Layer3 IP is added - Segment + IP = Packet
- At Layer2 MAC Add is added - Packet + MAC = Frame
- At Layer1 => This frame is put on wire 

1. Network devices operate at specific layers

- L2 devices only look into the datagram upto L2 headers (Switches, NIC)
- L3 devices only look into the datagram upto L3 headers (Routers)

2. Network Protocols operate at specific layers

-----

- **Neither of these are strict rules** - Exceptions exists
- **OSI Model is simply a model** - not regid rules everythings adheres to. (Like modern routers are capable of performing L3 & L4 operations, similarly ARP can perform L2 & L3 operations)
  
