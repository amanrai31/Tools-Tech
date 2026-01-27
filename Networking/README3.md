# Everything host do to speak on internet

This lesson will illustrate two scenarios

- Hosts connected directly to each other (Hosts communicating on same network)
- Hosts connected on the opposite side of router(through router) => (Hosts communicating on diff network)

### 1. Host A & B are directly connected

- Both hosts have NIC so a MAC Address
- Both hosts are configured with an IP address && Subnet Mask(Size of a subnet network)

- Host A has some data to send to HOST B
- HOST A knows the IP address of HOST B (ping 10.1.1.2) OR maybe through DNS
- HOST A knows 10.1.1.2(HostB's IP) is in its own IP Network (HOST A can determine this by looking at it's own IP & Subnet Mask)
- Host A can create the L3 header to attach to data(End to end delivery i.e. IP)
- HOST A does not know HOST B's MAC Address

- HOST A uses ARP(ADDRESS RESOLUTION PROTOCOL) to resolve target's MAC Address - ARP request ask for MAC address associated with target IP(ARP request includes sender's MAC address & sender's IP, ARP request is a Broadcast i.e. it is send to everyone on network || to deliver packet to every MAC addr ffff.ffff.ffff is used as default MAC)

- ARP Mapping are stored in an **ARP cache** (Receiver learns(make this cache) from sender's ARP request which had sender's IP & MAC)

- HostB responds by sending an ARP response(Unicast i.e. directly to HostA). HostA populates it's ARP cache with HostB IP/MAC mapping

- Now HostA has HostB's IP & MAC mapping, it creates L2(hop2hop) & DATA is sent to HostB

- If HostB has to communicate than HostB's ARP cache is already populated so HostB can directly send response to HostA

**NOTE :** Anything having IP has an **ARP Cache**

### 2. Host A & C are connected on Internet (HostA-----Router-----HostB)

- HostA, HostC, and the Router have MAC and IP addresses
- HostA has some data to send to HostC, HostA   knows the IP of HostC(Provided by user or Application)
- HostA knows that HostC's IP address is on foreign network(By looking at it's own IP and Subnet mask)
- HostA create a L3 header(End2End), HostA needs to create a L2 header(Hop2Hop & next Hop is router)
- Router's IP addr is configured in HostA as default gateway (So using ARP, HostA have to find MAC of Router)

**NOTE:** When you connect to internet, 3 things are configured, 1. IP Addr || 2. Subnet Mask || 3. Default Gateway

- HostA shoot a brodcast, & when response come from Router then HostA make it's ARP cache mapping. Now HostA have L2 Headers too.

- Now data is sent by HostA to Router. Now router discard L2 layer and router add new L2(Hop to Hop) Layer

-----

HostA first step when sending data is always the same. So it determines if target IP is on **Local** or **Foreign**

- Foreign - ARP for a Deafault Gateway
- Local - ARP for Target IP directly



