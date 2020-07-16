# Udacity SF Crime Data Project

## Submit codes

- kafka_server.py
- producer_server.py
- consumer_server.py
- data_stream.py

## Question?

Q : How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

A : I checked `inputRowsPerSecond` and `processedRowsPerSecond` value.

Q : What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?

A : I checked `inputRowsPerSecond` and `processedRowsPerSecond` . Finally, I got a best key/value pairs like below.

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

### Producer
```
python kafka_server.py
```
### Consumer
```
'python consumer_server.py'
```
### Data stream
```
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py
```
