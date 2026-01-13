# OSI Model

**Purpose of Networking :** Allow 2 hosts to share data with one another.

**Host must follow a set of rules like any language has some set of rules while communicating**

Like Human body is made up of various systems (Skeletal, Respiratory, Nervous, Cardiovascular, Muscular etc.), similarly OSI model divides rules of networking into 7 layers(if all layers are functioning, host can share data)

### 1. Physical Layer (Transporting bits)

Computer data exists in form of Bits(1's & 0's), something has to transport those bits between hosts. E.G. Ethernet cable, coaxial cable, fiber cable, WiFi, Repeaters, Hub.

### 2. Data Link (Hop to Hop delivery)

It interacts with the wire (Puts bits on the wire || retrive bits from wire). E.G. => NIC(Network interface Card), Wi-Fi access cards, Switches 

NIC to NIC (Hop to Hop) communication is enables using **MAC Address** of computer's NIC

**MAC Address :** It is 48 bits, represented as 12hex digits.

Here is same MAC addr which is displayed in 2 diff ways => 94-65-9C-3B-8A-E5(Window) || 94:65:9C:3B:8A:E5(Linux) || 9465.9C3B.8AE5(CISCO- router & switches)

=> When data is transferred from one Host to another Host, it goes through various routers in between, so the data contains IP of source & Destination Hosts(for End2End comm via IP) & data has also info of source Hop & next immediate destination Hop(Hop to Hop comm via MAC). When data packet reach from source hop to 1st router in the way, it drops the source's MAC & carry Router1 MAC(as source) & next router's MAC(as destination). 

### 3. Network (End to End delivery)

Addressing Scheme - IP addresses(32 bits). L3 Technologies: Routers, Hosts(Anything with an IP)

**NOTE :** Both IP & MAC addresses servers diff purposes, but together Layer2(Data Link) & Layer3(Network) is combinely called - **ARP(Address Resolution Protocol)**
