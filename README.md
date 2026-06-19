# AutoMQ vs Kafka (KRaft) Performance Benchmark

## Overview

This project demonstrates the deployment and benchmarking of AutoMQ and Apache Kafka (KRaft Mode) using Docker Compose.

### Objective

* Deploy MinIO as object storage
* Deploy AutoMQ connected to MinIO
* Deploy Apache Kafka in KRaft mode
* Run identical producer and consumer benchmarks
* Compare throughput and latency metrics

## Environment

* Docker Desktop
* MinIO
* AutoMQ
* Apache Kafka 3.9 (KRaft Mode)
* Kafka UI

## Test Configuration

* Topic: `perf-test`
* Messages Produced: 10,000
* Messages Consumed: 10,000
* Record Size: 100 bytes

## Producer Benchmark Results

| Metric      | AutoMQ         | Kafka KRaft    |
| ----------- | -------------- | -------------- |
| Throughput  | 70,422 msg/sec | 66,225 msg/sec |
| Avg Latency | 3.33 ms        | 5.84 ms        |
| Max Latency | 110 ms         | 109 ms         |
| p50         | 3 ms           | 3 ms           |
| p95         | 7 ms           | 14 ms          |
| p99         | 11 ms          | 15 ms          |
| p99.9       | 12 ms          | 15 ms          |

## Consumer Benchmark Results

| Metric            | AutoMQ          | Kafka KRaft     |
| ----------------- | --------------- | --------------- |
| Messages Consumed | 10,000          | 10,000          |
| Throughput        | 3169.57 msg/sec | 3172.59 msg/sec |
| Data Consumed     | 0.9529 MB       | 0.9529 MB       |

## Benchmark Commands

### Producer Test

```bash
/opt/kafka/bin/kafka-producer-perf-test.sh \
  --topic perf-test \
  --num-records 10000 \
  --record-size 100 \
  --throughput -1 \
  --producer-props bootstrap.servers=localhost:9092
```

### Consumer Test

```bash
/opt/kafka/bin/kafka-consumer-perf-test.sh \
  --bootstrap-server localhost:9092 \
  --topic perf-test \
  --messages 10000
```

## Conclusion

AutoMQ achieved higher producer throughput and lower latency than Apache Kafka (KRaft mode) in this 10,000-message benchmark test, while consumer throughput remained nearly identical.

## Repository Contents

* docker-compose.yml
* docker-compose-craft.yml
* docker-compose-cluster.yaml
* README.md
* benchmark-results.md
