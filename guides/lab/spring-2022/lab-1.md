---
description: Javac, Java, Git
---

# Lab 1

Lab spec: [https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab1/index.html](https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab1/index.html)

Welcome to the first lab of the semester! This lab is primarily focused on getting your computer set up with all the course software. I'm planning to write a more comprehensive setup guide later, so I won't be touching on that. For now, I'll be focusing on the Java assignment: `isLeapYear()`.

## Java Code Breakdown

For many students, this is your first time reading Java code! Let's go over the skeleton code provided. First, the class definition:

{% code title="Year.java" %}
```java
/** Class that determines whether or not a year is a leap year.
 *  @author YOUR NAME HERE
 */
public class Year {

    /** Return true iff YEAR is a leap year.  */
    static boolean isLeapYear(int year) {
        return true;    // TODO: YOUR CODE HERE
    }

    /** Print whether YEAR is a a leap year on System.out. */
    private static void checkLeapYear(int year) {
        if (isLeapYear(year)) {
            System.out.printf("%d is a leap year.\n", year);
        } else {
            System.out.printf("%d is not a leap year.\n", year);
        }
    }

    /** For each item in ARGS (an array of one or more numerals), print
     *  whether it is a leap year. */
    public static void main(String[] args) {
        if (args.length < 1) {
            System.out.println("Please enter command line arguments.");
            System.out.println("e.g. java Year 2000");
            System.exit(1);
        }
        for (int i = 0; i < args.length; i++) {
            try {
                int year = Integer.parseInt(args[i]);
                checkLeapYear(year);
            } catch (NumberFormatException e) {
                System.out.printf("%s is not a valid number.\n", args[i]);
            }
        }
    }
}
```
{% endcode %}

Lines 1-3 are called a **Javadoc comment**. A Javadoc comment explains what a particular snippet of code is/does, and contains various other bits of information. For example, we have an `@author` tag here, which denotes the author of that particular snippet of code. You should replace `YOUR NAME HERE` with your name. Writing Javadoc comments is best practice, and you can learn more information [here](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html).

Line 4 is called the **class definition**. Class definitions are crucial for the Java compiler to make sense of your program, especially when your programs span multiple files. `public` is a keyword that controls access -- but don't worry too much about it, you'll learn about it later. `class` denotes that the next word is the class name. `Year` is the class name for this particular file, and it's important to note that **the class name must (almost) always match the file name**. Another note on class names -- the convention is to use CapitalizedCamelCase. Finally, we have an open curly brace `{`, and at the end of the class we will have a closing curly brace `}`.

Line 7 is called the **method signature**. Methods in Java are similar to functions in Python. Like `public`, `static` is a keyword that you can ignore for now. Here's where methods in Java differ: types are specified in the method signature. In this case, the return type of the method is `boolean`, aka `true` or `false`. After the return type is the method name, which is conventionally formatted in camelCase. Finally, the method takes in one **parameter**, `int year`, which are specified in the parentheses `()`. Then, like the class definition, we have a pair of open/close curly braces `{}`.

At a glance, the structure of a method signature is:\
`accessKeywords returnType methodName(type parameter) { ... }`

Line 8 is the body of the method. It contains a `return` statement that returns an expression with the same type as the return type of the method signature. All methods must contain a return statement, with one notable exception (which I cover in the next paragraph). In this case, since the return type is `boolean`, we are able to return `true`.

Line 12 is another method signature. What's notable about this one is that the return type is `void`, which is a special keyword indicating no return type. As you see in the rest of the method body, there is no return statement.

Line 22 is what's known as the **main method**. Any program that you want to run will contain a main method, and the method signature is always the same: \
`public static void main(String[] args) { ... }`

The main method signature is not syntactically different from any other method signature -- the only special things about the main method is that&#x20;

1. It's called `main`
2. Java will start running your program from this method
3. Its parameters read in arguments from the command line

## Assignment Overview

You are asked to write a function that returns `true` if a year is a leap year, and `false` otherwise. A year is considered a leap year if it is:

* Divisible by 400, _or_
* Divisible by 4 but _not_ divisible by 100

There are two things that often trip up students when faced with these criteria. I will list these points a little more explicitly:

1. Only one of the two conditions need to be true for the year to be a leap year. That is, you don't need both conditions to be met in order to be true.
2. The second condition, "Divisible by 4 but _not_ divisible by 100", is one single condition, and should be grouped in our code as such.

**At this point, I recommend you go and try to figure out the answer by yourself.** If you are confused on any Java syntax, search it up! Just don't search up the solution -- that defeats the whole purpose of this assignment, and you won't learn the skills you need to complete future assignments.

## Wrong Solutions

Below I list some incorrect solutions that a student may come up with. Before you expand each explanation, **I highly recommend trying to figure out why it's wrong by yourself**. Doing so will help train your code-reading and debugging skills, which are crucial to your success in this course.

```java
static boolean isLeapYear(int year) {
    if (year % 400 == 0 || year % 4 == 0) {
        if (year % 100 == 0) {
            return false;
        } else {
            return true;
        }
    }
    return false;
}
```

<details>

<summary>Why it's wrong</summary>

Multiples of 400 will not be identified as leap years! Remember that only one of the conditions needs to be true. Also, make sure that the second condition is grouped properly.

</details>

```java
static boolean isLeapYear(int year) {
    if (year % 400 == 0) {
        if (year % 4 == 0 && year % 100 != 0) {
                return true;
            }
        }
    }
    return false;
}
```

<details>

<summary>Why it's wrong</summary>

This returns false for everything! Remember that only one of the two conditions need to be true.

</details>

```java
static boolean isLeapYear(int year) {
    if (year % 400 == 0 || year % 4 == 0 || year % 100 != 0) {
        return true;
    }
    return false;
}
```

<details>

<summary>Why it's wrong</summary>

All leap years will be correctly identified as true, but years such as 100, 200, 300, and 500 will be incorrectly identified as leap years. The second condition states that the year must be divisible by 4, and _not_ divisible by 100.

</details>
