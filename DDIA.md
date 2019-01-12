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
  * Leaderless replication

6. CH6 Patitioning
7. CH7 Transactions
