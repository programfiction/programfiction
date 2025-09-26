# ☁️ Azure Storage Accounts – Complete Guide

Azure Storage Accounts are foundational to storing data in Azure. They support a variety of services — including blobs, files, queues, and tables — and offer multiple performance, replication, and pricing options.  
This guide summarizes the types of storage accounts, performance tiers, services, and cost considerations.

---

## 1. 📦 Storage Account Basics

- A **storage account** is created in a specific **Azure region**.
- It determines how data is stored, accessed, and billed.
- Key choices during creation:
  - **Performance tier**: Standard vs. Premium
  - **Account kind**: General-purpose v2 (GPv2), Blob storage, etc.
  - **Replication option**: LRS, ZRS, GRS, RA-GRS

✅ **Best Practice:** Use **General Purpose v2 (GPv2)** for most scenarios — it supports all storage services and tiering.

---

## 2. ⚙️ Performance Tiers

| Performance Tier | Description | Common Use Cases |
|------------------|-------------|------------------|
| **Standard** | HDD/standard SSD-backed, consumption-based billing | Most scenarios (blobs, files, queues, tables) |
| **Premium** | SSD-backed, low-latency, provisioned performance | High-performance block blob or file workloads |

---

## 3. 🗂️ Storage Account Services

Azure Storage supports four main services. All can run under **Standard GPv2** accounts.

| Service | Description | Notes on Cost |
|--------|------------|---------------|
| **Blob Storage** | Stores unstructured data as objects (block, append, or page blobs) | Charged for capacity, replication, and operations |
| **File Storage** | Fully managed SMB file shares | Charged per GB stored and operations; Premium based on provisioned size |
| **Queue Storage** | Messaging service for decoupled communication | Capacity + transaction cost |
| **Table Storage** | NoSQL key-value store for structured data | Capacity + transaction cost |

---

## 4. 🛠️ Replication Options

Replication impacts both **resiliency** and **cost**:

| Option | Description | Copies | Notes |
|--------|-------------|--------|-------|
| **LRS** | Locally redundant | 3 | Cheapest; single data center |
| **ZRS** | Zone redundant | 3 | Across 3 zones in a region |
| **GRS** | Geo-redundant | 6 | Across primary + paired region |
| **RA-GRS** | Read-access GRS | 6 | Adds read access to secondary region |

💰 **Cost Impact:** More copies and greater distance = higher cost.

---

## 5. ☁️ Blob Storage – Tiers & Costs

Blobs are the most flexible storage type and support tiering to balance cost and access frequency:

| Tier | Access Pattern | Capacity Cost | Transaction Cost | Notes |
|------|------------------|----------------|------------------|-------|
| **Hot** | Frequent access | 🔼 Highest | 🔽 Lowest | Active data |
| **Cool** | Infrequent access | 🔽 Medium | 🔼 Higher | Backup/rarely accessed |
| **Archive** | Rare/long-term storage | 🔽 Lowest | 🔼 Highest | Offline; retrieval delay |

- **Hot**: Best for data accessed often — pay more for storage, less per transaction.
- **Cool**: Cheaper storage but higher transaction cost — ideal for infrequent use.
- **Archive**: Cheapest for capacity — offline storage with rehydration required.

> 🧠 Archive tier only supports **block blobs** (not append blobs).

---

## 6. ⚡ Premium Performance Options

Premium tiers provide **low latency**, **high throughput**, and **predictable performance**.  
These require creating **different types of storage accounts**.

### 📤 Premium Block Blob Storage

- Uses a **Block Blob storage account (Premium)**.
- ~10x **lower latency** than standard.
- Cheaper per-operation cost but **higher per-GB cost**.
- Lifecycle management **cannot** move data between standard and premium — migration requires copying data.

| Feature | Standard Block Blob | Premium Block Blob |
|--------|----------------------|--------------------|
| Billing | Capacity + operations | Capacity + operations |
| Latency | Single-digit ms | Sub-ms |
| Use Case | General storage | High-performance, interactive workloads |

---

### 📁 Premium File Storage

- Uses a **File Storage (Premium)** account.
- Billed based on **provisioned share size**, not actual usage.
- Provisioned size directly affects **IOPS** and **throughput**.
- Larger shares = higher performance (even if not fully used).

| Feature | Standard File | Premium File |
|--------|---------------|--------------|
| Billing | Per GB used + operations | Per provisioned share size |
| Performance | Based on consumption | Based on provisioned capacity |
| Best For | General file shares | Performance-sensitive workloads |

> ⚠️ You pay for the provisioned size even if empty. Plan capacity carefully.

---

## 7. 📄 Page Blobs and Legacy Usage

- **Page blobs** support random read/write operations.
- Historically used for **VM disks**, but **Managed Disks** are now preferred.
- Still useful for unmanaged disks or legacy scenarios.
- Premium **page blobs** are billed based on **provisioned size**, not usage.

---

## 8. 📊 Cost Structure Summary

Regardless of the service, costs are primarily driven by:

| Cost Factor | Applies To | Description |
|------------|------------|-------------|
| **Capacity** | All | Amount of data stored (or provisioned size for premium) |
| **Replication** | All | LRS, ZRS, GRS, RA-GRS choices |
| **Operations** | All | Read/write/list/delete transactions |
| **Data Access Tier** | Blobs, Files | Hot, Cool, Archive |
| **Provisioned Size** | Premium File, Premium Page Blobs | Fixed billing based on reserved capacity |
| **Egress Data** | All | Data leaving Azure incurs extra cost |

---

## 9. 🧭 Best Practices & Recommendations

- ✅ Use **GPv2 Standard** for most workloads.  
- ✅ Choose **Hot** tier for frequently accessed data, **Cool** for infrequent access, and **Archive** for long-term cold storage.  
- ✅ Use **Premium Block Blob** for low-latency, high-performance scenarios.  
- ✅ Use **Premium File Storage** when predictable performance is critical.  
- ✅ Plan capacity carefully for premium tiers to avoid overpaying.  
- ✅ Prefer **Managed Disks** over page blobs for VM storage.  
- ✅ Consider **replication trade-offs** — higher resiliency means higher cost.  

---

## 🧾 Summary

| Storage Type | Tier | Billing Basis | Best Use Case |
|--------------|------|----------------|----------------|
| **Blob Storage** | Standard (Hot/Cool/Archive) | Per GB + operations | General data storage |
| **Block Blob (Premium)** | Premium | Per GB + operations | Low-latency object storage |
| **File Storage** | Standard | Per GB + operations | SMB file shares |
| **File Storage (Premium)** | Premium | Provisioned share size | High-performance file workloads |
| **Page Blob** | Standard/Premium | Per GB (or provisioned) + ops | Legacy VM disks |
| **Queue/Table** | Standard | Per GB + operations | Messaging / NoSQL data |

---

## 🏁 Final Thoughts

For **99.9% of use cases**, a **Standard GPv2 storage account** is the right choice — it’s flexible, supports all services, and is cost-efficient.  
Premium options are ideal when **performance and latency** are critical, but they come at a higher cost and require careful capacity planning.

> 💡 **Golden Rule:** Plan storage based on **access patterns**, **performance needs**, and **cost trade-offs**. Hotter tiers cost more per GB but less per operation, while premium storage trades higher capacity costs for much lower latency and predictable performance.

---
