---
layout: presentation
title: Inheritance & Polymorphism
permalink: /slides/inheritance/
---

class: center, middle

# Inheritance & Polymorphism

---

# Agenda

1. [Overview](#concept)
1. [Basic Implementation](#implementation)
1. [Multi-Level Inheritance](#multi-level)
1. [Polymorphism](#polymorphism)
1. [Similarity & Difference](#difference)
1. [Is Inheritance Evil?](#evils)

---

name: overview

# Overview

--

## Concept

**Inheritance** is the mechanism of basing an object or a class on another object or class, retaining a similar implementation.

--

The properties and methods of one object or class are "passed down" automatically to the objects or classes that inherit from it.

---

template: overview

## Benefits

The touted benefits of inheritance include:

- Code reuse

- Less code redundancy

- Easier code maintenance

- Conceptual clarity

--

However, this is a controversial topic! See, e.g., this [link](https://codeburst.io/inheritance-is-evil-stop-using-it-6c4f1caf5117).

---

name: implementation

# Basic Implementation

--

## Abstract Example

Imagine we had the following class, `A` with just a single property, `message`, and its `getter` and `setter` methods.

```java
public class A {
    // no-args constructor
    public A() {
        System.out.println( "A new A object is born!" );
        this.message = "Hello!";
    }

    // just one property to keep it simple
    private String message;

    // getter + setter methods
    public String getMessage() {
        return this.message;
    }
    public void setMessage(String message) {
        if (msg.length > 0) this.message = message;
    }
}
```

---

template: implementation

## Abstract Example (continued)

Another class, `B`, inherits the properties and methods of `A` using the `extends` keyword.

```java
public class B extends A {

}
```
--

- A `B` object is instantiated with no further code and automatically inherits the public interface defined by `A`.

```java
B bObj = new B();
System.out.println( bObj.getMessage() );
```

---

template: implementation

## Abstract Example (continued)

We often create UML diagrams indicating class relationships, where the arrow points from parent to child.

![Class inheritance UML diagram](../files/oop-inheritance-simple.png)

--

In almost all cases, the child class contains its own additional properties and methods that make it different in some way from the parent... We have kept class `B` blank just to focus on the inherited properties and methods.

---

template: implementation

## Abstract Example (continued)

When this program is run, two lines are output:

```
A new A object is born!
Hello!
```

--

The first line above, '_A new A object is born!_' is output by the `A` class's constructor function, which our code does not explicitly call.

---

template: implementation

## Abstract Example (continued)

All classes, including our `B` class, are given a default **no-args constructor** by Java if no other constructor is defined.

--

This no-args constructor automatically calls **super()**. Note that if we were to write this constructor for `B` ourselves, it would look like:

--

```java
public B() {
        super();
}
```

The **super** keyword is a reference to the code in the parent class.

---

template: implementation

## Abstract Example (continued)

The second line output above, '_Hello!_', is a result of the call to the `B` object's `getMessage()` method.

- This method, like all other **public properties and methods**, is inherited from the parent class, `A`, into the child class, `B`.

- **Private properties and methods** are not inherited by a child class, but can be accessed through public getter and setter methods.

---

template: implementation

## Visibility

By definition, the _private_ property, `message`, of the `A` class is not visible from the `B` class.

- Yet, the `A` class's getter for that property, `getMessage()`, is public and thus is visible from within the `B` class.

---

name: multi-level

# Multi-Level Inheritance

## Concept

We can continue our example by giving `B` its own child, `C`.

```java
public class C extends B {

    // a no-args constructor
    public C() {
      super(); // call B's no-args constructor
    }

    // an overloaded constructor that accepts a message
    public C( String message) {
        super(); // call B's no-args constructor
        System.out.println( "A new C object is born!" );
        this.setMessage( message );
    }
}
```

---

template: multi-level

## Concept (continued)

A UML diagram showing multi-class inheritance.

![Multi-class inheritance UML diagram](../files/oop-inheritance-multi.png)


---

template: multi-level

## Analysis

`C` is now a child of `B`, which itself is a child of `A`.

- All the **public** properties and methods of `A` are inherited by `B`.

- All the **public** properties and methods of `B`, including those inherited from `A`, are inherited by `C`.

- Thus, `C` implements the **public interface** of both `A` and `B`.

--

What would the following code output?

```java
C cObj = new C( "Welcome!!" );
System.out.println( cObj.getMessage() );
```

---

name: polymorphism

# Polymorphism

--

## Concept

An object or class can assume more than one 'shape'.

- In our example, a `C` object implements the public interfaces of `C`, `B`, and an `A`.

- We could say that our `C` object _is_ a `C` object, as well as a `B` object, and an `A` object.

--

It's possible to verify this in code using the `instanceof` operator.

```java
if (cObj instanceof C && cObj instanceof B && cObj instanceof A) {
    System.out.println("It's a C, B, and A object all-in-one!");
}
```

---

template: polymorphism

## Application

Polymorphism is when we want to store objects of different, but related, types into an array to perform some kind of batch operation on them.

```java
A[] myObjs = {
    new A(),
    new B(),
    new C("Welcome!!")
};

for (A myObj : myObjs) {
    String message = myObj.getMessage();
    System.out.println(message);
}
```

---

template: polymorphism

## Overriding

We often want to have child classes implement the instance methods defined in the parent class differently.

--

A child class can define methods with the same signatures as the instance methods in the parent class - this is called **[overriding](https://coderanch.com/wiki/659959/Overriding-Hiding)**.

--

- For example, each of our `A`, `B`, and `C` classes could contain different implementations of the `getMessage()` method.

- It is possible for a child class's overridden method to call the parent class's version of that same method.

- A child class can call any public method as defined in its parent class's code by using the keyword **super**, e.g.

```java
super.getMessage();
```

---

name: difference

# Similarity & Difference

---

template: difference

## Example classes

The parent class:

```java
public class A {
    public void doSomething() {
        System.out.println("An A object doing something.");
    }
}
```

--

The child class:

```java
public class B extends A {
    public void doSomethingDifferent() {
        System.out.println("A B object doing something *different*.");
    }
}
```

---

template: difference

## Similarity

Since `B` inherits from `A`, both classes **encapsulate** `A`'s `doSomething()` method.



- `doSomething()` can be called on any `A` object, since it is defined within the `A` class.

```java
A myA = new A();
myA.doSomething();
```



- and it can be called on any `B` object, since `B` objects inherit it.

```java
B myB = new B();
myB.doSomething();
```

---

template: difference

## Similarity (continued)

Both `A` and `B` objects can be considered `A` objects, since `B` implements `A`'s public interface. So we can take advantage of **polymorphism** to perform a batch operation on both objects.



```java
// instantiate an A and a B object
A myA = new A();
B myB = new B();
```

```java
// put them both into an A-typed array
A[] myObjects = { myA, myB };
```

```java
// loop through all objects in array
for (A myObj : myObjects) {
    myObj.doSomething(); // works fine, since they both have this method
}
```

---

template: difference

## Difference

`B` objects, of course, have their own unique `doSomethingDifferent()` method that `A` objects do not have.

- In a polymorphic context, we can perform a batch operation on both objects using a loop, as done previously, but also have `B` objects do their own unique behavior, if desired, by using the `instanceof` operator.

--

```java
// loop through all objects in array
for (A myObj : myObjects) {
    myObj.doSomething(); // works fine, since they both have this method from A

    // have any B-type objects do their special behavior...
    if (myObj instanceof B) {
        // first cast to B-type
        B sameObjsAsBType = (B) myObj;
        // now call B-type's unique method
        sameObjsAsBType.doSomethingDifferent();
    }
}
```

---

name: evils

# Criticisms of Inheritance

--

## Concept

There are certainly those who criticise object-oriented progrmaming, and some specifically who disapprove of Java's inheritance model.

- The main criticism rests upon Java's inability to handle inheritance from multiple classes.

- This inability can lead to convoluted and undesireable code.

---

template: evils

## Example scenario

Take, for example, the ["Diamond-problem" scenario](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53).

- Imagine an `ElectronicDevice` class that has some behaviors that all electronic devices have, such as powering on and off.

- Next, imagine a `Scanner` class - a document scanner is an electronic device, so it makes sense to inherit the code from `ElectronicDevice` class.

- Next, imagine a `Printer` class - a document printer is also an electronic device, so it makes sense also to inherit the code from `ElectronicDevice` class.

---

template: evils

## Example scenario (continued)

The following UML diagram shows our classes so far, with some example properties and methods.

![Evil inheritance setup](../files/oop-inheritance-evil-setup.png)

---

template: evils

## Example scenario (continued again)

So far so good. But what if we added a `Copier` to the mix?

![Evil inheritance problem](../files/oop-inheritance-evil-problem.png)

---

template: evils

## The problem

In Java and other languages, inheritance from multiple classes is impossible.

--

Why? Well, suppose `Scanner` and `Printer` both had a method with the same name, say `start()`. Which version would `Copier` inherit?

--

The only solution is to use **composition** rather than inheritance:

```java
public class Copier {
    private Scanner scanner;
    private Printer printer;

    public Copier(Scanner scanner, Printer printer) {
        this.scanner = scanner;
        this.printer = printer;
    }
}
```

