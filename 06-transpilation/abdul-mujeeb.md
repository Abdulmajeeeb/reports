# Transpilation

## What is trasnpilation?

Transpilation is the process of converting one source code into another form of source code.

```text
Source code → Transpiler → Other source code
```
### Difference Between Transpilation and Compilation

**Transpilation** is a process of converting code written in a high-level language into another high-level language while keeping a similar level of abstraction, usually for compatibility.

While **compilation** is the process of converting source code into a lower-level representation, such as machine code.

For example:

```text
Transpilation:
Modern JavaScript → Older JavaScript

Compilation:
High-level source code → Machine code
```

## Why it exists?

For the purpose of **compatibility**.

Say a person uses the newer syntax/style to write code for the sake of conciseness, but the browser doesn't understand that syntax. So, before presenting the code to the browser, it is transpiled first into such a form which is understandable or executable by the browser.

Another reason for transpilation is that some languages, such as TypeScript, cannot be executed directly by the browser. Therefore, TypeScript code can be transpiled into JavaScript, which the browser can execute.

## How?

Transpilation is performed before the code is served to the browser. It is a kind of development process. Before a code is served, it is transpiled first. The process is done by a software tool/program, e.g.

* **Babel**
  A tool that converts JavaScript into JavaScript, like a newer version into an older version.

* **TypeScript compiler (`tsc`)**
  A compiler which converts TypeScript code into JavaScript.

### Basic Process

1. A person writes code, then the transpiler is run when the file is saved or as per the developer's settings.

   `Write source code → received by the transpiler`

2. Then the code is parsed by the transpiler, where it understands the structure of the code and represents it as an **Abstract Syntax Tree (AST)**.

   `Parsed → AST`

3. The original AST is then transformed into a compatible version.

   `AST → Transformed AST`

4. According to the new AST, the code generator generates another form of code, called transpiled code. Then the browser has access to the transpiled code.

   `Transformed AST → Code generator → Transpiled code → Browser`

#### Overall Process

```text
Write source code
       ↓
     Parser
       ↓
      AST
       ↓
  Transform AST
       ↓
 Code generator
       ↓
Transpiled source code
       ↓
    Browser
```

---

#### Process Example

##### TypeScript into JavaScript

1. ###### TypeScript Source Code

   ```ts
   let age: number = 28;
   ```

2. ###### Parser

   #### Understands the Structure

   * Create a variable called `age`
   * Type of the variable is `number`
   * Value of the variable is `28`

   ###### AST

   Abstract Syntax Tree is the structured representation of the parsed code.

   * Variable declaration

     * name = `age`
     * type = `number`
     * value = `28`

3. ###### Transform the AST

   For JavaScript, remove the TypeScript-specific information:

   * `: number`

4. ###### Code Generator

   Generate the JavaScript source code:

   ```js
   let age = 28;
   ```

   ###### Export

   The transpiled code is delivered to the browser, so the JavaScript can be executed.

In this process, the transpiler `tsc` performs all the tasks, like:

* parsing
* creating AST
* transforming AST
* generating JavaScript

---

## Proofs

### Example 1: TypeScript Function with Types into Plain JavaScript

Consider a TypeScript code:

```ts
function multiply(a: number, b: number): number {
    return a * b;
}

let ans: number = multiply(2, 3);

console.log(ans);
```

After the transpiler converts the code into JavaScript, the output is:

```js
function multiply(a, b) {
    return a * b;
}

let ans = multiply(2, 3);

console.log(ans);
```

Verified using the [TypeScript Playground](https://www.typescriptlang.org/play).

The transpiler does not change the intended logic behind the code. In this case, it removes the TypeScript-specific type annotations.

---

### Example 2: JavaScript Arrow Function

Suppose a function is written in modern syntax and then the transpiler converts it into an older version so that the browser can execute it.

#### Modern Function

```js
let multiply = (a, b) => a * b;
```

#### AST

When the transpiler parses this code, it identifies its AST in the following way:

* Variable declaration

  * `multiply`

    * Arrow Function

      * parameters

        * `a`
        * `b`
      * binary expression: `*`

        * `a`
        * `b`

*This is a variable named `multiply` whose value is an arrow function with two parameters, `a` and `b`, and whose body is `a * b`.*

After understanding the structure, the transpiler transforms the AST into a structure representing the older syntax of JavaScript.

#### New AST

* Variable declaration

  * `multiply`

    * Function Expression

      * parameters

        * `a`
        * `b`
      * Return Statement

        * binary expression: `*`

          * `a`
          * `b`

Then the **code generator** takes this new AST and generates the new code.

#### Transpiled Code

```js
var multiply = function multiply(a, b) {
    return a * b;
};
```

Verified using the [Babel REPL](https://babeljs.io/repl).

---

## Gist

***Transpilation*** *is the transformation of one source code into another source code for the purpose of compatibility, usually done before it is executed.*

---

## Source Maps

Mostly, the code executed by the browser is transformed in some format, either transpiled or minified, from the original source code written by the developer.

A source map is a JSON file that contains mappings between the generated code and the original source code. It allows the browser's developer tools to link a specific line in the generated code to the corresponding line in the original source code.

This is useful for debugging because the developer can see and debug the original source code instead of only seeing the transformed code.

For example:

```text
Original source code
        ↓
    Transpiler
        ↓
Generated JavaScript
        ↓
      Browser
        ↑
   Source map
        ↑
Original source code
```
---

## Difference Between Transpilation and Minification

**Transpilation** converts the code into another version or form for the sake of compatibility, such as from modern JavaScript to an older version of JavaScript.

On the other hand, **minification** is the process of removing unnecessary whitespace, comments, and, when possible, reducing variable names for the sake of reducing file size and improving performance.

For example, consider the following code:

```js
var multiply = function multiply(a, b) {
    return a * b;
};
```

After **minification**, it can become something like:

```js
var m = function multiply(a,b){return a*b;};
```

The language and logic remain the same. The main purpose is to make the code smaller.

---

## References

1. [What is transpiling? — Medium](https://medium.com/@edgington.m.w/what-is-transpiling-4438f33697ed)
2. [TypeScript: Transpile TypeScript into JavaScript — Node.js](https://nodejs.org/learn/typescript/transpile)
3. [Understanding JavaScript Bundlers: Bundling, Transpiling, Minifying & More — Medium](https://medium.com/@jitendrakhilar609/understanding-javascript-bundlers-bundling-transpiling-minifying-more-342cd412d9de)
4. [Difference Between Transpiler and Compiler — GeeksforGeeks](https://www.geeksforgeeks.org/compiler-design/difference-between-transpiler-and-compiler/)
5. [Source map — MDN Web Docs](https://developer.mozilla.org/en-US/docs/Glossary/Source_map)
