---
layout: presentation
title: Starter code, I/O using Scanner, data types, and arithmetic.
permalink: /slides/starter-code/
---

class: center, middle

# Starter code and I/O using the Scanner class

---

# Agenda
Part I: Starter code and I/O using the Scanner class
1. [Things you need](#assumptions)
1. [Your first Java program](#starter-code) 
1. [Explaining your first Java program](#java-program-explained)
1. [A Java program with the Scanner class](#code-scanner) 
1. [More about the Scanner class](#input)
1. [A note about division and type casts](#division-type-casts)

Part II (Next lecture -- in construction)
1. [Organizing projects I](#organizationI)
1. [Organizing projects II](#organizationII)
3. [Data types](#data-types)
4. [Java identifiers]
5. [Operators and operands]
6. [Arithmetic in Java]
7. [Conclusions](#conclusions)

---

name: assumptions

# Things you need

---

template: assumptions

You will need a UNIX terminal emulator.

- OS X users already have the Terminal app we will use for this purpose.
- Windows users must have [Git for Windows](https://gitforwindows.org/) installed.


You will need to have the [Java Development Kit](https://www.oracle.com/technetwork/java/javase/downloads/) (JDK) installed.


You will need a text editor. I will use [Visual Studio Code](https://code.visualstudio.com), which is a good plain text editor.

- OS X users should read [this](https://code.visualstudio.com/docs/setup/mac) to use Visual Studio Code in the command line. 
- In particular, you need to open the Command Palette (Cmd+Shift+P) and type 'shell command' to find the Shell Command: Install 'code' command in PATH command.
- After that, restart the terminal and you should be good to go.

---

name: starter-code

# Your first Java program

---

template: starter-code

## Create a file

Use the command line to make a new plain text file with the `.java` extension somewhere you know you can find it later.

```bash
foo@bar$ cd ~
foo@bar$ mkdir first_try
foo@bar$ cd first_try
foo@bar$ touch MyFirstJavaProgram.java
```

---

template: starter-code

## Add starter Java code to the file

Edit the text file you just created. Assuming you are using Visual Studio Code,

```bash
foo@bar$ code MyFirstJavaProgram.java
```

Add the following code:

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

---

template: starter-code

## Save your file

If you are using Visual Studio Code, press `Ctrl-S` to save.


## Compile your file

Java code must be compiled to byte code before it can be run. Use the `javac` command to do this.

```bash
foo@bar$ javac MyFirstJavaProgram.java
```

Note the full name of the .java file to compile.

The compiler will now have automatically created a file named MyFirstJavaProgram.class in the same directory.

---

template: starter-code

## Execute the Java byte code

The Java byte code can now be executed by the JVM, Java's interpreter, using the `java` command.

```bash
foo@bar$ java MyFirstJavaProgram
Welcome to Java from the command line!
```

Note the command does not require the `.java` or `.class` file extension.

---

name: java-program-explained

# Your first java program explained
---

template: java-program-explained

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

The first line defines a **class**.

Every Java program must have at least one class.

Each class has a name.
- The name of our class is MyFirstJavaProgram
- By convention, class names start with an uppercase letter.

The name of the class containing the main method must match the name of the source file (MyFirstJavaProgram.java)

---

template: java-program-explained

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

The second line defines the **main method**.

A java program is executed from the main method. It is the entry point where the program begins execution.

A method has a name (e.g., main) and contains a set a statements.

---

template: java-program-explained

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

`Public` , `Static` , `void` are called **reserved words**.

Each one of them has a specific meaning to the compiler. 

We will explain these words in detail later in the course.

---

template: java-program-explained

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

The line `// put the main contents of your program below here` is a **comment**.

A comment documents information about the program.

Comments help programmers communicate and understand the program.

Note: Comment your programs! See this [website](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/) for best practices.

---

template: java-program-explained

```java
public class MyFirstJavaProgram {
	public static void main(String[] args) {
		// put the main contents of your program below here
		System.out.println("Welcome to Java from the command line!");
		// put the main contents of your program above here
	}
}
```

`System.out.println` is a **Java statement**.

The statement `System.out.println` instructs the computer to display a message in the console.

The message we will be displaying in the program is "Welcome to Java from the command line!".

Note: Almost all statements in Java must end with a semicolon **;**.

---

name: code-scanner

# A Java program with the Scanner class

---

template: code-scanner

In order to easily receive keyboard input from a user, a Java program must import `java.util.Scanner`.

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
The next() **method** is used to get input from the user.

It can read the input only until a space(" ") is encountered.

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

- `next()` - returns a `String` with the user's input up until a space(" ") is encountered.
- `nextLine()` - returns a `String` with the user's input up to the newline (i.e. `\n`) character they type
- `nextInt()` - returns an `int` with the user's input, if they entered an integer; otherwise crashes
- `nextDouble()` - returns a `double` with the user's input, if they entered a number; otherwise crashes

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

## Note: Scanner weirdness

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

This program will always output, `Welcome, !` no matter what you do...

---

template: input

## Note: Scanner weirdness

One way to avoid Scanner's weirdness, when asking the user for data types besides String, is to use `nextLine()` for all input and then convert the String it returns to other data types.

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

name: division-type-casts

---

template: division-type-casts

## Note: Division and type casts

Consider the following Java codes, which intends to convert celsius temperature to its Fahrenheit equivalent:

```java
public class CelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9 / 5 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

Demo: What happens when the code is run?

---

template: division-type-casts

## Note: Division and type casts

```java
public class CelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9 / 5 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

The problem arises from the fact that both 9 and 5 are of type `int`, which means that the result is also an `int`.

Thus 9 / 5 = 1 in Java (!)

You can fix this problem by converting the fraction to a double, either by inserting decimal points or by using a type cast:

---

template: division-type-casts

## Note: Division and type casts

```java
public class BetterCelciusToFahrenheit {
	public static void main(String[] args) {
		double c = 100; // double data type is a double-precision 64-bit IEEE 754 floating point.
		double f = 9.0 / 5.0 *c + 32;
        System.out.println("Fahrenheit temperature is: " + f); // Correct temperature should be 212 degrees Fahrenheit
	}
}
```

Demo: Now it should work!

---

name: organizationI

# Organizing Java project files and folders I

---

template: organizationI

We'll organize different projects into different project directories.

```bash
project-directory/
       |
       |----------> src/ (Java source code)
       |
       |----------> lib/ (external dependencies)
       |
       |----------> bin/ (compiled byte code)
```

Each project directory contains three sub-directories: `src/`, `lib/`, and `bin/`.
- Java source code goes into `src/`.
- Compiled code goes into `bin/`.
- Any external dependencies (e.g., input from an external source) go into the `lib/`.

---

template: organizationI

Create a new directory called `project-directory` and add `src/`, `lib/`, and `bin/` directories in it.

```bash
foo@bar$ mkdir project-directory
foo@bar$ cd project-directory
foo@bar$ mkdir src
foo@bar$ mkdir lib
foo@bar$ mkdir bin
```

Create an empty Java file called AddingDoubles.java inside the src folder, and open the file with VSC:

```bash
foo@bar$ touch src/AddingDoubles.java
foo@bar$ code src/AddingDoubles.java
```

---

template: organizationI

Write or copy-paste the code below in AddingDoubles.java:

```java
import java.util.Scanner;

class AddingDoubles{
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);
    System.out.println("Type a number:");

    double x = myObj.nextDouble();

    System.out.println("Type another number:");
    double y = myObj.nextDouble(); // Read user input

    double sum = x + y;
    System.out.println("Sum is: " + sum); 
  }
}
```

We can compile and run the code using the following commands:

```bash
foo@bar$ javac -d bin src/AddingDoubles.java
foo@bar$ java -cp bin AddingDoubles
```

---

name: organizationII

# Organizing Java project files and folders II

---

template: organizationII

Java code can be organized into "packages" of related files.

A **package** in Java is used to group related classes. Think of it as a folder in a file directory.

Add a similar package declaration to your source code file in VSC, but replace gp2442 with your own NYU Net ID.

```java
package edu.nyu.cs.gp2442; // Add this line here, but with your NYU Net ID.
import java.util.Scanner;

class AddingDoubles{
  public static void main(String[] args) {
    Scanner myObj = new Scanner(System.in);
    System.out.println("Type a number:");

    double x = myObj.nextDouble();

    System.out.println("Type another number:");
    double y = myObj.nextDouble(); // Read user input

    double sum = x + y;
    System.out.println("Sum is: " + sum); 
  }
}
```

---

template: organizationII

**Note**: When using a package identifier, the .java and .class files must be located in a directory that matches the package.

Create an appropriate set of sub-directories, and move both files at once (replace gp2442 with your own NYU Net ID):

```bash
foo@bar$ mkdir -p src/edu/nyu/cs/gp2442
foo@bar$ mv AddingDoubles.* src/edu/nyu/cs/gp2442
```

The Java source code must now be re-compiled, since the byte code is no longer up to date.

```bash
foo@bar$ javac -d bin src/edu/nyu/cs/gp2442/AddingDoubles.java
```

Finally, we can run the compiled code:

```bash
foo@bar$ java -cp bin edu.nyu.cs.gp2442.AddingDoubles
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
- **arrays**, while not a data type, are a fundamental data structure in Java

---

template: data-types

## Overview (continued)

Observations:

- `float` and `double` are fundamentally inaccurate. Use `java.math.BigDecimal` for accuracy.
- there is no `String` primitive data type in Java. `String` is a `class` that is written in Java code.
- because it contains "primitive" data types that are not only `class` types, _Java is not a purely object-oriented language_.

---

template: data-types

## Utility/Helper/Wrapper classes

The Java API (a set of `classes` written in Java that are distributed with Java) offers a set of utility classes to help manipulate data of the fundamental primitive data types and structures.

- `Byte`
- `Short`
- `Integer`
- `Long`
- `Float`
- `Double`
- `Character`
- `Boolean`
- `Arrays`

--

- These classes are especially helpful when converting a value of one data type to another.

---

template: data-types

## Utility/Helper/Wrapper classes (continued)

Observations:

- Utility classes contain useful methods for manipulating the types of data usually stored as fundamental primitive data types.
- They are often called "wrapper" or "helper" classes because they offer additional functionality built around primitive data types.
- These are fully-**objected-oriented** correlates of the fundamental primitive data types.

---

template: data-types

## Apache Commons Lang

Due to the limitations of working with primitive data types and the conservative nature of the Java API's included Utility/HelperWrapper/ classes, the [Apache Software Foundation](https://apache.org) sponsors a project called [Commons Lang](https://commons.apache.org/proper/commons-lang/) that aims to provide functionality that many programmers regret is not present in the Java API. This library includes additional helper classes, such as:

- `NumberUtils`
- `CharUtils`
- `BooleanUtils`
- `ArrayUtils`
- ... and [many more](https://commons.apache.org/proper/commons-lang/apidocs/index.html) for dealing with data of non-primitive types.

--

- Commons Lang is perhaps most well-known for its `String`-related helper classes: `StringUtils`, `WordUtils`, and `StringEscapeUtils`.

---

template: data-types

## Strings

The `==` operator performs a comparison of the position in memory where two values are stored in memory.

- It does not compare the values stored at those locations of memory

```java
String x = "hello";
String y = "hello";
boolean theSameMemoryAddress = (x == y); // -> most likely true, but not guaranteed to be so
```

```java
Scanner scn = new Scanner(System.in);
String x = "hello";
String y = scn.nextLine(); // let's imagine the user enters the same text, "hello"...
boolean theSameMemoryAddress = (x == y); // -> most likely false!, but not guaranteed to be so
```

---

template: data-types

## Strings (again)

`String` is not a primitive data type, it's an object-oriented `class`.

- Only primitive data types with the same value are guaranteed to be stored in the same spot in memory
- So two Strings with the same value may be stored in different spots in memory
- So the `==` operator may not always result in a `true`, when comparing two Strings, even those with the same text.
- So use the `.equals()` method for Strings instead.

```java
String x = "hello";
String y = "hello";
boolean theSameMemoryAddress = x.equals(x); // -> true if they contain the same text, false otherwise
```

---

template: data-types

## Strings (once more)

There is also a `StringBuilder` class, which is a utility class for the `String` class.

- Even though `String` is actually fully object-oriented, Strings are immutable.
- The `StringBuilder` class is a convenient mutable equivalent of the String class.

```java
StringBuilder str = new StringBuilder();
str.append("goodbye");
str.append("foo");
str.append("world!");
str.delete(7,10); // remove the characters at index positions 7-9, i.e. "foo"
str.insert(" ", 7); // insert a space at index position 7
str.replace(0, 7, "hello"); // replaces the characters at index positions 0-6 (i.e. "goodbye) with "hello"
String result = str.toString(); // -> "hello world!";
System.out.println(result);
```

---

template: data-types

## Converting data types

Double to int:

```java
Double dbl = new Double(5.0);
int integer = dbl.intValue();
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

---

template: data-types

## Converting data types

Double to String:

```java
String str = Double.toString(5.0);
```

---

template: data-types

## Converting data types

Long to String:

```java
String str = Long.toString(50L);
```

---

template: data-types

## Converting data types

Float to String:

```java
String str = Float.toString(5.0F);
```

---

template: data-types

## Converting data types

String to Integer:

```java
int i = Integer.valueOf("5").intValue();
// or
int i = Integer.parseInt("5");
```

---

template: data-types

## Converting data types

String to Double:

```java
double d = Double.valueOf(str).doubleValue();
// or
double d = Double.parseDouble(str);
```

---

template: data-types

## Converting data types

String to Long:

```java
long l = Long.valueOf("5").longValue();
// or
long l = Long.parseLong("5");
```

---

template: data-types

## Converting data types

String to Float:

```java
float f = Float.valueOf("5").floatValue();
```

---

template: data-types

## Converting data types

Decimal to Binary:

```java
String bin = Integer.toBinaryString(50);
```

---

template: data-types

## Converting data types

Decimal to Hexadecimal:

```java
String hexstr = Integer.toHexString(50);
//or
String hexstr = Integer.toString(50, 16);
```

---

template: data-types

## Converting data types

Hexadecimal to Decimal:

```java
int i = Integer.valueOf("B8DA3", 16).intValue();
//or
int i = Integer.parseInt("B8DA3", 16);
```

---

template: data-types

## Converting data types

Char to String:

```java
String s = String.valueOf('c');
```

---

template: data-types

## Converting data types

Integer to ASCII code:

```java
int i  = (int) "A";
```

---

template: data-types

## Converting data types

Use **exception handline** to handle any problems encountered while attempting to convert one data type to another.

```
String aString = "foo bar baz bum"; //  a string that has no obvious int equivalent

try{
	// try to do the conversion...
	i = Integer.parseInt(aString); // will fail and produce an Exception
}
catch(NumberFormatException e) {
	// this block of code will run if there was a failure
	System.out.println(e); // will output the Exception but not crash the program
}
```

---

name: conclusions

# Conclusions

--

We can now use the command line to write and compile Java source code into Java byte code and then execute that byte code using the JVM interpreter. We also understand a bit about data types in Java.

--

- Thank you!
