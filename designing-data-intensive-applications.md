# Designing Data-Intensive Applications - by Martin Kleppmann

# Table of Contents
- [Designing Data-Intensive Applications - by Martin Kleppmann](#designing-data-intensive-applications---by-martin-kleppmann)
- [Table of Contents](#table-of-contents)
- [Part 1: Foundation of Data Systems](#part-1-foundation-of-data-systems)
- [Chapter 1. Reliable, Scalable, and Maintainable Applications](#chapter-1-reliable-scalable-and-maintainable-applications)
  - [Reliabiltiy](#reliabiltiy)
  - [Scalability](#scalability)
    - [Case study: Twitter](#case-study-twitter)
- [Chapter 2. Data Models And Query Language](#chapter-2-data-models-and-query-language)
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

### Case study: Twitter
**Main Operations**: Post tweet and home timeline  
**Tweet volume**: 4.6k requests/sec on average, over 12k/sec at peak  
**Problem**: fan-out  
**Approach**:
- Query home timeline on the spot  
- Cache home timeline  

**Load parameter**: The distribution of followers per user (weighted by how often those users tweet)  
**Final solution**: Hybrid of 2 approaches


# Chapter 2. Data Models And Query Language



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



