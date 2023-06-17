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
- [Chapter 6: Model Development and Offline Evaluation](#chapter-6-model-development-and-offline-evaluation)
  - [Evaluating ML Models](#evaluating-ml-models)
    - [Six tips for Model Selection](#six-tips-for-model-selection)
    - [Ensembles](#ensembles)
  - [Experiment Tracking and Versioning](#experiment-tracking-and-versioning)
    - [Experiment Tracking](#experiment-tracking)
    - [Versioning](#versioning)
  - [Debugging  ML Models](#debugging--ml-models)
  - [Model Offline Evaluation](#model-offline-evaluation)
    - [Baselines](#baselines)
    - [Evaluation Methods](#evaluation-methods)
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
| Focal loss | Assign a higher weight for samples that has a lower probability of being right |

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

Mixup improves model generalization, reduces their memorization of corrupt labels, increase their robustness to adversarial examples, and stabilizes the training of generative adversarial networks

Using neural network to synthesize training data (e.g. CycleGAN)

Resource: [A Survey on Image Data Augmentation for Deep Learning](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-019-0197-0)


# Chapter 5: Feature Engineering





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
    Given a dataset, sample with replacement to create different datasets (called bootstrap), and train a classification or regression model on each of these bootstraps. (eg: Random Forest)
  - Boosting  
    Boosting is a family of iterative ensemble algorithms that convert weak learners to strong ones. The samples are weighted differently among iterations, where future weak learners focus more on the misclassified examples. (eg: GBM - XGBoost, LightGBM)
  - Stacking  
    Create a meta-learner that combines the outputs of the base learners to output final predictions

## Experiment Tracking and Versioning
During the model development process, you often have to **experiment with many architectures and many different models**. It is important to keep track of all the definition needed to re-create an experiment and its relevant artifacts. An **artifact** is a file generated during an experiment (eg: loss curve, logs graph, intermediate results).

This enables you to compare different experiments and choose the best suited one. It helps the understnaing of how small changes affect model's performance.

The process of tracking the progress and results of an experiment is called **experiment tracking**. The process of logging all the details of an experiment is called **versioning**.

Experiment Tracking Tools: MLFlow, Weights & Biases  
Versioning Tools: DVC

### Experiment Tracking
It is important to track what's going on during training, not only to detect and address these issues, but also to evaluate whether the model is learning anything useful (eg: loss not decreasing, overfitting, underfitting).

Things to track:
- Loss curve corresponding to train and eval splits
- Model performance metrics (eg: accuracy, F1 score)
- Log of corresponding sample, prediction and ground truth label
- The speed
- System performance metrics (eg: RAM, CPU/GPU utilization)
- Parameter and hyperparameter

Tracking gives you observability into the state of the model, especially when something happens.

### Versioning
ML systems are part code, part data, so both need to be versioned.

Challenge of data versioning:
- Data is often larger than code, we can't use the same strategy to version data
- A line in data can be indefinitely long, especially if it's stored in a binary format. Specifying a diff can be not helpful
- Dataset can be so large than duplicating it multiple times across different versions might be unfeasible
- A dataset might not fit into a local machine
- Definition of a diff when versioning data
- Resolving merge conflicts can be challenging (especially when there is privacy law such as General Data Protection Regulation (GDPR))

As of 2021, data versioning tools like DVC only register a diff if the checksum of the total directory has changed and if a file is removed or added.

Aggressive tracking and versioning helps with reproducibility, but it doesn't ensure reproducibility. The framework and hardware might introduce nondeterminism to the experiment results.

## Debugging  ML Models
Reasons that an ML model can fail:
- Theoretical constraints
- Poor implementation of model
- Poor choice of parameters
- Data problems
- Poor choice of features

Tried-and-true debugging techniques by experienced ML engineers
- **Start simple and gradually add more components** -If you want to use a BERT-like model, which use both a masked language model (MLM) and next sentence prediction (NSP) loss, you might want to use only the MLM loss before adding NLS loss
- **Overfit a single branch** - Try to overfit a small amount of data. If it can't overfit, there might be something wrong with the implementation
- **Set a random seed** - to ensure consistency between different runs





## Model Offline Evaluation
"How can I know that our ML models are any good?"  

### Baselines
- Random baseline
- Simple heuristic
- Zero rule baseline
- Human baseline
- Existing solutions

### Evaluation Methods
- Pertubation tests
- Invariance tests
- Directional expectation tests
- Model calibration
- Confidence measurement
- Slice-based evaluation
  - Heuristics-based
  - Error analysis
  - Slice finder




# Chapter 7: Model Deployment and Prediction Service




# Chapter 8: Data Distribution Shifts and Monitoring





# Chapter 9: Continual Learning and Test in Production






# Chapter 10: Infrastructure and Tooling for MLOps






# Chapter 11: The Human Side of Machine Learning



