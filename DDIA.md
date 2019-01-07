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
4. CH4 various formats for data encoding (serialization)
