---
layout: presentation
title: Arrays
permalink: /slides/arrays/
---

class: center, middle

# Arrays

---

# Agenda

Part I: One-dimensional arrays; Utility classes for arrays
1. [Overview](#concept)
1. [Creation](#creation)
1. [Array Length](#length)
1. [Arrays Utility Class](#arrays-class)
1. [Value and reference types](#pass-by-value)


Part II: Manipulating arrays in Java; The ArrayList class; Multidimensional arrays

1. [Challenges with manipulating arrays in Java](#challenges)
1. [ArrayList Class](#arraylist)
1. [Multidimensional arrays: Overview](#concept-ma)
1. [The truth about multidimensional arrays](#truth)
1. [Ragged multidimensional arrays](#ragged)
1. [Rows & Columns](#rows-columns)

---

name: overview

# Overview

Formally, an array in Java is a *non-primitive* data type used to store multiple values of the same data type.

--

```java
int[] firstFiveFibonnaciNumbers = new int[5];

firstFiveFibonnaciNumbers[0] = '1';
firstFiveFibonnaciNumbers[1] = '1';
firstFiveFibonnaciNumbers[2] = '2';
firstFiveFibonnaciNumbers[3] = '3';
firstFiveFibonnaciNumbers[4] = '5';
```

Arrays can store *any* data type or structure... 

... as long as they are all the *same* type!

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

--

- In this case, Java knows that each `char` value consumes 16 bits, so it reserves enough memory space for 3 of them.

- The length of the array **cannot** be modified once memory has been allocated for an array of a specific length.

---

template: creation
name: creation-2

## Second way: Using syntactic sugar

Arrays can be created using shorthand syntax:

```java
char[] myFavoriteCharacters = { 'f', 'o', 'o' };
```
--

- This is useful if you know what values you want to put into the array.

- Note that both operations, declaring the variable and allocating and populating the array, must be done in one statement with this style.

---

template: creation
name: creation-3

## Third way (for Strings): Using String's split function

Arrays can be made from text that contains a particular separator.

```java
String myMessageToYou = "Don't worry about a thing";
String[] words = myMessageToYou.split(" ");
// now you have an array { "Don't", "worry", "about", "a", "thing" }
```

--

You can use [regular expressions syntax](https://docs.oracle.com/javase/tutorial/essential/regex/) to split a string using one of several separators:

```java
String myMessageToYou = "Don't, worry?about-a .thing";
String[] words = myMessageToYou.split("[ ,?-.]+");
// .split("[ ,?-.]+") means: split the string if you encounter *any* combination of " " or "," or "?" or "-" or "."
// In this example, the split method will encounter the comma and a space before encountering the charater 'w'. Thus it will parse out
// "Don't" from the delimiter ", ". split will then proceed from the rest of the string "worry?about-a .thing"".
// now you have an array { "Don't", "worry", "about", "a", "thing" }
```

--

**Warning**: You *will* have to use this in a future assignment!

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

Remember: Arrays in Java have **fixed length**. New positions cannot be added, and existing positions cannot be removed from an array.

---

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: arrays-class

# Java's native Arrays Utility Class

--

## Useful functions for arrays

While an array is *not* a primitive data type in Java, we nonetheless have access to different methods and utilities for arrays through the *Arrays utility class*.

--

Use `import java.util.Arrays` to invoke the library.

--

We'll discuss:

- Converting the contents on array into a string
- Comparing the values of two arrays
- Copying an array
- Searching an array
- Sorting an array

---

template: arrays-class
name: arrays-class-2

## Converting an array's contents into a String

The method `Arrays.toString()` prints out the array's contents.

- Inelegant, but good for debugging.

```java
String[] arrVar = { "hello", "and", "good", "morning" };
String contents = Arrays.toString(arrVar); // -> "[hello,and,good,morning]"
System.out.println(contents);
```

--

For multi-dimensional arrays (next class), use `.deepToString()`:

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

The method `Arrays.equals()` determines whether two arrays have the same set of values:

```java
String[] arrVar1 = { "hello", "and", "good", "morning" };
String[] arrVar2 = { "hello", "and", "good", "morning" }; // a separate array with the same values as arrVar1 but at a different location in memory
boolean sameValues = Arrays.equals(arrVar1, arrVar2); // -> true!
```

--

For multi-dimensional arrays (next class), use `.deepEquals()`:

```java
String[][] arrVar1 = { {"hello", "world"}, {"goodbye", "world"} }; // a two-dimensional array
String[][] arrVar2 = { {"hello", "world"}, {"goodbye", "world"} }; // a separate array with the same values as arrVar1 but at a different location in memory

boolean sameValues = Arrays.deepEquals(arrVar1, arrVar); // -> true!
```

**Warning**: Do *not* use the comparison operator `==` for this.

---

template: arrays-class
name: arrays-class-6

## Copying an array

The method `Arrays.copyOf()` copies the specified array, truncating or padding if necessary:

```java
int org[] = {1,2,3,4};
int[] copy1 = Arrays.copyOf(org, 4);
int[] copy2 = Arrays.copyOf(org, 2);
int[] copy3 = Arrays.copyOf(org, 5);

System.out.println(copy1);
System.out.println(copy2);
System.out.println(copy3);
```

--

name: arrays-class-copy

Use `.copyOfRange()` to clone a subset of the values in an array:

```java
int startIndex = 0;
int endIndex = 3;
int[] copy = Arrays.copyOfRange(arrVar, startIndex, endIndex);
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

---

template: arrays-class
name: arrays-class-4

## Sorting the values in an array

The method `Arrays.sort()` sorts an array (by default, in ascending order):

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

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: pass-by-value

# Value and reference types

--

We've discussed primitive (e.g., int, char...) and non-primitive (e.g., Strings, Arrays...) data types.

--

What happens when we pass a primitive or non-primitive argument to a method?

--

Let's slow down a little to consider this...

---

template: pass-by-value
name: pass-by-value-2

## Primitives are value types

This situation is easy when we pass a _value type_ (e.g., a primitive data type value) argument to a function.

--

- A copy of the argument's _value_ is passed to the function.
- Primitive values are called '**value types**' for this reason.

--

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

The situation is not so easy when we pass a _reference type_ (e.g., an array) argument to a function...

```java
import java.util.Arrays;
public class array4{
    public static void doSomething(int[] x) {
        int[] y = {25, 30, 35, 40};
        x = y; // the local variable is re-assigned to point to a different memory address
    }

    public static void doSomethingElse(int[] x) {
    x[2] = 555; // the third spot within the array is re-assigned to refer to a different integer
    }

    public static void main(String[] args) {
       int x[] = {5, 10, 15, 20};
       doSomething(x);
       System.out.println(Arrays.toString(x));
       doSomethingElse(x);
       System.out.println(Arrays.toString(x));
    }
}
```

What happens?

---

template: pass-by-value
name: pass-by-value-4

## Arrays and objects are reference types

The first output (before we invoke doSomethingElse) is `[ 5, 10, 15, 20 ]`. Why? 
- The local variable within the main function is never reassigned to refer to anything other than that array.
- That array has never had its contents modified!

--

The second output (after we invoke doSomethingElse) is `[ 5, 10, 555, 20 ]`. Why?
- The local variable within the doSomething function is an alias of the variable within the main function.
- They both refer to the same array in the same memory location and its inner values have been modified.
- **Important**: The values encapsulated within the array or object are NOT passed to the function.
- Changing the value in the method changes it outside the method!

--

**Warning**: You'll encounter this soon in future assignments and CS 102. :-)
---

<div align="center">
<span style="color: red;">Practice round</span> </div>

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

A user provides inputs, and we store them in an array.

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

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: concept-ma

# Multidimensional arrays: Overview

---

template: overview
name: overview-1

## Concept

**Multidimensional arrays** store other arrays nested within them.

--

- An array that stores arrays is called a two-dimensional array

--

- An array that stores arrays that themselves store arrays is called a three-dimensional array

--

- An array that stores arrays that themselves store arrays that themselves also store arrays is called a four-dimensional array...

--

- ...and so on.

---

template: concept-ma
name: overview-2

## Two-dimensional example

Here's a two-dimensional array that stores inner arrays of type `int`.

--

Note the **two** sets of square brackets after the data type declaration.

```java
int[][] numbers = {
        { 10, 9, 8 },
        { 1, 2, 3 },
        { 6, 5, 4 },
};
```

---

template: overview
name: overview-3

## Two-dimensional example (continued)

To output the third value in the second inner array, which is 3, write

```java
System.out.println( numbers[1][2] );
```

--

The syntax to modify one of the values in a two-dimensional array is the same.

```java
// modify the third value in the second inner array
numbers[1][2] = 11;
```

--

The entire inner array can also be replaced with a different one.

```java
numbers[1] = { 13, 12, 11 };
```

---

template: concept-ma
name: overview-4

## Three-dimensional example

Here's a three-dimensional array that stores inner arrays of type `String`.

--

Note the **three** sets of square brackets after the data type declaration.

```java
String[][][] words = {
        {
            {"who", "what", "when", "why", "how"},
            {"whither", "whence", "wherefore"}
        },
        {
            {"there", "that", "then"},
            {"thence", "hence", "heretofore"}
        }
};
```

--

To output the third value in the second child array of the first inner array - 'wherefore'.

```java
System.out.println( words[0][1][2] );
```

---

name: truth

# Truth

--

## It's all a lie!

Multidimensional arrays do not exist in Java

--

In a true multidimensional array, all elements within the array occupy a continuous block of memory.

--

This is not the case in Java.

--

In Java, a two-dimensional array is actually an array of pointers, that is, references to other memory locations where the inner arrays are kept, separately from the outer array.

---

template: truth
name: truth-1d

## It's all a lie! (continued)

![the truth](../files/arrays-multidimensional-truth.png)

---

name: ragged

# Ragged Arrays

--

## Concept

Inner arrays may have different lengths... such arrays are called **ragged** arrays.

```java
int[][] numbers = {
        { 10, 9, 8, 7, 6 },
        { 1, 2 },
        { 6, 5, 4, 4, 3, 2, 1 }
};
```

---

template: ragged
name: ragged-2

## Without syntactic sugar

When not using array syntactic sugar, it is possible to leave the length of all but the first dimension blank in the allocation statement to allow for ragged arrays.

```java
int[][] numbers = new int[3][]; // blank second dimension

// now populate each inner array with whatever length you prefer
numbers[0] = new int[] { 10, 9, 8, 7, 6};
numbers[1] = new int[] { 1, 2 };
numbers[2] = new int[] { 6, 5, 4, 4, 3, 2, 1 };
```

---

name: rows-columns

# Rows & Columns

--

## Concept

It is best to think of two-dimensional arrays as rows and columns of data, like a spreadsheet or table.

- It is helpful to even write each row on a separate line and align the columns

```java
String[][] naughtsAndCrosses = {
    { "X", "O", "X" }, // first row
    { "X", "O", "X" }, // second row
    { "X", "O", "X" }  // third row
};
```

---

template: rows-columns
name: rows-columns-2

## Looping through rows with syntactic sugar

To loop through each row, remember that each row of a two-dimensional array is itself a one-dimensional array.

Using `for` loop syntactic sugar.

```java
// iterate through each row in the outer array
for (String[] row : naughtsAndCrosses ) {

    // print out the row
    System.out.println( Arrays.toString(row) );

}
```

---

template: rows-columns
name: rows-columns-3

## Looping through rows with a counter

If you insist on using an accumulator-style `for` loop, that also works, of course.

Using `for` loop accumulator syntax.

```java
// iterate through each index value in the outer array
for ( int i=0; i<naughtsAndCrosses.length; i++ ) {

    // get the row at this index
    String[] row = naughtsAndCrosses[i];

    // print out the row
    System.out.println( Arrays.toString(row) );

}
```

---

template: rows-columns
name: rows-columns-4

## Looping through each column within each row

It's easy enough to iterate through each column within each row.

- Recall that each value in the inner array - each column - is a String.

Using `for` loop syntactic sugar syntax.

```java
// iterate through each row in the outer array
for (String[] row : naughtsAndCrosses ) {

    // iterate through each column within the current wor
    for (String col : row) {

        // print out the column value
        System.out.print( col );

    }

}
```

---

template: rows-columns
name: rows-columns-5

## Looping through each column within each row (the hard way)

The same can be done without syntactic sugar

Using `for` loop accumulator syntax.

```java
// iterate through each index value in the outer array
for ( int i=0; i<naughtsAndCrosses.length; i++ ) {

    // get the row at this index
    String[] row = naughtsAndCrosses[i];

    // iterate through each index value of the inner array
    for (int j=0; j<row.length; j++) {

        // print out the column value
        System.out.println( row[j] );

    }

}
```

---

<div align="center">
<span style="color: red;">Practice round</span> </div>
