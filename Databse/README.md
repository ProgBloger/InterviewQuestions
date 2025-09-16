# Database Interview Questions and Answers

A curated list of database interview questions with detailed answers.  
Use this repository to prepare for interviews or refresh your knowledge.

---

## 📑 Table of Contents

1. [Database Basics](#database-basics)  
2. [SQL](#sql)  
3. [NoSQL](#nosql)  
4. [Transactions & Concurrency](#transactions--concurrency)  
5. [Indexes & Optimization](#indexes--optimization)  
6. [Database Design](#database-design)  
7. [Replication & Sharding](#replication--sharding)  
8. [Backup & Recovery](#backup--recovery)  
9. [Miscellaneous](#miscellaneous)  

---

## Database Basics

### Q:  
**Answer:**  

---

## SQL

### Q:  
**Answer:**  

---

## NoSQL

### Q:  
**Answer:**  

---

## Transactions & Concurrency

### Q: What does the ACID acronym mean in databases?
**Answer:**
ACID defines the fuarantees of reliable transactions in relational databases:
  - **Atomicity** - all operations succeed or none do.
  - **Consistency** - a transaction brings the database from one valid state to another.
  - **Isolation** - transactions don't interfere; efects are not visible until commited.
  - **Durability** - once commited, data survives crashes or power loss.

Together, these ensure data correctness and reliability.

---

## Indexes & Optimization

### Q: What is the downside of using indexes in relational databases?
**Answer:**

Indexes speed up read queries but have trade-offs:
  - **Slower writes** - inserts, updates, and deletes must also update the index.
  - **Extra storage** - indexes take additional disk space.
  - **Maintenance cost** - poorly chosen or too many indexes can hurt performance instead of helping.

---

### Q: What are the isolation levels in databases?
**Answer:**

Isolation levels control how transactions interact when running at the same time.
They balance **consistency** vs **performance**. The ANSI SQL standart defines 4 levels:

  1. **Read Uncommited** - can see uncommited changes (dirty reads).
  2. **Read Commited** - only commited data visible (no dirty reads).
  3. **Repeatable Read** - same query in a transactions are fully isolated (like running one after antoher).
  4. **Serializable** - highest isolation; transactions are fully isolated (like running one after another).

Higher isolation = more consistency but less concurrency.

---

## Database Design

### Q:  
**Answer:**  

---

## Replication & Sharding

### Q:  
**Answer:**  

---

## Backup & Recovery

### Q:  
**Answer:**  

---

## Miscellaneous

### Q:  
**Answer:**  

---
