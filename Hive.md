## Hive Basics
1. ACID vs non-ACID tables, non-ACID table is preferred (ACID tables also need compaction, combine delta folder with base folder, cannot be read properly by Spark)
2. Choose proper format (compression) for tables 
3. Enable storage index, 'orc.create.index'='true'
4. Bucketing
5. Bloom filter
6. Partition, avoid too many partitions 
7. Record insertion should use sort by
8. For non-ACID tables, concatenate small files for Hive tables
9. Analyze table to update statistics

## Hive Transactions
* https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions
