- 2 programming approaches:

1. [Programming by contract](#1-programming-by-contract)
2. [Defensive programming](#2-defensive-programming)
   - use `assert()` to validate assumptions

## 1. Programming by contract:

- Definition:
  - Class states the contract.
  - Client agrees to meet the conditions (usually preconditions).
  - Class agrees to perform the duty.
- Types of conditions:
  - **preconditions**: What the client ensures to meet before calling the method.
  - **postconditions**: What the class ensures when method finishes.
  - **invariants**: Properties/conditions that must always be true throughout the execution of a method or the life cycle of an object (often on a class)
    - ex: field `balance` of a `BankAccount` class should always > 0 --> invariant.
- Benefits:
  - removes duplicate validity checks -> reduce system complexity
    - otherwise, client & class check for valid values.

## 2. Defensive programming:

- Definition:

  - Class ensures it's always in a valid state.
    - all input values and actions are validated by the class.
    - [using `assert`](#assert) to validate
  - Client code doesn't have to do anything.

- Benefits:
  - errors in calling code are caught quickly.
    - **_suggestion_**: should use for all calls accessible by untrusted code.

### Assertions:

- `assert` triggers a runtime error (i.e: crash the program) if a condition is false/invalid.
- Benefit:
  - convert a Logic error into a **Runtime error** -> helps debug faster.
- Enabling assertions: must be enabled in JVM `-ea`.
- Note: use to check for programmer errors, not "possible or UI" errors

### Error Handling options:
