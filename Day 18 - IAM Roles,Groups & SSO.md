# AWS – Day 18 Notes
## IAM Groups, Policies, Roles, SSO & Cross-Account Access

Today was a **deep dive into IAM**.

---

# 1. IAM Groups ⭐⭐⭐

**IAM Group = Collection of IAM Users**

```text
IAM Group
   │
   ├── User 1
   ├── User 2
   ├── User 3
   └── User 4
```

Groups are useful when multiple users need the same permissions.

### Important points

- A group can contain multiple IAM users.
- You can attach/detach policies to a group.
- Users inherit the group's permissions.
- One IAM user can belong to multiple groups.
- A group cannot contain another group (**nested groups are not supported**).
- Access keys are for **IAM users**, not groups.
- A newly created IAM user has no permissions by default unless permissions are granted.

---

# 2. IAM Group Example

Suppose:

```text
DevOps Group
   │
   ├── Hari
   ├── Dev
   ├── Sagar
   └── Santosh
```

Attach:

```text
DevOps Group
      ↓
EC2 + RDS + S3 permissions
```

All users in that group receive those permissions.

This is easier than attaching the same policy individually to every user.

---

# 3. IAM Policies ⭐⭐⭐

**Policy = Document that defines permissions.**

```text
User / Group
     ↓
 Policy
     ↓
Permissions
     ↓
AWS Resources
```

Policies are written in **JSON format**.

Example concept:

```text
Allow → EC2
Allow → S3
Deny  → RDS
```

---

# 4. Managed Policy

**Managed Policy = Policy created and managed by AWS.**

AWS provides many ready-made policies.

Examples from your class:

```text
AmazonEC2FullAccess
AmazonS3ReadOnlyAccess
```

These are easier to attach to users/groups.

---

# 5. Inline Policy

**Inline Policy = Policy created and managed directly by the customer for a specific identity.**

```text
IAM User
   ↓
Inline Policy
```

So:

```text
Managed Policy → AWS-managed/reusable policy

Inline Policy  → Directly embedded custom policy
```

---

# 6. User-Based vs Resource-Based Permissions

Your instructor introduced two permission concepts:

### User-based permissions

Permissions are attached to an IAM identity.

```text
IAM User
   ↓
Policy
   ↓
EC2 / S3 etc.
```

### Resource-based permissions

Permissions are defined at the AWS resource level where supported.

```text
Resource
   ↓
Resource Policy
   ↓
Who can access it?
```

---

# 7. ARN ⭐

**ARN = Amazon Resource Name**

ARN uniquely identifies AWS resources.

```text
ARN
 ↓
Amazon Resource Name
```

It is used in IAM policies to identify resources.

---

# 8. IAM Roles ⭐⭐⭐

This was one of the major topics today.

**IAM Role = Temporary access without using long-term credentials.**

```text
IAM Role
   ↓
Temporary permissions
   ↓
AWS Resource
```

---

# 9. EC2 + IAM Role ⭐⭐⭐

Suppose an EC2 instance needs access to S3.

### Bad approach ❌

Put AWS access keys inside the EC2 machine.

```text
EC2
 ↓
Access Keys
 ↓
S3
```

### Better approach ✅

Attach an IAM Role to EC2.

```text
EC2
 ↓
IAM Role
 ↓
S3
```

The application can then access AWS services according to the role's permissions.

---

# 10. Example

```text
             IAM Role
          KiranROLE
              │
         S3Policy
              │
              ↓
          EC2 Instance
              │
              ↓
              S3
```

The EC2 application can access S3 without storing permanent access keys on the machine.

---

# 11. Important IAM Role Points

From today's class:

- Roles are used for temporary access.
- Roles don't require you to configure long-term access keys on the machine.
- Permissions are attached to the role.
- An EC2 instance can have a role attached.
- A role can be used by multiple EC2 instances.

---

# 12. IAM Role for Applications ⭐

Suppose an application running on EC2 needs S3.

```text
EC2
 │
 ├── Java Application
 │
 └── IAM Role
        │
        ↓
       S3
```

The application doesn't need to store AWS access keys.

This is a **very important AWS concept for backend developers**. ⭐

---

# 13. SSO / Federation ⭐⭐⭐

Your class then introduced **Single Sign-On (SSO)** and federation.

Suppose a company already has users:

```text
Company
   │
Domain Users
   ├── user1
   ├── user2
   ├── user3
   └── userN
```

The company may use a directory service such as:

- Active Directory
- LDAP

Instead of creating separate AWS credentials for every employee, identity federation/SSO can allow employees to access AWS using their existing company identity.

---

# 14. SSO Flow

```text
Company User
     ↓
Company Login
     ↓
SSO / Identity Provider
     ↓
AWS
     ↓
IAM Role
     ↓
AWS Resources
```

Examples of identity providers mentioned:

- Okta
- OAuth
- Active Directory

---

# 15. Why SSO?

Without SSO:

```text
Company Account
      ↓
AWS Account
      ↓
Separate AWS credentials
```

With SSO:

```text
Company Credentials
       ↓
      SSO
       ↓
      AWS
```

So users can use their existing organizational identity.

---

# 16. IAM Role + SSO

The important relationship is:

```text
Company User
      ↓
     SSO
      ↓
IAM Role
      ↓
AWS Resources
```

The user receives permissions through the role.

---

# 17. Cross-Account IAM Role ⭐⭐⭐

The last part of today's class introduced **cross-account access**.

Suppose:

```text
AWS Account A
      │
      │
      ↓
AWS Account B
```

A user in Account A may need to access resources in Account B.

Instead of sharing credentials, Account B can create a role that Account A is allowed to assume.

---

# 18. Cross-Account Role Flow

```text
Account A
IAM User
   │
   │ Assume Role
   ↓
Account B
IAM Role
   │
   ↓
S3 / RDS / Lambda
```

Example from your class:

```text
Reyaz's AWS Account
        │
        │ IAM Role
        ↓
Khalid's AWS Account
```

The role provides controlled access to the required resources.

---

# 19. Why Roles Are Important ⭐⭐⭐

Think of the three major IAM mechanisms like this:

```text
IAM User
   ↓
Person / Identity

IAM Group
   ↓
Collection of Users

IAM Role
   ↓
Temporary / delegated access
```

---

# ⭐ Day 18 Quick Revision

```text
                       IAM
                        │
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
      Users           Groups           Roles
        │               │               │
        ↓               ↓               ↓
    Individual      Collection       Temporary/
    identity         of users        delegated access
        │               │               │
        └───────────────┼───────────────┘
                        ↓
                     Policies
                        ↓
                   Permissions
                        ↓
                 AWS Resources
```

### Most important points

- **IAM Group** → Collection of IAM users.
- **Policy** → Defines permissions.
- **Managed Policy** → AWS-managed policy.
- **Inline Policy** → Customer-created policy embedded with an identity.
- **IAM Role** → Temporary/delegated access without storing long-term credentials.
- **EC2 Role** → Allows EC2 applications to access AWS services securely.
- **SSO/Federation** → Use existing organizational identity to access AWS.
- **Cross-account Role** → Allows controlled access between AWS accounts.
- **ARN** → Amazon Resource Name used to identify AWS resources.