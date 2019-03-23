## Design Data-Intensive Applications
1. CH1 
  * Reliability		Hardware/Software/Human Errors 
  * Scalability 	scale up vs scale out
  * Maintainability	Operability/Simplicity/Evolvability

2. CH2 Data model and query languages
  * ORM: Object-relational mapping frameworks (ActiveRecord and Hibernate), reduce translation layer between OOP and SQL data model
  * self-contained document, a JSON representation, simpler than XML (Document-oriented DB, MongoDB, REthinkDB, CouchDB and Espresso)
  * CODASYL model: the network model IMS (different from graph model)
  * Relational(schema-on-write) vs Document (schema-on-read)
  * Document databases are schemaless
  * SQL is a declarative query language; IMS and CODASYL quiried DB using imperative code(tells the computer to perform certain operations)
  * Graph-like model
    * Property graph model: Neo4j, Titan and InfiniteGraph (Cypher)
    * triple-store model: turtle format, Neptune (SPARQL)
    * sematic web, RDF data
    * Datalog: older language

3. CH3 DB storage engine
  * Index
    * Hash Indexes: e.g. Bitcask(Riak), must fit in memory, range query not efficient
    * SSTable: e.g. LevelDB and RocksDB, Sorted-String Table, red-black trees/AVL trees (memtable). LSM-tree (Log-Structured Merge-Tree)
    * B-Tree: WAL (write-ahead log to restore B-tree)
    * Other Indexes: clustered-index(store the indexed row directly within an index), Multi-column index, Lucene for full-text search 
  * Transaction Processing vs Analytics: OLTP vs OLAP, Data Warehousing, Star and Snowflakes
  * Column-Orientied Storage
    * Column Compression: bitmap encoding (column family are stored together, Bigtable model is still row-oriented)
    * Sort Order in Column Storage, having multiple sort orders in a column-oriented store is similar to having multiple secondary indexes in a row-oriented store
    * Writing
    * Aggregation: data cube is a common special case of materialized view

4. CH4 various formats for data encoding (serialization)
  * Encoding (serialization or marshalling): the translation from the in-memory representation to a byte sequence
  * Data Encoding Formets: JSON, XML, Protocol Buffers, Thrift, Avro
  * Textual formats such as JSON, XML and CSV
  * Apache Thrift and Protocol Buffers are binary encoding libraries
  * Avro: encoding doesn't contain fields/datatypes, need writer's schema and reader's schema. Friedlier to dynamically generated schemas
  * Modes of Dataflow
    * Via databases
    * Via service calls: two popular approached to web services (REST, SOAP and RPC)
      * RPC modes tries to make a request to a remote network service look the same as calling a function/method in the programming language, within the same process. Current main focus of RPC framwork is on requests between services owned by the same organization.
    * Via asyschronous message passing: between RPC and databases by using a message broker. 
      * The actor model is a programming model for concurrency in a single process. Distributed actor framework integrates a message broker and the actor programming model.

5. CH5 Replication
  * Single-leader replication, asynchronous replication is widely used
    * Statement-based replication
    * Write-ahead log (WAL) shipping
    * Logical (row-based) log replication
    * Trigger-based replication
  * Problems with Replication Lag
    * implement read-after-write consistency
    * Monotonic Reads, always read from the same replica
    * Consistent Prefix Reads 
  * Multi-leader replication
    * Use Case: multi-datacenter operation, clients with offline operation, collaborative editing
    * Handling Write Conflicts: avoid by routing to same datacenter
    * Replication Topology: all-to-all
  * Leaderless replication: Amazon Dynamo
    * Quorum for read and write

6. CH6 Partitioning
  * Partition by Key Range
  * Partition by Hash of Key
  * Secondary index
    * local index: document-partitioned index, each partition maintains its own secondary indexes
    * global index: term-partitioned index, can be partitioned differently from the primary key index
  * Rebalancing Partitions
  * Routing requests
    * which component makes the routing decision
      * each node
      * routing tier: zookeeper maintains the authoritative mapping of partitions to nodes
      * client
  
7. CH7 Transactions
  * ACID: Atomocity, Consistency, Isolation and Durability
    * A and C describes what the database should do if a client makes several writes within the same transaction
    * Isolation
      * READ COMMITTED isolation guarantees no dirty reads and no dirty writes, lock to prevent dirty writes, remembers both old committed value and new value by write lock
      * SNAPSHOT isolation to address read skew: MVCC, multi-version concurrency control
      * lost updates
      * write skew, phantom addressed by materializing conflicts
    * Serialization isolation
      * Actual Serial Execution
      * Two-phase locaking
      * Serializable Snapshot Isolation 
  * BASE: Basically Available, Soft state and Eventual consistency

8. CH8 The Trouble with Distributed Systems
  Partial failures can occur 
  * Unreliable Networks
  * Unreliable Clock
  * Process Pause
  * Syetem model
    * timing assumptions: sychronous model, partially synchronous model, asynchronous model
    * node failures: crash-stop faults, crash-recovery faults, byzantine(arbitrary) faults 
  First detect the faults(timeouts), tolerate (get quorum to agree on)

9. CH9 Consistency and Consensus
  * Linearizability: make a system appeart as if there were only one copy of data and all operations are atomic
    * Linearizability vs Serializability
    * CAP theorem
  * Ordering Guarantees
    * Linearizability: total order of operations
    * Causality defines partial order
    * Linearizability is stronger than causal consistency
    * Total order broadcast
  * Distributed Transactions and Consensus
    * Atomic commit
    * two-phase commit: use coordinator
    * fault-tolerant consensus algorithms: VSR, Paxos, Raft and Zab, total order algorithms

10. CH10 Batch Processing
  * Unix tools: awk, sed, grep, sort, uniq, xargs
  * MapReduce and distributed filesystems
    * Reduce-Side join
    * Map-Side join
      * broadcast hash join
      * partitioned hash join
      * map-side merge join
    * Batch Process Output
      * Build search index
      * Key-value stores
    * Map reduce vs MPP: handling of faults and use of memory/disk 
  * Beyond MapReduce
    * Map reduce materilize intermediate state, other engines:Spark, Tez and Flink
    * Pregel processing model to process graph data

11. CH11 Stream Processing
  * Messaging Systems: publish/subscribe model
    * direct messaging from producers to consumers
    * Message brokers
      * AMQP/JMS-style message broker
      * log-based message brokers: Kafka, Kinesis etc., taking ideas from db
    * Change Data Capture: mutable
    * Event Sourcing: record immutable events
  * Processing Streams
    * Event time vs Processing Time
    * Stream-stream join, stream-table join, table-table join
    * fault-tolerance: exactly-once semantics
      * Microbatching: Spark Streaming; checkpointing: Apache Flink

12. CH12 The Future of Data Systems 
  * Data Integration
    * Unifying batch and stream processing
  * Unbundling Databases
  * Ensure processing is correct
  * Predictive analytics bias and privacy
