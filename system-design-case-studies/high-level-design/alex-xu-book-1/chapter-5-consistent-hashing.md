### Consistent hashing
Quoted from Wikipedia: "Consistent hashing is a special kind of hashing such that when a
hash table is re-sized and consistent hashing is used, only k/n keys need to be remapped on
average, where k is the number of keys, and n is the number of slots. In contrast, in most
traditional hash tables, a change in the number of array slots causes nearly all keys to be
remapped.
#### steps
1. hash servers and put inside a hash ring, same goes for keys also
2. add virtual nodes which helps to get more even distribution
3. keys are handled by next server in a ring.
#### pros
1. Minimized keys are redistributed when servers are added or removed
2. It is easy to scale horizontally because data are more evenly distributed
3. Mitigate hotspot key problem. Excessive access to a specific shard could cause server
	overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the
	same shard. Consistent hashing helps to mitigate the problem by distributing the data more
	evenly.
#### real world usages
• Partitioning component of Amazon’s Dynamo database 
• Data partitioning across the cluster in Apache Cassandra
• Discord chat application
• Akamai content delivery network 
• Maglev network load balancer
