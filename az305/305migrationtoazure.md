# Azure Migration Guide

A complete end-to-end guide for migrating on-premises workloads to Azure — from planning and discovery to migration, optimization, and decision-making frameworks.

---

## 📑 Table of Contents
1. [Overview & Summary](#overview--summary)
2. [Migration Flow](#migration-flow)
3. [Azure Migration Practical Guide](#azure-migration-practical-guide)
4. [Migration Decision Checklist & 5 R's](#migration-decision-checklist--5-rs)
5. [Tools & Tips](#tools--tips)

---

## 📘 Overview & Summary

### High-level Migration Flow

1. **Spring-clean** — Remove unused apps/data to reduce migration scope.
2. **Discover** — Inventory servers, OS, apps, hardware, performance, dependencies.
3. **Assess** — Right-size, group dependent systems, evaluate target services and feasibility.
4. **Migrate** — Replicate (agentless or agent-based), test migration, cutover (online/offline).
5. **Optimize** — Ongoing cost & performance optimizations after migration.

---

### Key Considerations

- **Business drivers:** Time, budget, ROI window, strategic importance.
- **Dependencies & latency:** Apps relying on sub-ms latency may need redesign.
- **The 5 R's:** Rehost, Refactor, Re-architect, Rebuild, Replace (SaaS).
- **Azure Migrate:** The central hub for discovery, assessment, and migration.
- **Data considerations:** Use Database Migration Service and compatibility checks.
- **Workload types:** VDI → Windows Virtual Desktop, Large data → Data Box, Web → App Service Migration Assistant.
- **Testing:** Always run test migrations and plan downtime carefully.

---

## 📈 Migration Flow

Below is the typical Azure migration lifecycle:

![Migration Flow](migration_flow.png)

---

## 🛠️ Azure Migration Practical Guide

### 0. Spring-clean
- Remove unused VMs, old file shares, and stale data before migration.

### 1. Discover
- Deploy Azure Migrate appliance:
  - OVA for VMware  
  - VHD for Hyper-V  
  - Installation package for physical/other hypervisors
- Capture:
  - OS and application inventory  
  - Hardware specs and performance counters  
  - Network dependencies
- Run discovery for days or weeks to capture peak and seasonal usage.

---

### 2. Assess
- Use Azure Migrate assessments to:
  - Right-size VM targets (based on 95th percentile, with padding).
  - Estimate cost and choose appropriate storage and regions.
  - Group dependent servers for co-migration.
  - Produce readiness and confidence ratings.
- Determine the best migration path per application using the **5 R’s**.

---

### 3. Migrate
- **Replication options:**
  - Agentless (VMware/Hyper-V snapshots) — simpler, safer for production.
  - Agent-based (mobility service) — for unsupported hypervisors or physical servers.
- Set up replication appliances: config server, process server as needed.
- Run **test migrations** to validate performance and functionality.
- Perform **final cutover**: shut down on-prem, finalize replication, and bring up workloads in Azure.

---

### 4. Optimize
- Post-migration:
  - Optimize VM sizes, storage tiers, and enable autoscaling.
  - Use reserved instances for cost optimization.
  - Refactor or re-architect strategic apps over time.
  - Monitor performance and costs continuously.

---

## 📋 Migration Decision Checklist & 5 R's

### Decision Checklist (Per Application)

- How long do we have to migrate?
- Is the app strategic (lifecycle 1–5+ years)?
- What’s the budget and ROI tolerance?
- Are there dependencies that anchor it on-prem?
- What downtime is acceptable? (online vs offline migration)
- What is the data seasonality and monitoring period?
- Security, compliance, and data sovereignty requirements?

---

### 5 R's – Migration Strategy

| Strategy | Description | Effort | Cloud-Native Benefit |
|----------|-------------|--------|-----------------------|
| **Rehost** | Lift-and-shift VM → VM | ⭐ | ⭐ |
| **Refactor** | Minimal code change, move to managed platform | ⭐⭐ | ⭐⭐ |
| **Re-architect** | Modify application for cloud-native patterns | ⭐⭐⭐ | ⭐⭐⭐ |
| **Rebuild** | Recreate application from scratch | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Replace** | Move to SaaS alternative | ⭐⭐ | ⭐⭐⭐⭐ |

![5 R's Matrix](5Rs_decision_matrix.png)

---

## 🧰 Tools & Tips

### Azure Migrate Hub
- Central hub for discovery, assessment, replication, and migration planning.
- Agentless discovery for VMware/Hyper-V.
- Supports Windows and Linux workloads.
- Integrates with partner tools for extended capabilities.

---

### Database Migration
- **Azure Database Migration Service**:  
  - Standard SKU – free, basic functionality  
  - Premium SKU – supports online replication
- Use **Database Migration Assistant** to check feature parity and compatibility before migration.

---

### VDI & Web Apps
- **VDI migrations** → Windows Virtual Desktop (often partner-assisted).
- **Web apps** → App Service Migration Assistant (for public-facing sites).
- **Large data** → Azure Data Box for offline bulk transfers.

---

### Best Practices
- Capture sufficient performance history to right-size workloads accurately.
- Group dependent workloads to preserve latency-sensitive communication.
- Use agentless replication for safety where possible.
- Always run **test migrations** — validate networking, DNS, and monitoring before final cutover.

---

## 🗺️ Target Mapping Reference

Map common on-prem workloads to Azure services:

![Target Mapping](target_mapping.png)

---

## ✅ Final Thoughts

Migrating to Azure is more than a technical exercise — it’s a strategic transformation.  
By following this structured approach — **spring-clean → discover → assess → migrate → optimize** — and making informed decisions using the **5 R’s**, organizations can modernize with confidence, reduce costs, and accelerate innovation.
