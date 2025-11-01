# MongoDB Interview Preparation  

## Introduction
NoSQL databases like MongoDB offer flexibility and scalability for modern applications. [Your Name] presents crucial MongoDB interview topics with practical, security-focused answers for student mastery.

---

### 8. What are the key differences between SQL and NoSQL databases?
**Explanation:** Database fundamentals for architectural decisions.
**Answer:**  
SQL databases use rigid schemas and ACID compliance. NoSQL (MongoDB) supports dynamic schema, horizontal scaling, and performance trade-offs for speed and flexibility.

---

### 9. How does MongoDB store data and what is a BSON document?
**Explanation:** Understanding storage format and its advantages.
**Answer:**  
MongoDB stores documents as BSON (Binary JSON), which adds data types (dates, binary) beyond regular JSON and is optimized for efficient handling.

---

### 10. How can you prevent NoSQL injection attacks in MongoDB?
**Explanation:** Defense against malicious data operations.
**Answer:**  
Always validate/sanitize user input, use ORM/ODM layers like Mongoose for abstraction, and avoid using client-supplied queries as selectors or operators.

---

### 11. Describe Mongoose and its advantages when working with MongoDB.
**Explanation:** Managed database interactions.
**Answer:**  
Mongoose objects data with schemas, enforces field validation, offers middleware/hook logic, and protects application integrity in Node.js projects.

---
