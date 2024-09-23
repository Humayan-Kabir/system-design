### Database Indexing
> sorts database rows based on some columns.
#### hash indexes
- **pros**
	- O(1) read / write
 - **cons**
	 - keys must be fit in memory 
	 - no range query
#### b-tree indexes [jordan](https://www.youtube.com/watch?v=Z2OaqmxiH20&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=4&pp=iAQB)[algo](https://www.youtube.com/watch?v=K1a2Bk8NrYQ)
- self balancing tree on disk
- no limit on key size 
- range query 
- read speed is high compare to write speed as re-balancing happens.
#### b+ tree indexes [algo](https://youtube.com/watch?v=h6Mw7_S4ai0)

#### LSM tree [rachit-jain](https://www.youtube.com/watch?v=P2xtlLymqqI) [jordan](https://www.youtube.com/watch?v=ciGAVER_erw&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=5)
- no limit on key size
- write speed is faster than b-tree index and slower than hash index.
- supports range query slower than b-tree index as need to go through all SS-TABLE.
- extra cpu usages due to merging of SS-TABLE.
- insert -> WAL -> write in memory tree -> when it is full -> flash it into SS-TABLE
- query -> search in memory tree -> when it is not there -> search in all the table 
	- rather than searching all the elements in a single SS-TABLE, we can create sparse index
- duplicate keys 
	- background process to do compaction (merging two table)
