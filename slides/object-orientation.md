---
layout: presentation
title: Object Orientation
permalink: /slides/object-orientation/
---

class: center, middle

# Object-Oriented Programming


---

# Agenda

Part I: Overview; The Black Box Metaphor; Objects and Classes
1. [Overview](#overview)
1. [Black Box](#black-box)
1. [Files](#example-1)
1. [Dogs](#example-2)
1. [Creating Difference](#difference)
1. [Controlling Belongingness](#belongingness)
1. [Comparing Sameness](#comparisons)
1. [Stringification](#stringification)

Part II: The Pillar of Object-Orientation; Object-oriented Thinking; Inheritance
1. [The 4 Pillars of Object-Orientation](#pillars)
1. [Inheritance and polymorphism](#overview2)
1. [Basic Implementation](#implementation)
1. [Multi-Level Inheritance](#multi-level)

---

name: overview

# Overview

---

template: overview
name: overview-1

## Concept

Object-oriented programming (**OOP**) is a programming paradigm.

--

OOP organizes software design around **classes** and **objects**.

--

Many programming languages  (e.g., C++, Java, Python) support OOP,
typically in combination with imperative programming.

--

- Code is written to represent virtual _things_.

--

- Each thing has certain **properties** (i.e., variables) that belong to it.

--

- Each thing has certain **actions** (i.e., methods) that it can perform.

---

template: overview
name: overview-2

## Concept (continued)

In object-oriented programming, we write a _description_ of things of a certain type.

--

- This acts as a blueprint or _concept_ for things of this type - a **class**.

--

- Things are then created that _embody_ the abstract concept - **objects**.

---

name: black-box

# Black Box Metaphor

---

template: black-box
name: black-box-1

## Smoke and mirrors

In object-oriented programming, we specify how problems should be solved.

--

Object orientation attempts to implement the [black box metaphor](https://en.wikipedia.org/wiki/Black_box) of engineering.

--

**Black box programming**: Given some input, a black box produces predictable output, but _the user  doesn't see or know implementation details_.

![Black box metapahor](../files/oop-black-box-metaphor.png)

---

template: example-1
name: example-1a

## Example 1: Files

Imagine you want to write code that represents **files** on a computer's hard drive.

--

Every file on the hard drive might have some properties, e.g.

- The data stored within the file
- Metadata: filename, size, date modified, etc.

--

The values these properties hold collectively represent the _internal state_ of any given file at any moment.

---

template: example-1
name: example-1c

## Example 1: Files

What actions could files take? Perhaps they could:

--

- update the data it holds
- change its filename
- save itself to a particular location on the hard drive

--

These actions represent a _public interface_ through which other code can interact with any given file and instruct it what actions to take.

--

```java
// telling the thing what to do...
myFile.setFilename("foobar.txt");
myFile.storeData(someData);
```

--

Calling these methods automatically updates the internal state of the _thing_.

--

```java
// ...causes an internal update of its state - i.e., the values of the properties
filename = "foobar.txt";
data = someData;
```

---

template: example-1
name: example-1d

## UML class diagram

There is a standardized way of representing such _things_, called the Unified Modeling Language (UML). Here is an example of a UML '**class**' diagram:

![UML file example](../files/oop-uml-file-example.png)

---

template: example-1
name: example-1e

## UML class diagram to class definition

This diagram can be translated into code as such:

```java
public class File {
    // properties
    private byte[] data;
    private String filename;
    private int size;
    private int modifiedDate;

    // actions
    public byte[] getData() { ... };
    public void setData(byte[] data) { ... };
    public String getFilename() { ... };
    public void setFilename(String filename) { ... };
    public void saveTo(String filePath) { ... };
}
```

---

template: example-1
name: example-1f

## Intention

A **class** definition is a template from which **objects** can be made as we like.

--

- Each File object has its copy of the properties and methods defined in the File class - these are termed **instance properties ** and **instance methods**.

--

- Each File object can have its specific set of values for the properties defined in the class.

--

- Each File object will respond to calls using any of the methods defined in the class.

--

Making the properties private hides each object's internal state, so code written inside other class definitions cannot see it.

---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: example-2

# Example 2 - Dogs

---

template: example-2
name: example-2a

## Concept

Let's imagine a **dog**, as a concept.

---

template: example-2
name: example-2b

## Properties

Dogs share, for example, the following properties:

- name
- age
- breed
- weight

--

Different dogs will have different values for each of these properties.

--

The value of each dog's properties at any given moment in time represents that dog's **internal state**.

---

template: example-2
name: example-2c

## Actions and their complications.

What actions could a dog _object_ make? Perhaps it could, e.g.:

--

- bark

--

- fetch

--

- sleep

--

There's a catch: Two dogs with different _internal states_ might make the same actions differently. For example:

--

- A lightweight lap dog might have a fast tinny yapping bark, whereas a heavy shepherd might occasionally produce a mellow deep woof sound.

--

- A young dog might generally successfully fetch an object, while an elderly dog might not.

--

- A breed known for its abilities as a guard dog might bark more often and more fiercely than others.

---

template: example-2
name: example-2g

## UML class diagram

A UML class diagram for this dog thing:

![UML dog example](../files/oop-uml-dog-example.png)

---

template: example-2
name: example-2h

## Class definition

This diagram can be translated into code as such:

```java
public class Dog {
    // properties
    private String name;
    private int age;
    private String breed;
    private int weight;

    // actions
    public void bark() { ... };
    public void fetch() { ... };
    public void sleep() { ... };
}
```

---

template: example-2
name: example-2i

## Intention

This Dog **class** definition is a template from which Dog **objects** can be made.

---

template: example-2i
name: example-2j

- Each Dog object has its own specific values for each of the properties the class defines.

---

template: example-2j
name: example-2k

- Each Dog object responds to calls to any of the methods that the Dog class defines.

---

template: example-2k
name: example-2l

- The actions produced by these method calls may differ slightly, depending upon the internal state of each Dog object.

---

name: difference

# Difference

---

template: difference
name: difference-1

## Constructing different objects from the same class

Why create a Dog template class? Because we want to _instantiate_ multiple, distinct objects from it.

---

template: difference-1
name: difference-2

- We also  want these objects to have some differences from one another...

---

template: difference
name: difference-2

## No difference

The following code, _placed in the code of some other class definition_, would instantiate two Dog objects from our Dog class.

```java
Dog dog1 = new Dog();
Dog dog2 = new Dog();
```

---

template: difference-2
name: difference-2a

These are different _things_ in memory.

```java
(dog1 == dog2) // false... they are different references
```

--

But they do not have any difference in terms of their _internal states_.

--

- `String name` -> `null` by default
- `int age` -> `0` by default
- `String breed` -> `null` by default
- `int weight` -> `0` by default

---

template: difference
name: difference-3

## Difference!

If the internal properties of each Dog object were **public** or **protected** (which they are not), it would be possible to give each object distinct values:

--

```java
Dog dog1 = new Dog();
// the following won't work, since the Dog's properties are all private
dog1.name = "Fido";
dog1.breed = "Bugle";
dog1.age = 10;

Dog dog2 = new Dog();
// the following won't work, since the Dog's properties are all private
dog2.name = "Tobik";
dog2.breed = "German Shepherd";
dog2.age = 3;
```

--

But this requires us to make visible the internal properties of the object, which goes against the black box metaphor and imperative-style programming.

---

template: difference
name: difference-3

## Difference! (continued)

What do we want? 

--

We want to set each Dog's name, breed, and age to different internal states, while retaining hidden internal properties for each object.

--

We would like to be able to do something like this:

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

--

At the moment, our class definition provides no mechanism for setting a given object's internal properties... How can we do this?

---

template: difference
name: difference-4

## Constructors

In order to be able to set each object's properties discretely, we need to modify the Dog class to have a special **constructor** function.

--

```java
public class Dog {

    // a constructor function!
    public Dog(String name, String breed, int age) {
        // set this object's internal properties
        this.name = name;
        this.breed = breed;
        this.age = age;
    }

    // properties
    private String name;
    private int age;
    private String breed;
    // and so on...
//...
```

---

template: difference
name: difference-5

## Constructors (continued)

Note that constructor functions do not specify a return type.

```java
public class Dog {
    //...
    public Dog(String name, String breed, int age) {
        //...
    }
    //...
}
```

---

template: difference
name: this

## This, not that

The `this` keyword is used to indicate which object we are talking about it.

--

- Since a single class is a blueprint that can be used to create many objects, Java needs to know which object we are referring to.

--

- So `this` always automatically refers to the object upon whom the current method is being called.

Imagine we defined the `Dog` class's bark method:

```java
public class Dog {
    //...
    public void bark() {
        System.out.printf( "%s says, 'Woof!' ", this.name );
    }
    //...
```

--

- Which dog's name will be output when this method is called?

---

template: difference

## This, not that (continued)

The answer is, "whichever dog the method is called upon".

--

If somewhere we call that method on a dog named Fido, then Fido's name will be output.

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);

//...

dog1.bark(); // outputs "Fido says, 'Woof!' "
```

--

Whereas, if we were to call that method on a dog named Tobik, then Tobik's name would be output.

```java
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);

//...

dog2.bark(); // outputs "Tobik says, 'Woof!' "
```

---

template: difference
name: difference-5

## Instantiating objects

With constructor functions, we can instantiate as many objects as we like with whatever property values we want them to have.

--

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

---

template: difference
name: difference-6

## Instantiating objects (continued)

We could make 101 Dalmatians with random names and ages, if we wanted...

```java
// let's make a random mix of names and ages objects
String[] names = "Patch,Lucky,Cadpig,Roly Poly,Penny,Freckles,Pepper".split(",");
int[] ages = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14 };

Dog[] dogs = new Dog[101]; // will hold 101 Dalmatians

for (int i=0; i<dogs.length; i++) {
    // assign each dog random property values from these arrays
    String randomName = names[ (int) (Math.random() * names.length) ];
    int randomAge = ages[ (int) (Math.random() * ages.length) ];

    dogs[i] = new Dog( randomName, "Dalmatian", randomAge ); // instantiate a Dog object

    dogs[i].bark(); // make each dog bark

}
```


---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

template: difference
name: difference-7

## Changing internal state

Constructors allow us to set up an object's internal state at its creation. But what if we wanted to update those values at some later date?

--

- For example, what if one of the 101 Dalmatians has a [happy] birthday and is now a year older... can we not update the age property?

--

- In other words, we would like to be able to do something like this:

```java
// instantiate an object with an initial internal statee
Dog dog1 = new Dog("Fido", "Bugle", 10);

// do some very important significant stuff...

// update the object's internal state at some later point
dog1.age = dog1.age + 1; // happy birthday!

```

--

By now, you know that this is not possible. The internal properties are **private** and cannot be accessed from 'user' code in a different class.

---

template: difference
name: difference-8

## Setters

To change an object's internal state, we need a '**setter**' function to allow us to set the value of an existing object.

--

```java
public class Dog {
    // ...etc etc
    // a setter function
    public void setAge(int age) {
        // first validate the value, and then use it if good
        if (age > 0 && age < 20) this.age = age;
    }
    // ...
// ...
```

--

- Note that the setter method performs **validation** - it only allows good values to be placed into the property - this is typical of setters.

--

- Note also that the method is _public_, so it can be called from code outside the `Dog` class.

---

template: difference
name: difference-9

## Setters (continued)

With setters, it is possible to set the values of properties on existing objects.

--

Assuming we have created a Dog object...

```java
Dog dog1 = new Dog("Roly Poly", "Dalmatian", 10); // instantiate a dog
```

--

...we can now update its age using the setter

```java
dog1.setAge(11);
```

---

template: difference

## Setters (continued again)

If setters are present, they should _always_ be used whenever an object's property values need to be changed.

--

- if a **constructor** sets an object's initial starting property values, it should do so by calling the object's setters.

--

- if **any other method** adjusts an object's property values, it should do so by calling the object's setters.

--

- this guarantees that any **validation** performed within the setter function is always used, and this validation logic is written in only one place in the code - in the setter.

---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

template: difference
name: difference-9

## Accessing internal state

What if you wanted to know a particular Dog's age... how could you find that out programmatically?

--

- For example, instead of hard-coding `11` in the statement `dog1.setAge(11);`, could we have programmatically determined `dog1`'s current age and simply added one to that?

--

- We certainly cannot do the following, since the age property is _private_ and cannot be read from code outside the `Dog` class:

```java
dog1.setAge ( dog1.age + 1 )
```

---

template: difference
name: difference-10

## Getters

Of course, we can allow access to an object's internal state. But we need to create '**getter**' functions to do so.

--

```java
public class Dog {
    // ...etc etc

    // a getter function
    public int getAge() {
        // simply return the value of the age property
        return this.age;
    }

    // ...and so on and so forth
// ...
```

--

- Note that this function simply returns the value of a private property of the object. It may seem a bit redundant, but this is typical of getters.

--

- Note also that the method is _public_, so it can be called from code outside the `Dog` class.

---

template: difference
name: difference-11

## Getters (continued)

With a getter function, we can read the current value of an object's property.

--

```java
System.out.println ( dog1.getAge() ); // will output dog1's age
```

--

... and use that information to help us understand that object's internal state

```java
dog1.setAge( dog1.getAge() + 1 );
```

--

Knowledge of an object's internal state can help us make decisions

```java
if ( dog1.getBreed().equals("Dalmatian") && dog1.getName().equals("Pepper") ) {
    // use your imagination
}
```

---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: belongingness

# Controlling Belongingness

--

## Non-static properties and methods

Neither _setters_ nor _getters_, nor even the methods that represent the object's actions (e.g., _bark_, _fetch_, _sleep_) were declared with the keyword `static` in their method signatures. Neither were any of the properties (e.g., _name_, _breed_, _age_).

--

The keyword `static` indicates that a method or property belongs to the class as a whole, not to each particular object independently.


--

Thus, properties and methods that we want to _belong to each object individually_ do not use the `static` keyword.

---

template: belongingness

## Shared concerns

When does it makes sense for a property or method to belong to the class as a whole, i.e., for it to be declared `static`?

--

- For example, imagine that you wanted to track how many dog objects had been instantiated from the Dog class.

--

- You could create a `static` property named `numDogs` that is incremented each time a Dog is instantiated.

---

template: belongingness

## Shared concerns (continued)

```java
public class Dog {
    //...
    public Dog(String name, String breed, int age) {
        //...
        Dog.numDogs++; // increment the static property
        //...
    }
    //...
    private static int numDogs = 0;

//...
```

--

- We refer to the property as `Dog.numDogs` rather than `this.numDogs`.

--

- `Dog.numDogs` communicates that the `numDogs` property belongs to the `Dog` class as a whole.

---

template: belongingness

## Shared concerns (continued again)

Every time we instantiate a new `Dog` object, the counter will be incremented.

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);
```

--

- Because the counter was declared as `private`, we cannot see how many dogs have been made from code outside the `Dog` class.

--

- Use a `public` _getter_ method to access the `numDogs` property!

--

```java
System.out.printf( "There exist %d dogs in our world.\n", Dog.getNumDogs() );
```

---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: comparisons

# Comparing Sameness

--

## Different kinds of difference

There are a few ways we can compare two objects.

--

- by whether they are, in fact, the same object in memory

--

- by whether their internal states are the same or similar

---

template: comparisons

## Identity comparison

What is we use the `==` operator to compare to dog objects?

--

```java
if (dog1 == dog2) {
    System.out.printf("%s is actually the same dog as %s!\n", dog1.getName(), dog2.getName);
}
```

--

- Objects in Java are **reference types**, meaning that a variable assigned to point to an object holds the memory address of that object.

--

- The `==` operator, when used with a reference type, compares memory addresses.

---

template: comparisons

## Objects as reference types

Because objects are reference types, when they are passed as arguments to a method, the memory address is what is passed.

--

```java
public void rename(Dog d) {
        d.setName("Dog");
}
```

```java
Dog dog1 = new Dog("Fido", "Bugle", 10);
rename(dog1);
System.out.println( dog1.getName() )
```

--

- The dog object referred to within the `rename` method as `d` is the same dog object referred to by the calling method as `dog1` - they are **aliases**.

--

- So the printed output will be "Dog", not "Fido".

---

template: comparisons

## Internal state comparison

To check whether two objects share the same internal state, even if they are different objects in memory, we have to write our own method.

--

- Simply define a method named `equals` to perform the comparison.

--

name: tedium

```java
public class Dog {
        //...

        public boolean equals(Dog that) {
            boolean sameName = this.name.equals( that.getName() ); // are the names the same?
            boolean sameAge = ( this.age == that.getAge() ); // same age?
            boolean sameBreed = ( this.breed.equals( that.getBreed() ) );
            boolean sameWeight = ( this.weight == that.getWeight() );
            return sameName && sameAge && sameBreed && sameWeight; // true if all the same, false otherwise
        }
        //...
```

---

template: comparisons

## Internal state comparison (continued)

To compare two dogs, you would use one of those dogs' `equals()` method.

```java
if ( dog1.equals(dog2) ) {
    System.out.printf("%s and %s have the same internal state!\n", dog1.getName(), dog2.getName);
}
```

---

name: stringification

# Stringification

--

## Concept

Converting an object to a String usually leads to unwanted text.

--

```java
// instantiate a Dog object
Dog dog2 = new Dog("Tobik", "German Shepherd", 3);

// do something that requires the object to be converted to a String
String text = String.format("The dog as a string looks like: %s", dog2);

// see what you get...
System.out.println(text);
```

--

By default, the output would show the **class** name of the object and a **[hashcode](https://coderanch.com/t/321515/java/HashCode)**.

```
The dog as a string looks like: Dog@63961c42
```

--

Wouldn't it be nice if we could instead output something descriptive:

```
The dog as a string looks like: Tobik, a 3-year-old German Shepherd
```

---

template: stringification

## Fulfilling our desires

Java allows us to describe how an object should be converted to a String: With a special method named `toString()`.

--

```java
public class Dog {
    //...
    public String toString() {
        String myself = String.format( "%s, a %d-year-old %s", this.getName(), this.getAge(), this.getBreed() );
        return myself;
    }
    //...
}
```

--

Now, converting the object to a String will result in something more descriptive, such as:

```
Tobik, a 3-year-old German Shepherd
```


---

name: pillars

# The 4 Pillars of Object-Orientation

The **four pillars of object-oriented programming**:

--

1. Abstraction

2. Encapsulation

3. Inheritance

4. Polymorphism

---

template: pillars

## Abstraction

> abstract (adjective): disassociated from any specific instance
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/abstract)

--

Abstraction is thus the _process of making something abstract_ or _the state of being abstracted_.

--

- The **black box metaphor** encourages abstraction.

- **Hiding implementation details** of code encourages abstraction

- **Classes** are abstractions of the objects that are instantiated from them.

- **Static properties and methods** are abstractions, too.

---

template: pillars

## Encapsulation

> encapsulate (verb): to enclose in or as if in a capsule
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/encapsulate)

--

Encapsulation is thus the _process of enclosing some things within other things_.

--

- **Instance properties and methods** are encapsulated within the objects to which they belong.

- **Static properties and methods** are encapsulated within the class to which they belong.

- **Classes** are encapsulated within the packages to which they belong.

- **Packages** may be encapsulated within parent packages.

---

template: pillars

## Inheritance

> inherit (verb): to receive from an ancestor
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/inherit)

--

Inheritance is thus _that which is inherited from an ancestor_.

--

- **Classes**, and the objects instantiated from them, can inherit properties and methods from ancestor classes.

- **Classes**, and the objects instantiated from them, can inherit properties and methods from ancestor interfaces.

---

template: pillars

## Polymorphism

> polymorphism (noun): the quality or state of existing in or assuming different forms
>
> -[Mirriam-Webster](https://www.merriam-webster.com/dictionary/polymorphism)

--

- **Objects** can be instances of more than one class (we have not discussed this yet).

- **Objects** can also be instances of one or more interfaces (we have not discussed this yet).

---



name: overview2

# Inheritance and polymorphism

--

## Concept

**Inheritance** is the mechanism of basing an object or a class on another object or class, retaining a similar implementation.

--

The properties and methods of one object or class are "passed down" automatically to the objects or classes that inherit from it.

---

template: overview2

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
    public void setMessage(String msg) {
        if (msg.length > 0) this.message = msg;
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

We often create UML diagrams indicating class relationships, where the arrow points from child to parent.

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

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: multi-level

# Multi-Level Inheritance

---

template: multi-level

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

<div align="center">
<span style="color: red;">Practice round</span> </div>

---
