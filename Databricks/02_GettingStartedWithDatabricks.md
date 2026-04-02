## 🟢 2. Getting Started with Databricks (Hands-on Guide)

---

### ☁️ What is Databricks?

![Image](https://images.openai.com/static-rsc-4/R_TZBFDoLHfkc4hWzqNuJvEXI6wbHYP7NZIJ9TTE4HTqpX2zGBrzicxa9WaHGSNxWyyH-blxxHbYSnyqEnBGsR4y4n50Hbb2GBrZ4QA-08YtRxdgAhhZ0y_90rJd1CzRNzYrpcvnw5NCcyPTlgz-qytA42KGvUDQyD165hi-y4K1dmQJlFi1EzXlfACwa_6p?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/QRxk_J1RWYpVcouTep664Htf_FMv9jb97XEcQ6GZjUa_XvPROWh2FGrHlvH47HS9Lz92lrm90ioOvr0PndrinZQlaRen2O4V5KtHnq9AIj6u-FAvZ9jyXyB10W7INc-vIKlkaNSsoCoTYp7t95EGt7X1E4JtxEt5jIBJS5yq5cDdTlnRtOjmnaK4vrho2jeU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/d5HolRTfJ20xWNbutcYVGBP0Iur8uLjs2DNxBPIUlf7b0aF3u9qiYiSfYtBBYIQXmLESNdokMjBwRfrbwNtgJUDef6CNt9gxUQeg1Ps8c7V6DvQ2rnVnccJT5tdbXMb4XPcQGyTKyZ-2s0ce68xtiv9CqG16A5p6psWDcX1HhwVsTFY-GG5gneAacviSx1hK?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/qz69wnc2X8hgG7vHDpv6VkvFB4fd4qbKYKzm0NFsFp_QwR84WeeDMNe8tggsoqJFKUGKPc47RL-IQxLD83ZnvfF-Dnvfg4PZkE77cUvieQNWQnDKMCneQaEy30oRvfBrXpYLbYCv4Przu1X68GXXWrG1N0qjPFBd6rdIvSaAwWDygol-FctVP5Vik2-PpRtA?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/ENUCLCLcaw2gFkm-PjMEFupatqUYOxavan8kyUrtRByRWZSmlddF8ipFttCeHpbDgkbzk67giq9KxUAYqKHi2XCO2MFyGuP8TLy5N5ZQmibLjp9mDGYvxiKc07tajfgt_UCCmKWLDJ8Hh7l-4NvJTwBiIjGv6XiUydjXYB5Ah1PMgPmoYsfLutyqadvxynim?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NJQHvv9zE-uI7QgjvyOjuwsMn-3Lkts9lavQdBIKcfnQX-e3PmZUALFS57LQ7iHKX1dQl1FPv3pMK1Db4wTWsEkdmR1uvYXhzwpx3S889nXyTWqyuGdZEJ5rBqgD1WXYeamOZ8IETaZ29C2S6GcLJZvp7LkdKrpi8z8Cfno9tiFIXtjTiRxXWOO5K20v0ElX?purpose=fullsize)

**Databricks** is a **cloud platform built on top of Apache Spark** that makes working with big data much easier.

#### 🔑 Why use Databricks?

* No need to manually set up Spark clusters
* Interactive notebooks (like Jupyter but more powerful)
* Built-in collaboration
* Optimized performance with **Delta Lake**

---

## 🧭 Step 1: Create Databricks Account

1. Go to: [https://www.databricks.com/](https://www.databricks.com/)
2. Sign up (Community Edition is free)
3. Login to your workspace

👉 After login, you’ll see:

* Workspace
* Clusters
* Data
* Compute

---

## ⚙️ Step 2: Create a Cluster

A **cluster = group of machines running Spark**

### Steps:

1. Go to **Compute / Clusters**
2. Click **Create Cluster**
3. Give a name (e.g., `my-first-cluster`)
4. Choose:

   * Runtime (latest version)
   * Node type (default is fine)
5. Click **Create**

⏳ Takes ~2–5 minutes

---

## 📓 Step 3: Create a Notebook

### Steps:

1. Go to **Workspace**
2. Click **Create → Notebook**
3. Choose:

   * Language: Python (PySpark)
   * Attach your cluster

---

## ▶️ Step 4: Run Your First Spark Code

```python
df = spark.range(10)
display(df)
```

👉 What this does:

* Creates numbers from 0 to 9
* Displays them in a table

---

## 📂 Step 5: Load Data

### Option 1: From Table

```python
df = spark.table("default.my_table")
display(df)
```

### Option 2: From CSV

```python
df = spark.read.csv("/FileStore/tables/data.csv", header=True, inferSchema=True)
display(df)
```

---

## 🔍 Step 6: Basic Exploration

```python
df.show(5)
df.printSchema()
df.columns
df.count()
```

---

## 🧠 Step 7: Run SQL in Notebook

Databricks supports SQL directly 👇

```sql
%sql
SELECT * FROM default.my_table LIMIT 10
```

---

## 💾 Step 8: Save Data

```python
df.write.saveAsTable("my_new_table")
```

---

## 📁 Step 9: Databricks File System (DBFS)

* Storage layer in Databricks
* Path example:

```
/FileStore/tables/
```

Upload files via UI:

* Data → Upload File

---

## ⚡ Step 10: Key Tips (Important)

* Use `display()` for visualization
* Use `show()` for quick debugging
* Avoid too many `.count()` calls (expensive)
* Always attach notebook to a cluster

---

# ✅ Mini Practice (Do This)

Try this in your notebook:

```python
df = spark.range(100)

df_filtered = df.filter(df.id > 50)

display(df_filtered)
```

---

# 🎯 What You Learned

* What Databricks is
* How to:

  * Create cluster
  * Create notebook
  * Run Spark code
  * Load & explore data

---
