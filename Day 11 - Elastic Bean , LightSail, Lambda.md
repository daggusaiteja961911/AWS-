# AWS – Day 11 Notes
## EC2, ELB, Elastic Beanstalk, Lightsail & Lambda

Day 11 introduced several important AWS services and how they are used together.

---

# 1. EC2 ⭐⭐⭐

**EC2 = Elastic Compute Cloud**

EC2 provides **virtual servers** in AWS.

```text
AWS
 ↓
EC2
 ↓
EC2 Instance
 ↓
Virtual Server
```

Your class uses:

> **Server = Instance**

So when someone says:

> "Launch an EC2 instance"

it means:

> **Create/start a virtual server in AWS.**

---

# 2. EC2 is a Regional Service

EC2 instances are launched in a specific AWS Region and Availability Zone.

```text
AWS Region
     │
     ├── AZ-1a
     │     └── EC2
     │
     ├── AZ-1b
     │     └── EC2
     │
     └── AZ-1c
           └── EC2
```

This connects directly with **Day 9: Regions & Availability Zones**.

---

# 3. Load Balancer ⭐⭐⭐

A **Load Balancer** distributes incoming traffic across multiple servers.

```text
                  Client
                    ↓
               Load Balancer
               /     |     \
              ↓      ↓      ↓
            EC2     EC2     EC2
```

Instead of sending all requests to one server, traffic is distributed among multiple instances.

---

# 4. ELB – Elastic Load Balancing

**ELB = Elastic Load Balancing**

AWS provides managed load-balancing services.

Your class describes ELB as distributing traffic across multiple EC2 instances, potentially across multiple AZs.

```text
                  ELB
                   ↓
        ┌──────────┼──────────┐
        ↓          ↓          ↓
      EC2         EC2        EC2
      AZ-1        AZ-2       AZ-3
```

### Benefits mentioned in class

ELB is managed by AWS and supports:

- High Availability
- Scalability
- Performance

---

# 5. You Don't Log in to ELB

An ELB is not a normal server where you log in and run commands.

Instead, you access it using its **DNS name**.

```text
Client
   ↓
ELB DNS Name
   ↓
Load Balancer
   ↓
EC2 Instances
```

---

# 6. Elastic Beanstalk ⭐

Your class describes:

> **Elastic Beanstalk = Easy and quick deployment of applications in AWS**

It is a **PaaS-style service**.

Instead of manually managing many infrastructure details, you provide your application and select the platform.

Example:

```text
Java Application
       ↓
Elastic Beanstalk
       ↓
AWS Infrastructure
       ↓
Application running
```

Your class mentions platforms such as:

- Java / Tomcat
- .NET
- Docker
- Python
- Go

---

# 7. EC2 vs Elastic Beanstalk

### EC2

You have more control.

```text
Application
     ↓
OS
     ↓
EC2
```

You configure and manage the server environment.

### Elastic Beanstalk

You mainly focus on deploying the application.

```text
Application
     ↓
Elastic Beanstalk
     ↓
AWS manages more of the underlying environment
```

Easy memory:

> **EC2 → More control**

> **Elastic Beanstalk → Easier application deployment**

---

# 8. AWS Lightsail

Your class also introduced **Lightsail**.

It is useful when you want to quickly create a virtual private server with many common components/configurations made easier to set up.

Your instructor mentioned examples such as:

```text
WordPress
GitLab
Node.js
Joomla
Drupal
Django
Ghost
Nginx
Redis
etc.
```

### Important point from your class

> **Lightsail → Easy setup, but it does not provide Auto Scaling in the same way as an EC2 Auto Scaling architecture.**

---

# 9. Lambda ⭐⭐⭐

**AWS Lambda** is a **serverless compute service**.

Your class describes:

> **Lambda is serverless.**

The key idea:

```text
You
 ↓
Lambda Function
 ↓
AWS manages the servers
```

You don't create/manage an EC2 server for the Lambda function.

---

# 10. Lambda Function

You create a function and provide code.

Your class mentions:

- Java
- Python
- Ruby
- etc.

```text
Create Function
       ↓
Write Code
       ↓
Lambda
```

---

# 11. Lambda is Event/Trigger Based

Lambda can be **invoked when a trigger/event occurs**.

Your class example:

```text
Event / Trigger
      ↓
   Lambda
      ↓
Execute Code
```

For example:

```text
EC2 Event
    ↓
Trigger
    ↓
Lambda
    ↓
Execute Python code
```

---

# 12. Lambda Automation Example ⭐

Your instructor gave a scheduling example.

Suppose you don't want EC2 instances running at night.

```text
9 PM
 ↓
Lambda
 ↓
Stop EC2 instances
```

Then:

```text
9 AM
 ↓
Lambda
 ↓
Start EC2 instances
```

So:

```text
              Schedule
                 │
        ┌────────┴────────┐
        ↓                 ↓
       9 PM              9 AM
        ↓                 ↓
 Stop Function       Start Function
        ↓                 ↓
 Stop EC2            Start EC2
```

This can help avoid running instances when they're not needed.

---

# 13. Lambda Lifecycle Example

Your class also shows:

```text
EC2
 ↓
Event
 ↓
Trigger
 ↓
Lambda
 ↓
Execute Code
```

For example, an event could trigger Lambda to perform an automated action on an AWS resource.

---

# 14. ELB + EC2 + Multiple AZs ⭐⭐⭐

This is the important architecture from today's class:

```text
                         Client
                           ↓
                      ELB DNS Name
                           ↓
                    Load Balancer
                     /     |     \
                    ↓      ↓      ↓
                  EC2     EC2     EC2
                  1a       1b      1c
```

This gives you:

- Traffic distribution
- Multiple instances
- Multiple AZs
- Better availability
- Scalability

---

# 15. Where Today's Services Fit

```text
                    AWS
                     │
       ┌─────────────┼──────────────┐
       ↓             ↓              ↓
      EC2           ELB           Lambda
       │             │              │
 Virtual Server   Traffic       Serverless
                 Distribution    Functions
```

And:

```text
Application Deployment
        │
        ├── EC2
        │    → More control
        │
        ├── Elastic Beanstalk
        │    → Easier deployment
        │
        └── Lightsail
             → Simplified VPS setup
```

---

# ⭐ Day 11 Quick Revision

| Service | Main Purpose |
|---|---|
| **EC2** | Virtual server |
| **ELB** | Distribute traffic |
| **Elastic Beanstalk** | Easy application deployment |
| **Lightsail** | Simplified virtual server setup |
| **Lambda** | Serverless/event-driven code execution |

### Most important:

```text
EC2
→ Server

ELB
→ Distribute traffic

Elastic Beanstalk
→ Deploy application easily

Lightsail
→ Simple VPS-style setup

Lambda
→ Run code without managing servers
```

### Overall architecture

```text
                       Client
                         ↓
                    ELB / DNS
                         ↓
              ┌──────────┼──────────┐
              ↓          ↓          ↓
             EC2        EC2        EC2
             AZ-1       AZ-2       AZ-3
                         ↑
                  Auto Scaling
                         
        Event/Schedule
              ↓
           Lambda
              ↓
        Automation
```