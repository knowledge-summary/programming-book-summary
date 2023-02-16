# Designing Data-Intensive Applications - by Martin Kleppmann

# Table of Contents
- [Designing Data-Intensive Applications - by Martin Kleppmann](#designing-data-intensive-applications---by-martin-kleppmann)
- [Table of Contents](#table-of-contents)
- [Part 1: Foundation of Data Systems](#part-1-foundation-of-data-systems)
- [Chapter 1. Reliable, Scalable, and Maintainable Applications](#chapter-1-reliable-scalable-and-maintainable-applications)
  - [Reliabiltiy](#reliabiltiy)
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

Faults (usually one components of a system) is not the same as failure (systems as a whole).

Triggering faults deliberately, althought counterintrutive, can be useful to build fault-tolerant systems.

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



