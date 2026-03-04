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

## Actors (Parties)

Actors are the parties involved in contracts. They are represented by the `Party` type. Parties can be

- signatories (authorize changes)
- observers (see contracts)
- controllers (exercise choices).

## Templates

Templates are blueprints for contracts on the ledger. Define them with the `template` keyword followed by data fields in a `with` block.

**Signatories**: Parties who must authorize contract creation and transitions. Use `signatory <party>`. At least one signatory is required.

**Observers**: Parties who can see the contract but cannot authorize changes. Use `observer <party>`. Observers must be able to see a contract before they can exercise choices on it.

**Validation**: Use `ensure` to add constraints. Example: `ensure name /= ""` prevents empty names.

## Choices

Choices are contract actions that create new contract states. They represent transitions and business logic.

**Syntax**: Define with `choice <Name> : <ReturnType>` (capitalized name, colon for return type).

**Controller**: Specifies which party can exercise the choice. Use `controller <party>`. The controller must be a signatory or observer.

**Consuming vs Nonconsuming**: By default, choices are consuming (archive the old contract). Use `nonconsuming` to read state without archiving.

**State Updates**: DAML has no mutable state. Update by creating a new contract with `create this with <field> = <newValue>` and archiving the old one.

**Assertions**: Use `assert` to validate conditions. Fails the transaction if false.

**Return Values**: Choices can return contract IDs, tuples, or any type. Use `return` to specify what the choice produces.

## Testing Contracts

Use `allocateParty` to create test parties. Use `submit <party> do` to execute actions as a party. Use `exerciseCmd` to exercise choices and `createCmd` to create contracts. Use `debug` to print values and `assertMsg` to verify expected results.
