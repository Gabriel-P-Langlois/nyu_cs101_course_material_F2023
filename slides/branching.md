---
layout: presentation
title: Branching
permalink: /slides/branching/
---

class: center, middle

# Branching

---

# Announcements

TBA.
---

# Agenda

1. [Overview](#concept)
2. [Flow Charts](#flow_charts)
4. [Boolean variables](#boolean)
5. [If/Else if/Else](#ifs)
6. [Switch/Case](#switch-case)
7. [The Ternary Operator](#ternary)

---

name: concept

# Overview

---

template: concept

## Concept

In computer science, [control flow](https://en.wikipedia.org/wiki/Control_flow) is the order in which individual statements, instructions, or function calls of a program are executed or evaluated. 

We can change the control flow of a program to deviate it from its '_normal_' path.

--

What is a program's 'normal' path?

--

- By default, a program will execute statements in the order written, from top to bottom.

- Some branches are _unconditional_ - the control will always break out of this sequential flow every time the program is executed.

- Other branches are _conditional_ - certain conditions must be met if the control of the program is to break out of its usual flow.

---

name: flow_charts

# Flow Charts

---

template: flow_charts

## Concept

We can visualize the control flow of a program using `flow diagrams`, irrespective of the programming language and code.

--

- Writing code is precarious, laborious, and error-prone.

- Creating flow diagrams can help understand and communicate the problem being solved without such burden.

--

- The [Unified Modeling Language](https://en.wikipedia.org/wiki/Activity_diagram) (UML) has attempted to define the "Activity Diagram" - a standard for how such diagrams should be drawn.

- In practice, people often use parts of the UML Activity Diagram style mixed with their own personal styles.

---

template: flow_charts

## Example

A virtual card game program randomly picks two cards, from 1 to 11.

- If those two cards add up to 21, the program outputs the text "Blackjack!"
- Otherwise, the program outputs the text, "Maybe next time!"

---

template: flow_charts

## Example

![Blackjack example diagram](../files/selections_blackjack_card_draw.png)

---

template: flow_charts

## UML Activity Diagram Rules

UML Activity Diagrams follow a few basic rules:

--

- The control flow starts at the top of the diagram and ends at the bottom.

--

- The start point is indicated with a **filled circle**, the end is indicated with a **filled circle with a line around it**.

--

- Any process is indicated with an **ellipse** or a **rounded rectangle**.

--

- If any process being diagrammed is so complex that it makes the diagram difficult to understand, make a separate activity diagram for that sub-process, and represent it as a single process in this diagram.

--

- Any decision point leading to more than one branch is indicated with a **rhombus** (diamond shape).

--

- Branches should have simple annotations indicating in what decision context they are followed.

---

name: boolean

# Boolean expressions

---

template: boolean

## Some history

The most important primitive data type in Java is **boolean** ('true' and 'false).

These are exactly the values if you want your program to make decisions!

--

The name boolean comes from the English mathematician **George Boole** who in 1854
wrote a book entitled `An Investigation into the Laws of Thought, on Which are Founded the
Mathematical Theories of Logic and Probabilities`.

That book introduced a system of logic that has come to be known as Boolean algebra, which
is the foundation for the boolean data type.

---

template: boolean

## Boolean operators

Boolean operators fall into two categories: **relational** and **logical** operators.

There are six relational operators that compares values of other types and produce a boolean's result:
 - `==` equals
 - `<` less than
 - `>` greater than
 - `!=` not equal
 - `<=` lesser than or equal to
 - `>=` greater than or equal to

For example, the expression `n<=10` has the value `true` if x is less
than or equal to 10 and the value `false` otherwise.

---

template: boolean

## Boolean operators

There are three logical operators:
 - `&&` Logical `AND`
 - `||` Logical `OR`
 - `!` Logical `NOT`

For instance:
 - `p && q` means both `p` and `q`.
 - `p || q` means either `p` or `q` (or both).
 - `!p` means the opposite of p.

---

template: boolean

## More on Boolean operators

Remember: Java uses `=` to denote assignments. To test whether two values are equal, you must use the `==` operator.

--

Java does not allow using more than one relational operator at a time.
 - For instance, the inequality `0 <= x <= 9` must be written in Java as
 - `0 <= x && x <= 9`.

--

The operator `||` means `either` or `both`, which is not always clear in the English interpretation of `or`.

---

template: boolean

## Short-circuit evaluation

--

Java evaluates `&&` and `||` using a strategy called short-circuit mode in which it evaluates the right operand only
if it needs to do so.

For example, if n is 0, the right hand operand of `&&` in

```java
n != 0 && x % n == 0
```

is not evaluated because `n != 0` is false.

--

One of the advantages of short-circuit evaluation is that you can use `&&` and `||`
to prevent execution errors. If n were 0 in the earlier example, evaluating `x % n` would cause a
“division by zero ” error.

---

template: boolean

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: ifs

# If/Else if/Else

---

template: ifs

## Isolated ifs

_if_ statements on their own either execute a particular branch or not.

```java
int card1 = (int) (Math.random() * 11) + 1; // number from 1 to 11
int card2 = (int) (Math.random() * 11) + 1; // number  from 1 to 11

if (card1 + card2 == 21) {
    // if the cards add up to 21...
    System.out.println("Blackjack!");
}
```

---

template: ifs

## Binary choice

_if_ statements followed by _else_ blocks can have control flow into one of two branches, depending on a single condition being met or not.

```java
int card1 = (int) (Math.random() * 11) + 1; // number from 1 to 11
int card2 = (int) (Math.random() * 11) + 1; // number  from 1 to 11

if (card1 + card2 == 21) {
    // if the cards add up to 21...
    System.out.println("Blackjack!");
}
else {
    // otherwise...
    System.out.println("Maybe next time!");
}
```

---

template: ifs

## n-ary

_if_ statements followed by one or more _else if_ blocks can have control flow into one of several different branches, depending on multiple conditions.

```java
int card1 = (int) (Math.random() * 11) + 1; // number from 1 to 11
int card2 = (int) (Math.random() * 11) + 1; // number  from 1 to 11

if (card1 + card2 == 21) {
    // if the cards add up to 21...
    System.out.println("Blackjack!");
}
else if (card1 == 1 && card2 == 1) {
    // otherwise if the cards are both ones...
    System.out.println("Snake eyes!");
}
else {
    // otherwise...
    System.out.println("Maybe next time!");
}
```

---

template: ifs

## UML Activity Diagram

![Blackjack example diagram](../files/selections_blackjack_card_draw_three_branches.png)

---

name: switch-case

# Switch/Case

---

template: switch-case

## Concept

In Java, an alternative to if/else if/else statements is switch/case statements.

- these can be easier to read and write in particular situations.

- such as when the branch followed depends upon the value of a single variable

- and when multiple conditions lead to the same branch

---

template: switch-case

## Example

Imagine a program that recommends how to dress.

![UML activity diagram for weather program](../files/selections_switch_weather.png)

---

template: switch-case

## Using switch / case

Using switch/case would remove the need for boolean operations and provide more readable code.

```java
Scanner scn = new Scanner(System.in);
String weather = scn.nextLine();

switch (weather) {
    case "raining":
    case "very sunny":
        // if it's raining or very sunny...
        System.out.println("Take an umbrella!");
        break;
    case "snowing":
        // otherwise, if it's snowing...
        System.out.println("Wear a hat!");
        break;
    default:
        // otherwise...
        System.out.println("Good luck!");
}
```

---

template: switch-case

## Not using switch / case

This could be handled by if/else if/else statements with some boolean operators thrown in.

```java
Scanner scn = new Scanner(System.in);
String weather = scn.nextLine();

if ( weather.equals("very sunny") || weather.equals("raining") ) {
    // if it's raining or very sunny...
	System.out.println("Take an umbrella");
}
else if (weather.equals("snowing") ) {
    // otherwise, if it's snowing...
	System.out.println("Wear a hat!");
}
else {
    // otherwise...
	System.out.println("Good luck!");
}
```

---

name: ternary

# The Ternary Operator

---

template: ternary

## Concept

It is often the case that we use if/else statements to control setting the value of a variable.

```javascript
if (breakfastWasServed && breakfastWasEaten) {
  satiationLevel = "full";
} else {
  satiationLevel = "hungry";
}
```

The ternary operator, `?`, thankfully allows us to simplify such syntax:

```javascript
satiationLevel = breakfastWasServed && breakfastWasEaten ? "full" : "hungry";

---

template: ternary

<div align="center">
<span style="color: red;">Practice round</span> </div>

---
