

## Highlights
Tags: [[Distributed Systems]], [[Database]], [[Books]]
Chapter 01: Reliable, Scalable, and Maintainable Applications

Thinking About Data Systems:
   > If you are designing a data system or service, a lot of tricky questions arise. How do you ensure that the data remains correct and complete, even when things go wrong internally? How do you provide consistently good performance to clients, even when parts of your system are degraded? How do you scale to handle an increase in load? What does a good API for the service look like?

[[Reliability]]:
   > • The application performs the function that the user expected. • It  can  tolerate  the  user  making  mistakes  or  using  the  software  in  unexpected ways. • Its  performance  is  good  enough  for  the  required  use  case,  under  the  expected load and data volume. • The system prevents any unauthorized access and abuse.

 * Page 6 (Reliability):
   > "continuing  to  work  correctly,  even  when  things  go wrong."

 * Page 13 (Describing [[Performance]]): 
   > "throughput: number of records we can process per second,"

 * Page 14 (Describing Performance):
   > Latency  and  response  time  are  often  used  synonymously,  but  they are not the same. The response time is what the client sees: besides the actual time to process the request (the service time), it includes network delays and queueing delays. Latency is the duration that a request is waiting to be handled—during which it is latent, await‐ ing service

 * Page 14 (Describing Performance):
   > it is better to use percentiles. If you take your list of response times and sort it from  fastest  to  slowest,  then  the  median  is  the  halfway  point

 * Page 15 (Describing Performance):
   > median  response  time  is  200  ms,  that  means  half  your  requests  return  in  less  than 200 ms, and half your requests take longer than that.

 * Page 15 (Describing Performance): "High  percentiles  of  response  times,  also  known  as  tail  latencies"

 * Page 15 (Describing Performance):
   > Amazon has also observed that a 100 ms increase in response time reduces sales by 1% [20], and others report that a 1-second slowdown reduces a customer sat‐ isfaction metric by 16% [21, 22].

 * Page 16 (Describing Performance): "head-of-line  blocking"

 * Page 16 (Describing Performance):
   > When generating load artificially in order to test the scalability of a system, the loadgenerating client needs to keep sending requests independently of the response time. If the client waits for the previous request to complete before sending the next one, that behavior has the effect of artificially keeping the queues shorter in the test than they would be in reality, which skews the measurements [23].

 * Page 16 (Describing Performance): "tail latency amplification"

 * Page 17 (Describing Performance): "shared-nothing architecture"

Chapter 02: Data Models and Query Languages

 * Page 63 (Summary):
   > 1. Document  databases  target  use  cases  where  data  comes  in  self-contained  docu‐ ments and relationships between one document and another are rare. 2. Graph databases go in the opposite direction, targeting use cases where anything is potentially related to everything.


Chapter 03: [[Storage]] and Retrieval

 * Page 69 (Chapter 3. Storage and Retrieval):
   > On the most fundamental level, a database needs to do two things: when you give it some data, it should store the data, and when you ask it again later, it should give the data back to you.

 * Page 76 (SSTables and LSM-Trees): "Sorted  String  Table,  or  SSTable  for  short"

 * Page 79 ([[B-Trees]]):
   > (A Bloom filter is a memory-efficient data structure for approximating the contents of a set. It can tell you if a key does not appear in the database, and thus saves many unnecessary disk reads for nonexistent keys.)

 * Page 79 (B-Trees):
   > In size-tiered com‐ paction,  newer  and  smaller  SSTables  are  successively  merged  into  older  and  larger SSTables. In leveled compaction, the key range is split up into smaller SSTables and older  data  is  moved  into  separate  "levels,"  which  allows  the  compaction  to  proceed more incrementally and use less disk space.

 * Page 82 (B-Trees):
   > In order to make the database resilient to crashes, it is common for B-tree implemen‐ tations to include an additional data structure on disk: a write-ahead log ([[WAL]], also known as a redo log).

 * Page 82 (B-Trees):
   > Instead  of  overwriting  pages  and  maintaining  a  WAL  for  crash  recovery,  some databases  (like  LMDB)  use  a  copy-on-write  scheme

 * Page 83 (Comparing B-Trees and LSM-Trees):
   > In general, pages can be positioned anywhere on disk; there is nothing requiring pages with nearby key ranges to be nearby on disk. If a query needs to scan over a large part of the key range in sorted order, that page-by-page layout can be ineffi‐ cient, because a disk seek may be required for every page that is read. Many B- tree implementations therefore try to lay out the tree so that leaf pages appear in sequential order on disk. However, it's difficult to maintain that order as the tree grows. By contrast, since LSM-trees rewrite large segments of the storage in one go during merging, it's easier for them to keep sequential keys close to each other on disk.

 * Page 84 (Comparing B-Trees and LSM-Trees):
   > is known as write ampli‐ fication. It is of particular concern on SSDs, which can only overwrite blocks a limi‐ ted number of times before wearing out.

 * Page 86 (Other [[Indexing]] Structures): "is  known  as  a  heap  file"

 * Page 86 (Other Indexing Structures): "This  is  known  as  a  clustered  index."

 * Page 86 (Other Indexing Structures): "covering index or index with included columns,"

 * Page 87 (Other Indexing Structures):
   > The most common type of multi-column index is called a concatenated index, which

 * Page 87 (Other Indexing Structures):
   > An  interesting  idea  is  that  multi-dimensional  indexes  are  not  just  for  geographic

 * Page 89 (Other Indexing Structures):
   > RAMCloud  is  an  open  source,  in-memory  key-value  store  with durability (using a log-structured approach for the data in memory as well as the data on disk) [43]. Redis and Couchbase provide weak durability by writing to disk asyn‐ chronously.

 * Page 90 (Transaction Processing or Analytics?):
   > Further  changes  to  storage  engine  design  will  probably  be  needed  if  non-volatile memory (NVM) technologies become more widely adopted [46]. At present, this is a new area of research, but it is worth keeping an eye on in the future.

 * Page 93 (Stars and Snowflakes: Schemas for Analytics):
   > These  include  Apache  Hive,  Spark  SQL,  Cloudera Impala, Facebook Presto, Apache Tajo, and Apache Drill [52, 53]. Some of them are based on ideas from Google's Dremel [54].

 * Page 93 (Stars and Snowflakes: Schemas for Analytics):
   > known  as  a  star  schema  (also  known  as  dimen‐ sional modeling [55]).

 * Page 94 (Stars and Snowflakes: Schemas for Analytics): "dimension tables."

 * Page 94 (Stars and Snowflakes: Schemas for Analytics): "who, what, where, when, how, and why of the event."

 * Page 96 (Column-Oriented Storage):
   > The idea behind column-oriented storage is simple: don't store all the values from one row together, but store all the values from each column together instead.

 * Page 97 (Column-Oriented Storage): "data warehouses is bitmap encoding"

 * Page 99 (Sort Order in Column Storage):
   > Operators,  such  as  the  bitwise  AND  and  OR  described  previously,  can  be designed to operate on such chunks of compressed column data directly. This techni‐ que is known as vectorized processing

 * Page 100 (Sort Order in Column Storage):
   > The  administrator  of  the  database  can  choose  the  columns  by  which  the table  should  be  sorted,  using  their  knowledge  of  common  queries.  For  example,  if queries often target date ranges, such as the last month, it might make sense to make date_key the first sort key. Then the query optimizer can scan only the rows from the last month, which will be much faster than scanning all rows.

 * Page 101 (Aggregation: Data Cubes and Materialized Views):
   > One way of creating such a cache is a materialized view. In a relational data model, it

 * Page 102 (Aggregation: Data Cubes and Materialized Views):
   > A common special case of a materialized view is known as a data cube or OLAP cube




Chapter 04: Encoding and Evolution

 * Page 112 (Formats for Encoding Data):
   > Backward compatibility Newer code can read data that was written by older code. Forward compatibility Older code can read data that was written by newer code.

   forward compatibility

 * Page 113 (Language-Specific Formats):
   > The trans‐ lation from the in-memory representation to a byte sequence is called encoding (also known  as  serialization  or  marshalling),  and  the  reverse  is  called  decoding  (parsing, deserialization, unmarshalling).ii

 * Page 115 (JSON, XML, and Binary Variants):
   > The  difficulty  of  getting  different  organizations  to  agree  on  anything  outweighs most other concerns.

 * Page 123 (Avro):
   > This means that the binary data can only be decoded correctly if the code reading the data is using the exact  same  schema  as  the  code  that  wrote  the  data.  Any  mismatch  in  the  schema between the reader and the writer would mean incorrectly decoded data.

 * Page 126 (Avro): "Dynamically generated schemas"

 * Page 128 (Modes of Dataflow):
   > volv‐ ability (making change easy by allowing you to upgrade different parts of your system independently, and not having to change everything at once)

 * Page 128 (Modes of Dataflow):
   > Compatibility is a rela‐ tionship between one process that encodes the data, and another process that decodes it.

 * Page 129 (Dataflow Through Databases):
   > in that case you can think of storing something in the database as sending a message to your future self.

 * Page 130 (Dataflow Through Databases): "data outlives code."

 * Page 132 (Dataflow Through Services: REST and RPC):
   > called a serviceoriented  architecture  (SOA),  more  recently  refined  and  rebranded  as  microservices architecture [31, 32].

 * Page 132 (Dataflow Through Services: REST and RPC):
   > For example, each service should be owned by one team, and that team should be able to release new versions of the service frequently, without having to coordinate with other teams.

 * Page 134 (Dataflow Through Services: REST and RPC): "mechanism  for  deduplication  (idempotence)"

 * Page 136 (Message-Passing Dataflow):
   > Thus, you only need backward compatibility on requests, and forward compatibility on responses.

 * Page 137 (Message-Passing Dataflow):
   > This  communication  pattern  is  asynchronous:  the  sender  doesn't  wait for the message to be delivered, but simply sends it and then forgets about it.

 * Page 137 (Message-Passing Dataflow):
   > one process sends a message to a named queue or topic, and the broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic







Chapter 05: [[Replication]]

 * Page 151 (Chapter 5. Replication):
   > All of the diffi‐ culty  in  replication  lies  in  handling  changes  to  replicated  data,

 * Page 156 (Handling Node Outages):
   > PostgreSQL  calls  it  the  log  sequence  number,  and MySQL calls it the binlog coordinates.

 * Page 159 (Implementation of Replication Logs): "but by default MySQL now switches to rowbased replication"

 * Page 160 (Implementation of Replication Logs):
   > a WAL con‐ tains details of which bytes were changed in which disk blocks. This makes replica‐ tion closely coupled to the storage engine. If the database changes its storage format from  one  version  to  another,  it  is  typically  not  possible  to  run  different  versions  of the database software on the leader and the followers.

 * Page 163 (Reading Your Own Writes): "we need read-after-write consistency, also known as read-your-writes consistency"

 * Page 163 (Reading Your Own Writes):
   > When  reading  something  that  the  user  may  have  modified,  read  it  from  the leader;

 * Page 163 (Reading Your Own Writes):
   > you could track the time of the last update and, for one minute after the last update, make all reads from the leader. You could also monitor the replication lag on followers and pre‐ vent queries on any follower that is more than one minute behind the leader.

 * Page 164 (Monotonic Reads): "moving backward in time."

 * Page 165 (Consistent Prefix Reads):
   > One way of achieving monotonic reads is to make sure that each user always makes their  reads  from  the  same  replica  (different  users  can  read  from  different  replicas). For example, the replica can be chosen based on a hash of the user ID, rather than randomly. However, if that replica fails, the user's queries will need to be rerouted to another replica.

 * Page 166 (Consistent Prefix Reads):
   > This guarantee says that if a sequence of writes happens in a certain order, then anyone reading those writes will see them appear in the same order.

 * Page 173 (Handling Write Conflicts):
   > If a timestamp is used, this technique is known as  last  write  wins  (LWW).

 * Page 174 (Handling Write Conflicts):
   > Operational transformation [42] is the conflict resolution algorithm behind col‐ laborative  editing  applications  such  as  Etherpad  [30]  and  Google  Docs  [31].  It was designed particularly for concurrent editing of an ordered list of items, such as the list of characters that constitute a text document.

 * Page 175 (Multi-Leader Replication Topologies):
   > To prevent infinite replication loops, each node is given a unique identifier, and in the replication log, each write is tagged with the identifiers of all the nodes it has passed through

 * Page 177 (Writing to the Database When a Node Is Down):
   > Dynamo system [37].vi  Riak,  Cassandra,  and  Voldemort  are  open  source  datastores  with  leaderless replication  models  inspired  by  Dynamo,  so  this  kind  of  database  is  also  known  as Dynamo-style.

 * Page 179 (Writing to the Database When a Node Is Down):
   > Read repair When a client makes a read from several nodes in parallel, it can detect any stale responses. For example, in Figure 5-10, user 2345 gets a version 6 value from rep‐ lica 3 and a version 7 value from replicas 1 and 2. The client sees that replica 3 has a stale value and writes the newer value back to that replica. This approach works well for values that are frequently read.

 * Page 179 (Writing to the Database When a Node Is Down):
   > values that are rarely read may be missing from some replicas and thus have reduced durability,

 * Page 183 (Sloppy Quorums and Hinted Handoff):
   > Is it better to return errors to all requests for which we cannot reach a quorum of w or r nodes? • Or  should  we  accept  writes  anyway,  and  write  them  to  some  nodes  that  are reachable but aren't among the n nodes on which the value usually lives?

 * Page 183 (Sloppy Quorums and Hinted Handoff): "sloppy  quorum"

 * Page 184 (Detecting Concurrent Writes): "hinted  handoff."

 * Page 186 (Detecting Concurrent Writes): "called  last  write  wins  (LWW),"

 * Page 186 (Detecting Concurrent Writes):
   > a  recommended  way  of  using  Cassandra  is  to  use  a UUID as the key, thus giving each write operation a unique key

 * Page 187 (Detecting Concurrent Writes):
   > we  simply  call  two  operations concurrent if they are both unaware of each other,

 * Page 187 (Detecting Concurrent Writes):
   > Consequently,  two  events that occur some distance apart cannot possibly affect each other if the time between the events is shorter than the time it takes light to travel the distance between them.

 * Page 190 (Detecting Concurrent Writes): "Riak  calls these concurrent values siblings."

 * Page 191 (Detecting Concurrent Writes): "s is called a version vector"

 * Page 191 (Detecting Concurrent Writes): "dotted version vector"

 * Page 191 (Detecting Concurrent Writes): "causal context.)"


Chapter 06:  [[Partitioning]]

 * Page 201 (Partitioning and Replication):
   > If the partitioning is unfair, so that some partitions have more data or queries than others, we call it skewed.

 * Page 201 (Partitioning and Replication): "skewed."

 * Page 201 (Partitioning and Replication):
   > A partition with disproportion‐ ately high load is called a hot spot.

 * Page 202 (Partitioning by Key Range):
   > In order to distribute the data evenly, the partition bound‐ aries need to adapt to the data.

 * Page 204 (Partitioning by Hash of Key): "case the technique is sometimes known as consistent hashing)."

 * Page 204 (Partitioning by Hash of Key):
   > table in Cassandra can be declared with a compound primary key

 * Page 205 (Skewed Workloads and Relieving Hot Spots):
   > a simple technique is to add a random number to the beginning or end of the key. Just a two-digit decimal random number would split the writes to the key evenly across 100 different keys, allowing those keys to be distributed to different partitions.

 * Page 206 (Partitioning Secondary Indexes by Document):
   > The  problem  with  secondary  indexes  is  that  they  don't  map  neatly  to  partitions. There  are  two  main  approaches  to  partitioning  a  database  with  secondary  indexes: document-based partitioning and term-based partitioning.

 * Page 207 (Partitioning Secondary Indexes by Document):
   > document-partitioned  index  is  also  known  as  a  local  index  (as  opposed  to  a  global index, described in the next section).

 * Page 207 (Partitioning Secondary Indexes by Document):
   > Thus, if you want to search for red cars, you need to send the query to all partitions, and combine all the results you get back.

 * Page 207 (Partitioning Secondary Indexes by Document): "scatter/gather"

 * Page 207 (Partitioning Secondary Indexes by Document):
   > Most database vendors recommend that you structure your partitioning scheme so that secondary index queries can be served from a single partition, but that is not always possible, especially when you're using multiple secondary indexes in a single query (such as filtering cars by color and by make at the same time).

 * Page 208 (Partitioning Secondary Indexes by Document):
   > Figure  6-5  illustrates  what  this  could  look  like:  red  cars  from  all  partitions  appear under color:red in the index, but the index is partitioned so that colors starting with the letters a to r appear in partition 0 and colors starting with s to z appear in parti‐ tion  1.  The  index  on  the  make  of  car  is  partitioned  similarly  (with  the  partition boundary being between f and h). We call this kind of index term-partitioned,

 * Page 208 (Partitioning Secondary Indexes by Document):
   > The  advantage  of  a  global  (term-partitioned)  index  over  a  document-partitioned index is that it can make reads more efficient: rather than doing scatter/gather over all  partitions,  a  client  only  needs  to  make  a  request  to  the  partition  containing  the term that it wants.

 * Page 209 (Rebalancing Partitions):
   > The process of moving load from one node in the cluster to another is called reba‐ lancing.

 * Page 210 (Strategies for Rebalancing):
   > Only entire partitions are moved between nodes. The number of partitions does not change, nor does the assignment of keys to partitions. The only thing that changes is the assignment of partitions to nodes. This change of assignment is not immediate— it  takes  some  time  to  transfer  a  large  amount  of  data  over  the  network—so  the  old assignment of partitions is used for any reads and writes that happen while the trans‐ fer is in progress.

 * Page 211 (Strategies for Rebalancing):
   > The  best  performance  is achieved  when  the  size  of  partitions  is  "just  right,"  neither  too  big  nor  too  small, which can be hard to achieve if the number of partitions is fixed but the dataset size varies.

 * Page 212 (Strategies for Rebalancing):
   > In  the  case  of  HBase,  the  transfer  of  partition  files  happens  through  HDFS,  the underlying distributed filesystem [3].

 * Page 213 (Operations: Automatic or Manual Rebalancing):
   > in other words, to have a fixed number of par‐ titions per node [23, 27, 28].

 * Page 213 (Operations: Automatic or Manual Rebalancing):
   > (the system decides automat‐ ically when to move partitions from one node to another, without any administrator interaction)

 * Page 213 (Operations: Automatic or Manual Rebalancing):
   > (the assignment of partitions to nodes is explicitly con‐ figured  by  an  administrator,  and  only  changes  when  the  administrator  explicitly reconfigures it)

 * Page 213 (Operations: Automatic or Manual Rebalancing):
   > However, it can be unpredictable. Rebalancing is an expensive operation, because it requires rerouting requests and moving a large amount of data from one node to another. If it is not done carefully, this process can overload the network or the nodes and harm the performance of other requests while the rebalancing is in progress.

 * Page 214 (Request Routing):
   > For that reason, it can be a good thing to have a human in the loop for rebalancing. It's  slower  than  a  fully  automatic  process,  but  it  can  help  prevent  operational surprises.

 * Page 214 (Request [[Routing]]):
   > 1. Allow clients to contact any node (e.g., via a round-robin load balancer). If that node coincidentally owns the partition to which the request applies, it can handle the  request  directly;  otherwise,  it  forwards  the  request  to  the  appropriate  node, receives the reply, and passes the reply along to the client. 2. Send all requests from clients to a routing tier first, which determines the node that  should  handle  each  request  and  forwards  it  accordingly.  This  routing  tier does not itself handle any requests; it only acts as a partition-aware load balancer. 3. Require that clients be aware of the partitioning and the assignment of partitions to  nodes.  In  this  case,  a  client  can  connect  directly  to  the  appropriate  node, without any intermediary.

 * Page 215 (Request Routing):
   > Many distributed data systems rely on a separate coordination service such as Zoo‐ Keeper to keep track of this cluster metadata,

 * Page 216 (Summary):
   > MongoDB has a similar architecture, but it relies on its own config server implemen‐ tation and mongos daemons as the routing tier.

 * Page 216 (Summary): "they use a gossip protocol amon"

 * Page 216 (Summary):
   > This model puts more complexity in the database nodes but avoids the dependency on an external coordination service such as ZooKeeper.

 * Page 216 (Summary):
   > When using a routing tier or when sending requests to a random node, clients still need  to  find  the  IP  addresses  to  connect  to.  These  are  not  as  fast-changing  as  the assignment of partitions to nodes, so it is often sufficient to use DNS for this purpose.

 * Page 216 (Summary): "massively  parallel  processing  (MPP)  relational  database  products,"

Chapter 07: [[Transactions]] 

 * Page 223 (The Meaning of ACID): "ACID  has  unfortunately  become  mostly  a  mar‐ keting term."

 * Page 224 (The Meaning of ACID):
   > The system can only be in the state it was before the operation or after the operation, not something in between.

 * Page 224 (The Meaning of [[ACID]]):
   > The ability to abort a transaction on error and have all writes from that transaction discarded is the defining feature of ACID atomicity. Perhaps abortability would have been  a  better  term  than  atomicity,  but  we  will  stick  with  atomicity  since  that's  the usual word.

 * Page 226 (The Meaning of ACID):
   > Durability is the promise that once a transaction has com‐ mitted  successfully,  any  data  it  has  written  will  not  be  forgotten,  even  if  there  is  a hardware fault or the database crashes.

 * Page 228 (Single-Object and Multi-Object Operations):
   > the database saves you from having to worry about partial failure, by giv‐ ing an all-or-nothing guarantee.

 * Page 228 (Single-Object and Multi-Object Operations):
   > if one transaction makes several writes, then another transaction should see either all or none of those writes, but not some subset.

 * Page 230 (Single-Object and Multi-Object Operations):
   > Atomicity can be implemented using a log for crash recov‐ ery  (see  "Making  B-trees  reliable"  on  page  82),  and  isolation  can  be  implemented using a lock on each object (allowing only one thr

 * Page 230 (Single-Object and Multi-Object Operations):
   > and  isolation  can  be  implemented using a lock on each object (allowing only one thread to access an object at any one time).

 * Page 230 (Single-Object and Multi-Object Operations):
   > have been dubbed "light‐ weight  transactions"

 * Page 232 (Single-Object and Multi-Object Operations):
   > This is a shame, because the whole point of aborts is to enable safe retries.

 * Page 232 (Single-Object and Multi-Object Operations):
   > If the transaction actually succeeded, but the network failed while the server tried to acknowledge the successful commit to the client (so the client thinks it failed), then retrying the transaction causes it to be performed twice—unless you have an additional application-level deduplication mechanism in place. • If  the  error  is  due  to  overload,  retrying  the  transaction  will  make  the  problem worse,  not  better.  To  avoid  such  feedback  cycles,  you  can  limit  the  number  of retries,  use  exponential  backoff,  and  handle  overload-related  errors  differently from other errors (if possible). • It is only worth retrying after transient errors (for example due to deadlock, iso‐ lation  violation,  temporary  network  interruptions,  and  failover);  after  a  perma‐ nent error (e.g., constraint violation) a retry would be pointless. • If the transaction also has side effects outside of the database, those side effects may happen even if the transaction is aborted. For example, if you're sending an email, you wouldn't want to send the email again every time you retry the trans‐ action. If you want to make sure that several different systems either commit or abort  together,  two-phase  commit  can  help  (we  will  discuss  this  in  "Atomic Commit and Two-Phase Commit (2PC)" on page 354).

 * Page 232 (Single-Object and Multi-Object Operations):
   > • If  the  client  process  fails  while  retrying,  any  data  it  was  trying  to  write  to  the database is lost.

 * Page 233 (Weak Isolation Levels):
   > For that reason, databases have long tried to hide concurrency issues from applica‐ tion developers by providing transaction isolation. In theory, isolation should make your life easier by letting you pretend that no concurrency is happening: serializable isolation means that the database guarantees that transactions have the same effect as if they ran serially (i.e., one at a time, without any concurrency).

 * Page 233 (Weak Isolation Levels):
   > but that misses the point. Even many popular relational data‐ base  systems  (which  are  usually  considered  "ACID")  use  weak  isolation,  so  they wouldn't necessarily have prevented these bugs from occurring.

 * Page 234 (Read Committed):
   > 1. When reading from the database, you will only see data that has been committed (no dirty reads). 2. When writing to the database, you will only overwrite data that has been com‐ mitted (no dirty writes).

 * Page 236 (Read Committed):
   > Only  one  transaction  can  hold  the  lock  for  any  given  object;  if another  transaction  wants  to  write  to  the  same  object,  it  must  wait  until  the  first transaction is committed or aborted before it can acquire the lock and continue. This locking is done automatically by databases in read committed mode (or stronger iso‐ lation levels).

 * Page 236 (Read Committed): "would be to use the same lock,"

 * Page 237 ([[Snapshot Isolation ]]and Repeatable Read):
   > the database remembers both the old com‐ mitted value and the new value set by the transaction that currently holds the write lock. While the transaction is ongoing, any other transactions that read the object are simply  given  the  old  value.  Only  when  the  new  value  is  committed  do  transactions switch over to reading the new value.

 * Page 237 (Snapshot Isolation and Repeatable Read):
   > At the time of writing, the only mainstream databases that use locks for read committed isolation are IBM DB2 and Microsoft SQL Server in the read_committed_snapshot=off configuration

 * Page 238 (Snapshot Isolation and Repeatable Read):
   > This  anomaly  is  called  a  nonrepeatable  read  or  read  skew:  if  Alice  were  to  read  the

 * Page 239 (Snapshot Isolation and Repeatable Read):
   > a  key  principle  of  snapshot  isolation  is  readers never block writers, and writers never block readers.

 * Page 239 (Snapshot Isolation and Repeatable Read): "this technique is known as multiversion concurrency control (MVCC)"

 * Page 239 (Snapshot Isolation and Repeatable Read):
   > A typical approach is that read committed uses a separate snapshot for each query, while snapshot isolation uses the same snapshot for an entire transaction.

 * Page 239 (Snapshot Isolation and Repeatable Read):
   > To be precise, transaction IDs are 32-bit integers, so they overflow after approximately 4 billion transac‐ tions. PostgreSQL's vacuum process performs cleanup which ensures that overflow does not affect the data.

 * Page 240 (Snapshot Isolation and Repeatable Read):
   > An  update  is  internally  translated  into  a  delete  and  a  create.

 * Page 241 (Snapshot Isolation and Repeatable Read):
   > 1. At the start of each transaction, the database makes a list of all the other transac‐ tions that are in progress (not yet committed or aborted) at that time. Any writes that  those  transactions  have  made  are  ignored,  even  if  the  transactions  subse‐ quently commit. 2. Any writes made by aborted transactions are ignored. 3. Any writes made by transactions with a later transaction ID (i.e., which started after  the  current  transaction  started)  are  ignored,  regardless  of  whether  those transactions have committed. 4. All other writes are visible to the application's queries.

 * Page 242 (Preventing Lost Updates):
   > called serializable, and in PostgreSQL and MySQL it is called repeatable read [23].

 * Page 243 (Preventing Lost Updates):
   > The lost update problem can occur if an application reads some value from the data‐ base,  modifies  it,  and  writes  back  the  modified  value  (a  read-modify-write  cycle).

 * Page 244 (Preventing Lost Updates): "known  as  cursor  stability"

 * Page 244 (Preventing Lost Updates):
   > Unfortunately,  object-relational  mapping  frameworks  make  it  easy  to  accidentally write  code  that  performs  unsafe  read-modify-write  cycles  instead  of  using  atomic operations provided by the database [38]. That's not a problem if you know what you are  doing,  but  it  is  potentially  a  source  of  subtle  bugs  that  are  difficult  to  find  by testing.

 * Page 244 (Preventing Lost Updates):
   > This  works,  but  to  get  it  right,  you  need  to  carefully  think  about  your  application logic.  It's  easy  to  forget  to  add  a  necessary  lock  somewhere  in  the  code,  and  thus introduce a race condition.

 * Page 244 (Preventing Lost Updates):
   > The FOR UPDATE clause indicates that the database should take a lock on all rows returned by this query.

 * Page 246 (Write Skew and Phantoms):
   > replicated databases is to allow concurrent writes to create several conflicting versions of a value (also known as siblings), and to use application code or special data structures to resolve and merge these versions after the fact.

 * Page 246 (Write Skew and Phantoms):
   > Atomic operations can work well in a replicated context, especially if they are com‐ mutative (i.e., you can apply them in a different order on different replicas, and still get the same result). For example, incrementing a counter or adding an element to a set  are  commutative  operations.  That  is  the  idea  behind  Riak  2.0  datatypes,  which prevent lost updates across replicas. When a value is concurrently updated by differ‐ ent  clients,  Riak  automatically  merges  together  the  updates  in  such  a  way  that  no updates are lost [39].

 * Page 246 (Write Skew and Phantoms): "Unfortunately, LWW is the default in many replicated databases."

 * Page 246 (Write Skew and Phantoms):
   > automatically by the database, or by manual safeguards such as using locks or atomic write operations.

 * Page 247 (Write Skew and Phantoms): "snapshot isolation,"

 * Page 247 (Write Skew and Phantoms): "write  skew"

 * Page 248 (Write Skew and Phantoms):
   > You  can  think  of  write  skew  as  a  generalization  of  the  lost  update  problem.  Write skew  can  occur  if  two  transactions  read  the  same  objects,  and  then  update  some  of those objects (different transactions may update different objects). In the special case where  different  transactions  update  the  same  object,  you  get  a  dirty  write  or  lost update anomaly (depending on the timing).

 * Page 250 (Write Skew and Phantoms):
   > The steps may occur in a different order. For example, you could first make the write, then the SELECT query, and finally decide whether to abort or commit based on the result of the query.

 * Page 251 ([[Serializability]]):
   > like  the  examples  we  discussed, phantoms can lead to particularly tricky cases of write skew.

 * Page 251 (Serializability): "materializing conflicts,"

 * Page 252 (Actual Serial Execution):
   > • Literally executing transactions in a serial order (see "Actual Serial Execution" on page 252) • Two-phase locking (see "Two-Phase Locking (2PL)" on page 257), which for sev‐ eral decades was the only viable option • Optimistic concurrency control techniques such as serializ

 * Page 252 (Actual Serial Execution): "• Optimistic concurrency control techniques such as serializable snapshot isolation"

 * Page 253 (Actual Serial Execution):
   > A system designed for single-threaded execution can sometimes  perform  better  than  a  system  that  supports  concurrency,  because  it  can avoid  the  coordination  overhead  of  locking.

 * Page 254 (Actual Serial Execution):
   > Instead, the application must submit the entire transaction code to the database ahead of time, as a stored procedure.

 * Page 255 (Actual Serial Execution):
   > If a transaction needs to use the current date and time, for example, it must do so through special deterministic APIs.

 * Page 255 (Actual Serial Execution):
   > but for applications with high write throughput, the single-threaded transaction processor can become a serious bottleneck.

 * Page 256 (Actual Serial Execution):
   > then each partition can have its own transaction processing thread running independently from the others. In this case, you can give each CPU core  its  own  partition,  which  allows  your  transaction  throughput  to  scale  linearly with the number of CPU cores [47].

 * Page 256 (Actual Serial Execution):
   > The  stored procedure needs to be performed in lock-step across all partitions to ensure serializa‐ bility across the whole system.

 * Page 256 (Actual Serial Execution): "This approach is known as anti-caching, as previously"

 * Page 258 (Two-Phase Locking (2PL)): "shared mode or in exclusive mode"

 * Page 258 ([[Two-Phase Locking]] (2PL)):
   > • If a transaction wants to read an object, it must first acquire the lock in shared mode. Several transactions are allowed to hold the lock in shared mode simulta‐ neously,  but  if  another  transaction  already  has  an  exclusive  lock  on  the  object, these transactions must wait. • If a transaction wants to write to an object, it must first acquire the lock in exclu‐ sive  mode.  No  other  transaction  may  hold  the  lock  at  the  same  time  (either  in shared  or  in  exclusive  mode),  so  if  there  is  any  existing  lock  on  the  object,  the transaction must wait. • If  a  transaction  first  reads  and  then  writes  an  object,  it  may  upgrade  its  shared lock  to  an  exclusive  lock.  The  upgrade  works  the  same  as  getting  an  exclusive lock directly.

 * Page 258 (Two-Phase Locking (2PL)):
   > • After a transaction has acquired the lock, it must continue to hold the lock until the  end  of  the  transaction  (commit  or  abort).  This  is  where  the  name  "twophase"  comes  from:  the  first  phase  (while  the  transaction  is  executing)  is  when the  locks  are  acquired,  and  the  second  phase  (at  the  end  of  the  transaction)  is when all the locks are released.

 * Page 258 (Two-Phase Locking (2PL)):
   > Since so many locks are in use, it can happen quite easily that transaction A is stuck waiting  for  transaction  B  to  release  its  lock,  and  vice  versa.  This  situation  is  called deadlock.  The  database  automatically  detects  deadlocks  between  transactions  and aborts  one  of  them  so  that  the  others  can  make  progress.  The  aborted  transaction needs to be retried by the application.

 * Page 258 (Two-Phase Locking (2PL)):
   > is  performance:  transaction  throughput  and  response times  of  queries  are  significantly  worse  under  two-phase  locking  than  under  weak isolation.

 * Page 260 (Two-Phase Locking (2PL)):
   > The key idea here is that a predicate lock applies even to objects that do not yet exist in  the  database,  but  which  might  be  added  in  the  future  (phantoms).  If  two-phase locking  includes  predicate  locks,  the  database  prevents  all  forms  of  write  skew  and other race conditions, and so its isolation becomes serializable.

 * Page 260 (Two-Phase Locking (2PL)):
   > most databases with 2PL actually implement index-range locking (also known as nextkey locking), which is a simplified approximation of predicate locking [41, 50].

 * Page 261 (Serializable [[Snapshot Isolation]] (SSI)):
   > If there is no suitable index where a range lock can be attached, the database can fall back to a shared lock on the entire table. This will not be good for performance, since it will stop all other transactions writing to the table, but it's a safe fallback position.

 * Page 262 (Serializable Snapshot Isolation (SSI)):
   > On top of snapshot isolation, SSI adds an  algorithm  for  detecting  serialization  conflicts  among  writes  and  determining which transactions to abort.

 * Page 262 (Serializable Snapshot Isolation (SSI)): "the premise may no longer be true."

 * Page 265 (Serializable Snapshot Isolation (SSI)):
   > the lock acts as a tripwire: it simply notifies the transactions that the data they read may no longer be up to date.

 * Page 265 (Serializable Snapshot Isolation (SSI)):
   > but the bookkeeping overhead can become significant. Less detailed tracking is faster, but may lead to more transac‐ tions being aborted than strictly necessary.

 * Page 265 (Serializable Snapshot Isolation (SSI)):
   > Compared to two-phase locking, the big advantage of serializable snapshot isolation is that one transaction doesn't need to block waiting for locks held by another trans‐ action. Like under snapshot isolation, writers don't block readers, and vice versa.

 * Page 265 (Serializable Snapshot Isolation (SSI)):
   > In particular, read-only queries can run on a consistent snapshot without requiring any locks, which is very appealing for read-heavy workloads.

 * Page 266 (Summary):
   > so SSI requires that read-write transactions be fairly short (longrunning read-only transactions may be okay). However, SSI is probably less sensitive to slow transactions than two-phase locking or serial execution.

Chapter 08: The Trouble with Distributed Systems

 * Page 273 (Chapter 8. The Trouble with Distributed Systems): "anything that can go wrong will go wrong.i"

 * Page 274 (Faults and Partial Failures):
   > but that is mostly just a consequence of badly written software

 * Page 275 (Cloud Computing and Supercomputing): "a partial failure."

 * Page 276 (Cloud Computing and Supercomputing): "build  fault-tolerance  mechanisms  into  the  software."

 * Page 277 (Unreliable Networks): "In distributed systems, suspicion, pessimism, and paranoia pay off."

 * Page 278 (Unreliable [[Networks]]):
   > it's  comparatively cheap  because  it  requires  no  special  hardware,  it  can  make  use  of  commoditized cloud  computing  services,  and  it  can  achieve  high  reliability  through  redundancy across multiple geographically distributed datacenters.

 * Page 279 (Network Faults in Practice):
   > The usual way of handling this issue is a timeout: after some time you give up waiting

 * Page 279 (Network Faults in Practice):
   > since it doesn't guard against human error (e.g., misconfig‐ ured switches), which is a major cause of outages.

 * Page 280 (Detecting Faults):
   > will helpfully close or refuse TCP connections by sending a RST or FIN packet in reply.

 * Page 281 ([[Timeouts]] and Unbounded Delays):
   > Conversely,  if  something  has  gone  wrong,  you  may  get  an  error  response  at  some level of the stack, but in general you have to assume that you will get no response at all. You can retry a few times (TCP retries transparently, but you may also retry at the application level), wait for a timeout to elapse, and eventually declare the node dead if you don't hear back within the timeout.

 * Page 281 (Timeouts and Unbounded Delays):
   > A long timeout means a long wait until a node is declared dead (and during this time, users may have to wait or see error messages).

 * Page 281 (Timeouts and Unbounded Delays):
   > when in fact it has only suffered a temporary slowdown (e.g., due to a load spike on the node or the network).

 * Page 281 (Timeouts and Unbounded Delays):
   > it could happen that the node actually wasn't dead but only slow to respond due to overload; transferring its load to other nodes can cause a cascading failure (in the extreme case, all nodes declare each other dead, and every‐ thing stops working). Imagine a fictitious system with a network that guaranteed a maximum delay forpackets—every packet is either delivered within some time d, or it is lost, but deliverynever takes longer than d. Furthermore, assume that you can guarantee that a non failed node always handles a request within some time r. In this case, you could guarantee that every successful request receives a response within time 2d + r—and if you don’t receive a response within that time, you know that either the network or the remote node is not working. If this was true, 2d + r would be a reasonable timeout to use.

 * Page 282 (Timeouts and Unbounded Delays): "unbounded  delays"

 * Page 282 (Timeouts and Unbounded Delays):
   > it's not sufficient for the system to be fast most of the time: if your timeout is low, it only takes a transient spike in round-trip times to throw the system off-balance.

 * Page 282 (Timeouts and Unbounded Delays):
   > On a busy network link, a packet may have to wait a while until it can get a slot (this is called network congestion).

 * Page 282 (Timeouts and Unbounded Delays):
   > • In virtualized environments, a running operating system is often paused for tens of milliseconds while another virtual machine uses a CPU core. During this time, the  VM  cannot  consume  any  data  from  the  network,  so  the incoming  data  is queued  (buffered)  by  the  virtual  machine  monitor  [26], further  increasing  the variability of network delays.

 * Page 282 (Timeouts and Unbounded Delays):
   > Imagine  a  fictitious  system  with  a  network  that  guaranteed  a  maximum  delay  for packets—every packet is either delivered within some time d, or it is lost, but delivery never takes longer than d. Furthermore, assume that you can guarantee that a nonfailed node always handles a request within some time r. In this case, you could guar‐ antee that every successful request receives a response within time 2d + r—and if you don't  receive  a  response  within  that  time,  you  know  that  either  the  network  or  the remote node is not working. If this was true, 2d + r would be a reasonable timeout to use.

   d = delivery time

   r = handle request

   timeout = 2d + r


 * Page 283 (Timeouts and Unbounded Delays): "which  is  calculated  from  observed  round-trip  times"

 * Page 283 (Timeouts and Unbounded Delays):
   > UDP is a good choice in situations where delayed data is worthless. For example, in a VoIP phone call, there probably isn't enough time to retransmit a lost packet before its  data  is  due  to  be  played  over  the  loudspeakers.  In  this  case,  there's  no  point  in retransmitting the packet—the application must instead fill the missing packet's time slot  with  silence  (causing  a  brief  interruption  in  the  sound)  and  move  on  in  the stream. The retry happens at the human layer instead. ("Could you repeat that please? The sound just cut out for a moment.")

 * Page 284 (Synchronous Versus Asynchronous Networks):
   > Even better, rather than using configured constant timeouts, systems can continually measure  response  times  and  their  variability  (jitter),  and  automatically  adjust  time‐ outs according to the observed response time distribution. This can be done with a Phi Accrual failure detector [30], which is used for example in Akka and Cassandra [31]. TCP retransmission timeouts also work similarly [27].

 * Page 284 ([[Synchronous]] Versus [[Asynchronous]] Networks):
   > Thus, for the duration of the call, each side is guaranteed to be able to send exactly 16 bits of audio data every 250 microseconds

 * Page 285 (Synchronous Versus Asynchronous Networks):
   > maximum end-to-end latency of the network is fixed. We call this a bounded delay.

 * Page 285 (Synchronous Versus Asynchronous Networks): "for bursty traffic."

 * Page 286 (Synchronous Versus Asynchronous Networks):
   > This approach has the downside of queueing, but the advan‐ tage  is  that  it  maximizes  utilization  of  the  wire.

 * Page 286 (Synchronous Versus Asynchronous Networks):
   > Variable delays in networks are not a law of nature, but simply the result of a cost/ benefit trade-off.

 * Page 287 (Unreliable [[Clocks]]):
   > we  have  to  assume  that  network  congestion,  queueing,  and  unbounded delays will happen. Consequently, there's no "correct" value for timeouts—they need to be determined experimentally.

 * Page 287 (Unreliable Clocks):
   > measure durations (e.g., the time interval between a request being sent and a response being received), whereas examples 5–8 describe points in time (events that occur on a particular date, at a particular time).

 * Page 288 ([[Monotonic]] Versus Time-of-Day Clocks):
   > the  most  commonly  used  mechanism  is  the  Network  Time  Protocol  ([[NTP]]),  which allows the computer clock to be adjusted according to the time reported by a group of servers  [37].  The  servers  in  turn  get  their  time  from  a  more  accurate  time  source, such as a GPS receiver.

 * Page 289 (Clock Synchronization and Accuracy):
   > NTP may adjust the frequency at which the monotonic clock moves forward (this is known  as  slewing  the  clock)

 * Page 289 (Clock Synchronization and Accuracy):
   > In  a  distributed  system,  using  a  monotonic  clock  for  measuring  elapsed  time  (e.g., timeouts) is usually fine, because it doesn't assume any synchronization between dif‐ ferent nodes' clocks and is not sensitive to slight inaccuracies of measurement.

 * Page 289 (Clock Synchronization and Accuracy):
   > The  quartz  clock  in  a  computer  is  not  very  accurate:  it  drifts  (runs  faster  or slower  than  it  should).

 * Page 289 (Clock Synchronization and Accuracy):
   > Google  assumes  a  clock  drift  of  200  ppm  (parts  per  million)  for  its servers [41]

 * Page 290 (Clock Synchronization and Accuracy):
   > by  performing  the  leap  second  adjustment  gradually  over  the  course  of  a  day (this is known as smearing) [47, 48], although actual NTP server behavior varies in practice [49].

 * Page 290 (Clock Synchronization and Accuracy):
   > For example, the MiFID II draft European regulation for financial  institutions  requires  all  high-frequency  trading  funds  to  synchronize  their clocks to within 100 microseconds of UTC, in order to help debug market anomalies such as "flash crashes" and to help detect market manipulation

 * Page 291 (Relying on Synchronized Clocks):
   > Thus,  if  you  use  software  that  requires  synchronized  clocks,  it  is  essential  that  you also  carefully  monitor  the  clock  offsets  between  all  the  machines.  Any  node  whose clock drifts too far from the others should be declared dead and removed from the cluster.  Such  monitoring  ensures  that  you  notice  the  broken  clocks  before  they  can cause too much damage.

 * Page 293 (Relying on Synchronized Clocks):
   > it's important to be aware that the definition of "recent" depends on a local time-of-day clock,

 * Page 293 (Relying on Synchronized Clocks):
   > because NTP's synchronization accuracy is itself limited by the network round-trip time

 * Page 293 (Relying on Synchronized Clocks): "So-called  logical  clocks"

 * Page 293 (Relying on Synchronized Clocks):
   > the  drift  in  an  imprecise  quartz  clock  can easily  be  several  milliseconds,  even  if  you  synchronize  with  an  NTP  server  on  the local network every minute. With an NTP server on the public internet, the best pos‐ sible accuracy is probably to the tens of milliseconds, and the error may easily spike to over 100 ms when there is network congestion [57].

 * Page 294 (Relying on Synchronized Clocks):
   > If we only know the time +/– 100 ms, the microsecond digits in the timestamp are essentially meaningless.

 * Page 294 (Relying on Synchronized Clocks):
   > An interesting exception is Google's TrueTime API in Spanner [41], which explicitly reports  the  confidence  interval  on  the  local  clock.  When  you  ask  it  for  the  current time,  you  get  back  two  values:  [earliest,  latest],  which  are  the  earliest  possible and  the  latest  possible  timestamp.  Based  on  its  uncertainty  calculations,  the  clock knows  that  the  actual  current  time  is  somewhere  within  that  interval.

 * Page 295 (Process Pauses):
   > Spanner implements snapshot isolation across datacenters in this way [59, 60]. It uses the clock's confidence interval as reported by the TrueTime API, and is based on the following observation: if you have two confidence intervals, each consisting of an ear‐ liest  and  latest  possible  timestamp  (A  =  [Aearliest,  Alatest]  and  B  =  [Bearliest,  Blatest]),  and those two intervals do not overlap (i.e., Aearliest < Alatest < Bearliest < Blatest), then B defi‐ nitely happened after A—there can be no doubt. Only if the intervals overlap are we unsure in which order A and B happened

 * Page 295 (Process Pauses):
   > Google  deploys  a  GPS  receiver  or  atomic  clock  in  each datacenter, allowing clocks to be synchronized to within about 7 ms [41].

 * Page 297 (Process Pauses): "This  feature  is  sometimes  used  for  live  migration  of  virtual"

 * Page 297 (Process Pauses): "machines is known as steal time."

 * Page 297 (Process Pauses):
   > most  of  its  time  swapping  pages  in  and  out  of  memory  and  getting  little  actual work  done  (this  is  known  as  thrashing).

 * Page 298 (Process Pauses):
   > All of these occurrences can preempt the running thread at any point and resume it at some later time, without the thread even noticing.

 * Page 298 (Process Pauses):
   > When writing multi-threaded code on a single machine, we have fairly good tools for making  it  thread-safe:  mutexes,  semaphores,  atomic  counters,  lock-free  data  struc‐ tures, blocking queues,

 * Page 298 (Process Pauses):
   > the  rest  of  the  world  keeps  moving  and  may  even  declare  the  paused  node dead because it's not responding. Eventually, the paused node may continue running, without even noticing that it was asleep until it checks its clock sometime later.

 * Page 298 (Process Pauses): "These are so-called hard real-time systems."

 * Page 303 (The Truth Is Defined by the Majority):
   > If  ZooKeeper  is  used  as  lock  service,  the  transaction  ID  zxid  or  the  node  version cversion  can  be  used  as  fencing  token.  Since  they  are  guaranteed  to  be  monotoni‐ cally increasing, they have the required properties [74].

 * Page 307 (System Model and Reality):
   > in  a  system.  We  do  this  by  defining  a  system  model,  which  is  an  abstraction  that

 * Page 308 (System Model and Reality):
   > Uniqueness No two requests for a fencing token return the same value. Monotonic sequence If request x returned token tx, and request y returned token ty, and x completed before y began, then tx < ty. Availability A  node  that  requests  a  fencing  token  and  does  not  crash  eventually  receives  a response.

 * Page 308 (System Model and Reality):
   > safety  and  liveness  properties.  In  the  example  just  given,  uniqueness  and monotonic sequence are safety properties, but availability is a liveness property.

 * Page 308 (System Model and Reality):
   > Safety is often informally defined as nothing bad happens, and liveness as something good eventually happens.

 * Page 309 (System Model and Reality):
   > However,  with  liveness  properties  we  are  allowed  to  make  caveats:  for  example,  we could say that a request needs to receive a response only if a majority of nodes have not crashed, and only if the network eventually recovers from an outage. The defini‐ tion of the partially synchronous model requires that eventually the system returns to a synchronous state—that is, any period of network interruption lasts only for a finite duration and is then repaired.

 * Page 311 (Summary):
   > To tolerate faults, the first step is to detect them, but even that is hard. Most systems

 * Page 311 (Summary):
   > Most non-safety-critical systems choose cheap and unreliable over expen‐ sive and reliable.

Chapter 09: [[Consistency]] and [[Consensus]]

 * Page 322 (Consistency Guarantees): "A better name for eventual consistency may be convergence"

 * Page 323 (Consistency Guarantees):
   > transaction  isolation  is  primarily  about  avoiding  race  conditions  due  to concurrently executing transactions, whereas distributed consistency is mostly about coordinating the state of replicas in the face of delays and faults.

 * Page 325 (What Makes a System [[Linearizable]]?):
   > is simple: to make a system appear as if there is only  a  single  copy  of  the  data.

 * Page 327 (What Makes a System Linearizable?):
   > writes for a register (every read must return the value set by the most recent write).

 * Page 332 (Relying on [[Linearizability]]):
   > might be faster than the internal replication inside the storage service. In this case, when the resizer fetches the image (step 5), it might see an old version of the image, or nothing at all. If it processes an old version of the image, the full-size and resized images in the file storage become permanently inconsistent.

 * Page 332 (Relying on Linearizability):
   > Since linearizability essentially means "behave as though there is only a single copy of the data, and all operations on it are atomic,"

 * Page 338 (The Cost of Linearizability): "dropping linearizability is performance, not fault tolerance."

 * Page 341 ([[Ordering]] and [[Causality]]):
   > [[Linearizability]] In a linearizable system, we have a total order of operations: if the system behaves as  if  there  is  only  a  single  copy  of  the  data,  and  every  operation  is  atomic,  this means that for any two operations we can always say which one happened first. This total ordering is illustrated as a timeline in Figure 9-4. Causality We said that two operations are concurrent if neither happened before the other (see  "The  "happens-before"  relationship  and  concurrency"  on  page  186).  Put another  way,  two  events  are  ordered  if  they  are  causally  related  (one  happened before the other), but they are incomparable if they are concurrent. This means that  causality  defines  a  partial  order,  not  a  total  order:  some  operations  are ordered with respect to each other, but some are incomparable.

 * Page 342 (Ordering and Causality):
   > linearizability implies causality: any system that is linearizable will preserve cau‐ sality correctly

 * Page 343 (Sequence Number Ordering): "to  know  which  operation  happened  before"

 * Page 343 (Sequence Number Ordering):
   > but if one operation happened before another, then they must be processed in that order on every replica. Thus, when a replica processes an operation, it  must  ensure  that  all  causally  preceding  operations  (all  operations  that  happened before) have already been processed; if some preceding operation is missing, the later operation must wait until the preceding operation has been processed.

 * Page 343 (Sequence Number Ordering):
   > instead  come  from  a  logical  clock,  which  is  an  algorithm  to  generate  a  sequence  of numbers  to  identify  operations,  typically  using  counters  that  are  incremented  for every operation.

 * Page 346 (Sequence Number Ordering):
   > This is shown in Figure 9-8, where client A receives a counter value of 5 from node 2, and then sends that maximum of 5 to node 1. At that time, node 1's counter was only 1,  but  it  was  immediately  moved  forward  to  5,  so  the  next  operation  had  an  incre‐ mented counter value of 6.

 * Page 348 (Total Order Broadcast):
   > his problem is known as total order broadcast or atomic broadcast

 * Page 353 (Distributed Transactions and Consensus): "atomic commit problem.xii"

 * Page 355 (Atomic Commit and Two-Phase Commit (2PC)): "compensating  transaction"

 * Page 356 (Atomic Commit and Two-Phase Commit (2PC)): "coordinator  (also  known  as  transaction  manager)."

 * Page 358 (Atomic Commit and Two-Phase Commit (2PC)): "n doubt or uncertain."

 * Page 363 (Distributed Transactions in Practice):
   > Many XA implementations have an emergency escape hatch called heuristic decisions:

 * Page 364 ([[Fault-Tolerant]] Consensus):
   > thus have a tendency of amplifying failures, which runs counter to our goal of building fault-tolerant systems.

 * Page 364 (Fault-Tolerant Consensus):
   > The  consensus  problem  is  normally  formalized  as  follows:  one  or  more  nodes  may propose  values,  and  the  consensus  algorithm  decides  on  one  of  those  values.

 * Page 365 (Fault-Tolerant Consensus):
   > Uniform agreement No two nodes decide differently. Integrity No node decides twice. Validity If a node decides value v, then v was proposed by some node. Termination Every node that does not crash eventually decides some value.

 * Page 368 (Fault-Tolerant Consensus):
   > he protocols define an epoch number (called the ballot number in Paxos,  view  number  in  Viewstamped  Replication,  and  term  number  in  Raft)  and guarantee that within each epoch, the leader is unique.

 * Page 372 (Membership and Coordination Services):
   > For  this purpose, some consensus systems support read-only caching replicas. These replicas asynchronously receive the log of all decisions of the consensus algorithm, but do not actively participate in voting. They are therefore able to serve read requests that do not need to be linearizable.

Chapter 10: Batch Processing

 * Page 394 (The Unix Philosophy):
   > This approach—automation, rapid prototyping, incremental iteration, being friendly to  experimentation,  and  breaking  down  large  projects  into  manageable  chunks— sounds remarkably like the Agile and DevOps movements of today. Surprisingly little has changed in four decades.

 * Page 396 (The Unix Philosophy):
   > lthough  it's  not  perfect,  even  decades  later,  the  uniform  interface  of  Unix  is  still something  remarkable.  Not  many  pieces  of  software  interoperate  and  compose  as well  as  Unix  tools  do:  you  can't  easily  pipe  the  contents  of  your  email  account  and your online shopping history through a custom analysis tool into a spreadsheet and post the results to a social network or a wiki. Today it's an exception, not the norm, to have programs that work together as smoothly as Unix tools do.

 * Page 396 (The Unix Philosophy): "leads to Balkanization of data."

 * Page 396 (The Unix Philosophy):
   > (One could say this is a form of loose coupling, late  binding  [15],  or  inversion  of  control  [16].)  Separating  the  input/output  wiring from the program logic makes it easier to compose small tools into bigger systems.

 * Page 397 (MapReduce and Distributed Filesystems):
   > However,  the  biggest  limitation  of  Unix  tools  is  that  they  run  only  on  a  single machine—and that's where tools like Hadoop come in.

 * Page 400 (MapReduce Job Execution): "putting the com‐ putation near the data"

 * Page 402 (MapReduce Job Execution):
   > The  process  of  partitioning  by reducer, sorting, and copying data partitions from mappers to reducers is known as the shuffle [26]

 * Page 402 (MapReduce Job Execution):
   > so this chain‐ ing is done implicitly by directory name: the first job must be configured to write its output to a designated directory in HDFS, and the second job must be configured to read that same directory name as its input. From the MapReduce framework's point of view, they are two independent jobs.

 * Page 406 (Reduce-Side Joins and Grouping):
   > This  algorithm  is  known  as  a  sort-merge  join,  since mapper output is sorted by key, and the reducers then merge together the sorted lists of records from both sides of the join.

 * Page 407 (Reduce-Side Joins and Grouping):
   > active database records are known as linchpin objects [38] or hot keys.

 * Page 407 (Reduce-Side Joins and Grouping): "skew  (also  known  as  hot spots)"

Chapter 11: Stream Processing

 * Page 441 (Messaging Systems):
   > What happens if the producers send messages faster than the consumers can pro‐ cess them?

 * Page 442 (Messaging Systems):
   > If messages are buffered in a queue, it is important to understand what happens as that queue grows.

 * Page 442 (Messaging Systems):
   > If so, how does the disk access affect the performance of the messaging system [6]?

 * Page 442 (Messaging Systems): "What happens if nodes crash or temporarily go offline"







