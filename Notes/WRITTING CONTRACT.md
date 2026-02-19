# Writing Contracts

Code is written in `daml/*.daml` files.

- File name must start with a capital letter
- File must end with `.daml`

## Module Definition

Define module at the top of the file:

```daml
module <file-name> where
```

- has to match the file name (without the .daml extension)
- has to be at the top of the file, before any imports or code

## Testing Functions

To test a function, you need to write a script in `daml/Main.daml`:

```daml
-- import script library
import Daml.Script

-- test function
-- to run the test, click Script results over the testHello function (only in DAML IDE)
-- define a script to test the hello function
testHello: Script()
testHello = script do
  -- call the hello function and print the result
  debug $ hello "DAML"
```