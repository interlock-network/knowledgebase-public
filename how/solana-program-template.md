# How to set up a Solana program (smart contract)

## This document is a pointer to the [Solana program template repository.](https://github.com/interlock-network/solana-program-template)

The purpose of the template is to show you how to create a comprehensive Solana smart contract, known in the Solana world as a **_program_**.

This template **does not rely on any frameworks, such as Anchor**. From an engineering durability standpoint this is good, because the documentation for Solana frameworks is ..not the best, and besides, black boxes run more risk for potentially exploitable 'undocumented features'.

This template contains enough code to present a compiling program that demonstrates the minimum main inner workings of a Solana program, but without getting into specific tasks.

The program itself contains references to fictitious accounts provided by the client, so unless those are accounted for, instructionOne will throw an error.

THIS TEMPLATE DOES **NOT** CONTAIN TESTS.

## As best-practice, in part specified by the [**Solana Cookbook**](https://solanacookbook.com/core-concepts/programs.html#writing-programs),

a complex Solana program should be broken into five main modules, plus utilities, and a lib file to link everything together, like so:

1. **entrypoint**
2. **processor**
3. **instruction**
4. **state**
5. **error**

for large projects,

6. **utils**

which in typical fashion are linked together via

7. **lib.rs**

.

## Quick overview of components

### **entrypoint**
> The entrypoint module contains _entrypoint.rs_, which is the interface between the program and the Solana runtime BPF loader. This is like the front door; you can't get in without it.

### **processor**
> The processor module contains components necessary to run the program, and process instructions as specified by a transaction. These components in general are _run.rs_ containing the ```run_process``` function which matches incoming instructions to the appropriate process function. In addition to _run.rs_, processor will contain one file per process instruction, eg _instructionOne.rs_, _instructionTwo.rs_, etc. Processor is the most complicated module.

### **instruction**
> The instruction module in general contains two components, and serves to handle incoming instruction data. One is _data.rs_, which declares the ```enum``` for all instructions' ```instruction_data```. The other is _unpack.rs_, which contains the function responsible for unpacking incoming ```instruction_data``` --returning data variables, and matching the incoming instruction tag with the appropriate instruction.

### **state**
> The state module deals with the interface between the program, and any onchain accounts that may be storing program state. _As a reminder, Solana programs, unlike Ethereum smart contracts, are **stateless**_. All state variables must be stored in dedicated non-executable accounts onchain. In general the state module will contain ```Pack``` crate implementations, one for each type of account. For example, the first account type would be specified in _FIRST.rs_, the second account type in _SECOND.rs_, and so on. Each implementation defines the appropriate ```struct```, along with the serialization and deserialization Pack implementations.

### **error**
> It helps to have some custom error types defined, and in general the error module will just have one _error.rs_.

### **utils**
> For large projects, a utilites module is conventient to define global constants and make code more reusable, the usual stuff.

### **lib.rs**
> This is standard Rust module management.

## Resources

For a smaller version of this template format, but a more complete demonstration of an end-to-end fully functioning Solana program, [check out PaulX Programming on Solana - An Introduction, Escrow Program](https://paulx.dev/blog/2021/01/14/programming-on-solana-an-introduction/).

For a hello world, but not best-practice structuring, [check out the Solana Labs Hello World Example](https://github.com/solana-labs/example-helloworld).

[The Solana cookbook is here.](https://solanacookbook.com)

[The Solana docs are here.](https://docs.solana.com/introduction)

[Solana-program Rust docs are here.](https://docs.rs/solana-program/latest/solana_program/)

