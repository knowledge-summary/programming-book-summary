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
  - [Graph-Like Data Model](#graph-like-data-model)
    - [Property graph](#property-graph)
    - [Triple Store](#triple-store)
    - [Datalog](#datalog)
- [Chapter 3. Storage And Retrieval](#chapter-3-storage-and-retrieval)
  - [Hash Indexes (key-value store)](#hash-indexes-key-value-store)
  - [SSTables and LSM-Trees](#sstables-and-lsm-trees)
  - [B-Trees](#b-trees)
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

MapReduce is more challenging to use as you need to write two carefully coordinated Javascript functions. Declarative query language offers more opportunities for query optimizer to improve performance. 

MongoDB 2.2 added support for a declarative query language called the aggregation pipeline.

Example:
- SQL
  ``` sql
  SELECT date_trunc('month', observation_timestamp) AS observation_month, 
        sum(num_animals) AS total_animals
  FROM observations
  WHERE family = 'Sharks'
  GROUP BY observation_month;
  ```
- Imperative
  ``` javascript
  if (user && user.name && !user.first_name) {
      // Documents written before Dec 8, 2013 don't have first_name
      user.first_name = user.name.split(" ")[0];
  }
  ```
- MapReduce
  ``` sql
  db.observations.mapReduce(
      function map() { 2
          var year  = this.observationTimestamp.getFullYear();
          var month = this.observationTimestamp.getMonth() + 1;
          emit(year + "-" + month, this.numAnimals); 3
      },
      function reduce(key, values) { 4
          return Array.sum(values); 5
      },
      {
          query: { family: "Sharks" }, 1
          out: "monthlySharkReport" 6
      }
  );
  ```
- MongoDB aggregation pipeline
  ``` sql
  db.observations.aggregate([
      { $match: { family: "Sharks" } },
      { $group: {
          _id: {
              year:  { $year:  "$observationTimestamp" },
              month: { $month: "$observationTimestamp" }
          },
          totalAnimals: { $sum: "$numAnimals" }
      } }
  ]);
  ```

## Graph-Like Data Model
A graph consists of two kinds of objects:
- *vertices* (aka *nodes*, *entities*)
- *edges* (aka *relationships*, *arcs*)

Graphs are not limited to homogenous data.

Different ways of structuring and querying data in graphs
- *property graph* model (e.g. Neo4j, Titan, InfiniteGraph)
- *triple-store* model (e.g. Datomic, AllegroGraph, and others)

Declarative query language for graphs
- Cypher
- SPARQL
- Datalog

Graph query language - Gremlin  
Graph processing framework - Pregel

### Property graph
Each vertex consists of 
- A unique identifier
- A set of outgoing edges
- A set of incoming edges
- A collection of properties (key-value pairs)

Each edges consists of
- A unique identifier
- The vertex at which the edge starts (the tail vertex)
- The vertex at which the edge ends (the head vertex)
- A label to describe the kind of relationship between the two vertices
- A collection of properties (key-value pairs)

Can think: graph = vertices table + edges table

Graphs are good for evolvability

*Cypher* is a declarative query language for property graphs, created for Neo4j graph database.

Example of creating the graph data
```
CREATE
  (NAmerica:Location {name:'North America', type:'continent'}),
  (USA:Location      {name:'United States', type:'country'  }),
  (Idaho:Location    {name:'Idaho',         type:'state'    }),
  (Lucy:Person       {name:'Lucy' }),
  (Idaho) -[:WITHIN]->  (USA)  -[:WITHIN]-> (NAmerica),
  (Lucy)  -[:BORN_IN]-> (Idaho)
```

Example of querying from graph database. Finding people born in US and living in Europe
```
MATCH
  (person) -[:BORN_IN]->  () -[:WITHIN*0..]-> (us:Location {name:'United States'}),
  (person) -[:LIVES_IN]-> () -[:WITHIN*0..]-> (eu:Location {name:'Europe'})
RETURN person.name
```

### Triple Store
Form: *(subject, predictive, object)*

Data can be written as triples in a format called *Turtle*, a subset of *Notation3 (N3)*.

Example:
```
@prefix : <urn:example:>.
_:lucy     a :Person;   :name "Lucy";          :bornIn _:idaho.
_:idaho    a :Location; :name "Idaho";         :type "state";   :within _:usa.
```

Triple store is closely linked to the *semantic web*.

Semantic web: website is human readable, hence, website can publish information that as machine-readable data, forming web of data (haven't shown any sign of being realized in practice)

*RFD data model* (Resource Description Framework) - a mechanism for different websites to publish data in a consistent format (can be in XML format or Turtle)

*SPARQL* is a query language for triple-stores using the RDF data model. Cypher's pattern matching is borrowed from SPARQL, they look quite similar
```
PREFIX : <urn:example:>

SELECT ?personName WHERE {
  ?person :name ?personName.
  ?person :bornIn  / :within* / :name "United States".
  ?person :livesIn / :within* / :name "Europe".
}
```

```
(person) -[:BORN_IN]-> () -[:WITHIN*0..]-> (location)   # Cypher

?person :bornIn / :within* ?location.                   # SPARQL
```

### Datalog
Datalog is an old language that provides foundation that later query language build upon. It is a query language of Datomic. Cascalog is a Datalog implementation for querying large datasets in Hadoop.

Datalog's data model: *predicate(subject, object)*

Example:
```
name(namerica, 'North America').
type(namerica, continent).
```

# Chapter 3. Storage And Retrieval
A database needs to do two things: store data and retrieve data

log-structured storage engine

page-oriented storage engines such as B-trees

What database needs to deal with
- concurrency control
- reclaiming disk space
- handling error and partially written records

General definition of log: an append-only sequence of records (doesn't have to be human-readable)

The simplest database system - a key value pair
- Pro: write is append which is fast
- Con: read is O(n)

An *index* is an additional structure that is derived from the primary data. Well-chosen indexes speed up read queries, but every index slows down writes. This is an important trade-off in storage systems.

Database don't usually index everything by default, but require the application developer to choose indexes manually, using knowledge of the application's typical query pattern.

## Hash Indexes (key-value store)
Hash indexes keep an in-memory hash map where every key is mapped to a byte offset in the data file.

To avoid running out of disk space, it break the logs into segments of a certain size by closing a segment file when it reaches a certain size, and making subsequent writes to a new segment file. Then, perform compaction on these segments.

Compaction - throwing away duplicate keys in the log, and keeping only the most recent update for each key. (can be applied after merging several segments)

A search is done by checking the latest segment hash map, if the key is not present, check the second-most recent segment, and so on.

Hash indexes is used by [Bitcask](https://github.com/basho/bitcask), the default storage engine of Riak.

Well suited from situations where the value for each key is updated frequently, and there are not too many distinct keys.

Design considerations
- File format - binary format for efficiency
- Deleting record - append a special deletion record (also called *tombstone*) to the data file, the merging process discard any previous value for the deleted key
- Crash recovery - storing snapshots of each segment's hash map on disk (e.g. when server restarts)
- Partially written record - Include checksums to detect and ignore corrupted part of the log
- Concurrency control - Only one write thread, can be read concurrently by multiple thread

Pro
- Sequential write operations are generally faster
- Concurrency and crash recovery is simpler
- Merging old segments avoids the problem of data files getting fragmented over time

Con
- If there is a lot of keys, the hash table might not be able to fit into memory. Storing hash table in disk requires a lot of random access I/O which is expensive
- Range queries is not efficient since keys in hash map are indepedent

## SSTables and LSM-Trees
Sorted String Table (SSTable) require that the sequence of key-value pairs is sorted by key

Pro
- Merging segment is simple and efficient
- No longer need to keep an index for all the keys in memory, can use a sparse in-memory index (e.g. one key for every few kilobytes of segment files)
- Possible to group records into a block and compress it before writing it to disk. Each entry of the sparse in-memory index then points at the start of a compressed block, which save space and reduce I/O bandwidth use

1. Write into an in-memory balanced tree data structure (e.g. red-black tree, AVL tree), called *memtable*
2. When the memtable get bigger than some thresholds (e.g. a few megabytes), write it out to disk as an SSTable file
3. When reading, first try to find the key in the memtable, then in the most recent on-disk segment of the database, and so on
4. Run merging and compaction in the background from time to time to discard overwritten and deleted value

To handle the situation when the recent entry is lose during crash, store an immediate appended log. This helps to restore the memtable after a crash

The terms SSTable and memtable are introduced by Google's Bigtable [paper](https://research.google/pubs/pub27898/).

Originally this indexing structure was described by Patrick O'Neil et al. under the name Log-Strcutured Merge-Tree (or LSM-Tree) in the [paper](https://www.cs.umb.edu/~poneil/lsmtree.pdf). Storage engines that based on this principle of merging and compacting sorted files are often called LSM storage engines.

Methods of performance optimization
1. Use *Bloom filter*, a memory-efficient data structure for approximating the content of a set. It can tell you if a key does not appear in the database and reduce unnecessary disk reads.
2. Size-tiered compaction - newer and smaller SSTables are successively merged into older and larger SSTables
3. Level compaction - key range is split up into smaller SSTables and older data is moved into separate levels, which allows the compaction to proceed more incrementally and use less disk space

List of storage engine libraries that use the concepts of SSTables and LSM-Trees
| Library Name | Usage | Remark | Strategy to determine the order and timing of how SSTables are compacted and merged |
| -- | -- | -- | -- |
| [LevelDB](https://github.com/google/leveldb/blob/main/doc/impl.md) (used in Riak as an alternative of Bitcask) | key-value storage engine libraries that are designed to be embedded into other applications |  | leveled compaction |
| [RocksDB](https://rocksdb.blogspot.com/2013/11/the-history-of-rocksdb.html) | key-value storage engine libraries that are designed to be embedded into other applications |  | leveled compaction |
| Cassandra |  |  | Both leveled compaction and size-tiered |
| [Hbase](https://blog.cloudera.com/apache-hbase-i-o-hfile/) |  |  | size-tiered |
| Lucene | an indexing engine for full-text search used by Elasticsearch and Solr | use similar method called term dictionary (key: a word (a term), value: a list of IDs of all the documents that contain the word (the postings list)) | 

## B-Trees
B-tree is the most widely used indexing structure. It remains the standard index implementation in almost all relational databases, and many nonrelational databases use them too.

Same as SSTables, B-trees key key-value pairs sorted by key.

B-trees break the database down into fixed-sized block or pages, and read or write one page at a time. This design corresponds more closely to the underlying hardware, as disks are also arranged in fixed-size blocks.

Each page can be identified using an address or location, which allows one page to refer to another, similar to a pointer, but on disk instead of memory. We can use these page references to construct a tree of pages.

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781491903063/files/assets/ddia_0306.png)

One page is designated as the root of the B-tree, which is the location to start when looking up a key in the index.

The keys between the references indicate where the boundaries between those ranges lie. Eventually, we get down to a page containing individual keys (a *leaf page*), which either contain the value for each key inline or contain references to the pages where the values can be found.

The number of references to child pages in one page of the B-tree is called the *branching factor*. In practice, it depends on the space required to store the page references and is typically several hundred.


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



