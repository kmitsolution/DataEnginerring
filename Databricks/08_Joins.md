## 🟢 8. Joins in Spark (Very Important 🔥)

Joins are **used everywhere in real projects** — combining datasets is a core skill in Apache Spark.

---

# 🔗 1. What is a Join?

A **join** combines two DataFrames based on a common column.

👉 Example:

* Movies table 🎬
* Ratings table ⭐
  → Join using `movie_id`

---

# 🧱 2. Basic Syntax

```python
df1.join(df2, on="common_column", how="type")
```

---

# 🔹 3. Types of Joins

---

## ✅ 1. Inner Join (Most Common)

Only matching rows from both tables

```python
df1.join(df2, on="id", how="inner")
```

👉 Use when:

* You only want **common data**

---

## ✅ 2. Left Join

All rows from left + matching from right

```python
df1.join(df2, on="id", how="left")
```

👉 Use when:

* You don’t want to lose data from left table

---

## ✅ 3. Right Join

All rows from right + matching from left

```python
df1.join(df2, on="id", how="right")
```

---

## ✅ 4. Full Outer Join

All rows from both tables

```python
df1.join(df2, on="id", how="outer")
```

---

## 🚫 Visual Understanding

![Image](https://images.openai.com/static-rsc-4/HYTshsVfu7nlPvYctpshtxr3RwJc9G9RPH8w_DxMykR3w-75fuKKogsbmOD3Si6DmlOOeW-HQ13hj-xgZ5L0UPkl--WlCWsDt7Da2C24XaRYx1ZGhABwDLkLM3tbMOiqAKS0yfEO1TYiGzQQv-ND2j4LkbnnV7bRdQy3lUEdpDy_tQEb65_57LPRWEWs8jgy?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/VCskIbSta0ck0EhdotogVZjdVEZOd6ufEEZ8FZtF1f-d7MG3Eao6XRk3jvlKcO1_HkfFIx3-LoD73JtnEZZdl9QgeMsa003lLDgc1rOFco6wjuMswdsO4B-GRkh6xkjnyUfSejJK0L7gFTnKWkiDFesLo5i8W-j2xqB6twn6TS8aKHsS_SVvESkiQnzqwCMa?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/soJCiNloI3xYZ-fsYgHsmJ8YEiXZ48ntWO0Adbo_r59HcMR6MlQqjM-SdjC1fDzi8OgsmTBbg6kPI6H7-RQ0khoC0KZgHa6poZ5qQ-dH-mGYCheZpUOVKI6OOtjSYT-RrrqF76WWaTjOX82bc7G9evg_QA8kbi8c08qf_uIlPkg6oW0d9HYbBL9mBn2ld6nZ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/3rNFrqV4u_B6wVZ0bFjDOmO-QhUxLBy2izCDF74tMp4Qbb7zCCiNxgaFNwIZP4-LOAk4loUTpOe9AlV5vSG5oNy3hYSHCRy0QEhEnKmapRa_zzp6IVGqW08KN1dRTLB4oi_0i5daY8lYcAREILN1rRXm0i6Ywi0eT0Wo3fnc1EV7Lbj5dzHF-Mv9gMxGVfM8?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/hYkPjYbRRxvz-meI3aQCo6oxysKLRh9fU55mcNU82EUcxzggQ_9mD-FtFxM5d5zmWmLQBjuAWVMdqPH17wvSUH3hjZUFvAz87As5Bad7z7JtV4OYdDwUz620sZ_k0t-i7JzZOmTgKHGNeQP9fsEkg6FAmho7gYf58PGNIJjP-v8uaVIWE-r2v49OaXqN3Rsw?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/KovWQCl1feoSaqMPWrSMsUOq8sjs1R86VvkejrR3oEYhJaECepoqVZOHtZ3JdW416L5bjv282woedH-Conf4zOOwvdWcLeUmrfwKux9O2ewKNTCbJm4ZjZt-ZPXMbOrRVvzR1Tl6hf5vnw-FHkksiipouoUhqZ0O_vF_EZak1Xr9uKhyOb-3Eqs-jTEPnJj0?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/oL5SI_s97M0tIYFma67EMxMzRfwhDq79h5Tu-llbAKjGPzWTchvvfQ8zZkTTkdkeTBRAp1aOKGROYZSlXs90UIoEmO-MlpSk34GtxROCKOcxSNAOUug24tL0DYrDO5HuG8lD0P-kTVd8_DfIE7xNwXV_vDGXOWrwFS_RjHzCDmI-e6giX-kWdYL1uxAZ4-gS?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/C7SVR7EFfXJaTCHY2oB8qGMoFeSeJH9fuvajuvEz0LzDLwH0jFJqbJE83Tqenfjahw6rNeXqBob1VK_6ZUjhvagw7Ymaus6mamNJNMbBjwXB7xS42Xmvyci3fo61upEnyd6K1OlMyS691-GrI9cvwgIjS--9VLHRZMijCQLKyqsF4v3fMGuqWQyGEWlgBGEg?purpose=fullsize)

---

# 🔎 4. Join on Different Column Names

```python
df1.join(df2, df1.id == df2.movie_id, "inner")
```

---

# ⚠️ 5. Handling Duplicate Columns

After join, same column names can cause confusion.

---

### 🔹 Solution 1: Select needed columns

```python
df1.join(df2, "id").select(df1.id, df1.name, df2.rating)
```

---

### 🔹 Solution 2: Rename before join

```python
df2 = df2.withColumnRenamed("id", "movie_id")
```

---

# 🎯 6. Real Example (Movies Dataset)

---

### Suppose:

* `movies` → movie details
* `ratings` → ratings data

```python
movies = spark.table("workspace.default.movies")
ratings = spark.table("workspace.default.ratings")
```

---

### 🔹 Join Example

```python
df_joined = movies.join(ratings, on="movie_id", how="inner")

display(df_joined)
```

---

# 📊 7. Join + Aggregation (Real Use Case)

```python
from pyspark.sql.functions import avg

df = movies.join(ratings, "movie_id") \
    .groupBy("industry") \
    .agg(avg("rating").alias("avg_rating"))

display(df)
```

👉 This is **real-world pipeline logic**

---

# ⚡ 8. Performance: Broadcast Join (VERY IMPORTANT)

If one table is small → use broadcast

```python
from pyspark.sql.functions import broadcast

df.join(broadcast(small_df), "id")
```

👉 Why?

* Avoids shuffle
* Much faster 🚀

---

# 🔥 9. Shuffle in Joins

⚠️ Joins can cause **heavy shuffle**

👉 Optimize by:

* Filtering before join
* Using broadcast
* Reducing columns

---

# 🧠 10. Join Types Summary

| Join Type | Result                   |
| --------- | ------------------------ |
| Inner     | Matching rows only       |
| Left      | All left + matched right |
| Right     | All right + matched left |
| Outer     | All rows from both       |

---

# ❌ Common Mistakes

* Joining without condition ❌
* Not handling duplicate columns ❌
* Joining large tables without optimization ❌

---

# 🧠 Interview Questions

👉 **Q: What is broadcast join?**
✔️ Joining small table efficiently without shuffle

👉 **Q: Which join is most used?**
✔️ Inner join

👉 **Q: Why are joins expensive?**
✔️ Because of shuffle

---

# ✅ Summary

* Joins combine multiple datasets
* Types:

  * inner
  * left
  * right
  * outer
* Broadcast join = optimization trick
* Joins are **core to real pipelines**

---

