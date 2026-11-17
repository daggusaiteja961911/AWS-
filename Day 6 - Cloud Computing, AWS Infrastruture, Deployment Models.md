# AWS – Day 6 Notes
## Cloud Computing, AWS Infrastructure, Deployment Models & Service Models

Day 6 connects **virtualization → cloud computing → AWS** and introduces the **types of cloud and cloud service models**.

---

# 1. AWS Global Infrastructure

AWS has a **global infrastructure** consisting of infrastructure/data centers in different geographical locations.

```text
             AWS Global Infrastructure
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
      India          USA           Europe
        │
    Data Centers
```

The important idea:

> AWS infrastructure is available in different remote geographical locations.

---

# 2. AWS as a Cloud Provider

**AWS = Amazon Web Services**

AWS is a **cloud provider** that provides infrastructure and other cloud services.

Your class specifically describes AWS as:

> **A Public Cloud Provider providing Infrastructure as a Service (IaaS).**

---

# 3. What is Cloud Computing?

Earlier:

```text
Your Computer / On-Premises
          ↓
      Computing
```

With cloud computing:

```text
Your Computer
      │
   Internet
      │
      ↓
Remote Location / Cloud
      │
      ↓
   Computing
```

### Definition

> **Cloud computing means performing computing using resources available at a remote location through a network/Internet instead of relying only on local/on-premises infrastructure.**

---

# 4. Remote Location

In your class:

> **Remote Location = Data Center**

For example:

```text
Hyderabad
    │
    │ Internet
    ↓
Mumbai Data Center
```

Your application/computing resources can be located in a remote AWS data center.

---

# 5. Why Internet is Important

To access cloud resources from your local machine, you generally need network connectivity.

```text
Local Machine
      │
      │ Internet
      ↓
AWS Cloud
      │
      ↓
AWS Data Center
```

---

# 6. Physical DC → Virtualization → Cloud → AWS ⭐

This is an important Day 5 + Day 6 connection.

```text
Physical Data Center
        ↓
   Virtualization
        ↓
   Cloud Computing
        ↓
       AWS
        ↓
Remote AWS Infrastructure
```

### Meaning

**Physical Data Center**

→ Physical servers and infrastructure.

**Virtualization**

→ Multiple virtual machines can run on physical infrastructure.

**Cloud**

→ Computing resources are provided remotely as services.

**AWS**

→ A major cloud provider offering these resources/services.

---

# 7. AWS Provides Infrastructure as a Service

AWS provides infrastructure resources through cloud services.

Examples you'll learn later:

```text
Compute
Storage
Networking
Database
Security
```

One important AWS example:

```text
EC2 → Virtual Servers
```

EC2 is an example of **IaaS-oriented cloud computing**.

---

# 8. Deployment Models / Types of Cloud

Your class introduced **four deployment models**:

1. Public Cloud
2. Private Cloud
3. Hybrid Cloud
4. Community Cloud

---

# 9. Public Cloud ⭐

A **Public Cloud** is cloud infrastructure/services provided by a cloud provider and made available to customers.

Examples:

- AWS
- Microsoft Azure
- Google Cloud

```text
             Public Cloud
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      AWS       Azure      GCP
```

### Example

A company uses AWS instead of building its own complete data center.

---

# 10. Private Cloud

A **Private Cloud** is cloud infrastructure dedicated to a particular organization.

Your class example mentions:

```text
Organization
     ↓
Private Cloud
     ↓
Only that organization
```

It is generally used when an organization wants greater control over its dedicated cloud environment.

---

# 11. Hybrid Cloud ⭐

**Hybrid Cloud = Combination of Public Cloud + Private Cloud**

```text
       Hybrid Cloud
            │
      ┌─────┴─────┐
      ↓           ↓
 Private        Public
  Cloud          Cloud
```

Example:

```text
Company Data
     ↓
Private Cloud

Public Application
     ↓
AWS Public Cloud
```

Both environments can work together.

---

# 12. Community Cloud

Your class describes Community Cloud as:

> Similar to a private cloud, but accessible by a few organizations that share common requirements.

```text
        Community Cloud
               │
       ┌───────┼───────┐
       ↓       ↓       ↓
    Org A    Org B    Org C
```

It is intended for organizations with shared requirements or interests.

---

# 13. Deployment Models — Quick Table

| Model | Basic Meaning |
|---|---|
| **Public Cloud** | Cloud services available to customers through a provider |
| **Private Cloud** | Cloud environment dedicated to an organization |
| **Hybrid Cloud** | Public + Private Cloud |
| **Community Cloud** | Shared by organizations with common requirements |

---

# 14. Cloud Service Models ⭐⭐⭐

Day 6 also introduced **three service models**:

```text
IaaS
PaaS
SaaS
```

---

# 15. IaaS — Infrastructure as a Service

**IaaS = Infrastructure as a Service**

The provider gives you infrastructure resources.

Examples:

- Virtual machines
- Storage
- Networking

```text
       IaaS
        ↓
   Infrastructure
        ↓
   VM / Storage /
    Networking
```

### AWS example

```text
Amazon EC2
```

You get a virtual server and manage much of the software stack yourself.

---

# 16. PaaS — Platform as a Service

**PaaS = Platform as a Service**

The provider manages the underlying infrastructure and provides a platform on which you can develop/deploy applications.

```text
Developer
    ↓
   PaaS
    ↓
Application
```

The developer focuses more on the application rather than managing the underlying infrastructure.

---

# 17. SaaS — Software as a Service

**SaaS = Software as a Service**

You directly use a software application provided through the internet.

```text
User
 ↓
Internet
 ↓
Software
```

You generally don't manage the underlying servers, operating system, or infrastructure.

Examples conceptually include online email, office applications, and CRM software.

---

# 18. IaaS vs PaaS vs SaaS ⭐

Think about **how much you manage**:

```text
             YOU MANAGE
                ↑
                │
IaaS  →  MORE
PaaS  →  MEDIUM
SaaS  →  LESS
                ↓
          PROVIDER MANAGES
```

| Model | Main Idea |
|---|---|
| **IaaS** | Infrastructure |
| **PaaS** | Platform |
| **SaaS** | Complete Software |

Easy memory:

> **IaaS → Infrastructure**  
> **PaaS → Platform**  
> **SaaS → Software**

---

# 19. Complete Day 6 Picture ⭐⭐⭐

```text
                    CLOUD
                      │
        ┌─────────────┴─────────────┐
        │                           │
 Deployment Models             Service Models
        │                           │
 ┌──────┼────────┐            ┌─────┼─────┐
 ↓      ↓        ↓            ↓     ↓     ↓
Public Private Hybrid       IaaS   PaaS  SaaS
        │
        ↓
      AWS
        │
        ↓
Remote AWS Infrastructure
        │
        ↓
   Data Centers
```

---

## ⭐ Day 6 Quick Revision

```text
AWS
 ↓
Cloud Provider
 ↓
Global Infrastructure
 ↓
Remote Data Centers
 ↓
Cloud Computing
```

### Deployment Models

```text
Public
Private
Hybrid
Community
```

### Service Models

```text
IaaS → Infrastructure
PaaS → Platform
SaaS → Software
```

### Most important connection

```text
Physical Data Center
        ↓
   Virtualization
        ↓
      Cloud
        ↓
       AWS
```

This is the foundation you'll need before moving into **AWS Regions, Availability Zones, EC2, VPC, S3, IAM, and other AWS services**.