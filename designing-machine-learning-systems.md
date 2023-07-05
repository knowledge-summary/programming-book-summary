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
- [Chapter 9: Continual Learning and Test in Production](#chapter-9-continual-learning-and-test-in-production)
- [Chapter 10: Infrastructure and Tooling for MLOps](#chapter-10-infrastructure-and-tooling-for-mlops)
  - [Storage and Compute](#storage-and-compute)
- [Chapter 11: The Human Side of Machine Learning](#chapter-11-the-human-side-of-machine-learning)



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





# Chapter 9: Continual Learning and Test in Production






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








# Chapter 11: The Human Side of Machine Learning



