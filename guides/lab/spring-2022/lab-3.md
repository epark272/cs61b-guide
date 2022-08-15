---
description: IntDLists and Debugging
---

# Lab 3

Lab spec: [https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab3/index.html](https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab3/index.html)

Welcome to lab 3! I won't be covering Git in this lab, but if you need a more comprehensive guide, you can use [this](https://inst.eecs.berkeley.edu/\~cs61b/sp22/docs/using-git.html).

## IntDList

An `IntDList` is like an `IntList`, but each node has pointers to both the previous element _and_ the next element. Here is an illustration from the lab spec:

![An IntDList has a \_front and \_back pointer, and each node has a \_prev, \_val, and \_next field.](<../../../.gitbook/assets/image (1).png>)

Your assignment is to fill out the various methods in `IntDList.java`. I recommend trying to implement these without seeing the following tips, and if you get stuck then come back to these.

<details>

<summary><code>getNode()</code></summary>

You'll need to follow the `_next` pointers to get to the next node. Remember that the first node is index 0.

</details>

<details>

<summary><code>get()</code></summary>

While you could copy your code from `getNode()` and make one change, this is bad practice! Instead, try using `getNode()` in order to do all that work for you :)

</details>

<details>

<summary><code>size()</code></summary>

One approach I see students often doing is iterating through the entire list and counting how many nodes there are. While this will get the right answer, it's inefficient. Instead, why not define a `_size` instance variable? (hint: when do you need to increment/decrement this variable). Using this approach will make this method very simple, although it will add more things for you to do in other methods.

</details>

<details>

<summary><code>insertFront()</code>/<code>insertBack()</code></summary>

* If you do `insertAtIndex()`, these methods will become easy. Inserting at the front is like inserting at which index? Inserting at the back is like inserting at which index?
* I will compile tips for these two methods in `insertAtIndex()`, since it's most general.

</details>

<details>

<summary><code>deleteFront()</code>/<code>deleteBack()</code></summary>

* If you do `deleteAtIndex()`, these methods will become easy. Deleting at the front is like deleting at which index? Deleting at the back is like deleting at which index?
* I will compile tips for these two methods in `insertAtIndex()`, since it's most general.

</details>

<details>

<summary><code>insertAtIndex()</code></summary>

If you're having a lot of trouble with this, go complete `insertFront()`/`insertBack()` and come back to this. For someone who knows how to manipulate the `IntDList`, doing this first is easier; but if you're still figuring it out, it's easier to figure out one case at a time.

To insert a node at index `i`, you need to keep track of 4 pointers: `i-1`'s `_next` pointer, `i`'s `_prev` pointer, and the new node's `_prev` and `_next` pointers. You need to set the new node's `_prev` pointer to point to `i-1`, and the new node's `_next` pointer to point to `i`. Then, you need to set both `i-1`'s `_next` pointer and `i`'s `_prev` pointer to point to the new node.&#x20;

Now here comes the tricky part: when the node you insert is the first item, there is no `i-1`'s `_next` pointer because node `i-1` doesn't exist. Instead, that's taken up by the `_front` pointer. Furthermore, the new node's `_prev` pointer needs to be set to null. You'll need to set up conditional statements to catch this case. **The same thing needs to be done for the last item, except in reverse.**

**The order in which you do these operations is important.** If you mix up the order, the indices will change, and it'll be a lot harder to keep track of which node is at which index. That being said, if you can keep track of it, then there's nothing inherently wrong with doing the operations in a different order.

</details>

<details>

<summary><code>deleteAtIndex()</code></summary>

If you're having a lot of trouble with this, go complete `deleteFront()`/`deleteBack()` and come back to this. For someone who knows how to manipulate the `IntDList`, doing this first is easier; but if you're still figuring it out, it's easier to figure out one case at a time.

To delete a node at index `i`, you need to keep track of 2 pointers: `i-1`'s `_next` pointer and `i+1`'s `_prev` pointer. You'll have to set both `i-1`'s `_next` pointer to point to `i+1` and `i+1`'s `_prev` pointer to point to `i-1`. Note that you don't need to worry about unsetting `i`'s pointers because node `i` will get **garbage collected**.

Like `insertAtIndex()`, there are also special cases for the first and last element. In the case of the first element, there is no node `i-1`, so instead of assigning `i-1`'s `_next` pointer, you need to assign the `_front` pointer. This is the same for the last item, except opposite.

</details>

## BuggyIntDList

**I cannot stress how important it is to learn how to use the debugger and the Java visualizer in order to succeed in this class.** You do _not_ want to be 30 hours into a project worth \~15% of your grade, stressing about a bug that you can't seem to track down, seemingly trying everything but having all the test cases fail, submitting Gitbugs only for them to get rejected (due to no apparent debugging effort), all because you didn't learn how to debug.

Some of you might shrug this warning off thinking that "it won't happen to _me_", only to find yourself in this exact scenario a few short weeks or months later. **Trust me, spend 30 minutes to learn how to debug now, and you'll save yourself hours of frustration in the rest of this course.** Take this exercise seriously, do everything that it tells you to do, and you'll thank yourself later.
