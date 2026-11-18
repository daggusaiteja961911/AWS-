# AWS – Day 7 Notes
## IaaS, PaaS, SaaS + Shared Responsibility

Based on your Day 7 class diagram, today's main topic was **how much responsibility the customer has in different cloud service models**.

---

# 1. AWS is a Group of Services

AWS is not just one service.

It provides many services for:

```text
Compute
Storage
Database
Networking
Security
Monitoring
etc.
```

One important compute service:

> **EC2 = Elastic Compute Cloud**

---

# 2. Virtual Machine = Server

In your class:

```text
Virtual Machine
       ↓
     Server
```

An **EC2 instance** is a virtual server provided by AWS.

```text
AWS
 ↓
EC2
 ↓
EC2 Instance
 ↓
Virtual Server
```

---

# 3. IaaS – Infrastructure as a Service ⭐

**IaaS = Infrastructure as a Service**

The cloud provider gives you infrastructure such as:

- Virtual machines
- Networking
- Storage
- Data-center infrastructure

### Example: AWS EC2

```text
Customer
   ↓
   EC2
   ↓
Virtual Machine
```

With IaaS, the **customer has more control**.

### Responsibility

```text
Customer
 ├── Application
 ├── Data
 └── OS

AWS
 ├── Virtualization
 ├── Network
 └── Data Center
```

So with EC2, you generally manage the **guest OS and everything above it**, while AWS manages the underlying infrastructure.

---

# 4. PaaS – Platform as a Service

**PaaS = Platform as a Service**

Here, the provider manages more of the underlying infrastructure and platform.

The customer mainly focuses on:

```text
Application
   +
Data
```

Your instructor mentioned:

> **AWS Elastic Beanstalk**

as a PaaS example.

### Basic idea

```text
Developer
    ↓
Application
    ↓
Elastic Beanstalk
    ↓
AWS manages underlying infrastructure
```

### Why use PaaS?

> **Easy and quick deployment of applications.**

You don't need to worry as much about managing servers.

---

# 5. SaaS – Software as a Service

**SaaS = Software as a Service**

Here, the provider manages almost everything and you simply **use the software**.

Examples from your class:

- Gmail
- Zoom
- Dropbox
- Salesforce

```text
User
  ↓
Internet
  ↓
SaaS Application
```

You don't manage:

- Servers
- OS
- Virtualization
- Data center

You simply use the application.

---

# 6. IaaS vs PaaS vs SaaS ⭐⭐⭐

The easiest way to understand them is by **responsibility**:

```text
                CUSTOMER CONTROL
                      ↑
                      │
IaaS  ────────────────┤ More
PaaS  ────────────────┤
SaaS  ────────────────┤ Less
                      ↓
                 PROVIDER
```

### Responsibility diagram

```text
IaaS

Customer:
Application
Data
OS

Provider:
Virtualization
Network
Data Center
```

```text
PaaS

Customer:
Application
Data

Provider:
OS
Virtualization
Network
Data Center
```

```text
SaaS

Customer:
Uses the software

Provider:
Application
Data infrastructure
OS
Virtualization
Network
Data Center
```

---

# 7. Simple Real-Life Understanding

Think about cooking:

### IaaS

You get a **kitchen and equipment**.

You prepare most things yourself.

### PaaS

You get a **ready-to-use kitchen/platform**.

You mainly focus on preparing your application.

### SaaS

You get the **finished food**.

You simply use the software.

---

# 8. IaaS, PaaS, SaaS Examples

| Model | Example from class | What you do |
|---|---|---|
| **IaaS** | AWS EC2 | Manage server/OS/application |
| **PaaS** | AWS Elastic Beanstalk | Deploy application |
| **SaaS** | Gmail, Zoom, Dropbox, Salesforce | Use application |

---

# 9. Important Concept — Responsibility

Remember:

```text
IaaS
↓
More responsibility for customer

PaaS
↓
Shared responsibility

SaaS
↓
More responsibility for provider
```

So:

> **IaaS → Customer manages more**

> **PaaS → Provider manages more**

> **SaaS → Provider manages most**

---

# 10. The 3 T's ⭐

Your instructor introduced:

### 1. Elasticity

Ability to **automatically increase or decrease resources according to demand**.

### 2. Scalability

Ability to **increase or decrease capacity to handle changing workload**.

### 3. High Availability

Ability of a system to **remain available even when some components fail**.

These are the **next topics**, so you don't need to go deeply into them yet.

---

# ⭐ Day 7 Quick Revision

```text
                 CLOUD SERVICES
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
         IaaS         PaaS         SaaS
          ↓            ↓            ↓
        EC2       Elastic Beanstalk  Gmail
          ↓            ↓            ↓
    More control   Less control   Just use
```

### Remember:

**IaaS → Infrastructure**

**PaaS → Platform**

**SaaS → Software**

And the progression is:

```text
IaaS → PaaS → SaaS
 ↓       ↓       ↓
More    Less    Least
customer responsibility
```

Next, your **Elasticity → Scalability → High Availability** topic will connect directly to why AWS is useful for real-world applications.