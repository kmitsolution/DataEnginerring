## 🟢 4. Working with DataFrames (Hands-On)

This is where you’ll spend **most of your time in Spark**. Since you already started using DataFrames 👍, we’ll make this very practical.

---

## 📌 1. What is a DataFrame?

A **DataFrame** in Apache Spark is:

* A distributed table (like SQL table)
* With rows + columns
* Optimized for big data processing

👉 Think:

* Pandas DataFrame (small data)
* Spark DataFrame (big data)

---

## 📥 2. Creating DataFrames

---

### 🔹 From Table (Databricks)

```python
df = spark.table("workspace.default.movies")
display(df)
```

---

### 🔹 From CSV

```python
df = spark.read.csv("/FileStore/tables/movies.csv", header=True, inferSchema=True)
display(df)
```

---

### 🔹 From List (for testing)

```python
data = [("A", 10), ("B", 20)]
df = spark.createDataFrame(data, ["name", "value"])
display(df)
```

---

## 🔍 3. Exploring Data

```python
df.show(5)           # quick view
df.printSchema()     # structure
df.columns           # column names
df.count()           # total rows
```

---

## 🧱 4. Selecting Columns

```python
df.select("title", "imdb_rating").show()
```

👉 Multiple ways:

```python
df.select(df.title, df.imdb_rating)
```

---

## 🔎 5. Filtering Rows

```python
df.filter(df.imdb_rating > 8).show()
```

👉 Multiple conditions:

```python
df.filter((df.imdb_rating > 8) & (df.release_year > 2000))
```

👉 Cleaner:

```python
df.filter(df.release_year.between(2000, 2010))
```

---

## ➕ 6. Adding / Modifying Columns

```python
from pyspark.sql.functions import col

df = df.withColumn("rating_plus_one", col("imdb_rating") + 1)
```

---

## ❌ 7. Dropping Columns

```python
df.drop("unwanted_column")
```

---

## ✏️ 8. Renaming Columns

```python
df.withColumnRenamed("imdb_rating", "rating")
```

---

## 🔄 9. Sorting Data

```python
df.sort("imdb_rating")              # ascending
df.sort(df.imdb_rating.desc())     # descending
```

---

## 🔢 10. Remove Duplicates

```python
df.dropDuplicates()
```

---

## ⚠️ 11. Handling Null Values

```python
df.dropna()                # remove null rows
df.fillna(0)               # replace nulls
```

---

## 🎯 12. Real Example (Movies Dataset)

This is very close to what you already wrote 👇

```python
df = spark.table("workspace.default.movies")

# Select columns
newdf = df.select("title", "imdb_rating", "industry")

# Filter movies between 2000–2010
movies_2000_2010 = df.filter(df.release_year.between(2000, 2010))

display(newdf)
display(movies_2000_2010)
```

---

## ⚡ 13. Important Tips

* Use `display()` in Databricks for better UI
* Use `show()` for quick debugging
* Avoid too many `.count()` calls (expensive ⚠️)
* Always filter early → improves performance

---

## 🧠 14. Common Beginner Mistakes

❌ Using `and` instead of `&`
✔️ Correct:

```python
(df.age > 20) & (df.salary > 5000)
```

❌ Forgetting parentheses
✔️ Always wrap conditions

❌ Expecting immediate execution
✔️ Spark is lazy (runs only on action)

---

## ✅ Summary

* DataFrame = distributed table
* Core operations:

  * `select()`
  * `filter()`
  * `withColumn()`
  * `drop()`
* Used for **almost all Spark work**

---

