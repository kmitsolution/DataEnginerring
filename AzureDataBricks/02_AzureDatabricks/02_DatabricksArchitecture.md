# 🚀 Azure Databricks Architecture (Control Plane vs Compute Plane)

This is a **very important concept** for interviews and real-world architecture understanding.

Azure Databricks runs on top of
Microsoft Azure and is designed with **two main subscriptions/planes**:

1. **Databricks Subscription → Control Plane**
2. **Customer Subscription → Compute Plane**

---

# 🔷 High-Level Architecture Overview

![Image](https://learn-attachment.microsoft.com/api/attachments/214e7b6e-1c2a-4e8b-acde-36113a900623?platform=QnA)

![Image](https://learn-attachment.microsoft.com/api/attachments/5b0ad376-8fbb-4697-9b5a-aa1bb06330ec?platform=QnA)

![Image](https://learn.microsoft.com/en-us/azure/architecture/solution-ideas/media/azure-databricks-modern-analytics-architecture.svg)

![Image](https://www.databricks.com/sites/default/files/2025-06/data_intelligence_end-to-end_architecture_with_azure_databricks.png?v=1749057860)

```
                ┌─────────────────────────────────┐
                │      Databricks Subscription    │
                │         (Control Plane)         │
                ├─────────────────────────────────┤
                │  UI (Workspace)                │
                │  Unity Catalog                 │
                │  Managed Identity              │
                │  Compute Orchestration         │
                │  Job Scheduler                 │
                │  Queries & Code Metadata       │
                └─────────────────────────────────┘
                               │
                               │ Secure Communication
                               ▼
                ┌─────────────────────────────────┐
                │      Customer Subscription      │
                │         (Compute Plane)         │
                ├─────────────────────────────────┤
                │  Classic Compute (Clusters)     │
                │  Serverless Compute             │
                │  Workspace Storage (ADLS)       │
                │  Customer Resources (VMs)       │
                └─────────────────────────────────┘
```

---

# 🔷 1️⃣ Databricks Subscription (Control Plane)

This is **managed by Databricks**, not by you.

It contains:

### 🔹 1. Workspace UI

* Browser-based interface
* Notebook editor
* Cluster management
* Jobs & workflows

Your code is written here.

---

### 🔹 2. Unity Catalog

Centralized governance layer:

* Access control
* Data lineage
* Metadata management
* Fine-grained security

---

### 🔹 3. Managed Identity

Used to:

* Authenticate securely with Azure services
* Access storage accounts
* Avoid storing credentials

---

### 🔹 4. Compute Orchestration

Control plane:

* Starts/stops clusters
* Scales nodes
* Allocates resources

It does NOT process data — it only manages compute.

---

### 🔹 5. Queries & Code Management

Stores:

* Notebook metadata
* Job definitions
* SQL query definitions
* Dashboard metadata

---

# 🔷 2️⃣ Customer Subscription (Compute Plane)

This is inside YOUR Azure subscription.

This is where actual data processing happens.

---

## 🔹 A. Classic Compute Plane

When you create a cluster:

```
Driver VM
Worker VM(s)
```

These VMs are created inside:

* Your VNet (if configured)
* Your Azure subscription

Data never leaves your subscription.

---

## 🔹 B. Serverless Compute Plane

Newer model:

* No cluster management
* Fully managed compute
* Auto scaling
* Optimized for SQL & notebooks

Still processes data inside secure infrastructure.

---

## 🔹 C. Workspace Cloud Storage (Data Lake)

Usually:

* Azure Data Lake Storage Gen2 (ADLS)

Stores:

* Delta tables
* Bronze/Silver/Gold data
* Checkpoints
* Logs

---

## 🔹 D. Customer Resources Created

When workspace is deployed, Azure creates:

* Managed Resource Group
* Virtual Machines
* Network Interfaces
* Load Balancers
* Storage accounts

These are visible in your Azure subscription.

---

# 🔥 Control Plane vs Compute Plane (Simple Comparison)

| Feature         | Control Plane | Compute Plane |
| --------------- | ------------- | ------------- |
| Managed By      | Databricks    | Customer      |
| Runs UI         | ✅             | ❌             |
| Runs Spark Jobs | ❌             | ✅             |
| Stores Data     | ❌             | ✅             |
| Governance      | ✅             | ❌             |
| Creates VMs     | ❌             | ✅             |

---

# 🔷 Real Execution Flow

```
User writes code in Notebook (Control Plane)
            ↓
Control Plane sends instructions
            ↓
Compute Plane spins up cluster (VMs)
            ↓
Spark processes data in ADLS
            ↓
Results returned to UI
```

---

# 🔷 With Unity Catalog Architecture

```
            User
              |
              v
        Workspace UI
              |
              v
        Unity Catalog
              |
              v
     Permission Check (RBAC)
              |
              v
        Compute Cluster
              |
              v
     Azure Data Lake Storage
```

---

# 🔥 Important Interview Questions

### Q1: Does data go to Control Plane?

❌ No. Data stays in Customer subscription.

### Q2: Where are clusters created?

Inside Customer subscription.

### Q3: Who manages Control Plane?

Databricks.

### Q4: What is Managed Resource Group?

A resource group automatically created by Azure Databricks to hold compute resources.

---

# 🔷 One-Line Summary

Azure Databricks separates:

👉 Control (UI, governance, orchestration)
👉 Compute (actual Spark processing in your subscription)

This ensures:

* Security
* Scalability
* Enterprise compliance

---

