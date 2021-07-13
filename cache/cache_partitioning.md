###why we need partitioning
leverage multiple computers and memories instead of a single computer

###partitioning algorithm
- range partitioning(need a range table for every type of object )
- hash partitioning

###where to implement partitioning:
- Client side partitioning
- Proxy assisted partitioning( Twemproxy)
- Query routing(Redis Cluster)

###Disadvantage of Partitioning
- Operations involving multiple keys are usually not supported
- transactions involving multiple keys can not be used.
- it is not possible to shard a dataset with a single huge key like a very big sorted set.
- data handling is more complex
- Adding and removing capacity can be complex
