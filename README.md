# SYSTEM-DESIGN-BLUEPRINT
THIS REPO GIVES AN OVERVIEW OF SYSTEM DESIGN, DEFINING ALL ITS IMPORTANT TERMINOLOGIES.
System Design Blueprint: The Ultimate Guide
This repository breaks down the "System Design Blueprint" into its core components, explaining each concept and how they interconnect to form a robust, scalable, and resilient system.

Table of Contents
Introduction to System Design

The Lifecycle of a Request: An Overview

Core Components

DNS (Domain Name System)

Load Balancing

API Gateway

Frontend Servers & CDN

Backend Servers

Database

Cache

Object Storage

Message Queue

Services to Scale the System

Distributed ID Generator

Rate Limiting

Common Fan-out Services

Notification Service

Recommendation Engine

Analytics Service

Payment Service

Conclusion

Introduction to System Design
System design is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements. It's a crucial skill for software engineers, as it involves making high-level design choices that can have a significant impact on the performance, scalability, and reliability of an application. The blueprint in the image illustrates a modern, distributed system architecture that is commonly used for building large-scale web applications.

The Lifecycle of a Request: An Overview
Before we dive into the individual components, let's take a high-level look at how a user's request flows through the system:

DNS Resolution: The user enters a domain name (e.g., www.example.com) into their browser. The browser contacts a DNS server to resolve this domain name into an IP address.

Load Balancer: The request is sent to the IP address of the load balancer. The load balancer's job is to distribute incoming traffic across multiple servers to ensure no single server becomes a bottleneck.

API Gateway: The request then hits the API Gateway, which acts as a single entry point for all client requests. It can handle tasks like authentication, rate limiting, and routing requests to the appropriate backend service.

Backend Servers: The API Gateway forwards the request to one of the backend servers. These servers contain the core business logic of the application.

Data Layer (Database, Cache, Object Storage): The backend server may need to read or write data to fulfill the request. It will interact with the database, cache, and object storage as needed.

Asynchronous Operations (Message Queue): For long-running or non-critical tasks, the backend server can push a message to a message queue. This allows the server to respond to the user quickly while the task is processed asynchronously by other services.

Response: The backend server sends a response back to the API Gateway, which in turn sends it back to the user's browser.

Core Components
DNS (Domain Name System)
Definition: The DNS is the phonebook of the Internet. It translates human-readable domain names (like www.google.com) into machine-readable IP addresses (like 172.217.168.68).

How it works: When you type a domain name into your browser, your computer sends a request to a DNS resolver. The resolver then queries a series of DNS servers to find the corresponding IP address.

External Link: What is DNS? | How DNS Works - Cloudflare

Load Balancing
Definition: Load balancing is the process of distributing network traffic across multiple servers. This ensures that no single server bears too much of the load, which improves responsiveness and availability.

Types of Load Balancers:

Layer 4 (Transport Layer): Makes routing decisions based on IP addresses and ports.

Layer 7 (Application Layer): Can make more intelligent routing decisions based on the content of the request (e.g., URL, cookies).

Common Algorithms:

Round Robin: Distributes requests to servers in a rotating sequential manner.

Least Connections: Sends traffic to the server with the fewest active connections.

IP Hash: The IP address of the client is used to determine which server receives the request.

External Link: What is Load Balancing? - NGINX

API Gateway
Definition: An API Gateway is a single entry point for all client requests. It acts as a reverse proxy, routing requests from clients to the appropriate backend services.

Key Responsibilities:

Authentication and Authorization: Verifying the identity of the user and ensuring they have permission to access the requested resource.

Rate Limiting: Protecting backend services from being overwhelmed with too many requests.

Request Routing: Directing requests to the correct microservice.

SSL Termination: Offloading the work of encrypting and decrypting HTTPS traffic from the backend servers.

External Link: What is an API Gateway? - AWS

Frontend Servers & CDN
Frontend Servers: These servers are responsible for delivering the user interface of the application to the client's browser. This often involves serving static assets like HTML, CSS, and JavaScript files.

CDN (Content Delivery Network): A CDN is a network of geographically distributed servers that work together to provide fast delivery of Internet content. By caching content in locations closer to the user, a CDN can significantly reduce latency.

External Link: What is a CDN? | How do CDNs work? - Cloudflare

Backend Servers
Definition: Backend servers are where the core business logic of the application resides. They are responsible for processing user requests, interacting with the database, and performing other application-specific tasks.

Scaling:

Horizontal Scaling: Adding more servers to the pool of resources.

Vertical Scaling: Increasing the resources (CPU, RAM) of a single server.

Key Concepts:

Microservices: An architectural style that structures an application as a collection of small, independent services.

Monolithic Architecture: An architectural style where all the components of the application are combined into a single, unified unit.

External Link: Backend Development Explained - freeCodeCamp

Database
Definition: A database is an organized collection of data, generally stored and accessed electronically from a computer system.

Types of Databases:

Relational (SQL): Data is stored in tables with a predefined schema (e.g., MySQL, PostgreSQL).

Non-Relational (NoSQL): Data is stored in a variety of ways, such as key-value, document, or graph (e.g., MongoDB, Cassandra).

Scaling Databases:

Replication: Creating copies of the database to improve read performance and availability.

Sharding (Horizontal Partitioning): Splitting the data across multiple databases to improve write performance.

Vertical Partitioning: Storing different tables or columns in separate databases.

External Link: What is a Database? - Oracle

Cache
Definition: A cache is a high-speed data storage layer that stores a subset of data, typically transient in nature, so that future requests for that data are served up faster than is possible by accessing the data's primary storage location.

Cache Invalidation Strategies:

Write-through: Data is written to both the cache and the database at the same time.

Write-back (or Write-behind): Data is written to the cache first, and then written to the database at a later time.

Write-around: Data is written directly to the database, and the cache is updated only when the data is read.

Cache Eviction Policies:

LRU (Least Recently Used): The least recently used items are discarded first.

LFU (Least Frequently Used): The least frequently used items are discarded first.

FIFO (First-In, First-Out): The first items added to the cache are the first to be removed.

External Link: What is Caching? - AWS

Object Storage
Definition: Object storage is a data storage architecture that manages data as objects, as opposed to other storage architectures like file systems which manage data as a file hierarchy and block storage which manages data as blocks within sectors and tracks.

Use Cases: Storing large amounts of unstructured data, such as images, videos, and log files.

Examples: Amazon S3, Google Cloud Storage, Azure Blob Storage.

External Link: What is Object Storage? - Red Hat

Message Queue
Definition: A message queue is a form of asynchronous service-to-service communication used in serverless and microservices architectures. Messages are stored on the queue until they are processed and deleted.

Benefits:

Decoupling: Services can communicate without being directly connected to each other.

Asynchronous Processing: Long-running tasks can be offloaded to a separate worker process, allowing the main application to remain responsive.

Load Leveling: Helps to smooth out spikes in traffic.

Examples: RabbitMQ, Apache Kafka, Amazon SQS.

External Link: What is a Message Queue? - IBM

Services to Scale the System
Distributed ID Generator
Definition: In a distributed system, it's often necessary to generate unique IDs for things like user accounts, posts, or transactions. A distributed ID generator is a service that is responsible for creating these unique IDs in a way that is scalable and fault-tolerant.

Common Approaches:

UUID (Universally Unique Identifier): A 128-bit number that is guaranteed to be unique.

Snowflake (by Twitter): A custom ID generation scheme that combines a timestamp, a machine ID, and a sequence number.

External Link: Generating unique IDs in a distributed environment at high scale - Instagram Engineering

Rate Limiting
Definition: Rate limiting is a strategy for limiting network traffic. It's used to prevent DoS (Denial of Service) attacks, reduce costs, and prevent servers from being overloaded.

Common Algorithms:

Token Bucket: Each user has a bucket of tokens that are refilled at a fixed rate. Each request consumes a token.

Leaky Bucket: Requests are added to a queue and processed at a fixed rate. If the queue is full, new requests are dropped.

Fixed Window Counter: A counter is maintained for a fixed window of time. If the counter exceeds a threshold, requests are dropped.

Sliding Window Log: A log of request timestamps is kept for each user. When a new request comes in, the log is checked to see if the user has exceeded the rate limit.

External Link: An Introduction to Rate Limiting - Segment

Common Fan-out Services
"Fan-out" is a pattern where a single event or message triggers multiple actions or notifications. This is often implemented using a publish/subscribe (pub/sub) model with a message queue.

Notification Service
Function: Sends notifications to users via various channels (e.g., email, push notifications, SMS).

Trigger: Can be triggered by a variety of events, such as a new message, a friend request, or a new post.

Recommendation Engine
Function: Suggests content or products to users based on their past behavior and the behavior of similar users.

Trigger: Can be triggered when a user visits a product page, adds an item to their cart, or makes a purchase.

Analytics Service
Function: Collects and analyzes data about user behavior to provide insights into how the application is being used.

Trigger: Tracks a wide range of events, such as page views, clicks, and conversions.

Payment Service
Function: Handles all aspects of payment processing, including credit card validation, fraud detection, and transaction logging.

Trigger: Triggered when a user initiates a purchase.

Conclusion
This document provides a high-level overview of the key components of a modern system design blueprint. Each of these components is a complex topic in its own right, and there are many different ways to implement them. The best design for a particular application will depend on its specific requirements.
