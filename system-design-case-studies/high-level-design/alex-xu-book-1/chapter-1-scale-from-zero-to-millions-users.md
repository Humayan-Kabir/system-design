### which database to use
1. Relational Database - MySQL, Oracle database, PostgreSQL
	1. good for structured data 
	2. ACID compliance
	3. you can perform join across table
2. NoSQL Database - MongoDB, CouchDB, Cassandra, Dynamo, Neo4j, Redis, Hbase
	1. when required super low latency
	2. when need to store massive amount of data 
	3. good for unstructured data
	4. when need to perform serialization and deserialization.
	5. types - key-value, graph, document, column
### horizontal vs vertical scaling
- vertical scaling (scale-up)
	- add more resources to a single server
	- when load is not too much this can be an option
	- introduce single point of failure
- horizontal scaling (scale-out) 
	- add more server to the pool
	- increase availability and scalability
	- best for large scale application
### load balancer 
1. A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set
2. provides better security
3. provides horizontal scaling and availability
### database replication
- copies data from one database to multiple databases.
- master-slave architecture
	- masters handles only write operation
	- salves handles only read operation
- improves performance more read requests can be handled
- provides reliability
- high availability
- if master goes down one of the slave will be promoted to master
	- it is quite complicated for production system, multi-master, circular replication could help.
### Cache
1. A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent request can be served quickly.
### Cache tier
* The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently

![[cache-access.png]]
#### Consideration for using cache
- important data should be saved to persistent stores
- use only for read heavy system
- eviction policy : LRU, LFU, TTL, FIFO
- consistency : challenging to maintain consistency between data store and cache when scaling to multiple region
- SPOF
	- scale to multiple region
	- put more buffer size than required
### CDN
- it is geo based distributed server to deliver static contents (image, video, css, javascript)

![[cdn-workflow.png]]
#### Consideration of using CDN
1. cost as run by third party
2. need to set appropriate TTL
3. need to set CDN fallback to handle outage
4. invalidation:
	1. using third party API provided by vendor
	2. use version number to support different version
#### Dynamic Content Caching
- It enables the caching of HTML pages that are based on request path, query strings, cookies, and request headers
### Stateful Web Tier
-  Sticky Session In LB
	- reduced LB effectiveness as same request will be routed to same server
	- SPOF if required server goes down
	- limit horizontal scaling as request can't be distributed
	- multi region support difficult
### State Less Web Tier
* remove state from web tier and use global shared data store
* auto scale web tier
### Data Center
- for better availability and scalability we need to scale the systems to multiple region. for each region we can have several data centre
#### challenges
1. **traffic redirection:** effective tools are required, *geo-dns* can used.
2. **data synchronization:** in failover case traffic should be routed to healthy data centre, so we need sync among data centre. netflix implement asynchronous *multi-data centre replication*
3. **test and deployment:** you need to test your system for different region. automatic deployment tools are vital to keep services consistent.
### Message Queue
A message queue is a durable component, stored in memory, that supports asynchronous communication. It serves as a buffer and distributes asynchronous requests

![[message-queue.png]]
### Logging, metrics, automation
1. Logging: Monitoring error logs is important because it helps to identify errors and problems in the system.
2. Metrics: Collecting different types of metrics help us to gain business insights and understand the health status of the system.
	- CPU, Memory, Disk, performance of db tier, cache tier, DAU, revenue.
3. Automation: When a system gets big and complex, we need to build or leverage automation tools to improve productivity.

### Database scaling
1. **vertical scaling**
	- greater risk for SPOF
	- overall cost is high
2. **horizontal scaling**
	1. **sharding**
		- sharding separates large database into smaller manageable parts, each shard holds unique data.
		- *sharding key* known as *partitioning key*, is the most important factor to choose so that data is distributed evenly.
	2. **re-sharding**
		* when certain shard exhausted or full, then it requires to update sharding function or to move data around. consistent hashing is common technique to use.
	3. **celebrity-problem**
		- also known as hotspot key problem. let suppose katty perry, justin bieber all end up to single shard. so, that shard will get huge read request.  so, we can make separate shard for the celebrity.
	4. **join and de-normalization
		- once db is sharded across multiple server, then it is difficult to perform join. one position solution is to *de-normalize* the database so that queries can be performed in a single table.
	 
![[database-sharding.png]]
### Overall HLD

![[alex-xu-hld-chapter-1.png]]
