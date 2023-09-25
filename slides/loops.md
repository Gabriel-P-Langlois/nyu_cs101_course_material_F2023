---
layout: presentation
title: Loops
permalink: /slides/loops/
---

class: center, middle

# Loops

> "History doesn’t repeat itself but it often rhymes"
>
> -Attributed mistakenly to [Mark Twain](https://en.wikipedia.org/wiki/Mark_Twain)

---

# Agenda

1. [Overview](#concept)
1. [While Loops](#while)
1. [For Loops](#for)
1. [do..while](#dowhile)
1. [Some Common Tasks](#common)

---

name: concept

# Overview

---

template: concept

## Concept

It is often useful to repeat a block of code more than once.

- Loops provide a way to write code `once` and indicate insturctions for how many iterations it should be repeated.

- Better that than copy/paste the same code multiple times in a sequence!

---

name: while

# While Loops

---

template: while

## Concept

While loops give us ultimate flexibility in controlling repetition.

- We can easily set up counter-based loops known as **accumulators** or loops based on the value in flag variables called **sentinels**.

- We can also write infinite loops that never stop repeating.

--

```java
while(condition) {
    // statements to be repeated
}
```

---

template: while

## Accumulator-based loop

One of the classic patterns, where a counter stops the loop after a certain number of iterations.

This is the **Repeat-N-Times** Idiom.

```java
int i = 0; // set the starting value of the counter
int N = 10; // set the how many iterations we wish to perform

while (i < N) {
    // iterate as long as the counter is below some target value
    System.out.println("The value of i is" + i);
    i++; // increment the counter -- equivalent to i = i + 1;
}
```

---

template: while

## Flag-based loop

Another classic pattern, where the value of a boolean variable causes the loop to stop iterating at some point.

This is the **Repeat-Until-Sentinel** Idiom.

```java
boolean sentinel = true; // This is the sentinel (a.k.a. the flag).

while (sentinel) { // by default, iterate.
    // iterate as long as the boolean value in the flag is true
    System.out.println("Iterating...");

    // stop the loop if a random number between 1-100 is equal to 22
    int rand = (int) (Math.random() * 100) + 1;

    // use the ternary operator to flip the value of the flag, if necessary
    sentinel = (rand == 22) ? false : true; // set to false if the rand value is 22, true otherwise
}
```

---

template: while

## Infinite loop

Usually undesireable, but while loops can iterate infinitely.

```java

while (true) {
    // iterate forever... until the user quits the program or the computer shuts it down
    System.out.println("Iterating!");
}
```

In Visual Studio Code, press CTRL + P and type `>task terminate` to stop the execution of the program and get out of the infinite loop.

---

name: for

# For Loops

---

template: for

## Concept

For loops allow us to simplify the syntax for writing an 'accumulator'- or 'counter'-based loop.

- The accumulator pattern is baked into the `for` loop syntax.

- A `for` loop can be set to terminate based on a flag's value, but its syntax is not designed for that.

- A `for` loop can be set to run infinitely, but its syntax is not designed for that.

---

template: for

## Accumulator-based loop

One of the classic patterns, where a counter stops the loop after a certain number of iterations.

- this is what `for` loops were designed to do!

```java
for (int i = 0; i < 10; i++) {
    // iterate as long as the counter is below some target value
    System.out.println("The value of i is" + i);
}
```

---

template: for

## Flag-based loop

Another of the classic patterns, where the value of a boolean variable causes the loop to stop iterating at some point.

- `for` loops are almost never used for this... but here we go!

```java
boolean keepGoing = true; // by default, iterate!

for (; keepGoing ;) {
    // iterate as long as the boolean value in the flag is true
    System.out.println("Iterating!");

    // stop the loop if a random number between 1-100 is equal to 22
    int rand = (int) (Math.random() * 100) + 1;

    // use the ternary operator to flip the value of the flag, if necessary
    keepGoing = (rand == 22) ? false : true; // set to false if the rand value is 22, true otherwise
}
```

---

template: for

## Infinite loop

Usually undesireable, but for loops can iterate infinitely.

```java

for (; ;) {
    // iterate forever... until the user quits the program or the computer shuts it down
    System.out.println("Iterating!");
}
```

---

template: for

## Equivalent statements

The statements below are equivalent:

```java
int s = 0;
for (i = 0; i < N; ++i) {
    s += i;
}
```

```java
i = 0;
s = 0;
while (i < N) {
    s += i;
    ++i;
}
```

---

name: dowhile

# Do..while statement

---

template: dowhile

You can use a `do...while` statement to check a certain condition only after executing the repeating statements

```java
do {
    // statement 1
    // statement 2
    // ...
} while(sentinel);
```

Important: The statements will always be executed once, and even so if `sentinel` is `false`!

---

name: common

# Some Common Tasks

---

template: common

## Iterating through values in an array

```java
// an array of strings
String[] messages = {
        "hi",
        "how are you?",
        "how's it going?",
        "good to see you!",
        "have a great day!",
        "hope to see you around :)"
};

// classic for loop that iterates as many times as there are elements in the array
for (int i=0; i<messages.length; i++) {
    // print out the value at each position in the array
    System.out.println("The value in the array at index " + i + " is: " + messages[i]);
}
```

---

template: common

## Iterating until a specific response is received from a user

```java
Scanner scn = new Scanner(System.in); // open the scanner outside the loop, since we could potentially need to get more than one int of input
keepGoing = true; // set the flag to true so this loop will at least iterate once
while (keepGoing) {
    // get user input
    System.out.print("Please enter an integer between 1 and 10: ");
    int num = scn.nextInt();

    // validate the user's input
    if (num >= 1 && num <= 10) {
        keepGoing = false; // change the value of the flag to cause the loop to terminate
        System.out.println("Thanks for the good input!... quitting loop");
    }

    // if the user's input is invalid, x is still true, so no need to set it to that!
}
scn.close(); // close the scanner resource to be nice to the processor
```

---

template: common

## Iterating through the characters in a string

In Java, strings contain arrays of `char` values. Note that the length of a string is obtained using the `length()` function, not the `length` property used with arrays.

```java
String s = "asparagus";
for (int i = 0; i < s.length(); i++) {
    char c = s.charAt(i);
    System.out.println(c);
}
```

---

template: common

## Calculating a running total

```java
Scanner scn = new Scanner(System.in);

int total = 0; // start the total at zero
String stop_response = "stop"; // what the user must type in order to stop the loop
String users_response = ""; // will hold what the user types in each iteration

// keep looping until the user types 'stop'
while (!users_response.equals(stop_response)) {
    System.out.println("Enter a number: "); // ask for a number
    users_response = scn.nextLine(); // get the user's response as a string
    try {
        int val = Integer.parseInt(users_response); // convert the respose to an int
        total = total + val; // add it to the running total
    }
    catch (Exception e) {
        // if the user types a non-integer, an error will be caught here
        System.out.println("Sorry, that's not a valid number");
    }
}
System.out.println("The total is " + total);
```
