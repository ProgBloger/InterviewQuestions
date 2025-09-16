# System Design Interview Questions and Answers

A curated list of system design interview questions with detailed answers.  
Use this repository to prepare for interviews or refresh your knowledge.

---

## 📑 Table of Contents

1. [System Design Basics](#system-design-basics)  
2. [Scalability](#scalability)  
3. [Caching](#caching)  
4. [Load Balancing](#load-balancing)  
5. [Database in System Design](#database-in-system-design)  
6. [Messaging & Queues](#messaging--queues)  
7. [APIs & Communication](#apis--communication)  
8. [Microservices](#microservices)  
9. [Fault Tolerance & Reliability](#fault-tolerance--reliability)  
10. [Security](#security)  
11. [Miscellaneous](#miscellaneous)  

---

## System Design Basics

### Q:  
**Answer:**  

---

## Scalability

### Q:  
**Answer:**  

---

## Caching

### Q: How would you calculate the efficiency of a cache system like Redis?
**Answer:**

Cache efficiency is usually measured by the **cache hit ratio**:

$$
\text{Hit Ratio} = \frac{\text{Cache Hits}}{\text{Cache Hits} + \text{Cache Misses}}
$$

  - **Cache Hit** - request served from cache.
  - **Cache Miss** - request not in cache, fetched from the database.

A higher ration = more effective cache.

Other metrics:
  - **Latency Reduction** - compare response time with and without cache.
  - **Cost savings** - fewer DB queries or reduced server load.

---

## Load Balancing

### Q:  
**Answer:**  

---

## Database in System Design

### Q: How can you scale databases?
**Answer:**
Scaling can be done in two main ways:

  - **Vertical scaling (scale up)** - add more resources (CPU, RAM, storage) to a single server. Simple but limited and expensive.
  - **Horizontal scaling (scale out)** - add more servers and distribute data/load across them. Common strategies:
    - **Replication** - copy data to multiple servers (improves read performance and availability).
    - **Sharding (partitioning)** - split data into chunks by key/range and distribute across servers (improves write scalability).
    - **Caching** - reduce database load using in-memory stores like Redis.

---

## Messaging & Queues

### Q:  
**Answer:**  

---

## APIs & Communication

### Q:  
**Answer:**  

---

## Microservices

### Q:  
**Answer:**  

---

## Fault Tolerance & Reliability

### Q:  
**Answer:**  

---

## Security

### Q:  
**Answer:**  

---

## Miscellaneous

### Q:  
**Answer:**  

---
