Absolutely. Since **Day 1 was mainly AWS introduction**, here are clean notes you can keep for revision/interviews.

# AWS – Day 1 Notes
### Introduction to AWS

## 1. What is AWS?

**AWS (Amazon Web Services)** is a cloud computing platform provided by **Amazon**.

It provides IT resources over the internet instead of requiring us to purchase and maintain physical infrastructure.

Examples:
- Servers
- Storage
- Databases
- Networking
- Security
- Monitoring
- AI/ML services

---

## 2. What is Cloud Computing?

Cloud computing means:

> **Using computing resources over the internet whenever we need them, instead of owning and maintaining them ourselves.**

### Traditional IT

Company needs a server:

`Buy Server → Install → Configure → Maintain → Upgrade`

### Cloud

`AWS → Select required resources → Use → Pay`

---

## 3. Why do we need AWS?

### Before Cloud

Companies had to:

- Buy physical servers
- Build data centers
- Purchase networking equipment
- Maintain hardware
- Hire people for infrastructure
- Pay for unused capacity
- Upgrade hardware manually

This required **high cost and time**.

### With AWS

We can:

- Create servers quickly
- Increase/decrease resources
- Pay based on usage
- Deploy applications globally
- Use managed services
- Avoid maintaining physical hardware

---

# 4. Advantages of AWS

### 1. Cost Effective

You don't necessarily need to purchase expensive physical servers.

You generally **pay for what you use**.

Example:

If you use a server for 5 hours, you pay for that usage rather than buying the entire physical server.

---

### 2. Scalability

AWS allows resources to be increased or decreased according to requirements.

Example:

Normal traffic:

`2 Servers`

High traffic:

`10 Servers`

After traffic decreases:

`2 Servers`

---

### 3. Elasticity

**Elasticity = Automatically adjusting resources according to demand.**

Example:

```text
Traffic increases
       ↓
Resources increase
       ↓
Traffic decreases
       ↓
Resources decrease
```

**Scalability** → Ability to increase/decrease resources.

**Elasticity** → Resources can automatically adjust according to demand.

---

### 4. High Availability

AWS provides infrastructure across multiple locations.

If one infrastructure component fails, another can potentially handle the workload.

Goal:

> **Keep applications available with minimum downtime.**

---

### 5. Global Reach

AWS has infrastructure in many geographical locations around the world.

Therefore applications can be deployed closer to users.

---

### 6. Security

AWS provides many security mechanisms such as:

- IAM
- Encryption
- Firewalls/security groups
- Monitoring
- Access control

But remember:

> **AWS provides security tools, but the customer is also responsible for properly configuring and using them.**

This is called the **Shared Responsibility Model**.

---

# 5. Is AWS Secure?

### Yes.

AWS provides strong security infrastructure.

However:

**AWS security ≠ automatically secure application.**

For example, if you give your AWS account password to someone, AWS cannot prevent you from making that mistake.

So security is shared between:

```text
AWS
+
Customer
```

---

# 6. AWS Shared Responsibility Model

This is an **important interview concept**.

### AWS is responsible for:

> **Security OF the Cloud**

Examples:

- Physical data centers
- Physical servers
- Networking infrastructure
- Hardware
- AWS global infrastructure

### Customer is responsible for:

> **Security IN the Cloud**

Examples:

- Passwords
- IAM permissions
- Application security
- Data
- Operating-system configuration depending on the service
- Security-group configuration

### Easy way to remember:

**AWS → Security OF the Cloud**

**Customer → Security IN the Cloud**

---

# 7. Capital Expenditure vs Operational Expenditure

### Traditional IT → CapEx

**Capital Expenditure**

Company purchases:

- Servers
- Data centers
- Networking hardware

Large upfront investment.

### Cloud → OpEx

**Operational Expenditure**

Company pays for resources/services according to usage.

```text
Traditional IT
     ↓
Buy infrastructure
     ↓
CapEx

AWS
     ↓
Use cloud resources
     ↓
OpEx
```

---

# 8. AWS Pay-as-you-go

AWS generally follows a **pay-as-you-go pricing model**.

You pay based on the resources/services you consume.

This helps companies avoid large upfront infrastructure costs.

---

# 9. AWS Services

AWS provides many services.

Some important ones you'll learn later:

| Requirement | AWS Service |
|---|---|
| Virtual Server | EC2 |
| Storage | S3 |
| Database | RDS |
| Networking | VPC |
| User Access/Security | IAM |
| Serverless Computing | Lambda |
| Monitoring | CloudWatch |

Don't worry about these deeply on Day 1.

---

# 10. Important AWS Terms

### Region

A **Region** is a geographical area containing multiple AWS infrastructure locations.

Example:

```text
Asia Pacific (Mumbai)
Asia Pacific (Hyderabad)
US East (N. Virginia)
Europe (Ireland)
```

---

### Availability Zone (AZ)

An **Availability Zone** is an isolated location within an AWS Region.

Conceptually:

```text
AWS Region
   |
   |--- AZ 1
   |
   |--- AZ 2
   |
   |--- AZ 3
```

Multiple AZs help improve availability and fault tolerance.

---

# 11. Most Important Day-1 Interview Questions

### What is AWS?

AWS is Amazon's cloud computing platform that provides computing, storage, networking, database and other IT resources over the internet.

### Why do companies use AWS?

Because it provides scalable, flexible and highly available infrastructure without requiring companies to purchase and maintain physical infrastructure.

### Is AWS secure?

Yes. AWS provides strong security infrastructure and services, but customers are responsible for securely configuring and using those services.

### What is the Shared Responsibility Model?

AWS is responsible for **security OF the cloud**, while customers are responsible for **security IN the cloud**.

### What is scalability?

The ability to increase or decrease resources according to workload requirements.

### What is elasticity?

The ability to automatically adjust resources according to changing demand.

### What is pay-as-you-go?

A pricing model where customers generally pay based on the resources/services they consume.

---

## ⭐ Day 1 — Remember These 7 Points

```text
AWS
 ↓
Cloud Computing
 ↓
No need to own physical infrastructure
 ↓
Pay-as-you-go
 ↓
Scalable + Elastic
 ↓
Highly Available
 ↓
Shared Responsibility for Security
```

These are enough for your **Day 1 notes**.