In **Azure Databricks**, `dbutils` is a built-in utility library that helps you interact with:

* File system
* Secrets
* Notebooks
* Widgets
* Jobs
* Libraries

Works inside:
Azure Databricks

---

# 🔷 What is dbutils?

`dbutils` = Databricks Utilities

It provides helper functions for managing:

```text
dbutils.fs        → File system
dbutils.secrets   → Secrets management
dbutils.widgets   → Parameterization
dbutils.notebook  → Notebook orchestration
dbutils.jobs      → Job information
dbutils.library   → Library management
```

---

# 🔷 1️⃣ dbutils.fs (File System Utility)

Used to interact with:

* Unity Catalog Volumes
* DBFS (if enabled)
* ADLS (via mounted or direct paths)

---

## ✅ List Files

```python
dbutils.fs.ls("/Volumes/main/default/raw_data")
```

---

## ✅ Make Directory

```python
dbutils.fs.mkdirs("/Volumes/main/default/raw_data/new_folder")
```

---

## ✅ Remove File / Folder

```python
dbutils.fs.rm("/Volumes/main/default/raw_data/new_folder", recurse=True)
```

---

## ✅ Copy Files

```python
dbutils.fs.cp(
    "/Volumes/main/default/raw_data/file1.csv",
    "/Volumes/main/default/raw_data/backup_file1.csv"
)
```

---

## ✅ Move Files

```python
dbutils.fs.mv(
    "/Volumes/main/default/raw_data/file1.csv",
    "/Volumes/main/default/raw_data/archive/file1.csv"
)
```

---

# 🔷 2️⃣ dbutils.secrets (Secrets Utility)

Used to securely store credentials.

Never hardcode:

❌ Bad:

```python
key = "my-storage-key"
```

---

## ✅ Get Secret

```python
storage_key = dbutils.secrets.get(
    scope="my-secret-scope",
    key="storage-key"
)
```

---

## ✅ Use Secret in Spark Config

```python
spark.conf.set(
    "fs.azure.account.key.storageaccount.dfs.core.windows.net",
    storage_key
)
```

Used for:

* ADLS access
* API keys
* Database passwords

---

# 🔷 3️⃣ dbutils.widgets (Parameterization)

Used to pass parameters to notebooks.

Very important for Jobs.

---

## ✅ Create Text Widget

```python
dbutils.widgets.text("env", "dev")
```

---

## ✅ Get Widget Value

```python
env = dbutils.widgets.get("env")
print(env)
```

---

## ✅ Dropdown Widget

```python
dbutils.widgets.dropdown(
    "environment",
    "dev",
    ["dev", "test", "prod"]
)
```

---

## ✅ Remove Widget

```python
dbutils.widgets.remove("env")
```

---

# 🔷 4️⃣ dbutils.notebook (Notebook Orchestration)

Used to run notebooks programmatically.

---

## ✅ Run Another Notebook

```python
result = dbutils.notebook.run(
    "/Workspace/Shared/bronze_notebook",
    timeout_seconds=60,
    arguments={"env": "prod"}
)
```

---

## ✅ Exit Notebook with Value

Inside child notebook:

```python
dbutils.notebook.exit("Success")
```

---

## 🔥 Difference Between %run and dbutils.notebook.run()

| %run                    | dbutils.notebook.run()   |
| ----------------------- | ------------------------ |
| Inline execution        | Separate execution       |
| Shares variables        | Does not share variables |
| Used for modular coding | Used for orchestration   |

---

# 🔷 5️⃣ dbutils.jobs

Used inside job runs to get metadata.

---

## ✅ Get Job Run Info

```python
job_id = dbutils.jobs.taskValues.get("job_id")
```

Mostly used in production workflows.

---

# 🔷 6️⃣ dbutils.library

Used to manage libraries.

---

## ✅ Restart Python

```python
dbutils.library.restartPython()
```

Used after:

```python
%pip install package_name
```

---

# 🔷 Real Production Example (End-to-End)

```python
# Step 1: Get environment parameter
dbutils.widgets.text("env", "dev")
env = dbutils.widgets.get("env")

# Step 2: Get storage secret
storage_key = dbutils.secrets.get(
    scope="prod-scope",
    key="storage-key"
)

# Step 3: List files in volume
files = dbutils.fs.ls("/Volumes/main/default/raw_data")
display(files)

# Step 4: Run silver notebook
result = dbutils.notebook.run(
    "/Workspace/Silver/02_clean_sales",
    300,
    {"env": env}
)

print("Notebook result:", result)
```

---

# 🔷 Best Practices for dbutils

✔ Use secrets instead of hardcoded credentials
✔ Use widgets for parameterization
✔ Use notebook.run for orchestration
✔ Avoid using legacy `/mnt` paths
✔ Use Unity Catalog volumes

---

# 🔥 Interview Questions

### Q1: What is dbutils?

Databricks utility library for file system, secrets, widgets, and notebook orchestration.

### Q2: How do you securely access storage?

Using `dbutils.secrets.get()`.

### Q3: How do you pass parameters to a notebook?

Using `dbutils.widgets`.

### Q4: Difference between %run and dbutils.notebook.run()?

%run shares context; notebook.run executes separately.

---

# 🎯 Quick Summary Table

| Utility          | Purpose                |
| ---------------- | ---------------------- |
| dbutils.fs       | File system operations |
| dbutils.secrets  | Secret management      |
| dbutils.widgets  | Parameterization       |
| dbutils.notebook | Run notebooks          |
| dbutils.jobs     | Job metadata           |
| dbutils.library  | Manage libraries       |

---

