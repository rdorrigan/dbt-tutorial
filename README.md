# dbt Fundamentals Certification & Analytics Engineering Showcase

[![dbt-core](https://img.shields.io/badge/dbt--core-1.7+-orange.svg)](https://www.getdbt.com/)
[![Snowflake/BigQuery](https://img.shields.io/badge/Warehouse-BigQuery%20%2F%20Snowflake-blue.svg)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains practical implementations, modular data models, testing suites, and documentation built during the completion of the **dbt Fundamentals** certification. It demonstrates enterprise analytics engineering patterns, modular model layering, testing assertions, and documentation generation.

---

## 🏗 Modular Data Architecture

The project follows dbt best practices, organizing SQL transformations into clear dimensional modeling layers:

```text
models/
├── staging/            # Source alignment, renaming, type casting, initial filtering
│   ├── jaffle_shop/
│      ├── src_jaffle_shop.yml
│      ├── stg_jaffle_shop.sql
│      └── stg_jaffle_shop__customers.sql
│      └── stg_jaffle_shop__orders.sql
│   ├── stripe/
│      ├── src_stripe.yml
│      ├── stg_stripe__payment.sql
└── marts/              # Production-ready Star Schema facts and dimensions
    ├── finance/
    │   └── fct_orders.sql
    └── marketing/
    │   ├── dim_customers.sql
│   ├── customers.sql
```

---

## 🔑 Core dbt Concepts Demonstrated

* **Sources & Staging:** Created modular staging models (`stg_`) using `source()` macros to decouple raw schema names from downstream transformations.
* **Ref Functions & DAG Management:** Leveraged `{{ ref() }}` to construct a dynamic Directed Acyclic Graph (DAG) for model lineage and dependency resolution.
* **Testing & Data Quality:**
* Implemented primary and foreign key constraints using out-of-the-box generic tests (`unique`, `not_null`, `relationships`, `accepted_values`).
* Custom Singular Tests for complex business logic validation (e.g., verifying `total_amount >= 0`).


* **Materialization Strategies:**
* `ephemeral` / `view` for staging models to save storage costs.
* `table` / `incremental` for heavy downstream marts to optimize query performance.


* **Documentation & Lineage:** Auto-generated interactive lineage documentation using `dbt docs generate`.

---

## ⚡ Quickstart

### 1. Prerequisites

* Python 3.10+
* dbt-core installed (`pip install dbt-core dbt-bigquery` or `dbt-snowflake`)

### 2. Environment Setup

```bash
# Clone the repository
git clone [https://github.com/rdorrigan/dbt-tutorial.git](https://github.com/rdorrigan/dbt-tutorial.git)
cd dbt-fundamentals-showcase

# Install dbt package dependencies (e.g., dbt-utils)
dbt deps

```

### 3. Run and Test Models

```bash
# Seed reference data
dbt seed

# Run all models in the DAG
dbt run

# Execute data quality tests
dbt test

# Generate and serve interactive docs
dbt docs generate
dbt docs serve

```
