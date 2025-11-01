# Server-Side Concepts: Security, Deployment, and Operations  
Authored by [Your Name]

## Introduction
A secure and resilient server-side is essential for successful APIs. This file, curated by [Your Name], shares best practices, common pitfalls, and essential deployment strategies.

---

### 19. How do you ensure API security on the server-side?
**Explanation:** Protecting data and infrastructure.
**Answer:**  
Validate and sanitize all inputs, use strong authentication/authorization (JWT/OAuth), enforce HTTPS, rate limiting, and monitor/log operations.

---

### 20. Explain CORS. How do you enable it in an Express.js API?
**Explanation:** Permit or deny cross-domain requests for APIs.
**Answer:**  
Enable CORS via Express middleware:  
const cors = require('cors');
app.use(cors());
Control origins and methods for better security.
