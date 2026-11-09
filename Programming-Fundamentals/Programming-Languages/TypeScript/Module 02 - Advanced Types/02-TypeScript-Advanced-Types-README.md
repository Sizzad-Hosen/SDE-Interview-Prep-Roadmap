# Module 02 --- TypeScript Modules, Types, Narrowing & Generics

*Intermediate · TypeScript Core Concepts*

**Learn Deeply. Build Practically. Explain Clearly.**

This module builds on TypeScript Fundamentals. You will learn how to
organize code with modules, combine types with unions, compare type
aliases and interfaces, understand type relationships, use type
assertions, narrow values safely, and write reusable generic
code---including generic Promise types.

Every lesson includes a simple explanation, a Mermaid visual, code
examples, real-world context, interview questions, and practice
exercises.

------------------------------------------------------------------------

## Table of Contents

-   [Learning Objectives](#learning-objectives)
-   [Your TypeScript Learning
    Workflow](#your-typescript-learning-workflow)
-   [2-0. Module Introduction](#2-0-module-introduction)
-   [2-1. Setting Up TypeScript
    Modules](#2-1-setting-up-typescript-modules)
-   [2-2. Union Types](#2-2-union-types)
-   [2-3. Type Alias vs Interface](#2-3-type-alias-vs-interface)
-   [2-4. TypeScript Type Hierarchy](#2-4-typescript-type-hierarchy)
-   [2-5. Examples of Different Types](#2-5-examples-of-different-types)
-   [2-6. Type Assertion](#2-6-type-assertion)
-   [2-7. Narrowing Down](#2-7-narrowing-down)
-   [2-8. Narrowing Continued](#2-8-narrowing-continued)
-   [2-9. Generics](#2-9-generics)
-   [2-10. Applying Generic Types to
    Promises](#2-10-applying-generic-types-to-promises)
-   [Module Review](#module-review)
-   [Final Module Challenge](#final-module-challenge)
-   [Recommended Resources](#recommended-resources)

------------------------------------------------------------------------

## Learning Objectives

By completing this module, you should be able to:

-   Organize TypeScript code with `export` and `import`.
-   Use union types to represent more than one possible type.
-   Explain similarities and differences between type aliases and
    interfaces.
-   Understand important relationships in TypeScript's type system.
-   Recognize common TypeScript type forms.
-   Use type assertions carefully.
-   Narrow union types using conditions and type guards.
-   Create reusable generic functions, interfaces, and type aliases.
-   Type asynchronous results using `Promise<T>`.
-   Build a small project using modules, narrowing, and generics.

------------------------------------------------------------------------

## Your TypeScript Learning Workflow

Follow this process for every lesson. Do not only memorize
syntax---understand why it works and when to use it.

``` mermaid
flowchart TD
    A["1. Read and Research"] --> B["2. Understand the Concept"]
    B --> C["3. Visualize the Idea"]
    C --> D["4. Write the Code"]
    D --> E["5. Practice and Debug"]
    E --> F["6. Document Your Learning"]
    F --> G["7. Review and Revise"]
    G --> A
```

1.  **Read:** Start with this lesson and the official TypeScript
    documentation.
2.  **Understand:** Explain the idea in your own words.
3.  **Visualize:** Follow the diagram and create your own example.
4.  **Implement:** Type the code yourself and run the compiler.
5.  **Practice:** Change the examples and solve the exercises.
6.  **Document:** Record useful notes and mistakes.
7.  **Review:** Explain the concept without looking at the notes.

------------------------------------------------------------------------

# 2-0. Module Introduction

*Intermediate · Module Overview*

## What Will You Learn?

In Module 01, you learned basic types, arrays, tuples, functions, object
types, type aliases, and interfaces.

In this module, you will learn how to use these ideas in more flexible
and reusable ways:

-   **Modules:** Split a project into separate files.
-   **Union types:** Allow a value to have more than one possible type.
-   **Type alias and interface:** Describe reusable data structures.
-   **Type hierarchy:** Understand broad and specific types.
-   **Type assertion:** Tell TypeScript what type you believe a value
    has.
-   **Narrowing:** Check a value and make its type more specific.
-   **Generics:** Write reusable code that preserves type information.
-   **Promise generics:** Describe the type of data returned by
    asynchronous operations.

## Visual Overview

``` mermaid
flowchart TD
    A["Module 02"] --> B["Code Organization"]
    A --> C["Type Relationships"]
    A --> D["Type Safety"]
    A --> E["Reusable Code"]

    B --> B1["Modules and Imports"]
    C --> C1["Union Types"]
    C --> C2["Type Alias vs Interface"]
    C --> C3["Type Hierarchy"]
    C --> C4["Different Types"]
    D --> D1["Type Assertion"]
    D --> D2["Narrowing"]
    E --> E1["Generics"]
    E --> E2["Generics with Promises"]
```

## Simple Explanation

This module helps you write TypeScript code that is better organized,
more flexible, reusable, type-safe, and easier to maintain.

------------------------------------------------------------------------

# 2-1. Setting Up TypeScript Modules

*Intermediate · Code Organization*

## Learning Objectives

-   Explain what a TypeScript module is.
-   Export code from one file.
-   Import code into another file.
-   Use named exports and default exports.
-   Organize a small project using modules.

## What Is a Module?

A module is a file that has its own scope and can share selected values
or types with other files.

-   `export` makes a value or type available to other modules.
-   `import` lets another module use an exported value or type.

**Simple idea:** Instead of putting all your code in one large file,
split it into smaller files and connect them when needed.

## Why Use Modules?

Modules help you keep related code together, reuse functions and types,
separate responsibilities, maintain projects, and collaborate with other
developers.

## Visual Explanation

``` mermaid
flowchart LR
    A["math.ts"] -->|"exports"| B["add() and subtract()"]
    B -->|"import"| C["app.ts"]
    C --> D["Calls imported functions"]
```

**Real-world analogy:** A company has separate departments for Finance,
HR, and Sales. Each department has its own responsibility but works with
the others. Modules organize code in a similar way.

## Named Exports and Imports

**math.ts**

``` typescript
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}
```

**app.ts**

``` typescript
import { add, subtract } from "./math";

console.log(add(10, 5));      // 15
console.log(subtract(10, 5)); // 5
```

## Default Export

**greet.ts**

``` typescript
export default function greet(name: string): string {
  return `Hello, ${name}`;
}
```

**main.ts**

``` typescript
import greet from "./greet";

console.log(greet("Sadman"));
```

A module can have one default export. A default import can use a chosen
local name.

## Exporting and Importing Types

**types.ts**

``` typescript
export interface User {
  id: number;
  name: string;
}
```

**app.ts**

``` typescript
import type { User } from "./types";

const user: User = {
  id: 1,
  name: "Sadman"
};

console.log(user.name);
```

`import type` makes it clear that the imported declaration is needed
only for type checking.

## Example Project Structure

``` text
my-typescript-app/
├── src/
│   ├── app.ts
│   ├── math.ts
│   ├── greet.ts
│   └── types.ts
├── package.json
└── tsconfig.json
```

The exact import paths and module settings depend on your project
configuration, such as Node.js ESM or CommonJS.

## Named Export vs Default Export

  -----------------------------------------------------------------------
  Feature                 Named Export            Default Export
  ----------------------- ----------------------- -----------------------
  Number per module       Multiple                One

  Import syntax           Usually uses `{ }`      No `{ }` required

  Import name             Matches exported name   Can choose a local name
                          unless aliased          
  -----------------------------------------------------------------------

## Common Mistakes

-   Importing from the wrong file path.
-   Using braces incorrectly for default imports.
-   Forgetting to export a function or type.
-   Mixing module systems without configuring the project.
-   Assuming every TypeScript file is automatically a module. A file
    with a top-level import or export is treated as a module.

## Interview Questions

**Q1. What is a module in TypeScript?**\
A file with its own scope that can export and import values or types.

**Q2. What is the purpose of `export`?**\
It makes selected declarations available to other modules.

**Q3. What is the difference between named and default exports?**\
A module can have multiple named exports but only one default export.
Their import syntax is different.

**Q4. Can we export an interface?**\
Yes. Interfaces and type aliases can be exported and imported.

## Practice Exercises

1.  Create `math.ts` and export two functions.
2.  Import both functions into `app.ts`.
3.  Create a default-exported greeting function.
4.  Create and export a `Product` interface.
5.  Import the `Product` type using `import type`.
6.  Organize the files inside a `src` folder.

## Quick Revision

-   `export` shares declarations.
-   `import` uses declarations from another module.
-   Named exports use their exported names.
-   A module can have one default export.
-   Types can be imported with `import type`.

------------------------------------------------------------------------

# 2-2. Union Types

*Intermediate · Flexible Types*

## Learning Objectives

-   Explain what a union type is.
-   Use the `|` operator.
-   Create functions that accept multiple types.
-   Understand why narrowing is needed when using unions.

## What Is a Union Type?

A union type allows a value to be one of several specified types. It
uses the pipe symbol (`|`).

``` typescript
let id: string | number;

id = "USER-101"; // Valid
id = 101;        // Valid
// id = true;    // Error
```

Here, `id` can be a string or a number, but not a boolean.

## Visual Explanation

``` mermaid
flowchart TD
    A["id: string | number"]
    A --> B["string"]
    A --> C["number"]
    B --> D["Allowed value"]
    C --> D
```

**Real-world analogy:** A customer may identify an account using a
numeric ID or a text-based membership code. The value has two possible
formats, so a union type is useful.

## Union Types in Functions

``` typescript
function printId(id: string | number): void {
  console.log("ID:", id);
}

printId(101);
printId("USER-101");
```

## Why Is Narrowing Needed?

A union value may be one of several types. TypeScript only allows
operations that are valid for every possible member until you narrow the
value.

``` typescript
function printId(id: string | number): void {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(2));
  }
}
```

## Union with Literal Types

``` typescript
type Status = "pending" | "success" | "failed";

let orderStatus: Status = "pending";

orderStatus = "success";
// orderStatus = "completed"; // Error
```

## Common Mistakes

-   Calling a type-specific method before narrowing.
-   Forgetting to narrow a union before using type-specific methods.
-   Making a union wider than necessary.
-   Confusing a union (`|`) with an intersection (`&`).

## Interview Questions

**Q1. What is a union type?**\
It allows a value to be one of several specified types.

**Q2. Which symbol is used for a union?**\
The pipe symbol (`|`).

**Q3. Can a union contain literal types?**\
Yes. For example, `"pending" | "success" | "failed"`.

## Practice Exercises

1.  Create a variable with type `string | number`.
2.  Write a function that accepts `string | boolean`.
3.  Create an order status union.
4.  Use `typeof` to narrow a union.
5.  Try using a string method before narrowing and inspect the error.

## Quick Revision

-   Union means one of several possible types.
-   The `|` operator creates a union.
-   Narrow a union before using operations specific to one member.

------------------------------------------------------------------------

# 2-3. Type Alias vs Interface

*Intermediate · Reusable Type Design*

## Learning Objectives

-   Define a type alias.
-   Define an interface.
-   Understand what both have in common.
-   Explain their important differences.
-   Extend object definitions using both approaches.

## What Is a Type Alias?

A type alias gives a name to a type.

``` typescript
type User = {
  id: number;
  name: string;
};
```

A type alias can describe object types, unions, primitives, tuples, and
more.

``` typescript
type ID = string | number;
type Status = "pending" | "success" | "failed";
```

## What Is an Interface?

An interface describes the expected structure of an object.

``` typescript
interface User {
  id: number;
  name: string;
}
```

It is commonly used to describe object contracts.

## Visual Explanation

``` mermaid
flowchart TD
    A["Need a reusable type"]
    A --> B["Type Alias"]
    A --> C["Interface"]
    B --> D["Objects, unions, primitives, tuples"]
    C --> E["Object contracts and extension"]
    D --> F["Type checking"]
    E --> F
```

**Real-world analogy:** A registration form requires a name and email
address. A type alias or interface can describe the expected fields so
TypeScript can check objects against that structure.

## Type Alias Example

``` typescript
type Product = {
  id: number;
  name: string;
  price: number;
};

const product: Product = {
  id: 1,
  name: "Keyboard",
  price: 2500
};
```

## Interface Example

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

## Extending Types

**Extending an interface**

``` typescript
interface Person {
  name: string;
}

interface Employee extends Person {
  employeeId: number;
}
```

**Combining type aliases**

``` typescript
type Person = {
  name: string;
};

type Employee = Person & {
  employeeId: number;
};
```

## Main Differences

  -----------------------------------------------------------------------
  Feature                 Type Alias              Interface
  ----------------------- ----------------------- -----------------------
  Describe object shape   Yes                     Yes

  Union types             Yes                     Not directly

  Primitive aliases       Yes                     No

  Tuple aliases           Yes                     No

  Combine object shapes   Intersection (`&`)      `extends` or
                                                  intersection

  Declaration merging     No                      Yes
  -----------------------------------------------------------------------

Both are useful. Choose based on the type you need and keep your project
style consistent.

## Declaration Merging

Interfaces with the same name can be merged.

``` typescript
interface Account {
  id: number;
}

interface Account {
  email: string;
}

const account: Account = {
  id: 1,
  email: "user@example.com"
};
```

Type aliases cannot be declared repeatedly with the same name in the
same scope.

## Common Mistakes

-   Assuming interfaces can directly define union types.
-   Assuming type aliases cannot describe object shapes.
-   Thinking one is always better than the other.
-   Forgetting that interface declaration merging can change the final
    shape.

## Interview Questions

**Q1. Can both type aliases and interfaces describe objects?**\
Yes.

**Q2. Which one can directly define a union type?**\
A type alias.

**Q3. Which one supports declaration merging?**\
An interface.

**Q4. How can you combine two object types?**\
Use an intersection (`&`) or extend an interface.

## Practice Exercises

1.  Create a `Product` type alias.
2.  Create a `Customer` interface.
3.  Create a union type for payment status.
4.  Extend an interface to create an `Admin`.
5.  Combine two type aliases using `&`.
6.  Try interface declaration merging.

## Quick Revision

-   A type alias names a type expression.
-   An interface describes an object contract.
-   Both can describe object shapes.
-   Interfaces support declaration merging.
-   Type aliases can directly represent unions and tuples.

------------------------------------------------------------------------

# 2-4. TypeScript Type Hierarchy

*Intermediate · Type Relationships*

## Learning Objectives

-   Understand broad and specific types.
-   Explain `unknown`, `any`, and `never`.
-   Understand assignability at a basic level.
-   Recognize why `never` is useful in exhaustive checks.

## What Is Type Hierarchy?

TypeScript types have relationships. Some types are broad and can accept
many values. Other types are more specific and accept fewer values.

A useful way to understand the type system is through assignability:

-   A value of a more specific type can often be assigned to a broader
    compatible type.
-   A broad value usually needs checking before it can be assigned to a
    more specific type.

## Important Types

**`unknown`**\
A safe top type for values whose types are not known. Any value can be
assigned to `unknown`, but you must narrow it before performing
type-specific operations.

**`any`**\
Disables most type checking. It can be assigned to and from almost any
type, so use it carefully.

**`never`**\
The bottom type. It represents values that cannot occur.

## Visual Explanation: Simplified Type Relationships

``` mermaid
flowchart BT
    N["never"] --> S["string"]
    N --> Num["number"]
    N --> Bool["boolean"]
    N --> Obj["object"]

    S --> U["unknown"]
    Num --> U
    Bool --> U
    Obj --> U
```

**Important:** This is a simplified learning picture, not a complete
TypeScript type lattice. `any` has special assignability behavior and
does not fit neatly into an ordinary top-to-bottom hierarchy. Union,
intersection, literal, and structural object types add further
relationships.

## Examples

**Unknown**

``` typescript
let value: unknown = "TypeScript";

// Error: value is not known to be a string.
// console.log(value.toUpperCase());

if (typeof value === "string") {
  console.log(value.toUpperCase());
}
```

**Any**

``` typescript
let data: any = 10;

data = "Hello";
data = true;
```

**Never**

``` typescript
function fail(message: string): never {
  throw new Error(message);
}
```

## Exhaustive Checking with Never

``` typescript
type Status = "pending" | "success";

function handleStatus(status: Status): string {
  switch (status) {
    case "pending":
      return "Please wait";

    case "success":
      return "Completed";

    default: {
      const impossible: never = status;
      return impossible;
    }
  }
}
```

If another status is added but not handled, the exhaustive check can
help reveal the missing case.

## Real-world Analogy

-   `unknown`: A sealed box. Inspect it before using what is inside.
-   `any`: A box with no type rules enforced by TypeScript.
-   `never`: A value that cannot exist in the current situation.

## Common Mistakes

-   Treating `unknown` like `any`.
-   Using `any` when `unknown` would be safer.
-   Thinking `never` means `null` or `undefined`.
-   Assuming one diagram can show every relationship in TypeScript's
    type system.

## Interview Questions

**Q1. What is the difference between `any` and `unknown`?**\
`any` disables most type checking. `unknown` requires narrowing before
type-specific operations.

**Q2. What is `never`?**\
It is the bottom type, used for values that cannot occur.

**Q3. Why is `never` useful in switch statements?**\
It can help ensure every member of a union has been handled.

## Practice Exercises

1.  Assign a string to an `unknown` variable.
2.  Try to call a string method before narrowing.
3.  Narrow the value with `typeof`.
4.  Compare the behavior of `any` and `unknown`.
5.  Write a function that returns `never`.
6.  Create an exhaustive switch using a union type.

## Quick Revision

-   `unknown` is a safe top type.
-   `any` disables most type checking.
-   `never` is the bottom type.
-   Narrow broad values before using them.
-   Use `never` to help check exhaustive cases.

------------------------------------------------------------------------

# 2-5. Examples of Different Types

*Intermediate · Type Practice*

## Learning Objectives

-   Recognize common TypeScript type forms.
-   Read and write type annotations.
-   Understand how different types are used in practical code.
-   Choose a suitable type for a value.

## Overview of Different Types

``` mermaid
flowchart TD
    A["TypeScript Types"]
    A --> B["Primitive"]
    A --> C["Literal"]
    A --> D["Union"]
    A --> E["Array and Tuple"]
    A --> F["Object"]
    A --> G["Function"]
    A --> H["Special Types"]

    B --> B1["string, number, boolean"]
    C --> C1["'admin', 'user'"]
    D --> D1["string | number"]
    E --> E1["number[], [string, number]"]
    F --> F1["Object properties"]
    G --> G1["Parameter and return types"]
    H --> H1["any, unknown, void, never"]
```

## Primitive Types

``` typescript
let username: string = "Sadman";
let age: number = 25;
let isActive: boolean = true;
```

## Array Type

``` typescript
let scores: number[] = [80, 90, 100];
let names: Array<string> = ["Sadman", "Rakib"];
```

Both syntaxes describe arrays whose elements have the specified type.

## Tuple Type

``` typescript
let userInfo: [string, number] = ["Sadman", 25];
```

The first position is a string and the second position is a number.

## Object Type

``` typescript
let user: {
  name: string;
  age: number;
} = {
  name: "Sadman",
  age: 25
};
```

## Literal Type

``` typescript
type Direction = "left" | "right" | "up" | "down";

let move: Direction = "left";
```

A literal type allows only specific exact values.

## Function Type

``` typescript
function multiply(a: number, b: number): number {
  return a * b;
}
```

## Union Type

``` typescript
let id: string | number;

id = 101;
id = "USER-101";
```

## Special Types

``` typescript
let unknownValue: unknown = "Hello";
let flexibleValue: any = 42;

function logMessage(): void {
  console.log("Hello");
}

function stop(message: string): never {
  throw new Error(message);
}
```

## Quick Comparison

  Type         Example              Use
  ------------ -------------------- ----------------------------
  `string`     `"Hello"`            Text
  `number`     `25`                 Numeric values
  `boolean`    `true`               True or false
  `number[]`   `[10, 20]`           List of numbers
  Tuple        `[string, number]`   Fixed-position values
  Object       `{ name: "Sam" }`    Related properties
  Literal      `"success"`          A specific allowed value
  Union        `string \| number`   One of several types
  `unknown`    External input       Unknown values
  `void`       Function return      No meaningful return value
  `never`      Throwing function    No normal completion

## Practice Exercises

1.  Create a string, number, and boolean variable.
2.  Create an array of product prices.
3.  Create a tuple for a person's name and age.
4.  Create an object type for a product.
5.  Create a literal type for order status.
6.  Write a function with typed parameters and return value.
7.  Create a `string | number` variable and narrow it.

## Quick Revision

-   TypeScript supports primitive and structured types.
-   Literal types restrict values to specific choices.
-   Union types allow one of several types.
-   Function types describe parameters and return values.
-   Choose the narrowest useful type for better type safety.

------------------------------------------------------------------------

# 2-6. Type Assertion

*Intermediate · Working with Existing Values*

## Learning Objectives

-   Explain what type assertion does.
-   Use the `as` syntax.
-   Understand when assertions are useful.
-   Recognize why incorrect assertions are dangerous.

## What Is Type Assertion?

Type assertion tells TypeScript to treat a value as a particular type.

It is useful when you know more about a value than TypeScript can infer
from the code.

**Important:** Type assertion does not convert the value and does not
validate it at runtime. It only changes how TypeScript understands the
value during type checking.

## Syntax

``` typescript
const value: unknown = "Hello TypeScript";

const text = value as string;

console.log(text.toUpperCase());
```

## Visual Explanation

``` mermaid
flowchart TD
    A["Value with a broad or unknown type"]
    A --> B["Developer has additional information"]
    B --> C["Type assertion: value as string"]
    C --> D["TypeScript treats it as string"]
    D --> E["String operations are allowed"]
    E --> F["Runtime value is not converted"]
```

## Real-world Example: DOM Element

``` typescript
const input = document.getElementById("username") as HTMLInputElement;

console.log(input.value);
```

The assertion tells TypeScript to treat the element as an
`HTMLInputElement`.

However, if the element does not exist or is not actually an input, the
assertion does not fix that problem.

A safer version checks the value:

``` typescript
const element = document.getElementById("username");

if (element instanceof HTMLInputElement) {
  console.log(element.value);
}
```

## `as` vs Angle-Bracket Syntax

TypeScript also supports angle-bracket assertions:

``` typescript
const value: unknown = "Hello";
const text = <string>value;
```

The `as` syntax is generally preferred in projects that use JSX, because
angle brackets are also used by JSX syntax.

## Common Mistakes

-   Thinking assertion converts a value.
-   Asserting a type without checking the real data.
-   Using assertions to silence errors instead of fixing the underlying
    problem.
-   Assuming an API response is valid just because it was asserted to a
    type.

## Interview Questions

**Q1. What is type assertion?**\
It tells TypeScript to treat a value as a specified type.

**Q2. Does assertion change the runtime value?**\
No. It has no runtime conversion or validation effect.

**Q3. What is the preferred assertion syntax?**\
The `as` syntax is commonly preferred, especially in projects using JSX.

## Practice Exercises

1.  Create a variable with type `unknown`.
2.  Assert it as a string.
3.  Access a string property after assertion.
4.  Select a DOM element and safely check its type.
5.  Explain why an assertion is not the same as runtime validation.

## Quick Revision

-   Assertion changes TypeScript's view of a value.
-   `value as SomeType` is common syntax.
-   Assertion does not convert or validate runtime data.
-   Use runtime checks when data is uncertain.

------------------------------------------------------------------------

# 2-7. Narrowing Down

*Intermediate · Safer Type Usage*

## Learning Objectives

-   Explain type narrowing.
-   Narrow primitive unions with `typeof`.
-   Narrow class instances with `instanceof`.
-   Understand how conditions affect the type of a value.

## What Is Narrowing?

Narrowing is the process of making a broad type more specific based on
checks in the code.

For example, a value may be `string | number`. After checking
`typeof value === "string"`, TypeScript knows that the value is a string
inside that branch.

## Visual Explanation

``` mermaid
flowchart TD
    A["value: string | number"]
    A --> B{"typeof value === 'string'?"}
    B -->|Yes| C["value is string"]
    B -->|No| D["value is number"]
    C --> E["Use string methods"]
    D --> F["Use number methods"]
```

## Narrowing with `typeof`

``` typescript
function printValue(value: string | number): void {
  if (typeof value === "string") {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}

printValue("typescript");
printValue(25);
```

`typeof` is useful for checking primitive values such as strings,
numbers, and booleans.

## Narrowing with `instanceof`

`instanceof` checks whether an object is an instance of a particular
class or constructor.

``` typescript
class Dog {
  bark(): void {
    console.log("Woof!");
  }
}

class Cat {
  meow(): void {
    console.log("Meow!");
  }
}

function speak(animal: Dog | Cat): void {
  if (animal instanceof Dog) {
    animal.bark();
  } else {
    animal.meow();
  }
}
```

## Real-world Analogy

Imagine a package arriving at a warehouse. Before sending it to the
correct department, a worker checks its label.

Narrowing works similarly: check what kind of value you have, then
safely use the operations available for that type.

## Common Mistakes

-   Calling a type-specific method before checking the type.
-   Using `typeof` when an object-specific check is needed.
-   Forgetting that `typeof null` is `"object"` in JavaScript.
-   Assuming every object can be reliably distinguished with
    `instanceof`, especially across different realms or plain JSON data.

## Interview Questions

**Q1. What is type narrowing?**\
It is the process of reducing a broad type to a more specific type using
checks and control flow.

**Q2. When should you use `typeof`?**\
It is commonly used to narrow primitive types.

**Q3. When should you use `instanceof`?**\
It is commonly used to check whether an object is an instance of a class
or constructor.

## Practice Exercises

1.  Write a function that accepts `string | number`.
2.  Use `typeof` to handle each type.
3.  Create two classes, `Dog` and `Cat`.
4.  Use `instanceof` to call the correct method.
5.  Test the function with different values.

## Quick Revision

-   Narrowing makes a broad type more specific.
-   `typeof` is useful for primitive types.
-   `instanceof` is useful for class instances.
-   Use checks before type-specific operations.

------------------------------------------------------------------------

# 2-8. Narrowing Continued

*Intermediate · Advanced Narrowing Techniques*

## Learning Objectives

-   Narrow object unions using the `in` operator.
-   Use equality and truthiness checks.
-   Create custom type guards.
-   Use discriminated unions.
-   Understand why exhaustive checks are useful.

## Narrowing with the `in` Operator

The `in` operator checks whether a property exists in an object.

``` typescript
type Fish = {
  swim: () => void;
};

type Bird = {
  fly: () => void;
};

function move(animal: Fish | Bird): void {
  if ("swim" in animal) {
    animal.swim();
  } else {
    animal.fly();
  }
}
```

## Visual Explanation: The `in` Operator

``` mermaid
flowchart TD
    A["Fish | Bird"]
    A --> B{"Does 'swim' exist?"}
    B -->|Yes| C["Fish"]
    B -->|No| D["Bird"]
    C --> E["Call swim()"]
    D --> F["Call fly()"]
```

## Narrowing with Equality Checks

``` typescript
function compare(
  a: string | number,
  b: string | boolean
): void {
  if (a === b) {
    // Both values must be strings here.
    console.log(a.toUpperCase());
  }
}
```

The equality check helps TypeScript identify the common possible type.

## Narrowing with Truthiness

``` typescript
function printMessage(message: string | null): void {
  if (message) {
    console.log(message.toUpperCase());
  } else {
    console.log("No message");
  }
}
```

A truthiness check removes falsy possibilities from the current branch.
Be careful when valid values such as `0` or an empty string are
possible.

## Custom Type Guards

A custom type guard is a function whose return type uses a type
predicate such as `value is Admin`.

``` typescript
type Admin = {
  name: string;
  role: "admin";
};

type User = {
  name: string;
  role: "user";
};

function isAdmin(person: Admin | User): person is Admin {
  return person.role === "admin";
}

function checkPerson(person: Admin | User): void {
  if (isAdmin(person)) {
    console.log("Admin:", person.name);
  } else {
    console.log("User:", person.name);
  }
}
```

## Discriminated Unions

A discriminated union uses a shared property with different literal
values to distinguish members of a union.

``` typescript
type Success = {
  status: "success";
  data: string;
};

type Failure = {
  status: "failure";
  error: string;
};

type Result = Success | Failure;

function handleResult(result: Result): void {
  if (result.status === "success") {
    console.log(result.data);
  } else {
    console.log(result.error);
  }
}
```

## Visual Explanation: Discriminated Union

``` mermaid
flowchart TD
    A["Result: Success | Failure"]
    A --> B{"Check result.status"}
    B -->|"success"| C["Success"]
    B -->|"failure"| D["Failure"]
    C --> E["Read data"]
    D --> F["Read error"]
```

## Exhaustive Checking

Use `never` to help ensure all union members are handled.

``` typescript
type Status = "pending" | "success" | "failed";

function getMessage(status: Status): string {
  switch (status) {
    case "pending":
      return "Please wait";

    case "success":
      return "Completed";

    case "failed":
      return "Something went wrong";

    default: {
      const impossible: never = status;
      return impossible;
    }
  }
}
```

If a new union member is added but not handled, TypeScript can report an
error at the exhaustive check.

## Common Mistakes

-   Using `in` without checking whether the property is a reliable
    discriminator.
-   Forgetting that truthiness checks also treat empty strings and zero
    as falsy.
-   Writing a custom type guard whose runtime check does not prove the
    claimed type.
-   Forgetting to handle every member of a discriminated union.

## Interview Questions

**Q1. What does the `in` operator do?**\
It checks whether a property exists on an object and can help narrow
object unions.

**Q2. What is a custom type guard?**\
A function that returns a type predicate such as `value is SomeType`.

**Q3. What is a discriminated union?**\
A union whose members share a property with different literal values,
allowing TypeScript to narrow based on that property.

**Q4. Why use exhaustive checking?**\
It helps detect when a new union member has not been handled.

## Practice Exercises

1.  Create a `Fish | Bird` union and narrow it with `in`.
2.  Create a function that accepts `string | null`.
3.  Write a custom type guard for an admin user.
4.  Create a success/failure result union.
5.  Handle the result using a discriminant.
6.  Add a new union member and test your exhaustive check.

## Quick Revision

-   `in` can narrow object unions.
-   Equality and truthiness checks can narrow values.
-   Custom type guards use type predicates.
-   Discriminated unions use a shared literal property.
-   `never` can help with exhaustive checks.

------------------------------------------------------------------------

# 2-9. Generics

*Intermediate · Reusable and Type-Safe Code*

## Learning Objectives

-   Explain what generics are.
-   Create generic functions.
-   Use generic interfaces and type aliases.
-   Understand basic generic constraints.
-   Explain why generics are useful.

## What Is a Generic?

A generic allows you to write reusable code that works with different
types while preserving type information.

Instead of writing a separate function for strings, numbers, and
objects, you can create one generic function.

The letter `T` is commonly used as a type parameter name. It is not a
reserved keyword.

## Without Generics

``` typescript
function getFirstString(items: string[]): string {
  return items[0];
}

function getFirstNumber(items: number[]): number {
  return items[0];
}
```

These functions repeat the same logic for different types.

## With Generics

``` typescript
function getFirstElement<T>(items: T[]): T {
  return items[0];
}

const firstName = getFirstElement<string>(["Sadman", "Rakib"]);
const firstScore = getFirstElement<number>([80, 90, 100]);
```

TypeScript can often infer the type argument:

``` typescript
const firstName = getFirstElement(["Sadman", "Rakib"]);
const firstScore = getFirstElement([80, 90, 100]);
```

## Visual Explanation

``` mermaid
flowchart TD
    A["Generic function: getFirstElement<T>"]
    A --> B["T = string"]
    A --> C["T = number"]
    A --> D["T = User object"]
    B --> E["Returns string"]
    C --> F["Returns number"]
    D --> G["Returns User"]
```

The same function works with different types and preserves the return
type.

## Generic Function

``` typescript
function identity<T>(value: T): T {
  return value;
}

const text = identity("Hello");
const count = identity(42);
```

## Generic Interface

``` typescript
interface Box<T> {
  value: T;
}

const stringBox: Box<string> = {
  value: "TypeScript"
};

const numberBox: Box<number> = {
  value: 100
};
```

## Generic Type Alias

``` typescript
type ApiResponse<T> = {
  success: boolean;
  data: T;
};

type User = {
  id: number;
  name: string;
};

const response: ApiResponse<User> = {
  success: true,
  data: {
    id: 1,
    name: "Sadman"
  }
};
```

## Generic Constraints

Sometimes a generic function needs to know that a type has a particular
property. Use `extends` to add a constraint.

``` typescript
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}

console.log(getLength("TypeScript"));
console.log(getLength([10, 20, 30]));
```

This works because strings and arrays both have a `length` property.

## Real-world Uses

Generics are common in reusable API response types, data repositories,
reusable UI components, typed collections, utility functions, and
asynchronous code.

## Common Mistakes

-   Using `any` instead of a generic when type information should be
    preserved.
-   Assuming `T` is a special reserved keyword.
-   Using a generic when a simple concrete type would be clearer.
-   Accessing properties that are not guaranteed by the generic
    constraint.

## Interview Questions

**Q1. What is a generic?**\
A generic lets you write reusable code that works with different types
while preserving type information.

**Q2. What does `T` represent?**\
It is a type parameter. The actual type is supplied or inferred when the
generic is used.

**Q3. What is a generic constraint?**\
A constraint limits which types can be used as a generic argument, often
with `extends`.

## Practice Exercises

1.  Write a generic identity function.
2.  Write a generic function that returns the first array element.
3.  Create a generic `Box<T>` interface.
4.  Create a generic `ApiResponse<T>` type.
5.  Write a generic function with a `length` constraint.
6.  Try explicit and inferred generic arguments.

## Quick Revision

-   Generics create reusable, type-safe code.
-   `T` is a type parameter.
-   TypeScript can often infer generic arguments.
-   `extends` can constrain a generic type.
-   Generics preserve relationships between input and output types.

------------------------------------------------------------------------

# 2-10. Applying Generic Types to Promises

*Intermediate · Generics with Asynchronous Code*

## Learning Objectives

-   Understand `Promise<T>`.
-   Describe the fulfilled value of a Promise.
-   Use a generic API response type.
-   Combine generics with async functions.
-   Read typed asynchronous results.

## What Is a Promise?

A Promise represents the eventual result of an asynchronous operation.

A Promise can be:

-   **Pending:** The operation has not completed.
-   **Fulfilled:** The operation completed successfully.
-   **Rejected:** The operation failed.

## Visual Explanation: Promise States

``` mermaid
flowchart TD
    A["Start asynchronous operation"]
    A --> B["Pending"]
    B -->|Success| C["Fulfilled"]
    B -->|Failure| D["Rejected"]
```

## What Does `Promise<T>` Mean?

`Promise<T>` describes a Promise that fulfills with a value of type `T`.

``` typescript
function getMessage(): Promise<string> {
  return Promise.resolve("Hello TypeScript");
}

function getNumber(): Promise<number> {
  return Promise.resolve(100);
}
```

-   `Promise<string>` means the Promise fulfills with a string.
-   `Promise<number>` means the Promise fulfills with a number.

A rejected Promise can contain a rejection reason. `Promise<T>`
describes the fulfillment value, not a typed rejection value.

## Create a Generic API Response

``` typescript
type ApiResponse<T> = {
  success: boolean;
  data: T;
};
```

Create a User type:

``` typescript
type User = {
  id: number;
  name: string;
};
```

## Use the Generic Type with Promise

``` typescript
function fetchUser(): Promise<ApiResponse<User>> {
  return Promise.resolve({
    success: true,
    data: {
      id: 1,
      name: "Sadman"
    }
  });
}
```

The return type tells us:

1.  The function returns a Promise.
2.  The Promise fulfills with an `ApiResponse<User>`.
3.  The response's `data` property is a `User`.

## Visual Explanation: Generic Promise

``` mermaid
flowchart TD
    A["fetchUser()"]
    A --> B["Promise<ApiResponse<User>>"]
    B --> C["Promise fulfills"]
    C --> D["ApiResponse<User>"]
    D --> E["success: boolean"]
    D --> F["data: User"]
    F --> G["id: number"]
    F --> H["name: string"]
```

## Read the Result with `.then()`

``` typescript
fetchUser().then((response) => {
  console.log(response.success);
  console.log(response.data.name);
});
```

TypeScript knows the type of `response.data` because the Promise has a
generic return type.

## Read the Result with `async` and `await`

``` typescript
async function showUser(): Promise<void> {
  const response = await fetchUser();

  console.log(response.data.name);
}

showUser();
```

The `await` expression gives you the fulfilled value of the Promise.

## Another Example: Product API

``` typescript
type Product = {
  id: number;
  title: string;
  price: number;
};

function fetchProduct(): Promise<ApiResponse<Product>> {
  return Promise.resolve({
    success: true,
    data: {
      id: 101,
      title: "Mechanical Keyboard",
      price: 4500
    }
  });
}

async function showProduct(): Promise<void> {
  const response = await fetchProduct();

  console.log(response.data.title);
  console.log(response.data.price);
}
```

The same `ApiResponse<T>` type works for both users and products.

## Common Mistakes

-   Confusing `Promise<T>` with `T`.
-   Forgetting that `await` gives the fulfilled value.
-   Assuming a generic type validates actual API data at runtime.
-   Assuming `Promise<T>` describes the rejection reason.
-   Using `any` for every API response instead of describing its data
    shape.

**Important:** If data comes from an external API, validate the actual
runtime data when necessary. A TypeScript type alone does not prove that
the server returned the expected structure.

## Interview Questions

**Q1. What does `Promise<string>` mean?**\
It describes a Promise that fulfills with a string.

**Q2. Why combine generics with Promise?**\
It allows asynchronous functions to describe their returned data type
while keeping the code reusable.

**Q3. What does `Promise<ApiResponse<User>>` mean?**\
It describes a Promise that fulfills with an API response whose `data`
property is a `User`.

**Q4. Does a TypeScript interface validate API data at runtime?**\
No. Runtime validation requires actual checks or a validation library.

## Practice Exercises

1.  Create a function returning `Promise<number>`.
2.  Create a `Product` type.
3.  Create a generic `ApiResponse<T>` type.
4.  Return `Promise<ApiResponse<Product>>` from a function.
5.  Read the result using `.then()`.
6.  Read the result using `async` and `await`.
7.  Explain why runtime validation may still be needed.

## Quick Revision

-   A Promise represents an asynchronous result.
-   `Promise<T>` describes the fulfilled value type.
-   Generics make API response types reusable.
-   `await` gives access to the fulfilled value.
-   Type annotations do not validate external data at runtime.


# Final Module Challenge

## Project: User Data Viewer

Build a small TypeScript application that demonstrates the concepts from
this module.

### Requirements

1.  Create separate modules for user types and user functions.
2.  Export and import the required declarations.
3.  Use a union type for a user ID.
4.  Use an interface or type alias for a user.
5.  Use narrowing to handle different ID types.
6.  Create a generic API response type.
7.  Create a function returning `Promise<ApiResponse<User>>`.
8.  Read the result with `async` and `await`.
9.  Handle errors with `try` and `catch`.
10. Keep the code organized and readable.

### Suggested Folder Structure

``` text
user-data-viewer/
├── src/
│   ├── types/
│   │   └── user.ts
│   ├── services/
│   │   └── user-service.ts
│   ├── utils/
│   │   └── find-user.ts
│   └── index.ts
├── package.json
└── tsconfig.json
```

### Project Workflow

``` mermaid
flowchart TD
    A["Define User and API Types"]
    A --> B["Export Types from user.ts"]
    B --> C["Import Types into User Service"]
    C --> D["Create Generic API Response"]
    D --> E["Return Promise<ApiResponse<User>>"]
    E --> F["Use async and await"]
    F --> G["Narrow and Display User Data"]
```
------------------------------------------------------------------------

**Learn Deeply. Build Practically. Explain Clearly.**

*Part of the SDE Interview Prep Roadmap --- An Open-Source Software
Engineering Knowledge Base.*
