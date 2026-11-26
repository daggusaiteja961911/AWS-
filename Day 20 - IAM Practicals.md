# AWS Day 20 — IAM Practicals & AWS Organizations

Today’s practicals focused mainly on **IAM Policies, Roles, Users, Switch Roles, and AWS Organizations**.

### 1. Create IAM Policy

An **IAM Policy** defines what actions a user, group, or role is allowed or denied to perform on AWS resources.

Basic flow:

```text
IAM
 ↓
Policies
 ↓
Create Policy
 ↓
Choose Service
 ↓
Select Permissions
 ↓
Specify Resources
 ↓
Review
 ↓
Create Policy
```

### 2. Visual Editor

AWS provides a **Visual Editor** to create policies without manually writing JSON.

You select:

- **Service** → Example: S3
- **Actions** → What the identity can do
- **Resources** → Which resources it can access
- **Conditions** → Optional restrictions

The Visual Editor generates the policy structure for you.

---

## 3. IAM Roles

An **IAM Role** provides permissions that can be temporarily assumed by a trusted entity.

### Role → AWS Service

A role can be created for an AWS service.

Example:

```text
EC2
 ↓
Assume IAM Role
 ↓
Access AWS Services
```

The EC2 instance can use the role's permissions **without storing AWS access keys inside the instance**.

### Role → AWS Account

A role can also allow access from another AWS account.

```text
Account A
   ↓
Assume Role
   ↓
Account B
   ↓
AWS Resources
```

### Temporary Access

One important advantage of IAM Roles:

**Temporary access can be provided without giving permanent credentials.**

---

# 4. IAM Users Practical

### Test 1

Create IAM user:

```text
test1
 ↓
IAMFullAccess
```

`test1` gets broad IAM permissions.

Login as `test1` and verify the permissions.

---

### Test 2

Create IAM user:

```text
test2
 ↓
IAMReadOnly
```

`test2` gets read-only IAM permissions.

Login as `test2` and verify that actions requiring write permissions are not allowed.

---

## 5. Custom / Inline Policy

The practical also covered creating a custom policy with limited permissions.

The required user should be able to:

- Create users
- List users
- Get users
- List policies

But should **not automatically receive full IAM permissions**.

This demonstrates the principle of giving only the permissions required.

---

# 6. Test 3 — Custom Policy

Create:

```text
test3
   ↓
Custom Policy
```

The custom policy created during the practical is attached to `test3`.

Then:

```text
Logout
   ↓
Login as test3
   ↓
Verify permissions
```

Only the actions specified in the custom policy should be available.

---

# 7. Switch Roles

**Switch Role** allows a user to switch from their current IAM identity to another IAM Role.

The practical mentioned using the **AWS Account ID** while switching roles.

Concept:

```text
Current User
     ↓
Switch Role
     ↓
Account ID + Role
     ↓
Temporary Role Permissions
```

This is useful when users need temporary access to resources with different permissions.

---

# 8. AWS Organizations

**AWS Organizations** is used to centrally manage multiple AWS accounts.

Basic structure:

```text
AWS Organization
       │
       ├── Account 1
       ├── Account 2
       ├── Account 3
       └── Account 4
```

It helps with centralized management of multiple AWS accounts.

---

# 9. Optional — Federation with Okta

The instructor also mentioned an optional practical:

```text
Okta
  ↓
Federation
  ↓
AWS
```

The idea is to create a free-tier Okta account and configure **federation with AWS**.

### Day 20 Key Points

- **Policy** → Defines permissions.
- **Visual Editor** → Helps create policies without manually writing JSON.
- **Role** → Provides temporary permissions through role assumption.
- **IAM User** → Individual AWS identity.
- **Custom Policy** → Specific permissions according to requirements.
- **Switch Role** → Temporarily use another role's permissions.
- **AWS Organizations** → Centrally manage multiple AWS accounts.
- **Federation** → External identity provider such as Okta can be integrated with AWS.