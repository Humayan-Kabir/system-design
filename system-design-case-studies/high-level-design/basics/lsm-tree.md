### Log Structured Merge Tree ![ref-alex-xu](https://www.youtube.com/watch?v=I6jB0nM9SKU)

A log-structured merge-tree (LSM tree) is a data structure that efficiently stores key-value pairs for retrieval in disk- or flash-based storage systems. Log structured merge trees optimize both read and write operations using a combination of in-memory and disk-based structures.

LSM trees organize data into multiple levels with a sequence of increasingly larger, sorted components. This merge process periodically consolidates data into structures, facilitating faster lookups and efficient write operations. For this reason, ultimately log structured merge trees are ideal for write operations and write-heavy workloads.

![Diagram showing log structured merge tree](https://www.scylladb.com/wp-content/uploads/log-structured-merge-tree-diagram-2.png)
## How Do Log Structured Merge Trees Work?

Log-structured merge-trees (LSM trees) handle both write and read operations efficiently with in-memory and disk-based storage structures. Here is an overview of log structured merge tree implementation:

Write operations. Incoming data is first stored in an in-memory structure called a memtable, memory tree, or write buffer. Often, the memtable allows for faster writes to memory compared to disk. The memtable frequently uses a red-black tree to maintain data in a sorted structure based on key-value pairs.

**Level 0 sorted runs (SSTables).** As the write buffer fills up, its contents are periodically flushed to disk as sorted string tables (SSTables) in Level 0. To compare the larger categories of log structured merge tree vs SSTtables, these smaller memory data structures contain contiguous key-value pairs and are involved with the compaction process. This involves sorting merged and compacted data across different levels to reduce fragmentation and eliminate overlapping key-value pairs.

[SSTables](https://www.scylladb.com/glossary/sstable/) are quick and efficient to read and write since they are append only and do not overwrite existing data to disk, and use binary search and index files to locate blocks and keys within blocks. And rather than store keys individually, they also gain speed by maintaining a selective or sparse index, keeping index entries for only a subset of the data rather than every individual record.

**Read operations.** A Bloom filter checks the memtable for the queried key and retrieves it directly if it locates it. If the key cannot be located, the LSM tree sequentially performs a multi-level search starting from the smallest and least sorted levels (Level 0) and moving upwards to higher, more sorted levels.

Log-structured merge-trees optimize workflows in several ways:

- **In-memory buffering.** Incoming writes are first stored in an in-memory structure, the memtable, to enable fast write operations and quick access.
- **Batched writes.** LSM trees accumulate writes in memory, batching them before flushing to disk to minimize the number of disk writes, improving efficiency.
- **Reduced overwrites.** By buffering writes in memory LSM trees reduce the number of random disk writes, enhancing performance.
- **Compaction.** Periodic compaction optimizes storage by merging and organizing data, reducing fragmentation and enhancing write performance.
- **Multi-level search.** Multi-level search and increasingly sorted data structures improves read efficiency. Compaction enhances read performance, reducing disk reads and improving data organization.
- **Tuning.** Tuning parameters allows users to optimize workflow performance based on specific use cases.
- **Adaptability.** Log-structured merge trees adapt well to varying workloads, efficiently handling write-heavy operations without sacrificing read efficiency.
- **Scalability.** LSM trees scale effectively due to their ability to manage data across multiple levels and optimize storage through compaction.

## B-Trees vs Log-Structured Merge Trees

![B-Tree v.s LSM-Tree](https://miro.medium.com/v2/resize:fit:1400/1*551nefvVUZD-TvXI119fMA.jpeg)


 **Some Limitations of B+ trees**
1. **Tree Balancing Overhead**: Whenever a write , update or delete operations happen on a B+ tree they need balancing operations (e.g., splitting or merging nodes) to maintain their balanced property. In scenarios with frequent such operations , these balancing operations can introduce overhead.
2. **Disk I/O Bottlenecks**: Whenever a write , update or delete operations happen on B+ tree they require updating nodes on disk. When the datasets are large enough these disk I/O can create bottlenecks due to the need to write large portions of the tree structure, leading to increased latency and decreased write throughput.
3. **Fragmentation and Space Overhead**: Write-heavy workloads can lead to index fragmentation and increased space overhead in B+ trees. Frequent insertions and deletions may result in fragmented index pages and wasted space, affecting the efficiency of index traversal and search operations.

**Illustration of a Log-Structured Merge (LSM) Tree**
- **MemTable:** MemTable is an in-memory Log kind of data structure implemented using LinkedList to provide sequential O(1) time write. As it fills up to some threshold value, its contents are flushed to disk in a batch where they are stored as Sorted String Tables (SSTables).
- **Sorted String Tables (SSTables):** SSTables store data in sorted order, which provides efficient range query. SSTables can be there for some time snapshots. Eventually all older SSTables can be garbage collected as per configuration.
- **Levels:** SSTables are organized as levels, with level closer to memTable contains most recent data and away from memTable holds older and compacted data. Number of SSTables are as per fine tuned configurations to prevent any bottlenecks.

**Writing in an LSM Tree**

Writes are performed sequentially in a memtable which is present in runtime memory. Which is significantly faster.

But wait , What if that application crashes somehow then what about our data ? Isn’t it prone to single point failure ?

Well to tackle this issue , Whenever a write comes it writes concurrently in [Write-ahead-log](https://en.wikipedia.org/wiki/Write-ahead_logging) file , with which our data is safe.

After some threshold value is reached , these values are then flushed to disk as an immutable SSTables,

why immutable ?

As in LSM Tree there is no in-place update mechanism.

**Reading from an LSM Tree**

For searching any data, the journey starts from memtable, It first tries to find the data in memtable if found good else it looks in all the SSTables one by one from lower level to higher level .  
So lets say I have 10 SSTables and each SSTables having roughly size 8 , So we require 10 * log2(8) = 30 operations. Since SSTables are sorted they can be queried in logarithmic time. which can further be optimised by indexing or sparse indices.

Well just for searching a single data I have to apply 30 operations , can’t it be optimsed ?

Oh yes , What if I can say with 100% surity that this data is not present in some SSTables ?

Then we can skip those SSTables right ?

Well how to know if this data is not present in some SSTables ?

There is a space optimised probabilistic data structure called [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter) .

Which can say with surity that this data is not present in these SSTables. This helps minimize expensive disk reads .

**Updating a data in an LSM Tree**

Since in LSM Tree there is no in-place update mechanism. How update happens in LSM Tree ?

In LSM Tree updates are append only meaning it will be simply appended as write happens. But when compaction happens latest data will be retained and older will be discarded.

**Deleting a data in an LSM Tree**

Since in LSM Tree there is no in-place delete mechanism. How delete happens in LSM Tree ?

In LSM Tree deletes are append only meaning it will be simply appended as write happens but with deletion marker ie tombstones. When compaction happens and latest data is marked as deleted so that data will be discarded all together.

**Advantages of LSM Tree**

1. **High Write Throughput**: LSM trees excel in write-heavy workloads due to their append-only nature. By buffering writes in memory and periodically flushing them to disk, LSM trees can achieve high write throughput rates, making them ideal for applications with frequent write operations.
2. **Efficient Write Amplification**: LSM trees minimize write amplification — the ratio of actual writes to logical writes — by batching and consolidating writes before persisting them to disk. This optimization reduces the number of disk I/O operations required for write operations, leading to improved storage efficiency and performance.
3. **Space and Memory Efficiency**: LSM trees optimize space and memory usage by leveraging compaction to merge and consolidate data on disk. By periodically merging smaller sorted runs into larger ones, LSM trees reduce storage overhead and improve query performance, while also minimizing memory consumption for in-memory data structures.
4. **Efficient Range Queries**: LSM trees offer efficient support for range queries, allowing applications to retrieve data within a specified range quickly. By maintaining data in sorted runs on disk, LSM trees enable efficient range scans without the need for costly index traversal or random disk seeks.

Thanks for reading !

B-trees and log-structured merge trees (LSM trees) are both efficient data structures, but they have different characteristics and are optimized for different scenarios.

A B-tree is a balanced structure of nodes with multiple keys and child pointers. Each node contains a range of keys and pointers to child nodes, enabling efficient search, insertion, and deletion.

A B-tree sorts and stores data in a hierarchical structure optimized for both read and write operations, providing more balanced performance for sequential and random access. It is efficient for range queries due to the hierarchical nature, as traversing the tree can quickly identify a range of keys.

B-trees store data in a sorted order within tree nodes, so they excel in scenarios where data needs to be continually accessed and modified. This is why B-trees are often used in file systems and databases.

In contrast, LSM trees consist of multiple levels where data is organized, leveraging both in-memory and disk-based storage structures. They are optimized for write-heavy workloads and handle write operations quickly by buffering data in memory before flushing to disk in sorted runs efficiently.

LSM trees require periodic compaction to merge and organize data, reducing fragmentation and optimizing storage. They excel in scenarios where write throughput is crucial and can tolerate slightly higher read latencies.

In terms of B-trees vs log-structured merge trees, there are important differences in write vs read optimization. LSM trees prioritize write optimization, making them suitable for write-heavy workloads. In contrast, B-trees maintain a more balanced approach for reads and writes.

Storage efficiency is also somewhat different, in that log-structured merge trees require periodic compaction to optimize storage and minimize fragmentation, while B-trees maintain a relatively stable structure.

Common use cases for B-trees include databases and file systems where data is frequently read and written. Log-structured merge trees are often used in systems that handle heavy write loads, such as certain types of databases, distributed storage systems, and log-structured file systems.

## Log Structured Merge Tree Database Comparison

There are many systems on the market that use LSM trees to optimize storage, writes, and reads while addressing different requirements of distributed systems, streaming platforms, and big data processing. Here are a few notable examples:

- Cassandra log structured merge tree emphasizes write optimization and is suitable for write-heavy workloads, time-series data, IoT, and logging.
- Kafka log structured merge tree excels in handling real-time streaming and event data with high throughput; it is best for real-time data pipelines, event streaming, and message queuing.
- Hbase log structured merge tree focuses on random read/write access to large datasets and is used in big data analytics and Hadoop-based systems requiring random access.

**Cassandra.** The Cassandra log structured merge tree implementation employs a combination of an in-memory memtable and disk-based SSTables to achieve a distributed NoSQL database designed for high scalability, fault-tolerance, and high-performance writes. **Leveled Compaction Strategy (LCS) and Size-Tiered Compaction Strategy (STCS)** are commonly used in [Cassandra](https://www.scylladb.com/learn/apache-cassandra/introduction-to-apache-cassandra/). This platform is suitable for scenarios requiring high write throughput, like [time-series data](https://www.scylladb.com/glossary/time-series-data/), IoT applications, and logging, due to its distributed nature and emphasis on writes. ScyllaDB takes a similar approach, and offers addtional compaction options (more details on ScyllaDB’s approach below).

**Kafka.** The [Kafka](https://www.scylladb.com/glossary/kafka-2/) log structured merge tree implementation uses a variant called Log-Structured Storage to manage disk space and optimize for high-throughput writes. It is a distributed streaming platform designed for building real-time data pipelines and streaming applications ideal for building real-time data pipelines, event streaming, and message queuing due to its persistent, high-throughput, and [low-latency](https://www.scylladb.com/glossary/low-latency-database/) characteristics.

**HBase.** The Hbase log structured merge tree implementation uses an LSM tree-based storage engine to manage data in HFiles (similar to SSTables) and in-memory Memstore and persistent HFiles on disk. This open-source, distributed, column-oriented database built atop the Hadoop Distributed File System (HDFS) is designed for random, real-time read/write access to large datasets. It is suited for applications requiring random access to large datasets, such as big data analytics.

## Does ScyllaDB Offer Solutions for Log Structured Merge Tree?

Yes. [ScyllaDB](https://www.scylladb.com/) uses an LSM tree structure, which makes it well-suited for teams with write-heavy workloads. ScyllaDB optimizes write speed because: 1) writes are sequential, which is faster in terms of disk I/O and 2) writes are performed immediately, without first worrying about reading or updating existing values (like databases that rely on B-trees do). As a result, users can typically write a lot of data with very low latencies. At the same time, ScyllaDB can offer fast reads as a result of its specialized internal cache (in contrast to Cassandra, which relies on Linux caching that is inefficient for database implementations.)

ScyllaDB leverages RUM conjecture and controller theory, to deliver a state-of-art LSM-tree compaction for its users. Find out more about how ScyllaDB can identify the latest versions of data to shave down time on queries in this [LSM Tree tech talk](https://www.scylladb.com/presentations/scaling-scylladb-storage-engine-with-state-of-art-compaction/) from ScyllaDB Engineering.