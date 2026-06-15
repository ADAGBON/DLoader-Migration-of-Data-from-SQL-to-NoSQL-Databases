# DLoader — Migration of Data from SQL to NoSQL Databases

A research-based study and documented methodology for migrating relational data into NoSQL stores, based on the paper by Rajaram, Sharma, and Selvakumar (Springer, 2023).

---

## Overview

This project explores **DLoader**, a proposed ETL pipeline for moving data from **MySQL** into **Cassandra** and **MongoDB**, using **HDFS (Hadoop Distributed File System)** as a distributed staging layer. The goal is to understand how relational data models must be redesigned — not just moved — when transitioning to NoSQL at scale.

DLoader is a research prototype, not a commercial tool. This write-up covers both its specific methodology and the broader principles of SQL-to-NoSQL migration that apply in industry.

---

## Contents

| File | Description |
|---|---|
| [DLoader_SQL_to_NoSQL_Migration.md](DLoader_SQL_to_NoSQL_Migration.md) | Full checkpoint writeup covering all topics below |

### Topics Covered

1. **Introduction to Data Migration** — what migration is, and when SQL's guarantees become NoSQL's opportunity
2. **Overview of DLoader** — schema mapping, HDFS staging, multi-target ETL pipeline
3. **Migration Process** — six-step flow from extraction to cutover
4. **Data Transformation** — joins → embedding, normalization → denormalization, type conversion
5. **Performance Considerations** — HDFS-distributed processing, YCSB and JMeter benchmarks
6. **Consistency and Integrity** — staging checkpoints, count verification, hash-based validation
7. **Practical Application** — worked MySQL e-commerce → MongoDB migration plan
8. **Case Studies and Examples** — DLoader's own benchmark findings; industry migration patterns
9. **Conclusion** — trade-offs, when to use DLoader vs. native tooling

---

## Key Findings

- Cassandra stored the same migrated dataset in **~41% less space** than MongoDB and delivered lower response times on large workloads (per DLoader's YCSB benchmark).
- HDFS staging decouples extraction from loading, protecting the source schema and enabling incremental, validated migration.
- The most important design decision is **schema re-design for query patterns**, not a mechanical table-to-collection copy.

---

## SQL vs NoSQL at a Glance

| Dimension | SQL | NoSQL |
|---|---|---|
| Schema | Fixed | Flexible |
| Scaling | Vertical | Horizontal |
| Relationships | Joins | Embedding / references |
| Consistency | ACID | Tunable (BASE) |
| Best fit | Structured, transactional | High-volume, semi-structured |

---

## Reference

Rajaram, K., Sharma, P., & Selvakumar, S. (2023). *DLoader: Migration of Data from SQL to NoSQL Databases.* In *Proceedings of the International Conference on Cognitive and Intelligent Computing* (pp. 193–204). Springer, Singapore.
https://doi.org/10.1007/978-981-19-2358-6_19

---

*GoMyCode — NoSQL Cloud Datastores: Mongoose & MongoDB vs NodeJS | Checkpoint 41*
