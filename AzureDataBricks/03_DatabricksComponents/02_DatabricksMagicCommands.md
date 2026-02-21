
#  Databricks Magic Commands (Updated for Unity Catalog)

Works with:

* Unity Catalog enabled workspace
* No public DBFS root
* Volumes
* External locations

---

# 🔷 1️⃣ %sql (Unity Catalog Aware)

Use `%sql` to work with:

* Catalog
* Schema
* Tables
* Volumes
* External locations

---

## 🔹 Show Catalogs

```sql
%sql
SHOW CATALOGS;
```

---

## 🔹 Use Catalog

```sql
%sql
USE CATALOG main;
```

---

## 🔹 Show Schemas

```sql
%sql
SHOW SCHEMAS;
```

---

## 🔹 Use Schema

```sql
%sql
USE SCHEMA default;
```

---

## 🔹 Create Table in Unity Catalog

```sql
%sql
CREATE TABLE sales_data (
  id INT,
  amount DOUBLE
);
```

---

## 🔹 Select Data

```sql
%sql
SELECT * FROM sales_data;
```

---

# 🔷 2️⃣ %fs (With Unity Catalog Volumes)

⚠️ Important: `/mnt` may not work anymore.

Instead use:

```
/Volumes/<catalog>/<schema>/<volume>/
```

---

## 🔹 List Volume Files

```python
%fs ls /Volumes/main/default/raw_data
```

---

## 🔹 Create Folder in Volume

```python
%fs mkdirs /Volumes/main/default/raw_data/new_folder
```

---

## 🔹 Remove Folder

```python
%fs rm /Volumes/main/default/raw_data/new_folder -r
```

---

# 🔷 3️⃣ %pip (Same as Before)

Still works the same.

## 🔹 Install Package

```python
%pip install pandas
```

## 🔹 Restart Python (If Needed)

```python
dbutils.library.restartPython()
```

---

# 🔷 4️⃣ %run (Reusable Notebooks)

Still used for modular notebook design.

Example:

```python
%run /Workspace/Shared/utils/common_functions
```

⚠️ Path format may vary depending on workspace folder.

---

# 🔷 5️⃣ Accessing Data Using ABFSS (Recommended Instead of Mount)

Instead of:

```
/mnt/datalake
```

Use:

```
abfss://container@storageaccount.dfs.core.windows.net/
```

---

## 🔹 Example: Read Delta Table

```python
df = spark.read.format("delta").load(
  "abfss://container@storageaccount.dfs.core.windows.net/bronze/sales"
)
display(df)
```

---

# 🔷 6️⃣ Unity Catalog Volume Write Example

## 🔹 Write CSV to Volume

```python
df.write.mode("overwrite").csv(
  "/Volumes/main/default/raw_data/sales_csv"
)
```

---

## 🔹 Read from Volume

```python
df = spark.read.csv(
  "/Volumes/main/default/raw_data/sales_csv",
  header=True
)
display(df)
```

---

# 🔷 7️⃣ Create Volume (Unity Catalog SQL)

```sql
%sql
CREATE VOLUME raw_data;
```

---

# 🔷 8️⃣ Create External Location (Admin Use)

```sql
%sql
CREATE EXTERNAL LOCATION my_external_loc
URL 'abfss://container@storageaccount.dfs.core.windows.net/'
WITH (STORAGE CREDENTIAL my_credential);
```

---

# 🔷 9️⃣ Important dbutils Commands (Still Valid)

## 🔹 List Files

```python
dbutils.fs.ls("/Volumes/main/default/raw_data")
```

---

## 🔹 Get Notebook Context

```python
dbutils.notebook.entry_point.getDbutils().notebook().getContext()
```

---

# 🔷 Old vs New (Important for Interview)

| Old Way                  | New Unity Catalog Way  |
| ------------------------ | ---------------------- |
| /mnt                     | /Volumes               |
| DBFS root                | Unity Catalog volumes  |
| Mount storage            | External location      |
| No fine-grained security | Catalog-based security |

---

# 🔥 Real Production Flow (Modern Databricks)

```text
1. USE CATALOG main
2. USE SCHEMA bronze
3. Read from ABFSS
4. Write to Delta Table
5. Store files in Volume
6. Govern access using Unity Catalog
```

---

# 🔷 Most Important Interview Points

### Q: Why avoid /mnt now?

Because public DBFS root is disabled in Unity Catalog-enabled workspaces.

### Q: What replaces mounts?

External Locations + Volumes.

### Q: How do you access storage now?

Using:

* abfss path
* Unity Catalog volumes

---

# 🎯 Final Best Practice

For new projects:

✅ Use Unity Catalog
✅ Use Volumes
✅ Use ABFSS direct paths
❌ Avoid legacy DBFS root

---

