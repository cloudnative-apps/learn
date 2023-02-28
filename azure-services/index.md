# Azure Services



## Azure Event Hubs

Azure Event Hubs is a managed, real-time, event streaming platform provided by Microsoft Azure. It is a highly scalable and flexible platform that can process millions of events per second.

Here is a high-level overview of how Azure Event Hubs works:

### Data Ingestion: 
Applications send data to Azure Event Hubs using a sender client library. The data can be sent in any format such as JSON, XML, or binary.

### Event Hubs
 Azure Event Hubs is a distributed, partitioned stream of events. The incoming events are partitioned and distributed across multiple nodes in the Azure infrastructure. Each partition can contain a subset of the data and is assigned a unique identifier.

### Producers
 Producers are applications that send data to the Event Hubs. A producer can send data to a specific partition or let the Event Hubs distribute the data across partitions.

### Consumers
 Consumers are applications that receive data from the Event Hubs. A consumer can read data from one or more partitions and can process the data in real-time. The consumers can use a receiver client library to receive data from Event Hubs.

### Event Processor Host
 The Event Processor Host is a library provided by Azure that simplifies the process of receiving and processing events from Event Hubs. The Event Processor Host provides features such as load balancing, checkpointing, and scaling.

### Scaling
Azure Event Hubs can scale horizontally to handle millions of events per second. The Event Hubs can automatically adjust the number of nodes and partitions based on the incoming data rate.

### Checkpointing
 Azure Event Hubs provides a built-in checkpointing mechanism that enables consumers to keep track of their progress. The checkpointing mechanism allows consumers to resume reading from where they left off in case of failure.

**How checkpoint works**

In the context of Azure Event Hubs, a checkpoint is a mechanism that enables a consumer to keep track of its progress while reading events from a partition. When a consumer reads events from a partition, it processes the events and moves forward to read the next batch of events. The checkpoint mechanism allows the consumer to store the information about the last event it read from the partition, so that it can resume reading from where it left off in case of a failure or a restart.

Here's how checkpointing works in Azure Event Hubs:

**Checkpoint Store:** Azure Event Hubs stores checkpoint information in a separate storage account that can be configured by the consumer. The checkpoint store can be an Azure Blob Storage account or an Azure Cosmos DB account.

**Checkpointing API:** Azure Event Hubs provides a checkpointing API that allows consumers to store the checkpoint information in the checkpoint store. The consumer can use the checkpointing API to store the offset of the last event it read from a partition.

**Checkpointing Frequency**: The frequency of checkpointing can be configured by the consumer. The consumer can choose to checkpoint after processing a fixed number of events, after processing events for a fixed duration of time, or after processing events up to a specific time.

**Checkpointing Responsibility**: The responsibility of checkpointing is on the consumer. The consumer needs to ensure that it checkpoints the last event it processed before shutting down or before another consumer takes over the partition.

**Checkpoint Recovery**: When a consumer restarts or takes over a partition, it reads the checkpoint information from the checkpoint store. The checkpoint information provides the offset of the last event that was processed by the previous consumer. The new consumer can then resume reading events from where the previous consumer left off.

Checkpointing is a crucial mechanism in Azure Event Hubs to ensure that consumers can resume reading events from where they left off in case of a failure or a restart. Checkpointing enables consumers to process large volumes of data without the risk of losing progress or processing the same data multiple times. It is important to configure checkpointing correctly to ensure that it meets the requirements of the consumer's use case.


### High level System design
             +----------------+        +----------------+         +-----------------+
             | Producer App 1 |        | Producer App 2 |         | Producer App N  |
             +-------+--------+        +-------+--------+         +-------+---------+
                     |                          |                          |
               +-----v--------------------------v--------------------------v-----+
               |                        Azure Event Hubs                        |
               |                                                                 |
               |     +------------------+   +-----------------+   +------------------+
               |     | Partition 1      |   | Partition 2     |   | Partition N      |
               |     +--------+---------+   +--------+--------+   +--------+---------+
               |              |                      |                     |
               |        +-----v------------+   +-----v------------+   +----v------------+
               |        | Consumer Group 1 |   | Consumer Group 2 |   | Consumer Group N |
               |        +-----------------+   +-----------------+   +-----------------+
               |                  |                      |                     |
               |     +------------v---------------+  +--v-----------------v--+
               |     |     Event Processor Host 1 |  |     Event Processor Host N |
               |     +---------------------------+  +---------------------------+
               |                                                                 |
               +-----------------------------------------------------------------+

In this diagram, we have multiple producer applications that send data to Azure Event Hubs. The data is then distributed across multiple **partitions** in the Event Hubs. Each partition can contain a subset of the data and is assigned a unique identifier.


_Consumers_ can read data from one or more partitions by using a consumer group. A consumer group is a view of a specific subset of the partitions in an Event Hub. Multiple consumer groups can read data from the same Event Hub simultaneously. Each consumer group has its own offset in each partition, so it can read the data independently.

The Event Processor Host is a library provided by Azure that simplifies the process of receiving and processing events from Event Hubs. The Event Processor Host provides features such as load balancing, checkpointing, and scaling. Multiple instances of the Event Processor Host can be running in parallel to process data from multiple partitions.

### Security
Azure Event Hubs provides security features such as access control, encryption, and firewalls. The data is encrypted in transit and at rest, and the access to the Event Hubs can be controlled using Azure Active Directory or Shared Access Signatures.

In summary, Azure Event Hubs is a managed, real-time, event streaming platform that enables applications to ingest, process, and analyze large volumes of data. The data is partitioned and distributed across multiple nodes, and can be processed in real-time using consumer applications. Azure Event Hubs provides features such as scaling, checkpointing, and security to ensure reliability and security of the data.

## Cosmos DB
Cosmos DB is a globally distributed, multi-model database service. It is designed to be highly available, globally scalable, and offer low-latency performance for different types of applications.

Cosmos DB's architecture is based on the principles of the Azure Service Fabric, which is a distributed systems platform used to build and deploy microservices-based applications. The Service Fabric architecture provides high availability, scalability, and reliability through the use of distributed systems techniques such as replication, partitioning, and quorum-based protocols.

The key components of Cosmos DB's architecture are:

### Components

**Partitioning**: Cosmos DB partitions data across multiple nodes to achieve horizontal scalability and low-latency performance. Partitioning is done automatically by the system based on the partition key, which determines the data distribution across different nodes.

**Multi-model support**: Cosmos DB supports multiple data models, including document, key-value, graph, and column-family. This allows developers to choose the right data model for their application and reduces the need for separate databases for different data models.

**Replication**: Cosmos DB replicates data across multiple regions to achieve high availability and disaster recovery. Replication is done automatically by the system and provides configurable consistency levels to meet different application requirements.

**Global distribution**: Cosmos DB is a globally distributed database service that enables users to replicate data across multiple regions worldwide. This allows applications to provide low-latency access to data for users located in different parts of the world.

**Consistency**: Cosmos DB provides configurable consistency levels, ranging from strong to eventual consistency, to enable developers to choose the right level of consistency for their application. This allows applications to balance data consistency and performance trade-offs based on their specific requirements.

**API layer**: Cosmos DB provides a unified API layer that abstracts the underlying data models and enables developers to access data using different programming languages and protocols. This API layer includes support for popular APIs such as SQL, MongoDB, Cassandra, and Azure Table Storage.

### high-level diagram 
             +-------------------+
             |      Frontend     |
             |  Application/API  |
             +--------+----------+
                      |
                      |
                      |
             +--------v----------+
             |      Gateway      |
             +--------+----------+
                      |
                      |
                      |
             +--------v----------+
             |     Query Layer   |
             |  (partitioned by  |
             |    partition key) |
             +--------+----------+
                      |
                      |
         +------------v-----------+
         |       Cosmos DB        |
         |(distributed database) |
         +------------+-----------+
                      |
                      |
                      |
       +--------------v-------------+
       |  Replication and Sync Layer |
       +--------------+-------------+
                      |
                      |
       +--------------v-------------+
       |    Physical Storage Layer   |
       +------------------------------+

This diagram shows the various components of Cosmos DB and their interactions:

**Frontend**: This component represents the application or API that interacts with Cosmos DB.

**Gateway**: The gateway component receives requests from the frontend and forwards them to the query layer.

**Query Layer**: The query layer is responsible for processing queries and updates to the database. It is partitioned by the partition key to achieve horizontal scalability and low-latency performance.

**Cosmos DB**: This is the distributed database that stores and manages the data. It is designed to be globally distributed and provide configurable consistency levels.

**Replication and Sync Layer**: This component is responsible for replicating data across multiple regions and ensuring data consistency. It also handles conflict resolution and provides disaster recovery capabilities.

**Physical Storage Layer**: This is the layer that stores the data on physical storage devices.


### Indexing in Cosmos DB
In Cosmos DB, automatic indexing is a feature that automatically indexes all properties of documents stored in a collection without requiring any explicit schema definition or index creation. This feature helps developers to build applications faster by eliminating the need for manual index creation and maintenance.

Here is how automatic indexing works in Cosmos DB:

Property Extraction: When a document is inserted into a collection, the automatic indexing system automatically extracts all properties and their values from the document.

Indexing Policy: The indexing policy for the collection determines which properties are indexed and how they are indexed. By default, all properties are indexed using the range index.

Range Indexing: Range indexing is used to support query predicates on numeric, string, and date/time data types. The system creates a separate index for each property of these data types and stores the indexed values in a B-tree structure.

Spatial Indexing: Spatial indexing is used to support geospatial queries on spatial data types. The system automatically creates a spatial index for each property of a spatial data type.

Composite Indexing: Composite indexing is used to support queries on multiple properties. The system automatically creates composite indexes for frequently used combinations of properties.

Automatic Index Maintenance: The system automatically maintains the indexes by updating them when the properties of the documents are modified.

Consistency: The system provides configurable consistency levels for queries on the indexed properties. The consistency level determines the level of consistency guarantee for the query results based on the time and order of the index updates.



### Autoscaling
Autoscaling in Cosmos DB is a feature that automatically adjusts the throughput of a database or a container based on the workload and usage patterns. Autoscaling enables applications to handle varying workloads and traffic spikes while ensuring optimal performance and cost efficiency.

Here is how autoscaling works in Cosmos DB:

**Throughput**: In Cosmos DB, throughput is a measure of the database's or container's provisioned resources, which includes CPU, memory, I/O, and network bandwidth. Throughput is expressed in Request Units (RUs), which is a currency for the database operations. Each operation in Cosmos DB consumes a certain amount of RUs based on its complexity, size, and consistency level.

**Metrics**: The autoscaling feature uses various metrics to monitor the workload and usage patterns of the database or container. The metrics include CPU utilization, storage utilization, request rate, and latency. The metrics are collected and aggregated over a period of time to provide a holistic view of the workload.

**Scaling Trigger**: Based on the collected metrics, the autoscaling feature triggers scaling operations to adjust the throughput of the database or container. The scaling operations can be either upscaling or downscaling, depending on the workload and usage patterns.

**Upscaling**: When the workload increases, the autoscaling feature triggers an upscaling operation to increase the throughput of the database or container. The upscaling operation can be done either by increasing the number of physical partitions or by increasing the provisioned RUs.

**Downscaling**: When the workload decreases, the autoscaling feature triggers a downscaling operation to reduce the throughput of the database or container. The downscaling operation can be done either by decreasing the number of physical partitions or by decreasing the provisioned RUs.

**Configuration**: The autoscaling feature can be configured to use different scaling policies, which define the rules and thresholds for triggering scaling operations. The scaling policies can be based on the maximum and minimum RUs, the percentage of CPU utilization, or the maximum latency.

**Integration**: The autoscaling feature can be integrated with Azure Monitor, which provides a centralized monitoring and alerting system for the database or container. The integration enables proactive monitoring and troubleshooting of the database or container based on the collected metrics and alerts.







Sharad Singh
How backup is done in Cosmos 
In Cosmos DB, backups are done automatically by the service to ensure data durability and availability. Cosmos DB provides two types of backups - automated backups and manual backups.

Automated Backups:
Cosmos DB automatically takes backups of all the data stored in a container or a database at regular intervals. The frequency of backups and retention period can be configured by the user. The automated backups are stored in Azure Storage Account and can be restored using the Azure Portal, Azure CLI or REST API. The automated backups are taken at the partition level and are consistent within a partition key range.

Manual Backups:
In addition to automated backups, Cosmos DB also provides the ability to take manual backups at any point in time. Manual backups are useful when a specific version of the data needs to be restored or for taking a backup before making major changes to the data. Manual backups are stored in Azure Storage Account and can be restored using the Azure Portal, Azure CLI or REST API.

Here is how backup works in Cosmos DB:

Backup Policy: The user configures the backup policy for a container or a database, which includes the backup frequency and retention period. The backup policy can be set using Azure Portal, Azure CLI or REST API.

Backup Schedule: Based on the backup policy, Cosmos DB takes automated backups at regular intervals. The backup schedule is based on the partition key ranges and is optimized for minimum impact on the application performance.

Backup Storage: The automated backups are stored in Azure Storage Account in the same region as the Cosmos DB account. The backup storage is encrypted and provides durability and availability guarantees.

Backup Restore: To restore a backup, the user can use the Azure Portal, Azure CLI or REST API. The restore operation creates a new container or database and restores the data from the backup storage.

Backup Monitoring: Cosmos DB provides monitoring and alerting capabilities for backups. The user can monitor the backup status, storage usage, and retention period using Azure Portal, Azure CLI or REST API. The user can also set up alerts for backup failures, storage usage, and retention period.

In summary, backup in Cosmos DB is done automatically at regular intervals based on the configured backup policy. The automated backups are stored in Azure Storage Account and can be restored using Azure Portal, Azure CLI or REST API. The user can also take manual backups at any point in time. The backup feature provides data durability and availability guarantees and can be monitored using Azure Portal, Azure CLI or REST API.




Sharad Singh
How to purge old records from cosmoscdb
To purge old records from Cosmos DB, you can use the TTL (Time to Live) feature provided by Cosmos DB. TTL is a mechanism that automatically deletes expired documents from a container or a database based on a configurable time-to-live value. The TTL value is specified in seconds and can be set on a per-document basis or on a container level.

Here are the steps to purge old records from Cosmos DB using TTL:

Set TTL on Container: You can set the TTL value for a container using Azure Portal, Azure CLI or REST API. The TTL value can be set in seconds and applies to all documents in the container.

Set TTL on Documents: Alternatively, you can set the TTL value on a per-document basis using the "_ttl" property. The "_ttl" property specifies the time-to-live value for a document in seconds. When a document expires, it is automatically deleted from the container.

Monitor TTL Expiration: You can monitor the TTL expiration using the Cosmos DB metrics or using Azure Monitor. The metrics provide information on the number of expired documents and the rate of expiration.

Purge Expired Documents: Once the documents expire and are deleted, they are still stored in the Cosmos DB backup for the retention period. To permanently delete the expired documents, you can use the Azure Portal, Azure CLI or REST API to purge the deleted documents. The purge operation removes the deleted documents from the backup storage.

It's important to note that once the documents are deleted using the TTL feature, they cannot be recovered. Therefore, it's recommended to test the TTL feature in a non-production environment before enabling it in production.

In summary, to purge old records from Cosmos DB, you can use the TTL feature provided by Cosmos DB. TTL automatically deletes expired documents from a container or a database based on a configurable time-to-live value. The TTL value can be set on a per-document basis or on a container level using Azure Portal, Azure CLI or REST API. The expired documents can be monitored using the Cosmos DB metrics or Azure Monitor, and can be purged using Azure Portal, Azure CLI or REST API.




