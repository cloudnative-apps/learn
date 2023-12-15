---
title: "System Design"
date: 2023-12-10T19:31:33+05:30
#draft: true
weight: 1
lightgallery: true

toc:
  auto: false
---
Contents


## Usefull system design links
### 1. Netflix
**Millions WRP - Casendra benchmarking**
https://netflixtechblog.com/benchmarking-cassandra-scalability-on-aws-over-a-million-writes-per-second-39f45f066c9e

**Streamlining Membership Data Engineering at Netflix with Psyberg**
https://netflixtechblog.com/1-streamlining-membership-data-engineering-at-netflix-with-psyberg-f68830617dd1

**Incremental Processing using Netflix Maestro and Apache Iceberg**
https://netflixtechblog.com/incremental-processing-using-netflix-maestro-and-apache-iceberg-b8ba072ddeeb

**Streaming SQL in Data Mesh**
https://netflixtechblog.com/streaming-sql-in-data-mesh-0d83f5a00d08

**Netflix’s HDR video streaming is now dynamically optimized**
https://netflixtechblog.com/all-of-netflixs-hdr-video-streaming-is-now-dynamically-optimized-e9e0cb15f2ba


## Some awsome blob post to read 
**Redis use cases in distributed systems**
https://medium.com/@maheshsaini.sec/top-5-redis-use-cases-in-distributed-systems-6aadc73121c6

**Mastering databases**
https://levelup.gitconnected.com/system-design-interview-mastering-databases-9fb40bb561cd


## Load Balancer

### Load Balancer Types:

#### 1. Hardware Load Balancer:
   - **Description:** Dedicated physical devices designed for load balancing.
   - **Advantages:**
     - High throughput and low latency.
     - Specialized features for traffic management.
   - **Considerations:**
     - Costlier than software-based solutions.
     - Limited scalability compared to some software solutions.

#### 2. Software Load Balancer:
   - **Description:** Implemented in software and typically runs on standard hardware.
   - **Advantages:**
     - Cost-effective and easier to scale horizontally.
     - Can be deployed on commodity hardware or virtualized environments.
   - **Considerations:**
     - May have limitations in terms of throughput compared to hardware solutions.

####  3. Application Load Balancer (Layer 7):
   - **Description:** Operates at the application layer, making routing decisions based on content.
   - **Advantages:**
     - Ideal for distributing traffic based on specific application data or user sessions.
     - Supports features like SSL termination and content-based routing.
   - **Considerations:**
     - Requires more processing power for content analysis.

####  4. Network Load Balancer (Layer 4):
   - **Description:** Operates at the transport layer and makes routing decisions based on network-level information.
   - **Advantages:**
     - Efficient for distributing traffic based on IP addresses and ports.
     - Suitable for TCP/UDP-based services.
   - **Considerations:**
     - Limited awareness of application-specific data.

### Considerations while designing and choosing loadbalancing**
1. _Scalability:_
   - Design the system to accommodate the potential growth in traffic and resources.
   - Use load balancers that support horizontal scaling.

2. _High Availability:_
   - Deploy multiple load balancers to avoid a single point of failure.
   - Implement failover mechanisms to ensure continuous operation.

3. _Health Checks:_
   - Integrate health checks to monitor the status of backend servers.
   - Automatically route traffic away from unhealthy servers.

4. _Session Persistence:_
   - Consider whether the application requires sticky sessions to maintain user state.
   - Implement session persistence configurations if needed.

5. _SSL Termination:_
   - Offload SSL/TLS encryption at the load balancer to reduce the workload on backend servers.
   - Ensure proper security measures for handling decrypted traffic.

6. _Content-Based Routing (for Layer 7):_
   - Use application load balancers for content-based routing if the application's architecture benefits from it.
   - Define routing rules based on URL paths, headers, or other application-specific data.

7. _Logging and Monitoring:_
   - Implement logging mechanisms to track traffic patterns and potential issues.
   - Integrate with monitoring tools to receive real-time insights into the load balancer's performance.

8. _Load-Balancing Algorithms:_
   - Choose the appropriate load-balancing algorithm based on the application's needs (e.g., Round Robin, Least Connections, Weighted).
   - Understand the characteristics of each algorithm and their impact on traffic distribution.

9. _Global Load Balancing:_
   - For distributed systems, consider global load balancing to route traffic based on user location or server health across multiple geographic regions.

10. _Cost Considerations:_
    - Evaluate the cost implications of the chosen load balancing solution, especially in cloud environments.
    - Optimize for cost-effectiveness without compromising performance.

11. _Integration with Auto-Scaling:_
    - If using auto-scaling for backend servers, ensure seamless integration with the load balancer to dynamically adjust capacity.

## System design principle and patterns:


###  1. **Quorum:**
   - **Purpose:** Ensures consistency in a distributed system by requiring a minimum number of nodes to agree on an operation.
   - **Use Case:** Distributed databases (e.g., Cassandra, MongoDB), consensus algorithms (e.g., Paxos, Raft), and fault-tolerant systems.
   - **Details:** In a distributed database, a write operation may require acknowledgment from a majority of nodes to ensure that the write is committed. This helps prevent conflicts and maintain data consistency.

###  2. **Checksum:**
   - **Purpose:** Verifies the integrity of data by generating a checksum (hash) and comparing it across distributed nodes.
   - **Use Case:** Data replication, fault detection, and error correction in distributed storage systems (e.g., Hadoop Distributed File System).
   - **Details:** Before replicating data across nodes, a checksum is calculated. Nodes can compare their locally calculated checksum with the checksum received to verify data integrity.

###  3. **Bloom Filter:**
   - **Purpose:** Provides a space-efficient data structure to test whether a given element is a member of a set.
   - **Use Case:** Distributed caches (e.g., Redis), distributed databases (e.g., Cassandra for indexing), and network routers.
   - **Details:** A Bloom filter quickly checks if an element is in a set or not. It can have false positives but no false negatives, making it efficient for reducing unnecessary data access.

###  4. **MapReduce:**
   - **Purpose:** Splits a large computation task into smaller sub-tasks that can be processed independently and then combines the results.
   - **Use Case:** Large-scale data processing (e.g., Apache Hadoop, Apache Spark), distributed data analysis, and batch processing.
   - **Details:** MapReduce breaks down a computation into map tasks (processing data) and reduce tasks (aggregating results). It enables parallel processing on distributed data.

###  5. **Leader Election:**
   - **Purpose:** Selects a single node as the leader to coordinate actions and maintain consistency in a distributed system.
   - **Use Case:** Consensus algorithms (e.g., Raft, ZooKeeper), fault-tolerant systems, and distributed databases.
   - **Details:** Nodes compete to become the leader, and only the leader makes decisions. Leader election ensures a single point of coordination, preventing conflicting decisions.

###  6. **Replication:**
   - **Purpose:** Copies data across multiple nodes to improve availability, fault tolerance, and load balancing.
   - **Use Case:** Distributed databases (e.g., MySQL, PostgreSQL with replication), caching systems (e.g., Redis), and content delivery networks.
   - **Details:** Replication involves maintaining identical copies of data on multiple nodes. It enhances availability and fault tolerance, but strategies vary (e.g., master-slave, multi-master).

###  7. **Sharding (Partitioning):**
   - **Purpose:** Divides a large dataset into smaller, more manageable partitions to distribute the workload.
   - **Use Case:** Distributed databases (e.g., MongoDB with sharding, Cassandra), search engines (e.g., Elasticsearch), and data warehouses.
   - **Details:** Sharding distributes data based on a chosen criterion (e.g., user ID, geographic location). Each shard operates independently, improving parallel processing.

###  8. **Event Sourcing:**
   - **Purpose:** Captures and stores the state of an application as a sequence of events.
   - **Use Case:** Event-driven architectures, auditing, and systems requiring strong traceability (e.g., financial systems, order processing).
   - **Details:** Each state change is recorded as an event. The system can be reconstructed by replaying these events, providing a complete audit trail.

###  9. **CQRS (Command Query Responsibility Segregation): **
   - **Purpose:** Separates the command (write) and query (read) responsibilities of a system.
   - **Use Case:** Event-driven architectures, systems with distinct read and write patterns (e.g., Axon Framework).
   - **Details:** CQRS allows for independent scaling and optimization of read and write models, improving performance and flexibility.

###  10. **Gossip Protocol: **
  - **Purpose:** Disseminates information across a network by having nodes share information with a few random peers.
    - **Use Case:** Distributed databases (e.g., Cassandra), peer-to-peer systems, and decentralized networks.
    - **Details:** Nodes periodically exchange information with a small set of random peers. This helps in propagating information efficiently across the network.

###  11. **Two-Phase Commit:**
- **Purpose:** Coordinates a distributed transaction to ensure that all nodes either commit or abort the transaction.
    - **Use Case:** Distributed databases (e.g., Oracle RAC), transactional systems, and financial applications.
    - **Details:** In the first phase, nodes agree to commit or abort. In the second phase, the decision is executed. If any node votes to abort, all nodes roll back the transaction.

###  12. **Saga Pattern:**
- **Purpose:** Manages long-running and distributed transactions by breaking them into smaller, more manageable steps.
    - **Use Case:** Order processing systems, financial transactions, and business workflows.
    - **Details:** Sagas break down a complex transaction into a series of smaller, independent steps. Each step is a separate transaction with its own commit or rollback.

###  13. **Bulkhead Pattern:**
- **Purpose:** Isolates components or services to prevent the failure of one from affecting others.
    - **Use Case:** Microservices architecture, fault isolation, and resilience (e.g., Netflix Hystrix).
    - **Details:** Inspired by ship design, the bulkhead pattern isolates components to contain failures. If one component fails, it does not adversely affect other components.

###  14. **Chubby (Distributed Lock Service):** 
- **Purpose:** Coordinates distributed systems by providing a distributed lock service.
    - **Use Case:** Synchronization across distributed nodes, coordination in large-scale systems (e.g., Google Chubby).
    - **Details:** Chubby provides locks and coordination primitives. It ensures that only one node can hold a lock at a time, preventing conflicts and ensuring synchronization.

###  15. **Delta Sync:**
- **Purpose:** Transfers only the changes (delta) between versions to minimize data transfer in distributed systems.
    - **Use Case:** Distributed file synchronization (e.g., Dropbox), data replication, and efficient communication between nodes.
    - **Details:** Delta sync involves transferring only the changes between versions of data, reducing the amount of data transmitted and improving efficiency.

###  16. **Write-Ahead Log (WAL):**
   - **Purpose:** Ensures durability by writing changes to a log before applying them to the data store.
   - **Use Case:** Distributed databases like PostgreSQL use write-ahead logs for durability. Before changes are applied to the main data store, they are first written to a log. In the event of a crash, the database can recover by replaying the log.

###  17. **Split Brain:**
   - **Purpose:** Mitigates the risk of network partitions causing inconsistencies by preventing conflicting decisions in different parts of the system.
   - **Use Case:** Systems using split-brain resolution mechanisms like ZooKeeper. In ZooKeeper, an ensemble of nodes elects a leader to avoid conflicting decisions and maintain consistency.

###  18. **Lease (Lease Mechanism):**
   - **Purpose:** Provides a time-limited ownership mechanism to prevent split-brain scenarios and coordinate actions among distributed nodes.
   - **Use Case:** Apache Hadoop's HDFS (Hadoop Distributed File System) uses a lease mechanism to manage file access. A lease is granted for a certain period, preventing conflicting modifications by multiple clients.

###  19. **Compensating Transaction:**
   - **Purpose:** Handles the reversal of a series of operations in case of a failure, ensuring consistency in distributed transactions.
   - **Use Case:** Order processing systems often use compensating transactions. If a payment fails after an order is shipped, a compensating transaction might initiate a refund.

###  20. **Eventual Consistency:**
   - **Purpose:** Allows replicas to diverge temporarily and guarantees that, given enough time, all replicas will converge to a consistent state.
   - **Use Case:** Amazon DynamoDB is an example of a system that prioritizes eventual consistency. Read operations may return stale data but eventually converge to a consistent state.

###  21. **Idempotent Receiver:**
   - **Purpose:** Ensures that processing the same message multiple times has the same effect as processing it once.
   - **Use Case:** Message queues like Apache Kafka ensure idempotent message processing. If a consumer processes the same message multiple times, the result is the same as processing it once.

###  22. **Caching:**
   - **Purpose:** Stores frequently accessed data closer to the computation nodes to reduce latency and improve performance.
   - **Use Case:** Content Delivery Networks (CDNs) use caching extensively. Cached content is stored at edge locations, reducing the distance between users and content.

###  23. **Token Bucket:**
   - **Purpose:** Controls the rate of requests or events to prevent resource exhaustion and maintain a balanced load.
   - **Use Case:** Rate limiting in APIs is often implemented using token buckets. Each token represents permission for one request, controlling the rate at which requests are processed.

###  24. **Version Vectors:**
   - **Purpose:** Tracks the causal relationship between events in a distributed system to resolve conflicts and ensure consistency.
   - **Use Case:** Version vectors are used in distributed databases like Riak. They help track and manage causality in distributed systems, especially during conflict resolution.

###  25. **Hedged Requests:**
   - **Purpose:** Sends multiple requests in parallel and returns the fastest response, improving overall system responsiveness.
   - **Use Case:** In systems like Elasticsearch, hedged requests are used to improve search query responsiveness. Multiple nodes are queried simultaneously, and the fastest response is used.

###  26. **Leaderless Replication:**
   - **Purpose:** Distributes the responsibility of coordination and data storage across multiple nodes, eliminating the need for a designated leader.
   - **Use Case:** Amazon DynamoDB Global Tables use leaderless replication. Each node in the DynamoDB table is responsible for both reads and writes, contributing to high availability and fault tolerance.

###  27. **Event Sourcing with CQRS:**
   - **Purpose:** Combines Event Sourcing and Command Query Responsibility Segregation to create an event-driven architecture with separate read and write models.
   - **Use Case:** Eventuate is an example of a framework that combines Event Sourcing with CQRS. It allows applications to capture events and separate the read and write models.

###  28. **Bulkhead Pattern:**
   - **Purpose:** Isolates components or services to prevent the failure of one from affecting others.
   - **Use Case:** In a microservices architecture, each microservice operates independently, preventing failures in one service from affecting others.

###  29. **Chubby (Distributed Lock Service):**
   - **Purpose:** Coordinates distributed systems by providing a distributed lock service.
   - **Use Case:** Google Chubby is a distributed lock service used for coordination in large-scale systems. It provides locks and ensures mutual exclusion.

###  30. **Delta Sync:**
   - **Purpose:** Transfers only the changes (delta) between versions to minimize data transfer in distributed systems.
   - **Use Case:** Dropbox uses delta sync to minimize data transfer during file synchronization. Only the changes between versions are transferred, reducing bandwidth usage.

 
 