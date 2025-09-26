# 🧊 Azure Blob Storage – Cold Tier Explained

## 📌 Overview

Azure has introduced a new **Cold Storage Tier** for block blobs. It fills the gap between the existing **Cool** and **Archive** tiers — offering **significantly lower cost than Cool (~60% cheaper)** while remaining **online and instantly accessible** (unlike Archive).

This tier is ideal for data you **rarely access but must retrieve immediately** when needed — such as **medical records, disaster recovery data, or compliance documents**.

---

## ☁️ Storage Account & Block Blobs Recap

- A **storage account** is the container for Azure storage services.
- **Block blobs** are highly versatile and support:
  - Large **unstructured data** (media files)
  - **Semi-structured data** (JSON, CSV)
  - **Structured data** (Parquet, stored as flat objects)
- Optional **Hierarchical Namespace** (ADLS Gen2) provides a true filesystem with:
  - Real directory structure
  - Atomic operations (true renames/moves)

---

## 💰 Cost Components in Blob Storage

| Cost Factor | Description |
|------------|-------------|
| **Capacity** | GB of storage consumed per month |
| **Operations** | Read/write/list operations |
| **Data Retrieval** | GB read from storage |
| **Advanced Features** | Optional services like SFTP, blob indexing, change feed, encryption scopes |

> Even within one application, access patterns and costs can vary widely. Azure storage tiers exist to optimize cost vs. access trade-offs.

---

## 🪶 Blob Storage Tiers Comparison

| Tier | Capacity Cost | Operation Cost | Data Retrieval | Min. Retention | Access Type | Key Use Cases |
|------|---------------|----------------|----------------|----------------|--------------|----------------|
| **Hot** | 🔥 Highest | 💸 Lowest | ❌ None | None | Instant | Frequently accessed data and large portions of files |
| **Cool** | 🧊 Medium | 💵 Higher | ✅ Yes | 30 days | Instant | Infrequently accessed data |
| **Cold** | ❄️ Lower (~60% cheaper than Cool) | 💵 Slightly higher | ✅ Slightly higher | 90 days | Instant | Rarely accessed data that must remain online |
| **Archive** | 🪶 Lowest | 💸 Highest (rehydration) | ✅ High | 180 days | ❌ Offline (rehydration 1–15 hrs) | Long-term storage where real-time access is not required |

---

## 🧊 Cold Tier Key Highlights

- ✅ **Online access** – no rehydration required.  
- 💰 **~60% cheaper** storage cost than Cool.  
- ⏱️ **90-day minimum retention** – deleting earlier incurs early deletion charges.  
- 📈 Slightly higher **operation and retrieval costs** than Cool.  
- 📦 Works with both **Blob Storage** and **ADLS Gen2** accounts.  
- 🔄 Can **upload directly** into the Cold tier via API (no need to upload to Hot first).

---

## ⚖️ Choosing the Right Tier

The choice of tier depends on:
- 📊 **Access frequency** – how often you read/write data.
- 📏 **Portion accessed** – small part of a large file vs. the entire file.
- 🕐 **Retention needs** – how long data must remain stored.
- 📡 **Access latency** – whether real-time retrieval is required.

> 🧠 Example:  
> - Frequently accessed full file → **Hot**  
> - Rare access, but immediate retrieval required → **Cold**  
> - Rare access, retrieval delay acceptable → **Archive**

---

## 🛠️ Automating Tier Transitions – Lifecycle Management

You can automate movement between tiers based on **last access** or **modification date**:

| Rule | Action | Delay |
|------|--------|--------|
| Hot → Cool | After 30 days | 30 days |
| Cool → Cold | After 60 days total (30 more) | 60 days |
| Cold → Archive | After 150 days total (90 more) | 150 days |

⚠️ Metadata such as `lastAccessTime` is not updated when tier changes — so delays are cumulative.

---

## 📊 Cost Optimization Workbook

Use Microsoft’s official **Blob Storage Tiering Workbook (Excel)** to estimate cost based on:
- Number of files  
- Average file size  
- Percentage of file accessed  

It visually compares cost trade-offs across **Hot**, **Cool**, **Cold**, and **Archive** tiers.

---

## 🧪 Current Preview Limitations

- ❌ Change feed not yet supported  
- ❌ Point-in-time restore not available  
- ❌ Object replication not supported  
- ❌ Cannot set Cold as default tier  

These limitations are expected to resolve as Cold tier moves to **General Availability (GA)**.

---

## ✅ Summary – Why Cold Tier Matters

| Feature | Cool | Cold | Archive |
|--------|------|------|----------|
| **Access** | Instant | Instant | Requires rehydration |
| **Cost** | Medium | Low (~60% cheaper) | Lowest |
| **Retention** | 30 days | 90 days | 180 days |
| **Use Case** | Periodic access | Rare access, immediate retrieval | Long-term retention, delayed access |

The **Cold tier** fills the cost and capability gap between **Cool** and **Archive**, giving you an affordable, instantly accessible option for rarely used data.

---

## 📎 Best Practices

- 📁 Upload data **directly into the desired tier** to avoid unnecessary operations.  
- ⚙️ Use **lifecycle policies** to automate tier transitions based on access patterns.  
- 📉 Consolidate many small files into larger blobs to reduce per-operation costs.  
- 🧪 Regularly evaluate access patterns and adjust tiering strategies to optimize cost.

---

**In short:**  
> ❄️ The new **Cold tier** offers the perfect balance between **cost savings** and **instant availability**, making it an excellent choice for infrequently accessed data that must remain online.
