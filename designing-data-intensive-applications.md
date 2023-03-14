# Designing Data-Intensive Applications - by Martin Kleppmann

# Table of Contents
- [Designing Data-Intensive Applications - by Martin Kleppmann](#designing-data-intensive-applications---by-martin-kleppmann)
- [Table of Contents](#table-of-contents)
- [Part 1: Foundation of Data Systems](#part-1-foundation-of-data-systems)
- [Chapter 1. Reliable, Scalable, and Maintainable Applications](#chapter-1-reliable-scalable-and-maintainable-applications)
  - [Reliabiltiy](#reliabiltiy)
  - [Scalability](#scalability)
    - [Describing Performance](#describing-performance)
    - [Case study: Twitter](#case-study-twitter)
  - [Maintainability](#maintainability)
- [Chapter 2. Data Models And Query Language](#chapter-2-data-models-and-query-language)
  - [Relational Model vs Document Model](#relational-model-vs-document-model)
  - [Query Language for Data](#query-language-for-data)
- [Chapter 3. Storage And Retrieval](#chapter-3-storage-and-retrieval)
- [Chapter 4. Encoding And Evolution](#chapter-4-encoding-and-evolution)
- [Part 2: Distributed Data](#part-2-distributed-data)
- [Chapter 5. Replica](#chapter-5-replica)
- [Chapter 6. Partitioning](#chapter-6-partitioning)
- [Chapter 7. Transactions](#chapter-7-transactions)
- [Chapter 8. The Trouble With Distributed Systems](#chapter-8-the-trouble-with-distributed-systems)
- [Chapter 9. Consistency And Consensus](#chapter-9-consistency-and-consensus)
- [Part 3: Derived Data](#part-3-derived-data)
- [Chapter 10. Batch Processing](#chapter-10-batch-processing)
- [Chapter 11. Stream Processing](#chapter-11-stream-processing)
- [Chapter 12. The Future Of Data Systems](#chapter-12-the-future-of-data-systems)


# Part 1: Foundation of Data Systems
# Chapter 1. Reliable, Scalable, and Maintainable Applications
Many applications today are data-intensive, as opposed to compute-intensive. (using databases, caches, search indexes, stream processing, batch processing)

## Reliabiltiy
Realiability means "continue to working correctly, even when things go wrong."

**Faults** are the things that can go wrong, systems that anticipate faults and can cope with them are called **fault-tolerant** or **resilient**.
- Hardware faults
  - Example solution:
    - Add redudancy
    - Using software fault-tolerance techniques
- Software faults
  - More likely to correlated across nodes
  - Example: A runaway process that uses up some shared resources, a software bug on a library that many applications depend on
  - Solution: careful about assumptions and interactions in the system, through testing, process isolation, allowing crash and restart, measuring, monitoring and analyzing system behaviours in production
- Human errors
  - Humans are known to be unreliable
  - Solutions:
    - Design systems that minimizes opportunities for errors
    - Decouple the places where people make the most mistakes from the places where they can cause failures
    - Test thoroughly at all levels
    - Allow quick and easy recovery from human errors
    - Set up detailed and clear monitoring
    - Implement good management practices and training

Faults (usually one components of a system) is not the same as failure (systems as a whole).

Triggering faults deliberately, althought counterintrutive, can be useful to build fault-tolerant systems.

## Scalability
Scalability is a system's ability to cope with increased load.

Question: If the system grows in a particular way, what are our options for coping with the growth?

One common reason for degradation is increased load.

Steps:
1. Describing loads
   - Using *load parameters* (e.g. requests per second, ratio of reads to writes in a database, hit rate on cache, number of users in a chat room).
2. Describing Performance
   - Increase load parameter, keep resources unchanged, how is the performance affected?
   - When increase a load parameter, how much increase in resources to keep performance unchanged?
   - Example: Batch processing - throughput, online system - response time (a distribution of values, using percentile is better than using average)

### Describing Performance
Latency and response time is not the same. Response time is what the user see.

Percentiles are abbreviated, median as p50, 95th percentile as p95. High percentiles of response times, also known as tail latencies are important. Slowest requests can be associated with valuable customers. 

Head-of-line blocking - queuing delay

Tail latency amplification - Even if only a small percentage of backend calls are slow, the chance of getting a slow call increases if an end-user request requires multiple backend calls, and so a higher proportion of end-user requests end up being slow

Approximation algorithm - Forward decay, t-digest, HdrHistogram

You need to rethink your architecture on every order of magnitude load increase.
- Scaling up (vertical scaling, moving to a more powerful machine)
- Scaling out (horizontal scaling, distributing the load across multiple smaller machines)

An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare—the load parameters.

### Case study: Twitter
**Main Operations**: Post tweet and home timeline  
**Tweet volume**: 4.6k requests/sec on average, over 12k/sec at peak  
**Problem**: fan-out  
**Approach**:
- Query home timeline on the spot  
- Cache home timeline  

**Load parameter**: The distribution of followers per user (weighted by how often those users tweet)  
**Final solution**: Hybrid of 2 approaches

## Maintainability
We can and should design software in such a way that it will hopefully minimize pain during maintenance, and thus avoid creating legacy software ourselves.

Three design principles of for software systems
- Operability
- Simplicity
- Evolvability (extensibility, modifiability, plasticity)

"Good operations can often work around the limitations of bad (or incomplete) software, but good software cannot run reliably with bad operations"

A big ball of mud

Possible symptoms of complexity:
- Explosion of the state space
- Tight coupling of modules
- Tangled dependencies
- Inconsistent naming and terminology
- Hacks aimed at solving performance problems
- Special casing to work around issues elsewhere

Hidden assumptions, unintended consequences, unexpected interactions.

Use abstraction to reduce complexity.

New changes:
- New facts
- Previously unanticipated use cases
- Business priorities change
- Users request new feature
- New platforms replace old platforms
- Legal or regulatory requirements change
- Growth of the system forces architectual changes

Agile working pattern - test-driven development (TDD) and refactoring.

An application has
- Functional requirements (what it should do, such as allowing data to be stored, retrieved, searched, and processed in various ways)
- Nonfunctional requirements (general properties like security, reliability, compliance, scalability, compatibility, and maintainability))


# Chapter 2. Data Models And Query Language
Data models are perhaps the most important part of developing software, because they have such a profound effect: not only on how the software is written, but also on how we think about the problem that we are solving.

Layers
1. Model real world in terms of objects or data strcutures, and APIs that manipulate those data structures.
2. Express objects in terms of general-purpose data model (JSON, XML), tables in relational database, graph model
3. Database software represents JSON/XML/relationship/graph data in terms of bytes in memory.
4. Hardware engineers represent bytes in terms of electrical currents, pulses of light, magnetic fields, and more.

## Relational Model vs Document Model
Relational model: Data is organized into relations (called tables in SQL), where each relation is an unordered collection of tuples.

Driving force of NOSQL (Not Only SQL)
- Need for greater scalability (very high write throughput or very large datasets)
- Preference for open source
- Specialized query operations that are not well supported by relational model
- Frustration with restrictiveness of relational schemas, desires for more dynamic and expressive data model

*Polygot persistence* - Using multiple data storage technologies for varying data storage needs across an application

*Impedance mismatch* - Mismatch of application model (e.g. OOP) and SQL data model

Object-relational matching framework - [ActiveRecord](https://guides.rubyonrails.org/active_record_basics.html), [Hibernate](https://hibernate.org/orm/).

Example: Representing a LinkedIn profile
- Traditional SQL model - put positions, education, and contact information in separate tables
- SQL standard that supports structured datatypes and XML data (multi-valued data to be stored within a single row)
- Store JSON/XML as text field and let the application interpret its structure and content

Other types of SQL
- **SQL standards that support XML**: Oracle, IBM DB2, MS SQL Server, PostgreSQL
- **SQL standards that support JSON**: IBM DB2, MySQL, PostgreSQL
- **Document-oriented databases**: MongoDB, RethinkDB, CouchDB, Expresso
  - Has better *locality*
  - Not supportive for joins

The advantage of using ID - It has no meaning to humans, it never needs to change.

The disadvantage of not using ID - Anything that is meaningful to humans may need to change in the future. If that information is duplicated, all the redundant copies need to be updated, which leads to write overhead, risk inconsistencies.

History - IBM's Information Management System (IMS) using hierarchical model (work well for one-to-many relationship, but doesn't work well for many-to-many relationship)

Hierarchical model represents all data as a tree of records nested within records, much like the JSON strcuture.

Solutions proposed to solve the limitations of hierarchical model:
- *Network model* (or called CODASYL model) - Generalization of hierarchical model, a record can have multiple parents, instead of one. The links between records were not foreign keys, but more like pointers. Need to transverse from the root record.
- *Relational model* - Query optimizer automatically decides which parts of the query to execute in which order.

Relational and document databases represents many-to-one and many-to-many relationships in a similar fashion. The related item is referenced by a unique identifier, *foreign key* (relational model), *document reference* (document model).

| Data model | Pro | Con |
| --- | --- | --- |
| Document data model | - Schema flexibility <br/> - Better performance due to locality <br/> - For some applications it is closer to the data structures used by the application | - Poor supports for join |
| Relational data model | - Better supports for joins, and many-to-one and many-to-many relationships | - Shredding (splitting a document-like structure into multiple tables) can lead to cumbersome schemas and unnecessarily complicated application code |

The schema-on-read approach is advantageous if the items in the collection don't all have the same structure. For example, having different types of objects which is not practical to put each object in its own table.

The locality advantage of document only applies when you need large parts of document at the same time.

Update to document can be wasteful as the entire document usually needs to be rewritten.

Grouping related data together for locality is not limited to the document model. E.g. 
- Google's Spanner allows schema to declare that a table's rows should be interleaved (nested) within a parent table
- Oracle uses multi-table index cluster tables
- Bigtable data model (used in Cassandra and HBase) has column-family concept

## Query Language for Data
Declarative query and MapReduce query.

SQL is declarative. In a declarative query language, you just specify the pattern of the data you want. It is up to the database system's query optimizer to decide which indexes and join methods to use.

Benefits of declarative language
- More limited in functionality gives the database much more room for automatic optimizations
- lend themselves to parallel execution

CSS and XSL are both declarative languages for specifying the styling of a document.

Alternative: Imperative query, e.g. use Javascript to change the style using for loop which is likely a more inferior method

*MapReduce* is a programming model for processing large amount of data in bulk across many machines. It is neither declarative or imperative but somewhat in between.
- `map`/`collect` 
- `reduce`/`fold`/`inject`

`map` and `reduce` are somewhat restrictive in what they are allowed to do. This allows the functions to be run everywhere, in any order, and rerun them on failure.
- Must be pure function
  - Only use the data passed as input
  - No additional database queries
  - Must not have side effects

MapReduce is fairly low-level programming model for distribution execution on a cluster of machines. SQL is higher-level query languages.



# Chapter 3. Storage And Retrieval



# Chapter 4. Encoding And Evolution



# Part 2: Distributed Data
# Chapter 5. Replica



# Chapter 6. Partitioning



# Chapter 7. Transactions



# Chapter 8. The Trouble With Distributed Systems



# Chapter 9. Consistency And Consensus



# Part 3: Derived Data
# Chapter 10. Batch Processing



# Chapter 11. Stream Processing



# Chapter 12. The Future Of Data Systems



