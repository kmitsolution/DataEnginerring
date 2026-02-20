#  How to Create Azure Databricks Workspace (Step-by-Step)

---

# 🔷 What is Azure Databricks?

Microsoft Azure provides
Azure Databricks — a managed Apache Spark service integrated with Azure.

It allows you to create a **workspace**, where you build notebooks, create clusters, and run data pipelines.

---

# 🔷 What is a Workspace?

## 🔹 Definition

A **Workspace** is a logical environment inside Azure Databricks where you:

* Create notebooks
* Create clusters
* Run jobs/workflows
* Manage users and permissions
* Store code and experiments

Think of it as:

```
Azure Subscription
    └── Resource Group
            └── Databricks Workspace
                    ├── Notebooks
                    ├── Clusters
                    ├── Jobs
                    ├── SQL Warehouses
                    └── Unity Catalog
```

Each workspace is isolated.

---

# 🔷 Step-by-Step: Create Azure Databricks Workspace (Azure Portal / Console)

## ✅ Step 1: Login to Azure Portal

Go to:

```
https://portal.azure.com
```

Login with your Azure account.

---

## ✅ Step 2: Create Resource

1. Click **Create a resource**
2. Search: **Azure Databricks**
3. Click **Create**

---

## ✅ Step 3: Fill Basic Details

You will see configuration page.

### 🔹 Basics Tab

Fill:

* **Subscription**
* **Resource Group** (Create new or use existing)
* **Workspace name**
* **Region** (Choose closest to you)
* **Pricing Tier** (Standard / Premium / Trial)

---

## 🔷 Standard vs Premium (Important Interview Question)

| Feature                   | Standard | Premium |
| ------------------------- | -------- | ------- |
| Basic Spark               | ✅        | ✅       |
| Role-based access control | ❌        | ✅       |
| Unity Catalog             | ❌        | ✅       |
| Credential passthrough    | ❌        | ✅       |
| Fine-grained security     | ❌        | ✅       |
| Audit logs                | ❌        | ✅       |
| SCIM provisioning         | ❌        | ✅       |

### 🔥 When to Use?

* **Standard** → Learning, small projects
* **Premium** → Enterprise production workloads

👉 In real companies, **Premium is commonly used**.

---

## 🔹 Networking Tab (Optional Advanced Setup)

You can:

* Enable VNet injection
* Configure secure networking
* Private endpoints

For beginners → keep default settings.

---

## ✅ Step 4: Review + Create

Click:

```
Review + Create → Create
```

Deployment takes 3–5 minutes.

---

# 🔷 After Deployment

Once deployment completes:

Go to:

```
Resource Group → Azure Databricks Workspace
```

You will see:

```
Launch Workspace
```

Click it.

---

# 🔷 What Happens When You Click "Launch Workspace"?

![Image](https://blog.coeo.com/hs-fs/hubfs/Blog%20images/120819_JG_Databrickspart3_2.png?name=120819_JG_Databrickspart3_2.png\&width=700)

![Image](https://learn.microsoft.com/en-us/azure/databricks/_static/images/administration-guide/admin-settings.png)

![Image](https://docs.databricks.com/gcp/en/assets/images/workspace-gcp-3f54f54b5cfd14cc8e4fa8c02334e855.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2APD_vM4mvzZGxw7S2aoD9oQ.jpeg)

You will enter the Databricks UI.

Inside you will see:

Left Sidebar:

* Workspace
* Clusters
* Workflows
* SQL
* Data
* ML
* Admin (Premium)

---

# 🔷 What You Do Inside Workspace

## 1️⃣ Create Cluster

Go to:

```
Compute → Create Cluster
```

Configure:

* Cluster name
* Runtime version
* Worker nodes
* Auto-scaling

---

## 2️⃣ Create Notebook

Go to:

```
Workspace → Create → Notebook
```

Choose language:

* Python
* SQL
* Scala
* R

Attach to cluster.

Now you can run Spark code.

---

# 🔷 Architecture View

```
Azure Portal
     |
     v
Create Databricks Resource
     |
     v
Databricks Workspace
     |
     v
----------------------------------
|  Notebooks                    |
|  Clusters                     |
|  Jobs / Workflows             |
|  SQL Warehouse                |
|  Unity Catalog (Premium)      |
----------------------------------
```

---

# 🔥 Real-World Flow

```
Azure Subscription
    ↓
Create Resource Group
    ↓
Create Azure Databricks Workspace
    ↓
Launch Workspace
    ↓
Create Cluster
    ↓
Create Notebook
    ↓
Run Spark Code
```

---

# 🔷 Important Interview Questions

### Q1: What is a Databricks Workspace?

A logical container where notebooks, clusters, jobs, and data governance are managed.

### Q2: Difference between Standard and Premium?

Premium supports enterprise features like Unity Catalog, RBAC, and audit logs.

### Q3: What happens after launching workspace?

You enter Databricks UI to create clusters and notebooks.

