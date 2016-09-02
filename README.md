# Why this book?

As a curious JavaScript developer, I was an early adopter of NodeJS. As I was moving to server-side programming, I need to implement data structures like linked lists, stacks and queues and there associated algorithms. Since I am an autodidact without computer science degree, I encountered several issues. Back in 2009, they was nothing about data structure in JavaScript so I have to study it in classic object-oriented languages like Java and C#. Today, things are slowly changing. But I still see many JavaScript developer moving to the server-side, don't know nothing about data structures and why studying them is important.
Through this guide, I will explain you what are the different data structures, their usages and implementation for server-side as well as their limitation due to JavaScript.

At the end, you will be able to chose the right data structure for the problems you have to solve.

# Getting Started
As developers, we are living in a world in rapid evolution. This is especially true in the JavaScript ecosystem and its constant growing number of tools, framworks and platforms. Nonetheless, the basic principles of computer science are still the foundation on which we stand when we use computers to solve problems.

You may have spend a l...

# Defining computer science
Computer science is a discipline that spans theory and practice. In short, it's the study of problems, problem-solving, and the solutions that come out of the problem-solving process. The solution is called an **algorithm**. An algorithm is a step-by-step set of operations for solving a clearly defined problem.

However, consider the fact that some problems may not have a solution. This assumption mean that we have to redifine computer science as the study of solutions to problems as well as the study of problems with no solutions.

As we are talking about computer science as a problem-solving process, it mean we have to approach the study of **abstraction**.
Abstraction allows us to separate problem and solution. Let's illustrate this separation with example:  
Consider the legs that you may use when you wake up the morning and go to the bathroom. You get up and put one foot before the other to your destination with a success conditioned by the level of alcohol you ingested the night before. From an abstraction point of view, we can say that you are seeing the logical perspective of the legs. You are using the functions provided by the evolution for the purpose of transporting you from one location to another. These functions are sometimes also referred to as the interface.

On the other hand, the surgeon who must treat a leg takes a very different point of view. She not only knows how to walk but must know all of the details necessary to carry out all the functions that we take for granted. She needs to understand how the body works, how the blood feeds the muscles, the way nerves transmit impulses from the brain, and so on. This is known as the physical perspective, the details that take place “under the hood.”

The same thing happens when we use computers. Most people use computers to surf the web, send and receive emails, without any knowledge of the details that take place to allow those types of applications to work. They view computers from a logical or user perspective. Peoples behind the scene take a very different view of the computer. They must know the details of how operating systems work, how network protocols are configured, and how to code various scripts that control function. They must be able to control the low-level details that a user simply assumes.

As another example of abstraction, consider the math.js library. Once we import the module, we can perform computations such as

```javascript
import math from mathjs

math.sqrt(-4);                    // 2i
```

This is an example of **procedural abstraction**. We do not necessarily know how the square root is being calculated, but we know what the function is called and how to use it. If we perform the import correctly, we can assume that the function will provide us with the correct results. We know that someone implemented a solution to the square root problem but we only need to know how to use it. This is sometimes referred to as a “black box” view of a process. We simply describe the interface: the name of the function, what is needed (the parameters), and what will be returned.

# Defining programming 