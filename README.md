# Udacity SF Crime Data with Spark Streaming

## Submit codes

- kafka_server.py
- producer_server.py
- consumer_server.py
- data_stream.py

## Question?

Q : How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

A : I monitored the following parameters:

    numInputRecords: The number of records processed in a trigger
    inputRowsPerSecond: The rate of data arriving
    processedRowsPerSecond: The rate at which Spark is processing data
    triggerExecution: Approximate time in milliseconds to process this micro-batch

Q : What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?

A : I realized that `inputRowsPerSecond` and `processedRowsPerSecond` are the two primary settings:

```
spark.streaming.kafka.maxRatePerPartition : 100
spark.streaming.backpressure.enabled : true
spark.default.parallelism : 100
spark.sql.shuffle.partitions : 100
```

## Environment

- Python 3.7
- Spark 2.3.4
- Kafka 0.10

## How to run
In order to run the application you will need to start:

1. Zookeeper:

`/usr/bin/zookeeper-server-start config/zookeeper.properties`

2. Kafka server:

`/usr/bin/kafka-server-start config/server.properties`

3. Produce data streams (Producer):

`python kafka_server.py`

4. Kafka consumer:

`python consumer_server.py`

5. Run Spark job:

`spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py`

### Kafka Consumer Console Output

![kafka consumer output](screenshots/Consumer_Console_Output.jpeg)

### Progress Reporter

![progress reporter](screenshots/Progress_Reporter.jpeg)

### Count Output

![count output](screenshots/Count_Output.jpeg)
