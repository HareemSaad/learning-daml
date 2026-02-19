# DAML

DAML is a smart contract language designed to build composable applications on the DAML Ledger Model.

**Example:** Alice buys a scooter from Bob.

## Smart Contracts

- Are self-executing contracts with the terms of the agreement directly written into code
- In one atomic transaction, they can transfer assets, update records, and trigger other actions
- In the example: the smart contract would transfer ownership and transfer payment from Alice to Bob in one atomic transaction

## Composable Applications

- Are applications that can be easily combined and reused across different contexts
- Like microservices
- Smaller workflows can be stitched together to create larger workflows
- In the example: the scooter purchase workflow can be combined with a financing workflow, where Alice can finance the purchase of the scooter through a loan from a bank

## DAML Ledger Model

- Record of transactions that are executed as a part of a workflow
- Ledger is shared between parties, and each party has a view of the ledger that is consistent with the other parties' views
- In the example:
  - DAML provides a shared ledger between Bob and the buyer's account
  - Bob gets to see the contracts executed for the scooters sold, and the bank gets to see the contracts based on the funds transferred to Bob

## Functional Programming Paradigm

As a language, it follows a functional programming paradigm. Meaning logic is written in functions. For example:

```daml
add x y = x + y
```

This function takes two arguments, `x` and `y`, and returns their sum.

## Advantages of Functional Programming in DAML

- **Composability:** Functions can be easily combined and reused across different contexts
- **Higher-order functions:** Can be passed as arguments to other functions, allowing for higher-order programming
- **Atomic:** Either successful or fails with an error, no side effects
- **Immutable variables:** Stateless functions

The DAML Standard Library is bundled with the SDK, such as `prelude`, which is automatically imported into every DAML file.
