# AWS – Day 9 Notes
## AWS Global Infrastructure: Regions & Availability Zones

Day 9 is very important because **Regions and Availability Zones (AZs)** are the foundation for AWS availability and deployment.

---

# 1. AWS Global Infrastructure

AWS has infrastructure in different geographical locations around the world.

```text
                 AWS Global Infrastructure
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
       Mumbai           Ireland           Other
       Region            Region           Regions
```

A **Region** is a geographical area where AWS has its infrastructure.

---

# 2. What is an AWS Region? ⭐

A **Region** is a geographical location containing AWS infrastructure.

Examples from your class:

```text
Mumbai Region
      ↓
ap-south-1
```

```text
Ireland Region
      ↓
eu-west-1
```

### Important

A Region contains **multiple Availability Zones**.

```text
Region
  │
  ├── AZ 1
  ├── AZ 2
  └── AZ 3
```

---

# 3. Mumbai Region

Your class uses Mumbai as the example:

```text
AWS Region = Mumbai
Region Name = ap-south-1
```

It contains multiple AZs:

```text
ap-south-1a
ap-south-1b
ap-south-1c
```

So:

```text
             Mumbai Region
             ap-south-1
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      1a          1b        1c
```

---

# 4. What is an Availability Zone? ⭐⭐⭐

An **Availability Zone (AZ)** is an isolated location within an AWS Region.

Your instructor describes it simply as:

> **AZ = group of Data Centers**

Conceptually:

```text
           REGION
             │
    ┌────────┼────────┐
    ↓        ↓        ↓
   AZ-1     AZ-2     AZ-3
    │        │        │
   DCs      DCs      DCs
```

So don't think:

> Region = one data center ❌

Instead:

> **Region → Multiple AZs → Data-center infrastructure**

---

# 5. Servers / Instances

Your class says:

> **Servers = Instances**

Instances are placed in Availability Zones.

```text
Mumbai Region
      │
      ├── AZ-1
      │    ├── Instance
      │    └── Instance
      │
      ├── AZ-2
      │    ├── Instance
      │    └── Instance
      │
      └── AZ-3
           ├── Instance
           └── Instance
```

---

# 6. Why Multiple Availability Zones? ⭐⭐⭐

Suppose you deploy everything in only one AZ:

```text
Region
  │
  └── AZ-1
       ├── Server
       ├── Server
       └── Server
```

If that AZ has an outage:

```text
AZ-1 ❌
   ↓
All servers affected
```

Instead, distribute instances:

```text
              Region
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
      AZ-1     AZ-2     AZ-3
       │        │        │
      EC2      EC2      EC2
       ✅       ✅       ✅
```

If one AZ goes down:

```text
AZ-1 ❌

AZ-2 ✅
AZ-3 ✅
```

Your application can continue running if designed appropriately.

---

# 7. Best Practice

Your class emphasizes:

> **Distribute instances across multiple AZs.**

This improves **availability and fault tolerance**.

```text
❌ Bad

AZ-1
 ├── EC2
 ├── EC2
 └── EC2


✅ Better

AZ-1       AZ-2       AZ-3
 EC2        EC2        EC2
```

---

# 8. Communication Between AZs

AZs within the **same Region** are interconnected through AWS networking.

Your class notes:

> AZs can communicate with each other by default.

And:

> AZ networks are interconnected.

The important idea is:

```text
       AZ-1
        │
        │ Network
        │
       AZ-2
        │
        │ Network
        │
       AZ-3
```

Communication within a Region is designed for low latency.

---

# 9. Low Latency ⭐

**Latency** = time taken for data to travel between two points.

```text
Low Latency
     ↓
Faster communication
     ↓
Good ✅
```

```text
High Latency
     ↓
Slower communication
     ↓
Bad ❌
```

For applications, we generally prefer resources that need frequent communication to be geographically close.

---

# 10. Regions Are Separate

Your instructor compared Mumbai and Ireland:

```text
Mumbai Region
ap-south-1

        ❌ No default communication

Ireland Region
eu-west-1
```

The key point from the class:

> **Different AWS Regions don't communicate with each other by default.**

If communication between Regions is required, it needs to be configured using appropriate AWS networking services.

---

# 11. Region vs Availability Zone ⭐⭐⭐

| Region | Availability Zone |
|---|---|
| Geographical area | Isolated location within a Region |
| Contains multiple AZs | Belongs to one Region |
| Example: Mumbai | Example: ap-south-1a |
| Larger scope | Smaller scope |
| Contains multiple AZs | Contains data-center infrastructure |

---

# 12. Simple Hierarchy

Remember this:

```text
AWS Global Infrastructure
            │
         Region
            │
     ┌──────┼──────┐
     ↓      ↓      ↓
    AZ-1   AZ-2   AZ-3
     │      │      │
    DCs    DCs    DCs
     │      │      │
   EC2    EC2    EC2
```

---

# 13. Region Naming ⭐

AWS Region names follow a naming pattern.

For example:

```text
ap-south-1
```

For your class:

```text
ap = Asia Pacific
south = South
1 = Region identifier
```

Mumbai:

> **ap-south-1**

Availability Zones are then identified as:

```text
ap-south-1a
ap-south-1b
ap-south-1c
```

---

# 14. Connection with High Availability

This directly connects to **Day 8**.

Day 8:

```text
High Availability
      ↓
Redundancy
      ↓
Multiple Servers
```

Day 9:

```text
Multiple AZs
      ↓
Servers distributed across AZs
      ↓
If one AZ has an issue
      ↓
Other AZs can continue serving
      ↓
Higher Availability
```

### Example

```text
                    Load Balancer
                         │
              ┌──────────┼──────────┐
              ↓          ↓          ↓
             AZ-1       AZ-2       AZ-3
              │          │          │
             EC2        EC2        EC2
              ✅         ✅         ✅
```

---

# ⭐ Day 9 Quick Revision

### Region

> **Geographical area containing AWS infrastructure.**

### Availability Zone

> **An isolated location within a Region containing data-center infrastructure.**

### Important relationship

```text
AWS
 ↓
Region
 ↓
Multiple AZs
 ↓
Data Centers
 ↓
EC2 Instances
```

### Mumbai example

```text
Mumbai Region
ap-south-1
    │
    ├── ap-south-1a
    ├── ap-south-1b
    └── ap-south-1c
```

### Most important concept

> **Deploying instances across multiple AZs helps protect an application from an AZ-level failure and improves high availability.**