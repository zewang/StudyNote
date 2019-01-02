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
