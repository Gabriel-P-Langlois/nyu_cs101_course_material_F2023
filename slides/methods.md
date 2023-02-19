---
layout: presentation
title: Methods
permalink: /slides/methods/
---

class: center, middle

# Methods

> "Take a method and try it. If it fails, admit it frankly, and try another. But by all means, try something."
>
> -[Franklin D. Roosevelt](https://en.wikipedia.org/wiki/Franklin_D._Roosevelt)

---

# Agenda

1. [Overview](#concept)
1. [Simple Methods](#simple)
1. [Parameters & scope](#parameter-scope)
1. [Overloading](#overloading)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview

## Concept

A **method** is a reusable sequence of statements that have been grouped
together under the same name.

--

Put another way, a method is a modular reusable block of code.

--

Methods make it easier to debug your code. In addition, they allow you to hide the details
of a method from the user (hiding complexity). This is called **information hiding**.

---

template: overview

## Concept

The following terms are useful when learning about methods:

--

- The **caller** is one who invokes a method.
- Invoking a method using its name is known as **calling** that method.
- You can pass information to a method by using **arguments**.
- When a method completes an operation, it **returns** to its caller.
- A method can pass information to the caller by **returning a result**.

--

A few more notes:

- The control flow of a program can easily switch to code within a method from anywhere else in the code.
- Calling a method is a form of unconditional branching - disrupting the 'usual' flow of a program.
- Once the control flow reaches the end of an invoked method, the control flow returns to the line of code from which it originally branched.

---

name: simple

# Defining methods

--

template: simple

Syntax:
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

Consider the following method for computing the maximum of two integers:

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

You can store values returned by methods inside variables. 
- E.g., `int n = max(2,19);`

Methods of type void can be used like statements. 
- E.g., `System.out.println(“Hello World”);`

Note: Once the method invocation completes, any local variables, including parameters, are wiped out of memory.

--

An **Activation Record** is information about a method that contains values of parameters and local variables. 

When a method is called, this Activation Record is stored in a location on memory known as a **stack**.


---

name: parameter-scope

# Passing parameters and scope

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

template: parameter-scope

## Understanding scope

What is the output of the following code?

```java
public class Increment{
    public class static void main(String[] args) {
    int x = 1;
    System.out.println("Before the call, x is " + x");
    increment(x);
    System.out.println("After the call, x is " + x");
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

---

template: overloading

Same name but different argument types:
```java
void sum(int a,int b) {
    System.out.println(a+b);
}

void sum(double a,double b) {
    System.out.println(a+b);
}
```

--

Note: A method cannot be overloaded by changing the return type of method.
- This will confuse the compiler and cause compilation errors.

---

name: conclusions

# Conclusions

--

You now have a basic understanding of methods in Java.

--

Upcoming deadlines + Info:
- Homework 2 is due today at 3 pm.
- Quiz 4 is due today at 11:59 pm.
- Quiz 5 will be posted today and due this coming Friday at 11:59 pm.
- Homework 3 will be posted on **Thursday** and due a week after.
