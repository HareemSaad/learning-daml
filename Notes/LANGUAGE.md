# DAML Language

## Declaring Functions

```daml
<name>: <type> -> <type>
```

- must start with a lowercase letter
- Left-hand side type is the argument type and can be many separated by `->`
- Right-hand side type is the return type
- Strong type checking id return value does not match the return type

## Defining Functions

```daml
<function-name> <argument1> <argument-n>... = <function-body>
-- example: hello name = "Hello, " <> name <> "!"
```

- has to be defined right after the function declaration

## Calling Functions

```daml
<function-name> <argument1> <argument-n>... 
-- example: hello "DAML"
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