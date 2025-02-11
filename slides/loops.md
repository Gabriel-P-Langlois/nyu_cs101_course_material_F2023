---
layout: presentation
title: Loops
permalink: /slides/loops/
---

class: center, middle

# Loops

---

# Agenda

1. [Overview](#concept)
1. [While Loops](#while)
1. [For Loops](#for)
1. [do..while](#dowhile)

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

Important: The statements will always be executed once, even if `sentinel` is `false`!
