# AWS – Day 8 Notes
## Scalability, Elasticity & High Availability

Today's topic is very important because these are the main reasons cloud platforms like AWS are useful.

---

# 1. Scalability ⭐

**Scalability** means increasing or decreasing the **capacity of a system/server** to handle workload.

Your class describes it as:

> **Increasing the capacity of the server is called Scalability.**

### Example

Suppose a database server has:

```text
8 GB RAM
4 CPU
```

If workload increases, we can upgrade it to:

```text
32 GB RAM
16 CPU
```

This is **Scale Up**.

```text
8 GB RAM
   ↓
32 GB RAM
```

---

# 2. Vertical Scaling

Scalability by increasing the capacity of an existing server is called:

> **Vertical Scaling**

```text
Before:

┌─────────────┐
│   Server    │
│  8 GB RAM   │
│  4 CPU      │
└─────────────┘

        ↓ Scale Up

┌─────────────┐
│   Server    │
│  32 GB RAM  │
│  16 CPU     │
└─────────────┘
```

### Scale Down

Reducing the capacity:

```text
32 GB RAM
    ↓
8 GB RAM
```

Your instructor describes **scalability as long-term**.

---

# 3. Elasticity ⭐

**Elasticity** means increasing or decreasing the **number of servers/resources according to workload**.

Your class definition:

> **Increasing and decreasing the number of servers to meet increasing or decreasing workloads.**

Example:

```text
Normal Traffic
     ↓
   2 Servers

High Traffic
     ↓
   5 Servers

Low Traffic
     ↓
   2 Servers
```

---

# 4. Horizontal Scaling

Adding or removing servers is called:

> **Horizontal Scaling**

```text
Before:

   Load Balancer
        ↓
     Server 1


High Traffic:

   Load Balancer
    /    |    \
   ↓     ↓     ↓
Server1 Server2 Server3
```

When traffic decreases:

```text
Server3 removed
      ↓
Server2 removed
```

---

# 5. Elasticity vs Scalability ⭐⭐⭐

| Elasticity | Scalability |
|---|---|
| Usually short-term response to changing demand | Capacity planning/change for larger workloads |
| Add/remove servers | Increase/decrease capacity |
| Often horizontal scaling | Often vertical scaling in your class |
| AWS Auto Scaling can provide it | Scale Up / Scale Down |

### Easy memory

```text
Elasticity
→ Number of servers
→ Horizontal
→ Short term

Scalability
→ Server capacity
→ Vertical
→ Long term
```

---

# 6. Auto Scaling

AWS can automatically increase or decrease resources based on demand.

Your class:

> **Auto Scaling = Scale Out and Scale In**

### Scale Out

Add servers:

```text
2 Servers
   ↓
4 Servers
```

### Scale In

Remove servers:

```text
4 Servers
   ↓
2 Servers
```

---

# 7. Auto Scaling Group (ASG)

**ASG = Auto Scaling Group**

It manages a group of EC2 instances.

Example from your class:

```text
        Auto Scaling Group
              │
       ┌──────┼──────┐
       ↓      ↓      ↓
      EC2    EC2    EC2
```

You can define boundaries such as:

```text
Minimum = 2
Maximum = 6
```

So the ASG can maintain instances within those boundaries according to demand and configuration.

---

# 8. High Availability ⭐⭐⭐

**High Availability (HA)** means keeping an application/service available for customers with minimal downtime.

Your class defines:

> **The period of time the service is available to the customer is called High Availability.**

If the service is unavailable:

> **Downtime**

---

# 9. Load Balancer + High Availability

A Load Balancer can monitor backend applications using **health checks**.

```text
                  Load Balancer
                       │
             ┌─────────┼─────────┐
             ↓         ↓         ↓
          Server 1  Server 2  Server 3
           Healthy   Healthy   Unhealthy
```

If one server becomes unhealthy, the Load Balancer can stop sending new traffic to it.

---

# 10. Health Check

The Load Balancer checks whether backend instances are healthy.

Your diagram shows:

```text
Health Check
     ↓
   200 OK
```

If the application responds successfully:

```text
Healthy ✅
```

If it fails:

```text
Unhealthy ❌
```

---

# 11. Round Robin Method

Your class mentions **Round Robin**.

Traffic is distributed sequentially:

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 3
Request 4 → Server 1
Request 5 → Server 2
...
```

Diagram:

```text
              Load Balancer
             /      |      \
            ↓       ↓       ↓
          S1        S2      S3
            ↑       ↑       ↑
             └──────┴───────┘
              Round Robin
```

---

# 12. High Availability — Simple Architecture

```text
                Client
                  ↓
             Load Balancer
                  ↓
          ┌───────┼───────┐
          ↓       ↓       ↓
        App1     App2    App3
          ✅       ✅      ❌
```

If App3 fails:

```text
Client
  ↓
Load Balancer
  ↓
App1 / App2
```

The failed server can be removed from traffic.

---

# 13. RMF

Your instructor mentioned:

> **RMF**

In the diagram:

```text
Redundancy
Monitoring
Failover
```

These are important for achieving high availability.

### Redundancy

Have multiple resources instead of relying on one.

```text
Server 1
Server 2
Server 3
```

### Monitoring

Continuously check the health/status of resources.

### Failover

If one resource fails, traffic/workload can move to another available resource.

---

# 14. Failover

Failover means switching to another healthy resource when the primary resource fails.

```text
Primary Server ❌
       ↓
Failover
       ↓
Backup Server ✅
```

Goal:

> **Little or minimum downtime.**

---

# 15. High Availability + Auto Scaling

These concepts can work together:

```text
                 Client
                   ↓
             Load Balancer
                   ↓
          ┌────────┼────────┐
          ↓        ↓        ↓
         EC2      EC2      EC2
          │        │        │
          └────────┼────────┘
                   ↓
              Auto Scaling
```

- **Load Balancer** → distributes traffic
- **Health Check** → detects unhealthy instances
- **Auto Scaling** → adds/removes instances
- **Multiple instances** → provides redundancy
- Together → improve **availability**

---

# ⭐ Day 8 Quick Revision

```text
SCALABILITY
    ↓
Increase/decrease capacity
    ↓
Scale Up / Scale Down
    ↓
Usually Vertical Scaling
```

```text
ELASTICITY
    ↓
Increase/decrease number of servers
    ↓
Scale Out / Scale In
    ↓
Horizontal Scaling
    ↓
AWS Auto Scaling
```

```text
HIGH AVAILABILITY
    ↓
Keep application available
    ↓
Redundancy
Monitoring
Failover
    ↓
Load Balancer + Health Checks
```

### Most important flow

```text
High Traffic
     ↓
Auto Scaling
     ↓
Scale Out
     ↓
More EC2 Instances
     ↓
Load Balancer distributes traffic
```

```text
Server Failure
     ↓
Health Check
     ↓
Unhealthy Server removed from traffic
     ↓
Failover / Auto Scaling
     ↓
Application remains available
```