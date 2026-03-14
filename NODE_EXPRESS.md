---

# Node.js + Express Cheat Sheet — Condensed & Practical

## Table of Contents

1. Node Philosophy
2. Project Setup
3. File Structure
4. Core Node Concepts
5. Express Basics
6. Routes
7. Request / Response
8. JSON APIs
9. Middleware
10. Static Files (frontend)
11. Forms & POST data
12. Query Parameters
13. Environment Variables
14. Calling Python Scripts
15. Async / Await
16. Error Handling
17. Logging
18. Simple Frontend Interaction
19. Fetch API (client → server)
20. Running the Server
21. Deployment Basics

---

# 1. Node Philosophy

Node = **JavaScript runtime for servers**

Core model :

```
Client (browser)
      ↓
HTTP request
      ↓
Node + Express server
      ↓
Route handler
      ↓
Response (HTML / JSON)
```

Example:

```
GET /simulation
↓
run simulation
↓
return JSON
```

---

# 2. Project Setup

Create project

```bash
mkdir webapp
cd webapp
```

Init node project

```bash
npm init -y
```

Install Express

```bash
npm install express
```

Install dev reload

```bash
npm install nodemon --save-dev
```

---

# 3. Basic File Structure

Minimal structure:

```
webapp
│
├── server.js
├── package.json
│
├── public
│   ├── index.html
│   ├── script.js
│   └── style.css
│
└── routes
    └── api.js
```

Meaning:

```
server.js → main backend
public/ → frontend files
routes/ → API logic
```

---

# 4. Core Node Concepts

### Import modules

```js
const express = require("express")
```

### Create server

```js
const app = express()
```

### Listen on port

```js
app.listen(3000, () => {
  console.log("Server running on port 3000")
})
```

---

# 5. Express Basics

Minimal server

```js
const express = require("express")

const app = express()

app.get("/", (req, res) => {
  res.send("Hello world")
})

app.listen(3000)
```

Run:

```
node server.js
```

Open:

```
http://localhost:3000
```

---

# 6. Routes

Routes define **what happens when a URL is called**

Syntax:

```
app.METHOD(PATH, HANDLER)
```

### GET route

```js
app.get("/hello", (req, res) => {
  res.send("hello")
})
```

### POST route

```js
app.post("/data", (req, res) => {
  res.send("received")
})
```

### Multiple routes

```js
app.get("/users", handler)
app.get("/simulation", handler)
app.post("/run", handler)
```

---

# 7. Request / Response

### Request (`req`)

Contains:

```
req.params
req.query
req.body
req.headers
```

Example:

```js
app.get("/user/:id", (req, res) => {
  console.log(req.params.id)
})
```

---

### Response (`res`)

Send data to client.

```js
res.send("hello")
```

Send JSON

```js
res.json({ result: 42 })
```

Send status

```js
res.status(404).send("not found")
```

---

# 8. JSON APIs

Most webapps use **JSON API**

Example route:

```js
app.get("/api/data", (req, res) => {

  const data = {
    agents: 100,
    step: 42
  }

  res.json(data)
})
```

Client receives:

```json
{
  "agents": 100,
  "step": 42
}
```

---

# 9. Middleware

Middleware = **functions executed before routes**

Example:

```js
app.use(express.json())
```

Purpose:

```
parse JSON
log requests
authentication
```

Example logger

```js
app.use((req, res, next) => {
  console.log(req.method, req.url)
  next()
})
```

---

# 10. Static Files

Serve frontend files.

```js
app.use(express.static("public"))
```

Now accessible:

```
public/index.html → /
public/script.js → /script.js
```

---

# 11. Forms & POST Data

Enable parsing:

```js
app.use(express.urlencoded({ extended: true }))
```

Example form POST

```html
<form action="/run" method="POST">
  <input name="agents">
  <button>Run</button>
</form>
```

Server:

```js
app.post("/run", (req, res) => {

  const agents = req.body.agents

  res.send("Simulation started")
})
```

---

# 12. Query Parameters

URL:

```
/simulation?agents=100&steps=50
```

Access:

```js
app.get("/simulation", (req, res) => {

  const agents = req.query.agents
  const steps = req.query.steps

})
```

---

# 13. Environment Variables

Used for:

```
ports
API keys
config
```

Install:

```bash
npm install dotenv
```

Create:

```
.env
```

Example:

```
PORT=3000
```

Use:

```js
require("dotenv").config()

const port = process.env.PORT
```

---

# 14. Calling Python Scripts

Very important for your use case.

Node can run Python via **child_process**.

```js
const { exec } = require("child_process")
```

Example:

```js
app.get("/run-sim", (req, res) => {

  exec("python simulation.py", (err, stdout, stderr) => {

    if (err) {
      return res.send("error")
    }

    res.send(stdout)
  })

})
```

---

# 15. Async / Await

Node is **asynchronous**.

Example:

```js
app.get("/data", async (req, res) => {

  const result = await fetchSomething()

  res.json(result)
})
```

---

# 16. Error Handling

Basic pattern:

```js
try {

  something()

} catch (err) {

  res.status(500).send("server error")

}
```

Global handler:

```js
app.use((err, req, res, next) => {

  console.error(err)

  res.status(500).send("error")

})
```

---

# 17. Logging

Basic logging:

```js
console.log("server started")
```

Better:

```bash
npm install morgan
```

Use:

```js
const morgan = require("morgan")

app.use(morgan("dev"))
```

---

# 18. Simple Frontend Interaction

HTML button:

```html
<button onclick="runSim()">Run</button>
```

JS:

```js
function runSim() {

  fetch("/run-sim")
    .then(res => res.text())
    .then(data => {
      console.log(data)
    })

}
```

---

# 19. Fetch API

GET request

```js
fetch("/api/data")
  .then(res => res.json())
  .then(data => console.log(data))
```

POST request

```js
fetch("/run", {

  method: "POST",

  headers: {
    "Content-Type": "application/json"
  },

  body: JSON.stringify({
    agents: 100
  })

})
```

---

# 20. Running the Server

Run normally

```
node server.js
```

Run with auto reload

```
npx nodemon server.js
```

---

# 21. Minimal Full Example

server.js

```js
const express = require("express")

const app = express()

app.use(express.json())
app.use(express.static("public"))

app.get("/api/hello", (req, res) => {
  res.json({ message: "hello" })
})

app.listen(3000, () => {
  console.log("Server running")
})
```

index.html

```html
<button onclick="test()">Test</button>

<script src="script.js"></script>
```

script.js

```js
function test() {

  fetch("/api/hello")
    .then(r => r.json())
    .then(data => console.log(data))

}
```

---

# 22. The 15 Commands You Actually Use

Most webapps use mainly:

```
npm init -y
npm install express
node server.js
npx nodemon server.js

app.get()
app.post()
res.send()
res.json()

app.use(express.json())
app.use(express.static())

fetch()

child_process.exec()
```

---

# Mental Model (IMPORTANT)

A webapp is **3 layers**

```
Frontend
HTML + JS
(buttons)

↓ HTTP

Backend
Node + Express
(routes)

↓ optional

Python simulation
Mesa / models
```
