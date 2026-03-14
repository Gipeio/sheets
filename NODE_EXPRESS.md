---

# Node.js + Express Cheat Sheet

## Table of Contents

1. [Node Philosophy](#node-philosophy)
2. [Project Setup](#project-setup)
3. [File Structure](#file-structure)
4. [Core Node Concepts](#core-node-concepts)
5. [Express Basics](#express-basics)
6. [Routes](#routes)
7. [Request / Response](#request--response)
8. [JSON APIs](#json-apis)
9. [Middleware](#middleware)
10. [Static Files](#static-files)
11. [Forms & POST Data](#forms--post-data)
12. [Query Parameters](#query-parameters)
13. [Environment Variables](#environment-variables)
14. [Calling Python Scripts](#calling-python-scripts)
15. [Async / Await](#async--await)
16. [Error Handling](#error-handling)
17. [Logging](#logging)
18. [Simple Frontend Interaction](#simple-frontend-interaction)
19. [Fetch API](#fetch-api)
20. [Running the Server](#running-the-server)
21. [Minimal Full Example](#minimal-full-example)
22. [The 15 Commands You Actually Use](#the-15-commands-you-actually-use)
23. [Mental Model](#mental-model)

---

# Node Philosophy

Node = JavaScript runtime for servers.

---

# Project Setup

```bash
mkdir webapp
cd webapp
npm init -y
npm install express
```

---

# File Structure

```text
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

---

# Core Node Concepts

```js
const express = require("express")
const app = express()

app.listen(3000)
```

---

# Express Basics

```js
app.get("/", (req, res) => {
  res.send("Hello world")
})
```

---

# Routes

```js
app.get("/hello", handler)
app.post("/data", handler)
```

---

# Request / Response

```js
req.params
req.query
req.body
```

```js
res.send()
res.json()
res.status()
```

---

# JSON APIs

```js
app.get("/api/data", (req, res) => {

  res.json({
    agents: 100,
    step: 42
  })

})
```

---

# Middleware

```js
app.use(express.json())
```

Example logger:

```js
app.use((req, res, next) => {
  console.log(req.method, req.url)
  next()
})
```

---

# Static Files

```js
app.use(express.static("public"))
```

---

# Forms & POST Data

```js
app.use(express.urlencoded({ extended: true }))
```

---

# Query Parameters

URL:

```
/simulation?agents=100
```

Server:

```js
req.query.agents
```

---

# Environment Variables

Install:

```bash
npm install dotenv
```

Use:

```js
require("dotenv").config()

process.env.PORT
```

---

# Calling Python Scripts

```js
const { exec } = require("child_process")

exec("python simulation.py", (err, stdout) => {
  console.log(stdout)
})
```

---

# Async / Await

```js
app.get("/data", async (req, res) => {

  const result = await fetchSomething()

  res.json(result)

})
```

---

# Error Handling

```js
try {

} catch (err) {

  res.status(500).send("error")

}
```

---

# Logging

```js
console.log("server started")
```

Better:

```bash
npm install morgan
```

---

# Simple Frontend Interaction

HTML:

```html
<button onclick="runSim()">Run</button>
```

JS:

```js
function runSim() {

  fetch("/run-sim")
    .then(res => res.text())
    .then(data => console.log(data))

}
```

---

# Fetch API

GET:

```js
fetch("/api/data")
  .then(res => res.json())
```

POST:

```js
fetch("/run", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ agents: 100 })
})
```

---

# Running the Server

```bash
node server.js
```

Hot reload:

```bash
npx nodemon server.js
```

---

# Minimal Full Example

server.js

```js
const express = require("express")

const app = express()

app.use(express.static("public"))

app.get("/api/hello", (req, res) => {
  res.json({ message: "hello" })
})

app.listen(3000)
```

---

# The 15 Commands You Actually Use

```text
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

# Mental Model

```text
Frontend (HTML + JS)
      ↓
HTTP request
      ↓
Node + Express
      ↓
Python simulation
```

---
