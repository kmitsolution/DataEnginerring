##  5. Data Cleaning & Preprocessing (Very Practical)

This is one of the **most important real-world skills** in Apache Spark — because real data is always messy.

---

# 🧹 1. Understanding Dirty Data

Typical issues:

* ❌ Missing values (nulls)
* ❌ Wrong data types
* ❌ Duplicate records
* ❌ Inconsistent formats (e.g., "USA", "us", "United States")

---

# 🔍 2. Inspect Data First (Always Do This)

```python
df.printSchema()
df.show(5)
df.describe().show()
```

👉 Goal: Understand structure before cleaning

---

# ⚠️ 3. Handling Null Values

---

### 🔹 Check Null Counts

```python
from pyspark.sql.functions import col, sum

df.select([sum(col(c).isNull().cast("int")).alias(c) for c in df.columns]).show()
```

---

### 🔹 Drop Null Rows

```python
df.dropna().show()
```

👉 Drop only specific columns:

```python
df.dropna(subset=["imdb_rating"])
```

---

### 🔹 Fill Null Values

```python
df.fillna(0)
df.fillna({"imdb_rating": 0})
```

---

# 🔄 4. Remove Duplicates

```python
df.dropDuplicates()
```

👉 Based on specific columns:

```python
df.dropDuplicates(["title"])
```

---

# 🔤 5. Fix Data Types (Very Important)

Sometimes data is read incorrectly (e.g., string instead of int)

```python
df.printSchema()
```

---

### 🔹 Convert Types

```python
from pyspark.sql.functions import col

df = df.withColumn("release_year", col("release_year").cast("int"))
df = df.withColumn("imdb_rating", col("imdb_rating").cast("double"))
```

---

# 🧼 6. Clean Text Data

---

### 🔹 Lowercase / Uppercase

```python
from pyspark.sql.functions import lower, upper

df = df.withColumn("industry", lower(col("industry")))
```

---

### 🔹 Trim Spaces

```python
from pyspark.sql.functions import trim

df = df.withColumn("title", trim(col("title")))
```

---

### 🔹 Replace Values

```python
df.replace("bollywod", "bollywood")
```

---

# 📅 7. Working with Dates

---

### 🔹 Convert to Date Type

```python
from pyspark.sql.functions import to_date

df = df.withColumn("release_date", to_date(col("release_date"), "yyyy-MM-dd"))
```

---

# 🔎 8. Filtering Bad Data

```python
df.filter(df.imdb_rating.isNotNull())
df.filter(df.imdb_rating > 0)
```

---

# 🧪 9. Real Cleaning Example (Movies Dataset)

```python
from pyspark.sql.functions import col, lower, trim

df = spark.table("workspace.default.movies")

# Remove duplicates
df = df.dropDuplicates()

# Handle nulls
df = df.dropna(subset=["imdb_rating"])

# Fix types
df = df.withColumn("release_year", col("release_year").cast("int"))

# Clean text
df = df.withColumn("industry", lower(trim(col("industry"))))

# Filter valid data
df = df.filter(df.imdb_rating > 0)

display(df)
```

---

# ⚡ 10. Best Practices

✔️ Always:

* Inspect data first
* Handle nulls early
* Fix schema before analysis
* Filter invalid data

❌ Avoid:

* Blindly dropping all nulls
* Ignoring data types
* Cleaning after heavy processing

---

# 🧠 Interview Tip

👉 Common question:
**“How do you handle null values in Spark?”**

Answer:

* Drop (`dropna`)
* Fill (`fillna`)
* Filter (`isNotNull`)
* Depends on business logic

---

# ✅ Summary

* Real data is messy → cleaning is essential
* Key steps:

  * Handle nulls
  * Remove duplicates
  * Fix data types
  * Clean text
* Clean data = better performance + accuracy

---

