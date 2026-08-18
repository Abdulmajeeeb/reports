# Transpilation

## What?

Transpilation is the process of converting one source code into another form of source code.

```text
Source code → Transpiler → Other source code
```

---

## When?

Transpilation is performed before the code is served to the browser. It is a kind of development process. Before a code is served, it is transpiled first.

---

## Why?

For the purpose of **Compatibility**.

Say a person uses the newer script/style to write code for the sake of conciseness, but the browser doesn't understand that script. So, before presenting the code to the browser, it is transpiled first into such a form which is understandable or executable by the browser.

---

## Tool?

The process is done by a software tool/program, e.g.

* **Babel**
  A tool that converts JavaScript into JavaScript, like a newer version into an older version.

* **TypeScript compiler (`tsc`)**
  A compiler which converts TypeScript language into JavaScript.

---

## Basic Process

1. A person writes code, then the transpiler is run by default when the file is saved or as per the developer's settings.

   `Write source code → received by the transpiler`

2. Then the code is parsed by the transpiler, where it understands the structure of the code, like **Abstract Syntax Tree (AST)**.

   `Parsed → AST`

3. The original version of the AST is then transformed into a compatible version, understandable by the browser.

   `AST → Transform AST`

4. According to the new AST, the code generator generates another code which is named as transpiled code. Then the browser has access to the transpiled code.

   `Transformed AST → Code generator → Transpiled code → Browser`

### Overall process

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

## Example

### TypeScript into JavaScript

1. ### TypeScript source code

   ```ts
   let age: number = 28;
   ```

2. ### Parser

   #### Understands the structure

   * Create a variable called `age`
   * Type of the variable is `number`
   * Value of the variable is `28`

   ### AST

   Abstract Syntax Tree is the structured representation of the parsed code.

   * Variable declaration

     * name = `age`
     * type = `number`
     * value = `28`

3. ### Transform the AST

   For JavaScript, remove the TypeScript-specific information:

   * `: number`

4. ### Code Generator

   Generate the JavaScript source code:

   ```js
   let age = 28;
   ```

   ### Export

   The transpiled code is delivered to the browser, so the JavaScript can be executed.

In this process, the transpiler `tsc` performs all the tasks, like:

* parsing
* creating AST
* transforming AST
* generating JavaScript

---

## Gist

***Transpilation*** *is the transformation of one source code into another source code for the purpose of compatibility, usually done before it is executed.*
