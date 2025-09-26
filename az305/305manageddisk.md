# Azure Managed Disks - Complete Guide

Azure **Managed Disks** are the recommended disk storage solution for Azure Virtual Machines (VMs). They simplify disk management by abstracting away storage accounts, provide better scalability, improved performance options, and integrate natively with Azure features such as RBAC, snapshots, and availability zones.

---

## 1. Introduction

Before managed disks, Azure used **unmanaged disks**, where users created a **page blob** inside a **storage account**. This approach required careful planning to avoid hitting storage account limits (IOPS, throughput).

Managed disks abstract this complexity. Instead of dealing with storage accounts directly, users work with disks as a **first-party ARM resource** with built-in benefits:

- **Role-Based Access Control (RBAC)**
- **Snapshots and Images** as native resources
- **Availability Sets / Zones** support
- **Consistent provisioning and billing**

> 📌 **Billing Model**: Managed disks are billed based on **provisioned capacity**, not actual usage.  
E.g., a 100 GB disk costs the same whether 1 KB or 100 GB is used.

---

## 2. Key Disk Performance Metrics

Managed disks have multiple performance characteristics. Understanding these is essential before choosing a disk type.

| Metric | Description | Importance |
|--------|-------------|------------|
| **Capacity** | Total storage size of the disk (in GiB/TiB) | Determines how much data you can store |
| **IOPS** | Input/Output operations per second | Indicates how many read/write operations per second the disk can handle |
| **Throughput** | MB/s that can be transferred per second | Critical for workloads with large data per operation |
| **Latency** | Time taken to complete an operation (ms) | Affects responsiveness and performance |
| **Bursting** | Ability to exceed provisioned IOPS/Throughput temporarily | Useful for handling short performance spikes |

---

## 3. Disk Type Comparison

Azure offers four main types of managed disks, each suited to different use cases:

| Disk Type | Storage Tech | Perf Guarantee | Latency | Burst Support | Typical Use Case | Notes |
|-----------|---------------|------------------|----------|----------------|------------------|-------|
| **Standard HDD** | HDD | ❌ No (Up to) | ~10 ms write, ~20 ms read | ❌ | Dev/Test, backup, non-critical data | Cheapest, lowest performance |
| **Standard SSD** | SSD | ❌ No (Up to) | Single-digit ms | ✅ Credit-based (up to 30 mins) | Web servers, low I/O apps | Better perf & latency than HDD |
| **Premium SSD** | SSD | ✅ Provisioned | Single-digit ms | ✅ Credit (≤P20), ✅ On-demand (≥P30) | Production workloads, enterprise apps | Can **separate capacity & performance** tiers |
| **Ultra SSD** | SSD | ✅ Provisioned | <1 ms | ❌ | High-performance databases, critical apps | Dynamically scale **IOPS & throughput** |

---

## 4. Premium SSD - Advanced Capabilities

Premium SSD introduces several advanced features:

### 🔁 Separate Capacity and Performance
- Choose disk size based on storage needs.
- Independently scale **performance tier** for temporary needs (e.g., data import jobs).
- Can reduce performance tier **once every 12 hours**.

### 📈 Bursting Options
- **Credit-based (≤P20):** Free, up to 30 minutes of burst.
- **On-demand (≥P30):** Paid, no time limit. Billed per extra I/O.

| Feature | Credit-Based | On-Demand |
|---------|--------------|------------|
| Availability | ≤ P20 disks | ≥ P30 disks |
| Duration | Up to 30 mins | Unlimited |
| Cost | Free | Extra charge |
| Use Case | Short spikes | Long-running spikes |

---

## 5. Ultra SSD - Maximum Performance

Ultra SSDs offer the **highest performance and flexibility**:

- **Three dials:** Capacity, IOPS, Throughput — all independently adjustable.
- **Dynamic Scaling:** Adjust performance live, even on running VMs.
- **Billing:** Pay separately for each component.

| Feature | Ultra SSD |
|--------|------------|
| Max IOPS | Up to **160,000** |
| Max Throughput | Up to **2,000 MB/s** |
| Latency | <1 ms |
| Bursting | ❌ None (dynamic scaling instead) |
| Use Case | High-end databases, latency-sensitive workloads |

---

## 6. Burst Mechanics Explained

For Standard and Premium SSD (credit-based), Azure uses a **bucket system**:

- Each disk starts with a **full burst bucket** (~30 min worth of burst).
- **Above provisioned IOPS** → bucket drains.
- **Below provisioned IOPS** → bucket refills.

### Bucket Refill Rate Example

| Disk | Provisioned IOPS | Burst Limit | Refill Speed |
|------|-------------------|--------------|---------------|
| P1 (4 GB) | 120 | 3500 | Slow (~120 IOPS/sec) |
| P20 (512 GB) | 2300 | 3500 | Fast (~2300 IOPS/sec) |

💡 **Key Takeaway:** Small disks take longer to refill burst buckets due to lower provisioned IOPS.

---

## 7. VM-Level Considerations

Disks are only part of the performance story — the **VM size and series** also matter.

| VM Attribute | Impact |
|--------------|--------|
| **Max IOPS & Throughput** | Defines total performance ceiling across all disks |
| **Disk Count** | Limited number of data disks per VM |
| **Burst Support** | Some VM types (e.g., Dsv3, Esv3) support burst on storage |
| **Network Bandwidth** | Affects SMB/NFS/iSCSI storage performance |
| **Premium Disk Support** | Requires `S` variants (e.g., `DS`, `ES`) |

📌 **Tip:** Ensure VM and disk performance capabilities are balanced. Over-provisioning disks without adequate VM support leads to wasted cost and throttled performance.

---

## 8. Other Important Features

| Feature | Standard HDD | Standard SSD | Premium SSD | Ultra SSD |
|--------|---------------|--------------|-------------|------------|
| **LRS** (Locally Redundant Storage) | ✅ | ✅ | ✅ | ✅ |
| **ZRS** (Zone Redundant Storage) | ❌ | ✅ | ✅ | ❌ |
| **Shared Disks** | ❌ | ❌ | ✅ | ✅ |
| **Resize (Increase)** | ✅ | ✅ | ✅ | ✅ |
| **Resize (Decrease)** | ❌ | ❌ | ❌ | ❌ |

---

## 9. Best Practices for Managed Disks

- **Understand workload patterns** – average vs. peak IOPS/throughput, duration, and frequency.
- **Match VM capabilities** – avoid disk overprovisioning beyond VM limits.
- **Use performance tier scaling** – adjust Premium SSD performance temporarily.
- **Leverage bursting** – ideal for short-lived spikes.
- **Plan capacity carefully** – you can increase disk size but not decrease it.
- **Use shared disks** – for clustered workloads requiring SCSI persistent reservations.
- **Monitor metrics** – track target IOPS, burst IOPS, and actual read/write ops in Azure Monitor.

---

## 10. Summary

Azure Managed Disks simplify storage management and provide performance scalability. Choosing the right type depends on **workload requirements**, **cost considerations**, and **performance SLAs**.

| Disk Type | Best For | Highlights |
|----------|----------|------------|
| Standard HDD | Dev/Test, backups | Cheapest, low performance |
| Standard SSD | Small apps, low I/O workloads | Better latency, free burst |
| Premium SSD | Production workloads | Provisioned IOPS, burst, performance tier control |
| Ultra SSD | High-end databases | Sub-ms latency, dynamic scaling |

---

**Key Takeaway:**  
⚡ *Choose managed disks based on workload performance characteristics, not just capacity. Always balance disk capabilities with VM limits for optimal results.*
