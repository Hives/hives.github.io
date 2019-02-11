---
layout: post
title: PLIBMTTBHGATY v4.0 - Java basics
date: 2019-02-10 18:00 +0000
category: makers
tags: java, hello world, TDD, PLIBMTTBHGATY
---


On Saturday 9th Feb I went in to the Makers PLIBMTTBHGATY\* open day, to have a
go at something new. I decided to try Java, not knowing anything about
it. Sat with a couple of other Makers' attendees, I worked through the exercises
in this repo:
<https://github.com/hives/java_intro>

\* "Programming language I've been meaning to try but haven't got around to yet"
🙂

## Lesson 0 - What is Java?

### Dynamically vs statically typed languages

Dynamically typed languages perform type checking at runtime, while statically
typed languages perform type checking at compile time. This means that scripts
written in dynamically types languages can compile even if they contain errors
which will stop the script running.

Statically-typed languages require you to declare the data types of your
variables before you use them, while dynamically-typed languages do not.

<https://docs.oracle.com/cd/E57471_01/bigData.100/extensions_bdd/src/cext_transform_typing.html>

**Java is statically typed.**

### Compiled vs interpreted languages

A compiled language is one where the program compiles into machine code. An
interpreted language is one where the instructions are not directly executed by
the target machine, but read and executed by another program , which normally
*is* written in the language of the native machine.

#### Compiled languages:
- C
- C++
- Erlang
- Haskell
- Rust
- Go

Advantages:
- Speed

Disadvantages:
- Has to be compiled separately for different environments
- Have to manually compile it each time you make a change (makes debugging
slightly more time-consuming)
- Compilers are hard to write!

#### Interpreted languages:
- PHP
- Perl
- Ruby
- Python

Advantages:
- Programs are platform independent
- Can be dynamically typed
- Smaller executable program size

Disadvantages:
- Slower (although gap is closing)

**Java is a *bytecode language*, which means it's somewhere in between:**

> Bytecode languages are a type of programming language that fall under the
> categories of both compiled and interpreted languages because they employ both
> compilation and interpretation to execute code.
<https://thesocietea.org/2015/07/programming-concepts-compiled-and-interpreted-languages/>

> Consequently, you can write a Java program (on any platform) and use the JVM
> compiler (called javac) to generate a bytecode file (bytecode files use the
> extension .class). This bytecode file can be used on any platform (that has
> installed Java). However, bytecode is not an executable file. To execute a
> bytecode file, you actually need to invoke a Java interpreter (called java).
> Every platform has its own Java interpreter which will automatically address
> the platform-specific issues that can no longer be put off. When
> platform-specific operations are required by the bytecode, the Java
> interpreter links in appropriate code specific to the platform.
<http://www.cs.cmu.edu/~jcarroll/15-100-s05/supps/basics/history.html>

## Lesson 1

Objectives: install the Java Development Kit (JDK), compile a java program to
bytecode, and run it.

- Installed the JDK (in Arch: `sudo pacman -S openjdk-src`)
- ran `java -version` to check install
- copy 'hello, world' code ([from here][princeton-hello-world]) into a file
- compile with `javac HelloWorld.java` - creates HelloWorld.class
- run it with `java HelloWorld`

## Lesson 2

Objectives: in Java variables must be declared before use, so we'll look at
that. Also printing to the console. 

- Wrote a short program to declare two string variables and combine them into a
message, compiled and ran it:
```java
public class Strings {
    public static void main(String[] args) {
      String name1 = "Bertie";
      String name2 = "Gertie";
      String message = "Hello " + name1 + ", and hello " + name2 + "!";
      System.out.println(message);
    }
}
```
- Wrote a short program to declare an int and a double, add them up and print
the result, compile and run it:
```java
public class Numbers {
    public static void main(String[] args) {
      int inty = 3;
      double doubly = 0.14159265359;
      double addEmUp = inty + doubly;
      System.out.println(addEmUp);
    }
}
```
- Wrote a program to create an array of strings, an array of numbers, and an
`ArrayList`, and print them:
```java
import java.util.*;
public class Arrays {
    public static void main(String[] args) {
    // declare an array of Strings and print it
    String[] names = {"Bertie", "Gertie", "Yurtie"};
    System.out.println(names);
    for (int i=0; i<names.length; i++)
        System.out.println(names[i]);

    // declare an array of integers and print it
    int[] numbers = {1, 3, 3, 7};
    System.out.println(numbers);
    for (int i=0; i<numbers.length; i++)
        System.out.println(numbers[i]);

    // declare an ArrayList of integers, add numbers to it, and then print it
    int n = 7;
    ArrayList<Integer> arrli = new ArrayList<Integer>(n);
    for (int i=1; i<=n; i++)
        arrli.add(i * 2);
    System.out.println(arrli);

    }
}
```
- What's an `ArrayList`?
> ArrayList is a part of collection framework and is present in java.util
> package. It provides us dynamic arrays in Java. Though, it may be slower than
> standard arrays but can be helpful in programs where lots of manipulation in
> the array is needed.
- So the most significant difference between `Array` and `ArrayList` is that
`ArrayList` is dynamic, meaning it can be resized after it's been declared.
- [Array vs ArrayList in Java][arrays-vs-arraylist]

## Lesson 3 - JavaBuzz

Objectives: getting user input, control flow and loops.

Gonna give up on putting the programs in here because they started getting too
long. Exercises are in my GitHub [here][lesson3-exercises].

- Wrote a program to take a number via user input and output whether it's odd or
even. Used a `while` loop to keep taking input until the number 17 was entered.
- Wrote a program to loop over an array of integers and print them out.
- JavaBuzz 🙂

## Lesson 4 - JavaBuzz, TDD style

Objectives: running JUnit tests in the console, annotations, "red, green,
refactor"

Exercises in my GitHub [here][lesson4-exercises].

- Downloaded `junit-4.13-beta-2.jar` and `hamcrest-core-2.1.jar`, the most
recent versions, following the instructions from the [JUnit
GitHub](https://github.com/junit-team/junit4), and put them in the same folder
with the exercises
- Compiled `Example.java` and `ExampleTest.java`.
- To compile `ExampleTest.java` I had to use this command:  
`javac -cp .:junit-4.13-beta-2.jar:hamcrest-core-2.1.jar ExampleTest.java`
- What does `java -cp` mean? Type `java` to get java command line help and this
is revealed:  
`-cp <class search path of directories and zip/jar files>`
- Tried to run the tests in ExampleTest.java using this command:  
`java -cp .:hamcrest-core-2.1.jar:junit-4.12.jar org.junit.runner.JUnitCore
ExampleTest`  
- No dice!  Failed with this error:  
`Exception in thread "main" java.lang.NoClassDefFoundError:
org/hamcrest/SelfDescribing`
- With some googling thought it might a problem with incompatible versions or
something? So re-read the JUnit instructions more carefully, downloaded the
recommended versions which were the older `junit-4.12.jar` and
`hamcrest-core-1.3.jar`, recompiled, and then the tests ran.

By this time it was 4.30 so I went home, and continued the following
afternoon...

- Q: What does `@Test` mean in e.g. [this example code][lesson4-exampleTest]?  
  A: It's an example of a Java annotation - a way of adding metadata to Java
  source code. In this case it identifies to JUnit that the method to which it
  is attached can be run as a test case.
  <http://junit.sourceforge.net/javadoc/org/junit/Test.html>
- Q: Investigate where our assertion method comes from. What else do we have
  available?  
  A: [The example code][lesson4-exampleTest] uses `assertEquals`, which comes
  from `org.junit.Assert`. Other options include `assertArrayEquals`,
  `assertFalse`, `assertNotNull`, `assertSame`...
  <http://junit.sourceforge.net/javadoc/org/junit/Assert.html>

The final part was to rewrite JavaBuzz from the previous chapter in TDD style.
This was my first attempt at writing TDD-style tests in any language.

- I rewrote JavaBuzz with a public method `JavaBuzz` which takes an integer and
returns "Java", "Buzz", "JavaBuzz" or the integer as a string as appropriate, so
that I could target the method with my tests. [See here.][lesson4-javabuzz]
- I wrote four tests ([see here][lesson4-javabuzztest]) which pass some
integers to `JavaBuzz` and check it gives
the correct answers for numbers which are:
  1. multiples of 5 but not 3
  2. multiples of 3 but not 5
  3. multiples of 3 and 5
  4. multiples of neither
- This seemed to work as desired. I fiddled around with the numbers in the
tests and found that the tests worked correctly or broke in the way I expected.

I think that's enough on this for now. The notes for Chapter 4 talk about
breaking the JavaBuzz method "down into its parts", and using `@Before` to make
the test more DRY, which suggests to me that they were thinking of a different
approach to the one I took, so there's something for me to continue with if I
come back to Java at some point.

[princeton-hello-world]:https://introcs.cs.princeton.edu/java/11hello/
[arrays-vs-arraylist]:https://www.geeksforgeeks.org/array-vs-arraylist-in-java/
[lesson3-exercises]:https://github.com/Hives/java_intro/tree/master/chapter3-JavaBuzz/exercises
[lesson4-exercises]:https://github.com/Hives/java_intro/tree/master/chapter4-JavaBuzz-TDD-style/exercises
[lesson4-exampleTest]:https://github.com/Hives/java_intro/blob/master/chapter4-JavaBuzz-TDD-style/exercises/ExampleTest.java
[lesson4-javabuzz]:https://github.com/Hives/java_intro/blob/master/chapter4-JavaBuzz-TDD-style/exercises/JavaBuzz.java
[lesson4-javabuzztest]:https://github.com/Hives/java_intro/blob/master/chapter4-JavaBuzz-TDD-style/exercises/JavaBuzzTest.java
