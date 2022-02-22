# INFO 443 Project 2 -- TypeScript

<figure>
<figcaption align="center"> <b>The Logo of TypeScript</b> </figcaption>
<img  src='./img/typescript.png'  alt='TypeScript logo'  width='700'>
<figcaption align="center"> <b>Figure 1: The Logo of TypeScript</b> </figcaption>
</figure>

## Project Overview
### Introduction
#### About the Codebase
This is the codebase for TypeScript, a programming language that builds on JavaScript by adding natural syntax for type specifications to data and adding compiler functionality. Developers can use TypeScript to create their own applications, either client- or server-side.
#### Authors/Maintainers
This software was developed by Microsoft (a large company) and is currently maintained by the company's employees (628 contributors). Additionally, contributions are accepted when following Microsoft's Code of Conduct, and a number of people appear to be in charge of approving these commits.
##### Frequent Contributors:
[@ahejlsberg](https://github.com/ahejlsberg), [@sheetalkamat](https://github.com/sheetalkamat), [@sandersn](https://github.com/sandersn), [@andy-ms](https://github.com/andy-ms), & [@DanielRosenwasser](https://github.com/DanielRosenwasser)

### Learn more about the system

[Official Github](https://github.com/microsoft/TypeScript) | 
[Official Documentations](https://www.typescriptlang.org/) |
[Basic Syntax](https://learnxinyminutes.com/docs/typescript/#:~:text=TypeScript%20is%20a%20language%20that,scale%20applications%20written%20in%20JavaScript.&text=It%20is%20a%20superset%20of,The%20TypeScript%20compiler%20emits%20JavaScript) |
[Compiler Details](https://www.youtube.com/watch?v=X8k_4tZ16qU)

### Team Members

INFO 443 project authors: Alex Gherman, Henry Bao, Lisi Case, & Patrick Cheng

## Development View

### Components

<details>
          <summary> Quick overview of the compilation process.[^1]</summary>

The process starts with preprocessing. 
The preprocessor figures out what files should be included in the compilation by following references (`/// <reference path=... />` tags, `require` and `import` statements).

The parser then generates AST `Node`s. 
These are just an abstract representation of the user input in a tree format. 
A `SourceFile` object represents an AST for a given file with some additional information like the file name and source text. 

The binder then passes over the AST nodes and generates and binds `Symbol`s.
One `Symbol` is created for each named entity.
There is a subtle distinction but several declaration nodes can name the same entity.
That means that sometimes different `Node`s will have the same `Symbol`, and each `Symbol` keeps track of its declaration `Node`s.
For example, a `class` and a `namespace` with the same name can *merge* and will have the same `Symbol`.
The binder also handles scopes and makes sure that each `Symbol` is created in the correct enclosing scope.

Generating a `SourceFile` (along with its `Symbol`s) is done through calling the `createSourceFile` API.

So far, `Symbol`s represent named entities as seen within a single file, but several declarations can merge multiple files, so the next step is to build a global view of all files in the compilation  by building a `Program`.

A `Program` is a collection of `SourceFile`s and a set of `CompilerOptions`.
A `Program` is created by calling the `createProgram` API. 

From a `Program` instance a `TypeChecker` can be created. 
`TypeChecker` is the core of the TypeScript type system. 
It is the part responsible for figuring out relationships between `Symbols` from different files, assigning `Type`s to `Symbol`s, and generating any semantic `Diagnostic`s (i.e. errors).

The first thing a `TypeChecker` will do is to consolidate all the `Symbol`s from different `SourceFile`s into a single view, and build a single Symbol Table by "merging" any common `Symbol`s (e.g. `namespace`s spanning multiple files).  

After initializing the original state, the `TypeChecker` is ready to answer any questions about the program.
Such "questions" might be: 
* What is the `Symbol` for this `Node`?
* What is the `Type` of this `Symbol`?
* What `Symbol`s are visible in this portion of the AST?
* What are the available `Signature`s for a function declaration?
* What errors should be reported for a file?

The `TypeChecker` computes everything lazily; it only "resolves" the necessary information to answer a question.
The checker will only examine `Node`s/`Symbol`s/`Type`s that contribute to the question at hand and will not attempt to examine additional entities.

An `Emitter` can also be created from a given `Program`.
The `Emitter` is responsible for generating the desired output for a given `SourceFile`; this includes `.js`, `.jsx`, `.d.ts`, and `.js.map` outputs. 
 </details>

 
### Table of the main components of TypeScript Compiler

|Component |Role & Relationship|Description|
|--|--|--|
|Program.ts|Core Compiler|Initializes and runs the necessary files involved in the compiler|
|Parser.ts|Crates a syntax tree<br>Depends on: Scanner|<ul><li>Makes tokens from scanner into a tree with more meaning <li> Knows when the right JavaScript is in the wrong context</ul>|
|Scanner.ts|Internally used and created by Parser|<ul><li>Converts text into syntax tokens <li> Knows only if the JavaScript itself is wrong</ul>|
|Checker.ts|Checks the syntax tree<br>Depends on: Binder|<ul><li>Provides most of the compiler diagnostics<li>Checks each part of syntax tree's node</ul>|
|Binder.ts|Internally used by Checker|<ul><li>Turns syntax into symbols<li>Sets up flow containers based on code scope with flow conditionals within<li>Sees a full syntax tree</ul>|
|Emitter.ts|Creates files<br>Depends on: Transformer|<ul><li>Takes a syntax tree and turns it into a file/files<li>Prints the tree into .js, .ts, and other file types</ul>|
|Transformer.ts|Used by Emitter|<ul><li>Takes a syntax tree and transforms it in various ways to match TypeScript configurations</ul>|


### System Organization Diagram

#### Dependencies

### Source Code Structure (Codeline Model)

### Testing & Configuration

Tests can be run manually from the TypeScript directory using Gulp tools after installing some dependencies.

#### Directory

Change to the TypeScript directory:

```bash
cd TypeScript
```

#### Dependencies

Install [Gulp](https://gulpjs.com/) tools and dev dependencies:

```bash
npm install -g gulp
npm ci
````

#### Tests

Run tests for the compiler using the following command:

```
gulp runtests --runner=<compiler>        # Run tests for the compiler suite.
```

Additional commands to run tests of your choice and record results are as follows:

```
gulp tests                               # Build the test infrastructure using the built compiler.
gulp runtests                            # Run tests using the built compiler and test infrastructure.
gulp runtests --runner=<runnerName>      # Run tests for a specific suite (e.g., conformance, compiler, fourslash, project, user, and docker).
                                         # Note: You'll need to have the docker executable in your system path for the docker runner to work, 
                                         # although we are not focusing on docker at the moment.
gulp runtests --tests=<testPath>         # Run a specific test.
gulp runtests-parallel                   # Like runtests, but split across multiple threads. Uses a number of threads equal to the system
                                         # core count by default. Use --workers=<number> to adjust this.
gulp baseline-accept                     # Replace the baseline test results with the results obtained from gulp runtests.
```

## Applied Perspective

## Styles & Patterns Used

## Architectural Assessment

## System Improvement


## Foot Notes
[^1]: [TypeScript Compiler Notes by Microsoft](https://github.com/microsoft/TypeScript-Compiler-Notes)