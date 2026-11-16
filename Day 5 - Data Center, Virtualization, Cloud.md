# AWS – Day 5 Notes
## Data Center → Virtualization → Cloud → AWS

Day 5 is a **very important foundation for understanding why cloud computing and AWS became necessary**.

---

# 1. Data Center

A **Data Center** is a physical facility where organizations keep their IT infrastructure.

It contains:

- Physical servers
- Storage
- Networking equipment
- Power systems
- Cooling systems
- Security systems

### Simple diagram

```text
                DATA CENTER
        ┌─────────────────────────┐
        │                         │
        │  Server  Server  Server │
        │  Server  Server  Server │
        │  Server  Server  Server │
        │                         │
        │  Network / Storage      │
        │                         │
        └─────────────────────────┘
```

Your instructor referred to this as:

> **On-Premises Data Center**

Meaning the company **owns and manages the physical infrastructure itself**.

---

# 2. Traditional / Physical Architecture

In traditional architecture, one physical machine normally contains:

```text
┌─────────────────────┐
│    Applications     │
├─────────────────────┤
│         OS          │
├─────────────────────┤
│      Hardware       │
└─────────────────────┘
```

For example:

```text
Physical Server
      ↓
Windows/Linux
      ↓
Application
```

The company has to purchase and maintain the physical machine.

---

# 3. Advantages of Data Centers

### 1. Complete control

Company controls its own:

- Hardware
- Network
- Servers
- Data

### 2. Security control

The organization can implement its own physical and network security.

### 3. Customization

Hardware and infrastructure can be configured according to company requirements.

---

# 4. Problems / Disadvantages of Data Centers

This is where cloud computing starts becoming useful.

### 1. High initial cost

Company has to purchase:

- Servers
- Storage
- Networking equipment
- Data center infrastructure

### 2. Maintenance

Company needs people to manage:

- Hardware
- OS
- Network
- Cooling
- Power
- Security

### 3. Resource wastage

Suppose a server has:

```text
16 GB RAM
```

but the application uses only:

```text
4 GB
```

Then a large portion of the resource is unused.

### 4. Scaling is difficult

If workload suddenly increases:

```text
Existing servers
       ↓
Need more servers
       ↓
Purchase hardware
       ↓
Install
       ↓
Configure
```

This takes time.

### 5. Hardware failure

Physical hardware can fail.

```text
Server failure
      ↓
Application affected
```

### 6. Capacity planning

Companies have to predict future requirements:

> How many servers will we need next year?

If they buy too many → resources are wasted.

If they buy too few → capacity becomes insufficient.

---

# 5. Virtualization ⭐⭐⭐

**Virtualization** allows us to create multiple **Virtual Machines (VMs)** on a single physical machine.

Instead of:

```text
1 Physical Server
      ↓
1 OS
      ↓
1 Application
```

we can have:

```text
             Physical Server
                    │
               Hypervisor
          ┌─────────┼─────────┐
          ↓         ↓         ↓
         VM1       VM2       VM3
          ↓         ↓         ↓
         OS        OS        OS
          ↓         ↓         ↓
        App       App       App
```

---

# 6. What is a Virtual Machine?

A **Virtual Machine (VM)** is a software-based computer running on a physical machine.

Each VM can have its own:

- Operating System
- Applications
- CPU allocation
- RAM allocation
- Storage

From the application's perspective, the VM behaves like a separate computer.

---

# 7. Hypervisor ⭐

The **Hypervisor** is the software layer responsible for creating and managing virtual machines.

```text
VM 1     VM 2     VM 3
 │        │        │
 └────────┼────────┘
          ↓
      Hypervisor
          ↓
   Physical Hardware
```

Examples shown in your class:

- VMware
- Hyper-V
- Oracle VirtualBox

---

# 8. Host Machine and Guest Machine

### Host Machine

The actual physical machine.

```text
Physical Hardware
       ↓
   Host Machine
```

### Guest Machine

A VM running on the host.

```text
Host Machine
   │
   ├── Guest VM 1
   ├── Guest VM 2
   └── Guest VM 3
```

Easy memory trick:

> **Host = Physical machine**  
> **Guest = Virtual machine**

---

# 9. Resource Sharing

Suppose a physical server has:

```text
16 GB RAM
100 GB HDD
```

Virtualization allows those resources to be allocated among multiple VMs.

Example:

```text
Physical Server
16 GB RAM
     │
     ├── VM1 → 4 GB
     ├── VM2 → 4 GB
     ├── VM3 → 4 GB
     └── VM4 → 4 GB
```

So one physical machine can run multiple workloads.

---

# 10. Migration: Physical → Virtual

Before virtualization:

```text
Physical Server 1
      ↓
Application 1

Physical Server 2
      ↓
Application 2

Physical Server 3
      ↓
Application 3
```

This can result in underutilized servers.

After virtualization:

```text
             Physical Server
                    ↓
                Hypervisor
          ┌─────────┼─────────┐
          ↓         ↓         ↓
         VM1       VM2       VM3
          ↓         ↓         ↓
        App 1     App 2     App 3
```

So multiple workloads can run on fewer physical machines.

---

# 11. Advantages of Virtualization

### 1. Better resource utilization

Physical resources can be shared among multiple VMs.

### 2. Cost reduction

Fewer physical servers may be required.

### 3. Isolation

One VM is logically separated from another.

### 4. Easy provisioning

Creating a new VM is much faster than purchasing a new physical server.

### 5. Scalability

Additional VMs can be created when required.

### 6. Flexibility

Different VMs can run different operating systems/applications on the same physical hardware.

---

# 12. Disadvantages of Virtualization

### 1. Host failure

If the physical host fails, multiple VMs running on it can be affected.

```text
Host Failure
     ↓
VM1 ❌
VM2 ❌
VM3 ❌
```

### 2. Resource contention

Multiple VMs share physical resources.

If one workload consumes too many resources, others can be affected.

### 3. Hypervisor dependency

The virtualization layer itself needs to be maintained and managed.

### 4. Additional complexity

Managing many VMs can become complicated.

---

# 13. Types of Virtualization Shown in Your Class

Your instructor showed two approaches.

## A. Bare-Metal Virtualization

The hypervisor runs directly on the physical hardware.

```text
┌─────────┬─────────┬─────────┐
│   VM1   │   VM2   │   VM3   │
└─────────┴─────────┴─────────┘
            ↓
       Hypervisor
            ↓
         Hardware
```

Examples mentioned:

- VMware
- Microsoft Hyper-V

This is also commonly called **Type 1 Hypervisor**.

---

# 14. Host-Based Virtualization

Here, a normal host OS exists between the hardware and virtualization software.

```text
┌─────────────────────────┐
│          VMs            │
├─────────────────────────┤
│   Virtualization Layer  │
├─────────────────────────┤
│      Host OS - Windows  │
├─────────────────────────┤
│        Hardware         │
└─────────────────────────┘
```

Your instructor mentioned:

> **Oracle VirtualBox**

This is commonly called **Type 2 Hypervisor**.

---

# 15. Bare Metal vs Host Based

| Bare Metal | Host Based |
|---|---|
| Hypervisor directly on hardware | Hypervisor runs on host OS |
| Type 1 | Type 2 |
| Better suited for servers/data centers | Common for desktops/testing |
| Example: VMware ESXi | Example: VirtualBox |

---

# 16. Entry of Cloud Computing ☁️

Now we reach the important point.

Companies had:

```text
Physical Data Center
       ↓
Virtualization
       ↓
Better resource utilization
```

But companies still had to:

- Own infrastructure
- Maintain hardware
- Manage data centers
- Handle power/cooling
- Purchase additional capacity

Cloud computing changed this model.

---

# 17. Cloud Computing

Instead of purchasing physical infrastructure ourselves:

```text
Company
   ↓
Cloud Provider
   ↓
Computing Resources
```

The cloud provider owns and manages the underlying infrastructure.

The customer can consume resources when required.

---

# 18. AWS Entry

AWS provides cloud infrastructure and services.

Conceptually:

```text
Traditional
───────────
Company
   ↓
Own Data Center
   ↓
Physical Servers


Virtualization
──────────────
Company
   ↓
Physical Servers
   ↓
Hypervisor
   ↓
VMs


Cloud
─────
Company
   ↓
AWS
   ↓
Cloud Infrastructure
   ↓
VMs / Storage / Database / Network
```

---

# ⭐ Day 5 Complete Journey

This is the **most important thing to remember from today's class**:

```text
Physical Data Center
        ↓
Physical Servers
        ↓
Resource wastage + High cost
        ↓
Virtualization
        ↓
Multiple VMs on one physical server
        ↓
Better utilization
        ↓
But still need to manage infrastructure
        ↓
Cloud Computing
        ↓
AWS
```

### One-line revision

> **Virtualization improves utilization of physical infrastructure; cloud computing allows us to consume infrastructure/services without owning the underlying data center.**