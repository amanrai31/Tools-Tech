# Networking

- [Resource](https://www.youtube.com/watch?v=H7-NR3Q3BeI&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=2)

## HOST, IP AND NETWORK

## Host 

Any device which is connected to internet && sends or recives traffic(Data). [e.g computer, phone, server, IoT devices, printer, cloud servers].

HOST is divided in 2 main categories - Client OR Server.

***Client -***  Device that initiates request.

***Server -***  Device that responds.

- ***Note -*** Client and server are relative terms that depend on specific communication. If the backend server made a request to database server, then the backend server is client here.

Every **HOST** on the internet has IP address. **IP is the  identity for each host on n/w.** When a data packet is send OR received, it has the source & destination IPs both.

## IP Address

IP Addr is 32 bits `01000101001010100011100010100101`, Containing 4 chunks `01000101`, `00101010`, `00111000`, `10100101` => `69`.`42`.`56`.`165`. Each with range 0-255 as 8bit min_value=0 & max_value=255. 

## Network(n/w) 

Host are connected to each other through n/w. Logical grouping of hosts that require similar connectivity. **Internet is just newtwork of networks(Bunch of interconnected n/w)**

**NOTE :** Before NETWORK transferring data literally required portable media (Disk, CD, penDrives etc)

**Hierarchically assigned IP (Subnet)** => Suppose there is an organization XYZ (having reserved ip starting like - 10.x.x.x), and it's newYork branch has IP which starts like(10.20.x.x) & Delhi IP like (10.30.x.x). Inside Delhi & NY we can have further hierarchies based on teams(sales, engineering). So if there is an IP like 10.30.55.125 - then we can say that this IP is of XYZ organisation(Delhi branch, engineering team(if .55 is assigned to Delhi's engineering team)). 

We can have nested networks (Subnet - Hierarchically assigned IP)
E.g. => An org > 3 diff offices at diff location > diff teams[hr, dev, finance] have own n/w.
- [Subnet](https://github.com/user-attachments/assets/89c79be0-6037-4d3f-bdbd-d56c9f6e96bf)

------

# [Switch, Router] & [Repeater,Hub and Bridge]

1. **Repeaters :** It regenerates signals, NEED- allowing communication across long distances.

2. **Hub :** It is a multi-port repeater. NEED- Connecting hosts directly to each other does not scale, hub gives a centralized space for hosts to connect. Downside of hub => Every computer which are connected on n/w through this HUB receives everyone's else data 

3. **Bridges :** Bridges sit between Hub-connected hosts. Bridges only have 2 ports. Bridges learn which hosts are on each side of the bridge. 

4. **Switch :** It is combination of **HUB** & **BRIDGE**. It has multiple ports(unlike bridge), & it knows/learns which host are on each port. **Switches facilitate communication *within* a network**

5. **Router :** It facilitate communication **between** networks. All the host of classRoom A are on same n/w (So they talk to each other using switches) && All the hosts of classRoom B are on different networks(they comm with each other using switches). But if we want any HOST of ClassRoom-A to comm with any other HOST of classRoom-B we need **Router**(because they are on diff n/w)

**Router provides a traffic control point (Security, filtering, redirecting).** All the logical grouping of networks(known as routes) are stored in **Routing Table**

6. **GATEWAY :** Each host's way out of their local network. IP of a Host is 172.16.20.33 wants to comm with another HOST(172.16.30.x) which is on another network then the request must go through the router so the IP addr of that router is stored as that host's default gateway (could be like 172.16.20.1)











