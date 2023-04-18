---
layout: presentation
title: Exception Handling
permalink: /slides/exception-handling/
---

class: center, middle

# Exception Handling

> Beginner knows rules, but veterans know exceptions.
>
> –Amit Kalantri, in [Wealth of Words](https://www.goodreads.com/book/show/32181272-wealth-of-words)

---

# Agenda

1. [Overview](#concept)
1. [Exception Handling](#handling)
1. [Custom Exceptions](#custom)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

An **exception** is a disruption to the _normal_ control flow of of a program.

--

- Exceptions occur when something unexpected has happened and are reported either during compilation or execution of the program.

--

- Ex 1: If Java code tries to open up a file that might not exist, an exception will be reported _during compilation_.

--

- Ex 2: If an array has a length of `5` and your code tries to access the array value at index position `7`, an exception will be reported _during execution_.

--

- Whether an exception is reported during compilation or execution depends upon whether it is _checked_ or _unchecked_.

---

template: overview

## Types

Exceptions are divided into two types, depending upon when they appear.

--

**Checked exceptions** are reported during compilation. These exceptions will crash the compiler if they are not _handled_. 

--

**Unchecked exceptions** are reported during execution. These exceptions are not checked by the compiler. Your program may crash if not _handled_ in your program.

--

**It is wrong** to think of exceptions as being errors.

--

**Errors**, in Java, are failures that result from factors outside the control of the program, such as running out of memory. Like unchecked exceptions, they cause the program to crash.

---

template: overview

## Exception lineage

```
Throwable
   |
   |---> Exception
   |        |
   |        |---> IOException
   |        |           |
   |        |           |---> FileIOException
   |        |
   |        |---> RuntimeException
   |                    |
   |                    |---> NullPointerException
   |                    |
   |                    |---> IndexOutOfBoundsException
   |
   |---> Error
```

- Exceptions are descended from the Java API's `Exception` class. **Unchecked** exceptions are descended from `Exception`'s child, `RuntimeException`.
- Errors are descended from `Error`.
- All these inherit from a `Throwable` ancestor.

---

template: overview

## Why two types?

Why doesn't the compiler check all exceptions so Java can avoid runtime crashes?

--

- Exceptions can occur frequently; if they were all checked (which requires extra code), _it would put a big burden on the programmer and the code_.

--

Now you may wonder why not leave all exceptions unchecked. The checks wouldn't then overburden the programmer and codebase!

--

- In some languages, like C++, _all exceptions are unchecked_. The compiler does not get involved and it is up to the programmer to make sure their code is reliable. _Java is not one of these languages_.

--

- This discussion is known as **The Java Unchecked Exceptions Controversy** - [read more about it](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html).

---

template: overview

## Net net

--

In conclusion, the Java people recommend the following:

- _Use checked exceptions if the program could reasonably be expected to recover_ from the situation in which the exception occurs.

--

- _Use unchecked exceptions if your program can't recover_ from the situation in which the exception occurs.

--

- We'll focus on understanding checked exceptions.

---

name: handling

# Exception Handling

--

## Options

Any method that includes code that _might_ cause a checked exception to occur _must_ handle that situation in one of two ways, in order to compile.

--

- First way: Encapsulate the uncertain code within a `try`/`catch` block.

--

name: handling-options

- Second way: declare in the method signature that the method `throws` one or more exceptions.

---

template: handling

## Example - the problem

For example, take a method that opens a file... this might cause a checked exception if the file being opened does not exist.

--

```java
public static void doSomething() {
   Scanner scn = new Scanner( new File( "data/foo.txt" ) );
   String line = scn.nextLine();
   System.out.println(line);
}
```

--

- This code will not compile. (**Demo**)

--

- The `Scanner` class's constructor declares that it may cause a checked exception when the file is not found. It declares this using the `throws` declaration which we'll return to a bit later.

--

- Yet the `doSomething()` method does not have any code to handle the situation in which this exception occurs.

---

template: handling

## Example - the try/catch solution

One way to get the code to compile would be to surround the code of concern within a `try`/`catch` block.

--

name: example-try-catch

```java
   public static void doSomething(){
        try{
            Scanner scn = new Scanner( new File( "data/foo.txt" ) );
            String line = scn.nextLine();
		    System.out.println(line);
        }
        catch (FileNotFoundException e) {
            System.out.println("Couldn't find the file...");
        }
    }
```

--

- (**Demo**)

---

template: handling

## Example - the throws solution

An alternative way to get that code to compile would have been to declare that the method `throws` an exception.

--

name: example-throws

```java
public static void doSomething() throws FileNotFoundException{
   Scanner scn = new Scanner( new File( "data/foo.txt" ) );
   String line = scn.nextLine();
   System.out.println(line);
}
```

--

- This is a form of '[passing the buck](https://dictionary.cambridge.org/us/dictionary/english/pass-the-buck)'.

--

- The `doSomething()` method has abdicated responsibility for the exception that may occur, and it is now the responsibility of any method that calls `doSomething()` to handle the exception.

--

- Any method that calls this method must now itself handle the situation in one of [the two ways we've discussed](#handling-options): using `try`/`catch` around the call to this method, or declaring that it too `throws` an exception.

---

template: handling

## Example - the throws solution (continued)

Let's imagine another method that calls our `doSomething` method.

--

```java
public void anotherMethod() {
  doSomething(); // call the method that might trigger an exception
}
```

--

- If `doSomething()` encapsulates the file opening code within a `try`/`catch` block, as in [an earlier example](#example-try-catch), then this code is fine - no need for any worry, since the exception is fully handled.

--

- If `doSomething()` instead declared that it `throws` an exception, as in our [most recent example](#example-throws), then this code will not compile.

--

- In the latter scenario, this method must either surround the call to `doSomething()` in a `try`/`catch` block, or declare that it too `throws` an exception.

---

template: handling

## Example - the throws solution (continued again)

Assuming `doSomething()` `throws` an exception, here are the two options for our `anotherMethod()` in order for it to compile:

--

```java
// the try/catch way
public void anotherMethod() {
  try {
    doSomething(); // call the method that might trigger an exception
  }
  catch (FileNotFoundException e) {
    System.out.println("So sorry, we couldn't open the file.");
    // put whatever you want to do in this situation here.
  }
}
```

--

```java
// the throws way
public void anotherMethod() throws FileNotFoundException {
  doSomething();
}
```

---

name: custom

# Custom Exceptions

--

## Concept

While the Java API comes with exception types useful for many common situations, it is possible to build one's own exception types.

--

- What we call an **exception** is simply an object of any type that is descended from the `Exception` class.

--

- If we subclass `Exception`, we can create our own checked exception types that we can then `throw` whenever we want.

---

template: custom

## Subclassing Exception

Here is an example of a custom exception type, useful for the situation where a virtual person sips a burning hot virtual cup of coffee.

--

```java
public class BurnedMouthException extends Exception {
  // .. put any code you want in here.
}
```

--

- elsewhere in our program, if a virtual person sips a burning hot cup of virtual coffee, we can throw an exception of this specialized type.

---

template: custom

## Throw and throws

Here is an example of the `sip()` method in our `Person` class that _might_ throw one of our custom exceptions if the `Coffee` object is burning hot.

--

```java
public class Person {

  public void sip(Coffee c) throws BurnedMouthException {
    // throw an exception if the temperature is too hot
    if ( c.getTemperature("Farenheit") > 113 ) {
      throw new BurnedMouthException();
    }
  }
}
```

--

- Note that the method must declare, with the `throws` keyword, that it _might_ throw an exception.

--

- Note also that the exception is nothing but an object of a class descended from `Exception` and is thrown using the `throw` keyword.

---

template: custom

## Throwing multiple possible exceptions

It's perfectly possible for a method to potentially throw more than one type of exception.

--

- For example, let's say we had a `OutOfCoffeeException` that we also threw if sipping an empty coffee.

--

```java
public void sip(Coffee c) throws BurnedMouthException, OutOfCoffeeException {

    // throw an exception if the temperature is too hot
    if ( c.getTemperature("Farenheit") > 113 ) {
      throw new BurnedMouthException();
    }

    // throw an exception if the coffee is empty
    else if ( c.coffeeRemaining() == 0 ) {
      throw new OutOfCoffeeException();
    }

}
```

---

template: custom

## Handling exceptions

As we have already learned, any other method that calls this `sip()` method must handle the possibility of a checked exception occurring in [one of two ways](#handling-options). Here is a `try`/`catch` solution:

--

```java
try {
  // let's imagine that we have Person object person and Coffee object coffee
  person.sip(coffee);
}
catch (BurnedMouthException e) {
  // do something in response to this exception being thrown
}
catch (OutOfCoffeeException e) {
  // do something in response to this exeption being thrown
}
```

--

- Notice that we can catch the two exceptions separately, allowing us to take different follow-up actions in each scenario.

---

template: custom

## Handling exceptions (continued)

Alternatively, this method could have declared that it `throws` the two exceptions that the `sip()` method might throw, thereby _passing the buck_ to any method that calls it.

--

```java
public static void main(String[] args) throws BurnedMouthException, OutOfCoffeeException {

    // imagine that we have Person object person and Coffee object coffee already instantiated

    // have the person take a sip
    person.sip(coffee);

}
```

--

- Notice that this code compiles, even though we never fully handle the exceptions with a `try`/`catch` block.

--

- The compiler ignores any exceptions thrown by the `main` method.... but the program crashes during runtime.

---

name: conclusions

# Conclusions

--

Like function arguments and return values, checked exceptions are yet another mechanism by which messages are passed from one part of a Java program to another.

--

Info:

- New quiz will be released later today.
- Next (and last) assignment will be released on Thursday and be due two weeks after (May 4th).
