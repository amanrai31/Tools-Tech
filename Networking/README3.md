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

- ARP Mapping are stored in an ARP cache (Receiver learns(make this cache) from sender's ARP request which had sender's IP & MAC)

- HostB responds by sending an ARP response(Unicast i.e. directly to HostA). HostA populates it's ARP cache with HostB IP/MAC mapping

- Now HostA has HostB's IP & MAC mapping, it creates L2(hop2hop) & DATA is sent to HostB

- If HostB has to communicate than HostB's ARP cache is already populated so HostB can directly send response to HostA

### 2. Host A & B are connected on Internet







