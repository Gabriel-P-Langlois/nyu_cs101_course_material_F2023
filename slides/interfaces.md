---
layout: presentation
title: Polymorphism
permalink: /slides/interfaces/
---

class: center, middle

# Polymorphism

---

# Agenda

1. [Polymorphism](#polymorphism)
1. [Similarity & Difference](#difference)
1. [Polymorphism with interfaces](#polymorphism_interfaces)
1. [Is Inheritance Evil?](#evils)

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

<div align="center">
<span style="color: red;">Practice round</span> </div>

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

name: polymorphism_interfaces

# Polymorphism with interfaces

--

- Imagine we have an interface called `Vehicle`.

- Imagine we had a second interface called `Flyable`.

- A single class could implement both the Vehicle and Flyable interfaces...

--

```java
public class Plane implements Vehicle, Flyable {
  // All properties and abstract methods from Vehicle must be implemented.
  
  // All properties and abstract methods from Flyable must be implemented.
}
```

---

template: polymorphism_interfaces

# Polymorphism with interfaces

Objects that implement a given interface can polymorphically be considered to be of the interface type.

For example, a Plane object could be referenced by a Vehicle-typed variable

```java
Vehicle jet = new Plane();
```

--

As with all polymorphism, this can be used to perform batch operations:

--

```java
Vehicle[] planes = {
  new Plane1(),
  new Plane2(),
  };
  
  // iterate through each object
  for (Vehicle plane : planes) {
    plane.speedUp(1);
  }
```

---

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
