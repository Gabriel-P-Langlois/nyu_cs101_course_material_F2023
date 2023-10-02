---
layout: presentation
title: Arrays
permalink: /slides/arrays/
---

class: center, middle

# Arrays

---

# Reminders and announcements

- Assignment 1 is due today at 11:59 p.m.
- Quiz 5 is out and is due on Friday, Oct 6.
- Assignment 2 is due next Tuesday, Oct. 10, at 11:59 p.m.
- Assignment 3 is out today and due on Tuesday, Oct. 17, at 11:59 p.m.

Important: My office hours next week will be held virtually on Zoom. I will also expand them (TBA on Thursday).

---

# Agenda

1. [Overview](#concept)
1. [Creation](#creation)
1. [Array Length](#length)
1. [Arrays Utility Class](#arrays-class)
1. [Search an Array](#binary-search)
1. [Challenges](#challenges)
1. [ArrayList Class](#arraylist)
1. [Java Is Pass By Value Language](#pass-by-value)
1. [Basic Usage Examples](#examples)

---

name: overview

# Overview

Arrays are used to store multiple values in a single variable.

--

There is no need to declare multiple variables for each value; use an array!

--

Formally, an array in Java is a *non-primitive* data type used to store multiple values of the *same* data type.

--

Arrays can store any data type or data structure, including arrays, so long they are all of the same type.

---

name: creation

# Creation

--

## First way: Using the `new` keyword

The `new` keyword tells Java to allocate a certain amount of memory for this array, *before* it has been populated.

```java
char[] myFavoriteCharacters = new char[3];
myFavoriteCharacters[0] = 'f';
myFavoriteCharacters[1] = 'o';
myFavoriteCharacters[2] = 'o';
```

- In this case, Java knows that each `char` value consumes 16 bits, so it reserves enough memory space for 3 of them.

- The length of the array **cannot** be modified once memory has been allocated for an array of a specific length.

---

template: creation
name: creation-2

## Second way: Using syntactic sugar

Arrays can be created using shorthand syntax that Java converts at compilation to longer form.

--

This is useful if you know the values you want to put into the array.

```java
char[] myFavoriteCharacters = { 'f', 'o', 'o' };
```

- Note that both operations - declaring the variable and allocating and populating the array - must be done in one statement with this style.

---

template: creation

## Object[] arrays

Actually, you can create an array of different types.

--

To do that, use Object[] for the type of your array.

```java
Object[] x = new Object[]{1,2,3,"srk"};
```

The first three elements of x are integers, and the last element is a string.

---

template: creation
name: creation-3

## Third way (for strings): Using String's split function

Arrays can be made from text that contains a particular separator.

```java
String myMessageToYou = "Don't worry about a thing";
String[] words = myMessageToYou.split(" ");
// now you have an array { "Don't", "worry", "about", "a", "thing" }
```

--

You can also use [regular expressions syntax](https://docs.oracle.com/javase/tutorial/essential/regex/) to split a string using one of several separators:

```java
String myMessageToYou = "Don't, worry?about-a .thing";
String[] words = myMessageToYou.split("[ ,?-.]+");
// .split("[ ,?-.]+") means: split the string if you encounter *any* combination of " " or "," or "?" or "-" or "."
// In this example, the split method will encounter the comma and a space before encountering the charater 'w'. Thus it will parse out
// "Don't" from the delimiter ", ". split will then proceed from the rest of the string "worry?about-a .thing"".
// now you have an array { "Don't", "worry", "about", "a", "thing" }
```

--

**Warning**: You'll have to use this for the assignment 3. :-)

---

name: length

# Array Length

## Counting elements in an array

The `length` property of any array counts its members.

--

```java
Scanner scn = new Scanner(System.in);
String[] veggies; // reference to an as-yet unallocated array
int num = 0;
while (num < 1) {
    System.out.println("Enter your favorite vegetables, separated by commas: ");
    String response = scn.nextLine();
    veggies = response.split(","); // array is now allocated and populated
    num = veggies.length;
}
```

Remember: Arrays in Java have **fixed length**. New positions cannot be added and existing positions cannot be removed from an array.

---

name: arrays-class

# Arrays Utility Class

--

## Useful array-related functions

An array is *not* a primitive data type in Java.

--

Nonetheless, Java provides different methods and utilities for arrays through the *Arrays utility class*.

--

The **Arrays utility class** provides methods for manipulating arrays.

--

Use `import java.util.Arrays` to invoke the library.

---

template: arrays-class
name: arrays-class-2

## Convert array contents to String

`Arrays.toString()` prints out the contents of the array _inelegantly_.

- Good for debugging.

```java
String[] arrVar = { "hello", "and", "good", "morning" };
String contents = Arrays.toString(arrVar); // -> "[hello,and,good,morning]"
```

--

... and for multi-dimensional arrays, use `.deepToString()`:

```java
String[][] arrVar = {
    {"hello", "world"},
    {"goodbye", "world"}
}; // a two-dimensional array
String contents = Arrays.deepToString(arrVar); // -> "[[hello,world],[goodbye,world]]"
```

---

template: arrays-class
name: arrays-class-3

## Comparing values in two arrays

`Arrays.equals()` determines whether two arrays have the same set of values:

```java
String[] arrVar1 = { "hello", "and", "good", "morning" };
String[] arrVar2 = { "hello", "and", "good", "morning" }; // a separate array with the same values as arrVar1 but at a different location in memory
boolean sameValues = Arrays.equals(arrVar1, arrVar2); // -> true!
```

--

... and for multi-dimensional arrays, use `.deepEquals()`:

```java
String[][] arrVar1 = { {"hello", "world"}, {"goodbye", "world"} }; // a two-dimensional array
String[][] arrVar2 = { {"hello", "world"}, {"goodbye", "world"} }; // a separate array with the same values as arrVar1 but at a different location in memory
boolean sameValues = Arrays.deepEquals(arrVar1, arrVar); // -> true!
```

Note: Do **not** use the comparison operator `==` for this.

---

template: arrays-class
name: arrays-class-4

## Sorting the values in an array

Put them in order.

```java
int[] arrVar = {134, 5, 3636, 34, 8};
Arrays.sort(arrVar);
// arrVar now holds {5, 8, 34, 134, 3636}
```

--

It is also possible to sort a subset of the array:

```java
int[] arrVar = {134, 5, 3636, 34, 8};
int startIndex = 1;
int endIndex = 4;
Arrays.sort(arrVar, startIndex, endIndex);
// arrVar now holds {134, 34, 3636, 8}
```

---

template: arrays-class
name: arrays-class-6

## Copying an array

Use `Arrays.copyOf()` to make a clone:

```java
int newArrLength = 10;
Arrays.copyOf(arrVar, newArrLength); // copy into array of different length
```

--

name: arrays-class-copy

... or `.copyOfRange()` to clone a subset of the values in an array:

```java
int startIndex = 0;
int endIndex = 3;
Arrays.copyOfRange(arrVar, startIndex, endIndex); // copy only a subset
```

---

template: arrays-class
name: arrays-class-7

## Filling an array

`Arrays.fill()` places default values into an array:

```java
String defaultValue = "foo";
Arrays.fill(arrVar, defaultValue);
```

---

template: arrays-class
name: arrays-class-8

## Searching an array

Binary search can be performed using the `Arrays.binarySearch()` method:

```java
int[] numbers = {2456, 35, 25986, 10, 12};
int searchTerm = 10;
int pos = Arrays.binarySearch(numbers, searchTerm); // -> 3
```

--

- The term `binary` refers to the searching algorithm used.
- It can only be used if the array can be `sorted`.

'Sorted': All primitive data types and `objects` that `implement` the Comparable `interface`. 

The concepts of objects, implementation and interface will all be covered later during the course.

--

- Use .linearSearch() to search an array that cannot be sorted.
- Search and sort algorithms will be encountered in CS 102. :-)

---

name: challenges

# Challenges

--

## Overview

Due to the **fixed-length** nature of arrays, it is not possible to add or remove values to an array "on the fly."

--

If we want to **"add" a new value to an array**, then we can:

1. Create a new array that is one longer than the old array
1. Copy the values from the old array into the new array (using a for loop or methods in the [Arrays utility class](#arrays-class-6).)
1. Add the new value into the last empty spot of the new array

--

Similarly, if we want to **"remove" a value from an array**, then we can:

1. Create a new array that is one shorter than the old array
1. Copy the values you want to keep into the new array, but don't copy the one you want to remove (using a for loop or methods in the [Arrays utility class](#arrays-class-copy).)

---

template: challenges
name: challenges-solution

## Example: Copy data into a new, bigger array

Here, a user provides us with inputs, and we store whatever they enter into an array.

```java
String[] veggies = new String[1]; // start with an array to hold just one value
Scanner scn = new Scanner(System.in);
boolean keepGoing = true;
while (keepGoing) {
    System.out.println("Please enter a vegetable you like: ");
    String response = scn.nextLine();
    veggies[veggies.length-1] = response; // add the user's response to the last spot in the array
    if (response.equals("stop")) {
        keepGoing = false;
    }
    else {
        String[] newVeggies = new String[veggies.length + 1]; // create a new array one bigger than the last
        for (int i=0; i < veggies.length; i++) {
            newVeggies[i] = veggies[i]; // copy each value from the old array to the new
        }
        veggies = newVeggies; // reassign the variable to point to the new longer array
    }
}
System.out.println(Arrays.toString(veggies));
```

---

template: challenges

## Another way: Use Apache Commons Lang's ArrayUtils

All of this was very tedious! *Question*: Can we do better?

--

*Answer*: Yes, we can. We can use another utility class developed for Arrays: [Apache Commons Lang](https://commons.apache.org/proper/commons-lang/)'s `ArrayUtils` class.

--

To use it, download and install the Commons Lang library `.jar` file into a project's dependencies directory (often the `lib` directory) and then import it using `import org.apache.commons.lang3.ArrayUtils;`

```java
int[] fibb = {0, 1, 2, 3, 5, 8};
fibb = ArrayUtils.add(fibb, 13);
System.out.println(Arrays.toString(fibb)); // outputs "[0, 1, 2, 3, 5, 8, 13]"
```

--

Note that this technique only works with arrays of primitive data types.

---

name: arraylist

# ArrayList Class

--

## Overview

The `ArrayList` class, part of the `java.util` package, gives programmers a more dynamic array-like experience than what primitive arrays can do.



- an `ArrayList` does not have a fixed length.

--

- an `ArrayList` can have new members added to it at any time.

--

- an `ArrayList` can have existing members removed from it at any time.

--

- `ArrayList` is not a primitive data type or data structure in Java.

--

- `ArrayList` is a reference type, as are all non-primitive data types or data structures.

---

template: arraylist

## Example

```java
ArrayList<String> veggies = new ArrayList<String>(); // initialize an ArrayList that will hold Strings
veggies.add("avocado"); // add avocado (a fruit) to our list of vegetables
veggies.add("tomato"); // add tomato (a fruit) to our list of vegetables
veggies.add("crispy lettuce"); // add crispy lettuce to our list of vegetables
veggies.add("ketchup"); // add ketchup (a sweetened condiment) to our list of vegetables
veggies.add("bacon"); // add bacon (an animal product) to our list of vegetables
veggies.remove("avocado"); // remove avocado from our list of vegetables
int pos = veggies.indexOf("ketchup"); // returns 3, since "ketchup" is at position 3
String sweetStuff = veggies.get(pos); // returns "ketchup", which is at position 3
```

--

The example above shows some of the most useful methods in the `ArrayList` class.

--

See the [full set of methods in ArrayLists](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html).

---

template: arraylist

## The veggies example, revisited

Here, a user provides us with inputs, and we store whatever they enter into an array.

```java
ArrayList<String> veggies = new ArrayList<String>(); // create a blank ArrayList
Scanner scn = new Scanner(System.in);
boolean keepGoing = true;
while (keepGoing) {
    System.out.println("Please enter a vegetable you like: ");
    String response = scn.nextLine();
    if (response.equals("stop")) {
        keepGoing = false;
    }
    else {
        veggies.add(response); // add what the user entered into the ArrayList
    }
}
System.out.println(veggies);
```

--

Compare this to performing the same task [using primitive arrays](#challenges-solution).

---

name: pass-by-value

# Value and reference types

--

We've talked a lot about primitive, non-primitive and reference data types.

--

What happens when we pass a primitive, non-primitive or reference argument to a method?

--

For example, what happens if we give an array as an argument to a method versus, say, an integer?

--

Let's slow down a little to consider this...

---

template: pass-by-value
name: pass-by-value-2

## Primitives are value types

When we pass a _value type_ (e.g., a primitive data type value) argument to a function, the situation is easy.

--

- A copy of the argument's _value_ is passed to the function.
- Primitive values are called '**value types**' for this reason.

---

template: pass-by-value
name: pass-by-value-3

```java
public static void doSomething(int x) {
    x = 10;
}
public static void main(String[] args) {
    int x = 5;
    doSomething(x); // the value 5 is passed to the function
    System.out.println(x);
}
```

The output of the above program is `5`, since the local variable within the main function is never reassigned to refer to anything other than 5.

- `doSomething()` is invoked and passed a copy of the value `5` (the value of the main function's local variable `x`).
- `doSomething()` creates its own local parameter variable `x` which refers to this value, `5`.
- `doSomething()` reassigns its local variable `x` to refer to `10` instead.
- `doSomething()` completes and control flows back to the main method, where the local variable `x` still is assigned the value `5`.

---

template: pass-by-value
name: pass-by-value-5

When we pass a _reference type_ (e.g., an array or object) argument to a function, the situation is easy.

```java
public static void doSomething(int[] x) {
    x = {25, 30, 35}; // the local variable is re-assigned to point to a different memory address
}
public static void main(String[] args) {
    int x[] = {5, 10, 15, 20};
    doSomething(x); // the memory address of the array is passed to the function
    System.out.println( Arrays.toString(x) );
}
```

The output of this program is `[ 5, 10, 15, 20 ]`, since the local variable within the main function is never reassigned to refer to anything other than that array, and that array has never had its contents modified.

---

template: pass-by-value
name: pass-by-value-4

## Arrays and objects are reference types

When we pass an _array_ or an _object_ argument to a function, the situation is not so easy.

- A copy of the argument's _reference_ - the **memory address** at which the array or object is stored - is passed to the function.
- Important: The values encapsulated within the array or object are NOT passed to the function.
- Arrays and objects are called '**reference types**' for this reason.

---

template: pass-by-value
name: pass-by-value-6

## Arrays and objects are reference types (continued)

But consider the following example:

```java
public static void doSomething(int[] x) {
    x[2] = 555; // the third spot within the array is re-assigned to refer to a different integer
}
public static void main(String[] args) {
    int x[] = {5, 10, 15, 20};
    doSomething(x); // the memory address of the array is passed to the function
    System.out.println( Arrays.toString(x) );
}
```

The output of the above program is `[ 5, 10, 555, 20 ]`, since the local variable within the doSomething function is an alias of the variable within the main function - they both refer to the same array in the same memory location and that array's inner values have been modified.

--

The trick to this is that the **references are themselves passed as values** - the value being the integer memory address at which the array or object resides.

--

**Warning**: You'll encounter this soon in future assignments and CS 102. :-)
