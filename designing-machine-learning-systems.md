# Designing Machine Learning Systems - by Chip Huyen

# Table of Contents
- [Designing Machine Learning Systems - by Chip Huyen](#designing-machine-learning-systems---by-chip-huyen)
- [Table of Contents](#table-of-contents)
- [Chapter 1: Overview of Machine Learning Systems](#chapter-1-overview-of-machine-learning-systems)
  - [When to use Machine Learning](#when-to-use-machine-learning)
  - [Machine Learning Use Cases](#machine-learning-use-cases)
  - [ML Research VS Production](#ml-research-vs-production)
- [Chapter 2: Introduction to Machine Learning System Designs](#chapter-2-introduction-to-machine-learning-system-designs)
  - [Objective](#objective)
  - [Requirements](#requirements)
  - [Iterative Process of ML Project](#iterative-process-of-ml-project)
  - [Framing ML Problems](#framing-ml-problems)
    - [Type of ML tasks](#type-of-ml-tasks)
    - [Decoupling objectives](#decoupling-objectives)
- [Chapter 3: Data Engineering Fundamentals](#chapter-3-data-engineering-fundamentals)
  - [Data sources](#data-sources)
  - [Data formats](#data-formats)
    - [Row-major vs Column-Major Format](#row-major-vs-column-major-format)
    - [Text vs Binary Format](#text-vs-binary-format)
  - [Data Models](#data-models)
    - [Relational Model](#relational-model)
    - [NoSQL](#nosql)
      - [Document Model](#document-model)
      - [Graph Model](#graph-model)
    - [Structure vs Unstructured Data](#structure-vs-unstructured-data)
  - [Data Storage Engines and Processing](#data-storage-engines-and-processing)
    - [ETL](#etl)
  - [Modes of Dataflow](#modes-of-dataflow)
    - [Data Passing Through Database](#data-passing-through-database)
    - [Data Passing Through Services](#data-passing-through-services)
    - [Data Passing Through Real-Time Transport](#data-passing-through-real-time-transport)
  - [Batch Processing vs Stream Processing](#batch-processing-vs-stream-processing)
- [Chapter 4: Training Data](#chapter-4-training-data)
- [Chapter 5: Feature Engineering](#chapter-5-feature-engineering)
- [Chapter 6: Model Development and Offline Evaluation](#chapter-6-model-development-and-offline-evaluation)
- [Chapter 7: Model Deployment and Prediction Service](#chapter-7-model-deployment-and-prediction-service)
- [Chapter 8: Data Distribution Shifts and Monitoring](#chapter-8-data-distribution-shifts-and-monitoring)
- [Chapter 9: Continual Learning and Test in Production](#chapter-9-continual-learning-and-test-in-production)
- [Chapter 10: Infrastructure and Tooling for MLOps](#chapter-10-infrastructure-and-tooling-for-mlops)
- [Chapter 11: The Human Side of Machine Learning](#chapter-11-the-human-side-of-machine-learning)



# Chapter 1: Overview of Machine Learning Systems
Machine Learning (ML) systems consists of ML algorithms, business logic, frondend UI, data, evaluation metric, logic for developing, monitoring and updating the models, stakeholders, as well as underlying infrastructure.

## When to use Machine Learning
ML is an approach to **learn** **complex patterns** from **existing data** and use these patterns to make **predictions** on **unseen data**.

- **Learn**: the system has the capacity to learn
- **Complex patterns**: there are patterns to learn, and they are complex
- **Existing data**: data is available, or it's possible to collect data
- **Predctions**: it's a predictive problem (eg: approximation for compute-intensive problems)
- **Unseen data**: unseen data shares patterns with the training data

Additional Problem Characteristics
- Repetitive
- The cost of wrong prediction is cheap
- At sclae
- The patterns are constantly changing

Conditions where ML shoudln't be used:
- Unethical
- When simpler solution do the tricks
- Not cost-effective

## Machine Learning Use Cases
- Recommender system
- Search engine
- Prediction typing
- Photo editing
- Face/fingerprint recognition/authentication
- Machine translation
- Fraud detection
- Price optimization
- Churn prediction
- Support ticket classification
- Brand monitoring

## ML Research VS Production
| | Research | Production |
| --- | --- | --- |
| Requirements | State-of-the-art model performance on benchmark datasets | Different stakeholders have different requirements |
| Computational priority | Fast training, high throughput | Fast inference, low latency |
| Data | Static | Constantly shifting |
| Fairness and Interpretability | Often not a focus | Must be considered |

---
** Criticism of ML Leaderboards
- These competitions have already handled hards steps needed for building ML systems
- A model can perform better just by luck (multiple hypothesis-testing scenario)
- Focus on accuracy at the expense of other qualities such as compactness, fairness, energy efficiency
---

> **_STATISTICS:_** In 2019, **Booking.com** found that an increase of about 30% in latency cost about 0.5% in conversion rate.
> In 2016, **Google** found that more than half of mobile users will leave a page if it takes >3 seconds to load.

> **_NOTE:_** It's a common practice to use high percentile to specify the performance for your systems. (eg: The 90th percentile latency of a system must be below a certain number.)



# Chapter 2: Introduction to Machine Learning System Designs
## Objective
Business objective &rarr; ML objectives  

The ultimate goal of business is to increase profit. 

The effect of ML project on business objectives can be hard to reason about. For example, an ML model that give more personalized can make customer happy and **spend more money**, it  can also solve their problem faster which makes them **spend less money**.

## Requirements
Requirements to guide the development of ML systems:
- **Reliability** - Perform correct function at desired level in the face of adversity
- **Scalability** - Scale up and down, artifact managements
- **Maintainability** - Allow different contributoras to work using the tools they are comfortable with. Documentation, versioning, reproducibility
- **Adaptability** - Adapt to shifting data distibutions and business requirements. Capacity to discovering aspects for performance improvement, and allowing updates without service interruptions.

## Iterative Process of ML Project
1. Project scoping
2. Data engineering
3. ML model development
4. Deployment
5. Monitoring and continual learning
6. Business analysis


## Framing ML Problems
Business problem &rarr; ML problem  

Changing the way you frame the problem might make your problem significantly harder or easier.

### Type of ML tasks
- Regression
- Classification
  - Binary
  - Multiclass (if number of classes is large, hierarchical classification might be useful)
  - Multilabel (usually more challenging for company)

### Decoupling objectives
When there are multiple objective (eg: improve quality, improve engagement), one can
1. (not so ideal) Combine the 2 lossess into one loss and train a model to minimize the loss
2. Train two different models, each optimized for one objective, and combine the model's output.


# Chapter 3: Data Engineering Fundamentals

## Data sources
- User input data (require more data validation and fast processing)
- System-generated data (eg: logs, model predictions)
- Internal databases (eg: inventory, customer relationship)
- Third-party data

## Data formats
The process of conveting a data structure of object state into a format that can be stored or transmitted and reconstructed later is *data serilization*.

| Format | Binary/Text | Human-readable | Example Use cases |
| --- | --- | --- | --- |
| JSON | Text | Yes | Everywhere |
| CSV | Text | Yes | Everywhere |
| Parquet | Binary | No | Hadoop, Amazon Redshift |
| Avro | Binary primary | No | Hadoop |
| Profobuf | Binary primary | No | Google, Tensorflow (TFRecord) |
| Pickle | Binary | No | Python, PyTorch seralization |


### Row-major vs Column-Major Format
**CSV** is row-major, **parquet** is column-major. Row-major means that consecutive elements in a row are stored next to each other, same for column-major.

Overall, row-major formats are better when you have to do a lot of writes, whereas column-major formats are better when you have to do a lot of column-based reads.

> **_NOTE:_** Pandas is built around the columnar format, while Numpy by default row-major.

### Text vs Binary Format
Text is readable but use more space, vice versa for binary format.

## Data Models

### Relational Model
Data is organized into relations; each relations is a set of tuples.

It is often desirable for relations to be normalized. **Data normalization** can follow normal forms such as first normal form (1NF), second normal form (2NF), etc.  
**Pro**: helps to reduce redundancy and improve data integrity.
**Con**: Data is spread across multiple relations. Joining can be expensive for large tables.  

Most popular query language - SQL
- Declarative language
- With certain added features, SWL can be Turing-complete

### NoSQL
For certain use cases, relational data model can be restrictive. (demands data follows a strict schema, painful schema management)

**NoSQL** stands for Not Only SQL. Two major types of nonrelational models are the document model and the graph model.

#### Document Model
The **document model** targets use cases where data comes in self-contained documents and relationships between one document and another are rare.  

A document can be JSON, XML, or binary format like BSON (binary JSON). All documents in a document database are assumed to be encoded in the same format.  

A documents in the same collection can have completely different schemas. It is much more flexible than a table.  

Documents shift the responsibility of assuming structures from the application that writes the data to the application that reads the data.  

Pro: Better locality than relational model  
Con: Harder and less efficient to execute joins across documents  

#### Graph Model
The **graph model** targets use cases where relationships between data items are common and important.  

A graph consists of nodes and edges, where the edges represent the relationships between the nodes. A database that uses graph structures to store data is called a graph database. It is faster to retrieve data based on relationships.

### Structure vs Unstructured Data
| Structured Data | Unstructured Data |
| --- | --- |
| Clearly defined schema | No schema |
| Can only handle data with specific schema, and have problem with schema change | Can handle any data, no worry about schema change (yet), as the worry is shifted to downstream application | 
| Easy to search and analyze | Fast arrival |
| Data warehouses | Data lakes |

## Data Storage Engines and Processing
Storage engines, also known as **databases**, are the implmentation of how data is stored and retrieved on machines.

Types of database workload
- Online transactional processing (OLTP)
- Online analytical processing (OLAP)

Transactional databases are designed to satisfy the low latency, high availability requirements. They are usually row-based. They usually follow ACID, which stands for
- Atomicity - To gurantee that all the steps in a transaction are completed as a group, which means all steps must fail when any steps fail.
- Consistency - To gurantee that all the transactions coming through must follow predefined rules (eg: must be made by valid user)
- Isolation - To gurantee two transactions that happen at the same time as if they were isolated (eg: two users shouldn't get the same drive on Uber)
- Durability - To gurantee that once a transaction has been committed, it will remain commited even in the case of system failure (eg: ride continue even when phone dies)

Systems that do not meet the ACID criteria are sometimes called BASE (Basically Available, Soft state, and Eventual consistency), which has a more vague definition.

Both the terms OLTP and OLAP have become outdated for the following reasons
1. The separation of transactional and analytical databases was due to limitations of technology, which has been closed (eg: CockroachDB, Apache Iceberg, DuckDB)
2. In the traditional OLTP or OLAP paradigm, storage and processing are tightly coupled. Paradigm shift of decoupling storage from processing (compute) has been adopted by many data vendors (eg: Google's BigQuery, Snowflake, IBM, Teradata). In this paradigm, the data can be stored in the same place, with a processing layer on top that can be optimized for different types of queries.
3. "Online" has become an overloaded term that can mean many different things. From *"connected to the internet"* to *"in production"* to *"the speed at which your data is processed and made available" (online, nearline, offline)*.

### ETL
**ETL** stands for:
- Extract - Extracting and validating data from data sources
- Transform - Processing the data (eg: standardization, deduplication, sort, aggregation, feature engineering, more data validations)
- Load - Deciding how and how often to load the transformed data into the target destination

*ELT (extract, load, transform)* loads data into storage first and then orocesses it later.

## Modes of Dataflow
When data is passed from one process to another, data flows from one process to another, which gives us a dataflow. There are three main modes of dataflow.
- Data passing through databases
- Data passing through services using requests (eg: REST and RPC APIs)
- Data passing through a real-time transport like Apache Kafka and Amazon Kinesis

### Data Passing Through Database
Process A write that data into a database, and process B simply reads from the database.

Cons:
1. Require both processed to have access to the same database
2. Read/write from database can be slow

### Data Passing Through Services
Process B sends a request to process A that specifies the data B needs, and A returns the requested data through the same network. As processes communicate through requests, we say that this is *request-driven*.

A service is a process that can be accessed remotely (eg: through a network). In this example, A is exposed to B as a service.

This mode of data passing is tightly coupled with the service-oriented architecture. Structuring different components as separate services allows each component to be developed, tested and maintained independently of one another, which gives a microservice architecture.

Con:
- Request-driven data passing is synchronous
  - If a service is down, another service might keep resending the request until it times out
  - If a service is down before it receives a response, the response will be lost
- A service that is down can cause all services that require data from it to be down

Popular Request Style:
- **REST (Representational State Transfer)**  
Designed for requests over networks. HTTP os am implementation of REST.
- **RPC (Remote Procedure Call)**  
Designed to "make a request to a remote network service look the same as calling a function or method in your programming language".

### Data Passing Through Real-Time Transport
Real-time transports (sometimes called event bus) can be thought of as in-memory storage for data passing among services. It acts as a broker.

A piece of data broadcast to a real-time transport is called an **event**. This architecture is therefore also called *event-driven*.  

[Request-driven architecture](#data-passing-through-services) works well for systems that rely more on logic than on data. Event-driven architecture works better for systems that are data-heavy.

This mode of data passing is somewhere between passing through databases and passing through services. It allows for asynchronous data passing with reasonably low latency.

Common types of real-time transports:
- **Pubsub (publish-subcribe)**  
    - Any service can publish to different topics in a real-time transport, and any services that subcribes to a topic can read all the events n that topic. The service that produce data don't care about what services consumes their data. Pubsub solutions usually have a retention policy (adta will be deleted or moved to a permanent storage after certain period of time)
    - Example: Apache Kafka, Amazon Kinesis
- **Message queue**  
    - An event often has intended consumers (an event with ntended consumers is called a message). Message queue is responsible for getting the message to the right consumers
    - Example: Apache RocketMQ, RabbitMQ

## Batch Processing vs Stream Processing
| Batch Processing | Stream Processing |
| --- | --- |
| Historical data | Streaming data (Data in [real-time transport](#data-passing-through-real-time-transport)) |
| Data processed in batch job | Doing computation on streaming data, can also be kicked off  periodically, but usually in much shorter period |
| High latency | Low latency when done right, stateful computation |
| Batch features (static features) | Streaming features (dynamic features) |

Both can be highly scalable and fully distibuted.

Tools for streaming data: Apache Flink, KSQL, Spark Streaming



# Chapter 4: Training Data






# Chapter 5: Feature Engineering





# Chapter 6: Model Development and Offline Evaluation






# Chapter 7: Model Deployment and Prediction Service




# Chapter 8: Data Distribution Shifts and Monitoring





# Chapter 9: Continual Learning and Test in Production






# Chapter 10: Infrastructure and Tooling for MLOps






# Chapter 11: The Human Side of Machine Learning



