# AWS – Day 14 Notes
## RDS, ElastiCache, Route 53, VPC & Direct Connect

Today covered **AWS database services, caching, DNS, networking and connectivity**.

---

# 1. Database Problems in On-Premises ⭐

Your instructor first compared an on-premises database with AWS.

Example:

```text
On-Premises
     ↓
Physical Machine
     ↓
SQL Server
     ↓
8 GB RAM
```

The class listed several challenges with managing databases yourself:

- No High Availability
- No elasticity
- Scalability issues
- Performance issues
- Database crashes
- Backup issues
- Restoration issues
- Upgrade issues
- Storage issues
- Replication issues
- Mirroring issues
- Migration issues
- Patching issues
- Login issues
- Security issues
- Failover issues
- Maintenance issues
- Tuning issues

This is where **AWS managed database services** become useful.

---

# 2. Amazon RDS ⭐⭐⭐

**RDS = Relational Database Service**

RDS is an AWS **managed service for relational databases**.

Your instructor's important point:

> **RDS is not a database itself; it is a database service.**

```text
                    Amazon RDS
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
      MySQL          Oracle         SQL Server
        ↓
    PostgreSQL
        ↓
      MariaDB
        ↓
      Aurora
```

RDS supports several relational database engines.

---

# 3. RDS vs On-Premises ⭐

### On-Premises

```text
You
 ↓
Physical Server
 ↓
OS
 ↓
Database
 ↓
Backup / Patching / Maintenance
```

You are responsible for much more infrastructure management.

### RDS

```text
You
 ↓
RDS
 ↓
Database
```

AWS manages much of the underlying infrastructure and database administration tasks, depending on the configuration.

---

# 4. RDS Database Engines

Your class mentioned:

| Engine | Type |
|---|---|
| MySQL | Open Source |
| Oracle | Oracle |
| Microsoft SQL Server | Microsoft |
| PostgreSQL | Open Source |
| MariaDB | Community |
| Aurora | AWS |

---

# 5. DynamoDB ⭐

Your instructor also introduced:

**DynamoDB = NoSQL database service**

```text
RDS
 ↓
Relational databases

DynamoDB
 ↓
NoSQL database
```

So:

```text
Database Services
       │
       ├── RDS → Relational
       │
       └── DynamoDB → NoSQL
```

---

# 6. Database vs Data Warehouse

Your class made this distinction:

### Database

Used to store application data.

```text
Application
     ↓
 Database
```

### Data Warehouse

Used for storing and analyzing large amounts of data.

```text
Many Data Sources
       ↓
 Data Warehouse
       ↓
Analytics / Reporting
```

AWS service:

> **Amazon Redshift → Data warehouse**

---

# 7. ElastiCache ⭐⭐⭐

**ElastiCache** is an **in-memory caching service**.

Main idea:

> Frequently accessed data can be kept in memory so applications can access it faster.

```text
          Application
               │
               ↓
            Cache
          ┌───────┐
          │ Data  │
          └───────┘
               │
          Database
```

Without cache:

```text
Application → Database
Application → Database
Application → Database
```

With cache:

```text
Application
     ↓
   Cache
     │
     └── if data not available
             ↓
          Database
```

---

# 8. Why ElastiCache?

Your instructor highlighted:

- **Low latency**
- **High performance**

Because memory access is much faster than repeatedly retrieving frequently accessed data from a database.

---

# 9. ElastiCache Engines

Your class mentioned:

```text
ElastiCache
    │
    ├── Redis
    └── Memcached
```

These are commonly used for caching.

---

# 10. Real Example

Suppose a shopping application receives millions of requests for frequently viewed product information.

```text
Mobile/Web Users
       ↓
Application Server
       ↓
     Cache
       ↓
   Database
```

Frequently accessed data can be served from the cache instead of repeatedly querying the database.

---

# 11. Route 53 ⭐⭐⭐

**Amazon Route 53** is AWS's **DNS service**.

Your class notes:

> **R53 is a DNS service in AWS.**

The number **53** comes from the DNS port:

> **DNS → Port 53**

---

# 12. What Does DNS Do?

DNS converts a domain name into an IP address.

```text
Browser
   ↓
www.example.com
   ↓
DNS
   ↓
IP Address
   ↓
Server
```

Instead of remembering an IP address, users use a domain name.

---

# 13. Route 53 + Load Balancer

Your class showed:

```text
                  Route 53
                     ↓
                 DNS Name
                     ↓
                    ELB
                     ↓
          ┌──────────┼──────────┐
          ↓          ↓          ↓
         EC2        EC2        EC2
         AZ-1       AZ-2       AZ-3
```

So a common architecture is:

> **Domain → Route 53 → Load Balancer → EC2**

---

# 14. DNS Mapping

For example:

```text
boom.com
    ↓
Route 53
    ↓
ELB DNS name
    ↓
Load Balancer
```

This is done using DNS records.

---

# 15. VPC ⭐

You already learned VPC on Day 10.

**VPC = Virtual Private Cloud**

It provides a logically isolated virtual network in AWS.

```text
AWS Region
    │
   VPC
    │
 ┌──┼──┐
 ↓  ↓  ↓
AZ AZ AZ
 │  │  │
EC2 EC2 EC2
```

---

# 16. VPC is Regional

Your instructor again emphasized:

> **VPC is regional.**

A VPC belongs to a Region and can contain resources across multiple Availability Zones.

```text
              Region
                 │
        ┌────────┴────────┐
        │       VPC       │
        │                 │
       AZ-1              AZ-2
        │                 │
       EC2               EC2
```

---

# 17. Direct Connect ⭐⭐⭐

The final topic in the image is **AWS Direct Connect**.

It provides a dedicated network connection between an **on-premises environment and AWS**.

```text
On-Premises
    │
    │ Direct Connect
    ↓
   AWS
    │
   VPC
```

Instead of relying only on the public internet:

```text
Company
   │
Public Internet
   │
  AWS
```

Direct Connect provides a dedicated connectivity option.

---

# 18. Complete Architecture from Day 14 ⭐⭐⭐

Now connect today's concepts:

```text
                       Users
                         │
                         ↓
                    Route 53
                      (DNS)
                         │
                         ↓
                        ELB
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
            EC2         EC2         EC2
           AZ-1        AZ-2        AZ-3
             │           │           │
             └───────────┼───────────┘
                         ↓
                    Application
                         │
                ┌────────┴────────┐
                ↓                 ↓
           ElastiCache            RDS
           Redis/                Database
           Memcached
```

For on-premises connectivity:

```text
                 AWS
                  │
                 VPC
                  │
           Direct Connect
                  │
                  ↓
             On-Premises
```

---

# ⭐ Day 14 Quick Revision

| Service | Purpose |
|---|---|
| **RDS** | Managed relational databases |
| **DynamoDB** | NoSQL database |
| **Redshift** | Data warehouse |
| **ElastiCache** | In-memory caching |
| **Redis** | Cache engine |
| **Memcached** | Cache engine |
| **Route 53** | DNS |
| **VPC** | Virtual private network |
| **Direct Connect** | Dedicated connectivity to AWS |

### Most important flow

```text
Route 53
   ↓
ELB
   ↓
EC2
   ↓
ElastiCache
   ↓
RDS
```

And for on-premises:

```text
On-Premises
     ↓
Direct Connect
     ↓
    VPC
     ↓
   AWS
```