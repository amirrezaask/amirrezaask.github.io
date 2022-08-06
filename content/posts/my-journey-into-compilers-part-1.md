---
title: "My journey into compilers: Part 1"
date: 2022-08-05T21:56:47+04:30
draft: false
toc: true
images:
tags:
  - untagged
---
From day 1 of my journey into programming, compilers were magical to me, programs that can get something we humans understand and produce 1s and 0s that computers understand.
Ofcourse that's not completely true but it was what I thought back then. So for a long time I was testing and looking at new compilers and new languages when they came out to see what ideas they brought to the table, and one day I decided to make my own, my language, my syntax, my set of features and most important my compiler.

So like all personal pet projects I created a repo chose a random name(loki) and started my research in compilers.

At first I had to chose what will my compiler generate when given a source file, you can emit another langauge let's say C or JS, you can emit LLVM-IR, you can emit JVM bytecode or CLR bytecode and most complicated one you can emit native code for CPU.
Each approach has its own pros and cons which I will discuss briefly:

- Generating another langauge like C/C++ or JS is probably simplest one and actually in most cases best one to start with, since you are generating something that is still readable and also still high level and you have access to target langauge ecosystem in your langauge so for example for printing you just use "stdio.h" and you don't need to have your own version of print.