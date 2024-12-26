# system_design

my rather cute attempts at solving system design problems :)

# Motivation

WIP

# Framework to solving System Design problems

## Clarify the Problem
  Ask questions to ensure you fully understand the requirements.

  **Functional requirements**: What does the system need to do? (e.g., real-time messaging, data storage, etc.)

  **Non-functional requirements**: Performance (latency, throughput), availability, scalability, fault tolerance, and security.

  **Edge cases**: Are there specific constraints or limits? (e.g., high load, low bandwidth, specific response time)

  __*Example*__: If you're asked to design a URL shortening service like Bitly, you should clarify:

  - Will the service allow custom aliases?
  
  - What is the expected scale (number of URLs, requests per second)?
  
  - What are the availability and fault tolerance requirements?

  - How will the service handle URL analytics (clicks, locations, etc.)?
## Define System Scope
**Identify the boundaries of the system**. This helps to narrow the scope and avoid trying to solve too many problems at once.

**Break the system into subsystems**. For example, in a URL shortener, you could divide it into:

- URL creation and mapping.
- Redirecting users to the original URL.
- Analytics (tracking clicks).

**Trade-offs**: Consider the trade-offs you’ll make regarding consistency, availability, and partition tolerance (CAP theorem).

## High-Level Architecture
Start with a high-level design and sketch it out.

Identify major components, such as databases, APIs, caching layers, and services.

**Examples of major components**:

- *Load Balancer*: To distribute traffic across servers.
- *API Gateway*: For routing requests to microservices.
- *Databases*: Relational (SQL) or NoSQL, depending on the use case.
- *Caching*: Redis or Memcached for high-speed lookups.
- *Message Queues*: Kafka or RabbitMQ for asynchronous processing.

Design a simple flow of how data will move through the system. 
Sketch out the request flow to understand how components interact.

**Example**:

For a URL shortener, the flow could be:

1. A user sends a request to create a short URL via the API Gateway.
2. The API service processes the request, stores the mapping (short URL -> original URL) in the database, and returns the short URL to the user.
3. When a user visits the short URL, the system fetches the original URL from the database and redirects them.
Track analytics (optional).


## Deep Dive into Key Components
Now, focus on important components of the system that need further clarification and optimization. Discuss these in detail:

**Database**: 

- Choose the appropriate type of database (SQL vs. NoSQL). For example, use NoSQL for scalable key-value pairs in a URL shortener.

- **Sharding**: Split data across multiple databases to handle large-scale traffic. Discuss your sharding strategy (e.g., range-based or hash-based).

- **Indexing**: Explain how you would index URLs for efficient retrieval.

**Scalability**:

- **Horizontal scaling**: Add more machines to distribute load. Discuss partitioning/sharding strategies.
- **Caching**: Introduce caching (e.g., Redis, Memcached) for frequently accessed data to reduce database load.

**Consistency**:

- Discuss **CAP theorem** and trade-offs between consistency, availability, and partition tolerance.

- For high availability, you may use techniques like eventual consistency, especially in large distributed systems.

**Load Balancing**:

- Use a load balancer (e.g., AWS Elastic Load Balancing, NGINX) to distribute incoming traffic across multiple instances.

- Consider sticky sessions or round-robin for session management.

**Fault Tolerance**:

- Discuss how the system can handle failures. You could use replication (e.g., master-slave database setups), failover mechanisms, and circuit breakers for resilience.

**API Design**:

- Define how clients (users, services) will interact with the system via REST or GraphQL APIs.

- Keep API endpoints simple, with proper HTTP methods (GET, POST, PUT, DELETE).

## Handle Scaling and High Availability

**Scaling**: As traffic grows, your system should scale. Consider:

- **Stateless design**: Ensure that each request can be handled independently.

- **Auto-scaling**: Set up automatic scaling for web servers and databases.

- **Database partitioning**: As your database grows, partition your data into smaller, more manageable pieces.

**Redundancy**: Ensure high availability by using multiple replicas and failover strategies.

- Replicate databases across regions or availability zones to maintain uptime in case of failure.
- Use content delivery networks (CDNs) for low-latency access to static resources.

## Monitoring and Maintenance

- **Logging**: Implement logging for traceability. Tools like ELK stack (Elasticsearch, Logstash, Kibana) can help analyze logs.

- **Metrics**: Monitor system health using metrics (e.g., latency, error rates, traffic). Tools like Prometheus and Datadog are often used.

- **Alerts**: Set up alerts for abnormal behavior (e.g., high latency, service down).

## Trade-offs and Limitations
- Be aware of trade-offs and be ready to discuss them:

  - If you increase consistency, you may reduce availability or performance.
  - Sharding introduces complexity but is necessary for scalability.
  - Eventual consistency may be acceptable for some systems (e.g., caching, analytics), but not for others (e.g., financial transactions).

- Explain why you chose one design over another. For example:

  - "I chose a NoSQL database because the system needs to handle billions of URL mappings and scale horizontally."
  - "I opted for a caching layer to reduce database hits and improve latency for frequently requested URLs."


## Wrap-Up with Future Improvements

Talk about future improvements or how the system can evolve:

- Data sharding strategies as the system grows.
- Possible use of machine learning to predict hot URLs and pre-cache them.
- Implementing API rate limiting to prevent abuse.

# Resources

Some helpful resources to get started or refreshed like myself.

## Videos

- [System Design Interview: A Step-By-Step Guide](https://www.youtube.com/watch?v=i7twT3x5yv8)

## Books

## Articles

# Practice makes perfect

be disciplined, lock in.
