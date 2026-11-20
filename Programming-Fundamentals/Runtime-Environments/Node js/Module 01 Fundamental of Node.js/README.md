
Module 01 --- Node.js Fundamentals
Learn Deeply. Build Practically. Explain Clearly.

Welcome to Module 01 of the Node.js learning path. This module explains
how the web works, why Node.js exists, how its runtime works internally,
and how to use its core APIs confidently.

The goal is not to memorize Node.js methods. The goal is to understand
what happens behind the code you write, why a particular feature exists,
when to use it, and what trade-offs it introduces.
Learning approach: Start with the mental model, study the visual,
run the example, change the code, and then explain the concept in your
own words.

Table of Contents
- Learning Objectives
- Priority Guide
- Your Learning Workflow
- Environment Setup
- 1-1. How the Web Works from
  Scratch
- 1-2. Frontend vs Backend
  Essentials
- 1-3. Tracing Where Everything
  Began
- 1-4. How Node.js Changed Server-Side
  Development
- 1-5. Node.js Architecture: The Big
  Picture
- 1-6. V8 Engine and libuv
- 1-7. Event-Driven Architecture and
  EventEmitter
- 1-8. Single-Threaded Node.js vs Multithreaded
  Servers
- 1-9. How the Event Loop Works
- 1-10. Asynchronous I/O, Callbacks, Promises, and
  Async/Await
- 1-11. Streams, Buffers, and
  Backpressure
- 1-12. Node.js Modules: IIFE, CommonJS, and
  ESM
- 1-13. Built-in Modules: fs, path, os, and
  HTTP
- 1-14. Process, Environment Variables, and Runtime
  Configuration
- 1-15. Error Handling in Node.js
- 1-16. Worker Threads and Child
  Processes
- 1-17. Cluster, Profiling, and Memory
  Optimization
- Common Mistakes
- Module Review
- Interview Questions
- Practice Exercises
- Quick Revision Sheet
- Recommended Resources
Learning Objectives
By completing this module, you should be able to:
- Explain what happens when a user enters a URL and opens a website.
- Distinguish frontend, backend, server, runtime, and database.
- Explain what Node.js is and why it was created.
- Describe the roles of V8, libuv, Node.js core APIs, and the
  operating system.
- Explain event-driven architecture and non-blocking I/O.
- Understand what "single-threaded" means in Node.js---and what it
  does not mean.
- Explain the Event Loop and its major phases at a useful practical
  level.
- Choose between callbacks, Promises, and async/await.
- Use CommonJS and ECMAScript Modules (ESM).
- Understand the Node.js module wrapper and the relationship between
  exports and module.exports.
- Work with built-in modules such as fs, path, os, events,
  http, crypto, and stream.
- Understand Buffers, Streams, and backpressure.
- Use process information and environment variables safely.
- Handle synchronous errors, Promise rejections, callback errors, and
  EventEmitter errors.
- Know when to use Worker Threads, child processes, and cluster.
- Recognize common performance and memory problems and know how to
  investigate them.
Priority Guide
Use this priority system to decide how deeply to study each topic.
  Priority                Meaning                 Topics
  P0 --- Core         Understand deeply.      Architecture, V8,
These concepts appear   libuv, Event Loop,
regularly in real       asynchronous I/O,
backend work and        callbacks, Promises,
interviews.             async/await, modules,
EventEmitter, File
System, HTTP

  P1 --- Important    Understand well and     Streams, Buffers,
practise with small     process, environment
projects.               variables, error
handling, Worker
Threads, child
processes
P2 --- Advanced     Understand the use      Cluster, profiling,
cases and trade-offs.   memory optimization
Practise when building
systems that need them.
Important: Priority does not mean that P1 or P2 topics are
unimportant. It means you should first build a strong foundation in P0
topics.
Your Learning Workflow
For every topic, follow this sequence:
1. What: Define the concept in simple words.
2. Why: Understand the problem it solves.
3. How: Understand its internal working.
4. When: Identify when it is useful.
5. Example: Run and modify the code.
6. Real-world use: Connect it to an API, backend service, or
   production system.
7. Interview check: Explain it without looking at the notes.
Do not move forward just because you have read the section. Move forward
when you can explain the main idea and write a small example yourself.
Environment Setup
What do you need?
  Tool                        Purpose
  Node.js                     Runs JavaScript outside the browser
npm                         Installs and manages JavaScript packages
VS Code or another editor   Writes and edits code
Terminal                    Runs Node.js commands
Browser                     Tests HTTP endpoints and web applications

Install a supported Active LTS version of Node.js from the official
website. Avoid choosing an old version just because a tutorial uses it.
- Official website: https://nodejs.org/
- Check Node.js version: node --version
- Check npm version: npm --version
Create your first project
mkdir node-fundamentals
cd node-fundamentals
npm init -y
For the examples in this module, use ECMAScript Modules (ESM). Add this
field to the generated package.json:
{
  "type": "module"
}
Create index.js:
console.log("Hello from Node.js!");
Run it:
node index.js
Expected output:
Hello from Node.js!
Why use "type": "module"?

It tells Node.js to interpret .js files in this package as ES modules.
You can then use import and export. You can also use .mjs for ESM
or .cjs for CommonJS when you need to make the module type explicit.
1-1. How the Web Works from Scratch
Level: Beginner
Priority: P0
1. Learning Objectives
By the end of this lesson, you should be able to:
- Explain the journey from a browser URL to a server response.
- Define DNS, IP address, client, server, HTTP, and HTTPS.
- Describe the basic request-response cycle.
- Explain why a backend server is needed.
2. What happens when you open a website?
Imagine you type:
https://example.com/products
Your browser needs to find the server that hosts the website, connect to
it, request the page or data, and display the response.

A simplified journey looks like this:
