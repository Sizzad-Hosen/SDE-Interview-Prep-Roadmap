# Module 01 --- TypeScript Fundamentals

**Learn Deeply. Build Practically. Explain Clearly.**

Welcome to Module 01 of the TypeScript learning path. This module builds
the foundation for understanding TypeScript, its relationship with
JavaScript, its compiler, development environment, and core type system.

Every lesson includes an easy explanation, a visual diagram, practical
code examples, real-world context, and exercises.

------------------------------------------------------------------------

## Table of Contents

-   [Learning Objectives](#learning-objectives)
-   [Your TypeScript Learning
    Workflow](#your-typescript-learning-workflow)
-   [1-1. Why Use TypeScript?](#1-1-why-use-typescript)
-   [1-2. What Is TypeScript?](#1-2-what-is-typescript)
-   [1-3. How TypeScript Works Under the
    Hood](#1-3-how-typescript-works-under-the-hood)
-   [1-4. Development Environment
    Setup](#1-4-development-environment-setup)
-   [1-5. Basic Types in TypeScript](#1-5-basic-types-in-typescript)
-   [1-6. tsconfig and Compiling TypeScript to
    JavaScript](#1-6-tsconfig-and-compiling-typescript-to-javascript)
-   [1-7. Array, Tuple, and Readonly
    Modifier](#1-7-array-tuple-and-readonly-modifier)
-   [1-8. Optional and Default Parameters in
    Functions](#1-8-optional-and-default-parameters-in-functions)
-   [1-9. Rest Parameters in
    Functions](#1-9-rest-parameters-in-functions)
-   [1-10. Objects, Type Alias, and
    Interface](#1-10-objects-type-alias-and-interface)
-   [Module Review](#module-review)
-   [Recommended Resources](#recommended-resources)

------------------------------------------------------------------------

## Learning Objectives

By completing this module, you should be able to:

-   Explain why TypeScript is used and what problems it helps solve.
-   Describe TypeScript as a typed superset of JavaScript.
-   Understand the roles of the TypeScript compiler, CLI, Language
    Service, `tsserver`, and LSP.
-   Explain the major stages of TypeScript compilation.
-   Set up a TypeScript development environment.
-   Use basic types and understand type inference.
-   Work with arrays, tuples, and readonly data.
-   Define functions with optional, default, and rest parameters.
-   Describe and type objects using type aliases and interfaces.
-   Configure a TypeScript project using `tsconfig.json`.
-   Compile TypeScript into JavaScript and run the output.

------------------------------------------------------------------------

# 1-1. Why Use TypeScript?

*Beginner · Introduction to TypeScript*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Explain common challenges in JavaScript projects.
-   Describe how TypeScript's static type system helps.
-   Understand the benefits and limitations of TypeScript.
-   Identify situations where TypeScript is useful.

## 2. Introduction

JavaScript is widely used for frontend and backend development. It is
flexible and quick to get started with. However, as an application
becomes larger, its code can become harder to maintain.

For example, a function may expect a number but accidentally receive a
string. JavaScript may accept the value and produce an unexpected
result. Other problems may only appear when a particular line of code
runs.

TypeScript builds on JavaScript and adds a static type system. It helps
developers describe the kinds of values their code expects and catches
many type-related mistakes before the application runs.

**In simple terms:** TypeScript helps developers find many mistakes
earlier and makes the intention of code easier to understand.

## 3. The Problem with JavaScript

JavaScript is dynamically typed. A variable can hold values of different
types during execution.

### Example: Unexpected type conversion

``` javascript
function add(a, b) {
  return a + b;
}

console.log(add(10, 20));    // 30
console.log(add(10, "20"));  // "1020"
```

The second call returns a string because JavaScript uses the `+`
operator for both addition and string concatenation.

### Example: Unexpected runtime error

``` javascript
function greet(user) {
  return user.name.toUpperCase();
}

console.log(greet(null)); // Runtime error
```

The function assumes that `user` is an object. Passing `null` causes an
error when the code tries to access `name`.

## 4. How TypeScript Helps

TypeScript lets us describe the expected types of function parameters
and return values.

``` typescript
function add(a: number, b: number): number {
  return a + b;
}

console.log(add(10, 20));   // 30
// add(10, "20");           // TypeScript error
```

The compiler can report that a string is not assignable to a number
parameter.

This does not mean TypeScript prevents every possible bug. It helps
catch many mistakes related to types before runtime.

## 5. Visual Explanation

### JavaScript and TypeScript: Two Development Paths

``` mermaid
flowchart TD
    subgraph JS["JavaScript workflow"]
        A["Write JavaScript"] --> B["Run the application"]
        B --> C["A type-related problem may appear at runtime"]
    end

    subgraph TS["TypeScript workflow"]
        D["Write TypeScript"] --> E["Static type checking"]
        E --> F{"Type error?"}
        F -->|Yes| G["Review and fix the code"]
        G --> E
        F -->|No| H["Compile to JavaScript"]
        H --> I["Run the application"]
    end
```

### Real-world analogy: Quality control

Imagine a factory that checks products before shipping them. Finding a
defect before a product reaches the customer is usually cheaper than
finding it afterward.

TypeScript provides a similar early-checking step for many type-related
problems in code.

## 6. Benefits of TypeScript

  -----------------------------------------------------------------------
  Benefit                             Explanation
  ----------------------------------- -----------------------------------
  Earlier error detection             Finds many type-related mistakes
                                      during development

  Better editor support               Enables autocomplete, navigation,
                                      and useful diagnostics

  Maintainability                     Makes data structures and function
                                      contracts clearer

  Refactoring support                 Helps identify code affected by a
                                      change

  Readability                         Makes expected inputs and outputs
                                      more explicit

  Team collaboration                  Helps developers understand shared
                                      code
  -----------------------------------------------------------------------

## 7. Limitations and Trade-offs

-   TypeScript adds a learning curve and project configuration.
-   Types are generally erased when TypeScript is compiled to
    JavaScript.
-   TypeScript does not automatically validate data received from an
    API.
-   Incorrect type assertions can hide problems.
-   It does not replace tests, security checks, or runtime error
    handling.

For example, data received from an external API should be validated at
runtime when its shape cannot be trusted.

## 8. Real-world Applications

TypeScript is commonly used in:

-   Large frontend applications.
-   React, Angular, and other frontend projects.
-   Node.js backend services.
-   Full-stack applications.
-   Shared libraries and SDKs.
-   Enterprise applications maintained by multiple developers.

## 9. Interview Questions

**Q1. Why do developers use TypeScript instead of plain JavaScript?**

TypeScript adds static type checking and stronger development tooling.
It helps catch many type-related mistakes earlier and makes large
codebases easier to maintain.

**Q2. Does TypeScript prevent all runtime errors?**

No. It catches many type-related errors, but runtime validation,
testing, and error handling are still necessary.

**Q3. Does TypeScript replace JavaScript?**

No. TypeScript builds on JavaScript and is commonly compiled into
JavaScript for execution.

## 10. Practice Exercises

1.  Write a JavaScript function that adds two values.
2.  Call it with two numbers and then with a number and a string.
3.  Rewrite the function in TypeScript with number parameters.
4.  Pass an incorrect argument and inspect the compiler diagnostic.
5.  Explain one bug that static type checking can catch and one runtime
    problem it cannot guarantee to catch.

## Quick Revision

-   JavaScript is dynamically typed.
-   TypeScript adds a static type system to JavaScript.
-   TypeScript catches many type-related errors during development.
-   TypeScript improves editor support and maintainability.
-   TypeScript does not replace runtime validation or testing.

------------------------------------------------------------------------

# 1-2. What Is TypeScript?

*Introduction to TypeScript*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Define TypeScript.
-   Explain the relationship between JavaScript and TypeScript.
-   Describe TypeScript's compiler and CLI.
-   Understand the TypeScript Language Service.
-   Distinguish `tsserver` from the Language Server Protocol (LSP).

## 2. What Is TypeScript?

TypeScript is a strongly typed programming language that builds on
JavaScript. It adds a static type system and development-time tooling
while retaining JavaScript as its runtime foundation.

TypeScript source code is typically compiled into JavaScript. Browsers
and Node.js execute the generated JavaScript, not TypeScript type
annotations.

## 3. TypeScript as a Superset of JavaScript

A typed superset means that TypeScript supports JavaScript syntax and
adds type-related features. In general, valid JavaScript code can be
used as TypeScript code, although project settings and type-checking
rules may reveal issues that need attention.

``` mermaid
flowchart TD
    A["JavaScript language features"] --> C["TypeScript"]
    B["Static type system and type syntax"] --> C
    C --> D["TypeScript source code"]
    D --> E["TypeScript compiler"]
    E --> F["JavaScript output"]
    F --> G["Browser or Node.js"]
```

## 4. TypeScript as a Programming Language

TypeScript provides features such as:

-   Variables and functions.
-   Classes and interfaces.
-   Type annotations and type inference.
-   Generics.
-   Union and intersection types.
-   Modules.
-   Compile-time type checking.

Example:

``` typescript
type User = {
  id: number;
  name: string;
};

function greet(user: User): string {
  return `Hello, ${user.name}`;
}

const student: User = {
  id: 1,
  name: "Sadman"
};

console.log(greet(student));
```

## 5. Static Type Checking

Static type checking means checking type compatibility without executing
the program.

``` typescript
let age: number = 25;

age = 30;       // Valid
// age = "30";  // TypeScript error
```

The TypeScript compiler can report the incorrect assignment during
development.

**Important:** TypeScript's types are primarily a development-time
system. They are not automatically enforced by the JavaScript runtime.

## 6. TypeScript Compiler (`tsc`)

The TypeScript compiler is commonly invoked using the `tsc` command.

Its responsibilities include:

-   Reading TypeScript source files.
-   Checking types and reporting diagnostics.
-   Applying compiler options.
-   Emitting JavaScript and, when configured, declaration or source map
    files.

Example:

``` bash
npx tsc
```

This compiles a project using its `tsconfig.json`, if one is present.

## 7. TypeScript CLI

CLI means **Command-Line Interface**. It allows developers to run
TypeScript tools from a terminal.

Common commands:

``` bash
# Check the installed TypeScript version
npx tsc --version

# Create a tsconfig.json file
npx tsc --init

# Compile the project
npx tsc

# Show compiler help
npx tsc --help
```

## 8. TypeScript Language Service

The TypeScript Language Service provides editor features that understand
TypeScript code.

Examples include:

-   Autocomplete.
-   Error diagnostics.
-   Go to Definition.
-   Find References.
-   Rename Symbol.
-   Refactoring support.
-   Type information on hover.

``` mermaid
flowchart TD
    A["Developer writes TypeScript"] --> B["Code Editor"]
    B <--> C["TypeScript Language Service"]
    C --> D["Autocomplete"]
    C --> E["Type Diagnostics"]
    C --> F["Go to Definition"]
    C --> G["Find References"]
    C --> H["Refactoring"]
```

## 9. `tsserver` and LSP

These terms are related but not identical.

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  TypeScript Language Service         The APIs that provide
                                      TypeScript-aware editor features

  `tsserver`                          The TypeScript server process that
                                      exposes language-service
                                      functionality to editors through
                                      its own protocol

  LSP                                 Language Server Protocol, a
                                      standardized protocol for
                                      communication between an editor and
                                      a language server

  `typescript-language-server`        A separate implementation that
                                      exposes TypeScript language
                                      features through LSP
  -----------------------------------------------------------------------

A useful way to remember this:

-   Language Service provides the language intelligence.
-   `tsserver` exposes TypeScript editor functionality through its
    server protocol.
-   LSP is a standard communication protocol used by compatible editors
    and language servers.

## 10. Visual Summary: TypeScript Development Tools

``` mermaid
flowchart LR
    A["Developer"] --> B["TypeScript source"]
    A --> C["Editor"]

    B --> D["TypeScript compiler: tsc"]
    D --> E["JavaScript output"]

    C <--> F["TypeScript editor integration"]
    F --> G["Language Service"]
    F --> H["tsserver or an LSP-based server"]

    G --> I["Autocomplete and diagnostics"]
    H --> I
```

## 11. Interview Questions

**Q1. What is TypeScript?**

TypeScript is a programming language that builds on JavaScript and adds
a static type system.

**Q2. What is the TypeScript compiler?**

It is the tool commonly invoked as `tsc` to type-check TypeScript code
and emit JavaScript or other configured outputs.

**Q3. What is the difference between `tsc` and `tsserver`?**

`tsc` is the compiler command-line tool. `tsserver` is a server process
used to provide TypeScript language features to editors.

**Q4. What is LSP?**

LSP is a standardized protocol that allows code editors to communicate
with language servers.

## 12. Practice Exercises

1.  Explain TypeScript as a typed superset of JavaScript.
2.  Run `npx tsc --version`.
3.  Create a TypeScript file and compile it.
4.  Explore autocomplete and type diagnostics in VS Code.
5.  Explain the difference between the compiler, Language Service,
    `tsserver`, and LSP.

## Quick Revision

-   TypeScript builds on JavaScript.
-   TypeScript adds a static type system.
-   `tsc` is the compiler CLI.
-   The Language Service powers TypeScript-aware editor features.
-   `tsserver` and LSP are related to editor communication, but they are
    not the same thing.

------------------------------------------------------------------------

# 1-3. How TypeScript Works Under the Hood

*Beginner · Compiler Fundamentals*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Explain the main stages of TypeScript compilation.
-   Understand tokens, parsing, and the Abstract Syntax Tree.
-   Describe the roles of the binder, type checker, and emitter.
-   Explain why TypeScript types do not normally exist in generated
    JavaScript.

## 2. Introduction

When you write TypeScript, the code does not normally run directly in a
browser or Node.js. The TypeScript compiler processes the source code
and can generate JavaScript.

Think of the compiler as a processing pipeline: it reads the source,
understands its structure, checks types, reports diagnostics, and emits
output according to the project configuration.

## 3. The Compilation Pipeline

``` mermaid
flowchart TD
    A["TypeScript source file (.ts)"] --> B["Scanner / Lexer"]
    B --> C["Tokens"]
    C --> D["Parser"]
    D --> E["Abstract Syntax Tree (AST)"]
    E --> F["Binder"]
    F --> G["Type Checker"]
    G --> H["Diagnostics"]
    G --> I["Emitter"]
    I --> J["JavaScript output (.js)"]
    I --> K["Optional declaration files (.d.ts)"]
    J --> L["JavaScript runtime"]
```

The diagram is a simplified learning model. The compiler has more
internal details and may perform work in ways that are not strictly a
single linear pass.

## 4. Understand Each Stage

### 4.1 Scanner / Lexer

The scanner reads source text and identifies tokens such as:

-   Keywords.
-   Identifiers.
-   Operators.
-   Numbers.
-   Strings.
-   Punctuation.

Example:

``` typescript
const age: number = 25;
```

The scanner identifies pieces such as `const`, `age`, `:`, `number`,
`=`, and `25`.

### 4.2 Parser

The parser takes tokens and analyzes their grammatical structure. It
builds a tree representation of the source code.

### 4.3 Abstract Syntax Tree (AST)

An AST represents the structure of a program as a tree.

For example, a variable declaration can be represented by a node
containing the variable name, type annotation, and initializer.

### 4.4 Binder

The binder connects declarations and references by creating symbols and
establishing relationships between scopes.

### 4.5 Type Checker

The type checker checks whether values are used consistently with their
types.

``` typescript
let age: number = 25;

// TypeScript reports an error:
// age = "twenty-five";
```

### 4.6 Emitter

The emitter generates output files according to compiler options. This
may include JavaScript, declaration files, and source maps.

## 5. Visual Analogy: A Code Factory

Imagine a factory:

1.  Raw materials arrive --- source code.
2.  Materials are separated --- scanning.
3.  Parts are organized --- parsing and AST creation.
4.  Labels and relationships are checked --- binding.
5.  Quality control happens --- type checking.
6.  The finished product is packaged --- emitting JavaScript.

## 6. Type Erasure: Where Do Type Annotations Go?

Consider this TypeScript:

``` typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

A simplified JavaScript output is:

``` javascript
function greet(name) {
  return `Hello, ${name}`;
}
```

The type annotations are removed during compilation. JavaScript does not
know that `name` was declared as a `string` in the original TypeScript
source.

## 7. Important Notes

-   TypeScript type checking is a development-time process.
-   Generated JavaScript runs in the JavaScript runtime.
-   Type annotations are generally erased.
-   Compiler options can affect whether output is emitted after errors.
-   With `noEmitOnError: true`, TypeScript does not emit output when
    errors are reported.

## 8. Interview Questions

**Q1. What is an AST?**

An Abstract Syntax Tree is a tree representation of the grammatical
structure of source code.

**Q2. What does the TypeScript type checker do?**

It checks type compatibility and reports type-related diagnostics.

**Q3. Does JavaScript understand TypeScript types?**

No. TypeScript type annotations are generally erased before JavaScript
execution.

**Q4. What is the emitter?**

The emitter generates output files, such as JavaScript, according to
compiler settings.

## 9. Practice Exercises

1.  Write a small TypeScript function.
2.  Compile it using `npx tsc`.
3.  Open the generated JavaScript file.
4.  Compare the TypeScript and JavaScript versions.
5.  Identify which TypeScript-only syntax disappeared.

## Quick Revision

-   Scanner identifies tokens.
-   Parser builds the source structure.
-   AST represents code as a tree.
-   Binder creates symbols and scope relationships.
-   Type checker checks type compatibility.
-   Emitter generates configured output files.

------------------------------------------------------------------------

# 1-4. Development Environment Setup

*Beginner · Environment and Tooling*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Install the tools needed for TypeScript development.
-   Create a TypeScript project.
-   Install TypeScript as a development dependency.
-   Create and compile a `.ts` file.
-   Run the generated JavaScript.

## 2. Required Tools

  Tool         Purpose
  ------------ ----------------------------------------
  Node.js      Runs JavaScript outside the browser
  npm          Installs and manages packages
  TypeScript   Provides the compiler and type checker
  VS Code      Code editor with TypeScript support
  Terminal     Runs project commands

## 3. Environment Setup Workflow

``` mermaid
flowchart TD
    A["Install Node.js"] --> B["npm is included"]
    B --> C["Create project directory"]
    C --> D["Initialize npm project"]
    D --> E["Install TypeScript"]
    E --> F["Initialize TypeScript configuration"]
    F --> G["Create src/index.ts"]
    G --> H["Compile TypeScript"]
    H --> I["Run generated JavaScript"]
```

## 4. Step-by-Step Setup

### Step 1 --- Install Node.js

Install a current Node.js LTS release from the official website:

https://nodejs.org/

Verify the installation:

``` bash
node --version
npm --version
```

### Step 2 --- Create a Project

``` bash
mkdir typescript-learning
cd typescript-learning
```

### Step 3 --- Initialize npm

``` bash
npm init -y
```

This creates a `package.json` file to describe the project and its
dependencies.

### Step 4 --- Install TypeScript

``` bash
npm install --save-dev typescript
```

The `--save-dev` option adds TypeScript as a development dependency.

### Step 5 --- Create a TypeScript Configuration

``` bash
npx tsc --init
```

This creates a `tsconfig.json` file. You will study its options in
Lesson 1-6.

### Step 6 --- Create Your First TypeScript File

Create `src/index.ts`:

``` typescript
const message: string = "Hello TypeScript!";

console.log(message);
```

### Step 7 --- Compile and Run

``` bash
npx tsc
```

If the compiler configuration emits JavaScript to the `dist` folder,
run:

``` bash
node dist/index.js
```

The exact output path depends on your `tsconfig.json`.

## 5. Recommended Project Structure

``` text
typescript-learning/
│
├── src/
│   └── index.ts
│
├── dist/
│   └── index.js
│
├── node_modules/
├── package.json
├── package-lock.json
└── tsconfig.json
```

## 6. Common Mistakes

-   Installing TypeScript globally when the project uses a local
    version.
-   Running commands from the wrong directory.
-   Trying to execute a `.ts` file directly with Node.js without an
    appropriate TypeScript execution setup.
-   Forgetting to compile before running generated JavaScript.
-   Committing `node_modules` to a normal application repository.

## 7. Practice Exercises

1.  Install Node.js and verify `node` and `npm`.
2.  Create a new project directory.
3.  Initialize npm.
4.  Install TypeScript as a development dependency.
5.  Create `src/index.ts`.
6.  Compile and run your first TypeScript program.

## Quick Revision

-   Node.js provides the JavaScript runtime.
-   npm manages project packages.
-   TypeScript is installed as a development dependency.
-   `npx tsc --init` creates a TypeScript configuration.
-   `npx tsc` compiles the project.

------------------------------------------------------------------------

# 1-5. Basic Types in TypeScript

*Beginner · Core Type System*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Understand primitive types.
-   Use special types such as `any`, `unknown`, `void`, and `never`.
-   Type variables and function return values.
-   Understand type inference.
-   Recognize common type errors.

## 2. What Is a Type?

A type describes the kind of value a variable can hold and the
operations that are valid for that value.

Examples:

-   A person's name is usually a `string`.
-   A person's age is usually a `number`.
-   Whether an account is active can be a `boolean`.

## 3. TypeScript Type Categories

``` mermaid
flowchart TD
    A["TypeScript Type System"]

    A --> B["Primitive Types"]
    B --> C["string"]
    B --> D["number"]
    B --> E["boolean"]
    B --> F["bigint"]
    B --> G["symbol"]
    B --> H["null and undefined"]

    A --> I["Special Types"]
    I --> J["any"]
    I --> K["unknown"]
    I --> L["void"]
    I --> M["never"]

    A --> N["Structured Types"]
    N --> O["Object Types"]
    N --> P["Array Types"]
    N --> Q["Function Types"]
```

## 4. Primitive Types

### 4.1 String

Used for text.

``` typescript
let username: string = "Sadman";
let message: string = "Welcome to TypeScript";
```

### 4.2 Number

Used for integer and floating-point numbers.

``` typescript
let age: number = 25;
let price: number = 99.99;
```

### 4.3 Boolean

Used for `true` or `false`.

``` typescript
let isLoggedIn: boolean = true;
let isAdmin: boolean = false;
```

### 4.4 BigInt

Used for integers larger than the safe integer range of JavaScript's
`number` type.

``` typescript
let largeNumber: bigint = 9007199254740993n;
```

### 4.5 Symbol

Used to create unique symbol values.

``` typescript
const id: symbol = Symbol("id");
```

### 4.6 Null and Undefined

``` typescript
let emptyValue: null = null;
let missingValue: undefined = undefined;
```

With strict null checking enabled, `null` and `undefined` are treated as
distinct types and must be handled explicitly.

## 5. Special Types

### 5.1 Any

`any` disables most type checking for a value. Use it carefully.

``` typescript
let data: any = 10;

data = "Hello";
data = true;
```

### 5.2 Unknown

`unknown` can hold any value, but you must narrow or validate it before
using it in a type-specific way.

``` typescript
let value: unknown = "TypeScript";

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

Prefer `unknown` over `any` when the type is not known.

### 5.3 Void

Commonly used as the return type of a function that does not return a
meaningful value.

``` typescript
function logMessage(): void {
  console.log("Learning TypeScript");
}
```

### 5.4 Never

Represents values that never occur. It is commonly used for functions
that never finish normally, or for exhaustive checks.

``` typescript
function throwError(message: string): never {
  throw new Error(message);
}
```

## 6. Type Inference

TypeScript can often infer a variable's type from its initial value.

``` typescript
let city = "Dhaka";
// TypeScript infers: string

let count = 10;
// TypeScript infers: number
```

You do not need to write an explicit type annotation everywhere.

## 7. Visual Explanation: Choosing a Type

``` mermaid
flowchart TD
    A["What kind of value are you storing?"]
    A --> B["Text"]
    A --> C["Numeric value"]
    A --> D["True or false"]
    A --> E["Unknown external value"]
    A --> F["No meaningful function return"]

    B --> G["string"]
    C --> H["number or bigint"]
    D --> I["boolean"]
    E --> J["unknown + validation"]
    F --> K["void"]
```

## 8. Real-world Example

``` typescript
let username: string = "Sadman";
let age: number = 25;
let isActive: boolean = true;

console.log(`${username} is ${age} years old.`);
console.log(`Active account: ${isActive}`);
```

  Data            Type         Example
  --------------- ------------ ------------
  Username        `string`     `"Sadman"`
  Age             `number`     `25`
  Active status   `boolean`    `true`
  Scores          `number[]`   `[80, 90]`

## 9. Common Mistakes

-   Using `any` everywhere and losing type safety.
-   Assuming `unknown` can be used without narrowing.
-   Confusing `void` and `never`.
-   Assuming TypeScript types validate external data at runtime.
-   Adding unnecessary type annotations when inference is already clear.

## 10. Interview Questions

**Q1. What is the difference between `any` and `unknown`?**

`any` largely disables type checking. `unknown` requires the value to be
narrowed or checked before type-specific operations.

**Q2. What is type inference?**

Type inference is TypeScript's ability to determine a type from the
surrounding code, such as a variable's initial value.

**Q3. What is the difference between `void` and `never`?**

`void` commonly describes a function that returns no meaningful value.
`never` describes a value that never occurs or a function that never
completes normally.

## 11. Practice Exercises

1.  Create variables for a name, age, email, and active status.
2.  Write a function that returns a number.
3.  Write a function with a `void` return type.
4.  Store a value as `unknown` and safely narrow it.
5.  Create a function that throws an error and returns `never`.

## Quick Revision

-   `string`, `number`, and `boolean` are common primitive types.
-   `any` opts out of much type checking.
-   `unknown` is safer for values whose types are not known.
-   `void` is commonly used for functions with no meaningful return
    value.
-   `never` represents a value that cannot occur.
-   TypeScript can infer types automatically.

------------------------------------------------------------------------

# 1-6. tsconfig and Compiling TypeScript to JavaScript

*Beginner · Environment and Configuration*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Explain the purpose of `tsconfig.json`.
-   Understand common compiler options.
-   Configure source and output directories.
-   Compile TypeScript into JavaScript.
-   Understand the relationship between compiler settings and output.

## 2. What Is `tsconfig.json`?

`tsconfig.json` is the project configuration file used by the TypeScript
compiler.

It controls how TypeScript files are checked and how output is
generated.

Think of it as an instruction manual for the compiler.

## 3. Compilation Workflow

``` mermaid
flowchart TD
    A["src/index.ts"] --> C["TypeScript Compiler: tsc"]
    B["tsconfig.json"] --> C
    C --> D["Read compiler options"]
    D --> E["Type checking"]
    E --> F["Emit JavaScript"]
    F --> G["dist/index.js"]
    G --> H["Node.js or Browser"]
```

## 4. Important Compiler Options

  -----------------------------------------------------------------------
  Option                              Purpose
  ----------------------------------- -----------------------------------
  `target`                            Selects the JavaScript language
                                      target

  `module`                            Controls the module format used for
                                      emitted JavaScript

  `strict`                            Enables a family of stricter
                                      type-checking options

  `rootDir`                           Defines the expected source
                                      directory

  `outDir`                            Defines the output directory

  `sourceMap`                         Generates source maps for debugging

  `noEmitOnError`                     Prevents output emission when
                                      errors are reported

  `esModuleInterop`                   Enables compatibility helpers for
                                      certain CommonJS imports
  -----------------------------------------------------------------------

## 5. Example `tsconfig.json`

The following is a simple learning configuration for a CommonJS-based
Node.js project:

``` json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "CommonJS",
    "strict": true,
    "rootDir": "./src",
    "outDir": "./dist",
    "sourceMap": true,
    "noEmitOnError": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```

Module settings should match the runtime and package configuration used
by your project. Modern Node.js projects may use Node's native ESM
configuration instead.

## 6. Source and Output Structure

``` text
typescript-learning/
│
├── src/
│   └── index.ts
│
├── dist/
│   └── index.js
│
├── package.json
└── tsconfig.json
```

-   `src/` contains your TypeScript source files.
-   `dist/` contains the generated JavaScript files.
-   `tsconfig.json` controls compiler behavior.

## 7. Compile the Project

``` bash
# Compile using tsconfig.json
npx tsc

# Run the generated JavaScript
node dist/index.js
```

You can also ask the compiler to check the project without emitting
files:

``` bash
npx tsc --noEmit
```

## 8. Common Mistakes

-   Setting `rootDir` to a folder that does not contain the intended
    source files.
-   Expecting output in `dist/` without configuring `outDir`.
-   Mixing CommonJS and ESM settings without understanding the runtime.
-   Assuming `strict: true` performs runtime validation.
-   Forgetting that compiler options affect emitted output.

## 9. Interview Questions

**Q1. What is `tsconfig.json`?**

It is the project configuration file that tells the TypeScript compiler
which files to include and which compiler options to use.

**Q2. What does `strict: true` do?**

It enables a group of stricter type-checking options.

**Q3. What is the purpose of `outDir`?**

It specifies the directory where emitted files are placed.

**Q4. What does `noEmitOnError` do?**

When enabled, it prevents the compiler from emitting output if errors
are reported.

## 10. Practice Exercises

1.  Create a `tsconfig.json` file.
2.  Set `rootDir` to `src` and `outDir` to `dist`.
3.  Enable strict type checking.
4.  Compile a TypeScript file.
5.  Inspect the generated JavaScript.
6.  Introduce a type error and test `noEmitOnError`.

## Quick Revision

-   `tsconfig.json` configures the TypeScript project.
-   `target` controls the JavaScript language target.
-   `module` controls the emitted module format.
-   `strict` enables stricter type checking.
-   `rootDir` and `outDir` organize source and output files.
-   `noEmitOnError` can stop output generation when errors are reported.

------------------------------------------------------------------------

# 1-7. Array, Tuple, and Readonly Modifier

*Beginner · Core Type System*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Declare typed arrays.
-   Understand tuples and fixed positions.
-   Use readonly arrays and tuples.
-   Choose between arrays and tuples for different data structures.

## 2. What Is an Array?

An array stores multiple values in an ordered collection.

A typed array describes the type of its elements.

``` typescript
let scores: number[] = [80, 90, 95];

let names: string[] = ["Sadman", "Rakib", "Amin"];
```

Another syntax is:

``` typescript
let scores: Array<number> = [80, 90, 95];
```

## 3. What Is a Tuple?

A tuple describes an array with a known number of positions and a type
associated with each position.

``` typescript
let user: [string, number] = ["Sadman", 25];
```

Here:

-   Position 0 must be a string.
-   Position 1 must be a number.

A tuple is useful when the position of each value has a specific
meaning.

## 4. What Is Readonly?

Readonly prevents certain changes through that reference.

``` typescript
const scores: readonly number[] = [80, 90, 95];

// scores.push(100); // Error
// scores[0] = 85;    // Error
```

Readonly tuple:

``` typescript
const user: readonly [string, number] = ["Sadman", 25];

// user[1] = 26; // Error
```

Readonly is a compile-time restriction. It does not automatically freeze
an object or array at runtime.

## 5. Visual Explanation

``` mermaid
flowchart TD
    A["Collection Types"]
    A --> B["Array"]
    A --> C["Tuple"]
    A --> D["Readonly Array or Tuple"]

    B --> E["Multiple elements"]
    E --> F["Usually one element type"]

    C --> G["Known positions"]
    G --> H["Position-specific types"]

    D --> I["Read allowed"]
    D --> J["Mutation through this reference is restricted"]
```

### Visual Analogy

-   Array: A row of storage boxes that can hold many values of the same
    type.
-   Tuple: A form with specific fields, such as name followed by age.
-   Readonly: A read-only document that you can inspect but cannot edit
    through that reference.

## 6. Array vs Tuple

  -----------------------------------------------------------------------
  Feature                 Array                   Tuple
  ----------------------- ----------------------- -----------------------
  Number of elements      Usually flexible        Known positions and
                                                  usually known length

  Element types           Usually one element     Can have different
                          type                    types by position

  Access                  By index                By index with
                                                  position-specific types

  Common use              Lists of scores or      Coordinates, pairs,
                          names                   structured return
                                                  values
  -----------------------------------------------------------------------

## 7. Practical Examples

### Array

``` typescript
const productPrices: number[] = [100, 200, 300];

productPrices.push(400);

console.log(productPrices);
```

### Tuple

``` typescript
type UserRecord = [number, string, boolean];

const user: UserRecord = [1, "Sadman", true];

console.log(user[1]);
```

### Readonly Array

``` typescript
function printScores(scores: readonly number[]): void {
  scores.forEach((score) => console.log(score));
}

printScores([80, 90, 95]);
```

## 8. Common Mistakes

-   Using a tuple when a normal array is more appropriate.
-   Assuming `readonly` makes data deeply immutable at runtime.
-   Assigning values in the wrong tuple position.
-   Mixing element types in an array without declaring a union type.

## 9. Interview Questions

**Q1. What is the difference between an array and a tuple?**

An array is generally a collection of elements of one element type. A
tuple describes known positions with specific types.

**Q2. What does `readonly` do?**

It prevents mutation through the readonly reference at compile time.

**Q3. Does readonly freeze an array at runtime?**

No. TypeScript's readonly modifier is a type-system restriction, not a
runtime freeze operation.

## 10. Practice Exercises

1.  Create an array of five product prices.
2.  Create a tuple containing a person's name and age.
3.  Create a readonly array of strings.
4.  Try to modify a readonly array and inspect the compiler error.
5.  Write a function that accepts a readonly array of numbers.

## Quick Revision

-   Arrays store ordered collections of values.
-   Tuples describe known positions and their types.
-   `readonly` restricts mutation through a reference.
-   Readonly types do not automatically freeze data at runtime.

------------------------------------------------------------------------

# 1-8. Optional and Default Parameters in Functions

*Beginner · Functions and Parameters*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Define function parameters with types.
-   Use optional parameters.
-   Use default parameter values.
-   Understand what happens when an argument is omitted.

## 2. Optional Parameters

An optional parameter is marked with `?`. The caller can omit it.

``` typescript
function greet(name: string, title?: string): string {
  if (title) {
    return `Hello ${title} ${name}`;
  }

  return `Hello ${name}`;
}

console.log(greet("Sadman"));
console.log(greet("Sadman", "Mr."));
```

An optional parameter may be `undefined` when it is not supplied.

Optional parameters should follow required parameters in a function's
parameter list.

## 3. Default Parameters

A default parameter uses a predefined value when the caller omits the
argument or passes `undefined`.

``` typescript
function welcome(
  name: string,
  role: string = "Developer"
): string {
  return `${name} is a ${role}`;
}

console.log(welcome("Sadman"));
console.log(welcome("Sadman", "Engineer"));
```

## 4. Optional vs Default Parameters

  -----------------------------------------------------------------------
  Feature                 Optional Parameter      Default Parameter
  ----------------------- ----------------------- -----------------------
  Syntax                  `title?: string`        `role = "Developer"`

  Can be omitted?         Yes                     Yes

  Value when omitted      `undefined`             Default value

  Typical use             Extra information may   A useful fallback is
                          be absent               available
  -----------------------------------------------------------------------

## 5. Visual Explanation

``` mermaid
flowchart TD
    A["Function is called"] --> B{"Was the argument provided?"}
    B -->|Yes| C["Use the supplied value"]
    B -->|No: Optional| D["Value is undefined"]
    B -->|No: Default| E["Use the default value"]
    C --> F["Execute function"]
    D --> F
    E --> F
```

## 6. Real-world Example

Imagine a notification function. The message is required, but the
delivery channel can be optional.

``` typescript
function sendNotification(
  message: string,
  channel: string = "email"
): void {
  console.log(`Sending "${message}" through ${channel}`);
}

sendNotification("Your order has shipped");
sendNotification("Your order has shipped", "SMS");
```

## 7. Common Mistakes

-   Putting an optional parameter before a required parameter.
-   Confusing an optional parameter with a parameter that has a default
    value.
-   Assuming an optional parameter always contains a value.
-   Passing `null` and assuming it behaves like an omitted argument.
    `null` and `undefined` are different values.

## 8. Interview Questions

**Q1. How do you make a function parameter optional?**

Add `?` after the parameter name, such as `title?: string`.

**Q2. What happens when a default parameter is omitted?**

The default value is used.

**Q3. What is the difference between optional and default parameters?**

An omitted optional parameter is `undefined`; an omitted default
parameter receives its default value.

## 9. Practice Exercises

1.  Write a function with a required name and optional nickname.
2.  Write a function with a default country parameter.
3.  Call each function with and without the optional argument.
4.  Pass `undefined` to a default parameter and observe the result.
5.  Explain the difference between `undefined` and `null`.

## Quick Revision

-   `?` makes a parameter optional.
-   Default parameters provide a fallback value.
-   Optional parameters may be `undefined`.
-   Default parameters use their fallback when omitted or passed
    `undefined`.

------------------------------------------------------------------------

# 1-9. Rest Parameters in Functions

*Beginner · Functions and Parameters*

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Explain what a rest parameter does.
-   Collect multiple function arguments into an array.
-   Type a rest parameter.
-   Distinguish rest syntax from spread syntax.

## 2. What Is a Rest Parameter?

A rest parameter allows a function to accept zero or more arguments and
collect them into a single array.

It uses three dots (`...`) before the parameter name.

``` typescript
function calculateTotal(...numbers: number[]): number {
  return numbers.reduce((total, value) => total + value, 0);
}

console.log(calculateTotal(10, 20, 30)); // 60
console.log(calculateTotal(5, 10));      // 15
```

## 3. Visual Explanation

``` mermaid
flowchart LR
    A["10"] --> D["Rest parameter: ...numbers"]
    B["20"] --> D
    C["30"] --> D
    D --> E["numbers = [10, 20, 30]"]
    E --> F["Calculate total"]
    F --> G["60"]
```

## 4. How It Works

When the function is called:

``` typescript
calculateTotal(10, 20, 30);
```

The rest parameter receives an array:

``` typescript
numbers = [10, 20, 30];
```

The function can then use normal array methods such as `reduce`, `map`,
and `forEach`.

## 5. More Examples

### Find the maximum value

``` typescript
function findMaximum(...numbers: number[]): number {
  return Math.max(...numbers);
}

console.log(findMaximum(10, 50, 30)); // 50
```

The `...` in `Math.max(...numbers)` is spread syntax: it expands an
array into individual arguments.

### Required parameter followed by rest parameter

``` typescript
function createMessage(
  title: string,
  ...tags: string[]
): string {
  return `${title}: ${tags.join(", ")}`;
}

console.log(createMessage("Learning", "TypeScript", "JavaScript"));
```

A rest parameter must be the last parameter in a function's parameter
list.

## 6. Rest vs Spread

  -------------------------------------------------------------------------------------
  Feature                 Rest                                  Spread
  ----------------------- ------------------------------------- -----------------------
  Main purpose            Collects multiple values              Expands an iterable or
                                                                object

  Common location         Function parameter                    Function call, array,
                                                                or object expression

  Example                 `function sum(...values: number[])`   `sum(...numbers)`
  -------------------------------------------------------------------------------------

## 7. Common Mistakes

-   Forgetting to type the rest parameter.
-   Placing a rest parameter before another parameter.
-   Confusing rest syntax with spread syntax.
-   Assuming rest parameters are separate values rather than an array
    inside the function.

## 8. Interview Questions

**Q1. What is a rest parameter?**

It collects zero or more function arguments into an array.

**Q2. What symbol is used for rest parameters?**

Three dots (`...`).

**Q3. Can a function have more than one rest parameter?**

No. A function can have only one rest parameter, and it must be last.

## 9. Practice Exercises

1.  Write a function that accepts any number of numeric values and
    returns their sum.
2.  Write a function that accepts a required username and any number of
    roles.
3.  Find the maximum and minimum values from rest parameters.
4.  Use spread syntax to pass an array to a function.
5.  Explain the difference between rest and spread.

## Quick Revision

-   Rest parameters collect multiple arguments into an array.
-   They use `...` before the parameter name.
-   A rest parameter must be last.
-   Spread syntax expands values; rest syntax collects them.

------------------------------------------------------------------------

# 1-10. Objects, Type Alias, and Interface

`<sub>`{=html}Beginner · Core Type System`</sub>`{=html}

## 1. Learning Objectives

By the end of this lesson, you should be able to:

-   Describe the shape of an object using TypeScript.
-   Use type aliases to define reusable types.
-   Use interfaces to describe object contracts.
-   Understand basic differences between type aliases and interfaces.
-   Reuse and extend object definitions.

## 2. What Is an Object Type?

An object groups related data using properties.

For example, a user may have an ID, name, and email address.

``` typescript
const user: {
  id: number;
  name: string;
  email: string;
} = {
  id: 1,
  name: "Sadman",
  email: "sadman@example.com"
};
```

This works, but repeating the same object shape throughout a project can
make code harder to maintain.

Type aliases and interfaces help create reusable descriptions.

## 3. Type Alias

A type alias gives a name to a type.

``` typescript
type User = {
  id: number;
  name: string;
  email: string;
};

const user: User = {
  id: 1,
  name: "Sadman",
  email: "sadman@example.com"
};
```

A type alias can describe more than object shapes.

``` typescript
type ID = string | number;

type Status = "pending" | "success" | "failed";
```

## 4. Interface

An interface describes the shape that an object should follow.

``` typescript
interface Admin {
  id: number;
  name: string;
  permissions: string[];
}

const admin: Admin = {
  id: 2,
  name: "Admin",
  permissions: ["read", "write"]
};
```

Interfaces can be extended:

``` typescript
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  permissions: string[];
}
```

## 5. Visual Explanation

``` mermaid
flowchart TD
    A["Object data"] --> B["Need a reusable structure"]
    B --> C["Type Alias"]
    B --> D["Interface"]
    C --> E["Describe properties and other types"]
    D --> F["Describe object contract"]
    E --> G["Type checking"]
    F --> G
    G --> H["More predictable object usage"]
```

### Real-world analogy: A form or blueprint

Imagine a registration form that always requires a name, email, and ID.

A type alias or interface acts like the form's blueprint. It describes
which fields are expected and what kind of values each field should
contain.

## 6. Type Alias vs Interface

  -----------------------------------------------------------------------
  Feature                 Type Alias              Interface
  ----------------------- ----------------------- -----------------------
  Describe object shape   Yes                     Yes

  Describe union types    Yes                     Not directly

  Describe intersection   Yes                     Can extend or be
  types                                           combined through other
                                                  type expressions

  Extend another object   Commonly with `&`       With `extends`
  shape                                           

  Declaration merging     No                      Yes

  Typical use             Unions, primitives,     Object contracts and
                          tuples, and object      extensible shapes
                          types                   
  -----------------------------------------------------------------------

### Extending with a type alias

``` typescript
type User = {
  id: number;
  name: string;
};

type Admin = User & {
  permissions: string[];
};
```

### Extending with an interface

``` typescript
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  permissions: string[];
}
```

Both approaches can be useful. Choose a consistent style for your
project.

## 7. Optional and Readonly Object Properties

Object properties can also be optional or readonly.

``` typescript
interface Profile {
  readonly id: number;
  name: string;
  bio?: string;
}

const profile: Profile = {
  id: 1,
  name: "Sadman"
};

// profile.id = 2; // Error: readonly property
profile.name = "Sadman Sazid";
```

-   `bio?` means the property may be omitted.
-   `readonly` prevents reassignment through this reference at compile
    time.

## 8. Common Mistakes

-   Using an object type that is too broad when a more specific shape is
    needed.
-   Confusing optional properties with properties that must contain
    `undefined`.
-   Assuming `readonly` freezes an object at runtime.
-   Assuming interfaces can directly represent union types.
-   Believing type aliases and interfaces are interchangeable in every
    situation.

## 9. Interview Questions

**Q1. What is a type alias?**

A type alias gives a name to a type, which may describe an object,
union, primitive, tuple, or other type expression.

**Q2. What is an interface?**

An interface describes an object shape or contract that values can be
checked against.

**Q3. What is the main difference between type and interface?**

Both can describe object shapes. Type aliases can also represent unions
and other type expressions. Interfaces support declaration merging and
can be extended with `extends`.

**Q4. Can an interface extend another interface?**

Yes. An interface can use the `extends` keyword to inherit properties
from another interface.

## 10. Practice Exercises

1.  Create a `Product` type with ID, name, and price.
2.  Create an interface for a user profile.
3.  Add an optional property to the profile.
4.  Add a readonly ID.
5.  Extend a base interface to create an admin interface.
6.  Create a union type for order status.
7.  Explain when you would choose a type alias and when you would choose
    an interface.

## Quick Revision

-   Objects group related properties.
-   Type aliases give reusable names to types.
-   Interfaces describe object contracts.
-   Both can describe object shapes.
-   Type aliases can represent unions and other type expressions.
-   Interfaces support declaration merging and `extends`.

------------------------------------------------------------------------

# Module Review

## Complete Learning Checklist

### Introduction to TypeScript

-   [ ] 1-1. Why Use TypeScript?
-   [ ] 1-2. What Is TypeScript?
-   [ ] 1-3. How TypeScript Works Under the Hood

### Development Environment and Configuration

-   [ ] 1-4. Development Environment Setup
-   [ ] 1-6. tsconfig and Compiling TypeScript to JavaScript

### Core Type System

-   [ ] 1-5. Basic Types in TypeScript
-   [ ] 1-7. Array, Tuple, and Readonly Modifier
-   [ ] 1-8. Optional and Default Parameters in Functions
-   [ ] 1-9. Rest Parameters in Functions
-   [ ] 1-10. Objects, Type Alias, and Interface

## Final Module Challenge

Build a small command-line program called **Student Record Manager**.

Your program should:

1.  Define a `Student` type or interface.
2.  Store multiple students in a typed array.
3.  Use a tuple for a small fixed-position record.
4.  Create functions with typed parameters and return values.
5.  Use an optional parameter for additional student information.
6.  Use a default parameter for a student status.
7.  Use a rest parameter to calculate the total of multiple scores.
8.  Configure the project with `tsconfig.json`.
9.  Compile the TypeScript source into JavaScript.
10. Run the generated JavaScript using Node.js.

### Suggested Project Structure

``` text
student-record-manager/
│
├── src/
│   ├── index.ts
│   ├── student.ts
│   └── utilities.ts
│
├── dist/
├── package.json
└── tsconfig.json
```

## Module Completion Criteria

Mark this module as complete when you can:

-   Explain the core concepts without reading your notes.
-   Recreate the important examples independently.
-   Understand and fix common compiler errors.
-   Complete the final practical challenge.
-   Answer basic TypeScript interview question
------------------------------------------------------------------------

**Learn Deeply. Build Practically. Explain Clearly.**

*Part of the SDE Interview Prep Roadmap --- An Open-Source Software
Engineering Knowledge Base.*
