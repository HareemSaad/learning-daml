# DAML Language

## Defining Functions

```daml
<name>: <type> -> <type>
```

## Calling Functions

```daml
<function-name> <argument1> <argument-n>... = <function-body>
-- example: hello name = "Hello, " <> name <> "!"
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
