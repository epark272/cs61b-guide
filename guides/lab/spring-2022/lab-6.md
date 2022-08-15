---
description: Unit Testing and Acceptance Testing for Enigma
---

# Lab 6

Lab spec: [https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab6/index.html](https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab6/index.html)

Welcome to lab 6! As a reminder of project collaborations policies:

> **We highly encourage you to work with a partner to understand Enigma, Permutations, the existing testing methods and utilities, and brainstorming tests and edge cases. HOWEVER, if you are planning on using the tests you write in this lab in your project,** _you will need to do the actual code-writing by yourself_**, since code for projects (including tests) must be written by you alone as per our** [**Project Collaboration Policy**](https://inst.eecs.berkeley.edu/\~cs61b/sp22/about.html#r-project-collaboration-policy)**.**

## Testing

I'll be operating under the assumption that you already know how to write tests. If not, see the [lab spec](https://inst.eecs.berkeley.edu/\~cs61b/sp22/materials/lab/lab6/index.html) or [my lab 2 guide](lab-2.md)!

My general approach to writing tests is to start small and work your way up to increasingly large and complex tests. This is what unit tests are great at! When writing tests, it's important to cover a large range of cases. The following list of what I like to check for is by no means comprehensive and can always be improved upon or added to.

* A few simple cases to establish basic functionality
* Any special cases involving 0, false, "", \[], {}, and null
* Any special cases involving 1, true, or objects with exactly one element
* Any special cases involving the limitations (or intended limits) of the function
* Any specific cases relevant to the function
  * For example, I would test that a prime number checker labels 2 as prime
* Any cases where an error is expected, such as passing in an invalid type
