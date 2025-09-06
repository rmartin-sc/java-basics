# Pre-JDK 25

If you are coming from introductory Python to a version of Java before 25, the content below may help you understand some of the additional complexity you encounter when first using older versions of Java.

## Defining Object Types (Classes)

### All variables and functions belong to a class
In Java, **every code file** must define one object type, also known as a class.  Note that this means that is is *not possible* to create a top-level (outside of a class) variable or function in Java like you can in Python.  All Java variables and functions are associated with a class.

You can define your own classes using the following syntax:

```java
class MyClass {
    // Code for a class
}
```

Class definitions declare all variables and functions (usually referred to as properties and methods) associated with objects of that type.  There is much to know about designing classes and structuring programs using classes, but this document focuses on the minimal basics of defining a class with functions that can be called much like plain functions in Python.

### Member variables

The first part of a class definition is usually a set of 'member variables', i.e. a set of variables associated with either the class as a whole (class variables) or with each 'object instance' of the class (instance variables).

#### Visibility

Each variable in a class definition has a *visibility* which determines the scope in which the variable can be referred to.

Variables that are `private` can only be referred to from within the class definition.  Variables that are `public` may be referred by code outsite the class definition.  There are [other visibilities](https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html) in Java but they are beyond the scope of this document.

#### Class variables

Class variables are declared using the `static` keyword:

```java
class MyClass {
    public static int aClassVariable;
}
```

Class variables may be called directly on the class.  I.e. there is no need to create an object instance of the class in order to refer to a class variable:

```java
int x = MyClass.aClassVariable;
int pi = Math.PI;  // PI is a class variable of the built-in Math class

// This does NOT work:
MyClass c = new MyClass();
int x = c.aClassVaraible; // Compile-time error because this is a class variable, not an instance variable
```

Class variables are the nearest thing in Java to a top-level variable in Python.

#### Instance variables

Instance variables are declared *without* the `static` keyword:

```java
class MyClass {
    public int instanceVariable;
}
```

Instance variables can only be referred to using object instances of the class:

```java
MyClass c = new MyClass();
int x = c.instanceVariable;

// This does NOT work:
int x = MyClass.instanceVariable;
```

### Methods (Functions)

In Java, functions are *always* associated with a specific object type, and are usually referred to as **methods**.

Methods can be given a visibility in the same way that class/instance variables can.

Methods can also be 'class methods' (static) or 'instance methods' (non-static) in the same sense as class/instance variables.

#### Defining Class Methods

Class methods are the nearest thing to a plain Python function that Java has.  Here is an example of a static method declaration inside a class named `MyClass`:

```java
class MyClass {
    public static void greet(String name) {
        // function body
    }
}
```

Some notes about this method:
- The `public` keyword indicates that this is a public method (a private method would use the keyward `private` instead)
- The `static` keyword indicates that this is a static method (removing the `static` keyword would make this an instance method)
- The `void` keyword indicates that this function returns no value (if the function *does* return a value, that value's type must be named here instead)
- `greet` is the name of the function
- Inside the parentheses are the method parameters, (here, there is one parameter of type String)
- The function body is contained within the curly braces after the method header

The function above could be called like this:
```java
MyClass.greet("Bob");

// This would NOT work because greet is a class method:
MyClass c = new MyClass();
c.greet("Bob");
```

#### Instance (non-static) Methods

Like instance variables, instance methods are defined *without* the `static` keyword:

```java
class MyClass {
    public void greet() {
        System.out.println("Hello, world!");
    }
}
```

The function above could be called like this:
```java
MyClass c = new MyClass();
c.greet();

// This would NOT work because greet is an instance method:
MyClass.greet();
```

Here are some more examples using the built-in String class:

```java
String.format("A format string %s", 1);  // format is a class method of the String class
"abcde".toUpperCase();                   // toUpperCase is an instance method of String objects

// These would NOT work:
"A format string %s".format(1);  // format is a class method, not an instance method
String.toUpperCase("abcde");     // toUpperCase is an instance method, not a class method
```

#### Constructor Methods

In order to create a new instance of a class (i.e. an object), a class must have a 'constructor' method.  If no such method is explicitly defined in a class, an implicit parameterless constructor can be used:

```java
class MyClass {}

// Even though MyClass is empty an instance can be created using the parameterless constructor:
MyClass c = new MyClass();
```

The syntax for a constructor method is as follows:

```java
class MyClass {
    public MyClass() {
        // ...
    }
}
```

Some notes:
- The name of the constructor method must be the same as the name of the class
- Constructor methods have no return type
- Constructor methods are (almost always) public

Constructor methods are often used to initialize instance variables:
```java
class MyClass {
    private int x;

    public MyClass(xVal) {
        x = xVal;
    }
}
```
Given the above class definition, one can create a new instance with the x instance variable initialized, like this:
```java
MyClass c = new MyClass(42);
```

#### Getter and Setter Methods
It is considered best practice to make all instance variables of a class private and provide public getters and/or setters for access to those variables from outside the class:

```java
class MyClass {
    private int x;

    public int getX() { return x; }
    public void setX(int xVal) { x = xVal; }
}
```

Note that getters and setters are (by convention) always named 'get'/'set' plus the name of the instance variable



### Interfaces

The 'public interface' of a class consists of its public members, i.e. its public class and instance variables, and its public class and instance methods.

Interfaces can also be defined as a separate unit of code in Java, and class definitions can be declared to 'implement' interfaces:

```java
// In CanDouble.java
interface CanDouble {
    public int double(int n);
}

// In CanTriple.java
interface CanTriple {
    public int triple(int n);
}

// In MyDoubler.java:
class MyDoubler implements CanDouble, CanTriple {
    public int double(int n) {
        return 2*n;
    }

    public int triple(int n) {
        return 3*n;
    }
}
```

> **Notes:**
> - Interfaces may only declare methods
> - The methods in an interface do not require bodies (those will be in the classes that implement the interface)
> - If a class implements an interface it *must* provide a method with the same interface as the one declared in the interface
> - The `implements` keyword precedes a comma-separated list of interface names which the class implements
> - A class may implement any number of interfaces
> - Many classes may implement any given interface

#### Functional Interfaces

Any interface that has **exactly one** abstract method is a 'functional interface'.  An abstract method is one with no implementation, (the implementation being defered to an implementing class).

Functional interfaces are an important part of Java's approach to functional programming concepts like higher-order functions.  (See the [Higher-order functions section](#higher-order-functions) below)

> **NOTE:** Passing an object as an argument is an aliasing assignment—the parameter becomes an alias for the object passed as an argument.  So mutating a parameter that is an object will change the object for the caller too!

```java
void mutate(Rectangle r) {
    r.setSize(30, 40);  // Mutate the object referenced by r
}

var x = new Rectangle(10, 20);
mutate(x);  // Pass x as an argument

IO.println(x.width);   // Prints 30 
```
