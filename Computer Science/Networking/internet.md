---

---
#cs161

At a high level, the internet is a global [[network]] of computers that can send data between browsers and servers that are connected to it.

## open systems interconnection
The internet is design using the **Open Systems Interconnection Model**, a layered architecture that relies on abstraction at each level. It is a 7-layer model, but layers 5 and 6 aren't used in the real world, so we ignore them.
#### 1. physical layer
The **physical layer** encodes bits to send them over some physical pathway, from one machine to another. This data can be send as electric voltages, photon intensities, or any physical medium.
#### 2. link layer
The **link layer** encodes messages into groups of bits called *frames*. The physical layer can then send each frame one at a time. A frame consists of at least three things:
- *Source*: who is sending the message
- *Destination*: where the message is being sent
- *Data*: what is being sent
**Ethernet** and **WiFi** are both common second-layer protocols that connect machines in a local network.

>[!info] Local Area Network (LAN)
>A LAN is a set of physically-linked computers on a shared network. These are very basic examples of networks, which constrain machines to being in the same physical location. LANs only require the first two abstraction layers of the OSI model.

The link layer uses *48-bit, 6-byte* **MAC addresses** to uniuely identify machines on the same local network. MAC addresses are typically written as 6 pairs of hex numbers, each separated by a colon (ex. `ca:fe:f0:0d:be:ef`). 
#### 3. network layer
The **network layer** is what enables multiple local networks to communicate with one another. Local networks are most of the time connected to a **router**, which allows for global addressing. The network layer sends encoded frames, known as *packets*, from any device to any other device.

$$\max \mathbb{P}[r_0, \dots, r_{N-1}, c_0, \dots, c_{N-1}, p_0, \dots, p_{N-1}]$$
The network layer uses *32-bit, 4-byte* **IP addresses** to uniquely identify all machines globally. These addresses are typically represented as 4 integers between 0 and 256 (ex. `128.32.131.10`), but more recent versions of the network layer protocol have expanded to 128-bit addresses to accomodate the growing size of the internet.

>[!tip] Address Resolution Protocol
>The ARP Protocol translates Layer 3 IP addresses into Layer 2 MAC addresses. The protocol itself does not ensure authenticity, which makes it vulnerable to spoofing (a type of man-in-the-middle attack). To protect against that, we can uses **switches**, which [[cache]] IP -> MAC address pairings, and returns the cached value for known IP addresses instead of broadcasting the packet to the entire network.

#### 4. transport layer
The transport layer solves a few problems presented by IP addresses in the network layer:
- IP addresses uniquely identify machines, but can't differentiate between multiple processes running on the same machine on the same network (browser tabs/windows)
- The IP protocol is a *best effort protocol*, meaning that packets can still get dropped or corrupted
The transport layer introduces *16-bit* **port numbers** to help. These addresses are specific to a single machine, and are used together with the IP address to pinpoint the exact destination point.

###### transmission control protocol
TCP ensures the reliability of transmitted data. It uses a three-way handshake to establish connections. 
###### user datagram protocol
UDP is an alternative to TCP--it is a connectionless protocol that prioritizes speed over reliability. This is preferable in real-time use cases such as gaming or streaming where some packet loss is acceptable.

###### transport layer security
TLS protocol is the sub-layer that ensures **end-to-end** security between the transport layer and the 7th layer. It ensures that even if part of the communication channel is compromised, only the sender and receiver are able to read or modify data.

Some examples of TLS applications include, **HTTPS**—which is HTTP with TLS—and **VPN**—virtual private network connections. 

#### 7. application layer
The application layer is what actually allows users to interact with applications and services on the Internet. Any type of web-based browsing, messing, gaming, or calling employs the application layer.

---
# dns
The **Domain Name System**, DNS, is the common method for indexing human-readable domains to their IP addresses.
#### dns hierarchy
Recall the structure of a domain. These are all examples of domains:
- `www.google.com`
- `eecs.berkeley.edu`
- Top-level domains: `.com`, `.net`, `.edu`, etc.
- Root server: `.`

In a web browser, users query resources (e.g. webpages) using their domain names. The **recursive DNS resolver** is the computer that responds to client requests by making requests starting from the top-level domain (TLD) all the way until it reaches the **authoritative nameserver**, which gives the definitive IP address of the requested resource.
#### dns records
DNS servers store information in the form of **DNS records**. These records are essentially a series of text files written in DNS syntax about a particular domain, including its corresponding IP address. It also includes a **time-to-live** (TTL) field, indicating how often that record is refreshed. Common types of DNS records include
- **A**: holds the IPv4 address of the domain
- **AAAA**: holds the IPv6 address of the domain
- **CNAME**: "canonical name", forwards one domain to another (used for aliasing)
- **NS**: "name server", stores the authoritative nameserver of where to find the IP




