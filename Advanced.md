# Advanced Situation-Based Backend Interview Scenarios  


## Introduction
Real-world development brings complex challenges. In this section, we provide situational questions and in-depth solutions for advanced Node.js, Express.js, MongoDB, and REST API interviews.

---

### 24. User registration race conditions in Mongoose
**Answer:**  
Define unique indexes and always handle duplicate key errors after attempted insertion, ensuring only one registration per unique email.

---

### 25. Returning stale data after update in MongoDB/Express
**Answer:**  
Check read preference (read from primary), invalidate or refresh cache after update, and use timestamps/versioning.

---

### 26. Public-Read, Admin-Write API route protection in Express
**Answer:**  
Create public GET endpoints and protect POST/PUT/DELETE with auth and admin middleware.

---

### 27. Validating new password is different from old (bcrypt)
**Answer:**  
Compare new password against stored hash with bcrypt’s `compare` before updating to ensure they differ.

---

### 28. Optimizing slow MongoDB queries in Node.js APIs
**Answer:**  
Introduce indexes, paginate large datasets, cache frequent queries (Redis), and project only necessary fields.

---

### 29. Preventing leakage of sensitive data in API output
**Answer:**  
Exclude password and token fields using query `.select()` or custom `.toJSON()` logic before returning user data.

---

### 30. Migrating session/cookie auth to JWT in Express.js
**Answer:**  
Consider token revocation and blacklisting, use short-lived access and refresh tokens, prefer `httpOnly` storage, and audit for XSS.

---

### 31. Enforcing self-deletion in DELETE user route
**Answer:**  
Check that JWT user ID matches route param or ensure admin role before allowing deletion.

---

### 32. Updating MongoDB schema for existing documents
**Answer:**  
Set model defaults and run scripting to update missing fields in existing records.

---

### 33. Mitigating brute-force attacks on login
**Answer:**  
Use rate-limiting middleware, lock accounts after failed attempts, and implement CAPTCHA after too many failures.

---

### 34. Managing environment-specific configs in Node.js
**Answer:**  
Keep secrets in `.env` files loaded by `dotenv`, ignore `.env` in version control, and reference variables via `process.env`.

---

### 35. Diagnosing and fixing hanging API requests
**Answer:**  
Audit for incomplete responses or missed `next()`/`send()` calls, verify DB operations, and always include error handlers.

---
