### Consistency Strategy
#### strong consistency
> Every read request returns the most up-to-date values.
> you need to sacrifice availability and latency to achieve this.
#### eventual consistency
> once data is updated, eventually it returns the updated values after certain time period.

### Distributed consensus
1. **Quorum consensus**
	- Quorum consensus can guarantee consistency for both read and write operations. Let us establish a few definitions first.
	- N = The number of replicas  
	- W = A write quorum of size W. For a write operation to be considered as successful, write operation must be acknowledged from W replicas.  
	- R = A read quorum of size R. For a read operation to be considered as successful, read operation must wait for responses from at least R replicas.
	- If R = 1 and W = N, the system is optimized for a fast read.
	- If W = 1 and R = N, the system is optimized for fast write.
	- If W + R > N, strong consistency is guaranteed (Usually N = 3, W = R = 2).
	- If W + R <= N, strong consistency is not guaranteed.
1. **RAFT**
2. **PAXOS**
