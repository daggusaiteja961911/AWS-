# AWS – Day 2 Notes
## Client–Server Architecture

Day 2 is important because AWS infrastructure is built around these basic concepts.

---

# 1. What is Client–Server Architecture?

It is an architecture where:

- **Client** → Requests a service/resource.
- **Server** → Processes the request and provides a response.

### Basic diagram

```text
┌──────────────┐
│    CLIENT    │
│              │
│ Browser/App  │
└──────┬───────┘
       │ Request
       ↓
┌──────────────┐
│    SERVER    │
│              │
│ Processes    │
│ request      │
└──────┬───────┘
       │ Response
       ↓
┌──────────────┐
│    CLIENT    │
└──────────────┘
```

### Example

When you open a website:

```text
Your Browser
     ↓
   Request
     ↓
Web Server
     ↓
   Response
     ↓
Your Browser
```

---

# 2. Client

A **client** is a device/application that requests a service from a server.

Examples:

- Laptop
- Mobile phone
- Web browser
- Mobile application
- Desktop application

Example:

```text
Chrome → requests → Google website
```

Chrome acts as the client.

---

# 3. Server

A **server** is a computer/system that receives requests and provides services or resources.

Examples:

- Web server
- Application server
- Database server
- File server

Example:

```text
Client
   ↓
Web Server
   ↓
HTML/CSS/JS
   ↓
Client
```

---

# 4. Client and Server Communication

Usually communication happens through a **network**.

```text
Client
  │
  │ Request
  ↓
Network
  │
  ↓
Server
  │
  │ Response
  ↓
Network
  │
  ↓
Client
```

Common protocols:

- HTTP
- HTTPS
- TCP/IP
- DNS

You will study these more deeply later.

---

# 5. What is a Network?

A **network** is a connection between devices that allows them to communicate and exchange data.

Example:

```text
Laptop ───┐
          │
Mobile ───┼── Router ─── Internet
          │
Printer ──┘
```

---

# 6. Network Devices

Some common network devices:

### 1. Router

Connects different networks and forwards packets between them.

```text
Home Network
     │
     ↓
  Router
     │
     ↓
 Internet
```

---

### 2. Switch

Connects multiple devices within the same network.

```text
        Switch
       /  |  \
      /   |   \
    PC   PC  Printer
```

---

### 3. Modem

Provides connectivity between your local network and the ISP connection.

Simple understanding:

```text
Your Network
     ↓
   Modem
     ↓
    ISP
     ↓
 Internet
```

---

### 4. Firewall

Controls network traffic based on security rules.

```text
Internet
   ↓
Firewall
   ↓
Internal Network
```

It can allow or block traffic.

---

# 7. What is Architecture?

Architecture describes **how different components of an application are organized and communicate with each other.**

For example:

```text
Client → Server
```

is a simple architecture.

As applications become bigger, we separate responsibilities into different layers.

This leads to:

1. **1-Tier Architecture**
2. **2-Tier Architecture**
3. **3-Tier Architecture**

---

# 8. 1-Tier Architecture

In **1-tier architecture**, everything is present in a single system/layer.

```text
┌───────────────────────────┐
│          CLIENT           │
│                           │
│ UI + Business Logic       │
│ + Database                │
│                           │
└───────────────────────────┘
```

Everything runs together.

### Example

A simple standalone application storing data locally.

```text
Application
    │
    ├── UI
    ├── Logic
    └── Data
```

### Advantages

- Simple
- Easy to develop
- Easy to deploy

### Disadvantages

- Difficult to scale
- Poor separation
- Not suitable for large applications

---

# 9. 2-Tier Architecture

In **2-tier architecture**, the application is divided into:

1. Client
2. Server

The client directly communicates with the server/database.

```text
┌──────────────┐
│    CLIENT    │
│              │
│ UI + Logic   │
└──────┬───────┘
       │
       │ Request
       ↓
┌──────────────┐
│    SERVER    │
│              │
│   Database   │
└──────────────┘
```

### Example

A desktop banking application directly communicating with a database server.

```text
Desktop App
     │
     │ SQL
     ↓
Database Server
```

### Problem

The client contains a lot of logic.

If thousands of clients connect directly to the database:

```text
Client 1 ──┐
Client 2 ──┤
Client 3 ──┤
Client 4 ──┼── Database
Client 5 ──┤
   ...     │
Client N ──┘
```

This can become difficult to manage and scale.

---

# 10. 3-Tier Architecture ⭐

This is **very important for software development and AWS**.

The application is divided into three layers:

```text
┌────────────────────┐
│    Presentation    │
│       Tier         │
│                    │
│ Browser / UI       │
└─────────┬──────────┘
          │
          ↓
┌────────────────────┐
│   Application      │
│       Tier         │
│                    │
│ Business Logic     │
└─────────┬──────────┘
          │
          ↓
┌────────────────────┐
│      Database      │
│       Tier         │
│                    │
│ Data Storage       │
└────────────────────┘
```

---

# 11. Three Tiers Explained

## Tier 1 – Presentation Tier

This is what the user interacts with.

Examples:

- HTML
- CSS
- JavaScript
- React
- Mobile UI

```text
User
 ↓
Browser
 ↓
UI
```

---

## Tier 2 – Application Tier

Contains the **business logic**.

Examples:

- Java
- Spring Boot
- Python
- .NET
- Node.js

For your Java path:

```text
Browser
   ↓
Spring Boot Application
   ↓
Business Logic
```

Example:

```text
User clicks "Transfer Money"
              ↓
       Java/Spring Boot
              ↓
       Validate request
              ↓
       Process transaction
```

---

## Tier 3 – Database Tier

Stores application data.

Examples:

- MySQL
- PostgreSQL
- Oracle
- MongoDB
- Amazon RDS

```text
Application
     ↓
Database
     ↓
User Data
```

---

# 12. Complete 3-Tier Example

Suppose you build an **online shopping application**.

```text
              USER
                │
                ↓
       ┌─────────────────┐
       │   Presentation  │
       │   React / HTML  │
       └────────┬────────┘
                │
                ↓
       ┌─────────────────┐
       │   Application   │
       │ Java + Spring   │
       │     Boot        │
       └────────┬────────┘
                │
                ↓
       ┌─────────────────┐
       │    Database     │
       │     MySQL       │
       └─────────────────┘
```

For example, when you open a product:

```text
Browser
   ↓
"Show iPhone"
   ↓
Spring Boot
   ↓
Query Database
   ↓
Database returns product
   ↓
Spring Boot
   ↓
Browser
   ↓
Product displayed
```

---

# 13. 3-Tier Architecture in AWS ⭐

This is where today's topic connects directly to AWS.

A simple AWS implementation can look like:

```text
                 INTERNET
                    │
                    ↓
              ┌───────────┐
              │   Client  │
              │  Browser  │
              └─────┬─────┘
                    │
                    ↓
              ┌───────────┐
              │    AWS    │
              │    EC2    │
              │  Backend  │
              └─────┬─────┘
                    │
                    ↓
              ┌───────────┐
              │   Amazon  │
              │    RDS    │
              │ Database  │
              └───────────┘
```

So:

| Tier | Example |
|---|---|
| Presentation | Browser / Frontend |
| Application | EC2 + Java/Spring Boot |
| Database | Amazon RDS |

Later, AWS introduces more services to make this architecture more scalable and secure.

---

# 14. 2-Tier vs 3-Tier

| 2-Tier | 3-Tier |
|---|---|
| Client + Server | Presentation + Application + Database |
| Fewer layers | Better separation |
| Client may directly access DB | Client doesn't directly access DB |
| Less scalable | More scalable |
| Suitable for simpler systems | Suitable for larger applications |

---

# 15. Important Interview Questions

### What is client-server architecture?

An architecture where a client sends requests and a server processes those requests and returns responses.

### What is 1-tier architecture?

All components such as UI, business logic and data are present in a single system/layer.

### What is 2-tier architecture?

The application is divided mainly into a client and a server, with the client communicating directly with the server/database.

### What is 3-tier architecture?

An architecture divided into:

**Presentation → Application → Database**

### Why use 3-tier architecture?

Because it provides **separation of responsibilities, easier maintenance, better security and better scalability.**

---

## ⭐ Day 2 Quick Revision

```text
CLIENT
   ↓
Network
   ↓
SERVER
```

Then architectures:

```text
1-Tier
Everything together
```

```text
2-Tier
Client → Server/Database
```

```text
3-Tier
Client
  ↓
Application
  ↓
Database
```

And in your Java + AWS career:

```text
Browser
   ↓
Java / Spring Boot
   ↓
Database
```

This **3-tier architecture** is one of the most important foundations to understand before learning AWS services like **EC2, VPC, Load Balancer, RDS, and Auto Scaling**.