## 📚 Table of Contents
- [Network \& Protocols](#network--protocols)
  - [Network Models](#network-models)
  - [Addresses](#addresses)
  - [Processes](#processes)
  - [Protocols](#protocols)
    - [Layer 2 (Data Link)](#layer-2-data-link)
    - [Layer 3 (Network)](#layer-3-network)
    - [Layer 4 (Transport)](#layer-4-transport)
    - [Layer 5-7 (Application)](#layer-5-7-application)
      - [Remote Access](#remote-access)
      - [Network Services](#network-services)
      - [Web](#web)
      - [File / Email Transfer](#file--email-transfer)
  - [Routing Algorithms](#routing-algorithms)

# Network & Protocols

## Network Models

- **OSI Model (Open Systems Interconnection)**: theoretical framework for computer network comms
  - *Please Do Not Touch Sam's Private Area.*
    1. **Physical Layer** - physical connection between devices
        - e.g. cables
    2. **Data link layer** - data transfer protocol between adjacent nodes
        - network segment: a group of networked devices using a shared medium / channel of comms
        - e.g. Ethernet, WiFi
    3. **Network layer** - logical addressing & routing between networks
        - e.g. IP, ICMP, VPN protocols (IPSec, SSL/TLS)
    4. **Transport layer** - comms between running apps on different hosts
        - end-to-end comms & data segmentation
        - e.g. TCP, UDP
    5. **Session layer** - establishing, maintaining & syncing comms between apps on different hosts
        - e.g. NFS, RPC
    6. **Presentation layer** - data encoding, compression, & encryption for Layer 7 to understand
        - e.g. ASCII / Unicode
    7. **Application layer** - provides network services to end-user apps
        - e.g. HTTP, FTP, DNS, POP3, SMTP, IMAP

- **TCP/IP** (Transmission Control Protocol / Internet Protocol) Model
  - allows a network to function with parts out of service
  - maps to the OSI model:
    2. (Data) Link Layer
    3. Internet (Network) Layer
    4. Transport Layer
    5,6,7. Application Layer

## Addresses


- **IP Address**
  - IPv4: most common, default
  - 4 octets, each 8 bits (0~255)
    - x.x.x.0 reserved for network address
    - x.x.x.255 reserved for broadcast address (targets all hosts on network)
  - **subnet mask** of 255.255.255.0 can be written as /24 (leftmost 24 bits of the IP doesn't change across the subnet)
  - **Private addresses** - isolated from the outside world; to access Internet the router must have a public IP addr and support [**NAT** (Network Address Translation)](#nat-network-address-translation)
    - 10.0.0.0 ~ 10.255.255.255 (10/8)
    - 172.16.0.0 ~ 172.31.255.255 (172.16/12)
    - 192.168.0.0 ~ 192.168.255.255 (192.168/16)

- **MAC address (Media Access Control)**
  - 6 bytes hexadecimal
  - Ethernet / WiFi addresses
  - first three - vendor who build the network interface
  - last three - unique address of the network interface

- **Port number**
  - 2 octets
  - port 0 is reserved


## Processes

- **Routing**
  - functions at layer 3
  - inspects IP addr, forwards packet to the best network (router) so packet gets closer to destination
  - see [routing algorithms](#routing-algorithms)

- **Encapsulation**
  - the process of every layer adding a header / trailer to the received unit of data and sending the encapsulated unit to layer below
    1. Transport layer adds TCP / UDP Header to application data, creating a TCP segment / UDP datagram
    2. Network layer adds IP header
    3. Data link layer adds proper Ethernet / WiFi header & trailer (frame)


## Protocols

### Layer 2 (Data Link)

- **ARP (Address Resolution Protocol)**
  - allows translation from layer 3 to 2 addressing
  - makes it possible to find MAC addr of another device on the Ethernet
    - originally Ethernet packets need MAC addr as destination & src
  - machine sends ARP request from MAC addr to broadcase MAC addr, to ask for the other to respond with its MAC addr
  - not encapsulated within UDP or IP packet; directly encapsulated within Ethernet frame

### Layer 3 (Network)

- **ICMP (Internet Control Message Protocol)**
  - network diagnostics & error reporting
  - commands that use ICMP
    - `ping` uses ICMP; measures round-trip time (RTT)
    - `traceroute` (linux) / `tracert` (Windows) uses ICMP to discover route from host to target; requires TTL field to become 0

- **NAT (Network Address Translation)**
  - uses one public IP addr to provide access to many private IP addrs
  - routers supporting NAT needs to track ongoing connections, & maintain a table translating network addrs between internal (generally private) & external (generally public) networks

### Layer 4 (Transport)

- **UDP (User Datagram Protocol)**
  - allows reaching to specific processes on target host
  - connectionless protocol operating 
  - layer 4 (transport layer)
  - 65,536 ports
  - does not even know if the packet has been delivered
  - a UDP data unit that encapsulates the app data is a *UDP datagram*.

- **TCP (Transmission Control Protocol)**
  - connection-oriented (required TCP connection) transport protocol
  - layer 4
  - 65,536 ports
  - each data octet has a sequence number - receiver can identify lost / duplicated packets, and acknowledge reception by specifying last received octet
  - TCP Connection
    - requires a **three-way handshake**
    1. *SYN Packet*: client initiates connection by sending SYN packet to server, containing client's random initial sequence number
    2. *SYN-ACK Packet*: server responds to SYN Packet with SYN-ACK, adds server's random initial sequence number 
    3. *ACK Packet*: client sends ACK Packet to acknowledge reception of SYN-ACK
  - A TCP data unit that encapsulates the app data is a *TCP segment*.

### Layer 5-7 (Application)

#### Remote Access

- **SSH (Secure Shell)**: a cryptographic network protocol for secure communication between edvices
  - encrypts data using crypto algorithms (e.g. [AES](#aes-advanced-encryption-system)) when sent over a network (e.g. Internet)
  - often used when logging in remotely to a computer or server
  - for `ssh` command usage see [`ssh`](linux_notes.md#ssh)


- **TELNET (Teletype Network)**
  - a network protocol for remote terminal connection
  - can be used to connect to any server *listening on a TCP port number*
  - `telnet x.x.x.x [port]` connects to specific port
  - *Echo server* - listens on **port 7**, server echoes everything you send
  - *Daytime server* - listens on **port 13**, replies with current day and time
  - *Web server* - listens on **port 80**, serves web pages
    - `GET / HTTP/1.1` gets the host
    - `GET /web.html` gets the page

#### Network Services

- **DHCP (Dynamic Host Configuration Protocol)**
  - level 7  protocol that relies on UDP (**port 67** for server, **port 68** for client)
  - automated way to configure devices connected to the server
  - four steps (*DORA*):
    1. *Discover* - broadcases DHCPDISCOVER message seeking the local DHCP server if exists
        - sends to broadcast addr
    2. *Offer* - server responds with a DHCPOFFER message with an IP addr available for client to accept
    3. *Request* - client responds with DHCPREQUEST message indicating accepting the offered IP
    4. *Acknowledge* - server responds with DHCPACK to confirm the offered IP addr being assigned to client
        - client changes addrb from no IP configuration to accepted IP
  - DHCP provides
    - leased IP addr to access network resources
    - gateway to route packets outside local network
    - a DNS server to resolve domain names

- **DNS (Domain Name Server)**
  - layer 7
  - UDP **port 53**, TCP **port 53**
  - many types of DNS records
    1. A record: hostname -> one or more IPv4 addresses
    2. AAAA record: similar to A, but for IPv6
    3. CNAME (canonical name) record: domain name -> another domain name
    4. MX (mail exchange) record: specifies mail server responsible for handling emails for a domain
  - **WHOIS records** 
    - information of domain domain owners
    - can be looked up using `whois [url]`

#### Web

- **HTTP (Hypertext Transfer Protocol) / HTTPS**
  - relies on TCP, usually TCP **port 80** and 443, sometimes 8080 and 8443
  - designed to retrieve web pages

#### File / Email Transfer

- **FTP (File Transfer Protocol)**
  - TCP **port 21**
  - higher speed than HTTP when all conditions equal
  - `ftp [ip]` -> log in -> `type ascii` -> `ls` / `get file.txt` downloads file to root
  
- **SMTP (Simple Mail Transfer Protocol)**
  - TCP **port 25**
    - `HELO`/`EHLO` initiates SMTP session
    - `MAIL FROM: <user@client.thm>` specifies sender's email addr
    - `RCPT TO: <user@client.thm>` specifies recipient's email addr
    - `DATA` indicates beginning sending mail content
    - `.` send on newline to indicate end of email message

- **POP3 (Post Office Protocol v3)**
  - TCP **port 110**
  - designed to allow client to comm with a mail server & retrieve email - email client sends by SMTP and retrieves using POP3
  - attempts to minimize server storage as email is downloaded & deleted from remote server
    - `USER <username>` identifies user
    - `PASS <password>` provides user's password
    - `STAT` requests # messages & total size
    - `LIST` lists all messages & sizes
    - `RETR <message_number>` retrieves specified message
    - `DELE <message_number>` marks message for deletion
    - `QUIT` ends POP3 session & applies changes

- **IMAP (Internet Message Access Protocol)**
  - TCP **port 143**
  - allows synchronizing read, moved, & deleted messages; convenient for checking via multiple clients
    - `LOGIN <username> <password>` authenticates user
    - `SELECT <mailbox>` selects mailbox folder to work with
    - `FETCH <mail_number> <data_item_name>` e.g. `FETCH 3 body[]`
    - `MOVE <sequence_set> <mailbox>` moves specified message to another mailbox
    - `COPY <sequence_set> <data_item_name>` copies specified message to another mailbox
    - `LOGOUT` logs out

## Routing Algorithms

- **OSPF (Open Shortest Path First)**
  - has routers exchange updates about states of their connected links & networks
  - each router has complete map of network and determines the best routes

- **EIGRP (Enhance Interior Gateway Routing Protocol)**
  - Cisco proprietary routing protocol
  - allows routers to share info about networks they can reach & cost (bandwidth, delay, etc.)
  - routers use info to choose most efficient paths

- **BGP (Border Gateway Protocol)**
  - primary routing protocol on the Internet
  - allows ISPs exchange routing info & establish paths
  - ensures data is routed efficiently even between networks

- **RIP (Routing Information Protocol)**
  - simple protocol used often in small networks
  - routers share information about networks they can reach & number of hops (routers) required
  - each router builds a routing table and chooses routes with fewest hops

