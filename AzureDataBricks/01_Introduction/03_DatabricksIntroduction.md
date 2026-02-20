--

# 🔷 What is Databricks?

**Databricks** is a **cloud-based data analytics platform** built on top of **Apache Spark**.

It provides:

* Big data processing
* Data engineering
* Data science
* Machine learning
* SQL analytics
* Lakehouse architecture

It simplifies Spark by providing:

* Managed clusters
* Collaborative notebooks
* Optimized Spark engine
* Built-in governance (Unity Catalog)

---

# 🔷 What is Apache Spark?

Apache Software Foundation developed
Apache Spark

## 🔹 Definition

Apache Spark is a **distributed computing engine** used for large-scale data processing.

It processes data:

* In-memory (fast)
* In parallel
* Across multiple machines (cluster)

## 🔹 Why Spark?

Traditional processing:

```
1 machine → slow → limited scale
```

Spark:

```
Many machines (Cluster) → Parallel processing → Fast
```

## 🔹 Spark Components

* Spark Core
* Spark SQL
* Spark Streaming
* MLlib
* GraphX

Databricks is built on Spark and enhances it.

---

# 🔷 Databricks Architecture (High-Level)

```
          +--------------------+
          |  Cloud Storage     |
          |  (ADLS / S3 / GCS) |
          +----------+---------+
                     |
                     v
        +---------------------------+
        |      Databricks Platform  |
        |---------------------------|
        | Workspace                 |
        | Clusters                  |
        | Notebooks                 |
        | Jobs / Workflows          |
        | Unity Catalog             |
        +---------------------------+
                     |
                     v
            +----------------+
            | BI / ML Tools  |
            +----------------+
```

---

# 🔷 Clusters in Databricks

## 🔹 What is a Cluster?

A **cluster** is a group of virtual machines used to run Spark jobs.

```
Driver Node  → Controls execution
Worker Nodes → Execute tasks
```

## 🔹 Types of Clusters

1. **All-purpose cluster**

   * Interactive analysis
   * Development

2. **Job cluster**

   * Runs scheduled jobs
   * Terminates after completion

## 🔹 Autoscaling

* Automatically increases/decreases worker nodes
* Cost efficient

---

# 🔷 Workspace & Notebooks

## 🔹 Workspace

The workspace is the main UI where you manage:

* Notebooks
* Clusters
* Jobs
* Libraries

## 🔹 Notebooks

Interactive development environment supporting:

* Python
* SQL
* Scala
* R

Features:

* %sql, %python magic commands
* Visualization
* Markdown documentation
* Collaboration

---

# 🔷 Administration & Access Control

Enterprise-level security features:

* Role-based access control (RBAC)
* Cluster permissions
* Notebook permissions
* Secret management
* Audit logs

Integrated with:

* Azure Active Directory (Azure)
* IAM (AWS)
* Google IAM (GCP)

---

# 🔷 Optimized Spark Engine (Photon)

## 🔹 What is Photon?

Photon is Databricks’ **vectorized query engine**.

It:

* Rewrites Spark execution engine in C++
* Optimizes SQL & Delta workloads
* Improves performance 2x–5x

Best for:

* SQL workloads
* Data warehousing

---

# 🔷 Unity Catalog

## 🔹 What is Unity Catalog?

Unity Catalog is a **centralized data governance solution**.

It manages:

* Data access control
* Metadata
* Lineage
* Auditing

Structure:

```
Metastore
   |
   +-- Catalog
         |
         +-- Schema
               |
               +-- Table
```

Provides:

* Fine-grained access control
* Column-level security
* Row-level security

---

# 🔷 Delta Lake

Delta Lake

## 🔹 What is Delta Lake?

Delta Lake is an **open-source storage layer** that adds:

* ACID transactions
* Schema enforcement
* Time travel
* Data versioning

It turns a Data Lake into a Lakehouse.

Example:

```
SELECT * FROM sales VERSION AS OF 5
```

---

# 🔷 Delta Live Tables (DLT)

## 🔹 What is DLT?

Delta Live Tables is a framework for building **reliable data pipelines**.

Features:

* Automatic dependency resolution
* Built-in data quality checks
* Incremental processing
* Monitoring UI

Example:

```
@dlt.table
def cleaned_data():
    return spark.read.table("bronze_table")
```

---

# 🔷 Workflows (Jobs)

Databricks Workflows allow you to:

* Schedule notebooks
* Create task dependencies
* Trigger pipelines
* Monitor failures

Example flow:

```
Task 1 → Bronze Load
Task 2 → Silver Transform
Task 3 → Gold Aggregation
```

Supports:

* Cron scheduling
* Event-based triggers

---

# 🔷 SQL Warehouse

## 🔹 What is SQL Warehouse?

Databricks SQL Warehouse is a **serverless SQL compute engine**.

Used by:

* Data analysts
* BI tools
* Power BI

Features:

* Auto-scaling
* Photon engine
* High concurrency

It behaves like a traditional data warehouse but runs on Lakehouse.

---

# 🔷 MLflow

MLflow

## 🔹 What is MLflow?

MLflow is used for:

* Experiment tracking
* Model versioning
* Model registry
* Deployment

Tracks:

* Parameters
* Metrics
* Models
* Artifacts

---

# 🔷 Databricks IQ

Databricks IQ is an AI-powered assistant integrated into Databricks.

It helps with:

* SQL query generation
* Code suggestions
* Error explanations
* Data insights

Built using generative AI.

---

# 🔷 Databricks Cloud Availability

Databricks is available on:

1. Microsoft Azure → Azure Databricks
2. Amazon Web Services → Databricks on AWS
3. Google Cloud → Databricks on GCP

All provide:

* Same Lakehouse platform
* Cloud-native integration
* Different cloud storage backend

| Cloud | Storage Used |
| ----- | ------------ |
| Azure | ADLS Gen2    |
| AWS   | S3           |
| GCP   | GCS          |

---

# 🔥 Quick Interview Summary

Databricks is:

* A managed Spark platform
* Built for Lakehouse architecture
* Provides governance (Unity Catalog)
* Optimized engine (Photon)
* Supports ETL, BI, ML in one platform
* Available on Azure, AWS, and GCP

---

