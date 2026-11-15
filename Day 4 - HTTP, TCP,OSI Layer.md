# AWS – Day 4 Notes
## HTTP, HTTPS, Ports, TCP/UDP & OSI Model

Based on today's class diagrams, Day 4 mainly covered **how a client communicates with a server using HTTP/HTTPS, ports and TCP/IP**, followed by the **7-layer OSI model**.

---

# 1. HTTP

**HTTP = HyperText Transfer Protocol**

It is used for communication between a client and a web server.

```text
Client/Browser
      │
      │ HTTP Request
      ↓
    Network
      │
      ↓
    Server
      │
      │ HTTP Response
      ↓
Client/Browser
```

HTTP transfers data **to and from** the browser and server.

---

# 2. HTTP Default Port

The default port for HTTP is:

```text
HTTP → 80
```

Example:

```text
http://google.com:80
```

Usually we don't write `:80` because 80 is the default.

```text
http://google.com
```

means:

```text
http://google.com:80
```

---

# 3. HTTPS

**HTTPS = HTTP Secure**

HTTPS provides secure communication between the client and server.

Default port:

```text
HTTPS → 443
```

```text
Browser
   │
   │ HTTPS
   │ 443
   ↓
Server
```

HTTPS uses **TLS** to provide encryption and secure communication.

---

# 4. HTTP vs HTTPS

| HTTP | HTTPS |
|---|---|
| Not encrypted | Encrypted |
| Port 80 | Port 443 |
| Less secure | Secure |
| Data can be transmitted in plaintext | Data is protected using TLS |

Simple:

```text
HTTP  → Not Secure
HTTPS → Secure
```

---

# 5. What is a Port?

A **port number** identifies a particular network service/application on a host.

Example:

```text
Server
192.168.10.10
      │
      ├── :80    HTTP
      ├── :443   HTTPS
      ├── :22    SSH
      └── :3389  RDP
```

Think:

```text
IP Address → Which machine?
Port        → Which service on that machine?
```

---

# 6. URL Structure

Your class showed:

```text
http://google.com
```

General structure:

```text
Protocol://DomainName:PortNumber
```

Example:

```text
http://google.com:80
```

Breakdown:

```text
http       → Protocol
google.com → Domain Name
80         → Port
```

---

# 7. Application Port Example — Tomcat

Your diagram shows:

```text
Application
   Tomcat
   8080

Server
192.168.10.10
```

Tomcat commonly listens on port **8080**.

So:

```text
http://192.168.10.10:8080
```

can be used to access an application running on Tomcat.

### Important

Port **8080 is not the default HTTP port**.

It is commonly used by application servers such as Tomcat.

```text
HTTP standard → 80
Tomcat commonly → 8080
HTTPS → 443
```

---

# 8. Why expose Port 80?

Your instructor explained that customers are generally recommended to access the application through standard ports such as **80/443**, while the backend application can run on another port.

Example:

```text
Internet
   │
   │ :80 / :443
   ↓
Web Server / Load Balancer
   │
   │ :8080
   ↓
Tomcat Application
```

So users don't necessarily need to know that Tomcat is running on `8080`.

---

# 9. HTTP Status Codes

When a server responds to a request, it returns an **HTTP status code**.

### 200 — Success

```text
200 OK
```

Request was successful.

---

### 401 — Unauthorized

```text
401 Unauthorized
```

Authentication is required or authentication failed.

---

### 404 — Not Found

```text
404 Not Found
```

The requested resource/page was not found.

---

### 500 — Internal Server Error

```text
500 Internal Server Error
```

Something went wrong on the server.

---

### 503 — Service Unavailable

```text
503 Service Unavailable
```

The server/service is currently unavailable.

---

# 10. Data Packet

When data travels through a network, it is divided into **packets**.

Your diagram represents a packet with:

```text
┌─────────────────┐
│ Source          │
│ Destination     │
│ Protocol        │
│ Port            │
│ Data            │
└─────────────────┘
```

### Source

Where the packet comes from.

### Destination

Where the packet should go.

### Protocol

Which communication protocol is being used.

### Port

Which service/application should receive the data.

### Data

The actual information being transferred.

---

# 11. TCP

**TCP = Transmission Control Protocol**

TCP provides **reliable, connection-oriented communication**.

Your instructor compared TCP to a:

> Messenger / bridge

Simple understanding:

```text
Host 1
  │
  │ TCP connection
  ↓
Host 2
```

TCP establishes a connection before transferring data.

### TCP provides

- Reliable delivery
- Ordered delivery
- Error checking
- Connection establishment

---

# 12. UDP

**UDP = User Datagram Protocol**

UDP is connectionless and generally has lower overhead than TCP.

```text
Host 1
  │
  │ UDP
  ↓
Host 2
```

Unlike TCP, UDP does not establish the same type of connection before sending data.

### Simple comparison

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable | No delivery guarantee |
| Ordered delivery | No ordering guarantee |
| More overhead | Less overhead |
| Used when reliability matters | Used when speed/low overhead matters |

---

# 13. HTTP Over TCP/IP

Your diagram shows:

```text
HTTP
  ↓
TCP
  ↓
IP
```

A simplified view:

```text
Application
    ↓
   HTTP
    ↓
   TCP
    ↓
    IP
    ↓
Network
```

For normal HTTP/1.1 and HTTP/2, HTTP uses TCP.

---

# 14. OSI Model ⭐⭐⭐

The **OSI Model** has **7 layers**.

From top to bottom:

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

Easy order:

```text
Application
Presentation
Session
Transport
Network
Data Link
Physical
```

---

# 15. Layer 7 — Application

This is the layer closest to the user/application.

Examples include protocols such as:

- HTTP
- DNS
- FTP
- SMTP

Your diagram shows:

```text
Application Layer → HTTP
```

---

# 16. Layer 6 — Presentation

Responsible for things such as:

- Data representation
- Encryption/decryption
- Compression

It helps ensure that data is represented in a form the receiving system can understand.

---

# 17. Layer 5 — Session

Responsible for establishing, managing and terminating communication sessions.

```text
Session
   ↓
Communication between applications
```

---

# 18. Layer 4 — Transport

Responsible for end-to-end transport.

Important protocols:

```text
TCP
UDP
```

```text
Transport Layer
      ↓
   TCP / UDP
```

---

# 19. Layer 3 — Network

Responsible for logical addressing and routing.

Important protocol:

```text
IP
```

```text
Network Layer
      ↓
      IP
```

Routers mainly operate at this layer.

---

# 20. Layer 2 — Data Link

Responsible for communication between devices on the same local network.

Examples include:

- Ethernet
- MAC addressing

Switches primarily operate at this layer.

---

# 21. Layer 1 — Physical

Deals with the physical transmission of bits.

Examples:

- Cables
- Electrical signals
- Fiber
- Radio signals

```text
Physical Layer
      ↓
  0s and 1s
```

---

# 22. Complete OSI Flow ⭐

```text
┌─────────────────────┐
│ 7. Application      │ ← HTTP
├─────────────────────┤
│ 6. Presentation     │
├─────────────────────┤
│ 5. Session          │
├─────────────────────┤
│ 4. Transport        │ ← TCP / UDP
├─────────────────────┤
│ 3. Network          │ ← IP
├─────────────────────┤
│ 2. Data Link        │ ← MAC / Ethernet
├─────────────────────┤
│ 1. Physical         │ ← Signals / Cables
└─────────────────────┘
```

---

# 23. How Everything Connects

When you open a website:

```text
Browser
   ↓
HTTP / HTTPS
   ↓
TCP
   ↓
IP
   ↓
Network
   ↓
Server
```

And on the server side:

```text
Internet
   ↓
Firewall
   ↓
Load Balancer
   ↓
Web Server
   ↓
Application Server
   ↓
Database
```

So your **Day 3 + Day 4** concepts connect like this:

```text
google.com
     ↓
DNS
     ↓
IP Address
     ↓
HTTPS : 443
     ↓
TCP
     ↓
IP
     ↓
Internet
     ↓
Firewall
     ↓
Load Balancer
     ↓
Web Server
     ↓
Application Server
     ↓
Database
```

---

## ⭐ Day 4 Quick Revision

Remember these:

```text
HTTP       → Port 80
HTTPS      → Port 443
SSH        → Port 22
RDP        → Port 3389
Tomcat     → Commonly 8080
```

```text
TCP → Reliable + Connection-oriented
UDP → Connectionless + Low overhead
```

```text
200 → Success
401 → Unauthorized
404 → Not Found
500 → Internal Server Error
503 → Service Unavailable
```

```text
OSI:

7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

**One important correction from the class diagram:** SSH and RDP are generally classified as **application-layer protocols**, not Presentation-layer protocols. The OSI model is mainly a conceptual model, so real-world protocols don't always fit perfectly into one layer.