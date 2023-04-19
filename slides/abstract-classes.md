---
layout: presentation
title: Abstract Classes
permalink: /slides/abstract-classes/
---

class: center, middle

# Abstract Classes

---

# Agenda

1. [Overview](#concept)
1. [Pick Your Abstraction](#picking)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

An **abstract class** is a class that contains one or more **abstract methods**, which are simply method declarations without a body.

--

Think of an abstract method like a prototype for a method. It declares the method’s return type and parameter list without implementing the method.

--

Abstract methods provide _a common definition of a base class that multiple derived classes can share_.

--

```java
public abstract class Animal {
  // Attributes
  public String name;

  // Methods
  public abstract void makeSound();
  public void sleep(); {
    System.out.println("Zzz");
  }
}
```

---

template: overview

## Similarity to concrete classes

A class which is not abstract is called a **concrete class**.

--

An abstract class can encapsulate _all the same properties and methods_ as a concrete class:

- Private, protected, or public properties and methods

- Static or non-static properties and methods

- Constants and non-constants

- Etc.

---

template: overview

## Difference from concrete classes

There are only two differences between an abstract class and a concrete class:

- Abstract classes _can contain abstract methods_, that is, method declarations without their corresponding implementation.

```java
public abstract class Animal {
  // Attributes
  public String name;

  // Methods
  public abstract void makeSound();
  public void sleep(); {
    System.out.println("Zzz");
  }
}
```

- Abstract classes _can never be instantiated_!

```java
Animal a = new Animal(); // This will result in a compilation error
```

---

template: overview

## Legacy

An abstract class has no use unless some other class extends it.

Any non-abstract child class **must** implement abstract methods declared in an abstract parent or other ancestor class.

---

template: overview

## Legacy

```java
public abstract class Animal {
  // Attributes
  public String name;

  // Methods
  public abstract void makeSound();
  public void sleep(); {
    System.out.println("Zzz");
  }
}
```

```java
public class Pig extends Animal {
  public Pig(String name) {
    super(name);
  }
  
  @Override
  public void makeSound(){
    System.out.println("Oink oink!")
  }
}
```

---

name: picking

# Concrete or abstact classes?

Given that abstract classes can share all the same sorts of code as a concrete class, and more, _how do you pick between the two_?

--

It's easy:

- Use an abstract class if it makes no conceptual sense for the class to ever be instantiated.

- Use a concrete class if it does make sense.

--

Example:

- Dogs, cats and pigs are all animals. What if we wanted to write code for representing them? 

- **One way**: Create an Animal class that encapsulates what dogs, cats and pigs have in common and have them inherit the properties of the Animal class.

- Does it make sense to instantiate an Animal object? No, not in this case. But it makes sense to create an abstract Animal class containing a lot of code shared in common by three concrete child classes, Dog, Cat and Pig.

---

name: conclusions

# Conclusions

--

Abstract classes can be useful, when implemented with tact. You now have an understanding of the various ways in which this might be the case.
