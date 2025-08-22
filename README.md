# Databricks Workflow: Multi-Task Job for Customer Data

This project implements a **multi-task job in Databricks** that ingests raw customer data, validates regions, and separates valid from invalid records into different Delta tables.

## 🚀 Features
- **Automated ingestion** of customer data from CSV files
- **Data validation workflow** to check region consistency
- **Multi-task job** configured with dependencies in Databricks Workflows
- **Output tables**:
  - `customers_bronze`
  - `customers_invalid_region`
  - `customers_valid_region`

## ⚙️ Tech Stack
- **Databricks Workflows**
- **PySpark**
- **Delta Lake**
- **Databricks SQL**

## 📂 Repository Structure
- `notebooks/` → ETL scripts for each workflow step
- `configs/job_config.json` → Job definition with task dependencies
- `docs/` → Architecture and workflow diagram

## 🖇️ Job Workflow
1. **Ingest CSV** → Load raw data into `customers_bronze`
2. **Invalid Region Table** → Extract rows with incorrect region values
3. **Valid Region Table** → Extract rows with correct region values

## ✅ Example Job Configuration
```json
{
  "name": "CustomerDataETL",
  "tasks": [
    {
      "task_key": "Ingest_CSV",
      "notebook_path": "notebooks/01_ingest_customers_csv.py"
    },
    {
      "task_key": "Create_Invalid_Region_Table",
      "depends_on": ["Ingest_CSV"],
      "notebook_path": "notebooks/02_create_invalid_region_table.py"
    },
    {
      "task_key": "Create_Valid_Region_Table",
      "depends_on": ["Ingest_CSV"],
      "notebook_path": "notebooks/03_create_valid_region_table.py"
    }
  ]
}
