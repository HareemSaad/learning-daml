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
- Infix: can write ` 1 `add` 2` instead of `add 1 2`
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
- `Int`: Integer numbers

## conditional expressions

- `do`: runs multiple expressions in sequence