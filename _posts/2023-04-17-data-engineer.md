---
layout: distill
title: Data Engineering
date:   2023-04-17
description: Principles and techinques for (big) data engineering
tags: big-data cloud-computing data-engineering
categories: review-notes
published: true
highlight: true

authors:
  - name: Tiziano Coccio
    affiliations:
      name: '-'

toc:
  - name: Introduction
    subsections:
      - name: Definition
      - name: Issues and challenges
      - name: Main aspects
      - name: Content overview
  - name: Big Data Engineering
    subsections:
      # - name: Definition
      # - name: Ecosystem
      # - name: Architecture
      - name: Ingestion
      - name: Processing
      - name: Storage
      - name: Analytics
      - name: Orchestration and Pipelining
      # - name: Visualization
      # - name: Security
  # - name: Big Data Technologies
  #   subsections:
  #     - name: Frameworks
  #     - name: Tools
  #     - name: Platforms
  #     - name: Applications
  #     - name: Databases
  #     - name: Programming Languages
  #     - name: Libraries
  - name: Software Engineering
    subsections:
      - name: Object-Oriented Principles
      - name: Architecture   
      - name: Other design paradigms   
      - name: Development Life Cycle (SDLC)
      - name: Requirements Engineering
      - name: Development Models
      - name: Design Patterns
      - name: Testing
      # - name: System Modeling
  - name: Soft Skills
    subsections:
      - name: Agile Methodologies
  - name: Practice Questions
  - name: Learning Resources
---
# Introduction
I put together this post to collect all the notes I gathered while I was studying for a job interview. It is a work-in-progress, which means that sometimes details may be missing, information may not be structured optimally, and the flow may not always be smooth.

## Definition
_Big data_ describes the large volume of structured and unstructured data that a business generates on a daily basis. Big data can be analyzed for insights that lead to better decisions and strategic business moves.

## Issues and challenges
- Data volume: data is generated at a high rate
- Data velocity: data is generated at a high rate
- Data variety: data is generated in different formats
- Data veracity: data is not always accurate
- Data value: data is not always useful

## Main aspects
- Data engineering: is concerned with the design, development, and maintenance of data systems. It is the main topic of this post. Although I will also cover some aspects of data science, software engineering, and development methodologies.
- Data science: is concerned with the extraction of knowledge from data.
- Data analytics: is concerned with the analysis of data to extract insights, in a sense it is a subset of data science
- Data visualization: is concerned with the presentation of data in a graphical format. This is a topic I will not discuss in this post.

## Content overview
### Data Engineering
Data flows from some source into a system, it is processed in _some_ way, and then it is stored in a database. The data is then analyzed and visualized. Finally, the data is used to make decisions. The main concern of data engineering is to design and implement the system that performs these tasks.

### Data Technologies
There are many tools and frameworks used in data engineering. In a processing pipeline, one can find tools for data ingestion, data processing, data storage and providers, data analysis, and for orchestrating the whole system. Additionally, there are services like Amazon Web Services (AWS) or Google Cloud Platform (GCP), that provide a platform for data engineering that offer an all-round ecosystem of tools and services.
The right tool will depend on the specific use case. Here's a first glimpse of some these tools and how they can be used:
  - Data ingestion: Apache Kafka, Apache Flume, Apache NiFi
  - Data processing: Hadoop, Apache Spark, Apache Flink, Apache Storm, Apache Beam
  - Data storage: Apache HBase, Apache Cassandra, Apache Druid
  - Storage providers: Amazon S3, Google Cloud Storage, Azure Blob Storage
  - Data analysis: Apache Hive, Apache Zeppelin
  - Data visualization: Apache Superset, Apache Zeppelin
  - Orchestration/Pipeline: Docker, Kubernetes, Apache Airflow, Apache NiFi, Luigi
Not specific to data engineering, but still important is the use of CI/CD tools like Jenkins, GitLab CI, or GitHub Actions.

### Software Engineering
Software engineering is the application of engineering principles to the development of software. It is concerned with the design, development, and maintenance of software systems. It is a topic that is not directly related to data engineering, but it is important to understand the software development process and the tools used in software engineering. In this post I will mostly focus on the software development life cycle, how one decides on _what_ needs to be built, which strategies can be used in the process, how one can reuse structural solutions to new problems, and discuss some common models of systems.

### Agile Methodologies
I will briefly mention the agile development process, advantages and disadvantages, and some alternatives.

<!-- Section 2: Big Data Engineering -->
# Big Data Engineering

<!--
## Definition
## Ecosystem
-->
## Architecture
Most data engineering systems are built on top of a distributed architecture. A distributed architecture is a system that is composed of multiple nodes, where each node is a computer that is connected to a network. Nodes are typically connected to each other, they can be physical computers or virtual machines. They can be located in different geographical locations, in the same data center, in the same physical rack, or even in the same virtual machine.

Typically, systems are structured in a layered architecture:
- Physical Storage
- Storage Engine
- Query Engine
- SQL Interface
- User Interface

**Physical Storage Layer**. This layer is responsible for storing the actual data on physical storage devices, such as hard drives, SSDs, or cloud storage. The data may be stored in a distributed manner across multiple nodes in the system, for scalability and fault tolerance.

**Storage Engine Layer**. This layer sits on top of the physical storage layer and provides an abstraction over it, allowing higher-level layers to interact with the data without worrying about the details of the physical storage. The storage engine layer may provide functionalities such as data partitioning, replication, compression, and indexing to optimize data access and performance.

**Query Engine Layer**. This layer is responsible for processing queries and data requests from higher-level layers, such as the SQL interface or user interface. The query engine may optimize queries by using techniques such as parallel processing, caching, and query planning to improve performance.

**SQL Interface Layer**. This layer provides a standard SQL interface for users to interact with the distributed system. Users can write SQL queries to access and manipulate the data stored in the system, without needing to know the details of the underlying storage and query engines.

**User Interface Layer**. This layer is the topmost layer in the system and provides a user-friendly interface for users to interact with the system. This may include graphical user interfaces (GUIs), command-line interfaces (CLIs), or APIs. Users can use this layer to perform various operations, such as querying data, performing analytics, and visualizing results.

## Theoretical Concepts

### OLTP systems
Online Transaction Processing (OLTP) systems are used to process high-volumes of transactions. Transactions are typically short-lived involving simple CRUD operations.

They are typically used to store and process data from online applications, such as e-commerce websites, social media platforms, and online banking systems, and whenever it's important to maintain data integrity and consistency. OLTP systems are designed to be highly available and highly performant, and they are optimized for read/write operations. OLTP systems are typically transactional databases, such as MySQL, PostgreSQL, and Oracle.

The key characteristics of OLTP systems are:

**High volume of transactions**. OLTP systems are designed to handle a large number of transactions in real-time. These transactions can come from various sources, such as online orders, credit card transactions, or inventory updates.

**Short response time**. Because OLTP systems are used in real-time environments, they need to respond quickly to requests. This means that queries and transactions should be processed quickly, typically within a few seconds.

**Concurrent access**. In an OLTP system, many users may be accessing the same data simultaneously. Therefore, the system should be designed to support concurrent access to avoid data conflicts and ensure data consistency.

**Data consistency**. OLTP systems require data to be consistent and accurate at all times. This means that the system should ensure that transactions are processed in a way that maintains the integrity of the data.

**ACID compliance**. OLTP systems often use the ACID (Atomicity, Consistency, Isolation, and Durability) model to ensure data integrity. This means that transactions should be Atomic (all or nothing), Consistent (data is in a valid state), Isolated (transactions should not interfere with each other), and Durable (once a transaction is committed, the data is saved permanently).

### OLAP systems
Online Analytical Processing (OLAP) systems are used to analyze large amounts of historical data. OLAP systems are typically used to perform complex queries and data analysis, such as business intelligence (BI) and data mining. OLAP systems are designed to be highly available and highly performant, and they are optimized for read-only operations. OLAP systems are typically data warehouses, such as Amazon Redshift, Google BigQuery, and Microsoft Azure SQL Data Warehouse.

They are often used in situations where it is important to analyze large amounts of data to gain insights, such as in business intelligence, financial analysis, and marketing.

Some key characteristics of an OLAP system include:

**Large volume of data**. OLAP systems are designed to handle large amounts of data, typically in the range of millions or billions of rows.

**Complex queries**. In an OLAP system, users often run complex queries to analyze data. These queries may involve multiple dimensions, calculations, and filters.

**Aggregated data**. OLAP systems often store data in an aggregated format, such as a **cube** or a **star** schema. This allows users to quickly access summarized data without needing to scan through all the individual records.

**Performance optimization**. Because OLAP systems are designed for analyzing large amounts of data, they often employ performance optimization techniques such as indexing, caching, and parallel processing.

**Ad hoc analysis**. OLAP systems allow users to perform ad hoc analysis, which means that users can explore data and generate insights in real-time without needing to rely on pre-built reports or queries.

### OLTP vs OLAP
OL**T**P systems have a focus on transactional operations, while OL**A**P systems have a focus on analytical operations. OLTP systems are designed to handle many transactions in real-time, while OLAP systems are designed to handle a large amount of historical data.

OLAP systems are optimized for read-heavy scenarios. OLTP systems are designed to efficiently process and store transactions, as well as query transactional data.

### Examples of OLTP and OLAP systems
In many cases, OLTP and OLAP systems are used together to provide a complete solution. For example, an e-commerce website may use an OLTP system to store and process data from online orders, and an OLAP system to analyze historical data from online orders to gain insights into customer behavior.

Often, software applications combine the two systems into a single system, while others may use separate systems. Here are some examples:

**Apache Hadoop**. An open-source software framework used for storing and processing large amounts of data in a distributed manner. It supports both **OLAP** and **OLTP** workloads through various tools and libraries, such as Hive and HBase.

**Apache Cassandra**. A distributed database management system designed for handling large amounts of data across multiple nodes. It is often used in **OLTP** systems that require high scalability and availability.

**Apache Spark**. An open-source data processing engine used for processing large amounts of data in-memory. It supports both **OLAP** and **OLTP** workloads through various tools and libraries, such as Spark SQL and Spark Streaming.

**Apache Flink**. An open-source data processing engine used for processing real-time data streams. It supports both **OLAP** and **OLTP** workloads through various tools and libraries, such as Flink SQL and Flink Streaming.

**Apache Kafka**. A distributed streaming platform used for processing and storing large amounts of data in real-time. It is often used in **OLTP** systems that require high scalability and low latency.

**Elasticsearch**: A distributed search and analytics engine used for processing and analyzing large amounts of data in real-time. It supports both **OLAP** and **OLTP** workloads and is often used in log analytics and business intelligence applications.

Now a more detailed look at how these components can be used to achieve OLAP and/or OLTP functionality.

#### Hadoop + Hive = OLAP
Hive is a **data warehousing** tool that provides SQL-like query capabilities on top of Hadoop. It uses a query language called **HiveQL**, which is similar to SQL, to allow users to query large datasets stored in HDFS. Hive is often used for **OLAP** workloads, such as business intelligence and data analysis. It provides an abstraction layer on top of Hadoop's MapReduce engine, allowing users to write queries without having to write complex MapReduce jobs.

#### Hadoop + HBase = OLTP
HBase is a column-family **NoSQL** database that is built on top of Hadoop and HDFS. It provides real-time read/write access to large datasets and is often used for **OLTP** workloads, such as storing sensor data, log data, or user profiles. HBase is designed to handle large volumes of structured or semi-structured data with high write throughput and low latency. It uses Hadoop's distributed file system (HDFS) to store data, and Hadoop's MapReduce engine to process data.


### ACID properties
ACID properties are a set of four properties that are essential for ensuring reliable and consistent transaction processing in a database system. The acronym "ACID" stands for:

**Atomicity**. This property ensures that a transaction is treated as a single, indivisible unit of work. Either all operations in the transaction are completed successfully, or none of them are. In other words, if any part of a transaction fails, the entire transaction is rolled back, and the database returns to its previous state.

**Consistency**. This property ensures that the database remains in a consistent state after a transaction completes. This means that the database must satisfy all integrity constraints, such as primary key and foreign key constraints, and that the data must adhere to all business rules and domain-specific constraints.

**Isolation**. This property ensures that multiple transactions can occur concurrently without interfering with each other. Each transaction must be isolated from other transactions and must operate as if it were the only transaction running in the system. This is achieved by using concurrency control mechanisms, such as locking and multi-version concurrency control.

**Durability**. This property ensures that once a transaction has completed successfully, its effects are permanent and will survive any subsequent failures, such as power outages, system crashes, or hardware failures. This is achieved by ensuring that all changes made by a transaction are recorded in a permanent storage medium, such as a hard disk, before the transaction is considered complete.

### CAP Theorem
The CAP theorem states that it is impossible for a distributed data system to simultaneously provide more than two out of the following three guarantees:

**Consistency**. This property ensures that all nodes in a distributed system have the same data at the same time. This means that if a client reads data from one node, and then reads the same data from another node, the data will be identical.

**Availability**. This property ensures that every request receives a response, without any errors, regardless of the state of the system. This means that if a client sends a request to a node, the node will either respond with the requested data or an error message.

**Partition tolerance**. This property ensures that the system continues to operate despite arbitrary message loss or failure of part of the system. This means that if a node fails or loses its connection to the network, the system will continue to operate as normal.

In practice:
- If a system provides consistency and availability, it will not be partition tolerant. 
- If a system provides consistency and partition tolerance, it will not be available. 
- If a system provides availability and partition tolerance, it will not be consistent.

In other words, if a network partition occurs, the system will have to trade off between consistency and availability.

### BASE properties
BASE properties are a set of three properties that are essential for ensuring reliable and consistent data processing in a distributed system. The acronym "BASE" stands for:

**Basically available**. This property ensures that the system will continue to operate even if some nodes fail or lose their connection to the network. This is achieved by replicating data across multiple nodes and using a consensus algorithm to ensure that all nodes have the same data.

**Soft state**. This property ensures that the system will continue to operate even if some nodes lose their state. This is achieved by using a consensus algorithm to ensure that all nodes have the same state.

**Eventual consistency**. This property ensures that the system will eventually become consistent, even if some nodes are inconsistent. This is achieved by using a consensus algorithm to ensure that all nodes eventually become consistent.

### Query optimization
Query optimization is the process of transforming a query into an efficient execution plan. The execution plan is a set of instructions that describe how the query will be executed. It is often represented as a tree, where each node represents a single operation, such as a join, sort, or aggregation. The execution plan is optimized by choosing the most efficient order of operations, and by pushing operations down to the lowest level possible.

Indexing is a strategy to map values to physical locations in a database. They are used to speed up data retrieval by reducing the number of disk reads required to find a particular record. Indexes are often used in OLTP systems, where data is frequently read and updated, but not written. In OLAP systems, data is often written and rarely read, so indexes are not used.

Indexing can be implemented with a **B-tree** or a **hash table**. A B-tree is a self-balancing tree data structure that is used to store data sorted by a key. It is often used in databases and file systems. A hash table is a data structure that maps keys to values. It is often used in databases and caches.

Queries can be optimized using different strategies: cost-based optimization, rule-based optimization, and heuristic-based optimization. Cost-based optimization uses the cost of each operation to determine the best execution plan. Rule-based optimization uses a set of rules to determine the best execution plan. Heuristic-based optimization uses a heuristic to determine the best execution plan. Caching can also be used to optimize query results.


### Data Warehouse
A data warehouse is a large, centralized repository of integrated data from one or more sources that is used to support business intelligence (BI) activities such as reporting, analysis, and data mining. It is designed to support strategic decision-making by providing a historical view of data that is optimized for querying and analysis.

Unlike transactional databases, which are optimized for efficient data processing and transactional processing, data warehouses are optimized for efficient querying and analysis. Data warehouses typically contain large volumes of historical data, which are organized by subject area and stored in a denormalized, or flattened, format to enable faster and easier analysis.

Data warehouses often employ Extract, Transform, and Load (ETL) processes to extract data from multiple sources, transform it into a common format, and load it into the data warehouse. This ensures that data is consistent, accurate, and complete.

Data warehouses typically use Online Analytical Processing (OLAP) techniques to enable users to analyze data in a multidimensional manner. Users can explore data using various dimensions, such as time, geography, or product, and perform calculations and aggregations on the data to gain insights into business performance.

### Data Lake
A data lake is a large and centralized repository of raw, unstructured, and structured data, which is designed to support a wide range of analytics and data exploration activities. It is a relatively new concept in the field of big data and is used to store data that is not ready for immediate analysis.

Unlike a data warehouse, which stores data in a structured and organized manner, a data lake stores data in its native format, regardless of the source or type. This means that data can be stored as text files, images, videos, or any other format. A data lake is designed to support the ingestion of data from multiple sources and in various formats, which enables organizations to store and process large volumes of data quickly and easily.

Data lakes are often used by data scientists and analysts to perform exploratory data analysis (EDA) and data mining. They can be used to identify patterns, trends, and relationships in data, as well as to perform predictive modeling and machine learning.

To manage a data lake, organizations typically use tools and technologies that enable data ingestion, data storage, data processing, and data governance. Examples of data lake technologies include Hadoop Distributed File System (HDFS), Amazon S3, and Microsoft Azure Data Lake Storage.

### Data Mesh
A data mesh is an approach to data architecture that emphasizes decentralization and domain-driven design. The concept was introduced by Zhamak Dehghani, a software architect at ThoughtWorks, in 2020.

In a data mesh architecture, data is treated as a product, and each domain or business unit is responsible for the quality, governance, and delivery of its own data products. This approach is in contrast to traditional data architectures, which are often centralized and governed by a central data team.

The core principles of a data mesh include:

**Domain-driven design**. Data products are organized around business domains, rather than technical infrastructure.

**Self-serve data infrastructure**. Data products are made available to consumers through standardized, self-serve interfaces.

**Federated data governance**. Data governance is distributed across domains, with each domain responsible for its own data quality and governance.

**Data platform as a product**. The data platform is treated as a product, with its own roadmap, backlog, and product owners.

In a data mesh architecture, data is decentralized and distributed across multiple domains or business units. Data products are owned and managed by the domain teams, who are responsible for their quality, governance, and delivery. This approach enables organizations to scale their data capabilities while maintaining agility and flexibility.


### Database Design Patterns
These are set of best practices used to promote performance optimization, data integrity, security, scalability, and maintainability of a database.

#### Single table
All data is stored in a single table, this can simplify queries, improve performance and reduce the need for complex joins.

#### Composite partition
Data is partitioned by one or more criteria. For example, partitions can be on date ranges, IDs, or geographical locations. This can improve query performance by reducing the amount of data that needs to be scanned.

#### Hierarchical data
Data is stored in a tree-like structure. Each record has a parent and child relationships with other records. This is commonly used to store organizational charts, taxonomies, product categories, and other hierarchical data.

#### Materialized view
A precomputed view of data is updated automatically when the underlying data changes, or at regular intervals.
It is often used in **OLAP** systems, where data is frequently read, but not written. In **OLTP** systems, data is often written and rarely read, so materialized views are not used.

#### Denormalization
Data is duplicated across multiple tables to improve query performance. This can be used when retrieval performance is more important than data consistency.

#### Sharding
Data is divided across multiple servers or databases. This can improve performance and scalability by dividing the work across multiple resources.

#### Replication
Data is copied across servers to improve availability and fault tolerance. 

## Ingestion
### Apache Kafka
Kafka is a distributed streaming platform. It is used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, and runs in production in thousands of companies.

### Apache Flume
Flume is a distributed, reliable, and available service for efficiently collecting, aggregating, and moving large amounts of log data. It has a simple and flexible architecture based on streaming data flows. It is robust and fault tolerant with tunable reliability mechanisms and many failover and recovery mechanisms. It uses a simple extensible data model that allows for online analytic application.


## Processing
### Hadoop
Hadoop is built on the Hadoop File System (**HDFS**), a distributed file system that can store very large files. It is designed to scale up from single machines to thousands of nodes. However, the end user is presented with a single file system interface. Typically, it is run on **commodity** hardware, making it easy and cheap to replace. This paradigm allows it to be highly fault-tolerant and reliable.

It is designed following a master-slave architecture. The **master** (aka _NameNode_) node is responsible for managing the cluster, and the **slaves** (aka _DataNodes_) are responsible for storing and processing data. The NameNode holds the cluster's metadata, including the file system namespace and the DataNode locations. It is also responsible for scheduling jobs, and setting the replication factor for each file. DataNodes store the actual data blocks and perform computation, such as map and reduce tasks. They also report to the NameNode to report they are functioning, this is implemented by sending _heartbeats_ to the NameNode.

Hadoop uses **YARN** (Yet Another Resource Negotiator) to manage resources across the cluster. YARN is a cluster resource management system that is responsible for scheduling and managing resources across the cluster. It is designed to be hardware-agnostic, and platform independent, so it can also be used to manage resources for other applications, such as Spark and Flink.

Hadoop stores files as read-only _immutable_ files. This ensures data integrity. It also means that Hadoop is optimal for batch data processing, but not for real-time data processing.

The core principle of Hadoop is to **move the computation to where the data is located**. This idea is based on the fact that moving large amounts of data across the network is expensive, while processing data locally is cheap. 

Hadoop, however, has a number of limitations:
- The system becomes inefficient when storing **small files**, as each file is stored as a separate block.
- Processing can be **slow** when the data is not evenly distributed across the cluster.
- It is **not** designed for **real-time** data processing, and is not suitable for applications that require low **latency**.
- Its design does not offer the ability to use an **iterative** algorithm. There are multiple reasons for this. MapReduce makes it difficult to implement iterative algorithms. Every iteration requires the instantiation of a new MapReduce job, which is expensive. Every iteration would also require the data to be written to disk, which is also expensive. Hadoop also does not support in-memory processing, which is required for iterative algorithms.
- The **MapReduce** paradigm per se can be challenging to use. It requires the developer to write the code in a specific way, and to understand the underlying architecture. This can be difficult for developers who are not familiar with the system.

#### MapReduce
MapReduce is a programming paradigm that was introduced by Google in 2004 to support distributed processing of large data sets on clusters of commodity hardware. It is a **highly scalable** and **fault-tolerant** approach to data processing that is widely used in big data processing frameworks like Apache Hadoop, Apache Spark, and others.

The MapReduce paradigm involves two main phases: the map phase and the reduce phase. The **map** phase takes a set of input data and maps it into a set of key-value pairs, where the keys are used to **group** the data by a common attribute and the values are the corresponding data elements. The map function is applied to each input element independently, producing a set of **intermediate** key-value pairs.

The intermediate key-value pairs are then **shuffled and sorted** by their keys, and the **reduce** phase begins. In the reduce phase, the intermediate key-value pairs are grouped by their keys, and the reduce function is **applied to each group** to produce a final output value. The reduce function aggregates or summarizes the values associated with each key, producing a smaller set of output key-value pairs.

The MapReduce paradigm is highly **scalable** because it can be applied to large data sets that can be partitioned across multiple nodes in a cluster. Each node in the cluster processes a subset of the input data, producing a set of **intermediate** key-value pairs that are then combined by the cluster into a final output. The MapReduce paradigm is also **fault-tolerant**, as intermediate data is stored on disk, and can be recomputed if a node fails during processing.

Here's a code example of the MapReduce paradigm in Python:

```python
# Define the map function
def map_function(num):
    intermediate_result = (1, num ** 2)
    print(f"Intermediate result: {intermediate_result}")
    return intermediate_result

# Define the reduce function
def reduce_function(key, values):
    result = (key, sum(values))
    print(f"Reduce result: {result}")
    return result

# Define the input data
data = [1, 2, 3, 4, 5]

# Apply the map function to the input data
intermediate_data = map(map_function, data)

# Group the intermediate data by key and apply the reduce function
output_data = {}
for key, value in intermediate_data:
    if key in output_data:
        output_data[key].append(value)
    else:
        output_data[key] = [value]
    print(f"Intermediate output: {output_data}")

print(f"Final output: {output_data}")

result = [reduce_function(key, values) for key, values in output_data.items()]

# Print the final result
print(result)

```

### Apache Spark
Spark was designed and introduced by Matei Alexandru Zaharia between 2013 and 2014 in his PhD [work](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2014/EECS-2014-12.pdf) "An Architecture for Fast and General Data Processing on Large Clusters". To day, it is perhaps the best introduction to Spark.

#### RDDs
The core idea in Spark is the RDD: Resilient Distributed Dataset. Let's start by its name:
- Resilient: It is fault-tolerant, which means that it can **recover** from failures.
- Distributed: It is distributed, which means that it can be operated on in **parallel** across multiple nodes in a cluster.
- Dataset: It holds a collection of **data**.

It is a fault-tolerant collection of data that can be processed in parallel across a cluster. It is also **immutable**, so once created, it cannot be modified. Any processing performed on an RDD yields a new RDD or a value, such as a string or a number. It is also **lazy**, which means that it does not compute its results immediately. Instead, it waits until an action is performed on it, such as a count or a save. This allows Spark to perform optimizations, such as caching and pipelining.

RDDs can be created in three ways:
1. By parallelizing a collection of objects in the driver program
2. By referencing a dataset in an external storage system, such as a shared filesystem, HDFS, HBase, or any data source offering a Hadoop input format.
3. By transforming an existing RDD.

Another key aspect of RDDs is their **lineage**. The lineage of an RDD is a directed acyclic graph (**DAG**) describing the sequence of transformations that created it, in other words its history. This is used to recover from node **failures**, by re-executing the transformations that created the lost RDDs. The lineage is also used to **optimize** the computation, by performing common subexpression elimination and caching.

#### Transformations, Actions, and DAGs

[Transformations](https://spark.apache.org/docs/latest/rdd-programming-guide.html#transformations) are operations that create a new RDD from an existing one. They are **lazy**, which means that they do not compute their results immediately. Some examples of transformations are `map`, `filter`, and `reduceByKey`.

[Actions](https://spark.apache.org/docs/latest/rdd-programming-guide.html#actions) are operations that trigger a computation on an RDD and return a value to the driver program or write it to an external storage system. They are **eager**, which means that they compute their results immediately. Some examples of actions are count, collect, and save.

The DAG (Directed Acyclic Graph) is built at the time of creating a Spark RDD, and is a fundamental concept used for representing the logical execution plan of a Spark job. A DAG is essentially a collection of stages, where each stage represents a set of transformations that can be executed in parallel.

The DAG is used to **optimize** the execution of a job by determining the optimal order of executing the different stages. Spark uses a lazy evaluation model, which means that transformations on RDDs are not executed immediately when they are defined, but only when an action is called. The DAG is used to keep track of the **dependencies** between RDDs and their transformations, so that Spark can optimize the execution by combining transformations together and minimizing data **shuffling** across the cluster.

The DAG in Spark is directed and acyclic, meaning that it has a specific **order** in which transformations must be executed and it does not contain any **cycles** that would cause infinite loops. Spark also provides a visualization tool called the DAG visualization, which can be used to view the DAG for a given Spark job and to identify performance bottlenecks.

When an RDD is created, Spark stores its **lineage** information in the DAG. If a node fails during processing, Spark can use this lineage information to **reconstruct** the lost data by re-executing the transformations that were used to create the lost RDD. This ensures that the processing can continue without interruption, and the **fault-tolerance** mechanism allows Spark to handle node failures transparently.

#### Shuffle operations
This text is mostly taken from [here](https://spark.apache.org/docs/latest/rdd-programming-guide.html#shuffle-operations).

Certain operations within Spark trigger an event known as the shuffle. The shuffle is Spark's mechanism for re-distributing data so that it’s grouped differently across partitions. This typically involves copying data across executors and machines, making the shuffle a complex and costly operation.

To understand what happens during the shuffle, we can consider the example of the `reduceByKey` operation. The `reduceByKey` operation generates a new RDD where all values for a single key are combined into a tuple - the key and the result of executing a reduce function against all values associated with that key. The challenge is that not all values for a single key necessarily reside on the same partition, or even the same machine, but they must be **co-located** to compute the result.

In Spark, data is generally not distributed across partitions to be in the necessary place for a specific operation. During computations, a single task will operate on a single partition - thus, to organize all the data for a single `reduceByKey` reduce task to execute, Spark needs to perform an **all-to-all** operation. It must read from all partitions to find all the values for all keys, and then bring together values across partitions to compute the final result for each key - this is called the **shuffle**.

#### RDDs Persistance
RDD persistence is a technique used to cache or store RDDs in memory or on disk, so that they can be reused efficiently across multiple operations or iterations. 

When an RDD is marked for persistence, Spark stores the RDD's partitions in memory or on disk, depending on the storage level specified. The storage level can be set to MEMORY_ONLY, MEMORY_ONLY_SER, MEMORY_AND_DISK, MEMORY_AND_DISK_SER, DISK_ONLY, etc. 

If an RDD is not persisted, it is recalculated every time it is used, which can be expensive, especially for iterative algorithms that use the same RDD repeatedly. By persisting an RDD, you can avoid this costly recalculation and improve the performance of your Spark application.

You can persist an RDD using the `persist()` method, which takes the storage level as an argument. Once an RDD is persisted, it stays in memory or on disk until it is explicitly unpersisted or until the Spark context is stopped.

It is important to note that persisting an RDD has trade-offs, since it consumes memory or disk space, and can slow down other operations that need to use the same resources. Therefore, it is important to choose the appropriate storage level based on the size of your data, available memory, and the frequency of RDD reuse in your application.

#### Broadcast Variables
Broadcast variables are a mechanism to efficiently share read-only data across all nodes in a cluster. Broadcast variables are used to store a value or a set of values that are needed by the tasks running on each worker node, but that do not change throughout the lifetime of the Spark application.

By broadcasting the variable, Spark serializes the data once on the driver node, and then sends it over the network to all the worker nodes where it is cached in memory. This avoids the overhead of sending the data multiple times, which can be significant for large datasets, and can also reduce the memory footprint of the application.

Broadcast variables are typically used to store lookup tables, dictionaries, or other types of data that are used frequently in Spark operations. For example, suppose you have a large lookup table that is used in multiple Spark tasks. Instead of sending the lookup table to each worker node every time it is used, you can broadcast the lookup table once and cache it in memory on all worker nodes. This can significantly reduce the network traffic and improve the performance of the application.


#### Spark Architecture and Components
Spark uses a Master-Worker architecture. Its key components are:
**Driver Program**. This is the main program that controls the overall execution of a Spark application. The driver program is responsible for creating SparkContext and coordinating the distribution of tasks across the cluster.

**SparkContext**. This is the entry point to any Spark functionality and represents the connection to a Spark cluster. The SparkContext is responsible for coordinating the execution of tasks across the cluster, managing the cluster resources, and communicating with the various components of the Spark architecture.

**Cluster Manager**. Spark can run on various cluster managers like Apache Mesos, Hadoop YARN, and Standalone. The cluster manager is responsible for allocating resources and scheduling tasks on the worker nodes in the cluster.

**Executors**. These are the worker nodes in the Spark cluster that are responsible for running tasks and processing data. Executors are launched on the worker nodes by the cluster manager, and each executor can run multiple tasks in parallel.

### DataFrames and Datasets

#### DataFrame
- Distributed collection of data organized into named columns (like a table in RDBMS)
- Can be created from various sources
	- Other RDDs
	- Hive
	- Avro
	- Parquet
	- ORC
	- JSON
	- JDBC
- High-level API for manipulation: filtering, aggregation, transformation, and SQL-like manipulation
- Schema inference: automatically infers the schema of the data
	- Useful for semi-structured data like JSON
- Lazy evaluation: transformations are evaluated only when an action is called
- Immutability: transformations on DataFrames generate new DataFrames
- Optimized with the Catalyst optimizer

#### Dataset
- Extension of DataFrames providing the benefits of RDDs (strong typing, functional programming capabilities) and those of DataFrames (optimizations, high-level APIs)
- Type safe: errors are caught at compile-time
- Encoders convert JVM objects <-> Spark's binary format: better performance and lower memory usage compared to RDDs
- Lazy evaluations
- Functional programming constructs
- Optimized with Catalyst and Tungsten


### Spark Structured Streaming
Spark Structured Streaming is an extension of Spark SQL that provides a high-level API for stream processing with the same expressiveness as batch processing. It allows developers to write SQL-like queries on streaming data and provides a unified programming model for batch and streaming processing.

The architecture of Spark Structured Streaming is based on the concept of Continuous Processing, which means that data is processed as soon as it arrives in a streaming source, rather than being processed in small batches like in Spark Streaming. Spark Structured Streaming provides a declarative API for defining streaming queries as SQL-like expressions, which are executed as continuous queries over the streaming data.

Spark Structured Streaming supports various streaming sources, including Kafka, Flume, HDFS, and TCP sockets, among others. It also supports various output sinks, including Kafka, HDFS, and databases, among others.

Spark Structured Streaming uses the same execution engine as Spark SQL, which means that it can leverage the same optimizations and performance optimizations as batch processing. It also provides fault-tolerance and data recovery mechanisms similar to Spark Streaming.

Spark Structured Streaming has a concept called Watermarking, which allows developers to specify how long they are willing to wait for late data. This helps to handle out-of-order data or delayed data arrival, and ensures that the data is processed correctly.

### Spark SQL and Catalyst optimizer
Spark SQL is a module in Apache Spark that provides a programming interface for working with structured and semi-structured data. It allows users to run SQL queries against their data and provides a DataFrame API for working with structured data in a more programmatic way.

Spark SQL also includes the Catalyst optimizer, which is a rule-based optimizer that generates efficient execution plans for Spark SQL queries. It does this by leveraging a tree-based representation of the query plan, which is optimized by applying a set of rules to transform and optimize the plan.

The Catalyst optimizer consists of three main components:

Analysis: The analysis phase parses and validates the SQL query and then creates a logical plan that represents the user's query.

Logical Optimization: The logical optimization phase applies a set of rules to the logical plan to simplify and optimize it. This includes things like predicate pushdown, common subexpression elimination, and constant folding.

Physical Optimization: The physical optimization phase maps the logical plan to a physical execution plan that can be executed on a cluster. This includes things like partition pruning, join reordering, and broadcast join optimization.

The Catalyst optimizer can improve the performance of Spark SQL queries by generating more efficient execution plans. It also provides a consistent and extensible optimization framework that allows for the addition of custom optimization rules and integration with external optimization tools.

### Spark MLlib
Spark MLlib is a machine learning library built on top of Apache Spark that provides a scalable and distributed framework for developing machine learning models. It provides a set of high-level APIs for common machine learning tasks like classification, regression, clustering, and collaborative filtering, among others.

Spark MLlib provides a set of algorithms and tools for data preprocessing, feature engineering, model selection, and evaluation. It also supports distributed training and model persistence, which allows developers to train and deploy machine learning models at scale.

Some of the key features of Spark MLlib include:

Distributed Computing: Spark MLlib is designed to work with distributed data, which means it can handle large datasets and can be scaled out to handle large-scale machine learning problems.

High-Level APIs: Spark MLlib provides high-level APIs for common machine learning tasks like classification, regression, and clustering, which makes it easy for developers to build and train models without having to write low-level code.

Integration with Spark: Spark MLlib integrates with other Spark components like Spark SQL and Spark Streaming, which makes it easy to integrate machine learning into larger Spark-based data processing pipelines.

Extensible Framework: Spark MLlib is designed to be an extensible framework, which means developers can add custom algorithms and tools to the library.

Some of the algorithms and tools provided by Spark MLlib include:

Linear Regression
Logistic Regression
Decision Trees
Random Forests
Gradient Boosted Trees
K-means Clustering
Principal Component Analysis (PCA)
Collaborative Filtering

### Spark GraphX
Spark GraphX is a graph processing framework built on top of Apache Spark that provides an API for graph computation and analysis. It enables the processing of large-scale graph data sets in a distributed manner by leveraging the distributed computing capabilities of Apache Spark.

With Spark GraphX, users can create and manipulate graphs and perform a wide range of graph algorithms, including graph pattern matching, graph traversal, page rank, and community detection, among others. GraphX provides a distributed implementation of the property graph model, which is a directed, labeled graph model that supports parallel operations on large graphs.

Some of the key features of Spark GraphX include:

Graph Processing: GraphX provides an API for graph processing that supports a wide range of graph algorithms and operations.

Distributed Graph Computation: GraphX leverages the distributed computing capabilities of Apache Spark to enable the processing of large-scale graph data sets in a distributed manner.

Integration with Spark Ecosystem: GraphX is designed to integrate seamlessly with other Spark components, including Spark SQL, Spark Streaming, and MLlib, which makes it easy to incorporate graph processing into larger Spark-based data processing pipelines.

High-level API: GraphX provides a high-level API that abstracts away many of the low-level details of distributed graph processing, which makes it easier for developers to build and maintain graph-based applications.

Some of the algorithms and tools provided by Spark GraphX include:

PageRank
Connected Components
Triangle Counting
Shortest Paths
Label Propagation
Subgraph Isomorphism
Community Detection

<!-- ### Performance Tuning & Optimization -->


### Apache Flink
Apache Flink is an open-source stream processing framework that provides a unified programming model for batch and stream processing. It is designed to be a general-purpose framework for processing data streams and can be used for a wide range of use cases, including real-time analytics, machine learning, and ETL.

## Storage
[TODO: Add content]
## Analytics
[TODO: Add content]
## Orchestration and Pipelining
[TODO: Add content]

### Docker
Docker allows consistency and reproducibility in the development, testing, and deployment of applications. It is OS-independent and offers a lightweight virtualization solution that allows developers to package applications and their dependencies into containers that can be deployed and run on any machine. Docker containers can be added or removed from a cluster without disrupting the rest of the cluster, which makes it easy to scale up or down as needed.

### Kubernetes
Kubernetes is an open-source container orchestration system that automates the deployment, scaling, and management of containerized applications. It is designed to be portable and extensible, which means it can be deployed on any cloud provider or on-premises.

In practice, it offers automatic scaling, load balancing, fault-tolerance, and resource management. It also provides a declarative API that allows developers to describe the desired state of their applications, which makes it easy to automate the deployment and management of containerized applications.

Kubernetes architecture is based on a master-slave architecture, which consists of a master node and one or more worker nodes. The master node is responsible for managing the cluster, while the worker nodes are responsible for running the actual containers. The other components of Kubernetes include:

**Pods**: Pods are the smallest unit of deployment in Kubernetes. They are the basic building blocks of Kubernetes and are responsible for running the actual containers.

**Services**: Services are a higher-level abstraction that allow developers to expose their applications to the outside world. They are responsible for load balancing and routing traffic to the containers running on the worker nodes.

**Controllers**: Controllers are responsible for managing the state of the cluster. They are responsible for creating, updating, and deleting pods and services.

### Zookeeper
- Manages distributed systems
- Manages metadata and cluster nodes

- Remember that ZooKeeper is different from Kubernetes, which is a container orchestration system. ZooKeeper is a distributed coordination system that is used to manage distributed systems. It is used to manage metadata and cluster nodes.

### Apache NiFi
NiFi is a dataflow system for automating the flow of data between systems. It is designed to be easy to use, powerful, and reliable. It is a tool for building dataflow pipelines that are highly configurable, yet easy to manage.

<!--
## Visualization
## Security
-->

<!-- Section 3: Big Data Technologies -->
<!-- # Big Data Technologies
## Frameworks
## Tools
## Platforms
## Applications
## Databases
## Programming Languages
## Libraries -->

<!-- Section 4: Software Engineering -->
# Software Engineering

## Object-Oriented Principles
### Abstraction
[TODO: Add content]
### Encapsulation
[TODO: Add content]
### Polymorphism
[TODO: Add content]
### Inheritance
[TODO: Add content]
### SOLID Principles
The SOLID principles are five design principles that help us to write better object-oriented code. They are: **S**ingle Responsibility, **O**pen-Closed, **L**iskov Substitution, **I**nterface Segregation, and **D**ependency Inversion.

Overall, applying the SOLID principles delivers the following benefits:
- Reduced coupling between modules
- Better reusability
- Improved testability
- Reduced complexity
- Improved maintainability

#### Single Responsibility
It suggests that a class should have only one responsibility, or in other words, only one reason to change.

This means that a class should be designed to have a single responsibility or concern, and should not be responsible for multiple, unrelated tasks. By having a single responsibility, the class becomes more cohesive, easier to understand, and easier to maintain.

For example, imagine a class that handles both user authentication and file storage. This violates the SRP because the class has multiple responsibilities, and changing one responsibility could potentially affect the other. Instead, we should split the class into two separate classes, each with its own single responsibility: one class for user authentication and another class for file storage.

By following the Single Responsibility Principle, we can create classes that are more focused, easier to understand, and easier to maintain. We can also reduce coupling between modules or classes, making the code more flexible and easier to modify over time.

The key benefits of SRP include:

- Better code organization: By having classes with a single responsibility, we can organize our code more effectively and make it easier to navigate.
- Easier to maintain: Classes with a single responsibility are easier to understand and modify, making them easier to maintain over time.
- Improved reusability: Smaller, more focused classes can be reused in different contexts, making the code more modular and extensible.


#### Open/Closed
Classes should be **open** for extension but **closed** for modification.

This means that we should design our software in a way that allows new functionality to be added without modifying existing code. Instead of modifying existing code, we should create new code that extends or overrides the existing code.

For example, imagine we have a class that calculates the total price of an order. If we want to add a new discount feature to the order, we should not modify the existing code. Instead, we should create a new class that extends the existing class and adds the discount functionality.

By following the Open-Closed Principle, we can create software that is more flexible, maintainable, and scalable. We can add new features or functionality without breaking existing code, and we can create new code that extends or overrides existing code, without modifying it.

The key benefits of OCP include:

- Reduced coupling: By avoiding modification of existing code, we can reduce the dependencies between modules or classes, making the code more flexible and easier to maintain.
- Better reusability: By creating new code that extends or overrides existing code, we can reuse existing code in different contexts, making the code more modular and extensible.
- Improved testability: By creating new code that extends or overrides existing code, we can test individual modules or classes in isolation.

#### Liskov Substitution
The Liskov Substitution Principle (LSP) defines how subtypes should behave in relation to their base types. It was initially proposed by Barbara Liskov in 1987. It states that any instance of a base type should be replaceable by any instance of its subtypes, without altering the correctness of the program.

This means that if a class A is a subtype of class B, any instance of class A should be able to be used in place of an instance of class B, without breaking the code. This is because class A should be fully compatible with class B, and should not change the expected behavior of the program.

For example, if we have a base class Animal, and a subtype Dog, we should be able to use a Dog object in place of an Animal object, without changing the behavior of the program. If we have a method that accepts an Animal object as a parameter, we should also be able to pass in a Dog object, and the method should work correctly.

The Liskov Substitution Principle helps to ensure that the code is more flexible, maintainable, and scalable, as new subtypes can be added without breaking the code that uses the base type. It also helps to ensure that the code is more testable, as tests written for the base type can be used to test the subtypes as well.

#### Interface Segregation
The Interface Segregation Principle (ISP) is a design principle that suggests that software entities, such as classes or interfaces, should not be forced to depend on methods they do not use.

In simpler words, it means that we should split larger interfaces into smaller, more specific ones, so that clients can depend only on the interfaces that are relevant to them. This avoids unnecessary dependencies and reduces coupling between modules or classes.

For example, imagine a messaging service interface that has methods for sending text messages, voice messages, and video messages. If a client only needs to send text messages, it should not be forced to depend on the methods for sending voice or video messages. Instead, we should split the messaging service interface into smaller interfaces, such as a `TextMessagingService` interface and a `VideoMessagingService` interface, so that clients can depend only on the interfaces they need.

The key benefits of ISP include:

- Reduced coupling: By reducing the dependencies between modules or classes, we can make the code more flexible and easier to maintain.
- Better reusability: Smaller interfaces can be reused in different contexts, making the code more modular and extensible.
- Improved testability: Smaller interfaces make it easier to test individual modules or classes in isolation.

#### Dependency Inversion
The idea is that a class should not depend on a concrete implementation, but on an abstraction. This way, the class can be used with any implementation of the abstraction. The traditional direction of dependency is from the abstraction to the concrete implementation. The dependency inversion principle inverts this direction, so that the dependency goes from the concrete implementation to the abstraction. This is a good thing, because it allows us to use the same abstraction with different concrete implementations.

This principle is important because it allows us to decouple classes from each other, making the code more flexible, testable, and maintainable. It also allows us to use dependency injection, which is a design pattern that allows us to inject dependencies into a class, instead of having the class create the dependencies itself.

Dependency injection is also related to Inversion of Control (IoC), which is a design pattern that allows us to decouple the creation of objects from their usage. IoC is a general concept, while dependency injection is a specific implementation of IoC. 

This is an example that demonstrates the use of dependency inversion:

```python

from abc import ABC, abstractmethod

# Define the interface for the low-level module
class StorageInterface(ABC):
    @abstractmethod
    def read(self, key):
        pass

    @abstractmethod
    def write(self, key, value):
        pass

# Implement the low-level module
class LocalStorage(StorageInterface):
    def read(self, key):
        # Read from local storage
        pass

    def write(self, key, value):
        # Write to local storage
        pass

# Define the high-level module that depends on the low-level module via an abstraction
class DataProcessor:
    def __init__(self, storage: StorageInterface):
        self.storage = storage

    def process(self, key):
        data = self.storage.read(key)
        # Process the data
        self.storage.write(key, data)

# Use the high-level module with a specific implementation of the low-level module
storage = LocalStorage()
processor = DataProcessor(storage)
processor.process("data_key")

```

## Architecture
A software architecture is the structure or structures of a software system, which comprise software elements, the externally visible properties of those elements, and the relationships among them. The architecture of a software system is a metaphor, analogous to the architecture of a building. It allows for the description of the system at different levels of abstraction, and it provides a framework for understanding the system and its components.

### Hexagonal Architecture
The Hexagonal Architecture, also known as the Ports and Adapters architecture or Clean Architecture, is a software design pattern that aims to create flexible and maintainable software systems. It was introduced by Alistair Cockburn in 2005 and later popularized by Robert C. Martin (Uncle Bob).

The Hexagonal Architecture is based on the idea of separating the core business logic of the system from the implementation details and infrastructure. The core business logic is surrounded by a layer of ports, which are interfaces that define the inputs and outputs of the system. The ports provide a way for the core business logic to interact with the outside world without being tied to any specific implementation.

The ports layer is then surrounded by an adapter layer, which contains the concrete implementations of the ports. Adapters are responsible for handling the translation between the system's internal representation and the outside world's representation. Adapters can be thought of as the glue that connects the ports to the rest of the system.

In the design one can identify the following components:
- Domain: This area contains the core business logic of the system, including the entities, value objects, and business rules. The domain is the heart of the system and should be independent of any infrastructure or technology.

- Ports: Ports are interfaces that define the inputs and outputs of the system. They provide a way for the domain to communicate with the outside world without being tied to any specific implementation. There are two types of ports: inbound ports, which handle incoming requests to the system, and outbound ports, which handle outgoing requests from the system.

- Adapters: Adapters are concrete implementations of the ports. They are responsible for handling the translation between the system's internal representation and the outside world's representation. There are two types of adapters: inbound adapters, which handle incoming requests from the outside world and translate them into a format that the domain can understand, and outbound adapters, which handle outgoing requests from the domain and translate them into a format that the outside world can understand.

- Infrastructure: The infrastructure is the outermost layer of the system and contains all the technical details, such as databases, frameworks, and external APIs. The infrastructure is responsible for implementing the adapters and providing the necessary services to the domain. The infrastructure should be replaceable without affecting the rest of the system.

The benefits of the Hexagonal Architecture include:

Separation of concerns: The separation of the core business logic from the implementation details and infrastructure makes the system more modular and easier to maintain.
Testability: The use of ports and adapters makes it easy to write automated tests for the core business logic without needing to mock out the infrastructure.
Flexibility: The ports and adapters provide a clear separation between the system's core functionality and the outside world, which makes it easier to adapt the system to changing requirements or new technologies.

### Onion Architecture
The Onion Architecture is a software architecture pattern that separates the core domain logic of an application from the infrastructure and external interfaces. It is based on the idea of a layered architecture, where each layer is dependent on the layer below it, but not on the layer above it.

It was introduced in 2008 by Jeffrey Palermo and is based on the idea of an onion, where the center represents the core domain logic and the outer layers represent the infrastructure and external interfaces. The Onion Architecture can be seen as a variation of the Hexagonal Architecture, the difference being that the Hexagonal architecture does not specify a strict hierarchical layering of the components. Instead, it allows for a more flexible and modular design.

### Microservices Architecture
[TODO: Add content]
### Serverless Architecture
[TODO: Add content]

### Patterns
#### MVC
[TODO: Add content]
#### MVVM
[TODO: Add content]
#### MVP
[TODO: Add content]
#### MVI
[TODO: Add content]
#### VIPER
[TODO: Add content]
#### Inversion of Control
[TODO: Add content]

## Other design paradigms
### Convention over configuration
[TODO: Add content]
### Don't repeat yourself (DRY)
[TODO: Add content]
### Avoid Hasty Abstraction (AHA)
[TODO: Add content]

## Software Development Life Cycle
[TODO: Add content]
## Requirements Engineering
[TODO: Add content]
## Development Models
[TODO: Add content]
## Design Patterns
This list is not complete, for a complete and updated overview of design patterns, see the [Design Patterns](https://en.wikipedia.org/wiki/Software_design_pattern) article on Wikipedia.

### Creational Patterns
[TODO: Add content]
### Structural Patterns
[TODO: Add content]
### Behavioral Patterns
[TODO: Add content]

## Testing
[TODO: Add content]
<!-- https://en.wikipedia.org/wiki/Smoke_testing_(software) -->

<!-- Section 5: Soft Skills -->
# Soft Skills
## Agile Methodologies

# Practice Questions
- What is the difference between ETL and ELT, when would you use one over the other?
- What is Hadoop used for? What are its limitations? How does Spark solve these limitations?
- What's the difference between "selection" and "projection"?
  - Selection is the process of selecting a subset of rows from a table or dataset based on some condition. The condition is specified using a Boolean expression that is evaluated for each row in the dataset, and only the rows for which the expression evaluates to true are selected.
  - Projection is the process of selecting a subset of columns from a table or dataset. The columns to be selected are specified using a list of column names, and only the columns that are specified are included in the result.
- What is the stackable trait pattern in Scala?
  > Stackable Traits is a design pattern in Scala that allows for flexible and modular composition of behavior in classes. The pattern is based on the idea of composing traits to create a stack of behavior that can be mixed into a class.
  >
  In this pattern, each trait provides a piece of behavior that can be mixed into a class. These traits are designed to be stackable, meaning that they can be combined in any order to create a customized set of behavior for a specific class. Traits can also override methods or values from other traits in the stack.
  >
  The stack of traits is built by linearizing the class hierarchy, which means that traits are added in the order of inheritance. This results in a linear sequence of traits that can be used to build up the behavior of a class. The linearization process also ensures that methods and values are resolved in the correct order, so that the behavior of the class is consistent and predictable.
  >
  One of the benefits of using stackable traits is that it allows for modular and reusable code. By breaking down behavior into small, composable pieces, traits can be mixed and matched to create new behavior without having to rewrite existing code. This makes it easier to write code that is flexible, extensible, and easy to maintain.
  >
  Another benefit is that stackable traits allow for the creation of highly specialized behavior that is tailored to specific use cases. By combining traits in different ways, it's possible to create classes that have exactly the behavior that is needed for a particular situation, without having to create separate classes for each variation.

- In which way the garbage collector in JVM select the objects to remove from the memory?
  > 
  The garbage collector in the Java Virtual Machine (JVM) uses a process called "Mark and Sweep" to identify and remove objects that are no longer being used by the application.
  >
  During the "Mark" phase, the garbage collector traverses the object graph starting from the root set (which includes all live objects and object references), marking all reachable objects as live. This involves following all object references from the root set and recursively marking all reachable objects. Any objects that are not marked as live are considered garbage and can be reclaimed.
  >
  During the "Sweep" phase, the garbage collector reclaims the memory occupied by the garbage objects that were not marked as live during the "Mark" phase. This is done by adding the memory occupied by these objects to a free list of memory blocks that can be reused for future object allocations.
  >
  The selection of objects to remove from memory is based on whether they are reachable from the root set. Objects that are no longer reachable are considered eligible for garbage collection, while objects that are still reachable are not.

- What is a selaed trait in Scala?
  > In Scala, a sealed trait is a trait that can only be extended by classes defined in the same file as the trait. This means that it restricts the set of classes that can extend the trait, and is often used to implement closed class hierarchies.
  >
  When a trait is marked as sealed, it means that any subclass of the trait must be defined in the same file as the sealed trait itself. This allows the Scala compiler to know all possible subclasses of the trait, which can be useful for certain pattern matching and exhaustiveness checks.
  >
  Here's an example of a sealed trait in Scala:
  ```scala
  sealed trait Shape
  case class Circle(radius: Double) extends Shape
  case class Rectangle(width: Double, height: Double) extends Shape
  ``` 



# Learning Resources
- [Microsoft Azure Guides](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/) - Much of the content is general and applicable to cloud computing in general.