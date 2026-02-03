# Data Engineering Homework 2: Workflow Orchestration with Kestra

## Preparation

**Backfill and execute using the `kestra-gcs-pipeline.yaml` file**

![Backfill Execution](<1. Backfill Jan to Jul .png>)

---

## Questions & Answers

### Question 1: Uncompressed File Size
**Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file `yellow_tripdata_2020-12.csv` of the extract task)?**

![Q1 Answer](<Q1 Answer.png>)

---

### Question 2: Variable Rendering
**What is the rendered value of the variable `file` when the inputs `taxi` is set to `green`, year is set to `2020`, and month is set to `04` during execution?**

```
green_tripdata_2020-04.csv
```

---

### Question 3: Yellow Taxi Row Count (2020)
**How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?**

```sql
SELECT DISTINCT count(*)
FROM `kestra-gcp-pipeline.zoomcamp.yellow_tripdata`
WHERE (TIMESTAMP_TRUNC(tpep_pickup_datetime, DAY) >= TIMESTAMP("2020-01-01")
AND TIMESTAMP_TRUNC(tpep_pickup_datetime, DAY) <= TIMESTAMP("2020-12-30"))
```

---

### Question 4: Green Taxi Row Count (2020)
**How many rows are there for the Green Taxi data for all CSV files in the year 2020?**

```sql
SELECT DISTINCT count(*)
FROM `kestra-gcp-pipeline.zoomcamp.green_tripdata`
WHERE TIMESTAMP_TRUNC(lpep_pickup_datetime, DAY) >= TIMESTAMP("2020-01-01")
AND TIMESTAMP_TRUNC(lpep_pickup_datetime, DAY) <= TIMESTAMP("2020-12-30")
```

---

### Question 5: Yellow Taxi March 2021
**How many rows are there for the Yellow Taxi data for the March 2021 CSV file?**

![Q5 Answer](<Q5 Anwer.png>)

---

### Question 6: Timezone Configuration
**How would you configure the timezone to New York in a Schedule trigger?**

Add a `timezone` property set to `America/New_York` in the Schedule trigger configuration.

---

## Pipeline Overview

This homework demonstrates:
- Kestra workflow orchestration
- Data ingestion from NYC TLC taxi data
- Google Cloud Storage (GCS) integration
- BigQuery data warehousing
- Backfill operations for historical data loading
- Schedule triggers with timezone configuration