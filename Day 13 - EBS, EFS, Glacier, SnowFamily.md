# AWS – Day 13 Notes
## EBS, EFS, Storage Gateway, Glacier & Snow Family

Today you learned about different **AWS storage services** and when to use them.

---

# 1. EBS – Elastic Block Store ⭐⭐⭐

**EBS = Elastic Block Store**

EBS provides **block storage** for EC2 instances.

```text
EC2 Instance
     │
     │ attach
     ↓
 EBS Volume
```

Think of EBS like a **hard disk attached to an EC2 server**.

---

# 2. EBS Volume

An EBS volume is a storage volume that can be attached to an EC2 instance.

```text
        EC2
   ┌─────────────┐
   │ Application │
   │     OS      │
   │             │
   └──────┬──────┘
          │
       EBS Volume
          │
       Storage
```

---

# 3. Root Volume ⭐

When an EC2 instance is launched, it has a **root volume**.

The root volume contains the **Operating System**.

```text
EC2 Instance
     │
     ├── Root Volume
     │      ↓
     │     OS
     │
     └── Additional Volume
            ↓
          Data
```

Examples of OS:

- Windows
- Linux

---

# 4. Additional EBS Volumes

You can attach additional EBS volumes to an EC2 instance.

```text
             EC2
              │
       ┌──────┴──────┐
       ↓             ↓
 Root Volume    Additional Volume
    (OS)             (Data)
```

Your class explains:

> EC2 can have one root volume and multiple additional volumes.

---

# 5. Attach and Detach ⭐

EBS volumes can be:

```text
EC2
 │
 ├── attach → EBS
 │
 └── detach ← EBS
```

This allows storage to be separated from the compute instance.

---

# 6. EBS and Availability Zone ⭐⭐⭐

Your instructor highlighted an important point:

> **EC2 instance and EBS volume should be in the same AZ.**

For example:

```text
Region
 │
 ├── AZ-1a
 │    ├── EC2
 │    └── EBS
 │
 └── AZ-1b
      └── EC2
```

An EBS volume is associated with a specific AZ.

---

# 7. Root vs Additional Volume

| Root Volume | Additional Volume |
|---|---|
| Contains OS | Usually contains application/data |
| Required for the instance's OS | Optional |
| Root disk | Extra storage |
| Example: `/dev/sda1` | Examples: `/dev/sdb`, `/dev/sdc` |

Your class also introduced device names such as:

```text
/dev/sda1
/dev/xvda
/dev/xvdf
```

---

# 8. EBS Volume Size

Your instructor discussed increasing the size of an EBS volume.

Important idea:

> **EBS volume size can be increased while the instance is running.**

```text
100 GB
  ↓
200 GB
  ↓
500 GB
```

The exact maximum depends on the **EBS volume type/configuration**, so don't memorize the class's 16-TB figure as a universal EBS limit.

---

# 9. EBS vs S3 ⭐⭐⭐

You learned S3 yesterday.

### S3

```text
S3
 ↓
Bucket
 ↓
Objects
```

**Object storage**

### EBS

```text
EC2
 ↓
EBS Volume
 ↓
Block storage
```

**Block storage**

Easy memory:

> **S3 → Store objects/files**

> **EBS → Disk-like storage for EC2**

---

# 10. EFS – Elastic File System ⭐⭐⭐

**EFS = Elastic File System**

EFS provides **file-based storage**.

It is designed to be accessed by multiple compute instances.

```text
              EFS
          /    |    \
         /     |     \
       EC2    EC2    EC2
       AZ-1   AZ-2   AZ-3
```

This is different from EBS.

---

# 11. EBS vs EFS ⭐⭐⭐

### EBS

```text
EC2 ───── EBS
```

Primarily attached to an EC2 instance.

### EFS

```text
        ┌── EC2
        │
EFS ────┼── EC2
        │
        └── EC2
```

Multiple EC2 instances can access the same EFS file system.

Your class specifically highlighted:

> **EFS can be mounted to multiple EC2 instances.**

---

# 12. EFS is File-Based Storage

EFS works like a shared file system.

```text
EFS
 │
 ├── file1
 ├── file2
 ├── folder1
 │     └── file3
 └── folder2
```

Your instructor also mentioned **NFSv4**.

---

# 13. EBS vs EFS vs S3

| Service | Storage Type | Main Use |
|---|---|---|
| **EBS** | Block | Disk/storage for EC2 |
| **EFS** | File | Shared file system |
| **S3** | Object | Files/objects |

Remember:

```text
EBS → Block
EFS → File
S3  → Object
```

---

# 14. Storage Gateway

Your class introduced **AWS Storage Gateway**.

It helps connect **on-premises storage/environments with AWS storage**.

Basic idea:

```text
On-Premises
    │
    ↓
Storage Gateway
    │
    ↓
   AWS
 ┌──┼──────┐
 S3 EBS Glacier
```

So it acts as a bridge between your on-premises environment and AWS storage services.

---

# 15. Glacier ⭐

**Amazon S3 Glacier** is designed for **archiving** and long-term data storage.

```text
Frequently Used Data
        ↓
       S3
        ↓
   Less frequently
      accessed
        ↓
     Glacier
        ↓
      Archive
```

Examples:

- Old backups
- Historical records
- Compliance data
- Data that is rarely accessed

Your class emphasized:

> **Glacier = Archive purpose**

---

# 16. Snow Family ⭐

The **AWS Snow Family** is used for transferring large amounts of data, especially when moving data between **on-premises environments and AWS**.

Your class mentioned:

```text
SnowCone
SnowEdge
SnowMobile
```

Conceptually:

```text
On-Premises
     │
     │ Large amount of data
     ↓
Snow Family Device
     │
     ↓
AWS
```

---

# 17. Snow Family vs Internet Transfer

Suppose you have a huge amount of data on-premises.

Instead of transferring everything through the internet:

```text
On-Premises
     │
     │ Internet
     ↓
    AWS
```

AWS Snow devices can physically transport the data:

```text
On-Premises
     │
     ↓
Snow Device
     │
     ↓
AWS
```

This is useful when the dataset is extremely large or network transfer would take too long.

---

# 18. Complete Storage Picture ⭐⭐⭐

Now connect Days 12 and 13:

```text
                    AWS Storage
                        │
       ┌────────────────┼────────────────┐
       ↓                ↓                ↓
      S3               EBS              EFS
   Object              Block             File
   Storage             Storage          Storage
       │                │                │
   Buckets           EC2 Disk       Shared Files
```

And:

```text
                 Other Storage Services
                         │
             ┌───────────┴───────────┐
             ↓                       ↓
       Storage Gateway         Snow Family
             │                       │
       On-prem ↔ AWS          Large data transfer
             
             
             Glacier
                ↓
             Archive
```

---

# ⭐ Day 13 Quick Revision

### EBS
> **Block storage mainly used with EC2.**

### EFS
> **Managed file system that can be mounted by multiple EC2 instances.**

### S3
> **Object storage for files/data.**

### Storage Gateway
> **Connects on-premises environments with AWS storage.**

### Glacier
> **Archive storage for rarely accessed data.**

### Snow Family
> **Physical devices for moving large amounts of data to/from AWS.**

### Most important memory trick:

```text
S3   → Object
EBS  → Block
EFS  → File
Glacier → Archive
Snow → Large Data Transfer
```