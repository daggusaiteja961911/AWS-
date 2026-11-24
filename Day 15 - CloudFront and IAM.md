# AWS – Day 15 Notes

Today you learned **CloudFront (CDN)** and **IAM (Identity and Access Management)**.

---

## 1. Amazon CloudFront ⭐⭐⭐

**CloudFront = CDN (Content Delivery Network)**

Its main purpose is to **deliver content faster to users** by caching content at locations closer to them.

### Without CloudFront

```text
User – Ireland
       │
       │ High Latency
       ↓
   AWS Origin
   Mumbai
```

A user far from the origin may experience higher latency.

### With CloudFront

```text
                 CloudFront
              ┌──────────────┐
              │ Edge Location│
              │    Cache     │
              └──────┬───────┘
                     ↓
User ───────────→ Edge Location
                     │
                     ↓
                  Origin
                  (EC2)
```

The user's request can be served from the nearby **Edge Location** when the content is already cached.

---

## 2. CloudFront Components

### Origin

The original source of the content.

Example:

```text
Origin → EC2 / S3
```

Your instructor's example:

```text
Application
    EC2
   Origin
   Mumbai
```

### Edge Location

A location where CloudFront caches content closer to users.

```text
User
 ↓
Edge Location
 ↓
Cache
```

### CDN

**CDN = Content Delivery Network**

CloudFront is AWS's CDN service.

---

## 3. Cache ⭐

Suppose the user requests:

```text
puppy.jpg
```

First request:

```text
User
 ↓
Edge Location
 ↓
Origin
 ↓
puppy.jpg
```

The content can then be cached at the Edge Location.

Next request:

```text
User
 ↓
Edge Location
 ↓
puppy.jpg
```

So the request may not need to travel all the way to the origin.

---

## 4. TTL ⭐

**TTL = Time To Live**

It determines how long cached content remains valid before it needs to be refreshed/revalidated.

Your instructor's example:

```text
TTL = 12 hours
```

After the cache period expires, CloudFront can retrieve/refresh the content from the origin.

---

## 5. Delete / Invalidate Cache

If you update content at the origin, an old version may still exist in the CloudFront cache.

You can use **cache invalidation** to remove cached content so the updated content can be fetched.

```text
Origin
  │
Updated file
  │
  ↓
Invalidate Cache
  │
  ↓
CloudFront gets updated content
```

---

## 6. CloudFront Architecture ⭐⭐⭐

```text
                 CloudFront
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   Edge Location  Edge Location  Edge Location
     Ireland        Tokyo          Sydney
       │             │             │
       └─────────────┼─────────────┘
                     ↓
                   Origin
                  EC2 / S3
```

### Key benefit

**Lower latency + faster content delivery.**

---

# 7. IAM ⭐⭐⭐

**IAM = Identity and Access Management**

IAM is used to **control access to AWS resources**.

```text
IAM
 │
 ├── Users
 ├── Permissions
 └── Access Control
```

Your instructor's key point:

> You can control AWS resources using IAM by giving appropriate permissions to IAM users.

---

# 8. Root User ⭐

When an AWS account is created, there is a **root user**.

```text
AWS Account
     │
     ↓
Root User
     │
     ├── Full permissions
     │
     └── IAM Users
```

The root user has very high-level/full access to the AWS account.

**Best practice:** Don't use the root user for normal daily AWS operations.

---

# 9. IAM User

An **IAM user** is an identity created within an AWS account.

Example from your class:

```text
Root Account
     │
     ├── IAM User 1 → EC2
     ├── IAM User 2 → S3, Lambda
     ├── IAM User 3 → RDS, VPC
     └── IAM User 4 → EFS
```

Different users can receive different permissions.

---

# 10. Root User vs IAM User

| Root User | IAM User |
|---|---|
| Full account-level access | Limited permissions can be given |
| Created with AWS account | Created by administrator |
| Very powerful | Permission-based |
| Avoid daily use | Used for normal operations |

---

# 11. IAM Permissions ⭐⭐⭐

Example:

```text
Rahul  → EC2
Kranthi → S3 + Lambda
Vishnu → RDS + VPC
Nitesh → EFS
```

So users don't necessarily get access to everything.

This follows the idea of **least privilege**:

> Give a user only the permissions they actually need.

---

# 12. AWS Organizations

Your class also introduced **AWS Organizations**.

It can be used to manage multiple AWS accounts centrally.

```text
             Organization
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     DevOps      AWS      Marketing
     Account    Account    Account
        │         │         │
      IAM       IAM       IAM
      Users     Users     Users
```

---

# 13. SCP ⭐

**SCP = Service Control Policy**

SCPs are used with **AWS Organizations** to control what actions member accounts can perform.

```text
Organization
     │
    SCP
     │
     ├── DevOps Account
     ├── AWS Account
     └── Marketing Account
```

Think of SCP as an **organization-level permission boundary/control**.

---

# ⭐ Day 15 Quick Revision

| Topic | Meaning |
|---|---|
| **CloudFront** | AWS CDN |
| **CDN** | Content Delivery Network |
| **Edge Location** | Location where content can be cached |
| **Origin** | Original source of content |
| **Cache** | Temporarily stored content |
| **TTL** | Time To Live for cached content |
| **Invalidation** | Remove cached content |
| **IAM** | Identity and Access Management |
| **Root User** | Full account-level access |
| **IAM User** | User with assigned permissions |
| **Organizations** | Manage multiple AWS accounts |
| **SCP** | Service Control Policy |

### Most important flows

```text
USER
 ↓
CloudFront
 ↓
Edge Location / Cache
 ↓
Origin (EC2 / S3)
```

```text
AWS Account
     ↓
    IAM
     ↓
Users + Permissions
     ↓
AWS Resources
```