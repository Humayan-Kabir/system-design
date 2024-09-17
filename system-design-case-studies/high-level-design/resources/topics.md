![[system-design-topics.png]]

* [bytebytego-101](https://github.com/ByteByteGoHq/system-design-101)
* [system-design-primer](https://github.com/donnemartin/system-design-primer)

#### **1. Caching Strategy**

- **Client-Side Caching** (Browser/Client-level)
- **Server-Side Caching** (In-memory cache: Redis, Memcached)
- **Cache Eviction Policies** (LRU, LFU, FIFO)
- **Cache Invalidation** (Write-through, Write-back, Write-around)
- **Distributed Caching** (Sharding, Replication)
- **Cache Consistency** (Eventual consistency, Strong consistency)
- **Dynamic Content Caching**

#### **2. Database Choices**

- **Relational Databases (RDBMS)** (MySQL, PostgreSQL, Oracle)
- **NoSQL Databases** (MongoDB, Cassandra, DynamoDB)
- **Columnar Databases** (HBase, Bigtable)
- **Graph Databases** (Neo4j, Amazon Neptune)
- **Key-Value Stores** (Redis, DynamoDB, Riak)
- **Time-Series Databases** (InfluxDB, TimescaleDB)

#### **3. Replication Strategy**

- **Master-Slave Replication**
- **Master-Master Replication**
- **Synchronous vs. Asynchronous Replication**
- **Quorum-Based Replication** (Cassandra’s consistency model)
- **Replication Lag**
- **Leader-Follower (Raft, Paxos)**

#### **4. Data Sharding and Partitioning**

- **Horizontal vs. Vertical Partitioning**
- **Range-Based Sharding**
- **Hash-Based Sharding**
- **Directory-Based Sharding**
- **Shard Key Selection**
- **Rebalancing Data Across Shards**

#### **5. Distributed Consensus**

- **Leader Election (Paxos, Raft, ZAB - ZooKeeper Atomic Broadcast)**
- **Two-Phase Commit (2PC)**
- **Three-Phase Commit (3PC)**
- **Byzantine Fault Tolerance (BFT)**
- **CAP Theorem** (Consistency, Availability, Partition Tolerance)

#### **6. Redundancy and Fault Tolerance**

- **Data Replication for Redundancy**
- **Active-Active vs. Active-Passive Failover**
- **Geo-Redundancy**
- **RAID Levels (Data Striping, Mirroring)**
- **Hot Standby vs. Cold Standby**

#### **7. Data Consistency Models**

- **Strong Consistency**
- **Eventual Consistency**
- **Causal Consistency**
- **Read-After-Write Consistency**
- **Consistency in Distributed Databases** (Cassandra, DynamoDB, etc.)

#### **8. Data Partitioning Strategies**

- **Range Partitioning**
- **List Partitioning**
- **Hash Partitioning**
- **Composite Partitioning**
- **Partition Pruning**

#### **9. Proxy and Reverse Proxy**

- **Load Balancing with Proxy Servers**
- **Layer 4 vs. Layer 7 Proxies**
- **Reverse Proxy (Nginx, HAProxy, Envoy)**
- **SSL Termination**
- **Caching in Proxy Servers**
- **Global Load Balancers (Anycast, GSLB)**

#### **10. Data Indexing**

- **Single-Column Indexes**
- **Composite Indexes**
- **Full-Text Search Indexes**
- **Bitmap Indexes**
- **Inverted Indexes (for search engines like Elasticsearch)**
- **Secondary Indexes in NoSQL Databases**

#### **11. Event Sourcing and CQRS (Command Query Responsibility Segregation)**

- **Event Log Architecture**
- **Write-Optimized Event Store**
- **Read-Optimized Projections**
- **Data Consistency with Event Sourcing**
- **CQRS in Distributed Systems**

#### **12. Backup and Disaster Recovery**

- **Point-In-Time Recovery (PITR)**
- **Snapshot-based Backups**
- **Incremental vs. Full Backups**
- **Disaster Recovery Plans**
- **Multi-AZ and Multi-Region Backup Strategies**

#### **13. Data Security and Encryption**

- **Data Encryption at Rest** (AES, KMS, HSM)
- **Data Encryption in Transit** (SSL/TLS)
- **Database Access Control** (Role-Based Access Control, Attribute-Based Access Control)
- **Audit Logging and Monitoring**

#### **14. Rate Limiting and Throttling**

- **Token Bucket Algorithm**
- **Leaky Bucket Algorithm**
- **Fixed Window, Sliding Window**
- **Rate Limiting at Proxy/Server Level**

#### **15. Distributed Transactions**

- **2PC and 3PC in Distributed Databases**
- **Sagas (for long-running distributed transactions)**
- **Idempotent Operations**
- **Eventual Consistency and Retry Strategies**

#### **16. Data Streaming and Messaging Systems**

- **Kafka, RabbitMQ, AWS Kinesis**
- **Event-Driven Architectures**
- **Real-Time Data Processing**
- **Stream Partitioning, Offsets, and Consumers**

#### **17. Query Optimization**

- **Indexing Strategies**
- **Query Caching**
- **Use of Materialized Views**
- **Database Query Planning and Execution**

#### **18. Data Deduplication**

- **Content-Addressable Storage**
- **Bloom Filters**
- **Data Hashing for Deduplication**
- **Tracking Unique Data in Streams**

#### **19. Data Compression**

- **Columnar Compression** (Parquet, ORC)
- **Data Deduplication for Storage Efficiency**
- **Lossless vs. Lossy Compression Techniques**

#### **20. API Gateway and Middleware**

- **Routing of Requests (API Gateway as Reverse Proxy)**
- **Rate Limiting at API Gateway**
- **Security at API Gateway (JWT, OAuth2.0)**
- **Request Throttling and Circuit Breakers**

#### **21. Microservice Patterns

- **Idempotency**
- **Circuit Breaker**
- **Retry Pattern**
- **Timeouts**
- **Bulkhead Pattern**
- **Fallback Pattern**
- **Service Discovery**
- **API Gateway Pattern**
- **Distributed Tracing**
- **Sidecar Pattern**
- **Event-Driven Microservices**
- **Database per Service**
- **API Composition Pattern**
- **Saga Pattern** (Choreography and Orchestration)
- **Strangler Fig Pattern**
- **Event Sourcing**
- **CQRS (Command Query Responsibility Segregation)**
- **Service Mesh**




