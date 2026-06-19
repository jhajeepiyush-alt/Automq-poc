# AutoMQ Performance Benchmark

## Overview

This project demonstrates AutoMQ deployment using Docker Compose and performance benchmarking using Kafka-compatible CLI tools.

## Test Configuration

* Broker: AutoMQ
* Topic: perf-test
* Messages Produced: 10,000
* Messages Consumed: 10,000
* Record Size: 100 bytes

## Producer Benchmark Results

| Metric      | Value          |
| ----------- | -------------- |
| Throughput  | 70,422 msg/sec |
| Avg Latency | 3.33 ms        |
| Max Latency | 110 ms         |
| p50         | 3 ms           |
| p95         | 7 ms           |
| p99         | 11 ms          |
| p99.9       | 12 ms          |

## Consumer Benchmark Results

| Metric            | Value            |
| ----------------- | ---------------- |
| Messages Consumed | 10,000           |
| Throughput        | 3,169.57 msg/sec |
| Data Consumed     | 0.9529 MB        |

## Commands Used

Producer Test:

```bash
/opt/kafka/bin/kafka-producer-perf-test.sh \
  --topic perf-test \
  --num-records 10000 \
  --record-size 100 \
  --throughput -1 \
  --producer-props bootstrap.servers=localhost:9092
```

Consumer Test:

```bash
/opt/kafka/bin/kafka-consumer-perf-test.sh \
  --bootstrap-server localhost:9092 \
  --topic perf-test \
  --messages 10000
```

## Conclusion

AutoMQ successfully handled a 10,000-message workload with low producer latency and high throughput.

