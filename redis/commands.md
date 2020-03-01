##Basic command
- INFO  get redis server information
- DBSIZE  return the number of existing keys in a redis server
- DEBUG SEGFAULT  crashes the Redis server process by performing an invalid memory access. It can be quite interesting to simulate bugs during the development of your application:
- EXPIRE set the expire time to a key in second time unit
- PERSIST command removes the existing timeout of a given key
- TTL get a key's time to live value in second  time unit
- PTTL command does the same thing, but the return value is in milliseconds rather than seconds
- DEL command removes one or many keys from Redis and returns the number of removed keys
- EXISTS command returns 1 if a certain key exists and 0 if it does not
- PING command returns the string "PONG". It is useful for testing a server/client connection and verifying that Redis is able to exchange data

- CLIENT LIST CLIENT LIST command returns a list of all clients connected to the server, as well as relevant information and statistics about the clients (for example, IP address,name, and idle time).
- CLIENT KILL command terminates a client connection. It is possible to terminate client connections by IP, port, ID, or type


- KEYS 

    list keys inside the system
    ```
    redis> MSET firstname Jack lastname Stuntman age 35
    "OK"
    redis> KEYS *name*
    1) "lastname"
    2) "firstname"
    redis> KEYS a??
    1) "age"
    redis> KEYS *
    1) "lastname"
    2) "age"
    3) "firstname"
    redis> 
    ```

##Operation for String,a string at maximum size of hold 512MB
- SET set a string key value pair
- SETEX command sets a value to a given key and also sets an expiration atomically.
- GET get a string value by a key
- MSET set multiple string key value pairs that separated by space
- MGET get multiple string values by keys separated by space
- INCR increment a integer by 1
- INCRBY increment a integer by specified value
- DECR decrement a integer by specified value
- DECRBY decrement a integer by specified value

##Operation for Bitmaps(Under the hood, a Bitmap is a String)
- SETBIT is used to give a value to a Bitmap offset, and it accepts only 1 or 0.
- GETBIT returns the value of a Bitmap offset
- BITOP requires a destination key, a bitwise operation, and a list of keys to apply to that operation and store the result in the destination key
- BITCOUNT returns the number of bits marked as 1 in a Bitmap
- BITPOS

##Operation for List(it's a LinkedList, fast for insert and delete from the beginning or end of a list)

the maximum number of elements a List could hold is 232-1(4 billion)
- RPUSH insert a element into the end of a List
- LPUSH insert a element into the beginning of a List
- LLEN return the length of a List
- LINDEX return the element at the given index(zero-based)
- LRANGE returns an array with all elements from a given index range
- LPOP removes and returns the first element of a List
- RPOP removes and returns the last element of a List
- RPOPLPUSH Atomically returns and removes the last element (tail) of the list stored at source, and pushes the element at the first element (head) of the list stored at destination
- HKEYS retrieve all field names of a hash
- HVALS retrieve all field values of a hash
- HSCAN when enconter a large hash could use command to incrementally retrieve  field values of a hash
##Operation for Set
- SADD is responsible for adding one or many members to a Set
- SINTER get the intersection of one or more sets
- SDIFF returns an array with all members of the first Set that do not exist in the Sets that follow it
- SUNION returns an array with all members of all Sets
- SREM removes and returns members from a Set
- SISMEMBER checks whether a element exists in a Set
- SMEMBERS returns all members of a Set
- SRANDMEMBER returns random members from a Set
- SCARD returns the count of members of a Set
##Operation for SortedSet
- ZADD add one or more elements to a SortedSet with specified score
- ZRANGE get a range of elements of SortedSet from lowest to highest score
- ZREVRANGE get a range of elements of SortedSet from highest to lowest score
- ZREM remove a member from a SortedSet
- ZSCORE return a member's score from a SortedSet
- ZRANK This returns the member rank (or index) ordered from low to high. The member with the lowest score has rank 0.
- ZREVRANK This returns the member rank (or index) ordered from high to low. The member with the highest score has rank 0.
##Operation for Hash, both key and value are Strings,Internally, a Hash can be a ziplist or a hash table
- HSET sets a value to a field of a given key
- HMSET sets multiple field values to a key, separated by spaces
- HINCRBY increments a field by a given integer
- HGET retrieves a field from a Hash
- HMGET retrieves multiple fields at once
- HDEL deletes a field from a Hash
- HGETALL returns an array of all field/value pairs in a Hash
##Operation for HyperLogLogs(not 100% accurate, but memory efficiency)
- PFADD adds one or many strings to a HyperLogLog.
- PFCOUNT accepts one or many keys as arguments. When a single argument is specified, it returns the approximate cardinality. When multiple keys are specified, it returns the approximate cardinality of the union of all unique elements
- PFMERGE requires a destination key and one or many HyperLogLog keys as arguments
