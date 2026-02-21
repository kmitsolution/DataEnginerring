# 🚀 Databricks Notebook Best Practices (Beginner → Advanced)

Applies to:
Azure Databricks with **Unity Catalog enabled**

This guide is structured for GitHub notes and interview preparation.

---

# 🔷 1️⃣ Workspace & Folder Structure (Start Clean)

Before writing code, organize properly.

## ✅ Recommended Folder Structure

```
Workspace/
 ├── Shared/
 │    ├── utils/
 │    ├── configs/
 │
 ├── Bronze/
 ├── Silver/
 ├── Gold/
 │
 ├── Jobs/
 └── Experiments/
```

### Why?

* Separation of concerns
* Easier collaboration
* Cleaner production deployment

---

# 🔷 2️⃣ Use Clear Notebook Naming Convention

❌ Bad:

```
test1
new notebook
abc
```

✅ Good:

```
01_bronze_ingestion_sales
02_silver_clean_sales
03_gold_sales_aggregation
```

Benefits:

* Execution order clear
* Easy orchestration
* Professional structure

---

# 🔷 3️⃣ Start Every Notebook with Markdown Documentation

Use `%md` for clarity.

```markdown
%md
# Bronze Layer - Sales Ingestion

## Source:
- ADLS container: raw
- Format: CSV

## Target:
- Unity Catalog Table: main.bronze.sales_raw
```

Why?

* Self-documenting code
* Easy onboarding
* Interview-friendly

---

# 🔷 4️⃣ Use Parameters (Avoid Hardcoding)

❌ Bad:

```python
path = "abfss://raw@storage.dfs.core.windows.net/sales/"
```

✅ Good (Widgets):

```python
dbutils.widgets.text("env", "dev")
env = dbutils.widgets.get("env")
```

Use:

* For dev/test/prod
* For reusability
* For Jobs

---

# 🔷 5️⃣ Avoid Using `/mnt` (Modern Approach)

With Unity Catalog:

❌ Avoid:

```
/mnt/datalake
```

✅ Use:

```
/Volumes/catalog/schema/volume
```

or

```
abfss://container@storageaccount.dfs.core.windows.net/
```

---

# 🔷 6️⃣ Always Use Explicit Schema

❌ Bad:

```python
df = spark.read.csv(path, header=True)
```

✅ Good:

```python
from pyspark.sql.types import *

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("amount", DoubleType(), True)
])

df = spark.read.schema(schema).csv(path, header=True)
```

Why?

* Better performance
* Avoid schema inference errors
* Production-ready

---

# 🔷 7️⃣ Use Delta Format (Always)

❌ Don’t write parquet directly in production.

✅ Use Delta:

```python
df.write.format("delta") \
  .mode("overwrite") \
  .saveAsTable("main.bronze.sales_raw")
```

Why?

* ACID
* Time travel
* Schema enforcement

---

# 🔷 8️⃣ Follow Medallion Architecture

Notebook separation:

```
Bronze → Raw ingestion
Silver → Cleaning & joins
Gold → Aggregations & KPIs
```

Never mix logic of multiple layers in one notebook.

---

# 🔷 9️⃣ Error Handling (Important for Jobs)

Use try-except:

```python
try:
    df.write.format("delta").mode("append").saveAsTable("main.bronze.sales_raw")
except Exception as e:
    print("Error occurred:", e)
    raise
```

For production:

* Log properly
* Fail fast

---

# 🔷 🔟 Use Logging Instead of print()

Better approach:

```python
import logging

logger = logging.getLogger("sales_job")
logger.setLevel(logging.INFO)

logger.info("Ingestion started")
```

Why?

* Professional
* Production ready

---

# 🔷 1️⃣1️⃣ Avoid Large Collect()

❌ Dangerous:

```python
df.collect()
```

Brings full dataset to driver memory.

✅ Use:

```python
df.show(10)
```

or

```python
df.limit(10).display()
```

---

# 🔷 1️⃣2️⃣ Optimize Writes

Use partitioning carefully:

```python
df.write.format("delta") \
  .partitionBy("date") \
  .mode("append") \
  .saveAsTable("main.silver.sales_clean")
```

Avoid:

* Over-partitioning
* Too many small files

---

# 🔷 1️⃣3️⃣ Use Reusable Utility Notebooks

Create:

```
/Shared/utils/common_functions
```

Call using:

```python
%run /Workspace/Shared/utils/common_functions
```

Good for:

* Validation functions
* Logging utilities
* Common transformations

---

# 🔷 1️⃣4️⃣ Use Jobs Instead of Manual Runs

Development:

* Interactive cluster

Production:

* Job cluster
* Scheduled workflow

Never run production pipelines manually.

---

# 🔷 1️⃣5️⃣ Cluster Best Practices

For development:

* Small cluster
* Auto terminate 30–60 mins

For production:

* Job cluster
* Autoscaling enabled
* Photon enabled

---

# 🔷 1️⃣6️⃣ Code Cleanliness

Follow:

* PEP8 for Python
* Proper indentation
* No unnecessary commented code
* Modular functions

---

# 🔷 1️⃣7️⃣ Security Best Practices

✅ Use:

* Unity Catalog
* Role-based access
* Managed identity
* Secret scopes

❌ Avoid:

* Hardcoding credentials
* Public DBFS root
* Exposing keys

---

# 🔷 1️⃣8️⃣ Version Control (Very Important)

Never rely only on workspace.

Integrate with:

* Azure DevOps
* GitHub

Use:

* Repos feature in Databricks
* Branching strategy

---

# 🔷 1️⃣9️⃣ Performance Best Practices

* Use broadcast joins for small tables
* Avoid unnecessary shuffle
* Cache only when needed
* Use OPTIMIZE on Delta tables
* Enable Photon

---

# 🔷 2️⃣0️⃣ Production Notebook Checklist

Before deploying:

✔ Uses Unity Catalog
✔ No hardcoded paths
✔ Explicit schema
✔ Delta format
✔ Error handling
✔ Parameterized
✔ Logging added
✔ Tested on small data

---

# 🔥 Common Beginner Mistakes

| Mistake                    | Why Bad          |
| -------------------------- | ---------------- |
| Using /mnt                 | Deprecated       |
| Using inferSchema          | Slow             |
| Using collect()            | OOM risk         |
| Mixing Bronze & Gold logic | Poor design      |
| No documentation           | Hard to maintain |

---

# 🎯 Final Professional Structure (Example)

```
01_bronze_sales_ingestion
02_silver_sales_cleaning
03_gold_sales_kpi
04_job_orchestration
```

Each notebook:

* Markdown header
* Parameters
* Explicit schema
* Delta write
* Logging
* Error handling

---

#  Interview Summary Answer

Databricks notebook best practices include:

* Clear folder structure
* Medallion architecture separation
* Use Delta format
* Use Unity Catalog
* Parameterization
* Logging and error handling
* Avoid collect()
* Version control integration
* Production-ready job orchestration

---


Tell me what you want next 🚀
