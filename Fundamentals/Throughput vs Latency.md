## **General Definitions**

| Metric         | Definition                                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Throughput** | The number of operations completed in a given time frame (e.g., requests per second, transactions per second).      |
| **Latency**    | The time taken to complete a single operation (e.g., time taken for a query to return a result, API response time). |


## **In Databases**

## **In Databases**

|Aspect|Throughput|Latency|
|---|---|---|
|**Definition**|Number of queries processed per second.|Time taken to execute a single query.|
|**Factors Affecting It**|- Connection pooling||
- **High Throughput, Low Latency:** A well-indexed query fetching records from a cached table.
- **High Throughput, High Latency:** A heavily loaded database handling many queries, each taking significant time.

## **In REST APIs**

| Aspect                   | Throughput                                 | Latency                                       |
| ------------------------ | ------------------------------------------ | --------------------------------------------- |
| **Definition**           | Number of API requests handled per second. | Time taken for a single API call to complete. |
| **Factors Affecting It** | - Number of concurrent users               |                                               |
- **High Throughput, Low Latency:** A stateless API with a fast cache (e.g., Redis) serving requests.
- **High Throughput, High Latency:** A slow API but handling a large number of concurrent users.

## **In Other Domains**

| Domain                               | Throughput                                  | Latency                                                       |
| ------------------------------------ | ------------------------------------------- | ------------------------------------------------------------- |
| **Message Queues (Kafka, RabbitMQ)** | Number of messages processed per second.    | Time taken to deliver a message from producer to consumer.    |
| **Networking**                       | Number of packets transmitted per second.   | Time taken for a packet to travel from source to destination. |
| **Microservices**                    | Number of service calls handled per second. | Time taken for one microservice to respond to another.        |
| **File Systems**                     | Number of read/write operations per second. | Time taken for a file to be read/written.                     |
## **Key Takeaways**

- **High Throughput ≠ Low Latency** → A system can process many requests but still have slow individual responses.
- **Trade-offs exist** → Increasing throughput (e.g., batch processing) might increase latency for individual requests.
- **Optimization strategies** depend on domain-specific bottlenecks (DB indexes, caching, horizontal scaling, etc.