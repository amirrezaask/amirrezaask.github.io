---
title: "My journey into compilers: Part 1"
date: 2022-08-05T21:56:47+04:30
draft: false
toc: true
images:
tags:
  - rustlang
  - rust
  - compilers
---

# Intro
From day 1 of my journey into programming, compilers were magical to me, programs that can get something we humans understand and produce 1s and 0s that computers understand.
Ofcourse that's not completely true but it was what I thought back then. So for a long time I was testing and looking at new compilers and new languages when they came out to see what ideas they brought to the table, and one day I decided to make my own, my language, my syntax, my set of features and most important my compiler.

So like all personal pet projects I created a repo chose a random name(loki) and started my research in compilers.

At first I had to chose what will my compiler generate when given a source file, you can emit another langauge let's say C or JS, you can emit LLVM-IR, you can emit JVM bytecode or CLR bytecode and most complicated one you can emit native code for CPU.
Each approach has its own pros and cons which I will discuss briefly:

1. Generating another langauge like C/C++ or JS is probably simplest one and actually in most cases best one to start with, since you are generating something that is still readable and also still high level and you have access to target langauge ecosystem in your langauge so for example for printing you just use "stdio.h" and you don't need to have your own version of print.

2. Generating some low level byte code like code, something like JVM bytecode or CLR bytecode or LLVM IR. This approach is really good cause forexample in case of JVM
you have access to all Java ecosystem and you also generating something more lowlevel and cause of that you can do some fun things with your output and basically adding new features to your langauge that do not necessarily map to a langauage construct in Java, forexample implementing some thing like `defer` keyword which java does not have. You can do this in approach 1 as well but it's simpler here and you know this approach feels more like a "real" compiler anyway.

3. Generating CPU instructions for a target architecture let's say x86/64. This one is the hardest one and I really don't think you should do it unless you want to get really down the stack, because even if you want fastest code approach 2 will generate faster code than yours probably.


Cause I wanted to just have fun and wanted to have a working thing ASAP I went with approach 1.


## Compiler Phases
You can see a compiler as a set of pure functions that get some input and produce some output. Of course for performance reasons most compiler phases are not pure and are convoluted in each other but for simplicity let's see them like that.

1. Frontend
   1. Lexer ( tokenizer ): This step gets your source code and generates stream of tokens.
   2. Parser: this step gets the stream of tokens you produced and will generate an AST out of that.
2. Analyzers
   1. Type Checker/Type Inference: Every static type language does a type checking phase where it will look at AST to see if everything in terms of types make sense, we elaborate on this later. also modern compilers will do type inference where they can guess type of things in your AST and modify the AST and add necessary type information to that.
   2. Semantic Analyzer: this step checks your AST for correct usage of stuff, forexample checks that if you have a `continue` stmt, it should be inside a `for` or `while` otherwise it's an error, this step really depends on your language and syntax.

3. Optimizer (optional): you can skip this step if you want to go with approach 1 or 2 because most of the times the target platform will do this for you but if you want this there are various optimizations that we will talk on later.
   
   
4. Target Code Gen: This is the final step that will get the modified AST/IR and generate output code from it.


I hope you liked this so far, stay tuned for next chapters that we elaborate on each phase.

