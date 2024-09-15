---
layout: presentation
title: Starter code, I/O using Scanner, data types, and arithmetic.
permalink: /slides/starter-code/
---

class: center, middle

# Starter code

---

# Agenda
Part I: Starter code; Input/Output (I/O) using the Scanner class; Variables and identifiers;
1. [Your first Java program](#starter-code) 
1. [Explaining your first Java program](#java-program-explained)
1. [A Java program with the Scanner class](#code-scanner) 
1. [More about the Scanner class](#input)
1. [Variables and identifiers](#variables-identifiers)

Part II: Data types; operators and operands (TBC.)
1. [Data types](#data-types)
1. [Operators and operands](#operators)
1. [A note about division and type casts](#division-type-casts)
1. [Assignment operators](#assignment)

---

# Things you need


You will need to have the [Java Development Kit](https://www.oracle.com/technetwork/java/javase/downloads/) (JDK) installed.

You will need the Eclipse IDE.

Note: You may use other IDEs or other text editors to write Java code, e.g., [Visual Studio Code](https://code.visualstudio.com). But if you intend to take the follow-up CSCI-102 course, you should know that some instructors require students to use Eclipse.

---

name: starter-code

# Your first Java program

---

template: starter-code

Launch Eclipse, and follow the instructions in the tutorial...

<div align="center">
<span style="color: red;">Live demo</span> </div>

---

name: java-program-explained

# Your first Java program explained

---

template: java-program-explained

```java
public class HelloWorld {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Hello World!");
	}
}
```

The first line defines a **class**.

Each Java program must have at least one class, and each class has a name.

--

- The name of our class is HelloWorld
- By convention, class names start with an uppercase letter.

Note: The class that contains the main method must match the name of the source file (HelloWorld.java)

---

template: java-program-explained

```java
public class HelloWorld {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Hello World!");
	}
}
```

The second line defines the **main method**.

A Java program is executed from the main method. It is the entry point where the program begins execution.

A method has a name (e.g., main) and contains a set of statements.

---

template: java-program-explained

```java
public class HelloWorld {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Hello World!");	
	}
}
```

`Public` , `Static` , `void`, `String` and `args` are called **reserved words**.

Each one of them has a specific meaning to the compiler... We will explain these words in detail as the course progresses.

---

template: java-program-explained

```java
public class HelloWorld {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Hello World!");
	}
}
```

The line `// put the main contents of your program below here` is a **comment**.

A comment documents information about the program.

Comments help programmers communicate and understand the program.

--

Note: Add comments to your programs! See this [website](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/) for best practices.

---

template: java-program-explained

```java
public class HelloWorld {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Hello World!");
	}
}
```

The statement `System.out.println` is a **Java statement**.

Here, `System.out.println` instructs the computer to display a message in the console.

The message displayed in the program is "Hello World!".

--

Note: Almost all statements in Java must end with a semicolon **;**.

---

name: code-scanner

# A Java program with the Scanner class

---

template: code-scanner

To receive keyboard input from a user, a Java program must import `java.util.Scanner`.

```java
import java.util.Scanner; // a predefined Java library for keyboard input

public class Welcome {
	public static void main(String[] args) {
		System.out.println("Enter your username:"); // prompt for input
		Scanner input = new Scanner(System.in);
		// the next line declares a String variable named "nextName" and
		// makes the input scanner reads the string. (input.next())
		String nextName = input.next();
		System.out.println("Welcome to Java Programming, " + nextName + "!");
		input.close(); // closing the input Scanner
	}
}
```

---

template: code-scanner

```java
import java.util.Scanner; // a predefined Java library for keyboard input

public class Welcome {
	public static void main(String[] args) {
		System.out.println("Enter your username:"); // prompt for input
		Scanner input = new Scanner(System.in);
		// the next line declares a String variable named "nextName" and
		// makes the input scanner reads the string. (input.next())
		String nextName = input.next();
		System.out.println("Welcome to Java Programming, " + nextName + "!");
		input.close(); // closing the input Scanner
	}
}
```

In Java, you must declare a variable before you can use it.

--

The declaration establishes the name and type of the variable.
- `Scanner` is the **type name**
- `input` is the **variable name**
- `new` is a **reserved** Java identifier (more on this later)
- `System.in` permits you to read input.

---

template: code-scanner

```java
import java.util.Scanner; // a predefined Java library for keyboard input

public class Welcome {
	public static void main(String[] args) {
		System.out.println("Enter your username:"); // prompt for input
		Scanner input = new Scanner(System.in);
		// the next line declares a String variable named "nextName" and
		// makes the input scanner reads the string. (input.next())
		String nextName = input.next();
		System.out.println("Welcome to Java Programming, " + nextName + "!");
		input.close(); // closing the input Scanner
	}
}
```
The **method** next() is used to get input from the user.

It reads the input until a space character (" ") is encountered.

---

template: code-scanner

```java
import java.util.Scanner; // a predefined Java library for keyboard input

public class Welcome {
	public static void main(String[] args) {
		System.out.println("Enter your username:"); // prompt for input
		Scanner input = new Scanner(System.in);
		// the next line declares a String variable named "nextName" and
		// makes the input scanner reads the string. (input.next())
		String nextName = input.next();
		System.out.println("Welcome to Java Programming, " + nextName + "!");
		input.close(); // closing the input Scanner
	}
}
```

**Demo**: Create a new java file (Welcome.java), compile it, and run it. 

Try using different inputs (e.g., username123, username 123, etc.)

---

name: input

# More about the Scanner class

---

template: input

## Scanner's built-in functions

Scanner has a few different functions for fetching the user input as different data types, e.g.:

`next()` - returns a `String` with the user's input up until a space(" ") is encountered.

`nextLine()` - returns a `String` with the user's input up to the newline (i.e. `\n`) character data type

`nextInt()` - returns an `int` with the user's input, if they entered an integer; otherwise crashes

`nextDouble()` - returns a `double` with the user's input, if they entered a number; otherwise crashes

---

template: input

## Example: Adding two integers

```java
import java.util.Scanner;

class AddingIntegers{
  public static void main(String[] args) {
    int x, y, sum;
    Scanner myObj = new Scanner(System.in);
    
    System.out.println("Type a number:");
    x = myObj.nextInt(); // Read user input

    System.out.println("Type another number:");
    y = myObj.nextInt(); // Read user input

    sum = x + y;  // Calculate the sum of x + y
    System.out.println("Sum is: " + sum); // Print the sum
  }
} 
```

Demo: Try it yourself!

---

template: input

Using `nextInt()` or `nextDouble()` with `nextLine()` can create complications. For example:

```java
import java.util.Scanner;

public class LookHowGreatJavaIs {
	public static void main(String[] args) {
		Scanner scnr = new Scanner(System.in);
		// get user's age
		System.out.println("Please enter your age: ");
		int ageAsInt = scnr.nextInt(); // an int
		// get user's name
		System.out.println("Please enter your name: ");
		String name = scnr.nextLine(); // a String
		// print out a friendly welcome message
		System.out.println("Welcome, " +  name + "! You are " + ageAsInt/7 + " years old in dog years!");
		scnr.close(); // close the Scanner to conserve resources
	}
}
```

--

This program will always print `Welcome, !` no matter what give as input...

---

template: input

One way to avoid this is to use `nextLine()` for all input and then convert the String it returns to other data types.

```java
import java.util.Scanner;

public class StickToScanningStrings {
    public static void main(String[] args) throws Exception {
		Scanner scnr = new Scanner(System.in);
		// get user's age
		System.out.println("Please enter your age: ");
		String ageAsString = scnr.nextLine(); // a String... avoid nextInt() and nextDouble!
        int ageAsInt = Integer.parseInt(ageAsString); // and for doubles use Double.parseDouble(age)
		// get user's name
		System.out.println("Please enter your name: ");
		String name = scnr.nextLine(); // a String
		// print out a friendly welcome message
		System.out.println("Welcome, " +  name + "! You are " + ageAsInt/7 + " years old in dog years!");
		scnr.close();
    }
}
```

---

name: variables-identifiers

# Variables and identifiers

---

template: variables-identifiers

## Variables

A **variable** is a placeholder for a value that can change as the program runs.

--

Think of a variable as a box containing a value.

--

Each variable has the following attributes:
- A name, which enables you to differentiate one variable from another.
- A type, which specifies what type of value the variable can contain.
- A value, which represents the current contents of a variable.

--

Note: The name and type of a variable are fixed, but the value changes whenever you assign it a new value.

---

template: variables-identifiers

## Identifiers

Names for variables (and other things) are called **identifiers**.

--

Identifiers in Java conform to certain rules:
- A variable name must begin with a letter or the underscore letter.
- The remaining characters must be letters, digits, or underscores.
- The name must NOT be one of Java's [reserved words](https://en.wikipedia.org/wiki/List_of_Java_keywords).
- Identifiers should make their purpose obvious to the reader.

---

template: variables-identifiers

## Variable declarations

In Java, you must declare a variable before you can use it.

The declaration establishes the name and type of the variable and, in most cases, specifies the initial value as well.

The most common form of a variable declaration is

```java
type_name = value; // int z = 10;
```

---

name: data-types

# Data types

--

## Overview

Java natively supports 8 fundamental [primitive data types](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html):

- `byte` = 8-bit signed integer
- `short` = 16-bit signed signed integer
- `int` = 32-bit signed integer (**the default** for integer literals)
- `long` = 64-bit signed floating-point number
- `float` = 32-bit floating point floating-point number
- `double` = 64-bit floating point number (**the default** for floating point literals)
- `char` = 16-bit Unicode character code
- `boolean` = 1-bit true (1) or false (0) value

---

template: data-types

**Byte**:
- Byte data type is an 8-bit signed two's complement integer.
- Minimum value is -128 (-2^7).
- Max value is 127 (2^7 - 1).
- Default value is 0.
- Byte data type is used to save space in large arrays (a byte is four times smaller than an int).
- Example: byte a = 100;

![starter-kit](../files/sign_and_magnitude_byte.png)

---

template: data-types

**float**:
- float data type is a single-precision 32-bit IEEE 754 floating point.
- IEEE stands for `Institute of Electrical and Electronics Engineers`.
- Float is used to save memory in large arrays of floating point numbers.
- Default value is 0.0f.
- Don't use it if you need precise value! Use BigDecimal instead.
- Example: float f1 = 234.5f;
- Example: BigDecimal k = BigDecimal.valueOf(floatvalue);

![starter-kit](../files/float32.png)

---

template: data-types

**Short**:
- Short data type is a 16-bit signed two's complement integer.
- Minimum value is -32,768 (-2^15).
- Max value is 32,767 (2^15 - 1).
- Default value is 0.
- Short data type can also be used to save memory.
- Example: short s = 10000;

**long**:
- long data type is a 64-bit signed two's complement integer.
- Minimum value is -9,223,372,036,854,775,808 (-2^63).
- Max value is 9,223,372,036,854,775,807 (2^63 - 1).
- Default value is 0L.
- This type is used when a wider range than int is needed.
- Example: long a = 100000L;

---

template: data-types

**int**:
- int data type is a 32-bit signed two's complement integer.
- Minimum value is -2,147,483,648 (-2^31).
- Max value is 2,147,483,647 (2^31 - 1).
- Default value is 0.
- **Generally the default data type for integers**.
- Example: int a = 100000;

**double**:
- double data type is a double-precision 64-bit IEEE 754 floating point.
- **Generally the default data type for decimal values**.
- Default value is 0.0d.
- Don't use it if you need precise value! Use BigDecimal instead.
- Example: double d1 = 123.4;
- Example: BigDecimal k = BigDecimal.valueOf(doublevalue);

---

template: data-types

**char**:
- char data type is a single 16-bit Unicode character.
- Minimum value is `\u0000` (or 0).
- Maximum value is `\uffff` (or 65,535).
- char data type is used to store any character.
- Example: char letterA = 'A';

**boolean**:
- boolean data type represents one bit of information.
- There are only two possible values: true and false.
- This data type is used for simple flags that track true/false conditions.
- Default value is false.
- Example: boolean one = true;
- (More on this next class!)
---

template: data-types

## Overview (continued)

There is no `String` primitive data type in Java. Instead, `String` is a predefined class that is written in Java code.

There is no `Arrays` primitive data type in Java. Instead, `Arrays` is a predefined class that is written in Java code.
- It is a fundamental data structure in Java (more on this later in the course).

Because Java contains primitive data types that are not only `class` types, _Java is not a purely object-oriented language_.

---

template: data-types

## Utility/Helper/Wrapper classes

The **Java API** (Application Programming Interface) is a set of `classes` written in Java that are distributed with Java.

It offers a set of utility classes to help manipulate data of the fundamental primitive data types and structures.

- `Byte`
- `Short`
- `Integer`
- `Long`
- `Float`
- `Double`
- `Character`
- `Boolean`
- `String`
- `Arrays`

These are helpful when converting the value of one data type to another!

---

template: data-types

## Utility/Helper/Wrapper classes (continued)

Utility classes contain useful methods for manipulating the types of data usually stored as fundamental primitive data types.

They are often called "wrapper" or "helper" classes because they offer additional functionality built around primitive data types.

These are **fully-objected-oriented** correlates of the fundamental primitive data types.

---

template: data-types

## Utility/Helper/Wrapper classes (continued)

Due to the limitations of working with primitive data types and the conservative nature of the Java API's included Utility/HelperWrapper/ classes, the [Apache Software Foundation](https://apache.org) sponsors a project called [Commons Lang](https://commons.apache.org/proper/commons-lang/) that aims to provide functionality that many programmers regret is not present in the Java API. This library includes additional helper classes, such as:

- `NumberUtils`
- `CharUtils`
- `BooleanUtils`
- `ArrayUtils`
- ... and [many more](https://commons.apache.org/proper/commons-lang/apidocs/index.html) for dealing with data of non-primitive types.

Commons Lang is perhaps most well-known for its `String`-related helper classes: `StringUtils`, `WordUtils`, and `StringEscapeUtils`.

---

template: data-types

## Converting data types

Double to String:

```java
String str = Double.toString(5.0);
```

Double to int:

```java
Double dbl = new Double(5.0);
int integer = dbl.intValue();
```

String to Double:

```java
double d = Double.valueOf(str).doubleValue();
// or
double d = Double.parseDouble(str);
```

---

template: data-types

## Converting data types

Integer to String:

```java
String str = Integer.toString(5);
// or
String str = ""  +  5;
```

String to Integer:

```java
int i = Integer.valueOf("5").intValue();
// or
int i = Integer.parseInt("5");
```

Char to String:

```java
String s = String.valueOf('c');
```

---

template: data-types

## Converting data types

Use **exception handling** to handle problems encountered while attempting to convert one data type to another.

```java
String aString = "foo bar baz bum"; //  a string that has no obvious int equivalent

try{
	// try to do the conversion...
	i = Integer.parseInt(aString); // will fail and produce an Exception
}
catch(NumberFormatException e) {
	// this block of code will run if there is a failure
	System.out.println(e); // will output the Exception but not crash the program
}
```

We'll talk more about exceptions later in the course.

---

template: data-types

## Converting data types

<div align="center">
<span style="color: red;">Practice round</span> </div>

---

name: operators

# Operators and operands

---

template: operators

Java specifies computation in the form of arithmetic expressions that closely resemble expressions in mathematics.

**Operators** usually appear between two subexpressions, which are called **operands**.

Common operators include:
- `+` Addition
- `-` Subtraction
- `*` Multiplication
- `/` Division
- `%` Remainder

Note: The `-` operator can also appear as a unary operator, as in the expression `-x`, which denotes the negative of `x`.

---

name: division-type-casts

# Division and type casts

---

template: division-type-casts

Consider the following Java codes, which intend to convert a Celsius temperature to its Fahrenheit equivalent:

```java
public class CelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9 / 5 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

**Demo**: Run the code. What do you observe?

---

template: division-type-casts

```java
public class CelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9 / 5 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

The problem is that both 9 and 5 are of type `int`, which means the result is also an `int`.

Thus 9 / 5 = 1 in Java (!)

You can fix this problem by converting the fraction to a double by inserting decimal points or using a `type cast`.

---

template: division-type-casts

```java
public class BetterCelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9.0 / 5.0 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

**Demo**: Try it now!

---

template: operators

## About the remainder operator

The remainder operator `%` applies only to integer operands.

It computes the remainder when the first is divided by the second:
- `14 % 5` returns 4.
- `14 % 7` returns 0.
- `7 % 14` returns 7.

This is a very useful operator!

---

template: operators

## Precedence

What if an expression contains more than one operator?

Java uses precedence to determine the order of evaluation.

From highest to lowest precedence:
- `unary - (type cast)`
- `* / %`
- `+ -`

Precedence applies only when two operands compute for the same operator.

**Note**: Use parentheses if you forget the precedence rule (or for clarity)!

---

name: assignment

## Assignment operators

---

template: assignment

You can change the value of a variable in your program by using an assignment statement: `variable = expression;`

--

The assignment statement computes the value of the expression on the right side of the equal sign and assigns that value to the variable that appears on the left.

--

Statements such as `x = x + value;` are so common that Java allows the following shorthand: `x += value;`.

--

The general form is `variable op = expression;`, where op is any of Java's binary operators.

--

Example: the following statement multiplies salary by 2: `salary *= 2;`

--

There are even increment and decrement operators, such as `x++;` and `x--;`, which are equivalent to `x = x + 1;` and `x = x - 1;`.

---

template: assignment

<div align="center">
<span style="color: red;">Practice round</span> </div>
