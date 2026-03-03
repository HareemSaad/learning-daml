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

### Custom Records

Define custom data types using the `data` keyword with named fields. Syntax:

```daml
data TypeName = TypeName with
  field1 : Type1
  field2 : Type2
  deriving (Eq, Show)  -- optional: inherit standard behaviors
```

**Creating instances**: Use `TypeName with field1 = value1, field2 = value2`

**Accessing fields**: Use dot notation `instance.fieldName`

**Updating records**: Create a modified copy with `instance with fieldName = newValue` without mutating the original

Use custom records to group related data together, improve type safety, and make code more readable and maintainable. The `deriving` clause automatically implements equality comparison (`Eq`) and string representation (`Show`) for your type.

### Type Classes

A type class defines a contract—a set of functions that any data type can implement. Type classes enable polymorphic behavior: writing generic functions that work with multiple different types.

**Define a type class** using the `class` keyword:

```daml
class ClassName a where
  functionName : Type
```

**Implement a type class** using the `instance` keyword:

```daml
instance ClassName ConcreteType where
  functionName = implementation
```

**Use type class constraints** in function signatures with `=>`:

```daml
functionName : ClassName a => a -> ReturnType
```

**When to use**: Type classes provide shared behaviors across unrelated types. Use them to write generic, reusable functions that work with any type that implements the class. This avoids code duplication and allows flexible, polymorphic code that can work with current and future types.

### Type Variables

A type variable is a placeholder for any concrete type, written as a single lowercase letter (e.g., `a`, `b`, `t`). Type variables enable generic functions that work with multiple different types without duplicating code.

**Syntax**: Type variables appear in function signatures:

```daml
genericFunction : a -> b -> c  -- a, b, c are type variables
```

**Type class constraints**: Restrict what types a variable can represent. Use `=>` to specify requirements:

```daml
constrainedFunction : Show a => a -> Text  -- 'a' must be an instance of Show class
```

The constraint `Show a =>` means the function can accept any type `a` as long as it implements the `Show` type class (enabling conversion to text).

**When to use**: Write generic functions with type variables when the same logic applies to multiple types. Use type class constraints to ensure types have the necessary capabilities without losing flexibility. This creates reusable, type-safe code that works with any type meeting the constraints, including types defined in the future.

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

## Iteration

### Functional Programming Patterns

**Recursion**: Functions call themselves with modified arguments to solve problems. Use guards to define base cases (when to stop recursing) and recursive cases (when to recurse again).

**Map**: Applies a function to every element in a list and returns a new list of transformed elements. Syntax: `map (function) list`. Use when you need to transform all elements in a list while keeping the list structure.

**Fold**: Reduces a list to a single value by accumulating results through repeated application of a function. Takes three arguments: a binary function, an initial accumulator value, and a list.

- `foldl`: Processes list left-to-right. Use for sequential operations like summing or building up results from left.
- `foldr`: Processes list right-to-left. Use when the associativity of right-to-left matters or when working with infinite lists.

Syntax: `foldl (binary_function) initial_value list` or `foldr (binary_function) initial_value list`

## Option Type

The `Optional` type (or `Option` in some contexts) represents a value that may or may not exist. It safely handles absence without relying on null, preventing null-reference errors.

**Forms**:

- `Some a`: Contains a value of type `a`
- `None`: Represents the absence of a value

**Creating Optional values**:

- `Some value`: Wrap an existing value
- `None`: Represent absence

**Handling Optional values**: Use `case` expressions to safely extract values:

```daml
case optionalValue of
  Some x -> -- handle the value x
  None -> -- handle absence
```

**When to use**: Return `Optional` from functions that might fail or produce no result (e.g., safe division by zero, searching for an element that may not exist, parsing that may fail). This forces callers to explicitly handle the possibility of absence, eliminating common programming errors from unexpected null/None values.

## Either Type

The `Either` type represents a value that is one of two possible types, typically used to communicate success or failure with additional information. Unlike `Optional`, `Either` can return either an error message or a success result.

**Forms**:

- `Left a`: Represents the first outcome, conventionally an error of type `a`
- `Right b`: Represents the second outcome, conventionally a success value of type `b`

**Creating Either values**:

- `Left errorValue`: Wrap an error or failure reason
- `Right successValue`: Wrap a successful result

**Handling Either values**: Use `case` expressions to branch on the outcome:

```daml
case eitherValue of
  Left error -> -- handle the error
  Right success -> -- handle the success value
```

**When to use**: Return `Either` from validation functions or operations that can fail with meaningful error information (e.g., parsing with error messages, computations with validation rules). This allows callers to distinguish between different failure types and handle errors appropriately, making error handling explicit and recoverable.

## Records

## Essential Functions for Scripting and Debugging

These functions are invaluable when writing Daml Scripts for testing or debugging your logic.

`String Concatenation (<>)`: To join two Text values, use the <> operator. This is most common when creating descriptive debug messages.

`show`: The versatile show function converts a value of almost any other type (like an Int or Date) into its Text representation. This is essential when you need to combine text with other data types for display, as you can only concatenate Text with other Text.

`setTime`: When testing time-dependent logic in a Daml Script, the setTime function is indispensable. It allows you to manually set the ledger's effective time, so you can test scenarios like contract expirations without having to wait.
