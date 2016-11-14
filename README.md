# 1.1 Why this book?

As a curious JavaScript developer, I was an early adopter of NodeJS. As I was moving to server-side programming, I need to implement data structures like linked lists, stacks and queues and there associated algorithms. Since I am an autodidact without computer science degree, I encountered several issues. Back in 2009, they was nothing about data structure in JavaScript so I have to study it in classic object-oriented languages like Java and C#. Today, things are slowly changing. But I still see many JavaScript developer moving to the server-side, don't know nothing about data structures and why studying them is important.
Through this guide, I will explain you what are the different data structures, their usages and implementation for server-side as well as their limitation due to JavaScript.

At the end, you will be able to chose the right data structure for the problems you have to solve.

# 1.10 Input and Output
We often have a need to interact with users, either to get data or to provide some sort of result. Most of the time we use an HTML form as a way of asking the user to provide some type of input. In our case, we will avoid this and use much simpler functions.

## 1.10.1 Client side
JavaScript provides us with a function that allows us to ask a user to enter some data and returns a reference to the data in the form of a string. The function is called `prompt()`.

A prompt dialog contains a single-line textbox, a Cancel button, and an OK button, and returns the (possibly empty) text the user entered into that textbox.

```javascript
var fruit = prompt("What's your favorite fruit?");

if (fruit.toLowerCase() == "apple") {
  alert("Wow! I love apples too!");
}
```

## 1.10.2 Server side (Node.js)
On the server, we need to use the `readline` module. It provides an interface for reading data from a Readable stream (such as process.stdin) one line at a time.

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question("What's your favorite fruit? ", (answer) => {

  if (answer.toLowerCase() == "apple") {
    console.log("Wow! I love apples too!");
  }

  rl.close();
});
```

_Note_ Once this code is invoked, the Node.js application will not terminate until the readline.Interface is closed because the interface waits for data to be received on the input stream.