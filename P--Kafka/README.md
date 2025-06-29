## Highlights
 * Page #1:
   > that we developed for collecting and delivering high volumes of log data with low latency.

 * Page #1:
   > Log data has long been a component of analytics used to track  user  engagement,  system  utilization,  and  other  metrics.

 * Page #1:
   > including  Facebook's  Scribe  [6],  Yahoo's  Data Highway  [4],  and  Cloudera's  Flume  [3].

 * Page #1:
   > we  needed  to  support  most  of  the real-time  applications  mentioned  above  with  delays  of  no  more than a few seconds.

 * Page #1:
   > many systems do not focus as strongly on throughput as their primary design constraint.

 * Page #2: "This  means  each  message  requires  a  full  TCP/IP roundtrip,"

 * Page #2:
   > At LinkedIn, we find the "pull" model more suitable for our applications since each consumer  can  retrieve  the  messages  at  the  maximum  rate  it  can sustain and avoid being flooded by messages pushed faster than it can  handle.

 * Page #2:
   > We support both the point-topoint  delivery  model  in  which  multiple  consumers  jointly consume  a  single  copy  of  all  messages  in  a  topic,  as  well  as  the publish/subscribe  model  in  which  multiple  consumers  each retrieve its own copy of a topic.

 * Page #2:
   > For better performance, we flush the segment files to disk  only  after  a  configurable  number  of  messages  have  been published or a certain amount of time has elapsed.

 * Page #2: "after it is flushed."

 * Page #3: "by its logical offset in the log"

 * Page #3:
   > From now on, we will use message ids and offsets interchangeably

 * Page #3:
   > Each pull  request  contains  the  offset  of  the  message  from  which  the consumption  begins  and  an  acceptable  number  of  bytes  to  fetch.

 * Page #3:
   > The  broker locates  the  segment  file  where  the  requested  message  resides  by searching the offset list, and sends the data back to the consumer

 * Page #3: "Instead, we rely on  the  underlying  file  system  page  cache."

 * Page #3:
   > This  has  the  additional  benefit  of  retaining warm cache even when a broker process is restarted.

 * Page #3:
   > On  Linux  and  other Unix  operating  systems,  there  exists  a  sendfile  API  [5]  that  can directly  transfer  bytes  from  a  file  channel  to  a  socket  channel. This typically avoids 2 of the copies and 1 system call introduced in steps (2) and (3). Kafka exploits the sendfile API to efficiently deliver bytes in a log segment file from a broker to a consumer.

 * Page #3:
   > the  information  about  how  much  each  consumer  has consumed  is  not  maintained  by  the  broker,  but  by  the  consumer itself.

 * Page #3:
   > Kafka solves this problem by using a simple  time-based  SLA  for  the  retention  policy.

 * Page #3: "rewind"

 * Page #3: "back  to  an  old  offset  and  re-consume  data."

 * Page #3: "consumer groups"

 * Page #3:
   > each  message  is  delivered  to  only  one  of the consumers within the group.

 * Page #4: "the smallest unit  of  parallelism"

 * Page #4:
   > This  means  that  at  any  given  time,  all messages  from  one  partition  are  consumed  only  by  a  single consumer within each consumer group

 * Page #4:
   > (a)  one can register a watcher on a path and get notified when the children of  a  path  or  the  value  of  a  path  has  changed;  (b)  a  path  can  be created as ephemeral (as oppose to persistent), which means that if the creating client is gone, the path is automatically removed by the Zookeeper server; (c) zookeeper replicates its data to multiple servers, which makes the data highly reliable and available.

 * Page #4:
   > track  of (1)  detecting  the addition and the removal of brokers and consumers, (2) triggering a  rebalance  process  in  each  consumer  when  the  above  events happen,  and  (3)  maintaining  the  consumption  relationship  and keeping the  consumed  offset  of  each  partition.

 * Page #4: "broker registry contains the broker's host name and port"

 * Page #4:
   > , and the set  of  topics  and  partitions  stored  on  it.

 * Page #4:
   > consumer group to which a consumer belongs and the set  of  topics  that  it  subscribes  to.

 * Page #4:
   > Each  consumer  group  is associated  with  an  ownership  registry  and  an  offset  registry  in Zookeeper

 * Page #4:
   > The  offset  registry  stores for  each  subscribed  partition,  the  offset  of  the  last  consumed message in the partition.

 * Page #4: "ephemeral  for  the  broker registry,  the  consumer  registry"

 * Page #4: "and  the  ownership  registry"

 * Page #4: "are  ephemeral"

 * Page #4: "persistent for the offset registry."

 * Page #4: "consumer  registers  a  Zookeeper  watcher"

 * Page #4:
   > When this happens, the first  consumer  simply  releases  all  the  partitions  that  it  currently owns, waits a bit and retries the rebalance process. In practice, the rebalance process often stabilizes after only a few retries.

 * Page #4:
   > Kafka  guarantees  that  messages  from  a  single  partition  are delivered to a consumer in order.

 * Page #5:
   > his  instance  of Kafka  runs  a  set  of  embedded  consumers  to  pull  data  from  the Kafka instances in the live datacenters

 * Page #5:
   > The  consumers  can  then  count  the number  of  messages  that  they  have  received  from  a  given  topic and  validate  those  counts  with  the  monitoring  events  to  validate the correctness of data.

 * Page #6:
   > Finally,  by  using  the sendfile API, Kafka reduces the transmission overhead.

 * Page #6: "pull-based  consumption  model"

