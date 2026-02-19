
# 📘 1. Data Warehouse

## 🔹 What is a Data Warehouse?

A **Data Warehouse** is a centralized storage system designed for:

* Structured data (tables)
* Business reporting
* BI tools
* Historical analysis

It is optimized for **read-heavy analytical queries**.

Examples:

* Azure Synapse Analytics
* Snowflake
* Amazon Redshift

---

## 🔹 Traditional Data Warehouse Architecture

```
          +-------------------+
          |   Source Systems  |
          |-------------------|
          | ERP | CRM | Apps  |
          +---------+---------+
                    |
                    v
              +-----------+
              |   ETL     |
              | (Transform|
              |  Clean)   |
              +-----------+
                    |
                    v
         +----------------------+
         |   Data Warehouse     |
         |  (Structured Tables) |
         +----------------------+
                    |
                    v
           +------------------+
           | BI / Reporting   |
           | Power BI / SQL   |
           +------------------+
```

---

## 🔹 Characteristics

* Schema-on-write
* Structured data only
* Expensive storage
* Strong governance
* Best for BI dashboards

---

# 📘 2. Data Lake

## 🔹 What is a Data Lake?

A **Data Lake** stores:

* Structured data
* Semi-structured data (JSON, XML)
* Unstructured data (images, logs, videos)

It stores raw data in its original format.

Examples:

* Azure Data Lake Storage (ADLS Gen2)
* Amazon S3

---

## 🔹 Data Lake Architecture

```
          +----------------------+
          |   Source Systems     |
          |----------------------|
          | DB | Logs | IoT | API|
          +-----------+----------+
                      |
                      v
         +--------------------------+
         |        Data Lake         |
         |--------------------------|
         | Raw Zone                 |
         | Clean Zone               |
         | Curated Zone             |
         +--------------------------+
                      |
                      v
              +----------------+
              | Processing     |
              | Spark / Hadoop |
              +----------------+
```

---

## 🔹 Characteristics

* Schema-on-read
* Cheap storage
* Stores raw data
* Flexible
* Needs processing engine (Spark)

---

# 📘 3. Data Lakehouse (Modern Architecture)

## 🔹 What is a Data Lakehouse?

A **Data Lakehouse** combines:

✔ Data Warehouse reliability
✔ Data Lake flexibility

It supports:

* ACID transactions
* Schema enforcement
* Time travel
* Batch + Streaming

👉 This is where **Azure Databricks + Delta Lake** comes in.

---

## 🔹 Lakehouse Architecture (Azure Databricks Model)

```
                  +------------------+
                  |   Source Systems |
                  +------------------+
                           |
                           v
                +----------------------+
                |   Data Lake Storage  |
                |   (ADLS Gen2)        |
                +----------------------+
                           |
                           v
               +------------------------+
               |  Delta Lake (Tables)   |
               |------------------------|
               | Bronze  (Raw)          |
               | Silver  (Cleaned)      |
               | Gold    (Aggregated)   |
               +------------------------+
                           |
                           v
                +----------------------+
                | Azure Databricks     |
                | (Spark Engine)       |
                +----------------------+
                           |
                           v
                  +------------------+
                  | Power BI / ML    |
                  +------------------+
```

---

# 📘 4. Warehouse vs Lake vs Lakehouse (Comparison)

| Feature    | Data Warehouse  | Data Lake      | Data Lakehouse     |
| ---------- | --------------- | -------------- | ------------------ |
| Data Type  | Structured      | All types      | All types          |
| Schema     | Schema-on-write | Schema-on-read | Schema enforcement |
| Cost       | High            | Low            | Medium             |
| ACID       | Yes             | No             | Yes                |
| BI Support | Excellent       | Limited        | Excellent          |
| Example    | Synapse         | ADLS           | Databricks         |

---

# 📘 5. How Azure Databricks Fits In

Azure Databricks provides:

* Apache Spark engine
* Delta Lake
* Notebook development
* Streaming + Batch processing
* ML support

It turns **Azure Data Lake** into a **Lakehouse architecture**.

---


