---
layout: presentation
title: Methods
permalink: /slides/methods/
---

class: center, middle

# Methods

---

# Agenda

1. [Overview](#concept)
1. [Simple Methods](#simple)
1. [Parameters & scope](#parameter-scope)
1. [Overloading](#overloading)
1. [Concept: Stepwise refinement](#method-abstraction1)
1. [Concept: Method abstraction](#method-abstraction2)

---

name: overview

# Overview

---

template: overview

## Concept

A **method** is a block of statements that has a name and can be executed by 
invoking it from some other place in your program.

--

Put another way, a method is a modular reusable block of code.

--

Methods make it easier to organize and debug your code. 

--

In addition, methods allow you to hide the details
of a method from the user (hiding complexity).

---

template: overview

## Concept

Technical terms pertaining to methods:

--

- The **invoker** is one who invokes a method.
- Invoking a method using its name is known as **invoking** that method.
- You can pass information to a method by using **arguments**.
- When a method completes an operation, it **returns** to its caller.
- A method can pass information to the caller by **returning a result**.

--

Invoking a method is a form of `unconditional branching`:

- The control flow of a program can switch to code within a method from anywhere else in the program.
- Once the control flow reaches the end of an invoked method, the control flow returns to the line of code from which it originally branched.

---

name: simple

# Defining methods

--

template: simple

Here's the syntax of a method:

```java
scope returnType methodName(list-of-parameters) {
    // method body
}
```

--

**Scope** specifies who has access to the method.

**returnType** can be any data type or void. Void methods do not return a value.

**methodName** is the name of the method.

**List-of-parameters** is a comma separated list of parameters written as type1
var1, type 2 var 2....This may also be just one parameter if a list is not required.


---

template: simple

Here's a method for computing the maximum of two integers:
```java
public static int max(int num1, int num2){
    // method body is below
    int result;
    
    if (num1 > num2){
        result = num1;
    else
        result = num2;
    }
    return result;  // returned value
}
```

--

- The method header is `public static int`.
- The scope is specified by `public static` (more on this later in the course).
- `int` is the return type
- `max` is the method name.
- `num1` and `num2` are the formal parameters.
- `max(int num1, int num2)` is the method signature.
- You return a value from a method by including a `return` statement.

---

template: simple

Calling the method means executing the code contained within the method. 

The previous method can be called into the `main` method.

--

You can store values returned by methods inside variables. 
- E.g., `int n = max(2,19);`

--

Methods of type void can be used like statements. 
- E.g., `System.out.println(“Hello World”);`

---

name: parameter-scope

# Passing parameters and scope

---

template: parameter-scope

## The concept of Scope

**Important**: Once the method invocation completes, any local variables, including parameters, are wiped out of memory.

--

<br />

<div align="center">
<span style="color: red;"> **Live demonstration**</span> </div>

--

An **Activation Record** is information about a method that contains values of parameters and local variables. 

When a method is called, this Activation Record is stored in a location on memory known as a **stack**.

---

template: parameter-scope

## Understanding scope

What is the output of the following code?

```java
public class Increment{
    public static void main(String[] args) {
    int x = 1;
    System.out.println("Before the call, x is " + x);
    increment(x);
    System.out.println("After the call, x is " + x);
    }
    
    public static void increment(int n) {
        n++;
        System.out.println("n inside the method is " + n);
    }
}
```

---

template: parameter-scope

## Understanding scope

**Scope** – This determines who has access to a method (where it can be referenced and used).

**Local Variable** – This scope allows variables to be used only where they are declared. 
- If a variable is declared inside a method, it may only be used within that method.

**Block Scope** – This scope allows variables to be used only within a block of code. 
- In this instance, a variable is declared within a block of code and may only be used within that block.


---

template: parameter-scope

## Understanding scope

Example 1:
- When the code blocks are not nested, the variable name can be reused.

```java
public static void main(String[] args) {
    ...
    {
        int x = 5;
        System.out.println("The value of x is " + x);
    }
    {
        int x = 7;
        System.out.println("The value of x is " + x);
    }
...
}
```

---

template: parameter-scope

## Understanding scope

Example 2:
- When the code blocks are nested, the variable name cannot be reused.

```java
public static void main(String[] args) {
    ...
    {
        int x = 5;
        System.out.println("The value of x is " + x);
        {
            int x = 7;
            System.out.println("The value of x is " + x);
        }
    }
...
}
```

---

template: parameter-scope

## Passing parameters to methods

When you call a method, the arguments **must** match the list of parameters from the method definition
in **order**, **number**, and **variable type**.

--

Consider a method whose header is `public int onePlusOne(int num1, int num2, String s)`

To call this method, you must do the following:

--

- Insert integers for num1 and num2, and a string for s.
- Insert the correct number of variables.
- You must also enter the parameters in the correct order.

Anything else yields an error!

---

template: parameter-scope

## Calling methods within methods

Methods can call other methods.

The order is determined by the control flow of the program.

- Each method invocation creates a new 'stack frame' - an area of memory dedicated to the newly invoked method.

- The Java interpreter is only ever looking at the method invocation at the top of the stack - the most recently invoked method.

- Once a method that has been invoked completes, its stack frame is popped (deleted) from the call stack and its memory is wiped clean.

---

name: overloading

# Overloading

---

template: overloading

Java allows multiple methods with the same name but different parameter sets. These are called **overloaded methods**.

--

Same name but different number of arguments:
```java
void sum(int a,int b) {
    System.out.println(a+b);
}

void sum(int a,int b, int c) {
    System.out.println(a+b+c);
}
```

--

Same name but different argument types:
```java
void sum(int a,int b) {System.out.println(a+b);}

void sum(double a,double b) {System.out.println(a+b);}
```

--

A method cannot be overloaded by changing the return type of method!

---

name: method-abstraction1

# Concept: Stepwise refinement

---

template: method-abstraction1

How should we write a large computer program? 

--

**Stepwise refinement** refers to the progressive refinement in small steps of a program specification into a computer program.

--

This is sometimes called **top-down design**.

--

You do not have to think about the code at first. 
You can outline the problem, find a logical deconstruction, and write your code.

---

template: method-abstraction1

![Task decomposition](../files/task_decomposition.png)

---

name: method-abstraction2

# Concept: Method abstraction

---

template: method-abstraction2

Methods are useful for stepwise refinement because they let us break a large task into simpler parts.

--

An important related concept is that of *method abstraction*.

--

**Method Abstraction**: Write the method, write its documentation, and 'hide' (abstract away) its implementation. 
The method is 'hidden', but anyone can use the method as long as you have the method signature (name and parameter list), the return type and the documentation. 

--

The author can make edits to the method as long as the header of the method remains the same.

---

template: method-abstraction2

We've already seen this in action!

--

For example, take our HelloNYU.java program:

```java
public class HelloNYU{
    public static void main(String[] args) {
    System.out.println("Hello NYU!");
}
```

--

The statement 'println()' is a method. Do we need to see its implementation to use it?

---

name: method-abstraction3

# Decomposition

---

template: method-abstraction3

Decomposing a large task is a subtle process in software engineering.

--

A good decomposition strategy avoids spreading or increasing complexity.

--

Generally, each level in the decomposition should take responsibility for certain
details and avoid pushing that responsibility to higher levels.

--

In Java, methods are useful for this. But the top-down design is useful outside of programming, too.

--

Interesting example: [Edgar Allan Poe's top-down design of the "Raven"](https://www.youtube.com/watch?v=GiDI2JH3_zk&embeds_referring_euri=https%3A%2F%2Fwww.cs.cornell.edu%2F&source_ve_path=MjM4NTE&feature=emb_title)
