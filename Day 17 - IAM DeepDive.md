# AWS – Day 17 Notes
## IAM Deep Dive ⭐⭐⭐

Today you went deeper into **IAM**, especially **MFA, IAM Users, Policies, Console Access and Programmatic Access**.

---

# 1. IAM – Basic Points

**IAM = Identity and Access Management**

- IAM is used mainly for **security and access control**.
- IAM is **Free**.
- IAM is a **Global service**.
- IAM allows you to centrally control access to AWS resources.

```text
                    AWS Account
                        │
                       IAM
                        │
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
       Users         Policies        MFA
          │
          ↓
    AWS Resources
```

---

# 2. Root User ⭐⭐⭐

The **Root User** has full permissions for the AWS account.

```text
Root User
    │
    └── Full Permissions
```

### Important

❌ Don't use the Root User for normal daily activities.

✅ Create IAM users and use appropriate permissions.

---

# 3. IAM User

An **IAM User** can be created under the AWS account and given required permissions.

Example from your class:

```text
IAM Users

Abhi    → EC2
Sravani → S3, IAM
Santosh → RDS
Srinu   → CloudFront
Sagar   → Admin (Except Billing)
```

Different users can have different permissions.

---

# 4. Permissions → Policies ⭐

Permissions are generally given through **IAM Policies**.

```text
IAM User
    ↓
Policy
    ↓
Permissions
    ↓
AWS Resource
```

Example:

```text
Abhi
 ↓
EC2 Policy
 ↓
EC2 Access
```

Policies can be **attached or detached** from IAM users.

---

# 5. MFA ⭐⭐⭐

**MFA = Multi-Factor Authentication**

Your class mentioned using an authenticator such as **Google Authenticator**.

Login flow:

```text
AWS Login
   ↓
Email / Password
   ↓
MFA Code
   ↓
AWS Console
```

### Recommended

Enable MFA for:

- Root User
- IAM Users

MFA provides an additional authentication factor.

---

# 6. Two Ways to Access AWS ⭐⭐⭐

Your instructor explained two major access methods:

```text
                AWS Access
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
    Console Access      Programmatic Access
       (GUI)              (CLI / SDK)
```

---

# 7. Console Access

AWS Console is the **web-based GUI**.

```text
Browser
   ↓
AWS Console
   ↓
Login
   ↓
IAM User / Root User
```

Authentication generally uses:

```text
Username / Email
        +
Password
        +
MFA (when enabled)
```

---

# 8. Programmatic Access ⭐⭐⭐

Programmatic access is used by:

- AWS CLI
- AWS SDKs
- Developer tools
- Applications/scripts

It uses **Access Keys**.

```text
Application / CLI
       ↓
Access Key ID
       +
Secret Access Key
       ↓
AWS
```

---

# 9. Access Key and Secret Access Key

An IAM user's access key consists of:

```text
Access Key ID
       +
Secret Access Key
       ↓
One Access Key Pair
```

Example:

```text
Access Key ID     → AKIA........
Secret Access Key → ************
```

### Important ⭐

- Access keys are **user-specific**.
- Don't share access keys with anyone.
- Create keys only when required.
- Don't create unnecessary keys.

---

# 10. Lost Secret Access Key

Your class highlighted an important point:

> If you lose the Secret Access Key, you cannot retrieve the same secret key again.

You can:

```text
Delete / deactivate old key
        ↓
Create new access key
        ↓
Get new credentials
```

The old secret key cannot be recovered.

### Important

**Secret Access Key is shown only once when it is created.**

So store it securely.

---

# 11. Maximum Access Keys

An IAM user can have:

> **Maximum 2 access-key pairs**

```text
IAM User
   │
   ├── Access Key 1
   └── Access Key 2
```

This is useful when rotating credentials.

---

# 12. Root Access Keys ⭐

Your instructor specifically mentioned:

> **Don't create Access Keys for the Root User.**

For normal programmatic access, use an IAM identity with the required permissions instead.

---

# 13. Console vs Programmatic Access

| Console Access | Programmatic Access |
|---|---|
| Web GUI | CLI / SDK / Developer tools |
| Username + Password | Access Key + Secret Access Key |
| Browser | Commands / Code |
| Human interaction | Automation / Applications |

---

# 14. IAM Security Best Practices ⭐⭐⭐

Remember these:

```text
1. Don't use Root for daily work
2. Enable MFA
3. Give minimum required permissions
4. Don't share passwords
5. Don't share access keys
6. Don't create unnecessary access keys
7. Rotate/delete credentials when required
```

---

# ⭐ Day 17 Quick Revision

```text
                    IAM
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
     Users        Policies         MFA
       │             │
       ↓             ↓
 Permissions     Access Control
       │
       ↓
 AWS Resources
```

### Access methods

```text
                 AWS
                  │
       ┌──────────┴──────────┐
       ↓                     ↓
 Console Access       Programmatic Access
       ↓                     ↓
Username/Password       Access Keys
       ↓                     ↓
     MFA*              CLI / SDK / Apps
```

**Most important interview points:**

- **IAM → Security and access control**
- **Root User → Full permissions**
- **IAM User → Controlled permissions**
- **Policy → Defines permissions**
- **MFA → Additional authentication factor**
- **Console → GUI access**
- **Access Keys → Programmatic access**
- **Secret Access Key → Cannot be retrieved again after creation**