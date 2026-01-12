# Networking

- [Resource](https://www.youtube.com/watch?v=H7-NR3Q3BeI&list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi&index=2)

## HOST, IP AND NETWORK

## Host 

Any device which sends or recives traffic(Data). [e.g computer, phone, server, IoT devices, printer, cloud servers]. Or in more simple terms - any device which is connected to internet is a host.

HOST is divided in 2 main categories - Client OR Server.

***Client -***  Device that initiates request.

***Server -***  Device that responds.

- ***Note -*** Client and server are relative terms that depend on specific communication. If the backend server made a request to database server, then the backend server is client here.

Every **HOST** on the internet has IP address. **IP is the  identity for each host on n/w.** When a data packet is send OR received, it has the source & destination IPs both.

## IP Address

IP Addr is 32 bits `01000101001010100011100010100101`, Containing 4 chunks `01000101`, `00101010`, `00111000`, `10100101` => `69`.`42`.`56`.`165`. Each with range 0-255 as 8bit min_value=0 & max_value=255. 

## Network(n/w) 

Host are connected to each other through n/w. Logical grouping of hosts that require similar connectivity. **Internet is just newtwork of networks**

**NOTE :** Before NETWORK transferring data literally required portable media (Disk, CD, penDrives etc)

**Hierarchically assigned IP (Subnet)** => Suppose there is an organization XYZ (having reserved ip starting like - 10.x.x.x), and it's newYork branch has IP which starts like(10.20.x.x) & Delhi IP like (10.30.x.x). Inside Delhi & NY we can have further hierarchies based on teams(sales, engineering). So if there is an IP like 10.30.55.125 - then we can say that this IP is of XYZ organisation(Delhi branch, engineering team(if .55 is assigned to Delhi's engineering team)). 

We can have nested networks (Subnet - Hierarchically assigned IP)
E.g. => An org > 3 diff offices at diff location > diff teams[hr, dev, finance] have own n/w.
- [Subnet](https://github.com/user-attachments/assets/89c79be0-6037-4d3f-bdbd-d56c9f6e96bf)

---

# [Switch, Router] & [Repeater,Hub and Bridge]

***Repeaters -*** It regenrates signals, NEED- allowing comm. across long distances.
***Hub -*** It is a multi-port repeater. NEED- Connecting hosts directly to each other does not scale, hub gives a centralized space for hosts to connect.





