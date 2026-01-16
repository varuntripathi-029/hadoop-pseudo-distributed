# Hadoop Pseudo-Distributed Setup (WSL)

## Overview
This project demonstrates a manually configured pseudo-distributed Hadoop cluster
running on WSL (Ubuntu), without Ambari or GUI tooling.  
The goal is to prove **hands-on understanding of HDFS, YARN, and MapReduce**, not just usage.

---

## Phase 1: Native Hadoop Setup (Completed)

### Components
- HDFS: NameNode, DataNode, SecondaryNameNode
- YARN: ResourceManager, NodeManager
- MapReduce: Hadoop MapReduce v2 (on YARN)

All services were started and debugged manually using CLI.

---

## Dataset Used (Large-Scale Validation)

- Dataset: **5 Million Sales Records**
- Format: CSV
- Size: **~596 MB**
- Rows: ~5,000,000
- Source: Public sales dataset (ExcelBI Analytics)

The dataset was:
1. Downloaded locally
2. Uploaded to HDFS
3. Processed using MapReduce on YARN

HDFS path used:/sales/input/sales_records_5m.csv


---

## Processing Performed

### 1. MapReduce WordCount
A built-in Hadoop MapReduce WordCount job was executed on the full 596 MB CSV file.

Command used:
```bash
hadoop jar hadoop-mapreduce-examples-3.3.6.jar \
wordcount /sales/input /sales/output

This validated:

Large-file ingestion into HDFS

Block splitting and parallel map tasks

Shuffle and reduce phase execution

Output persistence in HDFS

Output size:

part-r-00000 ≈ 214 MB

_SUCCESS marker present

Note:
Since WordCount tokenizes by whitespace, running it on CSV data produces
comma-separated token groups. This was intentional to validate distributed processing, not analytics correctness.

Key Learnings & Debugging

Environment variables must be explicitly propagated to Hadoop and YARN daemons

NodeManager is mandatory for MapReduce container execution

YARN containers do not inherit shell environments

Large-scale datasets expose real performance and configuration issues

Proof of Execution

HDFS namespace persistence verified

YARN application execution verified

MapReduce output stored in HDFS

Dataset size > 500 MB (non-toy workload)

Next Phases (Planned)

Phase 2: Dockerize Hadoop (reproducible single-node setup)

Phase 3: Add HBase on top of HDFS

Phase 4: Demonstrate CRUD operations in HBase

Why No GUI (Ambari)

This project intentionally avoids Ambari to ensure understanding of
service startup, configuration, and failure modes at the system level.


Save and exit.

---

# 2️⃣ What NOT to Commit (IMPORTANT)

You **do NOT commit**:
- CSV file
- ZIP file
- HDFS data
- `/sales-data` folder

This is **configuration + documentation**, not data hoarding.

If needed later, we’ll add a `.gitignore`.

---

# 3️⃣ Check Git Status (Sanity Check)

Run:

```bash
git status


Phase 2: https://github.com/varuntripathi-029/hadoop-docker-single-node
This repository provides a fully reproducible single-node pseudo-distributed Apache Hadoop setup using Docker.
It includes HDFS, YARN, and MapReduce, configured to run entirely inside a container with no dependency on host Hadoop installations.

The goal is infrastructure reproducibility, not a prebuilt demo image.


