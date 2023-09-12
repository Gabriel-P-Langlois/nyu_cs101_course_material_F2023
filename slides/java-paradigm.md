---
layout: presentation
title: The Java Paradigm
permalink: /slides/java-paradigm/
---

class: center, middle

# The Java Paradigm

"Write once, run anywhere"

---

# Announcements

The tutoring sessions schedule for this semester has been posted. Go on Brightspace, click the the Schedule + Lectures tab,
and click the link above the schedule table.

Quiz 1 is online -- you have plenty of time to finish it (two days after the add/drop deadline).

Assignment 1 will be posted next week on the 19th.

---

# Agenda

We'll talk a bit more about computers and programming.

1. [Computers](#computers)
2. [Programming](#programming)
3. [Machine code](#machine-code)
4. [Assembly languages](#assembly)
5. [High-level languages](#high-level-languages)
6. [Compiling](#compiling)
7. [Interpreting](#interpreting)
8. [Java](#java)
9. [Setting up Git Bash for VSC](#git)

---

name: computers

# Computers

---

template: computers
name: computers-1

## Definition

A computer is any device, entity, or object that can perform computations.

--

- [human computers](https://en.wikipedia.org/wiki/Computer_%28job_description%29)

--

- [mechanical computers](https://en.wikipedia.org/wiki/Mechanical_computer)

--

- [electronic computers](https://en.wikipedia.org/wiki/Computer#Digital_computers)

--

- [biological computers](https://en.wikipedia.org/wiki/Biological_computing)

--

- [quantum computers](https://en.wikipedia.org/wiki/Quantum_computing)

---

name: processor

# Processor

--

The processor is the part of an electronic computer that does the computation.

--

A processor can...

--

- jump to a particular location in memory

--

- read a number from [Random-Access Memory](https://en.wikipedia.org/wiki/Random-access_memory) (RAM)

--

- save a number to RAM

--

- add two numbers together

--

- compare two numbers to see which is larger

--

- send a number to a particular device (e.g., a monitor)

--

- receive a number from a particular device (e.g., a keyboard)

--

Note: **Every** statement in a computer program is reduced to a sequence of these processor actions!

---

name: programming

# Programming

---

template: programming
name: programming-1

## Purpose

> Computer programming is the process of writing an executable computer program to accomplish a specific computing result.
>
> -[Wikipedia](https://en.wikipedia.org/wiki/Computer_programming)

---

template: programming
name: programming-2

## Levels of abstraction

Programmers have established increasingly higher levels of abstraction in order to make programming faster and more intuitive.

--

### Low level:

- Machine languages
- Assembly languages

--

### High level:

- High-level programming languages
- [Visual programming](https://en.wikipedia.org/wiki/Visual_programming_language)

---

name: machine-code

# Machine code

--

## Binary instructions

At the lowest level, a program directly informs a computer what it should do by sending binary instructions to the processor.

--

Example of a set of machine instructions for an x86 processor to move the number 97 to the AL memory register:

```
10110000 01100001
```

--

The number `1011` is the machine's instruction to do a move operation, `0000` is the address of the AL register, and `01100001` is the number `97` written in binary.

--

Each family of processors is designed to "understand" particular binary numbers to mean particular operations.

---

name: assembly

# Assembly languages

---

template: assembly
name: assembly-1

## Mnemonics

It's easier to memorize words than binary numbers. 

--

Assembly languages provide mnemonics that a programmer can write, which are converted to machine language.

--

Example of a set of assembly instructions for an x86 processor to place the number 97 in the memory register called AL:

```
MOV AL, 61h
```

--

`MOV` is a mnemonic for `1011`, `AL` is a mnemonic for `0000`, and `61` is the number `97` written in hexadecimal notation.

---

template: assembly
name: assembly-4

## Assembling

Converting code written in assembly language to the equivalent machine language is known as **assembling**.

It's essentially a search/replace operation where mnemonics are replaced with their machine code equivalents.

--

The program to do so is called an **assembler**.

---

name: high-level-languages

# High level languages

---

template: high-level-languages
name: high-level-languages-1

## Abstraction

High-level languages are designed to be more intuitive.

The written code is further abstracted away from the machine instructions the processor will ultimately execute.

---

template: high-level-languages
name: high-level-languages-2

## Example

Storing the number 97 in a memory register using the C programming language:

```c
register int i = 97;
```

--

Other high-level programming languages include C, C++, C#, Java, Python, Ruby, Scratch, Javascript, and PHP. All offer higher-level capabilities, such as looping, functions, branching, etc.

---

template: high-level-languages
name: high-level-languages-4

## Translation to machine code

Converting code written in a high-level language to the equivalent machine code is done via one of two processes:

- compiling
- interpreting

---

name: compiling

# Compiling

--

## Concept

Code written in a high-level programming language is translated to its machine code equivalent all at once.

--

- A tool called a **compiler** reads the code, analyzes it, and outputs a file with the required machine code instructions.

--

- It can be time-consuming.

--

- Once compiled, the code can be executed efficiently.

--

- Many errors can be detected during compilation.

--

- Compilation is processor-specific.

---

template: compiling
name: compiling-5

## C language

The C programming language is a classic example of a compiled language.

--

- There are different compilers to translate C to machine code for each popular processor family.

--

- The high-level source code must be tweaked to match the features of the target processor before being compiled.

--

- It is not very portable...

--

- ...but it is fast!

---

name: interpreting

# Interpreting

--

Code written in a high-level programming language is translated to its machine code equivalent _and executed_ as a series of small steps.

--

- A tool called an **interpreter** reads one statement of high-level code at a time, converts it to its machine code equivalent, and immediately executes that machine code.

--

- It starts running immediately.

--

- It is not necessarily efficient since it only looks at one statement at a time.

--

- It does not always identify errors in statements that have not yet been interpreted.

---

name: java

# Java

--

## Write once, run anywhere

Unlike C code, Java source code is highly portable and executable on machines with almost any processor. How is this possible?

--

- Java is both compiled and interpreted.

--

- Java high-level source code is compiled to **byte code**.

--

- Java byte code is then interpreted to machine code by one of the **Java Virtual Machines** (JVM)

--

- JVMs are created for most processor families.

--

- Thus, Java byte code is highly portable.

--

- This is the **Java paradigm**!

---

template: java
name: java-8

## Write once, run anywhere

![The Java paradigm](../files/java_paradigm.png)

---

template: java
name: java-9

## Byte code and the JVM

Byte code is somewhere between machine code and a high-level source in abstraction - an _intermediate-level_ language.

--

- The Java Virtual Machines are virtual computers (a software simulation of a physical computer) that are designed to view byte code as their native machine code.

--

- These JVMs contain interpreters that can translate this byte code to the appropriate machine code for whichever physical processor they are actually running on.

--

- Any programming language that can be compiled Java byte code can run in a JVM... Groovy, Kotlin, and Scala are popular high-level languages with different syntax from Java that take advantage of this.

---

name: git
template: git

## What to do for the next class: Install Git Bash

Get git [for Mac](https://git-scm.com/downloads) or [Git for Windows](https://gitforwindows.org/).

Git for Windows additionally comes with Git Bash, which gives Windows users a UNIX-like command shell.

**Windows users**: You should use Git Bash or Windows Subsystem for Linux (WSL) rather than Windows' default Powershell or other command line shell program. To set Git Bash as the default terminal shell within Visual Studio Code, **follow** the instructions in [the second answer here](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal) by **Mahade Walid** and edited by **FruityOatyBar** (ignore the first answer, which is outdated).

Mac users already have a UNIX command shell in the Terminal app.
