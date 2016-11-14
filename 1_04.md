# 1.4 Defining programming

**Programming** is the process of taking an algorithm (the formulation of a computing problem) and encoding it into an executable computer program by using a programming language. Without an algorithm there can be no program.

An algorithm is a self-contained step-by-step set of operations to perform to produce the intended result. It also describe the data needed to represent the problem instance. Programming languages have some primitive building blocks for the description of data and the processes or transformations applied to them.

This control constructs allow algorithmic steps to be represented in a convenient and unambiguous way.   
To be used for algorithm representation a programming language must provide the following basic instructions:
 - Input: Get in data from a keyboard, a file, or another source.
 - Output: Display data on the screen or to a file or by another way.
 - Arithmetic: Perform basic arithmetical operations like addition and multiplication.
 - Conditional Execution: Check for certain conditions and execute the appropriate sequence of statements.
 - Repetition: Perform some action repeatedly, usually with some variation.

All data items in the computer are represented as strings of binary digits. In order to give these strings meaning, we need to have **data types**.  
For example, most programming languages provide a data type for integers. Strings of binary digits in the computer’s memory can be interpreted as integers and given the typical meanings that we commonly associate with integers (e.g. 23, 654, and -19). In addition, a data type also provides a description of the operations that the data items can participate in. With integers, operations such as addition, subtraction, and multiplication are common. We have come to expect that numeric types of data can participate in these arithmetic operations.

Unlike lower-level languages, JavaScript is a loosely typed/dynamic language. That means you don't have to declare the type of a variable ahead of time. The type will get determined automatically while the program is being processed. That also means that you can have the same variable as different types:

```javascript
var foo = 42;    // foo is now a Number
var foo = "bar"; // foo is now a String
var foo = true;  // foo is now a Boolean
```

The difficulty that often arises for us is the fact that problems and their solutions are very complex. These simple, language-provided constructs and data types, although certainly sufficient to represent complex solutions, are typically at a disadvantage as we work through the problem-solving process. We need ways to control this complexity and assist with the creation of solutions.