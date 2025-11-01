# Advanced Backend Interview Scenarios (Node.js, Express.js, MongoDB)

This section presents advanced real-world scenarios for backend interviews, framed as discussions between an interviewer and a candidate. Each includes applied reasoning, secure patterns, and optimized solutions for Node.js, Express.js, MongoDB, and REST API development.

---

## 24. Handling User Registration Race Conditions in Mongoose

**Interviewer:** Imagine two users attempt to register with the same email simultaneously. How would you prevent duplicate account creation?

**Candidate:**  
I would define a unique index on the email field and handle duplicate key errors gracefully after insertion. Even if two requests hit at the same time, only one write will succeed.

**Example:**
const userSchema = new mongoose.Schema({
email: { type: String, unique: true },
password: String
});

try {
await User.create({ email, password });
} catch (err) {
if (err.code === 11000) {
return res.status(409).json({ message: 'Email already registered' });
}
}


---

## 25. Returning Stale Data After an Update in Express/MongoDB

**Interviewer:** Sometimes, updated documents aren’t reflected in the response. How do you handle stale reads?

**Candidate:**  
This can happen due to read preferences or caching. I ensure that read operations use the primary node, clear or refresh caches after updates, and use document versioning or timestamps.

**Example:**
const updated = await User.findByIdAndUpdate(id, data, { new: true });
res.json(updated);


Adding `{ new: true }` ensures the API returns the most recent document.

---

## 26. Securing a Public-Read, Admin-Write API in Express

**Interviewer:** Suppose you have an endpoint where anyone can view data, but only admins can modify it. How would you set that up?

**Candidate:**  
I’d make GET routes public, and wrap POST/PUT/DELETE routes with authentication and role-based authorization middleware.

**Example:**
app.get('/products', getAllProducts);
app.post('/products', auth, adminOnly, createProduct);


This separation ensures safe public access without compromising administrative integrity.

---

## 27. Validating New Passwords Against the Old Password Using Bcrypt

**Interviewer:** How would you ensure a user cannot reuse their old password?

**Candidate:**  
Before updating, compare the new password (plain text) against the stored hashed password. If it matches, reject the update.

**Example:**
const isSame = await bcrypt.compare(newPassword, user.password);
if (isSame) return res.status(400).json({ message: 'Use a different password' });


---

## 28. Optimizing Slow MongoDB Queries in Node APIs

**Interviewer:** How would you improve query performance in a slow API?

**Candidate:**  
I would:
- Add indexes on frequently queried fields.  
- Implement pagination with `limit` and `skip`.  
- Cache frequent reads with Redis.  
- Return only required fields using projections.

**Example:**
User.find({ isActive: true })
.select('name email')
.skip(0)
.limit(20);


---

## 29. Preventing Sensitive Data Leakage in API Responses

**Interviewer:** A developer accidentally exposed passwords in an API response. What would you recommend?

**Candidate:**  
Always sanitize outputs using Mongoose `select()` or custom `toJSON()` to remove confidential fields.

**Example:**
userSchema.methods.toJSON = function () {
const obj = this.toObject();
delete obj.password;
delete obj.tokens;
return obj;
};


This ensures sensitive information never leaves the backend.

---

## 30. Migrating Session/Cookie Auth to JWT

**Interviewer:** You’re tasked to move a legacy Express app from session cookies to JWT. What’s your migration strategy?

**Candidate:**  
- Use short-lived access tokens and long-lived refresh tokens.  
- Store refresh tokens securely (e.g., in Redis).  
- Use httpOnly cookies for browser safety.  
- Implement token blacklisting and rotation for revocation.

**Example:**
res.cookie('token', accessToken, { httpOnly: true, secure: true });


---

## 31. Enforcing Self-Deletion in User DELETE Route

**Interviewer:** How do you ensure that only the logged-in user can delete their own account?

**Candidate:**  
By verifying that the JWT’s user ID matches the user ID in the route or confirming the user has admin rights.

**Example:**
if (req.user.id !== req.params.id && req.user.role !== 'admin') {
return res.status(403).json({ message: 'Unauthorized' });
}


---

## 32. Updating Mongoose Schema for Existing Documents

**Interviewer:** You added a new field to an existing schema. How do you populate it for old documents?

**Candidate:**  
I’d define a default in the schema and run a script to update existing records.

**Example:**
await User.updateMany({ newField: { $exists: false } }, { $set: { newField: 'default' } });


This ensures backward compatibility without data inconsistency.

---

## 33. Mitigating Brute-Force Login Attacks

**Interviewer:** How would you protect your login API from brute-force attacks?

**Candidate:**  
I would add rate-limiting, failed attempt tracking, and CAPTCHA verification after multiple failed logins.

**Example:**
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
windowMs: 15 * 60 * 1000,
max: 5,
message: 'Too many login attempts. Please try again later.',
});
app.post('/login', limiter, loginController);


---

## 34. Managing Environment-Specific Configurations

**Interviewer:** How do you manage environment configs in a large-scale Node.js project?

**Candidate:**  
Use `.env` files per environment, loaded via the `dotenv` package. Keep them out of version control.

**Example:**
require('dotenv').config();

const db = process.env.DB_URI;
const port = process.env.PORT || 3000;


This approach ensures configurable deployment while protecting secrets.

---

## 35. Diagnosing Hanging API Requests

**Interviewer:** A user reports that some API requests never finish. How do you diagnose that?

**Candidate:**  
First, I check that `res.send()` or `next()` is called in all routes. Then I verify that the database operation resolves and no middleware is blocking execution.

**Example:**
app.use((err, req, res, next) => {
console.error(err);
res.status(500).json({ message: 'Internal Server Error' });
});


Enabling error-handling middleware ensures unhandled promises or exceptions don’t hang requests.

---

_End of Advanced Backend Interview Q&A_