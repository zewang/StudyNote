## Spark Tuning and Cluster Sizing
1. Whether dynamic allocation is on, even with dynamic allocation, executor size needs to be determined
2. Some core settings
  * spark.driver.memory
  * spark.executor.memory
  * spark.executor.cores
  * driver core = 1 in client mode, core can be set in cluster mode
3. Memory Overhead
  * executor overhead = spark.yarn.executor.memoryOverhead
  * driver (cluster mode) = spark.yarn.driver.memoryOverhead
  * driver (client mode) = spark.yarn.am.memoryOverhead
4. If too much data collect to driver or large local computations, increase spark.driver.maxResultSize also
5. 5 cores per executor seems to be optimal
6. Within executot memory, around 25% is reserved for Spark internal meta data and user data structures, M = spark.executor.memory * spark.memory.fraction is used for caching and execution 
  * All cached data must fit in R = spark.executor.memory * spark.memory.fraction * spark.memory.storageFraction
7. number of tasks can be ran at the same time = # of cores * # of executors

## Serilization Options
1. RDDs: Java serialization or Kryo serialization
2. DataFrames/Datasets: Tungsten-based serialization

## Aditional Debugging Techniques
1. Interactive mode: take(1) or count
2. Understand driver or executor log to look at
3. Try using explicit functions instead of anonymous inner functions
4. Driver out-of-memory exception: be weary of collect statements, countByKey or some models in Spark ML or MLlib
5. Config and access logging for more information
6. Run Spark in local mode and attach debuggers

## Testing and Validation
1. General Spark Unit Testing
  * Factor code for testability: avoid using Scala's anonymous function
  * Regular Spark Job: create RDD and parallelize and apply transformation
  * Streaming
2. Getting Test Data: mllib RandomRDDs
3. Verifying Performance: SparkListener, spark-perf package

## Other Components
1. Spark MLlib and Spark ML
2. Spark Streaming: DStreams for RDD and Structured Streaming based on Spark SQL/DataFrames, long-running job needs to handle driver failure or checkpointing (HA)
3. GraphX: GraphFrames
