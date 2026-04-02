## 🟢 3. Spark Core Concepts (Very Important)

This is the **foundation of Spark**. If you understand this well, everything else becomes easy.

---

## 🧠 1. Driver vs Executor

![Image](https://images.openai.com/static-rsc-4/ig_pg4mu9rTKKrLsd8RcvgjLF9czNqI0LlXekK9nIhREn8ZIh7_X1dp1_VItkfi-9Zebaut-5nL0oSYIKgNjO6Xz5RbhFQ7quK-Knsjr4INZuz3osV8eLErv8C3bfqYpVHNAeRAtexmLlqCfDG3QVMX5Z2w-lka5qioC1puELD8y-A0iUDymZpUiRoVc9RKI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/vG9Y2_1v2d9rKhwMHSSJFpLZsofoLM3JZxxD2qNlS7NfQLjH1rYjtGDVmk_qEQZNU-iW34wgxuDMzJH9m1mIDv33FhJINqO7tLtpvNq1xaE-ljcxT_MHc4RGnVco0Z0_A_8ZPZ3TAS-EwPYaJZJ6EoSGiSwB2bM874UsgIZfYkxjUMjmAyBp2HYhbZKOx4Wx?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/CveutHVSKk5R-HrcHNh8z3dJ_EMPDsLYJMpDbVuZslS2nA-0WYhKWBwM_Zs_ooghON62SCXuwMSVMBjYWfw03mPKmDUonL_7mTizFLR9KdmqC-W1nKT41qIdmCqUDprTTtPQvAr8VG2VPjG-r62L_-3x0_wSySIoxPBms3l4CsKBEuqVwgI3cAwXP8SEzh1s?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/cXDe5M9jgatw6kCA8TY5fGJ_sQiRit0s226LsmVARmz32wRTBaH2YPuIHpZ3y1ewNj-94rqG6pFWXl1VPG_Wtjn4Lm7CBAy9HJY6kUvED7S17GLfJfqegzb2C0xspeu1UlPXhN5chmSbH8mi0hJonsfD2QuAAGakI9QGIVj-WACVxPbgaOQm2WO-2yTMpztS?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/SgjqkBJTnRKWY6pxrHgOONcvqm09WElrblU8oJc6GSYEflBKSFFokOY65uDczIcwnYuP7_A7RGUGb2X1zbUfU4w47adtmJRgQsHmt_5akTna3AO7jkrM3my_gKq-cE7rwPO_ywyV_lIEMmzESjCd9-NqjBHALNw3f2iLrnDGS_AKbzZdlGiD5qZF3HvZD8z-?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Ch2bl7Q33YM1XzHAA4ApV9NfS5doqkSqPpV0WUJGo9vscY3Fwb4Xv_qv4ghVicMvL6K-P0SL3EK9Kna46a8TwmWsAXW7yheeVxKYN8yCqvEOR-p11HhTyx0-DONzpHH5rWIrAVFmGCJTcrGg2c_31PJ0DtnvFJlR-LkJkFwNJoEo_ZUiMXL18fp9WYcwLklh?purpose=fullsize)

### 🔹 Driver

* The **main program** (your notebook code runs here)
* Responsible for:

  * Planning tasks
  * Creating execution plan (DAG)
  * Sending work to executors

### 🔹 Executors

* Worker nodes (machines)
* Responsible for:

  * Executing tasks
  * Processing data
  * Returning results

👉 **Simple analogy:**

* Driver = Manager 🧠
* Executors = Workers 👷‍♂️

---

## 🔄 2. Transformations vs Actions

This is one of the **most important Spark concepts**.

---

### 🔹 Transformations (Lazy)

Operations that **define what to do**, but don’t execute immediately.

Examples:

```python
df.select("name")
df.filter(df.age > 25)
df.withColumn("new_col", df.age + 10)
```

👉 These are **lazy** (no execution yet)

---

### 🔹 Actions (Trigger Execution)

Operations that **actually run the computation**.

Examples:

```python
df.show()
df.count()
df.collect()
```

👉 When you call an action → Spark executes everything

---

### ⚡ Key Idea:

* Transformations build a plan
* Actions execute the plan

---

## ⏳ 3. Lazy Evaluation

![Image](https://images.openai.com/static-rsc-4/cFwzSaCLVbLRqd4jiSQBC9I4xOHWPQzuQzh4mitI_kBojon2rKz6wh-w0Z_Un98PpFNAptkbI4ZQ4wF0SFqbF4MGssWX8NsW1BRWVMxXa5xKkkpuxmV2_R4bWJAEqeYhbAoR3ZWrwmVT4UGkXrErVUZjMho5oxXv9Fq28nRymqxF2J7ypt6lPcBsP_U13LRd?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/wwQoioxJlv0dmUusZu2Fv0s7SngqaqW1XyrmQ2Ee23xC0LTz4gjlKcUbpEMAf03BS2ivzOZcBdd0DpCDFui4R0KynBqSCYHmDlwy721i2VXSl7aLeB-BbbpHxW2KpJ9ne9AIFU_maRLZDsUULoLMgTu4UnrAXNre8PZO-cvySCsV70L5tqDW_mevxUrdaWqU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tFO1w5a-z23EmM2uPeit6_yr1s8P1yqZpATG-OhzxikTuSubI7tl3WCLdyCSHQFYQ_Z6J2fijcGNLzLjR4QatiGXsOqHrSXPRuiWgHrs79w0SBLx3JGT2Y_mPszk3LlHk8dtIIc9ai9lPKwazVwcXC_Na1Cw5PNTQdjd3yL8kTZLFZxc4wMoGKOWzwBDVxQQ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/2q1p-DGIf6nrKLI8yAv-CmrpcK0ULac-bSE5qHgCbOINRCiO9U_NTswU4K4y2zcKwYsugRPP-Q_8_PZ1hGs2GiSbRA0YOwWdD3s4i4TfJPnxAbbq9P3B7Vnq8eU0V4Yl2OUjLYIqSdmTGGBXv5p5wqDu6pjkNs1uViRYhdYcgwc11yhjfeclrbPRTFgwHOSu?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/nmexI1N-7Xq4Y89wtrPY9EQr8rriw7EkrACYV-8frNMaCkmKATMIReHPVhdbAbAE2oO3TQ9U6YX5g6tvKsx_8QpFWBVpuyLgIUwYSeMOXtM1yH308ul41hU1-Bzr7QWpiTbMkziytAX-Tt-lzkOFUQarSdRtHilVN2UfKIXCPwtm29jF5hV6TSBDQIjotkl4?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/mxAEsuM7NF2-8cTfq7oTmmJGa4GCWXATeELlmsg56M6asrlrTjA_C4EEk5a-UN1d7MBckupddGLZPKBvQYHZdjvYWZvXChkuKhYV1Gc3QICkZcGudT7UDyp4hQioOmqlWk5QXj8YztdX460R1XJDk-eAkchvcvJjtVLEGHMNxmrvzRe3UFHLAGUAW7YTR20M?purpose=fullsize)

Spark does **not execute immediately**.

Instead:

1. Builds a plan (DAG)
2. Optimizes it
3. Executes only when needed

### Example:

```python
df = spark.range(100)

df_filtered = df.filter(df.id > 50)
df_selected = df_filtered.select("id")

df_selected.show()
```

👉 Execution happens **only at `.show()`**

---

## 🔗 4. DAG (Directed Acyclic Graph)

* DAG = Execution plan of Spark
* Shows **how data flows through transformations**

### 🔹 Why important?

* Spark optimizes execution using DAG
* Avoids unnecessary work

---

## ⚙️ 5. Partitions

* Data is split into **chunks (partitions)**
* Each partition is processed in parallel

### Example:

* 1GB data → split into 10 partitions → processed simultaneously

👉 More partitions = more parallelism (but too many = overhead)

---

## 🔁 6. Narrow vs Wide Transformations

---

### 🔹 Narrow Transformation

* Data stays in same partition
* No data shuffle

Examples:

```python
df.select()
df.filter()
```

✅ Fast

---

### 🔹 Wide Transformation

* Data moves across partitions (shuffle happens)

Examples:

```python
df.groupBy()
df.join()
```

❌ Expensive

---

## 🔥 7. What is Shuffle?

* Data is redistributed across cluster
* Happens during:

  * joins
  * groupBy
  * aggregations

👉 Shuffle = **slowest operation in Spark**

---

## 🧩 8. Spark Execution Flow (Big Picture)

1. You write code in notebook (Driver)
2. Spark builds DAG
3. Tasks are sent to Executors
4. Executors process partitions
5. Results returned

---

## 🎯 Mini Example (Connect Everything)

```python
df = spark.range(100)

df_filtered = df.filter(df.id > 50)   # Transformation
df_grouped = df_filtered.groupBy().count()  # Transformation

df_grouped.show()   # Action → triggers execution
```

---

## ✅ Summary

* **Driver** → controls execution
* **Executors** → do actual work
* **Transformations** → lazy
* **Actions** → trigger execution
* **Lazy evaluation** → optimized execution
* **Partitions** → parallel processing
* **Shuffle** → expensive operation

---

