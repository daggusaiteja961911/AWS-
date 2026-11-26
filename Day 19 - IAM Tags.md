You're right. **Only Day 19 notes, based strictly on the image.**

# Day 19 — IAM Tags & AWS Organizations

## 1. IAM Tags

### What are Tags?
- Tags are **Key-Value pairs**.
- Tags contain information about an AWS resource.
- Tags are used for **identification purposes**.
- Tags are **not IAM-specific**; they are used throughout AWS.
- Tags are used to **manage AWS resources**.
- Tags can also be used for **Cost Optimization**.

### Example

```text
EC2

Name = WebServer
```

Here:
- **Key = Name**
- **Value = WebServer**

Another example:

```text
Jean

Tag:
Price = 10k
Size = L
Brand = Levi
```

---

## 2. Using Tags with IAM Users

Suppose there are **500 IAM Users**.

Users can be grouped using tags:

```text
Team = HR
Team = DevOps
```

Example:

```text
500 IAM Users

HR
DevOps
Architects
DB Admins
```

### Hard Worker
- Manually create/manage 500 users.
- Delete HR users manually.

### Smart Worker
Use tags to identify users.

Example:

```text
Key = Team
Value = HR
```

Then automation can identify/delete all IAM users where:

```text
Team = HR
```

The trainer mentioned **Python** for this type of automation.

---

## 3. Tags and EC2

Example:

```text
100 EC2 Instances
        ↓
      Tags
        ↓
     DevOps
```

Tags can help identify and manage large numbers of resources.

### Tag Limit

The image mentions:

**Per Resource = 50 Tags**

---

# 4. IAM Service

IAM service contains:

- IAM Users
- Groups
- Policies
- Roles

---

# 5. AWS Organizations

AWS Organizations is used for **managing multiple AWS accounts**.

### Purpose

Instead of managing many AWS accounts separately, they can be organized centrally.

```text
Management Account
        |
   ----------------
   |      |       |
 Account Account Account
```

The image shows:

- Root Account / Management Account
- Multiple member accounts
- SCPs

---

# 6. SCP

SCP = **Service Control Policy**

SCPs are used in AWS Organizations to control permissions for member accounts.

---

# 7. Reports

The image also mentions:

- **Analyze**
- **Generate Reports**
- **Credentials Report**

These can be used for IAM/account-related analysis and reporting.

---

## Day 19 — Quick Revision

```text
Tags
 ↓
Key + Value
 ↓
Identification
 ↓
Resource Management
 ↓
Cost Optimization
```

```text
AWS Organizations
 ↓
Management Account
 ↓
Multiple Member Accounts
 ↓
SCPs
```

**Main Day 19 topics:**
1. IAM Tags
2. Key-Value pairs
3. Resource identification
4. Cost optimization
5. Tag-based IAM user management
6. Python automation
7. 50 tags per resource
8. IAM Service
9. AWS Organizations
10. Management/Member Accounts
11. SCP
12. Reports / Credential Reports