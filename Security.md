# JWT & Password Security with Bcrypt  


## Introduction
Security underpins every backend project. This file details best practices for JWT-based authentication and secure password storage with Bcrypt.

---

### 12. What is JWT and how does it work for authentication?
**Explanation:** Modern token-driven user identity.
**Answer:**  
JSON Web Tokens encode user claims and are signed by the server. On login, the server issues a JWT, later verified for authentication in API calls.

---

### 13. How do you securely store JWTs on the client?
**Explanation:** Prevent token theft and misuse.
**Answer:**  
Best stored in `httpOnly` cookies inaccessible to JavaScript; avoid local storage/session storage to mitigate XSS risks.

---

### 14. How do you implement JWT validation middleware in Express.js?
**Explanation:** Controlled access for protected APIs.
**Answer:**  
Middleware extracts the token from request headers, validates it with the JWT secret, and attaches user info to the request object; requests without valid tokens are denied.

---

### 15. Why do we use bcrypt and how does it securely store passwords?
**Explanation:** Defense against brute-force and leaks.
**Answer:**  
Bcrypt creates slow, salted hashes for passwords, storing only the hash; password verification uses bcrypt’s `compare`, without exposing the plain password.

---
