# AWS – Day 10 Notes
## VPC – Virtual Private Cloud

Today you learned the basic concept of **VPC** and where it fits in the AWS infrastructure hierarchy.

---

# 1. What is VPC? ⭐

**VPC = Virtual Private Cloud**

A VPC is a **logically isolated virtual network in AWS** where you can launch and manage AWS resources.

Think of it as:

> **Your own private network inside AWS.**

---

# 2. Where does VPC fit?

From Day 9:

```text
AWS
 ↓
Region
 ↓
Availability Zone
 ↓
EC2 Instance
```

Now add VPC:

```text
AWS
 ↓
Region
 ↓
VPC
 ↓
Availability Zone
 ↓
EC2 Instance
```

More accurately, a VPC **spans a Region**, while its subnets are associated with specific AZs.

```text
              AWS Region
        ┌─────────────────────┐
        │        VPC          │
        │                     │
        │   ┌─────┐ ┌─────┐ │
        │   │ AZ-a│ │ AZ-b│ │
        │   │ EC2 │ │ EC2 │ │
        │   └─────┘ └─────┘ │
        │                     │
        └─────────────────────┘
```

---

# 3. Why is it called "Private"?

The VPC provides a logically isolated networking environment for your AWS resources.

You control things such as:

- IP addressing
- Routing
- Network access
- Subnets
- Security controls

So you can design how your resources communicate.

---

# 4. Multiple VPCs in a Region

Your instructor showed that:

> **One AWS Region can contain multiple VPCs.**

Conceptually:

```text
             AWS Region
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
      VPC-1      VPC-2      VPC-3
```

Each VPC is a separate logical network.

---

# 5. VPC and EC2

EC2 instances are launched **inside a VPC**.

```text
AWS Region
    │
   VPC
    │
   AZ
    │
  EC2 Instance
```

Example:

```text
┌─────────────────────────────┐
│          Region             │
│                             │
│   ┌─────────────────────┐   │
│   │        VPC          │   │
│   │                     │   │
│   │   ┌─────────────┐   │   │
│   │   │     AZ      │   │   │
│   │   │   ┌──────┐  │   │   │
│   │   │   │ EC2  │  │   │   │
│   │   │   └──────┘  │   │   │
│   │   └─────────────┘   │   │
│   └─────────────────────┘   │
└─────────────────────────────┘
```

---

# 6. VPC is Not the Same as AZ ⭐

This is important.

### VPC

A VPC is associated with a **Region**.

```text
VPC
 ↓
Region-wide
```

### Availability Zone

An AZ is a specific isolated location within that Region.

```text
Region
 ├── AZ-a
 ├── AZ-b
 └── AZ-c
```

A VPC can have resources across multiple AZs.

---

# 7. Why use Multiple VPCs?

Organizations may create separate VPCs for different environments or purposes.

For example:

```text
AWS Region
   │
   ├── VPC-Development
   │
   ├── VPC-Testing
   │
   └── VPC-Production
```

This provides logical separation between environments.

---

# 8. Important Hierarchy ⭐⭐⭐

For your AWS notes, remember this structure:

```text
                 AWS
                  │
               Region
                  │
          ┌───────┴───────┐
          │               │
         VPC             VPC
          │
       Subnets
          │
     ┌────┴────┐
     ↓         ↓
    AZ-a      AZ-b
     │         │
    EC2       EC2
```

**Important correction to the simplified classroom diagram:** VPCs are **regional**, while **subnets are tied to a specific Availability Zone**. EC2 instances are launched into subnets.

---

# ⭐ Day 10 Quick Revision

### VPC

> **Virtual Private Cloud = logically isolated virtual network in AWS.**

### Key relationship

```text
AWS
 ↓
Region
 ↓
VPC
 ↓
Subnet
 ↓
Availability Zone
 ↓
EC2 Instance
```

The most important concept to remember from today:

> **A VPC gives you a logically isolated network environment in an AWS Region, and you can place your AWS resources such as EC2 instances inside it.**