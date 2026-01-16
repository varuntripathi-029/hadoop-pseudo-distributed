The `README.md` file for the [hadoop-pseudo-distributed](https://github.com/varuntripathi-029/hadoop-pseudo-distributed) project by **varuntripathi-029** outlines a project focused on setting up a manually configured Hadoop cluster in a pseudo-distributed mode on WSL (Ubuntu).

Below is the structured content of the file:

---

# Hadoop Pseudo-Distributed Setup (WSL)

## Overview

This project demonstrates a manually configured pseudo-distributed Hadoop cluster running on WSL (Ubuntu), without Ambari or GUI tooling. The goal is to prove hands-on understanding of HDFS, YARN, and MapReduce.

## Phase 1: Native Hadoop Setup (Completed)

### Components

* **HDFS:** NameNode, DataNode, SecondaryNameNode
* **YARN:** ResourceManager, NodeManager
* **MapReduce:** Hadoop MapReduce v2 (on YARN)
All services were started and debugged manually using CLI.

## Dataset Used (Large-Scale Validation)

* **Dataset:** 5 Million Sales Records
* **Format:** CSV (~596 MB)
* **Source:** Public sales dataset (ExcelBI Analytics)
The dataset was processed by uploading it to HDFS and running MapReduce on YARN.

## Processing Performed

### 1. MapReduce WordCount

A built-in WordCount job was executed on the full 596 MB CSV file to validate:

* Large-file ingestion and block splitting.
* Parallel map tasks and shuffle/reduce phases.
* Output persistence (e.g., `part-r-00000` approx 214 MB).

## Key Learnings & Debugging

* Environment variables must be explicitly propagated to daemons.
* NodeManager is mandatory for container execution.
* Large-scale datasets reveal real performance and configuration issues.

## Planned Phases

* **Phase 2:** Dockerize Hadoop (reproducible single-node setup). [Repo Link](https://github.com/varuntripathi-029/hadoop-docker-single-node)
* **Phase 3:** Add HBase on top of HDFS. (I was not able to execute this phase due to local resource limitations)

## Why No GUI (Ambari)?

This project intentionally avoids Ambari to ensure understanding of service startup, configuration, and failure modes at the system level.

---
