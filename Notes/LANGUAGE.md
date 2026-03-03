# DAML Language

## Functions

### Declaring Functions

```daml
<name>: <type> -> <type>
```

- must start with a lowercase letter
- Left-hand side type is the argument type and can be many separated by `->`
- Right-hand side type is the return type
- Strong type checking id return value does not match the return type

### Defining Functions

```daml
<function-name> <argument1> <argument-n>... = <function-body>
-- example: hello name = "Hello, " <> name <> "!"
```

- has to be defined right after the function declaration

### Calling Functions

```daml
<function-name> <argument1> <argument-n>...
-- example: hello "DAML"
```

### Conventions

#### Left & Right Associativity

Associativity is a property of binary operations or functions. If a function is associative, it means that rearranging the order of the expressions won't change the results. For example, the addition function is associative. You can parse it from left to right or from right to left, and the result will come out to be the same. But some functions are required to be parsed from left to right. This is called left associativity. For example, subtraction and division are left associative function. .

#### Currying

Currying is the process of converting a function with multiple arguments to a function that takes a single argument and returns another function.

normal function:

```daml
add x y = x + y
increment x = x + 1
```

increment function can also be written as

```daml
increment = add 1 x
increment = add 1
```

increment x is the curried form of add 1 x.

Currying allows us to create new functions by partially applying existing functions. In this case, we can create an increment function by partially applying the add function with the first argument set to 1.

#### Infix/Prefix Notations

- Infix: can write `1`add` 2` instead of `add 1 2`
- Prefix: can write `(+) 1 2` instead of `1 + 2`

#### Lambda Functions

- uses inline notation
- nameless
- used only once / anonymous functions
- \ indicates a lambda function

```daml
-- example: add 1 2 can be written as (\x y -> x + y) 1 2
```

## Commenting Code

```daml
-- this is a comment
```

## Printing to Console

```daml
debug <message>
debug $ <function call>
```

## Data Types

- Numbers
  - Int (64 bit signed integer)
  - Numeric n (decimals with precision of 36 and scale of n, n is the number of digits after the decimal point)
  - Decimal (decimals with precision of 36 and scale of 10)
- Text (Text values are strings of characters enclosed by double quotes) (Text literals support backslash escapes to include their delimiter (\") and a backslash itself (\\))
- Boolean
- Time
  - Date (date 2007 Apr 5 Permissible dates range from 0001-01-01 to 9999-12-31 (using a year-month-day format).)
  - Time (time (date 2007 Apr 5) 14 30 05 Time values have microsecond precision with allowed range from 0001-01-01 to 9999-12-31 (using a year-month-day format))
  - RelTime (seconds 1, seconds (-2) RelTime values have microsecond precision with allowed range from -9,223,372,036,854,775,808ms to 9,223,372,036,854,775,807ms There are no literals for RelTime. Instead they are created using one of days, hours, minutes, seconds, milliseconds and microseconds (to get these functions, import DA.Time).)

## Data Structures

- Lists: [a] is the built-in data type for a list of elements of type a. The empty list is denoted by [] and [1, 3, 2] is an example of a list of type [Int].
- Tuples: type MyTuple = (Int, Text)
- Sets
- Maps

## Conditional Expressions

### Control Flow Patterns

**Conditionals.daml** demonstrates three fundamental control flow patterns in DAML:

1. **If-Then-Else**: Simple binary conditional logic (e.g., `getTradingFee` applies fees based on trade amount)
2. **Guards**: Pattern matching with conditions using `|` syntax for cleaner multi-branch logic (e.g., `getUserTier` categorizes users by trade count)
3. **Case Expressions**: Pattern matching on specific values or custom data types (e.g., `getStatusMessage` matches on `UserStatus` enum variants)

**ControlFlow.daml** demonstrates applying these three patterns to solve the same problem (grade calculation):

- `getLetterGradeUsingIf`: Nested if-else chains
- `getLetterGradeUsingGuards`: Guard clauses for readability
- `getScoreUsingCase`: Case expression for text matching
- `getAverageGradeLetter`: Combines guards with `where` clauses for local variable binding

Each pattern offers different readability and maintainability benefits depending on the use case.

## Essential Functions for Scripting and Debugging

These functions are invaluable when writing Daml Scripts for testing or debugging your logic.

`String Concatenation (<>)`: To join two Text values, use the <> operator. This is most common when creating descriptive debug messages.

`show`: The versatile show function converts a value of almost any other type (like an Int or Date) into its Text representation. This is essential when you need to combine text with other data types for display, as you can only concatenate Text with other Text.

`setTime`: When testing time-dependent logic in a Daml Script, the setTime function is indispensable. It allows you to manually set the ledger's effective time, so you can test scenarios like contract expirations without having to wait.
