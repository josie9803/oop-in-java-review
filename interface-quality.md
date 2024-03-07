# Interface Quality

- 2 points of view:

  1. user/client:

  - goals:
    - easy to understand (i.e: clear abstraction)
    - easy to use

  2. designer/programmer:

  - goals:
    - easy to design
    - easy to implement

- Challenges: easy to implement does not equal to easy to understand/use

- 4C's for interface quality analysis process:

1. [Cohesion](#1-cohesion)
2. [Completeness / Convenience](#2-completeness-convenience)
3. [Clarity](#3-clarity)
4. [Consistency](#4-consistency)
5. [Other factors](#5-other-ways-to-evaluate)

### 1. Cohesion:

- Interface methods should relate to a single abstraction
  - **Single Responsibility Principle**
- Solution:
  - split into multiple classes, each handles a single responsibility.
  - breaking encapsulation.

### 2. Completeness/ Convenience:

- Interface should have all features that client needs.
- Solution:
  - add features so that when client code uses the features they can use it most conveniently.
  - constructors create fully-formed objects.
  - implement `Iterable/ Comparable` ... when appropriate.

### 3. Clarity:

- Interface should be clear to programmer: clear naming, abstraction.
- Solution:
  - use well named classes, methods and variables to be intention revealing.
  - use meaningful abstractions.
  - one name for each idea.

### 4. Consistency:

- Everything should be consistent!
- Solution:
  - make things consistent!

### 5. Other ways to evaluate:

1. Mutability
    - is this class need to be changed?
2. Simplicity
3. Repetitive code
4. Maintainability
5. Scalability (not taught in this course)

