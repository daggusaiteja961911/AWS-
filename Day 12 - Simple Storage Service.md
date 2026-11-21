# AWS – Day 12 Notes
## S3 – Simple Storage Service

Today you learned about **Amazon S3**, AWS's object storage service.

---

# 1. What is S3? ⭐⭐⭐

**S3 = Simple Storage Service**

S3 is used to **store files/objects** in AWS.

```text
User
 ↓
Amazon S3
 ↓
Store / Upload / Download
 ↓
Files
```

Examples of files:

- Images
- Videos
- PDFs
- HTML files
- Documents
- Backups
- Logs

---

# 2. S3 is Object-Based Storage ⭐

S3 uses **object storage**.

The basic structure is:

```text
S3
 │
 └── Bucket
       │
       ├── Object
       ├── Object
       └── Object
```

### Easy comparison

| Traditional Storage | S3 |
|---|---|
| Folder | Bucket |
| File | Object |
| File name | Key |

Your class example:

```text
Windows
   ↓
Folder
   ↓
Files
   ↓
boom.mp4
```

Equivalent S3 concept:

```text
S3
 ↓
Bucket
 ↓
Objects
 ↓
Key
```

---

# 3. Bucket ⭐⭐⭐

A **Bucket** is a container for objects.

```text
Bucket
 ├── image.jpg
 ├── video.mp4
 ├── resume.pdf
 └── index.html
```

Think:

> **Bucket = container for objects**

---

# 4. Object

An **Object** is the actual file/data stored in S3.

```text
Bucket
   │
   ├── photo.jpg      ← Object
   ├── video.mp4      ← Object
   └── resume.pdf     ← Object
```

---

# 5. Key ⭐

The **Key** identifies an object within a bucket.

For a simple object:

```text
Bucket
   ↓
boom.mp4
   ↑
  Key
```

In practical S3 usage, keys can also contain path-like prefixes:

```text
images/profile/photo.jpg
```

Here the entire string is the object's **key**.

---

# 6. Upload and Download

S3 allows you to:

```text
        S3
       /  \
      ↓    ↑
 Upload    Download
      \    /
       Files
```

You can upload an object and later download/access it.

---

# 7. Can we Run Programs in S3? ❌

S3 is primarily **storage**, not a server for executing applications.

According to today's class:

```text
S3
 │
 ├── Store files       ✅
 ├── Download files    ✅
 ├── Install OS        ❌
 ├── Install DB        ❌
 └── Run .py/.NET etc. ❌
```

For running applications, services such as **EC2** or **Lambda** are used instead.

---

# 8. S3 is Serverless

S3 is a **managed/serverless storage service**.

You don't manage:

- Physical servers
- Operating systems
- Storage hardware
- Data-center infrastructure

AWS manages the underlying infrastructure.

```text
You
 ↓
S3
 ↓
AWS manages infrastructure
```

---

# 9. S3 and High Availability

AWS manages the underlying infrastructure needed for S3's durability, availability, and scalability.

So you don't need to manually create:

```text
Server 1
Server 2
Server 3
...
```

just to store your files.

---

# 10. S3 and Regions ⭐

Your class notes:

> **S3 is Global**

This needs a small clarification:

**Amazon S3 is a global AWS service, but S3 buckets are created in a specific AWS Region.**

For example:

```text
AWS
 │
 ├── Mumbai Region
 │      └── S3 Bucket
 │
 └── Ireland Region
        └── S3 Bucket
```

So remember:

> **S3 is a global service; each bucket belongs to a Region.**

---

# 11. S3 Storage Capacity

Your instructor described S3 as having **unlimited storage**.

For notes, remember:

> **S3 provides highly scalable storage capacity; you don't have to pre-provision a fixed disk size like a traditional server.**

---

# 12. S3 vs EC2 ⭐⭐⭐

This is very important.

### EC2

```text
EC2
 ↓
Virtual Server
 ↓
OS
 ↓
Application
```

Used to **run applications**.

### S3

```text
S3
 ↓
Bucket
 ↓
Objects
```

Used to **store files/data**.

| EC2 | S3 |
|---|---|
| Compute | Storage |
| Virtual server | Object storage |
| Runs applications | Stores objects |
| Has OS | No OS for you to manage |

---

# 13. Static Website Hosting ⭐⭐⭐

S3 can host **static websites**.

Static files can include:

```text
index.html
style.css
script.js
images
```

Basic idea:

```text
Browser
   ↓
S3
   ↓
index.html
   ↓
Website
```

Example:

```text
Bucket
 ├── index.html
 ├── style.css
 ├── script.js
 └── images/
```

S3 can serve these static website files without requiring an application server.

---

# 14. Why S3 is Useful?

```text
Application
     │
     ├── Images
     ├── Videos
     ├── Documents
     ├── Backups
     ├── Logs
     └── Static website files
             ↓
            S3
```

---

# ⭐ Day 12 Quick Revision

### S3
> **Simple Storage Service**

### Main purpose
> **Store and retrieve objects/files.**

### Structure

```text
S3
 ↓
Bucket
 ↓
Object
 ↓
Key
```

### Remember

```text
EC2 → Run applications
S3  → Store files
```

### Most important concepts

- **Bucket** → Container for objects
- **Object** → File/data stored in S3
- **Key** → Identifier/name of the object
- **S3** → Object-based storage
- **Bucket** → Created in a specific AWS Region
- **S3** → Highly scalable managed storage
- **Static website** → Can be hosted using S3 static website hosting