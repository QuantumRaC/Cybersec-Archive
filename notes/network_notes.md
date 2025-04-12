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
  - **Private addresses** - isolated from the outside world; to access Internet the router must have a public IP addr and support **NAT** (Network Address Translation)
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

- **Encapsulation**
  - the process of every layer adding a header / trailer to the received unit of data and sending the encapsulated unit to layer below
    1. Transport layer adds TCP / UDP Header to application data, creating a TCP segment / UDP datagram
    2. Network layer adds IP header
    3. Data link layer adds proper Ethernet / WiFi header & trailer (frame)

## Protocols

- **SSH (Secure Shell)**: a cryptographic network protocol for secure communication between edvices
  - encrypts data using crypto algorithms (e.g. [AES](#aes-advanced-encryption-system)) when sent over a network (e.g. Internet)
  - often used when logging in remotely to a computer or server
  - for `ssh` command usage see [`ssh`](linux_notes.md#ssh)

- **UDP (User Datagram Protocol)**
  - allows reaching to specific processes on target host
  - connectionless protocol operating 
  - layer 4 (transport layer)
  - does not even know if the packet has been delivered
  - a UDP data unit that encapsulates the app data is a *UDP datagram*.

- **TCP (Transmission Control Protocol)**
  - connection-oriented (required TCP connection) transport protocol
  - layer 4
  - each data octet has a sequence number - receiver can identify lost / duplicated packets, and acknowledge reception by specifying last received octet
  - TCP Connection
    - requires a **three-way handshake**
    1. *SYN Packet*: client initiates connection by sending SYN packet to server, containing client's random initial sequence number
    2. *SYN-ACK Packet*: server responds to SYN Packet with SYN-ACK, adds server's random initial sequence number 
    3. *ACK Packet*: client sends ACK Packet to acknowledge reception of SYN-ACK
  - A TCP data unit that encapsulates the app data is a *TCP segment*.

- **TELNET (Teletype Network)**
  - a network protocol for remote terminal connection
  - can be used to connect to any server *listening on a TCP port number*
  - `telnet x.x.x.x [port]` connects to specific port
  - *Echo server* - listens on port 7, server echoes everything you send
  - *Daytime server* - listens on port 13, replies with current day and time
  - *Web server* - listens on port 80, serves web pages
    - `GET / HTTP/1.1` gets the host