---
description: IntelliJ and IntLists
---

# Lab 2

Lab spec: [https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab2/index.html](https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab2/index.html)

Welcome to lab 2! This lab is primarily focused on getting IntelliJ set up. Like the previous guide, I won't be going over setup at all. For now, I'll be focused on IntLists and JUnit.

## IntLists

An `IntList` is 61B's implementation of an integer linked list. `IntList` has two main properties: `head` and `tail`. You can see these properties defined in the following code.

{% code title="IntList.java" %}
```java
import java.util.Formatter;

/** Scheme-like pairs that can be used to form a list of integers.
 *  @author P. N. Hilfinger, Josh Hug, Melanie Cebula.
 */
public class IntList {

    /** First element of list. */
    public int head;

    /** Remaining elements of list. */
    public IntList tail;

    ...
}
```
{% endcode %}

## Destructiveness

We call a method **destructive** if it modifies the original object passed into the method. Conversely, we call a method **non-destructive** if it preserves the original object passed into the it. Below, I've provided a few code snippets, and your job is to figure out if it is destructive or not.

Here is the base code that will be run:

```
public class Exercise {
    public static void main(String[] args) {
        IntList a = IntList.list(1, 2, 3);
        IntList b = IntList.list(4, 5);
        method(a, b);
    }
}
```

Following are various versions of `method()`. Try to figure out if each method is destructive or not, and as a bonus, what value each variable will end up as.

```java
public static void method(IntList x, IntList y) {
    x.tail.head = y.head;
}
```

<details>

<summary>Destructive or Non-Destructive?</summary>

Destructive! This changes `a` to be \[1, 2, 4].

</details>

```java
public static void method(IntList x, IntList y) {
    x.tail = y;
}
```

<details>

<summary>Destructive or Non-Destructive?</summary>

Destructive! This changes `a` to be \[1, 2, 4, 5].

</details>

```java
public static void method(IntList x, IntList y) {
    x = y.tail;
}
```

<details>

<summary>Destructive or Non-Destructive?</summary>

Non-destructive! What's happening here is that `x` now points to \[5]. However, `a` stays as \[1, 2, 3]. The reason this happens is that **none of the pointers inside the `IntList` were modified** -- only the pointer from the parameter to the actual `IntList`.

</details>

```java
public static void method(IntList x, IntList y) {
    x.head = y;
}
```

<details>

<summary>Destructive or Non-Destructive?</summary>

This one is actually a trick question. The answer is that there is a syntax error! `x.head` is of type `int`, and `y` is of type `IntList`. You might have scoffed a little at this, but identifying errors is an important skill for completing projects and solving exam-level problems. It's always a good idea to check that variable types match during assignment.

</details>

## Anatomy of a JUnit Test

Here, I'll break down the JUnit test syntax. You'll have to write a lot of tests over the course of the semester, so it's best to get to know the syntax early.

{% code title="AGTestYear.java" %}
```java
import static org.junit.Assert.*;
import org.junit.Test;

public class IntListTest {

    /** Sample test that verifies correctness of the IntList.list static
     *  method. The main point of this is to convince you that
     *  assertEquals knows how to handle IntLists just fine.
     */

    @Test
    public void testList() {
        IntList one = new IntList(1, null);
        IntList twoOne = new IntList(2, one);
        IntList threeTwoOne = new IntList(3, twoOne);

        IntList x = IntList.list(3, 2, 1);
        assertEquals(threeTwoOne, x);
    }
    ...
}
```
{% endcode %}

Lines 1-2 contain the **import statements** for JUnit. These are important for the Java compiler to understand where to find the relevant JUnit expressions, and if you don't include these, you'll probably see a lot of errors in IntelliJ.

Line 11 contains the `@Test` annotation. This basically signals to JUnit that the following method is a JUnit test and should be run. There are some other options that you can include in this annotation, which I'll link [here](https://junit.org/junit5/docs/current/user-guide/#writing-tests-annotations).

Lines 13-17 contains the setup to do the test. Here, we are verifying that our `IntList.list()` method is functioning properly. In lines 13-15, we construct the expected `IntList` in a way that we know is correct (remember, we pretend we don't know if `IntList.list()` is correct or not). Then, in line 17, we construct the actual value that we wish to test.

Line 18 contains the JUnit assert -- this is what is actually being tested. There are a number of different assert statements, such as `assertEquals`, `assertTrue`, and `assertNotNull`. A full list can be found [here](https://junit.org/junit5/docs/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html). By convention, we put the expected value first, then put the actual value (aka the value that we are testing).
