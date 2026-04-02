## 🟢 7. Aggregations & GroupBy (Core Analytics in Spark)

This is where you turn raw data into **insights** 📊 using Apache Spark.

---

# 📊 1. What is Aggregation?

Aggregation = **summarizing data**

👉 Examples:

* Average rating
* Total sales
* Count of movies

---

# 🔢 2. Basic Aggregation Functions

```python
from pyspark.sql.functions import count, sum, avg, max, min
```

---

### 🔹 Example:

```python
df.select(avg("imdb_rating")).show()
```

---

# 🧱 3. GroupBy (Most Important)

Group data by a column and apply aggregation.

---

### 🔹 Count Movies per Industry

```python
df.groupBy("industry").count().show()
```

---

### 🔹 Average Rating per Industry

```python
df.groupBy("industry").avg("imdb_rating").show()
```

---

### 🔹 Multiple Aggregations

```python
df.groupBy("industry").agg(
    avg("imdb_rating").alias("avg_rating"),
    count("*").alias("movie_count")
).show()
```

---

# 📈 4. Sorting Aggregated Data

```python
df.groupBy("industry") \
  .avg("imdb_rating") \
  .sort("avg(imdb_rating)", ascending=False) \
  .show()
```

👉 Cleaner:

```python
from pyspark.sql.functions import avg

df.groupBy("industry") \
  .agg(avg("imdb_rating").alias("avg_rating")) \
  .orderBy("avg_rating", ascending=False) \
  .show()
```

---

# 🔍 5. Filtering After Aggregation (HAVING)

```python
from pyspark.sql.functions import count

df.groupBy("industry") \
  .agg(count("*").alias("movie_count")) \
  .filter("movie_count > 10") \
  .show()
```

👉 Equivalent to SQL HAVING

---

# 🔗 6. GroupBy Multiple Columns

```python
df.groupBy("industry", "release_year") \
  .count() \
  .show()
```

---

# 🎯 7. Real Example (Movies Dataset)

```python
from pyspark.sql.functions import avg, count

df = spark.table("workspace.default.movies")

result = df.groupBy("industry") \
    .agg(
        avg("imdb_rating").alias("avg_rating"),
        count("*").alias("total_movies")
    ) \
    .orderBy("avg_rating", ascending=False)

display(result)
```

---

# ⚡ 8. Important Concept: Shuffle

⚠️ `groupBy()` causes **shuffle**

👉 What happens:

* Data moves across partitions
* Expensive operation

---

### 🚨 Tip:

* Reduce data before groupBy

```python
df.filter(df.release_year > 2000).groupBy("industry").count()
```

---

# 🧠 9. Distinct vs GroupBy

---

### 🔹 Distinct Values

```python
df.select("industry").distinct().show()
```

---

### 🔹 Count Distinct

```python
from pyspark.sql.functions import countDistinct

df.select(countDistinct("industry")).show()
```

---

# 🧩 10. Pivot (Advanced but Useful)

```python
df.groupBy("industry") \
  .pivot("release_year") \
  .count() \
  .show()
```

👉 Converts rows → columns

---

# ❌ Common Mistakes

* Not using `.alias()` → messy column names
* Grouping without filtering → slow
* Forgetting shuffle cost

---

# 🧠 Interview Questions

👉 **Q: What happens during groupBy?**
✔️ Data shuffle across partitions

👉 **Q: Difference between groupBy and reduceByKey?**
✔️ groupBy = DataFrame API
✔️ reduceByKey = RDD API

---

# ✅ Summary

* Aggregations = summarizing data
* `groupBy()` = most important operation
* Common functions:

  * `count()`, `avg()`, `sum()`
* Shuffle = expensive (optimize carefully)

---

