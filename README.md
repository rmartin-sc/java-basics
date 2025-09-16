# Java Basics

This document introduces the basics of Java syntax for programmers coming from an introductory Python background with knowledge of variables, conditionals, loops, functions, lists, dicts, file I/O, and exceptions.  No knowledge of Object-Oriented Programming (OOP) is assumed.

In fact, a discussion of OOP techniques is beyond the scope of this document and the reader should understand that there is *much* more to writing maintainable software in Java than is presented here.  This document simply translates the concepts mentioned above into their Java equivalents.

> **NOTE:** This document assumes a Java version of at least 25. Some features used here (like compact source files) are not available in earlier versions of Java.

## Table of Contents
<!-- TOC -->

- [Java Basics](#java-basics)
  - [Table of Contents](#table-of-contents)
  - [Java vs JavaScript](#java-vs-javascript)
  - [Java is a Compiled Language](#java-is-a-compiled-language)
    - [The Java Virtual Machine](#the-java-virtual-machine)
    - [The Java Development Kit](#the-java-development-kit)
    - [Java Versions](#java-versions)
  - [Running a Java REPL](#running-a-java-repl)
  - [Java Syntax Basics](#java-syntax-basics)
    - [Indentation](#indentation)
  - [Comments](#comments)
  - [Variables](#variables)
    - [Static vs Dynamic Typing](#static-vs-dynamic-typing)
    - [Type Inference](#type-inference)
    - [Variable Names](#variable-names)
  - [Types](#types)
    - [Primitive vs Object Types](#primitive-vs-object-types)
    - [Primitive Types](#primitive-types)
    - [Object Types (Classes)](#object-types-classes)
      - [Constructors](#constructors)
      - [Subclasses](#subclasses)
    - [Boxing and Unboxing Primitives](#boxing-and-unboxing-primitives)
    - [Converting (Casting) Between Types](#converting-casting-between-types)
    - [Determining a Value's Type](#determining-a-values-type)
    - [The Math class](#the-math-class)
  - [Packages](#packages)
    - [Importing packages](#importing-packages)
  - [Printing Values](#printing-values)
    - [Before Java 25](#before-java-25)
  - [Before you go on...](#before-you-go-on)
  - [Declaring Functions](#declaring-functions)
    - [JavaDoc](#javadoc)
  - [Running a Simple Java App](#running-a-simple-java-app)
    - [Hello, world! in Java](#hello-world-in-java)
    - [Before Java 25](#before-java-25-1)
    - [Compiling and Running a Java Code File](#compiling-and-running-a-java-code-file)
  - [Values and Operations](#values-and-operations)
    - [Numbers](#numbers)
      - [Arithmetic operators](#arithmetic-operators)
    - [Characters and Strings](#characters-and-strings)
      - [String Operations](#string-operations)
      - [Escape sequences](#escape-sequences)
      - [Immutability of Strings](#immutability-of-strings)
      - [Formatting Strings](#formatting-strings)
      - [Logical operators](#logical-operators)
    - [Null](#null)
      - [Null and Object Types](#null-and-object-types)
    - [Equality and Object types](#equality-and-object-types)
    - [Objects and References](#objects-and-references)
  - [Conditionals](#conditionals)
    - [Switch Statements](#switch-statements)
  - [Loops](#loops)
    - [While Loops](#while-loops)
    - [For loops](#for-loops)
    - [For-each Loops](#for-each-loops)
    - [Exiting Loops](#exiting-loops)
  - [Arrays](#arrays)
    - [Arrays Have one Type of Element](#arrays-have-one-type-of-element)
    - [Arrays are Fixed-length](#arrays-are-fixed-length)
      - [Initialize an Array with an Array Literal](#initialize-an-array-with-an-array-literal)
      - [Initialize an Array to a specific size](#initialize-an-array-to-a-specific-size)
    - [Indexing and Updating Arrays](#indexing-and-updating-arrays)
    - [Determining the Length of an Array](#determining-the-length-of-an-array)
    - [Comparing Arrays](#comparing-arrays)
    - [Traversing Arrays](#traversing-arrays)
      - [With For Loops](#with-for-loops)
      - [With For-Each Loops](#with-for-each-loops)
      - [Other For-Each Loop Techniques](#other-for-each-loop-techniques)
  - [Collection Types and Generics](#collection-types-and-generics)
    - [Generic Collections](#generic-collections)
    - [ArrayList](#arraylist)
      - [ArrayList Operations](#arraylist-operations)
    - [Maps (dictionaries)](#maps-dictionaries)
      - [Traversing Maps](#traversing-maps)
  - [Higher-Order Functions](#higher-order-functions)
    - [Functional Interfaces](#functional-interfaces)
    - [Method references](#method-references)
    - [Lambda expressions](#lambda-expressions)
      - [Lambda expression shorthand](#lambda-expression-shorthand)
    - [Streams and Filter / Map / Reduce](#streams-and-filter--map--reduce)
  - [Obtaining User Input](#obtaining-user-input)
    - [Scanner](#scanner)
  - [Errors and Error Handling](#errors-and-error-handling)
    - [Raising errors](#raising-errors)
      - [Functions that raise errors](#functions-that-raise-errors)
    - [Catching errors](#catching-errors)
  - [Reading and writing files](#reading-and-writing-files)
    - [Simple one-liners](#simple-one-liners)
    - [Using FileReader and BufferedReader](#using-filereader-and-bufferedreader)
    - [Try with resources](#try-with-resources)
    - [Dealing with platform differences](#dealing-with-platform-differences)

<!-- /TOC -->

## Java vs JavaScript

Java and JavaScript are two completely separate languages.  They have some syntactical similarities, but are otherwise quite different.  

When searching for information about Java, be sure you are not finding information about JavaScript instead!

## Java is a Compiled Language

Java is a **compiled language**, which means that code files must be compiled before they can be executed.  This is in contrast to interpretted languages like Python, where code files are loaded and executed directly by an interpreter.

### The Java Virtual Machine
Java programs are compiled to a secondary language called Java bytecode, which is understood by a program called the Java Virtual Machine (JVM).  The JVM is available for a wide range of platforms, making possible the 'write once, run anywhere' nature of Java programs.  

This is in contrast to languages like C and C++ which must be compiled for specific CPU architectures, meaning that for a single software program there is often a need to write different code for different target platforms.

### The Java Development Kit
In order to create Java programs, you must install a Java Development Kit (JDK).  There are many JDK implementations, some of which are free and some require paid licensing.

[OpenJDK](https://jdk.java.net/25/) is a popular free open source implementation of the JDK.

### Java Versions
The Java language continues to be updated regularly with new versions.  It is possible to install multiple JDKs on one system, and these JDKs may be for different versions of Java.  It is important to know which version of Java your code is using.

Some versions of Java are released as 'long term service' (LTS) versions.  LTS versions are typically the ones used in production environments.

The most recent LTS versions of Java are 21, 17, and 11, released in 2023, 2021, and 2018 respectively.

## Running a Java REPL

As of Java 9, JDKs come with a REPL shell called JShell.  JShell is useful for executing exploratory code, as each statement is executed and evaluated immediately, eliminating the need for the additional compile and run step that is usually required to run Java code.

```java
$ jshell
| Welcome to JShell -- Version 25.0.1
| For an introduction type: /help intro

jshell> int x = 1;
x ==> 1

jshell> int y = 2;
y ==> 2

jshell> x + y
$3 ==> 3

jshell> /exit
|  Goodbye
```

## Java Syntax Basics

- Case sensitive (foo and Foo are two different names)
- Instructions end in semi-colons
- Indentation is NOT part of the syntax.  Instead, curly braces are used to indicate blocks of code like conditional/loop/function bodies

The following two Java snippets are equivalent (but which is more readable?):

```java
void foo() { 
    String name = "Ali"; 
    IO.println("Hello, " + name + "!"); 
}
```

```java
void foo() { String name = "Ali"; IO.println("Hello, " + name + "!"); }
```

### Indentation

While indentation is not syntactically important, using careful indentation *does* make your code more readable, and all programmers should strive to write readable code.

Typically:
- All lines of code within a curly brace should be indented one level from the opening brace.
- The closing brace should be 'outdented' back to the same level as that of the opening brace

## Comments

```java
// This is a one-line comment
// This is another one-line comment
int x = 1;  // Everything after the slash until the end of the line is a comment

/* This is a multi-line comment.
It can span multiple lines.
Everything inside the opening slash-star 
and the closing star-slash is a comment */
```

## Variables

### Static vs Dynamic Typing
Java is **statically typed**, meaning that programers must declare in code the *type* of any variables and parameters.  This is in contrast to a **dynamically typed** language like Python where a variable's type is determined at runtime and need not be made explicit in code.

```java
// Compile-time error! No type specified
x = 1;      
s = "Hello, world!";

// These are ok
int x = 1;
String s = "Hello, world!";
```

Note the syntax for variable declarations.  You may declare a variable without assigning a value to it, or you may initialize a variable with a value immediately.

```java
// Declaration
<type> <variablename>;
```
```java 
// Declaration with initializaiton
<type> <variablename> = <value>;
```

Once a variable has been declared, you may reassign the variable without indicating the type, but the value you assign *must be of the same type* as the initial declaration.

```java
boolean q = true;
int x;
x = 1;   // Ok
x = q;   // Nope!  x and q are of different types
```

### Type Inference
As of Java 10, you can use the `var` keyword in place of a variable's type for variables that are declared...

- inside a function body
- with initialization

The type of such variables will be **inferred** by the compiler based on the value initially assigned to the variable in the declaration.

For example:
```java
var x = 1;    // x will have type int
var s = "Hi"; // s will have type String
```

Type inference is particularly useful when declaring variables with complex types.  Notice in the example below how type inference eliminates the need to repeat the full type on both the left and right sides of the assignment statement:

```java
// Without type inference:
ArrayList<HashMap<String, String>> L = new ArrayList<HashMap<String,String>>();

// With type inference:
var L = new ArrayList<HashMap<String,String>>();
```

### Variable Names

Variable names may include alphabetical symbols, numerical symbols, and/or `_` but may not start with a number.

Variable names may not be a Java keyword.

In Java, convention is to name variables using 'camel casing'

```java
int typicalVariableNameInJava = 1;   // Prefer this...
int unusual_variable_name_in_java = 1;  // ...over this
```

## Types

### Primitive vs Object Types
In Java, there are two basic categories of types: primitive and object.  Unlike Python, where every 'thing' is an object, in Java, primitive types are pure values and never have methods associated with them.

### Primitive Types

```java
boolean   // 1 bit - either true or false
byte      // 8-bit integer
short     // 16-bit integer
int       // 32-bit integer
long      // 64-bit integer
float      // 32-bit floating point number
double    // 64-bit floating point number
char      // 16-bit Unicode character
```

Note that the primitive type names all start with lower case letters.

> **NOTE:** The `char` type, which can hold a single Unicode character, has no equivalent in Python which has only strings.

### Object Types (Classes)

All types other than the primitive types mentioned above are 'object types'.  Unlike primitive types, 'object type' variables store *references to* their values rather than storing the values directly.  This is similar to the way in which Python's lists/dicts are references.

Object types are also referred to as Classes

It is convention for class names to begin with a capital letter.

```java
// In Java, strings are object types...
String s = "Hello, world!";

// ... and thus have methods...
s.toUpperCase(); // Yields "HELLO, WORLD!"
```

#### Constructors

Unlike Strings, which can be declared with a string literal, most object type variables must be declared using the `new` keyword followed by a call to a 'constructor function', or just 'constructor'.  Note that all constructors share the type's name:

```java
Object o = new Object();
ArrayList list = new ArrayList();
String s = new String();  // Strings can be declared like this too
```

Some constructors accept arguments:

```java
String s = new String("Hello, world");  // Initialize a string with a value
ArrayList list = new ArrayList(10);     // Initialize an ArrayList with an initial capacity
```

#### Subclasses

Object types are sometimes arranged in a 'type hierarchy' with the Object class as the 'root'.  For example, all classes in Java are 'subclasses' of the Object class.  Each subclass 'inherits' the variables and functions associated with all of its 'superclasses'.  That is, any variable or function available on a 'superclass' is also available on any of its subclasses.  A subclass may itself be a superclass for a further subclass.

One aspect of designing software in in OOP languages like Java is understanding when/how to take advantage of such type hierarchies, but a discussion of OOP design is beyond the scope of this document.

### Boxing and Unboxing Primitives
Each primitive type in Java has a corresponding object type which can be used to represent the same values, but with additional useful methods available.

> **NOTE:** Primitive types are typically more performant than equivalent Object types, but can only be used in certain contexts.

```java
Boolean  // Object version of boolean
Byte     // Object version of byte
Short    // Object version of short
Integer  // Object version of int
Long     // Object version of long
Float    // Object version of float
Double   // Object version of double
Char     // Object version of char
```

Values of a primitive type *may* be assigned to a variable of the corresponding object type, and vice versa.  This automatic converstion between primitives and their corresponding object types is known as automatic **boxing** and **unboxing**.

```java
int x = 1;

// Automatic boxing of primitive type into an object type
Integer y = x;  

// Automatic unboxing of objet type into primitive
int z = y;      
```

### Converting (Casting) Between Types

Some classes have methods that can be used to cast from one type to another:

```java
// String to number
int n = Integer.parseInt("1000");   
float n = Float.parseFloat("10.0");
float n = Float.parseFloat("1.23e-6");  // Scientific notation works

// Number to string
String s = "" + 1000;
String s = "" + 10.0;
```

There is also a casting syntax that can be used in certain circumstances:

```java
// You can cast between numeric types:
double pi = 3.14159;
int p = (int)pi;
double p2 = (double)p;

// Any subclass can be cast into one of its superclasses
String s = "100";
Object o = (Object)s;   // This works because String is a subclass of Object
String s2 = (String)o;  // This also works because o was a String in the first place

// This does NOT work because Integer is not a subclass of String
// (Yes, even though the value of s contains a string that represents a number.)
Integer i = (Integer)s; 
```

### Determining a Value's Type

The `getClass()` method can be used to determine the type of an object (like Python's `type()` function).  This method of course does *not* work on primitives.
```java
"hi".getClass();     // java.lang.String
Integer x = 1;
x.getClass();        // java.lang.Integer

int x2 = 2;
x2.getClass();       // Error because x2 is a primitive
```

The `instanceof` operator yields true if the left operand is of the type specified by the right operator.  This operator only works on object types:

```java
"Hi" instanceof String  // Yields: true
1 instanceof String     // Yields: false
```

### The Math class

The Math class contains many properties and methods for performing mathematical calculations

```java
Math.PI
Math.pow(x,y)    // Yields x raised to the power y
Math.sqrt(x)     // Yields the square root of x
Math.random()    // Yields a random number between 0 and 1 (but never exactly 1)
Math.round(x)    // Round x to nearest integer
Math.floor(x)     // Round x DOWN to nearest integer
Math.ceil(x)     // Round x UP to nearest integer
Math.max(a, b)
Math.min(a, b)
```

... and [more](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/Math.html)

## Packages

Java programs are usually arranged in packages, which usually correspond exactly with the directory structure of the code files.  For example the code file for a class in a `ca.saultcollege` package would be inside the `src/ca/saultcollege` directory.

You declare the package a code file belongs to using a `package` statement:

```java
package ca.saultcollege;

// This code is in the ca.saultcollege package
// and should be in a src/ca/saultcollege directory
```

### Importing packages

Import all classes (`*`) from the `ca.saultcollege`:
```java
import ca.saultcollege.*;
```

Import just the `MyClass` class from the `ca.saultcollege` package:

```java
import ca.saultcollege.MyClass;
```

## Printing Values

The `IO.println` function prints values to the console (like Python's `print`).

```java
IO.println("Hello, world!");
```

### Before Java 25

Before Java 25, the `System.out.println` function was used to print values to the console:

```java
System.out.println("Hello, world!");
```

## Before you go on...

If you do not have access to version 25 of Java, you may want to read the [Pre-JDK 25](https://github.com/rmartin-sc/java-basics/blob/main/pre-jdk-25.md) document that complements this one before reading on.

## Declaring Functions

Since Java is a statically typed language, every function declaration must include the type of each parameter as well as the return type of the function.

```java
<return type> <function name>( <parameter list> ) {
    // Function body
    // May include a return statement if return type is not void
}
```

Example:

```java
int sum(int a, int b) {
    return a + b;  // The return keyword is used to return a value
                   // This value must be of the type specified in the function declaration
}
```

A function that returns no value has a 'void' return type

```java
void greet(String name) {
    IO.println("Hello, " + name + "!");
}
```

### JavaDoc

There is a special comment format in Java called 'JavaDoc' that is used by convention to document Java functions (akin to Python's docstrings).  It is considered best practice to document each non-trivial function using JavaDoc.

Many programming tools, including the `javadoc` command that comes with the JDK can parse JavaDoc comments and automatically produce documentation for a program.

```java
/**
 * Add two numbers
 * @param a One number to add
 * @param b The other number to add
 * @return The sum of the given numbers
 */
int add(int a, int b) {
    return a + b;
}
```

> **NOTE:**
> - JavaDoc comments start with `/**` (2 stars instead of the usual 1)
> - Each line begins with ` * `
> - The `@return` 'keyword' can be used to specificy information about what (if anything) the function returns
> - The `@param` 'keyword' can be used to provide information about each parameter
> - one `@param` line per parameter
> - The name of the parameter is included before the description of the parameter
> - You can add arbitrary documentation in addition to the `@returns` and `@param` lines
> - There is [much more](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html) you can do with this style of comment, but what you see here is enough to get you started


## Running a Simple Java App

### Hello, world! in Java
The basic "Hello, world!" app in Java is as follows:

```java
void main() {
    IO.println("Hello, world!");
}
```

> **Notes:**
> - Every Java application must have at least one function named `main`.  This is where Java will begin executing code when the program is run.
> - The `main` function must have a `void` return type (returns nothing)

### Before Java 25

Before Java 25, the simplest "Hello, world!" app in Java looked like this (can you see why Java 25 is a more pleasant experience for beginners?):

```java
// In a file named Main.java...
class Main {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

### Compiling and Running a Java Code File
To run a Java program, you must first **compile** it to bytecode using the `javac` command.

```sh
$ javac Main.java
# Produces a bytecode file named Main.class
```

> **NOTE:** It gets more complex for programs consisting of multiple files, but that is outside the scope of this document.

Once the code has been compiled, there are many ways the code may be executed, depending on your goals.

One simple way is to run the class that contains the `main` function using the `java` command:

```sh
$ java Main
Hello, world!
```

> **NOTE:** When running the program, you specify the name *without* the `.java` extension.


## Values and Operations

### Numbers

```java
1           // An int
1.23        // A float
1.23e-5     // A decimal number using scientific notation
```

#### Arithmetic operators

```js
1 + 2       // Addition
1 - 2       // Subtraction
1 * 2       // Multiplication
1 / 2       // Division **See Note below**
9 % 7       // Modulus (the remainder when 9 is divided by 7)
```

> **NOTE:** Division of two ints yields an integer result (the quotient rounded down).  To get a float result, at least one of the operands must be a float:
> ```java
> 5 / 2       // Yields 2
> 5.0 / 2     // Yields 2.5


### Characters and Strings

In Java, character literals are delimited using single-quotation marks, and strings are delimited using double-quotation marks:

```java
char c = 'A';
String s = "A string";

// Syntax errors:
char c = "A"; // Can't assign a String to a char variable
String s = 'c'; // Can't assign a char to a String variables
```

#### String Operations

```java
"a" + "b"                   // Yields "ab"  (concatenation)
"a".repeat(3)               // Yields "aaa" (repetition)
"abcdef".contains("d")      // Yields: true 
"abcdef".indexOf("d")       // Yields: 3 
"abcdef".indexOf("z")       // Yields: -1
"abc".toUpperCase()         // Yields "ABC"
"ABC".toLowerCase()         // Yields "abc"
"  abc  ".trim()            // Yields: "abc"
"a,b,c".split(",")          // Yields an array of strings, {"a", "b", "c"}
String.join(",", strArray)  // Yields a string from an array of strings, 
                            // with each element separated by the value in the first argument

// Strings can be sliced:
"Super duper!".substring(2,5)    // Yields "per"
"Super duper!".substring(6)      // Yields "duper!"
"Super duper!".substring(-1)     // Yields "!"
```

...and [more](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/lang/String.html)

#### Escape sequences

You can use the backslash to create 'escape sequences' for certain special symbols in a string...

```java
"A pair of \"double quotes\" inside a string!"
"First line\nSecond line"
```

#### Immutability of Strings

Strings are immutable:

```java
String s = "abcdef";
s[0] = "z";    // Error!
```

#### Formatting Strings

Strings can be formatted using [format strings](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Formatter.html#syntax)

```java
String.format("A string: %s", "Hi"); 
String.format("An int: %d", 42);
String.format("A floating point number: %f");
String.format("A date/time: %t", LocalDateTime.now());
```

Several other Java functions accept format strings:

```java
// Strings for a `formatted` method
"My name is %s".formatted("Ali");

### Booleans

Java has two boolean literals: `true` and `false`.

#### Comparison operators

```java
2 == 2      // Equal
2 != 1      // Not equal
3 > 2       // Greater than
2 < 3       // Less than
3 >= 2      // Greater than or equal
2 <= 3      // Less than or equal
```
#### Logical operators

```java
&&          // and
||          // or
!           // not

// Examples
true && true == true
true || false == true
! false == true
```

> **NOTE:** `&` and `|` are also operators in Java, but they are *not* the same as `&&` and `||`


### Null

In Java, the value `null` represents 'no value'. (Like Python's `None`.)

#### Null and Object Types

*No* primitive type may have the value `null`.

*Any* object type may have the value `null`. It is important to take into account this possibility in your code.

```java
int x = 1;
int y = 2;      
int z = null // Error!

// This will never fail because x and y are primitives and could never be null
int sum = x + y;
```

```java
Integer x = 1;
Integer y = 2;      
Integer z = null // This works!

// Be careful!  This could fail if x or y is null!
Integer sum = x + y;

// This is better:
if ( x != null && y != null ) {
    Integer sum = x + y;
}
```

### Equality and Object types

The `==` operator only compares **the actual value stored in a variable**. For object types, the value stored a reference, meaning that `==` only evaluates to true if both operands refer to the **same object**. (I.e. it operates like Python's `is` operator.)

```java
int x = 1234;
int y = 1234;

// This evaluates to true!
y == x; 

Integer x = 1234;
Integer y = 1234;
Integer z = y;

y == x;  // This evaluates to false because x and y are two different objects!
y == z;  // This evaluates to true, but only becuase y and z refer to the same object
```

So how can you compare the **value** of two object types?  Every object type has an `equals()` method:

```java
Integer x = 1234;
Integer y = 1234;

// This evaluates to true!
y.equals(x); 
```

### Objects and References

As mentioned above, Java object types are **references**.  Thus, aliasing assignments (eg. `Integer x = y`) simply create a new reference to the *same object*.

Consider the following code using the `Rectangle` class:

```java
var x = new Rectangle(10,20);
var y = x;                    // Aliasing assignment
y.width = 30;                 // Mutate the object referenced by y
// Prints 30 because x and y are references to the same object
IO.println(x.width);   
```


## Conditionals

```java
if ( conditionExpression ) {
    // instructions to execute if conditionExpression is true
} else if ( otherConditionExpression ) {
    // instructions to execute if otherConditionExpression is true
} else {
    // instructions to execute if none of the above condition expressions were true
}
```

### Switch Statements

If all the condition expressions in a conditional statement are discrete **equality** checks, a switch statement can be more readable and more computationally efficient.

The following two code blocks are equivalent:
```java
if ( condition === 0 ) {
    IO.println("Poor");
} else if ( condition === 1 ) {
    IO.println("Good");
} else if ( condition === 2 ) {
    IO.println("Excellent");
} else {
    IO.println("Unknown condition!");
}
```

```java
switch(condition) {
    case 0:
        IO.println("Poor");
        break;  // IMPORTANT: Don't forget the break after each case!!
    case 1:
        IO.println("Good");
        break;
    case 2:
        IO.println("Excellent");
        break;
    default:
        IO.println("Unknown condition!");
        break;
}
```

As of Java 12, there is an alternate switch expression syntax:

```java
// condStr will have the value corresponding to the selected case
String condStr = switch (condition) {
    case 0 -> "Poor";
    case 1 -> "Good";
    case 2 -> "Excellent";
    default -> "Unknown condition!";
}
```

## Loops

### While Loops

```java
while ( conditionExpression ) {
    // Instructions to execute repeatedly until conditionExpression is false
    // (May never be executed!)
}
```

### For loops

The basic for loop in Java is nothing more than a while loop in which all the 'book keeping' is done in one spot.  For example, the two loops below are equivalent:

```java
int i = 0;              // Initialization of counter
while ( i < 10 ) {      // Check counter for exit condition
    IO.println(i);
    i += 1;             // Increment counter
}
```

```java
for ( int i = 0 ; i < 10 ; i += 1 ) {
    IO.println(i);
}
```

In a basic for loop, initialization, check, and increment are all done inside the parentheses, each separated  by a semi-colon.

### For-each Loops

Java also has 'for-each' loops, which operate much like python's `for..in` loops.  For-each loops will be discussed further in the section on arrays.

### Exiting Loops

The `break` statement immediately exits a loop and resumes execution at the first instruction after the loop.  

The `continue` statement immediately ends the current iteration of the loop.

## Arrays

Java has a simple collection type called 'array'.

### Arrays Have one Type of Element
Unlike Python's lists, which may have different types in each element, Java arrays must contain the same type in each element.

### Arrays are Fixed-length
Once an array has been initialized, its length cannot be changed.

To declare an array, add `[]` after the type, as in...
```java
int[] numbers;  // An array of ints
String[] words; // An array of Strings
```

To initialize an array, use one of the following two approaches:

#### Initialize an Array with an Array Literal
```java
int[] numbers = { 1, 2, 3 };
String[] words = { "apples", "oranges" };
```

#### Initialize an Array to a specific size
```java
int[] numbers = new int[10]; // An array that can hold 10 ints
String[] words = new String[10]; // An array that can hold 10 Strings
```

Some notes:
- Array literals are delimited using **curly braces**.  (Python's lists use square brackets.)
- The `new` keyword is necessary to create an array, since it is an object type.
- The length of the array is indicated on the right-hand side, *not* the left.  (The left side is the *type*, the right side is the *value*.)

### Indexing and Updating Arrays

Java arrays are 'zero-indexed', meaning the first element is at index 0.

An array variable may be indexed using the same `[]` syntax as Python's list indexing.

Arrays are mutable.  You may update elements in an array also using the typical `[]` syntax.

```java
int[] a = {1, 2, 3};
String[] b = {"one", "two", "three"};

a[0] == 1;       // Evaluates to true.
String s = b[1]  // s now has value "two"
a[2] = 99;       // The third element of a is now 99
```

### Determining the Length of an Array
All arrays have a `length` property that stores the number of items in the array

```java
int[] a = {1, 2, 3, 4, 5};
a.length;  // Yields the value 5
```

### Comparing Arrays

Since arrays are object types, the `==` operator works like Python's `is` operator.  (See the notes above regarding [Equality and Object Types](#equality-and-object-types))

```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
int[] c = a;

a == a      // Yields: true
a == c      // Yields: true
a == b      // Yields: false because a and b are two distinct obects
```

To check if two arrays contain the same set of values you can use the `Arrays.equals(..)` utility method built into Java:

```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};

Arrays.equals(a,b); // Yields: true
```

### Traversing Arrays

#### With For Loops
One typical way to traverse an array in Java is using a `for` loop:

```java
int[] a = {1, 2, 3, 4, 5};

for ( int i = 0; i < a.length; i += 1 ) {
    var item = a[i];
    // do stuff with the item
}
```

#### With For-Each Loops
As of version 5, Java also has a `for-each` loop syntax that works similarly to Python's `for..in` loop:

```java
int[] a = {1, 2, 3, 4, 5};

for ( int item : a ) {
    // Do stuff with the item
}
```

Some notes about for-each loops in Java:
- The name to the right of the `:` may be an array, but may also be any 'iterable' type.  (See the collection types below, for example.)
- The type of the part to the left of the `:` must correspond to the type of the elements in the array/iterable
- The name of the part to the left of the `:` can be any variable name. On each iteration of the loop, this variable will contain the value of the next item in the array/iterable.

#### Other For-Each Loop Techniques

The `toCharArray` method on Strings returns an array of the `char`s in the string which can then be iterated over, like so:
```java
for ( char letter : "supercalifragilisticexpialidocious".toCharArray() ) {
    IO.println(sletter);
}
```

The built-in `IntStream.range` function is similar to Python's `range` function (except you must supply *both* the start and end values).  You can convert it to an array of `int`s using the `toArray` method, like so:

```java
for ( int n : IntStream.range(0,5).toArray() ) {
    // n iterates through the values 0 to 4
}
```

## Collection Types and Generics

Java's array type has its uses when high performance is of utmost importance, but its fixed-size limitation and lack of useful methods can make it unwieldy.

Java also has a set of more featureful **'collection'** types, which can be used to store collections of values.  For now, a couple collection types that are equivalent to Python's lists and dictionaries will be introduced, but there are [many more](https://docs.oracle.com/en/java/javase/23/docs/api/java.base/java/util/doc-files/coll-reference.html).

### Generic Collections

Collections are defined 'generically', meaning they may 'hold' any type.  However, like arrays, the items in a collection must each be of the *same type*.  This type must be explicit in the declaration of any collection variable.  Thus, for collections there are at least two types that must be declared:  the collection type, and the type which the collection will 'hold'.

For arrays, this is done by adding `[]` to the 'held' type.  (For example, an `int[]` is an array that 'holds' ints.)

With generic collecions, the syntax is different.  You first state the collection type, and then state the 'held' type (or types in some cases) inside of angle brackets.

For example a `List<Integer>` is a list that holds integers; a `Map<String, Integer>` is a data structure that maps String keys to Integer values.

> **NOTE:** Generic collections *cannot* hold primitive types.  (But remember that primitive types can be [automatically boxed](#boxing-and-unboxing-primitives) into their corresponding object type.)

### ArrayList

Java's `ArrayList` is the collection object type most similar to Python's lists.

```java
var numbers = new ArrayList<Integer>(); // A list of Integers
var words = new ArrayList<String>();    // A list of Strings
```

#### ArrayList Operations

```java
// Create an ArrayList with an initial set of values using the List.of function
var a = new ArrayList<Integer>(List.of(1, 2, 3, 4, 5));

a.size();            // Yields: 5  (NOTE: ArrayLists do NOT have a length property like arrays do)
a.contains(1);       // Yields true if 1 is in the list

a.add(1);            // Add a new element with value 1 to the end of the list
a.set(0, 99);        // Set the value at index 0 to 99
a.addAll(b)          // Append all elements of b to a
                     // (b must be a collection holding the same type as a)

a.remove(2)                     // Delete element at index 2
a.remove(Integer.valueOf(2))    // Delete the first element with the value 2

// Slicing arrays
a.subList(2,4);   // Yields an ArrayList with values [3, 4]

// Copying arrays
var a2 = new ArrayList(a); // Make a copy of a
a.toArray();               // Convert the ArrayList to a regular Java array
```

### Maps (dictionaries)

Java's HashMap class is the closest type to Python's dicts.  This type is generic over **two** types, the key type and the value type.  Each of these types is specified in the angle brackets as a comma-separated list.

```java
var m = new HashMap<String, Integer>();  // Map String keys to Integer values
m.put("mykey", 1)                        // Set a key-value pair
m.get("mykey")              // Yields the value corresponding to the given key, 
                            //     or null if there is no such key
m.remove("mykey")           // Removes the entry corresponding to the given key
m.size()                    // The number of elements in the map
```

#### Traversing Maps

HashMaps may be traversed using a a `for-each` loop and the map's `keySet()` method, like so:

```java
// Assuming m is a HashMap with String keys...
for ( String key : m.keySet() ) {
    int val = m.get(key);   // Assuming m has Integer values
    // do stuff with key and/or val
}
```

You can also traverse a map using its `entrySet()` method, which yields objects of type `Map.Entry<K,V>` where `K` is the key type and `V` is the value type.  This is often more efficient than using `keySet()` because it avoids having to look up each value by its key.

```java
// Assuming m is a HashMap with String keys and Integer values...
for ( Map.Entry<String, Integer> entry : m.entrySet() ) {
    String key = entry.getKey();
    int val = entry.getValue();
    // do stuff with key and/or val
}
```

## Higher-Order Functions

In Python, functions are objects, which allows for the creation of higher-order functions (i.e. functions which accept as arguments or return other function objects).

In Java, functions are *not* objects, which unfortunately precludes the creation of higher-order functions.  However, as of version 8, Java allows some syntax which enables much of the expressivity granted by higher-order functions.

As an example, many collection types have a `forEach` method.  The `forEach` method expects a `Consumer` object as an argument. `Consumer` is a 'functional inteface', that is...

### Functional Interfaces

A full discussion of functional interfaces is beyond the scope of this document, but roughly speaking, a functional interface is a type with only one method.  The `Consumer` interface has one method which accepts one argument and returns nothing (void).

You can take advantage of functional interfaces in a couple useful ways:

### Method references

In Java, **any** method that has the same interface as that of the one method of a functional interface may be referred to using the 'method reference' syntax, which is similar to the method calling syntax excpet you use `::` instead of `.`.

For example, we could print each element in a list named `myList` by calling `forEach` on the list with a references to the `IO` class's `println` method.  This will work because `println` has the same interface as `Consumer`'s method (i.e. it is a void function that accepts one argument)

```java
myList.forEach(IO::println);  
```

### Lambda expressions

It is also permitted to use a 'lambda expression' where an object with a functional interface is expected.

A lambda expression in Java is a special syntax which enables programmers to declare functions as an expression.

The syntax for a lambda expression is as follows:

```java
(param1, param2, etc) -> {
    // function body
}
```

**Notes:**
- A lambda expression has no name (it is sometimes referred as an anonymous function)
- A `->` separates the parameter list from the function body
- No parameter or return types need to be declared.  (This is because lambda expressions are only allowed where a functional interface is expected, and the compiler can infer the types from that functional interface.)

Here is another example using the `myList` object from above and a lambda expression.  Note again that the main requirement here is that the lambda expression has the same interface as the functional interface expected by the function to which the lambda is passed (in this case the `Consumer` interface's method).

```java
myList.forEach( (i) -> {
    IO.println("The next number is... " + i);
});
```

#### Lambda expression shorthand

In certain circumstances a shorthand syntax may be used for lambda expressions.

If there is only one parameter, the parentheses around the parameter list may be left out:

```java
// This...
param1 -> {
    // body
}

// ...is the same as this...
(param1) -> {
    // body
}
```

If the body consists of nothing more than a single return statement, then the curly braces the return keyword and the ending semi colon may all be left out:
```java
// This...
name -> { return "Hello, " + name; }

// ...is the same as this...
name -> "Hello, " + name
```

Using this shorthand, the above `myList` example could be written as:
```java
myList.forEach( i -> IO.println("The next number is... " + i) );
```

### Streams and Filter / Map / Reduce

Java collections have a `stream()` method which returns a `Stream` object which has a number of useful methods such as `filter`, `map`, and `reduce`.

The `filter` and `map` methods each return another `Stream` object that represents the filtered/mapped original collection, so calls may be chained:

```java
var a = new ArrayList<Integer>(List.of(1, 2, 3, 4, 5));

a.stream()
    .filter(n -> n % 2 == 0)   // Keep only even numbers
    .map(n -> n * 2)          // Double all the remaining numbers
    .reduce((a,b) -> a + b);  // Sum the remaining numbers
```

## Obtaining User Input

```java
// As of Java 25...
String response = IO.readln("What is your favourite number? ");
```

### Scanner

There is a more powerful way to obtain keyboard input (and it is the *only* way before Java 25).  You must first create a `Scanner` object.  Then you can prompt the user for a response using the scanner object's `next` method:

```java
Scanner scanner = new Scanner(System.in);
System.out.println("What is your favourite number? ");
String response = scanner.nextLine();
```

There are [functions other than `next`](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html) that allow you to obtain a specific type of input.

```java
int n = scanner.nextInt();
float x = scanner.nextFloat();
String line = scanner.next();  // Just one word (separated by space characer)
```

## Errors and Error Handling

### Raising errors

```java
throw new Exception("Something bad happened");
```

#### Functions that raise errors

Java distinguishes between two kinds of errors:

1. **Runtime exceptions** are errors that may be raised at any time, and should be used to indicate programming errors.  E.g. `NullPointerException`, `IndexOutOfBoundsException`, `IllegalArgumentException`, etc.
2. **Checked exceptions** are errors that may be raised due to external circumstances, and should be used to indicate problems that may be outside the control of the programmer.  E.g. `IOException`, `SQLException`, etc.

Any function that raises a **checked exception** must declare this fact explicitly like so:

```java
void myFunc() throws IOException {
    // Code that may or may not throw an IOException
}
```

A method may throw multiple different kinds of exceptions:
```java
void myFunc() throws IOException, FileNotFoundException {
    // Code that may or may not throw any of the above exceptions
}
```

### Catching errors

Catch errors that may be raised:
```java
try {
    // code that may raise an error
} catch (Exception e) {
    // error-handling code
}

// OR
try {
    // code that may raise an error
} catch (IOException e) {
    // code that handles specifically IOExceptions
} catch (IndexOutOfBounds e) {
    // code that handles specifically IndexOutOfBoundsExceptions
} catch (Exception e) {
    // code that handles any other Exception
}

// OR
try {
    // code that may raise an error
} catch (Exception e) {
    // error-handling code
} finally {
    // instructions here will ALWAYS be executed
}
```

## Reading and writing files

Reading and writing files can be more involved in Java than it is in Python.  There are quite a number of ways to read the contents of a file into a variety of data structures.  Here are some examples.

### Simple one-liners

```java

// Read
List<String> lines = Files.readAllLines(Paths.get("myfile.txt"));
String theWholeFile = Files.readString(Paths.get("myfile.txt"));

// Write
// If lines is a List<String>...
Files.write(Paths.get("myfile.txt"), lines, StandardOpenOption.WRITE);
// If theWholeFile is a String...
Files.writeString(Paths.get("myfile.txt"), theWholeFile, StandardOpenOption.WRITE);
```

### Using FileReader and BufferedReader

```java
var br = new BufferedReader(new FileReader("myfile.txt"));
var lines = new List<String>();
try {
    while ( true ) {
        String line = br.readLine();

        if ( line == null ) {
            break;
        }

        lines.add(line);
    }
} finally {
    br.close();  // Make sure the file gets closed
}
```

### Try with resources

Similar to Python's `with` block, Java has a `try-with-resources` syntax which ensures that the resource declared in the `try` header is always closed:

```java
try(BufferedReader br = new BufferedReader(new FileReader("myfile.txt"))) {
    var lines = new List<String>();
    while ( true ) {
        String line = br.readLine();

        if ( line == null ) {
            break;
        }

        lines.add(line);
    }
}
// br is automatically closed when the try block exits
```

### Dealing with platform differences

```java
// A platform-independent line separator:
System.lineSeparator();

// A platform-independent path separator:
import java.nio.file.FileSystems;
FileSystems.getDefault().getSeparator();
```
