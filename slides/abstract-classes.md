---
layout: presentation
title: Abstract Classes
permalink: /slides/abstract-classes/
---

class: center, middle

# Abstract Classes and Interfaces

---

# Agenda

1. [Overview](#concept)
1. [Concrete or Abstract classes?](#picking)
1. [Conclusions](#conclusions)

---

name: overview

# Overview of Abstract classes

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

# Concrete or abstract classes?

--

## Choosing between the two

Given that abstract classes can share all the same sorts of code as a concrete class, and more, _how do you pick between the two_?

--

It's easy:

- Use an abstract class if it makes no conceptual sense for the class to ever be instantiated.

- Use a concrete class if it does make sense.

---

template: picking

## Example

- Dogs, cats and pigs are all animals. What if we wanted to write code for representing them? 

- **One way**: Create an Animal class that encapsulates what dogs, cats and pigs have in common and have them inherit the properties of the Animal class.

- Does it make sense to instantiate an Animal object? No, not in this case. 

- But it makes sense to create an abstract Animal class containing a lot of code shared in common by three concrete child classes, Dog, Cat and Pig.

---

name: overview-interfaces

# Overview of Interfaces

--

## Concept

An **interface** is a blueprint of a class.

A java interface contains static constants and abstract methods. _It cannot contain anything else_.

--

```java
public interface Vehicle {
    // Attributes -- all attributes are public, static, and final by default.
    final float MAX_VELOCITY;
    
    // Methods -- all methods are public and abstract by default
    void speedUp(int a);
    void applyBrakes(int a);
}
```

---

template: overview-interfaces

## Concept

Interfaces serve as a sort of contract.

--

- An interface is similar to an abstract class, but its intent is to specify what methods that a class **must** implement.

--

- Any class can declare that it implements an interface, meaning it agrees to implement the behaviors the interface specifies.

--

- Java will not compile the code if any class that agreed to adhere to an interface does not properly implement its public interface.

---

name: example-interface

# Example

--

## Vehicle interface

Imagine the following vehicle interface:

```java
public interface Vehicle {
    // Attributes -- all attributes are public, static, and final by default.
    final float MAX_VELOCITY;
    
    // Methods -- all methods are public and abstract by default
    void speedUp(int a);
    void applyBrakes(int a);
}
```

--

Any class can adhere to this interface using the **implements** keyword.

```java
public class Bicycle implements Vehicle {
  float MAX_VELOCITY = 30; // MPH
  
  public void speedUp(int a) {
    // implementation goes there
  }
  
  public void applyBrakes(int a) {
    // implementation goes there
  }
}
```

---

template: example-interface

## Some notes

Classes that implement an interface _must_ implement the methods declared within the interface. The code won't compile otherwise.

- The class may contain other properties and methods in addition to those specified in the interface.

--

The value of an interface is that it can ensure the same set of behaviors across several different classes.

- The expectation is that these behaviors are implemented differently among the classes that implement them.

---

name: conclusions

# Conclusions

--

Abstract classes can be useful, when implemented with tact. You now have an understanding of the various ways in which this might be the case.
