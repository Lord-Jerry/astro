# Astro Programming Language
![hound](https://camo.githubusercontent.com/23ee7a697b291798079e258bbc25434c4fac4f8b/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50726f7465637465645f62792d486f756e642d6138373364312e737667)
[![Build Status](https://travis-ci.org/appcypher/astro.svg?branch=dev)](https://travis-ci.org/appcypher/astro)
[![Coverage Status](https://coveralls.io/repos/github/AppCypher/Astro/badge.svg?branch=dev)](https://coveralls.io/github/AppCypher/Astro?branch=dev)
[![Maintainability](https://api.codeclimate.com/v1/badges/9739900850aeebc6b2d5/maintainability)](https://codeclimate.com/github/AppCypher/Astro/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/9739900850aeebc6b2d5/test_coverage)](https://codeclimate.com/github/AppCypher/Astro/test_coverage)
![Maintained](https://img.shields.io/maintenance/yes/2017.svg)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
#### Work in Progress :construction:
Current Version: 0.1.12
![astro screenshot](https://github.com/AppCypher/Astro/blob/dev/media/images/astro-syntax.png)

### What is Astro?
Astro is a multi-paradigm high-level programming language designed for high-performance numerical-computing web applications and as a result Astro
- is a statically-typed,
- compiles to WebAssembly,
- has no GC and
- has a syntax similar to [Python](https://en.m.wikipedia.org/wiki/Python_(programming_language)) with
- full type inference

### Why create yet another programming language?
SIMD, threads and direct access to Web APIs are planned for WebAssembly. These and the proposed GPU Compute standards will make the web a desirable HPC target in the near future.
While such web apps can be written in C/C++ or Rust, we believe Astro introduces some useful features that can make creation of those apps easier, quicker and less buggy.

Astro started as a hobby for learning programming language design and compiler construction but that has since changed when Astro started gathering a set of unique features that should make any level of development fun.

Astro is designed to have no runtime [Garbage Collector](https://en.m.wikipedia.org/wiki/Garbage_collection_(computer_science))(GC) as it is expected to be fast enough to develop games and other real-time software. 
It needs to do this while being as expressive as python.

In addition, Astro makes some design decisions that are intuitive for numerical computing applications. For example, it has builtin aupport for vectors and matrices, vectorization, unicode identifiers, etc. 

Astro is basically a high-level language with low-level access.

### Why compile directly to WebAssembly? Why not LLVM?
Compiling to LLVM IR brings with it some benefits. 
One is getting a free WebAssembly compilation step and the other is the provision of decade-worth optimization passes.
These are indeed valuable features, but wasm is an easier target to get started with. It is portable and runs on major JavaScript VMs, which means Astro can leverage the Nodejs ecosystem instead of building its own from scratch.

Astro compiler is also expected to be lightweight, fast and responsive, LLVM passes will add some major overhead to the compilation time. It is, however, important to note that compiling to LLVM will be considered in the future when the wasm backend is stable enough.

### What is Astro automatic memory management like? Rust's or Swift's?
Neither.
Astro uses a special [Automatic Reference Counting](https://en.m.wikipedia.org/wiki/Reference_counting)(ARC) system that automatically breaks reference cycles, so its unlike Swift's ARC which requires some special annotations in cases like that.
It's also unlike Rust memory management model as it puts lesser restrictions on how references can be moved around while still being memory safe.

Astro simply, stays out of your way, lets you write your code like you would in any other garbage-collected langauges.

### How close is Astro to being ready for production use?
Not close. Astro is at its infancy, there are several tasks —which you can find [below](#tasks)— to complete before it becomes usable.

For now, Astro can only compile its source code to ast format. It is not ready for even the simplest application.

### How will Astro tooling be like?
Astro is meant for interactive high-productivity usage therefore a visual REPL, for visualizing and introspecting different kinds of data, is planned.
It will also have a set of language tools for making editor support easier.

Incremental compilation is a goal as well since the language requires a lot of compile-time computations like type inference and program flow analysis.

### <a name="tasks"></a> What are the important tasks to complete?
- [x] ~Improve project structure~
- [x] ~Add automated unit testing and coverage reports~
- [x] ~Redesign and remove certain inconsistencies in language syntax~
- [ ] Complete parser implementation
- [ ] Implement basic semantic analysis
- [ ] Create ambiguity finders for inheritance, multiple dispatch, etc.
- [ ] Implement type inference and garbage collection using program flow analysis
- [ ] Add wasm code generation
- [ ] Incorporate incremental compilation
- [ ] Build REPL
- [ ] Create specialized error handler

### Technologies used
- [PEGjs](https://github.com/pegjs/pegjs) - a simple parser generator for JavaScript that produces fast parsers with excellent error reporting
- [wast2wasm](https://www.npmjs.com/package/wast2wasm) - translates from s-expressions to the WebAssembly binary-encoding.

### Other interesting new languages that compile to WebAssembly
- [Forest](https://github.com/forest-lang/core) - multi-syntax functional programming language
- [AssemblyScript](https://github.com/AssemblyScript/assemblyscript) - a new compiler targeting WebAssembly while utilizing TypeScript's syntax and node's vibrant ecosystem. 
- [Walt](https://github.com/ballercat/walt) - an alternative syntax for WebAssembly text format. It's an experiment for using JavaScript syntax to write to as 'close to the metal' as possible.

### Project folder structure
```
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── MVP.md
├── README.md
├── docs
│   ├── README.md
│   ├── compiler
│   │   ├── README.md
│   │   └── compiler-workings.ast
│   └── language
│       ├── README.md
│       ├── development.ast
│       ├── feature-proposals.md
│       └── summary.ast
├── media
│   └── images
│       └── astro-syntax.png
├── package-lock.json
├── package.json
├── samples
│   ├── README.md
│   ├── fibonacci
│   │   └── fibonacci.ast
│   ├── fizzbuzz
│   │   └── fizzbuzz.ast
│   ├── hello-world
│   │   └── hello-world.ast
│   ├── miscellaneous
│   │   └── preview.ast
│   ├── normalize
│   │   └── normalize.ast
│   ├── product
│   │   └── product.ast
│   ├── sum
│   │   └── sum.ast
│   ├── vectorized
│   │   └── vectorized.ast
│   └── wordcount
│       └── wordcount.ast
├── src
│   ├── compiler
│   │   ├── README.md
│   ├── stdlib
│   │   └── README.md
│   └── support
│       ├── README.md
│       └── editors
│           ├── sublime-text
│           │   └── astro.sublime-syntax
│           └── vscode
│               ├── CHANGELOG.md
│               ├── README.md
│               ├── language-configuration.json
│               ├── package.json
│               ├── syntaxes
│               │   └── astro.tmLanguage.json
│               ├── tsconfig.json
│               └── vsc-extension-quickstart.md
└── tests
    ├── README.md
    ├── compiler
    │   ├── codegen
    │   ├── semantics
    │   ├── syntax
    │   │   ├── declarations.spec.js
    │   │   └── misc.spec.js
    │   └── utils
    │       └── utils.spec.js
    └── samples
        └── fibonacci.spec.js
```

#### Do you have an unanswered question?
Please [open an issue](https://github.com/appcypher/astro/issues/new) and ask questions, offer to help, point out bugs or suggest features.
