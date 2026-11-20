# Module 01 --- Node.js Fundamentals: Interview Questions & Answers

**A practical interview preparation guide for Node.js fundamentals**

This question bank follows the topics covered in **Module 01 --- Node.js
Fundamentals**. It is designed to help you explain concepts clearly,
reason about runtime behavior, answer follow-up questions, and solve
small coding problems.

> **How to use this guide:** First answer each question without looking.
> Then compare your answer with the explanation. For output-based
> questions, predict the output before running the code.

------------------------------------------------------------------------

## Table of Contents

1.  [How the Web Works](#1-how-the-web-works)
2.  [JavaScript, Node.js, and Its
    History](#2-javascript-nodejs-and-its-history)
3.  [Node.js Architecture, V8, and
    libuv](#3-nodejs-architecture-v8-and-libuv)
4.  [Event-Driven Architecture and
    EventEmitter](#4-event-driven-architecture-and-eventemitter)
5.  [Single-Threaded Model, Concurrency, and
    Parallelism](#5-single-threaded-model-concurrency-and-parallelism)
6.  [Event Loop](#6-event-loop)
7.  [Asynchronous I/O, Callbacks, Promises, and
    Async/Await](#7-asynchronous-io-callbacks-promises-and-asyncawait)
8.  [Modules: IIFE, CommonJS, and ESM](#8-modules-iife-commonjs-and-esm)
9.  [Built-in Modules: fs, path, os, and
    HTTP](#9-built-in-modules-fs-path-os-and-http)
10. [Buffers, Streams, and
    Backpressure](#10-buffers-streams-and-backpressure)
11. [Process and Environment
    Variables](#11-process-and-environment-variables)
12. [Error Handling](#12-error-handling)
13. [Worker Threads, Child Processes, and
    Cluster](#13-worker-threads-child-processes-and-cluster)
14. [Profiling, Performance, and
    Memory](#14-profiling-performance-and-memory)
15. [Output-Based Questions](#15-output-based-questions)
16. [Scenario-Based Questions](#16-scenario-based-questions)
17. [Coding Interview Exercises with
    Solutions](#17-coding-interview-exercises-with-solutions)
18. [Rapid-Fire Revision](#18-rapid-fire-revision)
19. [Final Interview Checklist](#19-final-interview-checklist)

------------------------------------------------------------------------

# 1. How the Web Works

### Q1. What happens when you enter a URL in a browser?

**Answer:**

1.  The browser parses the URL and identifies the protocol, domain, and
    path.
2.  DNS resolution finds the IP address associated with the domain, if
    it is not already available from cache.
3.  The browser establishes a connection to the server.
4.  For HTTPS, TLS negotiation establishes a protected connection.
5.  The browser sends an HTTP request.
6.  The server processes the request and may communicate with a database
    or another service.
7.  The server returns an HTTP response.
8.  The browser processes the response and renders the page or displays
    the returned data.

The exact sequence can vary because browsers use caches, connection
reuse, HTTP/2, HTTP/3, and other optimizations.

### Q2. What is the difference between a client and a server?

**Answer:**

A client requests a service, while a server receives requests and
provides responses.

For example, a React application in a browser can act as a client, and a
Node.js API can act as a server.

### Q3. What is DNS?

**Answer:**

DNS stands for Domain Name System. It is a distributed naming system
that helps resolve domain names, such as `example.com`, into IP
addresses and other DNS records.

DNS responses can be cached, so a new lookup is not necessarily required
for every request.

### Q4. What is the difference between HTTP and HTTPS?

**Answer:**

HTTP is a protocol for communication between clients and servers. HTTPS
is HTTP protected by TLS.

HTTPS provides encryption, integrity, and server authentication, helping
protect information while it travels over the network.

### Q5. What is an HTTP request and an HTTP response?

**Answer:**

An HTTP request is a message sent by a client to a server. It commonly
contains a method, URL, headers, and sometimes a body.

An HTTP response is the server's reply. It contains a status code,
headers, and usually a response body.

### Q6. What is the difference between GET and POST?

**Answer:**

-   `GET` is commonly used to retrieve a resource.
-   `POST` is commonly used to submit data or ask the server to
    create/process a resource.

The intended semantics matter more than the fact that both can
technically carry data in certain situations.

### Q7. What is an API?

**Answer:**

An API is a defined interface through which software components
communicate. A web API commonly exposes endpoints that clients call
using HTTP.

------------------------------------------------------------------------

# 2. JavaScript, Node.js, and Its History

### Q8. What is Node.js?

**Answer:**

Node.js is an open-source, cross-platform JavaScript runtime
environment. It allows JavaScript to run outside a web browser and
provides APIs for tasks such as file-system access, networking, streams,
and process management.

### Q9. Is Node.js a programming language?

**Answer:**

No. JavaScript is the programming language. Node.js is the runtime
environment that executes JavaScript and provides server-side APIs.

### Q10. What is the difference between JavaScript, a JavaScript engine, and a runtime?

**Answer:**

-   **JavaScript:** The programming language.
-   **JavaScript engine:** Software that parses and executes JavaScript.
-   **Runtime:** An environment that combines an engine with APIs and
    other facilities needed to run applications.

For example, V8 is an engine, while Node.js is a runtime that uses V8.

### Q11. What is V8?

**Answer:**

V8 is Google's open-source JavaScript and WebAssembly engine. Node.js
uses V8 to execute JavaScript.

V8 handles JavaScript parsing, execution, optimization, and JavaScript
heap management.

### Q12. Who created Node.js and when was it introduced?

**Answer:**

Ryan Dahl introduced Node.js in 2009. It used Google's V8 engine to make
it practical to run JavaScript outside the browser.

### Q13. Why was Node.js created?

**Answer:**

Node.js made server-side JavaScript practical with an event-driven,
non-blocking I/O model. This was particularly useful for applications
that handle many network connections and spend significant time waiting
for I/O operations.

### Q14. What is npm?

**Answer:**

npm is the package manager commonly used in the Node.js ecosystem. It
helps developers install, update, and manage third-party packages and
project dependencies.

### Q15. Can Node.js be used only for backend development?

**Answer:**

No. Node.js is commonly used for backend APIs, command-line tools, build
tools, automation, server-side rendering, real-time applications, and
development tooling.

------------------------------------------------------------------------

# 3. Node.js Architecture, V8, and libuv

### Q16. Explain Node.js architecture.

**Answer:**

A simplified Node.js architecture contains:

-   **Application JavaScript:** The code written by the developer.
-   **Node.js core APIs:** Features such as `fs`, `http`, `events`, and
    `stream`.
-   **V8:** Executes JavaScript.
-   **Node.js native bindings:** Connect JavaScript-facing APIs to
    lower-level implementation.
-   **libuv:** Provides the Event Loop and cross-platform asynchronous
    I/O support.
-   **Operating system:** Provides networking, file-system, and process
    facilities.

### Q17. What is the role of V8 in Node.js?

**Answer:**

V8 executes JavaScript. It parses source code, creates internal
representations, executes and optimizes code, and manages the JavaScript
heap through garbage collection.

V8 does not itself provide Node.js's `fs` or `http` APIs.

### Q18. What is libuv?

**Answer:**

libuv is a cross-platform library used by Node.js. It provides the Event
Loop, asynchronous I/O support, and a worker pool used by selected
operations.

### Q19. What is the difference between V8 and libuv?

**Answer:**

  -----------------------------------------------------------------------
  V8                                  libuv
  ----------------------------------- -----------------------------------
  Executes JavaScript                 Coordinates the Event Loop and
                                      asynchronous I/O

  Manages the JavaScript heap         Provides a worker pool for selected
                                      operations

  Handles JavaScript execution and    Helps Node.js interact with
  optimization                        operating-system facilities
  -----------------------------------------------------------------------

### Q20. Does every asynchronous Node.js operation use the libuv worker pool?

**Answer:**

No. Some operations use operating-system asynchronous I/O facilities
directly. Selected operations, such as many file-system operations,
`dns.lookup()`, and certain crypto or compression operations, use the
libuv worker pool.

Do not assume that every network request is executed by a worker-pool
thread.

### Q21. What is the libuv thread pool?

**Answer:**

It is a pool of background threads used by libuv for selected operations
that should not block the main JavaScript thread.

The pool has a configurable size. Its default size is commonly four
threads. It can be configured using `UV_THREADPOOL_SIZE`, subject to
Node.js and libuv constraints.

### Q22. What happens when Node.js reads a file asynchronously?

**Answer:**

At a high level:

1.  JavaScript calls an asynchronous file-system API.
2.  Node.js starts the file operation.
3.  The operation is handled using the runtime's file-system facilities
    and libuv's worker pool.
4.  JavaScript can continue with other work while the file operation is
    in progress.
5.  When the operation completes, the Promise or callback is made ready.
6.  The Event Loop coordinates execution of the callback or Promise
    continuation.

The exact implementation path depends on the API and platform.

### Q23. What is the difference between a JavaScript engine and a runtime API?

**Answer:**

The engine executes the language. Runtime APIs provide capabilities
outside the language itself.

For example, JavaScript syntax does not define a built-in file-system
API. Node.js provides `node:fs` for file operations.

------------------------------------------------------------------------

# 4. Event-Driven Architecture and EventEmitter

### Q24. What is event-driven architecture?

**Answer:**

Event-driven architecture is a design approach in which one component
emits or publishes an event and other components react to it.

For example, after an order is created, separate components may react by
sending a confirmation email, updating inventory, and recording
analytics.

### Q25. What is an event?

**Answer:**

An event is a signal that something has happened, such as
`user.registered`, `order.created`, or `payment.completed`.

### Q26. What is EventEmitter in Node.js?

**Answer:**

`EventEmitter` is a class from the `node:events` module. It allows an
object to emit named events and register functions that listen for those
events.

### Q27. What is the difference between `on()` and `once()`?

**Answer:**

-   `on()` registers a listener that can run every time the event is
    emitted.
-   `once()` registers a listener that runs at most one time and is then
    removed.

### Q28. What does `emit()` do?

**Answer:**

`emit()` triggers a named event and calls its registered listeners.

### Q29. Are EventEmitter listeners asynchronous by default?

**Answer:**

No. EventEmitter listeners are called synchronously in the order they
were registered.

A listener can start asynchronous work, but EventEmitter does not
automatically move the listener to another thread.

### Q30. What happens when an EventEmitter emits an `error` event without an error listener?

**Answer:**

If an EventEmitter emits `'error'` and no listener is registered for it,
Node.js throws the error. If it is not handled, the process can
terminate.

### Q31. Is EventEmitter a message queue?

**Answer:**

No. EventEmitter is an in-process event mechanism. It does not provide
durable storage, cross-process delivery, or guaranteed delivery after a
process restarts.

For distributed messaging, use an appropriate message broker or durable
messaging system.

------------------------------------------------------------------------

# 5. Single-Threaded Model, Concurrency, and Parallelism

### Q32. Is Node.js single-threaded?

**Answer:**

Node.js application JavaScript normally runs on one main JavaScript
thread by default. However, the Node.js runtime also uses other threads
internally and supports Worker Threads.

So saying "Node.js is completely single-threaded" is inaccurate.

### Q33. If Node.js is single-threaded, how can it handle many requests?

**Answer:**

Node.js uses non-blocking I/O and an Event Loop. It can start I/O
operations, continue handling other ready work, and execute callbacks
when operations complete.

It does not need one JavaScript thread for every incoming request.

### Q34. What is concurrency?

**Answer:**

Concurrency means multiple tasks make progress during overlapping
periods. They do not necessarily execute at exactly the same time.

### Q35. What is parallelism?

**Answer:**

Parallelism means multiple tasks execute simultaneously, usually on
different CPU cores or execution units.

### Q36. What is the difference between concurrency and parallelism?

**Answer:**

Concurrency is about managing multiple tasks whose progress overlaps.
Parallelism is about executing multiple tasks at the same time.

Node.js can handle many concurrent I/O operations without running all
their JavaScript callbacks in parallel.

### Q37. What happens if CPU-intensive code runs on the main JavaScript thread?

**Answer:**

It blocks that thread. While the synchronous CPU-heavy code is running,
the Event Loop cannot execute other JavaScript callbacks on that thread.
This can delay requests, timers, and I/O callbacks.

### Q38. Is Node.js always faster than a multithreaded server?

**Answer:**

No. Performance depends on the workload, application architecture,
implementation, hardware, and bottlenecks. Node.js is particularly
suitable for many I/O-heavy workloads, but it is not automatically
faster for every task.

------------------------------------------------------------------------

# 6. Event Loop

### Q39. What is the Event Loop?

**Answer:**

The Event Loop is the mechanism that coordinates asynchronous operations
and executes callbacks when they are ready. It allows Node.js to handle
non-blocking I/O without waiting synchronously for every operation.

### Q40. What are the main Event Loop phases?

**Answer:**

The main phases are:

1.  Timers.
2.  Pending callbacks.
3.  Idle and prepare.
4.  Poll.
5.  Check.
6.  Close callbacks.

The phases are part of libuv's loop. The exact callback scheduling
behavior also depends on Node.js queues and runtime details.

### Q41. What happens in the timers phase?

**Answer:**

Eligible callbacks scheduled by `setTimeout()` and `setInterval()` are
executed.

A timer delay is a minimum threshold, not a guarantee that the callback
runs at an exact time.

### Q42. What happens in the poll phase?

**Answer:**

The poll phase retrieves and processes many I/O-related events. It can
also wait for I/O when there is no immediate work to process.

### Q43. What happens in the check phase?

**Answer:**

Callbacks scheduled using `setImmediate()` are executed in the check
phase.

### Q44. What is `setImmediate()`?

**Answer:**

`setImmediate()` schedules a callback to run in the check phase, after
the poll phase.

### Q45. What is `setTimeout()`?

**Answer:**

`setTimeout()` schedules a callback to become eligible after a specified
minimum delay. The callback runs when the Event Loop can process it.

### Q46. What is the difference between `setTimeout()` and `setImmediate()`?

**Answer:**

`setTimeout()` is associated with the timers phase, while
`setImmediate()` is associated with the check phase.

Their order is not universally fixed. When scheduled from the main
module, the order between a zero-delay timer and `setImmediate()` can
vary. Inside an I/O callback, `setImmediate()` generally runs before a
zero-delay timer scheduled in that context.

### Q47. What is `process.nextTick()`?

**Answer:**

`process.nextTick()` schedules a callback to run after the current
JavaScript operation completes and before the Event Loop continues to
another phase.

It is not an Event Loop phase.

### Q48. What is the Promise microtask queue?

**Answer:**

Promise handlers such as `.then()`, `.catch()`, and `.finally()`, along
with `queueMicrotask()` callbacks, are processed as microtasks.

Node.js also has a separate next-tick queue. In typical Node.js
execution, next-tick callbacks are processed before the Promise
microtask queue at the relevant checkpoint.

### Q49. Can `setTimeout(fn, 0)` run immediately?

**Answer:**

No. It becomes eligible after the timer threshold, and its callback runs
when the Event Loop reaches a point where it can process the callback.

### Q50. Can the Event Loop be blocked?

**Answer:**

Yes. Long-running synchronous JavaScript, large CPU-heavy loops, and
synchronous APIs in request-handling paths can block the main JavaScript
thread.

### Q51. What changed about timers in Node.js 20?

**Answer:**

Node.js 20 uses libuv 1.45.0 or later. Starting with libuv 1.45.0,
timers run after the poll phase in each loop iteration rather than both
before and after poll as in earlier behavior. This can affect some timer
and `setImmediate()` ordering examples.

------------------------------------------------------------------------

# 7. Asynchronous I/O, Callbacks, Promises, and Async/Await

### Q52. What is I/O?

**Answer:**

I/O means Input/Output. It includes communicating with files, networks,
databases, and other external systems.

### Q53. What is blocking I/O?

**Answer:**

Blocking I/O makes the current execution wait until the operation
completes before continuing.

### Q54. What is non-blocking I/O?

**Answer:**

Non-blocking I/O allows an operation to start while the application
continues other work. The result is handled later through a callback,
Promise, or another completion mechanism.

### Q55. What is a callback?

**Answer:**

A callback is a function passed to another function so it can be invoked
later, often after an operation completes or an event occurs.

### Q56. What is an error-first callback?

**Answer:**

It is a common Node.js callback convention where the first argument
represents an error and the following arguments contain the successful
result.

Example:

``` js
readFile("notes.txt", "utf8", (error, data) => {
  if (error) {
    console.error(error);
    return;
  }

  console.log(data);
});
```

### Q57. What is callback hell?

**Answer:**

Callback hell refers to deeply nested callbacks that make asynchronous
code difficult to read, maintain, and handle errors in.

Promises and `async/await` can make many asynchronous flows easier to
structure.

### Q58. What is a Promise?

**Answer:**

A Promise represents the eventual completion or failure of an
asynchronous operation.

A Promise has three states:

-   Pending.
-   Fulfilled.
-   Rejected.

### Q59. What is the difference between `then()`, `catch()`, and `finally()`?

**Answer:**

-   `then()` handles fulfillment and can also receive a rejection
    handler.
-   `catch()` handles rejection.
-   `finally()` runs after the Promise settles, whether fulfilled or
    rejected. It is commonly used for cleanup.

### Q60. What does `async` do?

**Answer:**

An `async` function always returns a Promise. If it returns a normal
value, that value becomes the fulfillment value of the returned Promise.
If it throws, the returned Promise rejects.

### Q61. What does `await` do?

**Answer:**

`await` waits for a Promise or thenable to settle inside an async
function or another supported await context. It pauses that function's
continuation, not the entire Node.js process.

### Q62. Does async/await create a new thread?

**Answer:**

No. Async/await is syntax for working with Promises. It does not
automatically create a new thread or move CPU-heavy JavaScript to the
background.

### Q63. What is the difference between sequential and concurrent asynchronous operations?

**Answer:**

Sequential operations wait for one operation before starting the next.
Concurrent operations are started without waiting for one another, when
they are independent.

Sequential:

``` js
const user = await getUser();
const orders = await getOrders();
```

Concurrent:

``` js
const [user, orders] = await Promise.all([
  getUser(),
  getOrders()
]);
```

### Q64. What does `Promise.all()` do?

**Answer:**

It returns a Promise that fulfills when all input Promises fulfill. It
rejects when one of the input Promises rejects.

It is useful for independent operations that can run concurrently.

### Q65. What is the difference between `Promise.all()` and `Promise.allSettled()`?

**Answer:**

-   `Promise.all()` rejects if an input Promise rejects.
-   `Promise.allSettled()` waits for every input Promise to settle and
    returns the outcome of each one.

### Q66. When should you use synchronous file-system APIs?

**Answer:**

They may be acceptable in small scripts, startup tasks, or situations
where blocking is intentional. They should generally be avoided in
high-traffic request paths because they block the main JavaScript
thread.

------------------------------------------------------------------------

# 8. Modules: IIFE, CommonJS, and ESM

### Q67. What is a module?

**Answer:**

A module is a reusable unit of code that can expose selected
functionality to other parts of an application.

### Q68. What is IIFE?

**Answer:**

IIFE stands for Immediately Invoked Function Expression. It is a
function expression that is executed immediately after it is defined.

### Q69. Why were IIFEs used?

**Answer:**

IIFEs were commonly used to create private scope and avoid polluting the
global namespace before modern JavaScript module systems were widely
available.

Modern ESM modules already have module scope, so an IIFE is not normally
needed just to hide variables in a module.

### Q70. What is CommonJS?

**Answer:**

CommonJS is a module system traditionally used by Node.js. It uses
`require()` to load modules and `module.exports` or `exports` to expose
values.

### Q71. What is ESM?

**Answer:**

ESM stands for ECMAScript Modules. It is the standard JavaScript module
system and uses `import` and `export`.

### Q72. What is the difference between CommonJS and ESM?

**Answer:**

  -----------------------------------------------------------------------
  CommonJS                            ESM
  ----------------------------------- -----------------------------------
  `require()`                         `import`

  `module.exports`                    `export`

  Traditional Node.js module system   Standard JavaScript module system

  `.cjs` is CommonJS                  `.mjs` is ESM
  -----------------------------------------------------------------------

For `.js` files, package configuration and Node.js module-detection
rules determine how the file is interpreted.

### Q73. What is the CommonJS module wrapper?

**Answer:**

Node.js conceptually wraps each CommonJS module in a function that
provides module-scoped variables such as `exports`, `require`, `module`,
`__filename`, and `__dirname`.

### Q74. What is the difference between `exports` and `module.exports`?

**Answer:**

Initially, `exports` references the same object as `module.exports`.

This works:

``` js
exports.add = (a, b) => a + b;
```

This does not replace the exported value:

``` js
exports = {
  add: (a, b) => a + b
};
```

To replace the exported value, assign to `module.exports`.

### Q75. What is the difference between named and default exports?

**Answer:**

Named exports expose values under specific exported names. They are
imported using matching names, although they can be locally renamed.

A default export is the module's primary exported value and can be
imported using any local name.

### Q76. What does `"type": "module"` do in package.json?

**Answer:**

It tells Node.js to interpret `.js` files in that package scope as
ECMAScript Modules.

Use `.mjs` for explicit ESM and `.cjs` for explicit CommonJS.

### Q77. Does ESM provide `__dirname` automatically?

**Answer:**

No. In ESM, use `import.meta.url` and convert it with `fileURLToPath()`
from `node:url`. Then use `path.dirname()` to obtain the directory path.

------------------------------------------------------------------------

# 9. Built-in Modules: fs, path, os, and HTTP

### Q78. What are Node.js built-in modules?

**Answer:**

Built-in modules are modules included with Node.js. They provide
functionality without requiring a separate npm installation.

Examples include `node:fs`, `node:path`, `node:http`, `node:events`,
`node:stream`, `node:crypto`, and `node:os`.

### Q79. What is the purpose of the `fs` module?

**Answer:**

The File System module provides APIs to read, write, update, rename,
delete, and inspect files and directories.

### Q80. What is the difference between `readFile()` and `createReadStream()`?

**Answer:**

-   `readFile()` reads the entire file into memory before returning the
    result.
-   `createReadStream()` reads data in chunks.

Streams are often more appropriate for large files because they avoid
loading the entire file into memory at once.

### Q81. What is the purpose of the `path` module?

**Answer:**

It provides cross-platform utilities for constructing and inspecting
file-system paths.

### Q82. What is the difference between `path.join()` and `path.resolve()`?

**Answer:**

-   `path.join()` combines path segments using the platform's path
    separator.
-   `path.resolve()` resolves path segments into an absolute path, using
    the current working directory when needed.

Neither method alone validates a user-supplied path for security.

### Q83. What is the purpose of the `os` module?

**Answer:**

It provides operating-system information, such as platform,
architecture, CPU information, memory, and home directory.

### Q84. What is the purpose of the `http` module?

**Answer:**

The `node:http` module allows Node.js to create HTTP servers and
clients.

### Q85. How do you create a basic HTTP server in Node.js?

**Answer:**

``` js
import { createServer } from "node:http";

const server = createServer((req, res) => {
  res.writeHead(200, {
    "Content-Type": "application/json"
  });

  res.end(JSON.stringify({
    message: "Hello from Node.js"
  }));
});

server.listen(3000);
```

`createServer()` creates the server, and `listen()` starts accepting
connections on the specified port.

### Q86. What is the difference between raw Node.js HTTP and Express?

**Answer:**

Raw Node.js uses the built-in `node:http` module directly. You handle
routing, request parsing, and many details yourself.

Express builds on Node.js HTTP capabilities and provides convenient
routing, middleware, and other abstractions.

Understanding raw HTTP helps you understand what a framework simplifies.

------------------------------------------------------------------------

# 10. Buffers, Streams, and Backpressure

### Q87. What is a Buffer?

**Answer:**

A Buffer is a fixed-length sequence of bytes. It is used to handle
binary data such as images, files, and network data.

### Q88. What is a Stream?

**Answer:**

A Stream is an abstraction for processing data incrementally over time
instead of requiring the entire data source to be loaded into memory at
once.

### Q89. What are the four main types of streams?

**Answer:**

1.  Readable --- provides data.
2.  Writable --- receives data.
3.  Duplex --- can read and write.
4.  Transform --- reads data, transforms it, and outputs the result.

### Q90. What is the difference between a Buffer and a Stream?

**Answer:**

A Buffer represents bytes held in memory. A Stream provides a way to
process data incrementally.

A stream may deliver data through Buffers or strings, depending on its
mode and configuration.

### Q91. What is backpressure?

**Answer:**

Backpressure is a flow-control mechanism used when a producer generates
data faster than a consumer can process it.

The producer should slow down or pause to prevent excessive buffering
and memory usage.

### Q92. What does `write()` returning `false` mean for a writable stream?

**Answer:**

It means the writable stream's internal buffer has reached its
threshold. The producer should stop writing and wait for the `'drain'`
event before continuing.

### Q93. What does `pipe()` do?

**Answer:**

`pipe()` connects a readable stream to a writable stream and manages
data flow, including backpressure.

For robust pipelines, Node.js's `pipeline()` utility is often preferable
because it provides coordinated error handling and cleanup.

### Q94. Why are streams useful for large files?

**Answer:**

Streams process data in chunks, reducing the need to keep the entire
file in memory. They are useful for uploads, downloads, file copying,
compression, and data transformation.

------------------------------------------------------------------------

# 11. Process and Environment Variables

### Q95. What is a process?

**Answer:**

A process is a running instance of a program. When you run
`node server.js`, the operating system starts a Node.js process to
execute it.

### Q96. What is the `process` object?

**Answer:**

The `process` object provides information and control related to the
current Node.js process.

Examples include `process.pid`, `process.version`, `process.cwd()`,
`process.argv`, `process.env`, and `process.memoryUsage()`.

### Q97. What are environment variables?

**Answer:**

Environment variables are configuration values provided to a running
process.

Examples include `PORT`, `NODE_ENV`, `DATABASE_URL`, and `REDIS_URL`.

### Q98. Why should secrets not be hardcoded in source code?

**Answer:**

Hardcoded secrets can accidentally be committed to version control or
exposed through logs and code sharing. Sensitive configuration should be
provided through environment configuration or a secret manager.

### Q99. Are environment variable values strings?

**Answer:**

Yes. Environment variable values are strings, so applications should
validate and convert them before using them as numbers, booleans, or
other types.

### Q100. What is graceful shutdown?

**Answer:**

Graceful shutdown means stopping new work and closing active resources
cleanly before the process exits.

An HTTP server may stop accepting new connections, finish active
requests, close database connections, and flush logs.

### Q101. What is the difference between `process.exit()` and `process.exitCode`?

**Answer:**

`process.exit()` forces the process to terminate immediately, which can
interrupt pending asynchronous work or output.

`process.exitCode` sets the exit status that Node.js will use when the
event loop has no more work. It is generally preferable when a clean
shutdown is possible.

------------------------------------------------------------------------

# 12. Error Handling

### Q102. How do you handle synchronous errors in Node.js?

**Answer:**

Use `try/catch` around code that may throw synchronously.

``` js
try {
  const data = JSON.parse("{ invalid }");
} catch (error) {
  console.error(error.message);
}
```

### Q103. How do you handle Promise rejections?

**Answer:**

Use `.catch()` or `try/catch` with `await`.

``` js
try {
  const user = await getUser();
} catch (error) {
  console.error(error);
}
```

### Q104. Does `try/catch` catch an error thrown later inside an ordinary callback?

**Answer:**

Not automatically. A `try/catch` only catches errors thrown during the
execution of its `try` block. An error thrown later in a callback
executes in a different call stack.

Use the callback API's error argument or handle errors inside the
callback.

### Q105. What is an unhandled Promise rejection?

**Answer:**

It occurs when a Promise rejects and the application does not attach an
appropriate rejection handler. Unhandled rejections should be prevented
through deliberate error handling.

### Q106. What is `uncaughtException`?

**Answer:**

It is a process-level event emitted when an exception escapes JavaScript
execution without being caught.

It is a last-resort mechanism, not a replacement for normal error
handling. After an uncaught exception, the application may be in an
unknown state and should generally perform cleanup and shut down.

### Q107. Why should stack traces not be exposed to public API clients?

**Answer:**

Stack traces can reveal internal file paths, implementation details,
dependencies, and other information useful to attackers. Log detailed
errors internally and return safe, appropriate error responses to
clients.

### Q108. What is centralized error handling?

**Answer:**

It is a design in which errors are passed to a common part of the
application that logs them and converts them into consistent responses.
Web frameworks such as Express and NestJS provide ways to implement
centralized error handling.

------------------------------------------------------------------------

# 13. Worker Threads, Child Processes, and Cluster

### Q109. What are Worker Threads?

**Answer:**

Worker Threads allow JavaScript to execute in separate threads within
the same Node.js process. They are useful for CPU-intensive JavaScript
tasks that should not block the main Event Loop.

### Q110. When should you use Worker Threads?

**Answer:**

Use them for CPU-heavy tasks such as computational work, data
transformation, and expensive parsing when the work can be separated
from the main request-handling thread.

### Q111. What is a child process?

**Answer:**

A child process is a separate operating-system process started by the
current process. It has its own process identity and memory space.

### Q112. When should you use child processes?

**Answer:**

Use child processes when you need to run external commands, start
another program, run another Node.js script, or isolate work in a
separate process.

### Q113. What is the difference between Worker Threads and child processes?

**Answer:**

  -----------------------------------------------------------------------
  Worker Threads                      Child Processes
  ----------------------------------- -----------------------------------
  Separate JavaScript threads in one  Separate OS processes
  process                             

  Can share memory using suitable     Separate memory spaces; communicate
  shared-memory APIs                  through IPC or other channels

  Useful for CPU-heavy JavaScript     Useful for running programs and
                                      process isolation

  Lower process-level isolation       Stronger process-level isolation
  -----------------------------------------------------------------------

### Q114. What is the difference between `spawn()`, `exec()`, and `fork()`?

**Answer:**

-   `spawn()` starts a process and exposes its standard streams.
-   `exec()` runs a command through a shell and buffers output.
-   `fork()` starts another Node.js process with an IPC communication
    channel.

Use care with shell commands. Never pass untrusted input into a shell
command without safe handling.

### Q115. What is the Cluster module?

**Answer:**

The Cluster module allows multiple Node.js worker processes to share a
server port. It can help a server use multiple CPU cores for incoming
connections.

### Q116. What is the difference between Cluster and Worker Threads?

**Answer:**

Cluster uses multiple processes, each with its own memory and V8
instance. Worker Threads use multiple JavaScript threads within one
process.

### Q117. Should you create a Worker Thread for every request?

**Answer:**

No. Creating workers has overhead. For repeated CPU-heavy tasks, a
worker pool is often more efficient than creating a new worker for every
small task.

------------------------------------------------------------------------

# 14. Profiling, Performance, and Memory

### Q118. What is profiling?

**Answer:**

Profiling means measuring an application's runtime behavior to find
performance bottlenecks. It can measure CPU usage, execution time,
memory, and Event Loop delay.

### Q119. How would you investigate a slow Node.js API?

**Answer:**

1.  Measure request latency and identify the slow endpoint.
2.  Break down time spent in database queries and external services.
3.  Check CPU usage and CPU profiles.
4.  Measure Event Loop delay.
5.  Inspect synchronous work in request handlers.
6.  Review memory usage and garbage collection behavior.
7.  Optimize the actual bottleneck rather than guessing.

### Q120. What is a memory leak?

**Answer:**

A memory leak occurs when objects remain referenced and consume memory
even though the application no longer needs them.

### Q121. What commonly causes memory leaks in Node.js?

**Answer:**

Common causes include:

-   Unbounded caches.
-   Growing global arrays.
-   Event listeners that are never removed.
-   Timers that are never cleared.
-   Closures retaining large objects.
-   Resources that are not closed.

### Q122. Does garbage collection prevent every memory leak?

**Answer:**

No. Garbage collection can reclaim unreachable objects, but it cannot
reclaim objects that remain reachable through application references.

### Q123. What does `process.memoryUsage()` return?

**Answer:**

It returns memory metrics such as:

-   `rss`: Resident memory used by the process.
-   `heapTotal`: Total V8 heap allocated.
-   `heapUsed`: V8 heap currently used.
-   `external`: Native memory associated with JavaScript objects.
-   `arrayBuffers`: Memory used by ArrayBuffers and related buffers.

### Q124. What is the difference between `heapUsed` and `rss`?

**Answer:**

`heapUsed` describes the portion of the V8 heap currently used by
JavaScript objects. `rss` describes the total resident memory used by
the process, including more than just the JavaScript heap.

### Q125. What is a heap snapshot?

**Answer:**

A heap snapshot captures information about objects in the V8 heap.
Developers can compare snapshots to identify objects that remain
retained and investigate possible memory leaks.

### Q126. Why should you measure before optimizing?

**Answer:**

Because performance problems are not always where developers expect them
to be. Measurement helps identify the actual bottleneck and prevents
unnecessary or harmful optimization.

------------------------------------------------------------------------

# 15. Output-Based Questions

**Instructions:** Predict the output before reading the answer. These
questions test your understanding of JavaScript execution and Node.js
scheduling.

## Q127. Synchronous execution

``` js
console.log("A");
console.log("B");
console.log("C");
```

**Answer:**

``` text
A
B
C
```

**Why?** Synchronous statements run in program order.

## Q128. Promise microtask

``` js
console.log("Start");

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

**Answer:**

``` text
Start
End
Promise
```

**Why?** The Promise handler runs as a microtask after the current
synchronous JavaScript completes.

## Q129. `process.nextTick()` and Promise

``` js
console.log("Start");

process.nextTick(() => console.log("NextTick"));

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

**Answer in a typical CommonJS execution:**

``` text
Start
End
NextTick
Promise
```

**Why?** Synchronous code runs first. At the relevant checkpoint,
Node.js processes the next-tick queue before the Promise microtask
queue.

Be careful when reasoning about nested scheduling and ESM top-level
execution contexts.

## Q130. `setTimeout()` and `setImmediate()`

``` js
setTimeout(() => console.log("Timeout"), 0);

setImmediate(() => console.log("Immediate"));
```

**Answer:**

There is no universal fixed order when this is scheduled from the main
module. The result can depend on timing and context.

**Interview point:** Do not claim that one always runs before the other.

## Q131. EventEmitter execution order

``` js
import { EventEmitter } from "node:events";

const emitter = new EventEmitter();

emitter.on("hello", () => console.log("Listener"));

console.log("Before");
emitter.emit("hello");
console.log("After");
```

**Answer:**

``` text
Before
Listener
After
```

**Why?** EventEmitter listeners run synchronously by default.

## Q132. Async function return value

``` js
async function getValue() {
  return 10;
}

console.log(getValue());
```

**Answer:**

It prints a Promise object, not the plain number `10`.

**Why?** An async function always returns a Promise.

## Q133. Await continuation

``` js
async function run() {
  console.log("A");
  await Promise.resolve();
  console.log("B");
}

console.log("Start");
run();
console.log("End");
```

**Answer:**

``` text
Start
A
End
B
```

**Why?** The function runs synchronously until it reaches `await`. Its
continuation is scheduled after the Promise settles.

## Q134. Synchronous blocking

``` js
console.log("Start");

const end = Date.now() + 1000;
while (Date.now() < end) {}

setTimeout(() => console.log("Timer"), 0);

console.log("End");
```

**Answer:**

``` text
Start
End
Timer
```

**Why?** The synchronous loop blocks the main JavaScript thread. The
timer callback cannot execute until the current synchronous code
finishes.

## Q135. `Promise.all()`

``` js
const a = Promise.resolve("A");
const b = Promise.resolve("B");

Promise.all([a, b]).then((values) => {
  console.log(values);
});
```

**Answer:**

``` text
["A", "B"]
```

The result order follows the input order, not necessarily the order in
which the Promises complete.

------------------------------------------------------------------------

# 16. Scenario-Based Questions

### Q136. Your Node.js API becomes slow whenever a large calculation runs. What is happening?

**Answer:**

The calculation may be running synchronously on the main JavaScript
thread and blocking the Event Loop.

**Possible solution:** Move CPU-heavy work to Worker Threads, a worker
pool, or a separate processing service.

### Q137. Your application reads a 5 GB file using `readFile()`. What is the concern?

**Answer:**

`readFile()` loads the entire file into memory. This can create high
memory usage or cause the process to run out of memory.

**Possible solution:** Use a readable stream and process the file in
chunks.

### Q138. A file upload is faster than the destination storage can write. What problem can occur?

**Answer:**

The producer may overwhelm the consumer, causing internal buffers to
grow and memory usage to increase.

**Possible solution:** Respect stream backpressure and pause production
when a writable stream signals that its buffer is full.

### Q139. Your process memory keeps increasing over several hours. What would you investigate?

**Answer:**

-   Unbounded caches and collections.
-   Event listeners that accumulate.
-   Timers that are not cleared.
-   Large objects retained by closures.
-   Resources that are not closed.
-   Heap snapshots and memory trends.

Do not assume every increase is a memory leak; inspect the actual
retained objects and memory metrics.

### Q140. A database query takes two seconds. Does it block the Event Loop for two seconds?

**Answer:**

Not necessarily. If the database driver performs the query
asynchronously, the main JavaScript thread can handle other ready work
while waiting for the database response.

However, synchronous processing before or after the query can still
block the Event Loop.

### Q141. You need to send an email after an order is created. Should the HTTP request wait for the email to finish?

**Answer:**

It depends on the business requirement. If email delivery is not
required to complete the order response, a background job or queue can
decouple email delivery from the request.

For important work, use a durable queue or reliable event mechanism
rather than relying only on an in-memory EventEmitter.

### Q142. You need to run a CPU-heavy JavaScript calculation. Should you use `setTimeout()`?

**Answer:**

No. `setTimeout()` schedules a callback; it does not move CPU-heavy
JavaScript to another thread.

Use Worker Threads or a separate processing service.

### Q143. You need to run a shell command from Node.js. Which API would you consider?

**Answer:**

Use `spawn()` or `execFile()` when you need to run an executable with
arguments. Use `exec()` when shell behavior is specifically needed and
inputs are safely controlled.

Avoid passing untrusted input into shell commands.

### Q144. Your app receives SIGTERM during deployment. What should it do?

**Answer:**

It should begin graceful shutdown:

1.  Stop accepting new requests.
2.  Allow active requests to finish within a reasonable timeout.
3.  Stop background workers from accepting new jobs.
4.  Close database and other connections.
5.  Flush logs and exit with an appropriate status.

### Q145. Your EventEmitter listener runs twice. What could be wrong?

**Answer:**

The listener may have been registered more than once, or the event may
have been emitted multiple times. Inspect listener registration and
event emission paths. Use `once()` if the listener should run only once.

### Q146. A `Promise.all()` task rejects, but other operations may still be running. What should you know?

**Answer:**

`Promise.all()` rejects when one input rejects, but it does not
automatically cancel the other operations. If cancellation is needed,
design the operations to support cancellation, for example with
`AbortController` where supported.

### Q147. You need to serve an API across multiple CPU cores. What options do you have?

**Answer:**

You can run multiple Node.js processes using Cluster, a process manager,
containers, or an orchestration platform. The right approach depends on
deployment architecture and operational needs.

### Q148. Your API returns a 500 error, but the client needs a safe message. What should you do?

**Answer:**

Log the detailed error internally with useful context, avoid logging
secrets, and return a generic safe response with an appropriate status
code. Do not expose stack traces to public clients.

------------------------------------------------------------------------

# 17. Coding Interview Exercises with Solutions

## Exercise 1 --- Create a Basic HTTP Server

**Question:** Create a server that returns JSON for `GET /health` and
returns `404` for every other route.

**Solution:**

``` js
import { createServer } from "node:http";

const server = createServer((req, res) => {
  if (req.method === "GET" && req.url === "/health") {
    res.writeHead(200, {
      "Content-Type": "application/json"
    });

    res.end(JSON.stringify({
      status: "ok"
    }));

    return;
  }

  res.writeHead(404, {
    "Content-Type": "application/json"
  });

  res.end(JSON.stringify({
    message: "Not found"
  }));
});

server.listen(3000, () => {
  console.log("Server listening on port 3000");
});
```

**What this tests:** HTTP fundamentals, request methods, URL matching,
status codes, and response headers.

## Exercise 2 --- Read a File Asynchronously

**Question:** Read `notes.txt` and handle errors using async/await.

**Solution:**

``` js
import { readFile } from "node:fs/promises";

async function readNotes() {
  try {
    const content = await readFile("./notes.txt", "utf8");
    console.log(content);
  } catch (error) {
    console.error("Unable to read file:", error.message);
  }
}

readNotes();
```

**What this tests:** Promise-based APIs and error handling.

## Exercise 3 --- Build a Custom EventEmitter

**Question:** Emit an `order.created` event and register two listeners.

**Solution:**

``` js
import { EventEmitter } from "node:events";

const events = new EventEmitter();

events.on("order.created", (order) => {
  console.log("Send email:", order.id);
});

events.on("order.created", (order) => {
  console.log("Update inventory:", order.id);
});

events.emit("order.created", {
  id: 101
});
```

**What this tests:** Event-driven programming and EventEmitter.

## Exercise 4 --- Run Independent Tasks Concurrently

**Question:** Run two independent asynchronous functions concurrently
and collect both results.

**Solution:**

``` js
async function getUser() {
  return { id: 1, name: "Alex" };
}

async function getOrders() {
  return [{ id: 101 }, { id: 102 }];
}

async function main() {
  const [user, orders] = await Promise.all([
    getUser(),
    getOrders()
  ]);

  console.log({ user, orders });
}

main().catch(console.error);
```

**What this tests:** Promise composition and concurrency.

## Exercise 5 --- Copy a Large File with Streams

**Question:** Copy a large file without loading the entire file into
memory.

**Solution:**

``` js
import { createReadStream, createWriteStream } from "node:fs";
import { pipeline } from "node:stream/promises";

async function copyFile() {
  await pipeline(
    createReadStream("./large-file.bin"),
    createWriteStream("./large-file-copy.bin")
  );

  console.log("Copy complete");
}

copyFile().catch(console.error);
```

**What this tests:** Readable streams, writable streams, backpressure,
and pipeline error handling.

## Exercise 6 --- Validate Environment Variables

**Question:** Read a port from `process.env.PORT`, use 3000 as a
default, and reject invalid values.

**Solution:**

``` js
const rawPort = process.env.PORT ?? "3000";
const port = Number(rawPort);

if (!Number.isInteger(port) || port < 1 || port > 65535) {
  throw new Error("PORT must be a valid TCP port");
}

console.log("Port:", port);
```

**What this tests:** Process configuration and input validation.

## Exercise 7 --- Explain and Fix Event Loop Blocking

**Question:** Why is this code harmful in a request handler?

``` js
function calculate() {
  let total = 0;

  for (let i = 0; i < 1_000_000_000; i++) {
    total += i;
  }

  return total;
}
```

**Answer:**

The loop performs CPU-intensive synchronous work on the main JavaScript
thread. It blocks the Event Loop and delays other callbacks.

**Possible solution:** Move the calculation to a Worker Thread or a
separate processing service. The exact solution depends on the workload
and how frequently the calculation is requested.

## Exercise 8 --- Implement a Promise-Based Delay

**Question:** Write a function that resolves after a given number of
milliseconds.

**Solution:**

``` js
function delay(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function main() {
  console.log("Start");
  await delay(1000);
  console.log("One second later");
}

main();
```

**What this tests:** Promises, timers, and async/await.

## Exercise 9 --- Handle a Child Process

**Question:** Start a child process to run `node --version` and print
its output.

**Solution:**

``` js
import { spawn } from "node:child_process";

const child = spawn("node", ["--version"]);

child.stdout.on("data", (data) => {
  process.stdout.write(data);
});

child.on("error", (error) => {
  console.error("Failed to start child:", error);
});

child.on("close", (code) => {
  console.log("Exit code:", code);
});
```

**What this tests:** Child processes, standard output, and process
lifecycle events.

## Exercise 10 --- Inspect Process Memory

**Question:** Print the current process memory usage in megabytes.

**Solution:**

``` js
const memory = process.memoryUsage();

for (const [key, bytes] of Object.entries(memory)) {
  console.log(
    `${key}: ${(bytes / 1024 / 1024).toFixed(2)} MB`
  );
}
```

**What this tests:** Process metrics and memory basics.

------------------------------------------------------------------------

# 18. Rapid-Fire Revision

  -----------------------------------------------------------------------
  Question                            Short answer
  ----------------------------------- -----------------------------------
  Is Node.js a language?              No, it is a runtime.

  Which engine does Node.js use?      V8.

  What is libuv?                      A library providing the Event Loop
                                      and asynchronous I/O support.

  What is npm?                        A package manager for JavaScript
                                      packages.

  What is DNS?                        A distributed domain-name
                                      resolution system.

  What is HTTPS?                      HTTP protected by TLS.

  What is an Event Loop?              A mechanism coordinating
                                      asynchronous callbacks.

  What is non-blocking I/O?           Starting I/O without synchronously
                                      waiting for completion.

  Is Node.js completely               No. Main JavaScript normally runs
  single-threaded?                    on one thread, but the runtime uses
                                      other threads and OS facilities.

  What is concurrency?                Overlapping progress of multiple
                                      tasks.

  What is parallelism?                Simultaneous execution of multiple
                                      tasks.

  What is EventEmitter?               A named-event and listener
                                      mechanism.

  Are EventEmitter listeners async by No, they run synchronously.
  default?                            

  What is `process.nextTick()`?       A callback scheduled for the
                                      next-tick queue.

  What is `setImmediate()`?           Schedules a callback in the check
                                      phase.

  What does `setTimeout()` guarantee? A minimum delay threshold, not
                                      exact execution time.

  What is a Promise?                  A representation of an eventual
                                      result.

  Does async/await create a thread?   No.

  What is CommonJS?                   `require()` and `module.exports`.

  What is ESM?                        `import` and `export`.

  What is an IIFE?                    An immediately invoked function
                                      expression.

  What is a Buffer?                   A fixed-length sequence of bytes.

  What is a Stream?                   An abstraction for incremental data
                                      processing.

  What is backpressure?               Flow control when a producer is
                                      faster than a consumer.

  What is `process.env`?              Environment variables available to
                                      the process.

  What is graceful shutdown?          Closing work and resources cleanly
                                      before exit.

  What is a Worker Thread?            A separate JavaScript thread in the
                                      same process.

  What is a child process?            A separate operating-system
                                      process.

  What is Cluster?                    Multiple Node.js worker processes
                                      sharing a server port.

  What is profiling?                  Measuring runtime behavior to find
                                      bottlenecks.

  What is a memory leak?              Unneeded objects remain referenced.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 19. Final Interview Checklist

Use this checklist to evaluate your preparation.

## Foundation

-   [ ] I can explain what happens after entering a URL.
-   [ ] I understand DNS, HTTP, HTTPS, requests, and responses.
-   [ ] I can distinguish JavaScript, V8, and Node.js.
-   [ ] I can explain why Node.js is useful for I/O-heavy applications.

## Runtime and Architecture

-   [ ] I can explain the roles of V8 and libuv.
-   [ ] I understand the main Node.js architecture components.
-   [ ] I can explain the Event Loop phases.
-   [ ] I understand `process.nextTick()`, Promise microtasks, timers,
    and `setImmediate()`.
-   [ ] I can explain concurrency versus parallelism.
-   [ ] I understand why synchronous CPU-heavy code blocks the Event
    Loop.

## Asynchronous Programming

-   [ ] I can write callback-based code.
-   [ ] I understand Promises and their states.
-   [ ] I can use async/await with error handling.
-   [ ] I know when to use `Promise.all()` and `Promise.allSettled()`.
-   [ ] I can identify when independent operations can run concurrently.

## Modules and Core APIs

-   [ ] I can explain IIFE, CommonJS, and ESM.
-   [ ] I understand `exports` versus `module.exports`.
-   [ ] I can use `fs`, `path`, `os`, and `http`.
-   [ ] I can create a raw Node.js HTTP server.

## Streams and Production Concepts

-   [ ] I understand Buffers and all four stream types.
-   [ ] I can explain backpressure.
-   [ ] I can use `pipeline()` for file streaming.
-   [ ] I understand environment variables and graceful shutdown.
-   [ ] I can handle callback, Promise, and EventEmitter errors.

## Advanced Concepts

-   [ ] I can explain Worker Threads versus child processes.
-   [ ] I understand the purpose of Cluster.
-   [ ] I can inspect process memory.
-   [ ] I understand profiling and heap snapshots.
-   [ ] I can describe a systematic approach to diagnosing a slow API or
    memory leak.

------------------------------------------------------------------------

## Recommended Study Strategy

1.  **Round 1 --- Understand:** Read each question and answer. Focus on
    the concepts.
2.  **Round 2 --- Recall:** Hide the answers and explain each topic
    aloud.
3.  **Round 3 --- Practise:** Run the output-based examples and coding
    exercises.
4.  **Round 4 --- Interview simulation:** Answer scenario-based
    questions without notes.
5.  **Round 5 --- Review:** Revisit questions you could not answer
    confidently.

### How to give a strong interview answer

Use this simple structure:

1.  **Definition:** What is it?
2.  **Purpose:** Why do we need it?
3.  **Working:** How does it work?
4.  **Example:** Where have you used it?
5.  **Trade-off:** What limitation or alternative should be considered?

For example, when asked "What is the Event Loop?", do not stop at "It
handles asynchronous operations." Explain how it coordinates callbacks,
why non-blocking I/O matters, and how CPU-heavy synchronous JavaScript
can block it.

**Final reminder:** The goal is not to memorize these answers word for
word. Understand the concepts well enough to explain them naturally,
write code, and reason through unfamiliar situations.
