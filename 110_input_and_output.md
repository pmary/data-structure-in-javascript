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