# Express.js Interview Preparation  



---

### 4. What is Express.js and why do we use it?
**Explanation:** Framework foundation for Node.js web development.
**Answer:**  
Express.js is a lightweight framework simplifying HTTP server creation, routing, middleware use, and more. It abstracts tedious boilerplate and enables modular web and REST API construction.

---

### 5. What's middleware in Express.js? Give examples.
**Explanation:** Middleware drives Express's logic layering.
**Answer:**  
Middleware are functions with access to request, response, and the next handler. They enable chaining logic like logging, parsing, authentication, and error handling. Example:  
app.use(express.json());
app.use((req, res, next) => { console.log("Request received"); next(); });

---

### 6. Explain the difference between `app.get()` and `app.use()` in Express.js.
**Explanation:** Routing vs. middleware setup.
**Answer:**  
`app.get()` registers a handler for GET requests to a path, while `app.use()` applies middleware functions to all routes, optionally filtered by path.

---

### 7. How do you implement routing parameters and query string parsing in Express.js?
**Explanation:** Server-side data extraction techniques.
**Answer:**  
Path parameters:  
app.get('/users/:id', (req, res) => { const id = req.params.id; });


Query parameters:  
app.get('/search', (req, res) => { const term = req.query.term; });


---