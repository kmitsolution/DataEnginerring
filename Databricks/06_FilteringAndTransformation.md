## 🟢 6. Filtering & Transformations (Build Real Logic)

Now we move from basics → **real data manipulation** in Apache Spark.

This is where you start thinking like a **Data Engineer**.

---

# 🔍 1. Advanced Filtering

---

### 🔹 Single Condition

```python
df.filter(df.imdb_rating > 8)
```

---

### 🔹 Multiple Conditions

```python
df.filter((df.imdb_rating > 8) & (df.release_year > 2000))
```

👉 OR condition:

```python
df.filter((df.industry == "bollywood") | (df.industry == "hollywood"))
```

---

### 🔹 Using `isin()` (Very Useful)

```python
df.filter(df.industry.isin("bollywood", "hollywood"))
```

---

### 🔹 Using `like()` (Pattern Matching)

```python
df.filter(df.title.like("%love%"))
```

---

### 🔹 Null Filtering

```python
df.filter(df.imdb_rating.isNotNull())
```

---

# ➕ 2. Column Transformations

---

### 🔹 Add New Column

```python
from pyspark.sql.functions import col

df = df.withColumn("rating_double", col("imdb_rating") * 2)
```

---

### 🔹 Rename + Transform Together

```python
df = df.withColumn("rating", col("imdb_rating") + 1)
```

---

# 🔀 3. Conditional Columns (`when / otherwise`)

Very important for real logic 👇

```python
from pyspark.sql.functions import when, col

df = df.withColumn(
    "rating_category",
    when(col("imdb_rating") >= 8, "Excellent")
    .when(col("imdb_rating") >= 6, "Good")
    .otherwise("Average")
)
```

---

# 🔤 4. String Transformations

```python
from pyspark.sql.functions import lower, upper, length

df = df.withColumn("title_lower", lower(col("title")))
df = df.withColumn("title_length", length(col("title")))
```

---

# 📅 5. Date Transformations

```python
from pyspark.sql.functions import year, month

df = df.withColumn("release_year", year(col("release_date")))
df = df.withColumn("release_month", month(col("release_date")))
```

---

# 🔗 6. Combining Multiple Transformations

```python
from pyspark.sql.functions import col, when

df = df.withColumn("rating_category",
        when(col("imdb_rating") >= 8, "Excellent").otherwise("Other")
    ) \
    .filter(col("release_year") > 2000) \
    .select("title", "rating_category", "release_year")
```

👉 This is how real pipelines look

---

# 🧠 7. Using SQL Style (`expr`)

```python
from pyspark.sql.functions import expr

df = df.withColumn("rating_bonus", expr("imdb_rating + 0.5"))
```

---

# 🎯 8. Real Example (Movies Dataset)

```python
from pyspark.sql.functions import col, when, lower

df = spark.table("workspace.default.movies")

df_transformed = df \
    .filter(df.release_year >= 2000) \
    .withColumn("industry", lower(col("industry"))) \
    .withColumn(
        "rating_category",
        when(col("imdb_rating") >= 8, "Excellent")
        .when(col("imdb_rating") >= 6, "Good")
        .otherwise("Average")
    ) \
    .select("title", "industry", "imdb_rating", "rating_category")

display(df_transformed)
```

---

# ⚡ 9. Key Patterns You MUST Remember

---

### ✅ Pattern 1: Filter Early

```python
df.filter(...)
```

👉 Reduces data → improves performance

---

### ✅ Pattern 2: Chain Transformations

```python
df.withColumn(...).filter(...).select(...)
```

---

### ✅ Pattern 3: Use Built-in Functions

👉 Faster than UDFs

---

# ❌ Common Mistakes

* Using Python `if` instead of `when`
* Forgetting parentheses in filters
* Writing too many separate steps (not chaining)

---

# 🧠 Interview Insight

👉 Question:
**“How do you create conditional columns in Spark?”**

Answer:

* Use `when()` and `otherwise()`

---

# ✅ Summary

* Filtering = selecting rows
* Transformations = modifying data
* Key tools:

  * `filter()`
  * `withColumn()`
  * `when()`
  * string/date functions
* This is where real data logic is built

---

