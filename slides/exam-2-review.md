---
layout: presentation
title: Exam 2 Review
permalink: /slides/exam-2-review/
---

class: center, middle

# Exam 2 Review

Intro to Computer Science

---

# Agenda

1. [Exam Structure](#structure)
1. [Multidimensional Arrays](#multidimensional-arrays)
1. [Object-Oriented Programming](#oop)
1. [Pillars](#pillars)
1. [Patterns](#patterns)
1. [Strings](#strings)
1. [Inheritance](#inheritance)
1. [This is Super](#this-super)

---

name: structure

# Structure

--

## Overview

The exam will take place during class time. It will be composed of two parts:

1. Multiple choice, True/False and Multiselect questions (50%)
1. Two written programming questions (%50), one on multidimensional arrays and one OOP implementation question.

---

name: multidimensional-arrays

# Multidimensional Arrays

--

## Main themes

- You must first understand one-dimensional arrays
- Two-dimensional arrays can be visualized as tables with rows and columns
  - first dimension is like the rows
  - second dimension is like the columns
- Declaring, allocating, and assigning values
  - Using syntactic sugar
  - Without using syntactic sugar
- Looping through multi-dimensional arrays
  - the 'standard' way using nested counter-based loops
  - using the **foreach** type of loop (e.g. `for (String[] val : values) { /* ... */ }`)
- Ragged arrays exist
  - Declaring ragged arrays with syntactic sugar
  - Declaring ragged arrays without syntactic sugar
- Passing arrays as arguments to methods

---

name: #oop

# Object-Oriented Programming

--

## Main themes

Basic object-oriented programming

- Classes are essentially custom data types.
- Classes are reference types in Java.
- Objects are instances of a class.
- Defining a class...
- Constructors...
- Instance methods and properties...
- Static methods and properties...
- Instantiating an object...

---

name: pillars

# Pillars

--

## Main themes

The **4 pillars** of object-oriented programming theory:

- abstraction
- encapsulation
- inheritance
- polymorphism

---

name: patterns

# Patterns

--

## Main themes:

- `private` for instance properties and methods
- getters and setters to provide public access for `private` properties, where desired
- perform validation in setters
- always use those setters, even within the same class file
- overloaded methods and contructors provide multiple variants of the same action
- `static` for shared properties and methods
- `final` for values that never change
- inheritance

---

name: strings

# Strings

--

## Main themes:

- `String` is a class in the Java API, not a fundamental primitive data type.
- because different objects are stored at different locations in memory, compare the value of two `String` objects with its custom `.equals()` method, not `==`.
- `String` is designed following the principle of object-oriented abstraction (e.g. `.length()` rather than `.length`)
- Encapsulated within every `String` is a `char` array.
- Because `String` has been designed to be immutable and quite limited, a variety of helper classes exist to work around that (e.g. `StringBuilder`, Apache Commons Lang's `StringUtils`, etc)

---

name: inheritance

# Inheritance

--

## Main themes:

- Child classes inherit properties and methods of parent classes, except...
  - `private` properties and methods are not inherited...
  - ...but `private` properties are still accessible via any inherited `public` getters and setters
  - constructors are not inherited, but are accessible via the `super` keyword
- use of the `super` keyword to refer to code belonging to the parent class

---

template: inheritance

## Polymorphism

Polymorphism goes hand-in-hand with inheritance.

- child objects can be considered to be of their parent class.
- e.g., if `B` inherits from `A`, then a `B` object can be referred to as both a `B` and an `A` object.
- can be useful when storing objects of a variety of child types into a single array typed as the parent type.
- that allows you to easily loop through them all.
- `typeof` operator allows you to check whether an object is of a given type.

---

name: this-super

# This is Super

--

## Main themes:

- the `this` keyword, when used within a method, refers to the object upon which that method was called.
- you cannot use the `this` keyword within a `static` method, since that method can never be called on an object.
- the `super` keyword, when used within a method, refers to code in the parent class.
- a call to the parent class's constructor can be added to a child class constructor, if useful (e.g. `super()` or `super(someArgs)`

---

name: practice-problems

# Practicing for the midterm:

Please attempt some of the following exercises on this [website]{https://www3.ntu.edu.sg/home/ehchua/programming/java/j3f_oopexercises.html#zz-4}: 1.1 to 1.9.
Being able to implement a public class from a Unified Modeling Language (UML) diagram is **crucial**.

---

# Practicing for the midterm:
Complete the following program. The program must grades the test and displays the result. It compares each student's answers with the key, counts the number of correct answers, and displays it.

```java
public class GradeExam {
  /** Main method */
  public static void main(String[] args) {
  // Students' answers to the questions
  char[][] answers = {
    {'A', 'B', 'A', 'C'},
    {'D', 'B', 'A', 'B'},
    {'E', 'D', 'D', 'A'},
    {'C', 'B', 'A', 'E'}};
  
  // Key to the questions
  char[] keys = {'D', 'B', 'A', 'C'};
  
  // Grade all answers
  // COMPLETE
  
  }

}
```
