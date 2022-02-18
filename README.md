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
