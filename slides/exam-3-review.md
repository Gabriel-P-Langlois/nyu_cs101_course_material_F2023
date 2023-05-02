---
title: Exam 3 Review
permalink: /slides/exam-3-review/
---

class: center, middle

# Exam 3 Review

Intro to Computer Science

---

# Agenda

1. [Exam Structure](#structure)
1. [Prior Knowledge](#prior-knowledge)
1. [Inheritance](#inheritance)
1. [Polymorphism](#polymorphism)
1. [Interfaces](#interfaces)
1. [Abstract Classes](#abstract-classes)
1. [Exceptions and Errors](#exceptions)
1. [Recursion](#recursion)
1. [Conclusions](#conclusions)

---

name: structure

# Structure

--

The exam will take place on Monday, May 15th in CIWW 101 from 8:00-09:50 am. It will be composed of three parts:

Multiple choice, True/False and Multiselect questions (~30%)

- About 15 questions from quizzes 9 and 10 (Exceptions and Abstract Classes and Interfaces)
- About 15 questions from quizzes 1-8.

One short answer question (~10%) about exception handling.
- E.g., Create your own exception class (by extending the Exception class).
- Given a public class with a user defined method and a main method, show me how 1) you can handle the exception at the level of the user defined method and 2) you can handle the exception in the main method.

---

template: structure

Written programming questions (~60%)

- One question about OOP \w Abstract Classes. E.g., I give you the UML Class diagram of an abstract class and a child class that extends it. Write those classes.
- One question about OOP \w Interfaces. E.g., I give you the UML Class diagram of one or two interfaces and a child class that implements either or both. Write said classes.

Note: The written programming questions will be designed to test your understanding of

- Method overloading
- Method overriding
- Abstract classes, abstract methods, default methods
- Inheritance
- Polymorphism

One short bonus question on recursion (+5%)

---

name: prior-knowledge

# Prior Knowledge

--

## Cumulative by nature

By nature of the material, the exam will include what was tested previously. So you would be wise to brush up:

- Java Exam 1 Review
- Java Exam 2 Review

---

name: inheritance

# Inheritance

--

## Overview

We now know there are multiple types of inheritance in Java:

- inheritance from a class
  - concrete classes
  - abstract classes
- inheritance via interfaces
  - a class can implement more than one interface
  - interfaces can pass on both abstract and default methods

---

name: polymorphism

# Polymorphism

--

## Overview

The reference to an object is of a different type than the object's declared type.

```java
Mammal barstein = new Human("Foo", "Barstein");
```

---

template: polymorphism

## Reference types

Polymorphic references can be of:

- an ancestor class type
- an interface type

Polymorphic references can not be of:

- a child class type

---

template: polymorphism

## In practice

In practice, polymorophism is applied to process a bunch of objects that share a common ancestor. We place those various objects into some sort of collection (array, ArrayList, etc) that is typed as the ancestor class or interface that all the objects share in common.

```java
//say you have a bunch of Mammals
Mammal[] mammals = {
    new Human("Foo", "Barstein"),
    new Dog("Fido"),
    new Mouse("Minnie")
};

//do some kind of batch process on all these Mammals
for (Mammal mammie : mammals) {
//do some things all Mammals can do, regardless of their declared type
mammie.tickle();

    //do some things only a particular declared sub-type of Mammal can do
    if (mammie instanceof Dog) {
        ((Dog) mammie).bark();
    }

}
```

---

name: interfaces

# Interfaces

--

## Overview

Interfaces are a reference type that provide a form of inheritance, similar to classes, but with some key differences in purpose and implementation.

---

template: interfaces

## Raison d'être

Interfaces are used to impose a contractual obligation on classes that they implement a particular set of methods with specific signatures. Why might this be useful?

---

template: interfaces

## Limitations

Interfaces can contain only:

- static constants
- static methods
- abstract methods
- default methods

All methods and properties in an interface are public.

In what case are default methods useful?

---

name: abstract-classes

# Abstract classes

--

## Overview

Like interfaces, abstract classes can contain abstract methods and provide a form of inheritance. In what cases are abstract classes preferable to interfaces? To concrete classes?

---

template: abstract-classes

## Raison d'être

In what case are abstract classes preferable to interfaces?

---

template: abstract-classes

## Limitations

Unlike interfaces, abstract classes can contain any sorts of properties and methods. Thus, they are in many ways similar to concrete classes. However...

--

Unlike concrete classes, abstract classes...

- can contain abstract methods
- can not be instantiated

---

name: exceptions

# Exceptions and Errors

--

## Errors

Errors are irremediable failures that are usually due to external factors outside the scope of your code

- stack overflow
- running out of memory
- hard drive problems
- database problems

---

template: exceptions

## Exceptions

Exceptions represent known problematic situations that can potentially be handled in code by one of two means:

- `throws` declaration
- `try`/`catch`

Exceptions are represented in code as objects of various classes that extend Exception class.

---

name: recursion

# Recursion

--

## Overview

Methods that invoke themselves. A form of iteration, but different from loops.

---

template: recursion

## Classic examples

The classic pattern: handle the base case, and then recurse on the remainder. Examples:

- Fibonacci numbers
- Computing powers
- Counting digits
- Flipping strings backwards
- Linear search
- Fractal images

---

template: recursion

## Termination

The recursion must terminate somehow in order not to trigger a stack overflow error. How does it stop recursing?

---

name: conclusions

# Conclusions

I'll provide supplementary exercises and practice questions to help you prepare for the exam.

For now, start with this:
- [Java Programming Tutorial (ntu.edu.sg)](https://www3.ntu.edu.sg/home/ehchua/programming/java/j3f_oopexercises.html#zz-6): Exercises 6.1 to 6.8.
- [Linuxtopia](https://www.linuxtopia.org/online_books/programming_books/thinking_in_java/TIJ311_024.htm): Exercises 1 to 3.

