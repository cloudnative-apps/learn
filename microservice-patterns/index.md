# Microservice Patterns


## DDD in brief

 



### Aggregates and aggregate roots

 * The aggregate pattern is a specific software design pattern within DDD. It promotes the collection of related entities and aggregates them into a unit.
 * Aggregates make it easier to define ownership of elements in large systems.
 Aggregates make it easier to enforce certain rules for data and validation across multiple objects.
 *  aggregates are conceptually composed of entities and value objects that relate to each other in some way
 ### Entity
 An entity represents data that might need to traverse multiple microservices and, as a result, needs to have an identity value that can uniquely identify it in any system.
  * Mutable
   * Independent Persistance
   * Identity Equality
 ### Value Object
   objects that are indeed defined by their values are value objects
   Value objects are allowed to have methods and behaviors, but their scope should be limited
   * Immutable
   * No Independent Persistance
   * Structutal Equality

###Resilient:
 We need to ensure that our service calls are done via durable channels. 
we need to consider two patterns that will make our services resilient, Retry and Circuit Breaker:
#### Retry pattern:
 Transient failures are common and temporary failures can derail an operation’s completion. However, they tend to go away by themselves, and we would prefer to retry the operation a few times, as opposed to failing the application’s operation completely. Using this pattern, we retry our service call a few times, based on a configuration, and should we not have any success, trigger a timeout. For operations that augment the data, we will need to be a bit more careful since the request might get sent and a transient failure might prevent a response from being sent. This doesn’t mean that the operation wasn’t actually completed, and retrying might lead to unwanted outcomes.

#### Circuit breaker pattern: 
This pattern is used to limit the number of times that we try to make the service call. Multiple calls might fail because of how long a transient failure takes to resolve itself, or the number of requests going to the service might cause a bottleneck in the available system resources and allocations. So, with this pattern, we could configure it to limit the amount of time we spend trying to call one service.

###Traced and monitored: 
We have established that a single operation can span multiple services. This brings another challenge in monitoring and tracing activities through all the services, from one originating point


## Http Status Codes
1xx (Informational): This communicates protocol-level information.
2xx (Success): This indicates that the request was accepted, and no errors occurred during processing.
3xx (Redirection): This indicates that an alternative route needs to be taken in order to complete the original request.
4xx (Client Error): This is the general range for errors that arise from the request, such as poorly formed data (400) or a bad address (404).
5xx (Server Error): These are errors that indicate that the server failed to complete the task for some unforeseen reason. When constructing our services, it is important that we properly document how requests should be formed, as well as ensure that our responses are in keeping with the actual outcomes.

### HTTP versus gRPC communication
We have seen examples of how we can interact with our services via the HTTP or RESTful methods and the gRPC protocol. Now, we need to have a clearer picture of when we would choose one method over the other.

##### The benefits of using REST include the following:

Uniformity: REST provides a uniform and standard interface for exposing functionality to subscribers.
Client-server independence: There is clear independence between the client and the server applications. The client only interacts with URIs that have been exposed or are needed for functionality. The server is oblivious to which clients might be subscribing.
Stateless: The server does not retain information about the requests being made. It just gets a request and produces a response.
Cacheable: API resources can be cached to allow for faster storage and retrieval of information per request.

##### The benefits of using gRPC  include the following:

Protocol buffers: Protocol buffers (or protobufs for short) serialize and deserialize data as binary, leading to higher data transmission speeds and smaller message sizes, given the much higher compression rate.
HTTP2: HTTP2, unlike HTTP 1.1, supports the expected request-response flow, as well as bidirectional communication. So, if a service receives multiple requests from multiple clients, it can achieve multiplexing by serving many requests and responses simultaneously.


### CAP Theorem:

Consistency: This means that every read operation against a data store will yield the current and most up-to-date version of the data, or an error will be raised if the system cannot guarantee that it is the latest.
Availability: This means that data will always be returned for a read operation, even if this is not the latest guaranteed version.
Partition tolerance: This means that systems will operate even when there might be transient errors that would stop a system under normal circumstances. Imagine we have minor connectivity issues between our services and/or messaging systems. Data updates will be delayed, but this principle will suggest that we need to choose between availability and consistency.
