# AWS – Day 16 Notes

Today you learned **CloudWatch, CloudTrail, AWS Config, SNS, Metrics, Alarms and AWS Support**.

---

## 1. Amazon CloudWatch ⭐⭐⭐

**CloudWatch = Monitoring service**

It is used to monitor AWS resources such as:

- EC2
- ELB
- RDS
- S3
- ASG (Auto Scaling Group)

```text
AWS Resources
     │
     ↓
 CloudWatch
     │
     ├── Metrics
     ├── Logs
     └── Alarms
```

### What does CloudWatch monitor?

Mainly **performance and operational metrics**.

Example:

```text
EC2
 ├── CPU Usage
 ├── Network
 ├── Disk
 └── Other metrics
```

---

# 2. CloudWatch Metrics ⭐

A **metric** is a measurement of something happening in a resource.

Example:

```text
EC2
CPU Utilization

11:00 → 40%
11:05 → 65%
11:10 → 80%
11:15 → 92%
```

CloudWatch collects these data points over time.

Common metrics:

- CPU utilization
- Network usage
- Request count
- Latency
- Memory* 

\*Memory monitoring generally requires additional monitoring/agent setup; it isn't a standard EC2 basic metric.

---

# 3. Basic vs Detailed Monitoring

### Basic Monitoring

According to your class:

```text
Every 5 minutes
FREE
```

### Detailed Monitoring

```text
Every 1 minute
CHARGED
```

So:

```text
Basic    → 5 min
Detailed → 1 min
```

---

# 4. CloudWatch Alarms ⭐⭐⭐

An **Alarm** watches a metric and performs an action when a defined condition is met.

Example:

```text
EC2
 ↓
CPU > 90%
 ↓
CloudWatch Alarm
 ↓
SNS
 ↓
Email / SMS
```

Your instructor's example:

```text
CPU > 90%
     ↓
   Alarm
     ↓
    SNS
   ↙   ↘
Email   SMS
```

---

# 5. SNS

**SNS = Simple Notification Service**

It can send notifications.

Example:

```text
CloudWatch Alarm
       ↓
      SNS
     ↙   ↘
 Email    SMS
```

So remember:

> **CloudWatch detects → Alarm triggers → SNS notifies**

---

# 6. CloudTrail ⭐⭐⭐

**CloudTrail = AWS activity/audit logging service**

Your class described it as monitoring the AWS environment and recording/tracking/auditing activities.

Example:

```text
User
 ↓
Creates EC2
 ↓
CloudTrail
 ↓
Records the API activity
```

It helps answer questions such as:

- Who performed an action?
- What action was performed?
- When was it performed?
- Which AWS resource was affected?

### Easy memory

> **CloudWatch → Performance**

> **CloudTrail → User/API activity**

---

# 7. AWS Config

**AWS Config** is used to monitor and track **changes/configuration of AWS resources**.

Example:

```text
EC2 Configuration
      ↓
Changed
      ↓
AWS Config
      ↓
Records configuration change
```

### Difference

```text
CloudWatch → How is the resource performing?

CloudTrail  → Who did what?

Config      → What configuration changed?
```

This distinction is very important. ⭐

---

# 8. CloudWatch vs CloudTrail vs Config

| Service | Main purpose |
|---|---|
| **CloudWatch** | Monitor performance/metrics |
| **CloudTrail** | Track AWS API/user activity |
| **AWS Config** | Track resource configuration |

Easy way:

```text
CloudWatch → Performance
CloudTrail  → Activity
Config      → Configuration
```

---

# 9. AWS Support

Your instructor introduced different AWS Support plans:

```text
AWS Support
     │
     ├── Basic
     ├── Developer
     ├── Business
     └── Enterprise
```

The class notes mentioned:

- **Basic** → Free
- **Developer** → $100
- **Business**
- **Enterprise** → $15,000

> Support-plan pricing can change, so treat the numbers in the class notes as the values discussed in your course, not permanent AWS pricing.

---

# 10. SLA ⭐

**SLA = Service Level Agreement**

It defines the level of service/availability that the provider commits to under specified terms.

Your class mentioned **15 minutes** in the support discussion.

---

# ⭐ Day 16 Quick Revision

```text
CloudWatch
   ↓
Metrics → CPU, Network, etc.
   ↓
Alarm
   ↓
SNS
   ↓
Email / SMS
```

And:

```text
CloudWatch → Performance
CloudTrail  → Activity / Audit
Config      → Configuration Changes
SNS         → Notifications
```

### Most important interview point

**Q: Difference between CloudWatch, CloudTrail and Config?**

> **CloudWatch monitors performance, CloudTrail records AWS activity/API calls, and AWS Config tracks resource configurations and their changes.**