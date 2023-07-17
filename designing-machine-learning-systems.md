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
  - [Sampling](#sampling)
    - [Nonprobability Sampling](#nonprobability-sampling)
    - [Probability-Based Sampling](#probability-based-sampling)
  - [Labeling](#labeling)
    - [Hand labels](#hand-labels)
    - [Natural labels](#natural-labels)
    - [Methods to Handle the Lack of Labels](#methods-to-handle-the-lack-of-labels)
      - [Weak Supervision](#weak-supervision)
      - [Semi-supervision](#semi-supervision)
      - [Transfer learning](#transfer-learning)
      - [Active learning](#active-learning)
  - [Class Imbalance](#class-imbalance)
    - [Data-level methods: Resampling](#data-level-methods-resampling)
    - [Algorithm-level methods](#algorithm-level-methods)
  - [Data Augmentation](#data-augmentation)
    - [Simple label-preserving transformations](#simple-label-preserving-transformations)
    - [Pertubation](#pertubation)
    - [Data Synthesis](#data-synthesis)
- [Chapter 5: Feature Engineering](#chapter-5-feature-engineering)
  - [Common Feature Engineering Operations](#common-feature-engineering-operations)
    - [Handling Missing Values](#handling-missing-values)
    - [Scaling](#scaling)
    - [Discretization](#discretization)
    - [Encoding Categorical Features](#encoding-categorical-features)
    - [Feature Crossing](#feature-crossing)
    - [Discrete and Continuous Positional Embeddings](#discrete-and-continuous-positional-embeddings)
  - [Data Leakage](#data-leakage)
    - [Reason of leakage](#reason-of-leakage)
  - [Engineering Good Features](#engineering-good-features)
- [Chapter 6: Model Development and Offline Evaluation](#chapter-6-model-development-and-offline-evaluation)
  - [Evaluating ML Models](#evaluating-ml-models)
    - [Six tips for Model Selection](#six-tips-for-model-selection)
    - [Ensembles](#ensembles)
  - [Experiment Tracking and Versioning](#experiment-tracking-and-versioning)
    - [Experiment Tracking](#experiment-tracking)
    - [Versioning](#versioning)
  - [Debugging  ML Models](#debugging--ml-models)
  - [Distributed Training](#distributed-training)
    - [Data Parallelism](#data-parallelism)
    - [Model Parallelism](#model-parallelism)
  - [AutoML](#automl)
    - [Soft AutoML: Hyperparameter Tuning](#soft-automl-hyperparameter-tuning)
    - [Hard AutoML: Architecture Search and Learned Optimizer](#hard-automl-architecture-search-and-learned-optimizer)
  - [4 Phases of ML Model Development](#4-phases-of-ml-model-development)
  - [Model Offline Evaluation](#model-offline-evaluation)
    - [Baselines](#baselines)
    - [Evaluation Methods](#evaluation-methods)
- [Chapter 7: Model Deployment and Prediction Service](#chapter-7-model-deployment-and-prediction-service)
  - [Batch Prediction vs Online Prediction](#batch-prediction-vs-online-prediction)
  - [Model Compression](#model-compression)
    - [Low-Rank Factorization](#low-rank-factorization)
    - [Knowledge Distillation](#knowledge-distillation)
    - [Pruning](#pruning)
    - [Quantization](#quantization)
  - [ML on the Cloud and on the Edge](#ml-on-the-cloud-and-on-the-edge)
    - [Edge Devices](#edge-devices)
      - [Optimize Model for Edge Device](#optimize-model-for-edge-device)
      - [Manual vs Using ML to Optimize ML](#manual-vs-using-ml-to-optimize-ml)
      - [ML in Browsers](#ml-in-browsers)
- [Chapter 8: Data Distribution Shifts and Monitoring](#chapter-8-data-distribution-shifts-and-monitoring)
  - [System Failures](#system-failures)
    - [Software System Failures](#software-system-failures)
    - [ML-Specific Failures](#ml-specific-failures)
      - [Degenerate Feedback Loops](#degenerate-feedback-loops)
  - [Data Distribution Shift](#data-distribution-shift)
    - [Type of Data Distribution Shifts](#type-of-data-distribution-shifts)
    - [Detecting Data Distribution Shifts](#detecting-data-distribution-shifts)
    - [Addressing Data Distribution Shifts](#addressing-data-distribution-shifts)
  - [Monitoring and Observability](#monitoring-and-observability)
    - [Monitoring Toolboxs](#monitoring-toolboxs)
      - [Log](#log)
      - [Dashboard](#dashboard)
      - [Alert](#alert)
    - [Observability](#observability)
- [Chapter 9: Continual Learning and Test in Production](#chapter-9-continual-learning-and-test-in-production)
  - [Continual learning](#continual-learning)
    - [Stateless Retraining vs Stateful Retraining](#stateless-retraining-vs-stateful-retraining)
- [Chapter 10: Infrastructure and Tooling for MLOps](#chapter-10-infrastructure-and-tooling-for-mlops)
  - [Storage and Compute](#storage-and-compute)
    - [Public Cloud vs Private Data Centers](#public-cloud-vs-private-data-centers)
  - [Development Environment](#development-environment)
    - [IDE](#ide)
    - [Containers](#containers)
  - [Resource Management](#resource-management)
    - [Basic Components](#basic-components)
    - [Workflow management tools](#workflow-management-tools)
  - [ML Platform](#ml-platform)
    - [Model Development](#model-development)
    - [Model Store](#model-store)
    - [Feature Stores](#feature-stores)
  - [Build vs Buy](#build-vs-buy)
- [Chapter 11: The Human Side of Machine Learning](#chapter-11-the-human-side-of-machine-learning)
  - [User Experience](#user-experience)
  - [Team Structure](#team-structure)
    - [Involvement of subject matter experts (SME)](#involvement-of-subject-matter-experts-sme)
    - [End-to-end data scientists](#end-to-end-data-scientists)
      - [Approach 1: Have a separate team to manage production](#approach-1-have-a-separate-team-to-manage-production)
      - [Approach 2: Data scientists own the entire process](#approach-2-data-scientists-own-the-entire-process)
  - [Responsible AI](#responsible-ai)
    - [Case study 1: Automated grader](#case-study-1-automated-grader)
    - [Case Study 2: Anonymous data](#case-study-2-anonymous-data)
    - [A Framework for Responsible AI](#a-framework-for-responsible-ai)



# Chapter 1: Overview of Machine Learning Systems
Machine Learning (ML) systems consists of ML algorithms, business logic, frondend UI, data, evaluation metric, logic for developing, monitoring and updating the models, stakeholders, as well as underlying infrastructure.

## When to use Machine Learning
ML is an approach to **learn** **complex patterns** from **existing data** and use these patterns to make **predictions** on **unseen data**.

- **Learn**: the system has the capacity to learn
- **Complex patterns**: there are patterns to learn, and they are complex
- **Existing data**: data is available, or it's possible to collect data
- **Predictions**: it's a predictive problem (eg: approximation for compute-intensive problems)
- **Unseen data**: unseen data shares patterns with the training data

Additional Problem Characteristics
- Repetitive
- The cost of wrong prediction is cheap
- At scale
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
    - Approach 1: Treat it as multilabel classification problems
    - Approach 2: Turn it into a set of binary classification problems

### Decoupling objectives
When there are multiple objective (eg: improve quality, improve engagement), one can
1. (not so ideal) Combine the 2 lossess into one loss and train a model to minimize the loss
2. Train two different models, each optimized for one objective, and combine the model's output.


Data science hierarchy of needs
![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781098107956/files/assets/dmls_0207.png)

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
- **Pro**: helps to reduce redundancy and improve data integrity.  
- **Con**: Data is spread across multiple relations. Joining can be expensive for large tables.  

Most popular query language - SQL
- Declarative language
- With certain added features, SQL can be Turing-complete

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
- **Atomicity** - To gurantee that all the steps in a transaction are completed as a group, which means all steps must fail when any steps fail.
- **Consistency** - To gurantee that all the transactions coming through must follow predefined rules (eg: must be made by valid user)
- **Isolation** - To gurantee two transactions that happen at the same time as if they were isolated (eg: two users shouldn't get the same drive on Uber)
- **Durability** - To gurantee that once a transaction has been committed, it will remain commited even in the case of system failure (eg: ride continue even when phone dies)

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
Common challenges in creating training data
- Label multiplicity problem
- The lack of labels problem
- The class imbalance problem
- Lack of data problem

Data is full of potential biases. These biases can have many possible causes. There are biases caused during collecting, sampling or labelling. Historical data might be embedded with human biases, and ML models trained on this data can perpetuate them. Use data but don't trust it too much!

## Sampling
Sampling can happen in different steps of an ML project lifecycle.
- Sampling from real world to create dataset
- Sampling from dataset to split training and test dataset
- Sampling from ML events for monitoring

Sampling allows quick experiments.

Two major families of sampling, *nonprobability sampling* and *random sampling*.

### Nonprobability Sampling
- **Convenience sampling** -  Sampling based on data availability
- **Snowball sampling** - Future samples are selected based on existing samples. (e.g. scrape Twitter users, and their connections)
- **Judgement sampling** - Experts decide what samples to include
- **Quota sampling** - Select samples based on certain quotas for certain slices of data without any randomization. (e.g. 100 responses from 10-30, 30-50, above 50)

Nonprobability sampling are riddled with selection biases. Example: language model use data that can be easily collected, sentiment analysis use review data with natural labels, self-driving cars data are from the company location with more specific weather.

### Probability-Based Sampling
- **Simple Random Sampling** - All samples in the population have equal probabilities of being selected.
  - Pro: Easy to implement
  - Con: Rare categories of data can be missing
- **Stratified Sampling** - Divide popultation into group (stratum) and sample from each groups separately
  - Con: Might not work if sample belong to multiple groups
- **Weighted Sampling** - Each sample is given a weight, which determine the probability of it being sampled. (e.g. recent data is more valuable and hence given a higher weight)
  - In python: this can be done using `random choices` with the `weights` argument
  - Another similar concepts, **sample weights** are used to assign weights or importance to training samples, which affect the loss function
- **Reservoir Sampling** - useful for streaming data
  - Steps
    1. Put the first k elements into the reservoir.
    2. For each incoming n-th element, generate a random number `i` such that `1 <= i <= n`
    3. If `1 <= i <= k`, replace the i-th element in the reservoir with the n-th element. Else, do nothing.
  - Each incoming n-th element have `k/n` probability of being selected
- **Importance Sampling** - Allow us to sample from a distribution when we only have access to another distribution.
  - Example: `P(x)` is hard to sample, we sample with proposal distribution / importance distribution `Q(x)` and weigh this sample by `P(x)/Q(x)`.
  - Example use case in ML: policy-based reinforcement learning

## Labeling
Most ML models in production today are supervised, and hence need labelled data. The performance depends heavily on the quality and quantity of the labeled data it's trained on.

Data labeling has gone from being an auxiliary task to being a core function of many ML teams in production.

Type of labeling
- Hand labels
- Natural labels

### Hand labels
Cons:
- Expensive, especially when subject matter expertise is required
- Threat to data privacy (e.g. confidential financial information, patient's medical records)
- Slow (e.g. lung cancers X-rays label took almost a year to obtain sufficient label)
  - Make model less adaptive to changing environment and requirements
- Label multiplicity
  - Example: Different labelers may label entity differently (e.g. `[Dark Lord] of the [Sith]` vs `[Dark Lord of the Sith]`)
  - Solution: Set clearer rules

**Data lineage** - Keep track of the origin of each of the data samples as well as its labels

### Natural labels
Natural labels are model's predictions that can be automatically evaluated or partially evaluated by the system.

Example: Estimated time of arrival of a certain route on Google Map, stock price prediction

The canonical example of tasks with natural labels is *recommender system*. 

The label of recommender system is whether the recommended items get clicked within a certain time frame. The recommendation that don't get clicked can be presumed to be bad, which is called *implicit label* (negative label presumed due to the lack of positive label).

**Behavioral labels** - Natural labels that are inferred from user behaviors like clicks or ratings

Even if the task doesn't inherently have natural labels, it might be possible to set up feedback collection. (e.g. Like button in news, asking for user translation on Google translate)

**Feedback loop length** - The time between the serving prediction and receive feedback.
- Minute long - Recommend product in Amazon, recommend people to follow on Twitter
- Hours - Blog post, YouTube video

User feedbacks can differ in volume, strength of signal and feedback loop length. For example, clicks is high is volume but weaker signal, while adding a product to cart has lower volume but stronger signal. Focusing on any is valid approach.

There might also be premature negative label.

### Methods to Handle the Lack of Labels
| Method | How | Groud truth requirement |
| --- | --- | --- |
| Weak supervision | Leverages (often noisy) heuristics to generate labels | No, but a small number of lables are recommended to guide the development of heuristics |
| Semi-supervision | Leverage structural assumptions to generate labels | Yes, a small number of initial labels as seed to generate more labels |
| Transfer learning | Leverage models pretrained on another task for your new task | No for zero shot learning, yes for fine-tuning, the number of ground truths required is often much smaller than training from scratch |
| Active learning | Labels data samples that are most useful for your model | Yes |

#### Weak Supervision
Rely on heuristics, which can be developed with subject matter expertise, to label data.

Most popular open source tool: Snorkel (developed bu Stanford AI Lab). 

*labeling function (LF)* - a function that encode heuristics

Types of heuristics
- Keyword heuristic
- Regular expressions
- Database lookup
- The output of other models

Heuristics can be noisy and multiple heuristics can have conflicts.

Pro:
- Can be helpful when the data has strict privacy requirements.
- Much easier to rerun comparing to hand label

#### Semi-supervision
*Literature survey: [link](https://pages.cs.wisc.edu/~jerryzhu/pub/ssl_survey.pdf), [link](https://link.springer.com/article/10.1007/s10994-019-05855-6)*

Leverages structural assumptions to generate new labels based on a small set of initial labels.

Methods:
- *Self training* - Training a model with existing labels and generate predictions. Assuming that the predictions with high raw probability scores are correct, added these labels to the training set and train a new model on the expanded training set. Iterate until the model is satisfactory.
- Assume that data samples with similar characteristics share the same label. E.g. all hashtags in the same tweet can be tagged to the same label
- Pertubation-based method - Apply small pertubations to training instances to obtain new training instances, assumptions that small pertubations to a sample shouldn't change its label. The perturbed samples have the same labels as the unperturbed samples. (e.g. adding white noise to image, random value to embedding)

Most useful when the number of training labels is limited.

Challenge: how much of the limited data should be used to evaluate multiple candidate model

Solution: Use a reasonably large evaluation set to select the best model, then continue training the champion model on the evaluation set.

#### Transfer learning
Reused a developed model as starting point for a model on a second task.

Usually base task is trained on cheap and abundant training data.

Transfer learning lowers the entry barrier into ML by reducing upfront cost for labeling data. It enables many applications that were previously impossible due to the lack of training samples.

#### Active learning
*Literature survey: [link](https://burrsettles.com/pub/settles.activelearning.pdf)*

Label the samples that are most helpful to the models according to some metrics or heuristics.

Example: 
- Using metric uncertainty measurement, labels the example that the models are less certain about
- Query-by-committee (ensemble method) - Use a committee of several candidate models to vote for which label next based on uncertainty
- Select model that reduce the loss the most or give highest gradient descent updates


Active learning can be helpful when works with real-time data. Active learning allows your model to learn more effectively in real time and adapt faster to changing environments

## Class Imbalance
Class imbalance typically refers to a problem that there is a substantial difference in the number of samples in each class of the training data. E.g. X-ray images of 99% normal patient and 1% cancer patient.

Can also happen to regression, e.g. strongly left-skewed or right-skewed.

Class imbalance makes ML difficult for the following three reasons.
1. Insufficient signal for your model to learn to detect the minority class
2. Make it easier for the model to stuck in nonoptimal solution (e.g. model learn to predict normal as it is 99% accuracy)
3. Asymmetric costs of error (rare class costs more), and the model need to be able to handle it

Class imbalance is a norm in real-world settings. (e.g. fraud detection, disease screening, resume screening, object detection)

Causes of class imbalance
1. Inherent
2. Biases during the sampling process (e.g. spam email are filtered before reaching inbox, getting from inbox might result in limited percentage of spam label)
3. Labeling error (e.g. labeler not aware of a label and hence only label the other labels)

Sensitivity to imbalance increases with the complexity of the problem

Solutions to handle class imbalance
1. Choosing the right metrics for your problem
2. Data-level model, which means changing the data distribution to make it less imbalanced
3. Algorithm-level methods, which means changing your learning method to make it more robust to class imbalance

Use precision-recall curve, which gives a more informative view of an algorithm's performance on tasks with heavy class imbalance.

### Data-level methods: Resampling
- Oversampling 
  - **SMOTE (synthetic minority oversampling technique)** - synthesizes novel samples of the minority class through sampling convex combinations of existing data points within the minority class
- Undersampling 
  - **Tomek Link** - find pair of samples from opposite classes that are close in proximity and remove the sample of the majority class in each pair

Other methods - Near-Miss, one-sided selection, two-phase learning, dynamic sampling

The methods above only work well for low-dimensional data

Two-phase leaarning - Randomly undersampling large classes until each class only have N instances, and then fine-tune your model on the original data

Dynamic sampling - Oversampling the low-performing classes and undersampling the high-performing classes during the training process

### Algorithm-level methods
Alter the algorithm to make it more robust to class imbalance

Adjustment to loss function, give important instance higher weight
| Method | Description | Con |
| -- | -- | -- |
| Cost-sensitive learning | Using a cost matrix to specify cost `C_ij` (e.g. false positive is twice costly than false negative) | Need to manually define the cost matrix |
| Class-balanced loss | Make the weight of each class inversely proportional to the number of samples in that class. A more sophisticated version of this loss can take into the overlap among existing samples, such as class-balanced loss based on effective number of samples | - |
| Focal loss | Assign a higher weight for samples that has a lower probability of being right | - |

Emsembles have shown to help with the claas imbalance problem too


## Data Augmentation
Data Augmentation is a family of technique to increase the amount of training data. It is traditionally used for tasks with limited data. In recent year, it is shown to be useful even when there are a lot of data, to make the models more robust to noise and even adversarial attack.

### Simple label-preserving transformations
- Computer Vision - Randomly modify an image whole preserving its label. These include cropping, flipping, rotating, inverting (horizontally or vertically), erasing part of the image, etc
- Natural Language Processing - Randomly replace a word with a similar word (e.g. happy -> glad), assuming that this replacement wouldn't change the meaning or the sentiment of the sentence

### Pertubation
Using deceptive data to trick a neural network into making wrong predictions is called *adversarial attack*. Adding noise to samples is a common technique to create adversarial sample

Adding noisy samples to training data can help models recognize weak spots in their learned decision boundary and improve their performance. Noisy samples can be created by either
- adding random noise
- search strategy

This type of augmentation is called *adversarial augmentation*

*DeepFool* - An algorithm that find the minimum possible injection needed to cause a misclassification with high confidence

Adversarial augmentation is less common in NLP, as adding random characters to a random sentence will make it gibberish. 

However, it can be used to make models more robust. E.g. BERT, where the model randomly choose 15% of all tokens in each sequence and replace 10% of the chosen tokens with random words. (which means 1.5% of all tokens might result in non-sensical meaning). Their [study](https://aclanthology.org/N19-1423.pdf) shows that a small fraction of random replacement gives the model a small performance boost.

### Data Synthesis
- Natual Language Processing - templates (e.g. `Find me a [CUISINE] resturant within [NUMBER] miles of [LOCATION]`)
- Computer Vision - Mixup (Combine existing examples with discrete labels to generate continuous labels)
- Using neural network to synthesize training data (e.g. CycleGAN)

Mixup improves model generalization, reduces their memorization of corrupt labels, increase their robustness to adversarial examples, and stabilizes the training of generative adversarial networks

Resource: [A Survey on Image Data Augmentation for Deep Learning](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-019-0197-0)


# Chapter 5: Feature Engineering
There are many possible features to use in your model. The process of choosing what information to use and extract them into usable format is **feature engineering**.

Traditionally, for Natural Language Processing (NLP), you would have to manually apply classical text processing techniques (e.g. lemmatization, stop-word removal, lowercase, n-gram, etc). 

With the rise of deep learning, you can split raw text into words and create vocabulary out of the word, and let deep learning model to extract the useful feature. Deep learning is sometimes called feature engineering.

However, as of this writing, the majority of ML applications in prodcution isn't deep learning. Also, an ML system will likely need data beyond just text and images and hence require engineered features (e.g. number of upvotes/downvotes, characteristics of user, popularity of thread)

## Common Feature Engineering Operations
### Handling Missing Values
Types of missing values
- Missing not at random (MNAR) - the reason of is because of the value itself (e.g. respondents with higher income didn't disclose their income)
- Missing at random (MAR) - the reason of missing is not due to the value itself, but due to another observed variable (e.g. people with gender A don't like disclosing their age)
- Missing completely at random (MCAR) - no pattern

Technique to handle missing values
| Name | Technique | Pro | Con |
| -- | -- | -- | -- |
| **Deletion** | <li>**Column deletion**</li> <li>**Row deletion** - Work when the missing values is completely at random and the number of examples with missing values is small (e.g. 0.1% instead of 10%)</li> | Easier to do | <li>Might remove important information and reduce the accuracy of the model (e.g. Marital status might be highly correlated with buying houses, removing missing values not at random can remove important implicit information)</li><li>Create biases</li> |
| **Imputation** | Fill missing values with<li>default (e.g. empty string `''`)</li> <li>mean, median, mode</li> | Work well in many cases | <li>Filling missing values with possible values makes it hard to distinguish between missing data and valid data with default value</li> <li>Injecting biases and add noises</li> <li>Potential data leakage</li> |

### Scaling
**Feature scaling** - scale feature to similar ranges

- Scale to [0, 1]
- Scale to custom range
- Standardization
- Log transformation (for skewed distribution)

Scaling is a common source of data leakage, and it requires global statistics (e.g. min, max, mean) which might change significantly in the future and hence it is important to retrain frequently.

### Discretization
Rarely help in practice

Discretization (also called quantization or binning) is a process of turning a continuous feature into a discrete feature.

Pro: Supposed to be helpful with limited training data
Con: Introduce discontinuities at the category boundaries, choosing boundaries can be non-trivial

### Encoding Categorical Features
Categories can change (e.g. new brand, new user, which might not be appropriate to classify as `unknown` due to the variety of new objects)

*Hashing trick* - use a hashing function to generate a hashed value of each category, define a hash space which fix the number of encoded values for a feature in advance (e.g. hash space of `2^18 = 262,144` possible hashed values)

Hashed functions can have the problem of collision. The impact is not that bad.

Locality-sensitive hashing function - similar categories are hashed into values close to each other

### Feature Crossing
*Feature Crossing* is the technique to combine two or more features to generate new features. This technique is useful to model the nonlinear relationship between features. 

- It is essential for models that can't learn or bad at learning nonlinear relationship (e.g. linear regression, logistics regression)
- It is less important in neural network, can be helpful to speed up the learning of nonlinear relationship

DeepFM and xDeepFM are the family of models that have successfully leveraged explicit feature interactions for recommender systems and click-through-rate prediction.

Con:
- Can make the feature space blow up
- Might overfit the models

### Discrete and Continuous Positional Embeddings
For model like a transformer, words are processed in parallel, as compared to recurrent neural network. Therefore, words' position need to be explicitly inputted.

Absolute position (e.g. 1, 2, 3, ..., n) does not work, as the number can get very big. Scaling doesn't work, as the numbers can get too small.

Position embeddings can be fixed and pre-defined with function, usually sine and cosine. Fixed positional embedding is a special case known as Fourier features.
![](https://i.imgur.com/Psd4fLr.png)

The embedding size of positional embeddings usually have the same as the embedding size for words so that they can be summed and become the final embeddings of the words.

## Data Leakage
Data leakage refers to the phenomenon when a form of the label "leak" into the set of features used for making predictions, and this same information is not available during inference

This will cause the models to perform well during evaluation but failed to be usable in actual production settings.

Example: serious patient might do MRI with more advanced machine, and hence the model pick up the different of machine instead of the seriousness of the disease

The data leakage might not be obvious

### Reason of leakage
| Reason | Solution |
| -- | -- |
| Splitting time-correlated data randomly instead of by time | Split by time instead of randomly |
| Scaling before splitting | Splitting before scaling |
| Fill in missing data with statistics from the test split | Use only statistics from train split |
| Poor handling of data duplication before splitting | Check for duplicate before sampling, perform oversampling after splitting |
| Group leakage (e.g. patient with 2 CT scans that are a week apart, one of them become test data) | Understand how the data was generated |
| Leakage from data generation process | Understand how the data is collected and processed, normalize data from different sources, incorporate subject matter expert |

Ways to detect data leakage
- Measure predictive power of features or set of features and be skeptical of high correlation
- Do ablation studies to measure how important a feature is
- Keep an eye on new features added to the model
- Be careful with test split and only use it to report a model's final performance

## Engineering Good Features
More features doesn't always mean better model performance.
- More opportunities for data leakage
- More likely to overfit
- Increase memory requirement
- Increase latency
- Useless features become technical debts

2 factors to consider when evaluating whether a feature is good
- **Feature importance** 
  - measured by how much that model’s performance deteriorates if that feature or a set of features containing that feature is removed from the model 
  - E.g. XGBoost build-in feature importance, SHAP(SHapley Additive exPlanations), [InterpretML](https://github.com/interpretml/interpret)
- **Feature generalization** 
  - Two aspects to consider with regards to generalization - *feature coverage* and *distribution of feature values*
    - Feature coverage - percentage of the sample that has values for this feature
    - Distribution of feature values - if the set of value appear in train and test data is inconsistent, it might be a problem


# Chapter 6: Model Development and Offline Evaluation

## Evaluating ML Models
Classical ML algorithms is not going away. 
- Many recommender systems still rely on collaborative filtering and matrix factorization.
- Tree-based algorithms, including gradient-boosted trees, still power many classification tasks with strict latency requirements.

Neural networks and classic ML algorithms can be used in tandem.
- A k-means clustering model might be used to extract features to input into a neural network
- A pretrained neural network (like BERT and GPT-3) might be used to generate embeddings to input into a logistic regression model

When selecting a model for your problem, you don't choose from every possible model out there, but usually focus on a set of models suitable for your problem. Therefore, knowledge of common ML tasks and the typical approaches to solve them is essential in the process.
- Detect toxic tweets (text classification) - naives Bayes, logistic regression, RNN, transformer-based models such as BERT, GPT
- Detect fradulent transactions (classic abnormality detection) - k-nearest neighbors, isolation forest, clustering, and neural networks

When considering what model to use, besides of model's performance (eg: accuracy, F1 score), other properties, such as how much data, compute and time required for training, inference latency and interpretability is also important to consider.


> **_NOTE:_** To understand different algorithms, the best way is to equip yourself with basic ML knowledge and run experiments with the algorithms you're interested in

> **_NOTE:_** To keep up to date with so many new ML techniques and models, the author recommends to monitor trends at major ML conferences such as NeurIPS, ICLR and ICML, as well as following researchers whose work has a high signal-to-noise ratio on Twitter.


### Six tips for Model Selection
1. Avoid the state-of-the-art trap
2. Start with the simplest models
3. Avoid human biases in selecting models
4. Evaluate good performance now versus good performance later
5. Evaluate trade-offs
6. Understand your model's assumptions

**1. Avoid the state-of-the-art trap**
- Researcher usually evaluate models in academic settings, SOTA often means that it performs better on some static datasets.
- It doesn't mean this model will be fast or cheap enough for implementation, or even this model will perform better than other simpler models
- The most important thing to do when solving a problem is finding solutions that can solve that problem

**2. Start with the simplest models**
- Zen of Python - "**simple is better than complex**"
- Easier to deploy, and deploying early **allows you to validate that your prediction pipeline** is consistent with your training pipeline
- Starting with something simple and adding more complex components step-by-step makes it **easier to understand** your model and debug it
- Simplest model serves as a baseline to compare with more complex models
- Example: Bert can be easy to implement due to the community around this solution, but hard to debug

**3. Avoid human biases in selecting models**
- An engineer will likely spend more time experimenting an architecture they are more excited about, which might result in better-performing models for that architecture
- When comparing different architectures, it's important to **compare them under comparable setups**

**4. Evaluate good performance now versus good performance later**
- The best model now does not always mean the best model in the future. For example, tree-based model can be better now, but neural network can outperform when there are more data in the future
- One can use learning curves to get a sense of whether one can expect more performance gain from more training data
- While evaluating models, you might want to **take into account their potential for improvements** in the near future and how easy/difficult it is to achieve those improvements

**5. Evaluate trade-offs**
- Example
  - false positives vs false negative
  - compute requirements vs accuracy
  - interpretability vs performance
- Understanding what is important in the performance of your ML system will help you choose the most suitable model

**6. Understand your model's assumptions**
- "All models are wrong, but some are useful" - George Box
- Understanding whether our data satisfies the assumptions of the model can help us evaluate the model that works best
- Assumptions
  - *Prediction assumption* - Predictive model assume that it is possible to predict Y based on X
  - *Independent and Identically Distributed (IID)* - Neural networks assume that all examples are independently drawn from the same joint distribution
  - *Smoothness* - Supervised machine learning method assumes that there is a smooth function to transform input to output
  - *Tractability* - Generative model assumes that it's tractable to compute the probability `P(Z|X)`, where `Z` is the latent representation of `X`
  - *Boundaries* - A linear classifier assumes that the decision boundaries are linear
  - *Conditional independence* - A naive Bayes classifier assumes that the attribute values are independent of each other given the class
  - *Normal distributed* 

### Ensembles
- Use an emsemble of multiple models instead of just an individual model to make prediction. Each model in the ensemble is called a *base learner*
- High rate of winning solution in Kaggle and [SQuAD 2.0](https://rajpurkar.github.io/SQuAD-explorer/explore/v2.0/dev/)
- More complex to deploy and hard to maintain, hence less favored in production
- When creating an ensemble, the less correlation there is among base learners, the better the ensemble will be. (eg: one transformer model, one RNN, one gradient-boosted tree)
- Type of ensembles
  - Bagging (bootstrap aggregating)  
    Given a dataset, sample with replacement to create different datasets (called bootstrap), and train a classification or regression model on each of these bootstraps. (e.g. Random Forest)
  - Boosting  
    Boosting is a family of iterative ensemble algorithms that convert weak learners to strong ones. The samples are weighted differently among iterations, where future weak learners focus more on the misclassified examples. (eg: GBM - XGBoost, LightGBM)
  - Stacking  
    Create a meta-learner that combines the outputs of the base learners to output final predictions

[Ensemble guide](https://github.com/MLWave/Kaggle-Ensemble-Guide) by Kaggle legendary's team, MLWave

## Experiment Tracking and Versioning
During the model development process, you often have to **experiment with many architectures and many different models**. It is important to keep track of all the definition needed to re-create an experiment and its relevant artifacts. An **artifact** is a file generated during an experiment (eg: loss curve, logs graph, intermediate results).

This enables you to compare different experiments and choose the best suited one. It helps the understanding of how small changes affect model's performance, and give more visibility into how your model works.

The process of tracking the progress and results of an experiment is called **experiment tracking**. The process of logging all the details of an experiment is called **versioning**.

Experiment Tracking Tools: MLFlow, Weights & Biases  
Versioning Tools: DVC

### Experiment Tracking
It is important to track what's going on during training, not only to detect and address these issues, but also to evaluate whether the model is learning anything useful (e.g. loss not decreasing, overfitting, underfitting, dead neuron, fluctuating weight values, running out of memory).

Things to track:
- Loss curve corresponding to train and eval splits
- Model performance metrics (eg: accuracy, F1 score)
- Log of corresponding sample, prediction and ground truth label
- The speed
- System performance metrics (eg: RAM, CPU/GPU utilization)
- Parameter and hyperparameter

Tracking gives you observability into the state of the model, especially when something happens.

Example: Automatically make copies of all the code files needed for an experiment, log all outputs with their timestamp

### Versioning
ML systems are part code, part data, so both need to be versioned.

Challenge of data versioning:
- Data is often larger than code, we can't use the same strategy to version data
- A line in data can be indefinitely long, especially if it's stored in a binary format. Specifying a diff can be not helpful
- Dataset can be so large than duplicating it multiple times across different versions might be unfeasible
- A dataset might not fit into a local machine
- Definition of a diff is unclear when versioning data (checksum, existence of file)
- Resolving merge conflicts can be challenging 
- Privacy law such as General Data Protection Regulation (GDPR) might make it legally impossible to recover older version of data

As of 2021, data versioning tools like DVC only register a diff if the checksum of the total directory has changed and if a file is removed or added.

Aggressive tracking and versioning helps with reproducibility, but it doesn't ensure reproducibility. The framework and hardware might introduce nondeterminism to the experiment results.

## Debugging  ML Models
Challengs of debugging ML models
- ML models fails silently
- Difficulty in validating whether a bug has been fixed
- Cross-functional complexity (data, labels, algorithm, code, infrastructure), which might be owned by different teams

Reasons that an ML model can fail:
- Theoretical constraints (e.g. linear regression might fail when the decision boundaries aren't linear)
- Poor implementation of model (e.g. forgot to stop gradient updates when running evaluation)
- Poor choice of parameters
- Data problems (e.g. noisy labels, outdated statistic when performing normalization)
- Poor choice of features (e.g. data leakage)

Tried-and-true debugging techniques by experienced ML engineers (from [A Recipe for Training Neural Network](http://karpathy.github.io/2019/04/25/recipe/))
- **Start simple and gradually add more components** -If you want to use a BERT-like model, which use both a masked language model (MLM) and next sentence prediction (NSP) loss, you might want to use only the MLM loss before adding NLS loss
- **Overfit a single branch** - Try to overfit a small amount of data. If it can't overfit, there might be something wrong with the implementation
- **Set a random seed** - to ensure consistency between different runs and allows reproducibility

## Distributed Training
It's common to train a model using data that doesn't fit into memory (e.g. medical data, large-language models)

Expertise in scalability is hard to acquire because it requires having regular access to massive compute resources.

There are different scenarios
- Full data doesn't fit into memory
- Single data sample doesn't fit into memory

When the data doesn't fit into memory, the algorithm of preprocessing (e.g. zero centering, normalizing, whitening), shuffling, batching data need to run out of core and in parallel. Gradient checkpoint can be used when a single data sample can't fit into memory.

### Data Parallelism
Data parallelism is a method to split data on multiple machines, train the model on all of them and accumulate gradients.

Ways of accumulating gradients from different machines
- Synchronous stochastic gradient descent (SGD) - models wait for all of the machines to finish a run
- Asynchronous stochastic gradient descent - models update the weight using the gradient from each machine separately

Synchronous SGD might face problems with straggler (machine that is slow, possibly due to low computing power), which cause the entire system to slow down. There have been algorithms that effectively address this problem.

Asynchronous SGD might face problems of gradient staleness because the gradients from one machine have caused the weights to change before the gradients from another machine have come in.

In theory, asychronous SDG requires more steps to converge. In practice, when the number of weight is large, gradient updates are sparse which means most gradients updates does not update the same weight. In that case, gradient staleness becomes less of a problem and model converges similarly for both synchronous and asynchronous SGD.

A problem of data parallelism is that spreading the model on multiple machines can cause the batch size to be very big (e.g. 1 machine 1,000 batches -> 1,000 machines 1 million batches). In practice, increasing batch size past a certain point yields diminishing returns. An intuitive way is to increase learning rate, but big learning rate might lead to unstable convergence.

Another potential problem is that the main worker might uses a lot more resources, hence need to figure out a way to balance out the workload for better machine utilization

### Model Parallelism
Model parallelism is when different components of the models are trained on different machine (e.g. machine 0 handles first 2 layers while machine 1 handles the next 2 layers, some machines handle forward pass while others handle backward pass)

*Pipeline parallelism* is a clever technique to make different components of a model on different machines run more in parallel. For example, breaking a mini-batch to 4 micro-batches and run it on 4 machines. After machine 1 compute the first layer on the first micro-batch, machine 2 compute the second layer on the first micro-batch while machine 1 compute the first layer on the second micro-batch.


## AutoML
AutoML refers to automating the process of finding ML algorithms to solve real world problems.

### Soft AutoML: Hyperparameter Tuning
A hyperparameter is a parameter supplied by users whose value is used to control the learning process (e.g. learning rate, batch size, number of hidden layers, dropout probability, quantization)

A model can give drastically different performances with different sets of hyperparameters.

Despite the importance of hyperparameter tuning, many still ignore systematic approaches to hyperparameter tuning and perform manual, gut-feeling approach (e.g. Graduate Student Descent, a technique which graduate student fiddles around with the hyperparameters until the model works)

Many popular frameworks come with built-in utilities or having third-party capabilities for hyperparameter tuning
- Scikit-learn - auto-sklearn
- Tensorflow - Keras Tuner
- Ray - Tune

Methods of hyperparameter tuning
- Random search
- Grid search
- Bayesian optimization

Model's performance might be more sensitive to some hyperparameters, which should be more carefully tuned.

Relevant book: [AutoML: Methods, Systems, Challenges](https://www.automl.org/book/)

### Hard AutoML: Architecture Search and Learned Optimizer
Architecture search or neural architecture search (NAS) for neural network, treat components of the model or the entire model as hyperparameter (e.g. size of convolution layer, existence of skip layer, existence of pooling layer). The set of building blocks varies based on the base architecture (e.g. CNN vs transformers)

NAS setup consists of three components
- *A search space* (define possible model architectures)
- *A performance estimation strategy* (without training each candidate architecture until convergence as it is expensive)
- *A search strategy* (random search can still be expensive, common approaches include reinforcement learning and evolution)
  - Reinforcement learning - rewarding the choices that improve the performance estimation
  - Evolution - Adding mutations to an architecture, choosing the best performance one, adding mutations to them, and so on

In a typical ML training process, you have a model and a learning process (e.g. gradient descent). An optimizer specify how to update a model's weights given gradient updates.

Optimizers can be sensitive to the setting of the hyperparameters, and the default hyperparameters don't often work well across architectures.

A way to tackle this is to train optimizer instead of using hand-designed optimizer.

Training optimizer for every task can be redundant. Another approach is to train it once on a set of existing tasks, and use it for every task after that, this makes use of aggregated loss on the existing tasks as the loss function, and existing designed optimizers as the learning rule. The learned model can then be used to train a better-learned optimizer.

Training AutoML is expensive.

EfficientNets, a family of models produced by Google's AutoML team, surpassed SOTA with up to 10x efficiency.

## 4 Phases of ML Model Development
1. Before machine learning (e.g. simple heuristics)
2. Simplest machine learning models (e.g. Logistic regression, k-nearest neighbors, gradient-boosted tree)
3. Optimizing simple models
4. Complex models (once reached the limit of simple models and the use case demands significant model improvement)

> You might even find non-ML solutions work fine and you don't need ML yet

## Model Offline Evaluation
"How can I know that our ML models are any good?"  

Lacking a clear understanding of how to evaluate ML systems can limit your ability to find the best solution for your need, and make it harder to convince your managers to adopt ML.

Ideally, the evaluation methods should be the same during both development and production. However, it is usually impossible as you don't have ground truth labels in production.

For tasks with natural labels, this might work. For others, one might have to rely on extensive monitoring to detect changes and failures in the ML system's performance.

### Baselines
Evaluation metrics, by themselves, mean little. It is essential to know the baseline you are evaluating against.

The five baseline that might be useful across use cases
- **Random baseline** (e.g. prediction generated using uniform distribution or task's label distribution)
- **Simple heuristic** (e.g. rank newsfeed in reverse chronological order, to optimize user time spend)
- **Zero rule baseline** (heuristics where the baseline model always predicts the most common class)
- **Human baseline** (ML can be designed to automate what would have been otherwise done by human, hence it's useful to know how the model perform compared to human experts, e.g. self-driving system)
- **Existing solutions** (ML can be designed to replaced existing solutions, hence it is crucial to compare the performances)

### Evaluation Methods
- **Pertubation tests** - Make small changes to test splits (e.g. add background noise or randomly clip the audio clips to simulate variance of real-world data) to see how they affects the model's performance, make the model more resilient
- **Invariance tests** - Keep the inputs same but change the sensitive information (e.g. race) to see if the output change, to detect biases
- **Directional expectation tests** - Certain changes in the inputs should cause predictable changes in outputs (e.g. increasing lot size should increase housing price). Investigate if the model learns in the opposite direction
- **Model calibration** - Imagine that a prediction state that a watcher has a watching habits of 80% romance and 20% comedy, a calibrated system will have recommendations that are more representative of user's actual watching habits, instead of only romance movies (techniques: `sklearn.calibration.calibration_curve`, platt scaling)
- **Confidence measurement** - While most metrics measure the system's performance on average, confidence measurement is a metric for each individual sample. Can be a way to think about the usefulness threshold for each individual prediction
- **Slice-based evaluation** - separate data into subsets (e.g. majority group and minority group) and looks at model's performance on each subset separately. Can help to detect biases and improve model's performance both overall and on critical data, and improve confidence of model performance in a more fine-grained way
  - **Heuristics-based** - Slice data using domain knowledge
  - **Error analysis** - Manually go through misclassified examples and find patterns among them
  - **Slice finder** - Generating slice candidates with algorithms such as beam search, clustering or decision, then pruning out clearly bad candidates for slices, and then rank the candidates that are left

Problem on focusing on overall metrics
- Model might perform differently on different slices of data when the model should perform the same (e.g. lower accuracy in minority group despite higher overall accuracy)
- Model might perform the same in different slices of data when the model should perform differently (e.g. paid vs unpaid users will have different churn rates)

Simpson's paradox - a phenomenon in which a trend appears in several groups of data but disappears or reverses when the groups are combined


# Chapter 7: Model Deployment and Prediction Service
Production is a spectrum

A quote from Internet - Deploying is easy if you ignore all the hard parts

Hard parts of deployment
- Make your model available to millions of users with a latency of milliseconds and 99% uptime
- Setting up the infrastructure so that the right person can be immediately notified when something goes wrong
- Figure out what went wrong
- Seamlessly deploy the updates to fix what's wrong

Serialization - converting a model (model definition and model's parameter values) into a format that can be used by another application (e.g. tensorflow uses `tf.keras.Model.save()`, PyTorch uses `torch.onnx.export()`)

| Myth | Truth |
| -- | -- |
| You only deploy one or two ML models at a time | Companies can have many ML models (e.g. Uber has models for ride demand, driver availability, estimated time for arrival, dynamic pricing, customer churn, etc) |
| If we don't do anything, model performance remains the same | Software program degrades over time - software rot, bit rot; ML systems - data distribution shifts |
| You won't need to update your models as much | "How often ~~should~~ can I update my models" is the correct question. ML should learn from DevOps practices. Companies like Weibo, Tik Tok have iteration cycle for updating some of the ML models in 10 minutes |
| Most ML engineers don't need to worry about scale | Most tech people works in company which likely serving a reasonable number of users |


## Batch Prediction vs Online Prediction
*Online prediction* (or *on-demand prediction*, *synchronous prediction*) is when predictions are generated and returned as soon as requests for these predictions arrive (e.g. Google Translate). Traditionally, it is done through RESTful APIs 

*Batch prediction* (or *asynchronous prediction*) is when predictions are generated periodically or whenever triggered (e.g. Netflix's movie recommendations for all of its users every few hours). The predictions are stored somewhere, and retrieved as needed

Three main mode of predictions
- Batch prediction that uses batch features
- Online prediction that uses batch features (e.g. precomputed embedding)
- Online prediction that uses batch features and streaming features (*streaming prediction*)

Example - an order of DoorDash food delivery require batch features (restaurant mean preparation time) and streaming features (available delivery people, number of existing orders)

It might be helpful to combine different types of prediction. E.g. precompute predictions for popular or larger queries, generate predictions online for less popular or smaller queries

|  | Batch prediction (asynchronous) | Online prediction (synchronous) |
| -- | -- | -- |
| Frequency | Periodical, such as every four hours | As soon as requests come |
| Useful for | Processing accumulated data when you don't need immediate results (such as recommender systems) | When predictions are needed as soon as a data sample is generated (such as fraud detection) |
| Optimized for | High throughput | Low latency |

Other examples of online prediction - high frequency trading, autonomous vehicles, voice assistants, fingerprint unlocking, fall detection of elderly, fraud detection

Requirements for online predictions
- A (near) real-time pipeline that can work with incoming data -> extract streaming features (if needed) -> input features into model -> return prediction (e.g. a streaming pipeline with real-time transport and a stream computation engine)
- A model with acceptable speed of prediction

Example of unifying batch pipeline and streaming pipeline - Google Map 
- Training using last month data
- Continuously update prediction as users' trip progress, using features such as average speed of all cars

Unifying batch pipeline and streaming pipeline might be a common cause of bugs

Some companies made major infrastructure overhauls by using a stream processor like Apache Flink. Some use feature store to ensure the feature consistency

## Model Compression
3 ways to reduce inference latency
- *Inference Optimization* - Make the model does inference faster
- ***Model Compression* - Make the model smaller**
- Make the hardware it's deployed on run faster

Useful link: [Awesome open source](https://awesomeopensource.com/projects/model-compression)

Techniques ([survey](https://arxiv.org/abs/1710.09282))
- Low-rank optimization
- Knowledge distillation
- Pruning
- Quantization

### Low-Rank Factorization
Replace high-dimensional tensors with lower-dimensional tensors.

Type
- *Compact convolutional filters* - replace over-parameterized convolutional filters with compact blocks
  - Example: SqueezeNet uses a number of strategies, including replacing *3 x 3* convolution with *1 x 1* convolution, which achieves AlexNet-level accuracy on ImageNet with 50 times fewer parameters
- MobileNets decomposes the standard convolution of size *K x K x C* into a depthwise convolution (*K x K x 1*) and a pointwise convolution (*1 x 1 x C*), *K* is kernel size and *C* is number of channels

Low-rank factorization tends to be specific to certain type of models and requires a lot of architectural knowledge to design, so it is not widely applicable

### Knowledge Distillation
A method in which a small model (student) is trained to mimic a larger model or ensemble of models (teacher)

Example: DistilBERT which reduces the size of BERT model by 40% and being 60% faster, while retaining 97% of its language understanding capabilities

Example design: Random forest as student and a transformer as the teacher

Knowledge distillation tends to be highly dependent on the availability of a teacher network (easier for pretrained model as teacher, hard if teached model doesn't available). It is also sensitive to applications and model architecture, hence hasn't found wide usage in production.

### Pruning
Pruning is originally used for decision tree where uncritical/redundant sections of a tree are removed

Pruning, in the context of neural networks, has 2 meanings
- Remove entire node of a neural network
- (more common) Find parameters least useful to predictions and set them to 0. This doesn't reduce the number of parameters. It helps with reducing the size by making a neural network more sparse

Experiments show that the count of nonzero parameters can be reduced by 90% without compromising overall accuracy

There are also idea of using the pruned architecture and retrain a dense model from scratch.

### Quantization
Quantization reduces a model's size by using fewer bits to represent its parameter. It is the most general and commonly used model compression method as it is straight-forward to do and generalize.

Example: Using 16 bits (*half precision*) or integer (8 bits, method known as *fixed point*) to represent a float

Extreme example: Using 1-bit representation (binary weight neural networks), such as BinaryConnect and XNOR-Net

Pro
- Reduce memory footprint
- Improve computation speed (increase batch size, reduce training time and inference latency)

Con
- Represent a smaller range of values
- Rounding number leads to rounding errors, risk rounding the number to under-/overflow and rendering it to 0

Low-precision training has become increasingly popular
- NVIDIA introduces Tensor Cores, processing units that support mixed-precision training
- Google TPUs (tensor processing units) support training with Bfloat16 (16-bit Brain Floating Point Format) which Google dubbed "the secret to high performance on Cloud TPUs"

Training in fixed-point is not yet as popular, but has had a lot of promising results. Fixed-point inference has become a standard in the industry. 

Most popular frameworks for on-device ML inference offer post-training quantization for free with a few lines of code
- Google's Tensorflow Lite
- Facebook's PyTorch Mobile
- NVIDIA's TensorRT

## ML on the Cloud and on the Edge
On the cloud means a large chunk of computation is done on the cloud, on the edge means a large chunk of computation is done on consumer devices

On the cloud is more straight-forward to deploy. Downside includes 
- high cloud costs
- need for reliable network to send the data to the cloud and back
- network latency

On the edge helps to mitigate the risks, by 
- reducing computation on the cloud which reduce cloud bills
- working where there are no internet connection or the connections are unreliable
- avoid sending data through network

On the edge might also be helpful for handling sensitive data and complying with regulations such as GDPR.

However, on the edge requires the edge devices to be powerful enough to handle the computation. (e.g. running BERT will quickly drain the battery)

There is a race of developing edge devices optimized for different ML use cases.
- Google, Apple, Tesla making their own chips
- ML hardware start-ups that raised billions to develop better AI chips

### Edge Devices
Different hardware backends have different memory layouts and compute primitives.

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781098107956/files/assets/dmls_0711.png)

The compute primitives of different hardware backends
- CPU - number (scalar)
- GPU - One-dimensional vector
- TPU - Two-dimensional vector

Therefore, performing a operator (e.g. convolution operator) will be very different with different hardware backends. There are also different L1, L2, L3 layouts and buffer size which need to be taken into account to use them efficiently. Hence, providing support for a framework on a hardware backend is time-consuming and engineering-intensive.

For example, TPUs were released in February 2018, but only started supporting PyTorch in September 2020.

Intermediate representation (IR) is a middleman to bridge the platform and the frameworks. With that, framework developers only need to translate their framework code into this middleman, hardware vendors can then support one middleman instead of multiple frameworks.

Compilers generate a series of high- and low-level IRs before generating the code native to a hardware backend. The generation of IRs is also called lowering (lower high-level framework code into low-level hardware-native code)

#### Optimize Model for Edge Device
A few reasons that models are slow in the hardware
- The generated code not taking advantage of data locality and hardware caches, or advanced features such as vector or parallel operations
- No optimization across frameworks (e.g. pandas, tensorflow, LightGBM), although individual function in the framework might be optimized

Expensive solution: Hire optimization engineers to optimize the models for the hardware (e.g. develop quantization and robustness AI retraining tools, develop compiler features, develop neural network optimized for hardware)

Optimizing compilers (compilers that optimize the code) is an alternative solution, as they can automate the process of optimizing models when lowering ML code into machine code (convolution, loops, cross-entropy).

Local optimization techniques (run in parallel or reduce memory on chips)
- *Vectorization* - execute multiple elements contagious in memory at the same time
- *Parallelization* - Divide an array into independent chunks and process them individually
- *Loop tiling* - Change data access order in a loop based on hardware, to leverage hardware's memory or cache
- *Operation fusion* - Fuse multiple operators into one to avoid redundant memory access (e.g. horizaontal and vertical fusion of the computation graph of convolutional neural network)

![Operation fusion](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781098107956/files/assets/dmls_0714.png)
Vertical and horizontal fusion of the computation graph of a convolution neural network

#### Manual vs Using ML to Optimize ML
There are many possible ways to execute a given computation graph. Traditionally, optimization engineers come up with heuristics based on their experience (e.g. engineers focus exclusively on speeding up ResNet-50 on DGX 100 server)

A few drawbacks of heuristics optimization
- Most likely is nonoptimal
- Nonadaptive, and require enormous amount of efforts for each new frameworks and hardwares
- Dependent on operations (e.g. optimization of transformer, RNN, CNN are different)

ML is good at approximating the solution to intractable problems. It can be used to narrow down the search space for executing a computation graph.

Example of optimizing the execution of computation graph
- For PyTorch on GPUs, there is `torch.backends.cudnn.benchmark=True`, which enable cuDNN autotune, which search over a predetermined set of options to execute a convolution operator and choose the fastest way (only work for convolution operators)
- [autoTVM](https://tvm.apache.org/docs/reference/api/python/autotvm.html) which works with subgraphs

ML-powered compilers can be slow and take hours or even days to perform optimization. This optimization is ideal when there is a model ready for production and target hardware to run inference on. The result can be cached and used to both optimize existing model and provide a starting point for future tuning sessions.

#### ML in Browsers
Running ML in browsers avoid the hardware compatibility issues. However, it can be slow.

Approach
- Compile model into Javascript (Tensorflow.js, Synaptic, brain.js)
- Compile model to WebAssembly (WASM)

WASM is more performant than Javascript, and it is widely. However, running models in browser using WASM is still slower comparing to running in native applications


# Chapter 8: Data Distribution Shifts and Monitoring
## System Failures
A failure happens when one or more expectations of the system is violated.

In traditional software, we care about operational metric (e.g. latency and throughput)\
In ML system, we care about both operational metrics and its ML performance metrics (e.g. accuracy)

Operational expectation violations are easier to detect, as they're usually accompanies by an operational breakage (e.g. timeout, 404 error, out-of-memory error, segmentation fault)\
ML performance expectation violations are harder to detect, as they required measuring and monitoring the performance of ML models in production

### Software System Failures
Software system failures are failures that would have happened to non-ML systems.
- *Dependency failure* - A software package or codebase that your system depends on break
- *Deployment failure* - Failure caused by deployment errors (e.g. deploy wrong version of model, insufficient permission)
- *Hardware failure* - Hardware used to deploy the model doesn't behave the way it should (e.g. overheat and break down)
- *Downtime or crashing* - Server (e.g. AWS, hosted service) is down

Addressing software system failures require not ML skills, but traditional software engineering skills

ML engineers at Google found that 60 out of 96 failures happened due to causes not directly related to ML, and usually related to distribution systems (e.g. workflow scheduler, orchestrator, data pipeline)

### ML-Specific Failures
ML-specific failures are failures specific to ML systems.
- Data collection and processing (discussed in Chapter 4)
- Poor hyperparameters (discussed in Chapter 6)
- Change in the training pipeline not correctly replicated in the inference pipeline and vice versa (discussed in Chapter 7)
- Data distribution shifts - production data differing from training data
- Edge cases - data samples so extreme that they might cause the model to make catastrophic mistakes, different with outliers
- Degenerate feedback loops

#### Degenerate Feedback Loops
A *degenerate feedback loop* can happen when the predictions themselves influence the feedback, which in turn, influences the next iteration of the model (e.g. a system that recommend songs to users might rank the recommended songs higher, which make users click on initial predictions more). This is named "exposure bias", "popularity bias", "filter bubbles", "echo chambers". Another example is resume screening, recruiters only interview people whose resumes are recommended by the model, and form a bias data for the model.

Ways to detect degenerate feedback loops
- Measure popularity diversity of a system's output using metrics such as *aggregate diversity* and *average coverage of long-tail items*
- Measurement of hit rate against popularity
  - Divide items into bucket based on their popularity
  - Measure the prediction accuracy for each bucket
  - Check if the recommender system is better at recommending popular items

Ways to correct degenerate feedback loops
- Randomization - instead of showing only the items that the system reanked highly, show users random items and use their feedbacks to determine the true quality of these items (e.g. TikTok). Con is that it is at the cost of user experience
- Positional features - Add positions as a feature to account for its affect during training, set position as the same across sample during inference
  - More sophisticated approach - 2 models
    - First model predicts the probability of user see and consider a recommendation based on position
    - Second model predicts the probability that the user clicks on the item

## Data Distribution Shift
*Data distribution shift* refers to the phenomenon in supervised learning when the data a model works with change over time, which causes this model's prediction to become less accurate as time passes.

Source distribution vs target distribution (distribution of the data of the model)

The test data we use to evaluate a model during development is supposed to represent unseen data, and the model's performance on the test data is supposed to give us an idea of how well the model will generalize

The assumption for the training data and the unseen data to come from a stationary distribution that is the same, is usually incorrect in the real world.
- The underlying distribution of the real-world data is unlikely to be the same as the underlying distribution of the training data. Real world data is multifaceted and virtually infinite. This divergence between training and real world leads to common failure mode known as *train-serving skew*
- The real world isn't stationary, things change (e.g. searching for Wuhan when covid happen was different than before, season change)

A lot of what might looks like data shifts might be caused by internal error, such as mishandled of data, feature, deployed model version

### Type of Data Distribution Shifts
Input as X and output as Y
| Type | Definition | Example | Remark |
| -- | -- | -- | -- |
| *Concept drift* (also known as *posterior drift*) | When *P(Y\|X)* changes but *P(X)* remains the same | Housing price before and during COVID pandemic have the same distribution of houses feature, but different pricing distribution |
| *Covariate drift* | When *P(X)* changes but *P(Y\|X)* remains the same | Training data of breast cancer prediction which consist more female above 40, while inference data does not, but given the age, the probability of breast cancer should be the same | Can be caused by sample selection problem or artificial altered data or model learning process (e.g. active learning). If real-world input distribution is known, one can leverage importance weighting to train the model to work for real-world data |
| *Occasionally label shift* (also known as *prior drift*, *prior probability shift*, or *target shift*) | When *P(Y)* changes but *P(X\|Y)* remains the same | Randomly select person with breast cancer in training data (with more women above 40) and test data respectively, both have the same probability of being over 40 | When the input distribution changes, the output distributions also changes, result in both covariate shift and label shift |

> A covariate is an independent variable that can influence the outcome of a given statistical trial but is not of direct interest.

General data distribution shifts
- *Feature change* - When new features added, older features removed, or the set of all potential values of a feature changes (e.g. feature age change from year to month)
- *Label schema change* - When the set of possible values for Y change (e.g. extra class, regression with new range)

### Detecting Data Distribution Shifts
Data distribution shifts is only a problem if they cause your model's performance to degrade.

Ways to detect data distribution shifts
1. Monitor model's accuracy-related metrics (e.g. accuracy, F1 score, recall, AUC-ROC, etc)
   - Using ground truth if it is possible
   - Monitor other distribution of interest (e.g. input distribution `P(X)`, label distribution `P(Y)`, conditional distribution `P(X|Y)` and `P(Y|X)`)
> In the industry, most drift detection method focus on detecting changes in the input distribution
2. Statistical method
   - Compare statistics such as min, max, mean, variance, various quantiles (such as 5th, 25th, 75th, 95th), skewness, kurtosis, etc
     - [Tensorflow Extended's built-in data validation tools](https://www.tensorflow.org/tfx/data_validation/get_started). 
     - Might not be sufficient
   - Two-sample hypothesis test (two-sample test) - determine whether the difference between two population is statistically significant (difference detected with small sample is a more powerful indicator)
     - Example: 
       - Kolmogorov–Smirnov test (K-S or KS test) - non-parametric test that can work with any distribution, but can only used for one-dimensional data
       - Least-Squares Density Difference - an algorithm based on the least-squares dentsty difference estimation method
       - Maximum Mean Discrepancy (MMD) - a kernel-based technique for multivariate two-sample testing
       - Learned Kernel MMD
     - Example implementation - [Alibi Detect](https://github.com/SeldonIO/alibi-detect)
     - It is recommended to perform dimension reduction before performing a two-sample test on it
3. Time scale windows for detecting shifts
   - A common approach to detect shift that happen over time is to treat input data to ML applications as time-series data
   - The time scale window of data we look at affect the shift we can detect. Detecting temporal shifts is hard when shifts are confounded by seasonal variation
   - Difference betwen *cumulative* and *sliding statistics*. Sliding statistics are computed within a single time slide window (e.g. an hour). Cumulative statistics are continually updated with more data
   - Working with data in temporal space require knowledge of time-series analysis techniques such as time-series composition
   - Current solution
     - Company use distribution of training data as base and monitor production data distribution at a certain granularity (e.g. hourly, daily). The shorter the time frame, the faster the detection, but might have more false positive
     - Platforms dealing with real-time data analysis provide merge operation that merges statistics from shorter time scale windows to create statistics for larger time series windows
     - More advanced monitoring platforms provide *root cause analysis (RCA)* that analyze and detect exactly the time windows where a change in data happened

> Spatial shifts are shifts that happen across access point (e.g. application getting a new group of users). Temporal shifts are shifts that happen over time.
> Abrupt changes are easier to detect than slow, gradual change

### Addressing Data Distribution Shifts
Different companies have different capabilities and priorities when it comes to handling data distribtuion shifts

Three main approaches
1. Train models using massive datasets, hoping that training dataset is large enough to learn a comprehensive distribution, and whatever data points encountered in production come from this distribution
2. Adapt a trained model to a target distribution without requiring new labels 
   - Use causal interpretations together with kernel embeddings of conditional and marginal distributions to correct models' predictions for both covariate shifts and label shifts without using label from the target distribution
   - Use domain-invariant representation learning, an unsupervised domain adaptation technique that can learn data representations invariant to changing distributions
3. Retrain your model using the labeled data from the target distribution
   - Considerations
     1. Train from scratch (stateless training) or continue training from the last checkpoint (stateful training)
     2. What data to use (e.g. data from last 24 hours,3 months, or from the point when data has started to droft)
   - Other terms: domain adaptation and transfer learning
     - Domain adaptation - Adapt current model/distribution (domain) to new distribution
     - Transfer learning - Adapt a model trained on one joint distribution to another joint distribution
   - Design your system to be robust to shift
     - Consider the trade-off between performance and stability, a feature can be good for accuracy but deteriorate quickly
     - Example: To predict whether a user will download an app, app ranking is used as a feature. App ranking can change quickly, you might want to instead bucket them into top 10, between 11 to 100, and so on, which has less power but more stability
   - Design your system to be adaptive to shift
     - Example: Housing price in major cities change faster than rural cities and require more frequent update. If you use one model, you need to update the model at the more frequent rate using data from both markets. Using separate model allow you to update each of them only when necessary

Performanc degradation of models in production might be caused by huamn errors. It can be hard to identify what causes a data distribution shifts.


## Monitoring and Observability
**Monitoring** referes to the act of tracking, measuring and logging different metrics that can help to determine when something goes wrong.

**Observability** means setting up our system in a way that gives us visibility into our system to help us investigate what went wrong. Observability is part of monitoring

**Instrumentation** is the process of setting up our system for observability (e.g. adding timers to functions, counting NaNs in features, tracking how inputs are transformed, logging unusual events)

ML systems are software systems, the first class of metrics to monitor are the operational metrics, which convey the health of the system. They are generally divided to three levels - network, machine, application

Operational metrics
- Latency and throughput
- Number of prediction requests in the last minute, hour, day
- Percentage of requests returning 2xx code
- CPU/GPU and memory utilization

Example: 
Measuring *availability* - how often the system is available to offer reasonable performance to users \
Metric: *uptime* - percentage of time a system is up

> The condition to determine whether a system is up are defined in the service level objectives (SLOs) or service level agreements (SLAs). For example, an SLA may specify that the service is considered to be up if it has a median latency of less than 200 ms and a 99th percentile under 2s.
> A service provider might offer an SLA that specifies their uptime guarantee, such as 99.99% of the time, and if this guarantee is not met, they'll give their customers back money.

ML-specific metrics
- Model's accuracy-related metrics
  - Example: user feedback such as click, purchase, upvode, downvote, favourite, bookmark, share, etc
  - Application can be engineered to collect user feedbacks
  - Some feedback can be used to infer natural labels, or detect changes in performance (e.g. duration of time users spent on recommended video)
- Predictions
  - Low dimensional, easy to visualize and compute two-sample tests
  - Acts as proxy for input distribution shifts
- Features
  - Feature monitoring is the focus of ML monitoring solutions in the industry
  - Features include the intermediate and final features, they are well structured and follow predefined schema
  - *Feature validation* (sometimes known as *table testing*, *table validation*, *unit tests for data*) - ensure that the features follow an expected schema (expected schemas are generated from training data or from common sense)
    - If the min, max or median of a feature are within an acceptable range
    - If the values of a feature satisfy a regular expression format
    - If all the values of a feature belong to a predefined set
    - If the values of a feature are always greater than the values of another features
  - Tools: [Great Expectations](https://github.com/great-expectations/great_expectations), [Deequ](https://github.com/awslabs/deequ)
  - Two-sample tests to detect whether the underlying distribution of a feature or a set of features has shifted
- Raw inputs
  - Raw data from different sources might have different formats
  - Raw data is usually managed by other teams, such as data platforms team

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781098107956/files/assets/dmls_0805.png)

Major concerns when doing feature monitoring
- **Have many models in production, and each model uses many features** - monitoring can be expensive and increase system latency
- **Tracking features is useful for debugging, but not very useful for detecting model performance degradation** - Feature distributions shifts all the time, and most changes are benign. If most drift alert is false negative, it can cause "alert fatigue" where the monitoring team stops paying attention to the alerts because they are so frequent
- **Feature extraction is often done in multiple steps** - it can be hard to detect the cause of the drift
- **Schema that your feature follow can change over time**

### Monitoring Toolboxs
Measuring, tracking and interpreting metrics for complex system is a nontrivial task, and engineers rely on a set of tools to help them do so.

Terms
- Logs - record events produced at runtime
- Events - anything that can be of interest to the system developers, either at the time the event happens or later for debugging and analysis
- Traces - a form of logs
- Metrics - computed from logs
- Dashboard
- Alert

Example of events
- When a container starts
- The amount of memory it takes
- When a function is called and finished running
- Other functions that the functions called
- Input and output of a function
- Crashes, stack traces, error codes

#### Log
The number of logs can grow very large very quickly (e.g. billions per day). Today, a system might consists of many different components: containers, schedulers, microservices, polyglot persistence, mesh routing, ephemeral auto-scaling instances. It can be hard to detect where the problem is.

*Distributed tracing* is a method of monitoring and observing service requests in applications built on a microservice architecture.
- Give each process a unique ID
- Record all the metadata related with each event (e.g. the time it happens, the service where it happens, the function that is called)

Many companies use ML to analyze log
- Anomaly detection
- Classify each event in terms of its priorities such as usual, abnormal, exception, error, and fatal
- Predict the probability of related services being affected when a service fauls

Logs are usually processed in batches - efficient, but problems can only be discovered periodically

#### Dashboard
Dashboard can be used to visualize metrics, and make monitoring accessible to non-engineers. Interpreting graphs require experience and statistical knowledge

> Dashboard rot - Excessive metrics on dashboard that become counterintuitive

It is important to pick the right metrics and abstract out lower-level metrics

#### Alert
Alert consists of three components
- *An alert policy* - condition for an alert (e.g. accuracy < 90%)
- *Notification channels* - who to be notified (e.g. slack channel, PagerDuty, email address)
- *Description of the alert* - to help alerted person with understanding alert (e.g. provide mitigation instructions or runbook)

Avoid alert fatigure
- Nobody likes to be awakened at night for something outside of their responsibilities
- Trivial alerts might desensitive people to critical alerts

### Observability
Observability is about instrumenting your system in a way to ensure that sufficient information about a system's runtime is collected and analyzed
- Allows figuring out what went wrong by logs and metrics, without having to ship code to the system
- Allows more fine-grain metrics, on top of detection of model's performance degrade
  - Example: outliers in the last 10 minutes, all the users which receive wrong prediction, intermediate output
  - Require to log system's output using tag and other identifying keywords
- Observability also encompasses interpretability, to help understand how the entire Ml system, including ML models, works (e.g. ability to identify features that contribute to wrong predictions in the last hour)

> Telemetry - A system's outputs collected at runtime. In the monitoring context, it refers to logs and metrics collected from remote components (e.g. cloud services, applications run on customer devices)

Monitoring is passive


# Chapter 9: Continual Learning and Test in Production
How do we adapt our models to data distribution shifts? The answer is by continually updating our ML models.

## Continual learning
Continual learning is largely an infrastructural problem.

Very few companies update their models with every incoming samples in production, due to the following reason
- If your model is neural network, learning with every incoming samples makes it susceptible to catastrophic forgetting. Catastrophic forgetting refers to the tendency of a neural network to completely and abruptly forget previously learned information upon learning new information
- It makes training more expensive, as most hardware backends today were designed for batch processing

Companies that employ continual learning in production update their models in micro-batches (e.g. update after every 512 or 1024 examples)The updated shouldn't be deployed until it's evaluated.

Instead, you create a replica of the existing model and update this replica on new data, and only replace the existing model with the updated replica if the updated replica proves to be better. The existing model is called the champion model, and the updated replica, the challenger. In reality, a company might have multiple challenges at the same time, and handling the failed challengers is a lot more sophisticated than simply discarding it.

A simplified workflow
![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781098107956/files/assets/dmls_0901.png)

Company might not need to update their models very frequently
- The company don't have enough traffic (i.e. enough new data)
 for that retraining schedule to make sense
- The models don't decay that fast
- More overhead and if there isn't justifiable performance improvement

### Stateless Retraining vs Stateful Retraining





# Chapter 10: Infrastructure and Tooling for MLOps
Production is a spectrum, the infrastructure required can vary.
- Middle spectrum, reasonable scale - Gigabytes or Terabytes a day (e.g. Zillow, Uber)
- High spectrum - Petabyte a day (e.g. Facebook)

Infrastructure is a set of fundamental facilities that support development and maintenance of ML systems

Four layers of infrastructure
- **Storage and compute**
  - Storage layer - where data is collected and stored (e.g. hard drive disk (HDD), solid stat disk (SSD))
  - Compute layer - provide compute needed to run your ML workloads
- **Resource management** - tools to schedule and orchestrate workloads (e.g. Airflow, Kubeflow, Metaflow)
- **ML platform** - provides tools to aid the development of ML applications (such as model stores, feature stores, and monitoring tools) (e.g. SageMaker, MLFlow)
- **Development environment**

An ML platform required up-front investment from a company, but if it's done right, it can make the life of data scientists so much easier

## Storage and Compute
**Storage layer** is where data is collected and stored. **Compute layer** is all the compute resources and the mechanism to determine how these resources can be used.

Storage layer can be HDD, SSD, Amazon S3, Snowflake, can be single source or spread out across multiple locations.

Compute layer can be single CPU/GPU core, cloud compute managed by AWS Elastic Compute Cloud (EC2) or GCP.

Compute units can be
- Concurrent thread
- Multiple CPU cores joined together to execute a larger job
- Created for short-lived jobs such as AWS Step Function and GCP Cloud Run
- More permanent without being tied to a job (e.g. Virtual Machine/instance)
- Job in Spark or Ray
- Pod in Kubernetes

Metrics for compute units - memory (GB) and operation speed (FLOP - Floating Point Operations per Second)

Some companies care not only about memory a compute unit have, but also how fast it is to load data in and out of memory (bandwidth memory or I/O bandwidth)

- Hardware vendor advertises their GPUs/TPUs/IPUs have teraFLOPS
- Companies that measure FLOP might have different idea of what is counted as an operation. Also, capability of compute units (FLOPS) isn't equivalent to speed of job (FLOPS).
- As FLOPS is not very useful, many people just look into the number of cores

*Utilization* - the ratio of number of FLOPs a job can run to the number of FLOPs a compute unit is capable of handling
- Depending on the hardware backend and the application, a same utilization rate might be considered good or bad.
- Utilization also depends on how fast you can load data into memory to perform the next operations

Popular benchmark for hardware vendors to measure their hardware performance - [MLPerf](https://mlcommons.org/en/inference-datacenter-11/)

### Public Cloud vs Private Data Centers
Cloud compute is elastic, easy to use and can scale automatically, allows companies to build without worrying about the compute layer.

As company grows, cloud cost gets high which prompts companies to moving their workload back to their data centers (called 'cloud repartition'). Cloud repartition require nontrivial up-front investment in both commodities and engineering effort.

Some companies follow multicloud strategy to leverage different technologies available (e.g. GCP/Azure for ML training, AWS for deployment). The strategy don't usually happen by choice.

## Development Environment
The dev environment is where ML engineers write code, run experiments, and interact with the production environment where champion model are deployed and challenger models evaluated.

The dev environment is severely underrated and underinvested in at most companies.

Example
- Git for version control code
- DVC to version data
- Weights & Biases or Comet.ml to track experiment during development
- MLFlow to track artifacts of models when deploying them
- GitHub actions for CI/CD

Claypot AI is working on a platform that can help version and track all ML workflows in one place

It is important to standardise dev environments
- Dependency - using `requirements.txt`
- Python version
- Local vs cloud environment (e.g. Amazon SageMaker Studio)

Benefits
- Make IT support easier
- Convenient for remote work
- Help with security
- Reduces the gap between dev and prod environment

Cloud Dev environemtn might require some initial investments
- Educate employees on cloud hygiene
- Establishing secure connections to cloud
- Security compliance
- Avoiding wasteful cloud usage

### IDE
IDE is the editor where you write your code.

Example
- Native apps: VS Code, Vim
- Browser-based: AWS Cloud9, GitHub Codespaces

Notebook is stateful, but the order can be messy.

Tools for notebook: 
- [PaperMill](https://github.com/nteract/papermill) - parameterizing, executing, and analyzing Jupyter Notebook
- [Commutor](https://github.com/nteract/commuter) - A notebook hub for viewing, finding, and sharing notebooks within an organization.
- [nbdev](https://nbdev.fast.ai/) - A notebook-driven development platform

### Containers
In production, your environment is inherently stateless and new instances require new dependencies installations.

Docker is designed to solve the problem to re-create an environment on any new instance

In Docker, you create a Dockerfile with instructions. Running Dockerfile gives you a Docker image. Running Docker image gives you a Docker container.

Docker image can be build from sctratch or from existing Docker image.

Container registry (e.g. Dockre Hub, AWS ECR) is where you can share or find Docker image

Different containers might be needed for different steps in the pipeline which requires different infrastructure or have conflicting dependencies. 

*Container orchestration* can help with managing multiple containers
- *Docker compose* is a light weight container orchestrator that can manage containers on a single host
- *Kubernetes (K8s)* creates a network for containers to communicate and share resources. It helps to scale up and down and maintain high availability for the system

## Resource Management
In pre-cloud world, storage and compute resources were finite. Engineering efforts are spent on making the most out of the limited resources.

In the cloud world, storage and compute resources were more elastic. Engineering efforts shifted from maximizing resource utilization to how to use resources cost-effectively. As long as the return is justified, company are OK with adding more resources to an application.

ML workloads have two characteristics: repetitiveness and dependencies. These repetitive processes can be schedules and orchestrated to run smoothly and cost-effectively using available resources

Most workflow management tools require you specify the workflow in a form of Directed acyclic graph (DAG). Else, if cycle exists, the job will run forever.

### Basic Components
- *Cron* - schedule repetitive jobs to run at a fixed times
- *Schedulers* - cron programs that can handles dependencies (e.g. event-based triggers, actions on job fails). Handle job-type abttractions such as DAGs, priority queues, user-level quotes
  - Schedulers tends to leverage queues to keep track of, query, prioritize and allocate resource to job. Hence it needs to be aware of the resources available (specified by user or estimated by scheduler)
  - Example: Slurm, Google's Borg
  - Concerned with *when* to run jobs and *what* resources are needed
  - Often used for periodical jobs
- *Orchestrators* - Handle lower-level abstracions such as machines, instances, clusters, service-level grouping, replication, etc
  - Have ability to provision more computers to handle workloads exceeding the pool of available instances
  - Example: Kubernetes (managed Kubernets - AWS Elastic Kubernetes Service (EKS) or Google Kubernetes Engine (GKE)), HashiCorp Nomad
  - Concerned with *where* to get the resources
  - Often used for services where you have a long-running server that responds to requests

Schedulers usually run on top of orchestrators

### Workflow management tools
Data science workflow management tools - Airflow, Argo, Prefect, Kubeflow, Metaflow

Workflow management tools come with schedulers, and the schedulers work with orchestrators to allocate resources to run the workflow.

| Tool | Description | Con |
| -- | -- | -- |
| Airflow | <li>One of the earliest workflow orchestrator</li><li>Amazing task scheduler that comes with a huge library of operators connecting to cloud providers, databases, storage options</li><li>*Configuration as code* principle - belief that workflows are complex and should be defined with code instead of YAML</li> | <li>Monolithic - package entire workflows into one container --> hard to work across different containers</li><li>DAGs are not parameterized --> have to create new workflow for different parameter</li><li>DAGs are static --> Can't automatically create new steps at runtime as needed</li> |
| Prefect | <li>Prefect's workflows are parameterized and dynamic<li>*Configuration as code* principle</li> | Containerized steps aren't the first priority of Prefect |
| Argo | <li>Every step in an Argo workflow is run in its own container</li><li>Workflows are defined in YAML file, which allows you to define each step and its requirements in the same file</li> | <li>Can only run on K8s clusters, which are only available in production, local minikube can get messy</li><li>YAML file can get messy</li> |
| Kubeflow | <li>Kubeflow Pipelines which is built on top of Argo and meant to used on top of K8s</li><li>Fully parameterized and dynamic</li><li>Write workflow in Python, Dockerfile and YAML file</li> | Kubeflow helps you abstract away other tools’ boilerplate by making you write Kubeflow boilerplate |
| Metaflow | <li>Can be used with AWS Batch of K8s</li><li>Fully parameterized and dynamic</li><li>Use a Python decorator `conda` to spceify the requirements. Metaflow will automatically create container with all these requirements</li><li>Use `batch` decorator to execute on AWS batch</li> | - |

## ML Platform
As companies finds uses for ML in more applications, it is better to leveraging the same set of tools for multiple applications instead of different tools for each applications. This shared set of tools for ML deployment makes up the ML platform.

Common components - Model development, model store, feature store

Considerations when choosing a ML platform
- Whether it works with your cloud providers or your own data center
- Open source or managed service (security and privacy, extra engineering time for maintenance)

### Model Development
Tools for model development
- AWS - [SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/realtime-endpoints-deployment.html)
- GCP - [Vertex AI](https://cloud.google.com/vertex-ai/docs/predictions/overview#model_deployment)
- Azure - [Azure ML](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-deploy-online-endpoints?view=azureml-api-2&tabs=azure-cli)
- Alibaba - [Machine learning studio](https://www.alibabacloud.com/help/en/machine-learning-platform-for-ai/latest/online-model-use-cases)
- [MLflow Models](https://www.mlflow.org/docs/latest/models.html)
- [Seldon](https://www.seldon.io/)
- [Cortex](https://github.com/cortexlabs/cortex) (no longer actively maintained)
- [Ray Serve](https://docs.ray.io/en/latest/serve/index.html)

Consideration when choosing model development tool
- Ease of doing both batch and online prediction (batch prediction is usually trickier)
- Monitoring capability such as shadow deployment, canary release, A/B testing

### Model Store
Storing model alone in blob storage isn't enough. To help debugging and maintenance, it's important to track as much information associated with a model as possible.
| Information | Description | Example |
| -- | -- | -- |
| Model definition | Information required to create the shape of the model | Loss function, number of hidden layers |
| Model parameters | Actual value of the parameters of the model |  |
| Featurize and predict functions | Instruction to extract feature and predict. Usually wrapped in endpoints |  |
| Dependencies | Python version, Python packages |  |
| Data |  | Pointers to the loocation where the data is stored, name of the data, DVC commit that generated the data
| Model generation code | Code that spcifies how the model was created |  |
| Experiment artifacts | Artifacts generated during the model development phase | Graph, raw numbers |
| Tags | Helps with model discovery and filtering | Owner, task |

Companies might store artifacts in different places
- S3 - Model definition and model parameters
- Container - Dependencies
- Snowflake - Data
- Weights & Biases - Experiment artifacts
- AWS Lambda - Featurize and prediction funcions

MLflow is the most popular model store as of writing the book

### Feature Stores
Feature store can help address
- *Feature management* - help teams to share and discover features, as well as manage roles and sharing settings for each feature, act as feature catalog (e.g. [Amundsen](https://www.amundsen.io/amundsen/), [DataHub](https://github.com/datahub-project/datahub))
- *Feature transformation/computation* - perform feature computation and store the results of this computation, act like a data warehouse
- *Feature consistency* - Unify the logic for both batch features and streaming features to ensure the consistency between features during training and features during inference

Exact capabilities of feature stores vary from vendor to vendor

[Feast](https://feast.dev/) is the most popular feature store as of writing the book

[Tecton](https://www.tecton.ai/feature-store/) is a fully managed feature store that promise to handle both batch features and online features

## Build vs Buy
Factors for build vs buy decision
- **The stage your company is at** - leveage vendor solutions in early stage to get started quickly, move out when vendor costs become exorbitant
- **What you believe to be the focus or the competitive advantages of your company** - "if it is something we want to be really good at, we'll manage that in-house. If not, we'll use a vendor"
- **The maturity of the available tools** - Early adopters of new techs might not be able to find solution that is mature enough


# Chapter 11: The Human Side of Machine Learning
## User Experience
Nature of ML systems
- ML systems are probabilistic instead of deterministic
- Due to this probabilistic nature, ML systems’ predictions are mostly correct, and the hard part is we usually don’t know for what inputs the system will be correct
- ML systems can be large and might take an unexpectedly long time to produce a prediction

| Challenge | Description | Problem | Solution |
| -- | -- | -- | -- |
| Ensuring user experience consistency | Users expects a certain level of consistency, the inconsistency in ML predictions can be a hindrance | Booking.com have 200 filters, the ML team uses ML to suggest filters that the users want, but the predictions might change each time, and it confuses users | ML team atBooking.com create a rule by specifying <li>the conditions in which the system must return the same filter recommendations (e.g., when the user has applied a filter)</li> and <li>the conditions in which the system can return new recommendations (e.g., when the user changes their destination)</li> |
| Combatting "mostly correct" predictions | In some cases, we want less consistency and more diversity in a model's predictions | Predictions from large language model such as GPT are not always correct, and it's expensive to fine-tune them on task-specific data. Mostly correct prediction is useful for users who can easily correct them and not the users who don't know how to or can't correct the responses | Show users multiple resulting predictions for the same input to increase the chance of at least one of them being correct. These predictions should be rendered in a way that even non-expert users can evaluate. Example: Render generated react code into visual web pages for non-engineering users to evaluate. Sometimes called *"human-in-the-loop"* |
| Smooth failing | Actions when the queries where models take too long to respond | - | Backup systems that is less optimal than the main system but is guaranteed to generate predictions quickly (e.g. heuristics or simple models, cached precomputed predictions). Route to the backup system when main model takes too long to run |

> Consistency–accuracy trade-off - the recommendations deemed most accurate by the system might not be the recommendations that can provide user consistency
> Speed-accuracy trade-off - a model might have worse performance but run inference much faster

## Team Structure
### Involvement of subject matter experts (SME)
- SMEs include lawyers, dockers, farmers, bankers, stylists, etc
- ML projects might benefits a lot to have SMEs involed in each step of the lifecycle
- It is important to involve SMEs early on in the project planning phase and empower them to make contributions
- Many companies build low-code/no-code platforms for SMEs, most of them are currently at the labeling, quality assurance, and feedback stages

### End-to-end data scientists
ML is not just ML problem but also an infrastructure problem. MLOps require Ops expertise, especially around deployment, contanerization, job orchestration, workflow management

#### Approach 1: Have a separate team to manage production
Pro:
- Make hiring easier (hire people with one set of skills instead of multiple skills)
- Make life easier for the hire

Con:
- Communication and debugging overhead
- Debugging challenges - Might need cooperation from multiple teams to figure out what's wrong
- Finger-pointing - Each team might think it's another team's responsibility to fix the problem
- Narrow context - Less incentives to make changes to things outside of scope

#### Approach 2: Data scientists own the entire process
This is what the book's audience resonate with.

Con:
- Data scintists are expected to know everything about the process, and might end up writing more boilerplate code than data science

1. Version control
2. SQL + NoSQL
3. Python
4. Pandas/Dask
5. Data structures
6. Prob & stats
7. ML algos
8. Parallel computing
9. REST API
10. Kubernetes + Airflow
11. Unit/integration tests

Data scientists who own the entire process need good tools/infrastructures.

> According to both Stitch Fix and Netflix, the success of a full-stack data scientists relies on the tools they have. They need tools that "abstract the data scientists from the complexities of containerization, distributed processing, automatic failover and other advanced computer science concepts.

In Netflix's model, the specialists - people who originally owned a part of the project - first create tools that automate their parts, which can then be leverage by other people to own their own projects end-to-end.

## Responsible AI
Responsible AI is the practice of designing, developing, and deploying AI systems with good intentions and sufficient awareness to empower users, to engender trusts, and to ensure fair and positive impact to society. It consists of areas like fairness, privacy, transparency and accountability.

ML is deployed into almost every aspect of our lives, failing to make ML sytems fair and ethical can cause catastrophic consequences.

As developers of ML systems, you have the responsbility to
- think about how your systems will impact users and society at large
- help all stakeholders better realize their responsibilities towards the users by concretely implementing ethics, safety, and inclusitivity into your ML systems

AI incident database - [website](https://incidentdatabase.ai/)

### Case study 1: Automated grader
UK cancelled A-level in the summer of 2020 due to COVID-19 pandemic. The Office of Qualifications and Examinations Regulation (Ofqual) sanctioned the use of an automated system to assign final A-level grades to students. The result turned out to be unjust and untrustworthy, and led to public outcries.

Besides of a low model accuracy of 60%, there are other major failures.

| Failure | Description |
| -- | -- |
| Setting the wrong objective | Ofqual choose the objective "maintaining standard across school" instead of "optimizing grading accuracy for students". This leads to disproportionately downgrade high-performing cohorts from historically low-performing schools (e.g. An A student from low-performing schools was downgraded to B) <br><br> Ofqual also failed to take into account the bias that that school with more resources outperform schools with fewer resources |
| Insufficient fine-grained model evaluation to discover biases | Failed to address teachers' inconsistency in evaluation across demographic groups, multiple disadvantages for some protected groups, and racial discrimination that is endemic in some schools. Besides that, Ofqual doesn't have enough data for small schools, and use only teacher-assessed grades to assign final grades, which leads to better grades for private school with smaller classes <br><br> These biases might be discovered through the public release of the model's predicted grades with fine-grained evaluation to understand the model's performance for different slices of data (e.g. for schools of different sizes and for students from different backgrounds) |
| Lack of transparency | Ofqual failed to make important aspects of their auto-grader public before it was too late (e.g. objective of the system, how they use teacher's assessment), the public therefore can't express their concern. <br><br> The consideration came from good intention, but also means that the system didn't get sufficient independent, external scrutiny |

The boundary between what should be automated by algorithms and what should not is murky. A clearer boundary can only be achieved with more investments in time and resources from AI developers, the public and the authorities.

### Case Study 2: Anonymous data
Collecting and sharing datasets might violate the privacy and security of the users whose data is part of these datasets. To protect users, there has been calls for anonymization of personally identifiable information (PII)

Anonymization may not be sufficient to prevent data misuse and erosion of privacy expectations.

Example: Online fitness tracker Strava collects paths it records from users around the world as they exercise. This data, despite anonymization, allows people to discover patterns that exposes military bases

Solution:
- Opt-in instead of opt-out for default privacy setting
- Make its clearer or easier for users to manage privacy setting
- Developers must understand that their users might not have the technical know-how and privacy awareness, and proactively work to make the right settings the default

### A Framework for Responsible AI
| Framework | Description |
| -- | -- |
| **Discover sources for model biases** | Bias can come from any step during a project lifecycle <li>*Training data* - might be biases against less represented group</li> <li>*Labeling* - the more annotators have to rely on their subjective experience, the more room for human biases</li><li> *Feature engineering* - features related to legally protected class (e.g. ethnicity, gender, religious practices). For example, zip code and high school diplomas are correlated to race </li><ul><li> Technique to tackle this: [AIF360](https://github.com/Trusted-AI/AIF360), [Infogram method](https://docs.h2o.ai/h2o/latest-stable/h2o-docs/admissible.html)</li></ul><li> *Model's objective* - prioritizing model's performance on all users can skew the model towards the majority group of user</li><li> *Evaluation* - The need of adequate, fine-grained evaluation (sliced-based evaluation)</li> |
| **Understand the limitations of data-driven approach** | Socioeconomic and cultural aspects, identify blind spot caused by too much reliance on data <li>Example: To build equtiable automated grading system, it's essential to work with domain experts to understand the demographic distribution of student population and how socioeconomic factors get reflected in the historical performance data</li>
| **Understand the trade-offs between different desiderata** | <li>Privacy vs accuracy trade-off</li> The accuracy of differential privacy models drops much more for the underrepresented classes and subgroups <br><br><li>Compactness vs fairness trade-off</li> Model compression technique amplify algorithmic harm when the protected feature (e.g. sex, race, disability) is in the long tail of the distribution. It is found that pruning incurs a far higher disparate impact than is observed for the quantization techniques <br><br>Allocating more resources to auditing model behavior is recommended to avoid unintended harm |
| **Act early** | Companies might decide to bypass ethical issues in ML models to save cost and time, only to discover risks in the future when they end up costing a lot more <br><br> The earlier in the development cycle of an ML system that you start thinking about how this system will affect the life of users and what biases your system might have, the cheaper it will be to address these biases |
| **Create model cards** | Models cards are short documents accompanying trained model that provide information on how these models were trained and evaluated. Models cards are a step toward increasing transparency into the development of ML models. Tools: [Tensorflow](https://github.com/tensorflow/model-card-toolkit), [Metaflow](https://docs.metaflow.org/metaflow/visualizing-results/effortless-task-inspection-with-default-cards), [Scikit-learn](https://cloud.google.com/blog/products/ai-machine-learning/create-a-model-card-with-scikit-learn) |
| **Establish processes for mitigating biases** | Systematic process reduce room for human error. E.g. Google's [recommended best practices for responsible AI](https://ai.google/responsibility/responsible-ai-practices/), IBM's [AI Fairness 360](https://ai-fairness-360.org/) |
| **Stay up-to-date with responsible AI** | [ACM FAccT Conference](https://facctconference.org/index.html), the [Partnership on AI](https://partnershiponai.org/), the [Alan Turing Institute’s Fairness, Transparency, Privacy group](https://www.turing.ac.uk/research/interest-groups/fairness-transparency-privacy), and the [AI Now Institute](https://ainowinstitute.org/) |

Responsible AI is an essential practice in today’s ML industry that merits urgent actions
