# What is SQLite

## Lightweight
Its files are only a few hundred kiB. 

## Embeddable
It can be used in the same process. There is no requirement for a separate process. 

## It supports ACID properties
ACID (atomicity, consistency, isolation, durability) 

## Crash Recovery

## Thread Safe

## Cross Platform
Any DB file created can literally be copied and pasted to another OS and everything will work just the same.

## Simple


# Architecture

## Tokeniser
The tokeniser reads the word in the input string and transforms them into their corresponding number. Each command or allowed character has a designation number.

## Parser
At its core, this component checks to see if the tokens satisfy certain grammar rules. If they do, it calls a specific function.

## Byte Code Generator
Each SQL statement is essentially its own computer program with the text command as its source code. The byte code generator creates a prepared SQL statement, binds information to it (like a name, perhaps), sends the command to the VDBE, resets the statement, and then destroys it.