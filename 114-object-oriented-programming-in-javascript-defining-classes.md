# 1.14 Object-Oriented Programming in JavaScript: Defining Classes

Object-oriented to the core, JavaScript features powerful, flexible OOP capabilities. So far, we have used a number of built-in classes to show examples of data and control structures. One of the most powerful features in an object-oriented programming language is the ability to allow a programmer \(problem solver\) to create new classes that model data that is needed to solve the problem.

Remember that we use abstract data types to provide the logical description of what a data object looks like \(its state\) and what it can do \(its methods\). By building a class that implements an abstract data type, a programmer can take advantage of the abstraction process and at the same time provide the details necessary to actually use the abstraction in a program. Whenever we want to implement an abstract data type, we will do so with a new class.

## 1.14.1. A Fraction Class

A very common example to show the details of implementing a user-defined class is to construct a class to implement the abstract data type `Fraction`.

A fraction such as `3/5` consists of two parts. The top value, known as the numerator, can be any integer. The bottom value, called the denominator, can be any integer greater than 0 \(negative fractions have a negative numerator\). Although it is possible to create a floating point approximation for any fraction, in this case we would like to represent the fraction as an exact value.

The operations for the `Fraction` type will allow a `Fraction` data object to behave like any other numeric value. We need to be able to add, subtract, multiply, and divide fractions. We also want to be able to show fractions using the standard “slash” form, for example `3/5`. In addition, all fraction methods should return results in their lowest terms so that no matter what computation is performed, we always end up with the most common form.

In JavaScript ES2016, we define a new class by providing a name, a constructor and a set of method definitions that are syntactically similar to function definitions.

```js
class Fraction {
  constructor() {
  }
  // The methods go here
}
```

The first method that all classes should provide is the constructor. This is a special method with the name "constructor"  for creating and initializing an object created with a class. To create a `Fraction` object, we will need to provide two pieces of data, the numerator and the denominator.

```js
class Fraction {
    constructor(top, bottom) {
        this.num = top;
        this.den = bottom;
    }
}
```

As described earlier, fractions require two pieces of state data, the numerator and the denominator. The notation `this.num` in the constructor defines the fraction object to have an internal data object called num as part of its state. Likewise, `this.den` creates the denominator. The values of the two formal parameters are initially assigned to the state, allowing the new `fraction` object to know its starting value.

To create an instance of the `Fraction` class, we must invoke the constructor. This happens by using the name of the class and passing actual values for the necessary state \(note that we never directly invoke `constructor`\). For example:

```js
var myFraction = new Fraction(3, 5);
```

It creates an object called `myFraction` representing the fraction 3/5 \(three-fifths\). The next thing we need to do is implement the behavior that the abstract data type requires. To begin, consider what happens when we try to print a `Fraction` object.

```js
var myFraction = new Fraction(3, 5);
console.log(myFraction);
// Fraction {num: 3, den: 5}
```

What it does is printing a reference to the object but we may want to print the fraction state in the proper format. For this, we will create a `show` method that allows us to view the fraction using the standard “slash” form.

```js
class Fraction {
    constructor(top, bottom) {
        this.num = top;
        this.den = bottom;
    }

    show() {
        console.log(`${this.num}/${this.den}`);
    }
}

var myFraction = new Fraction(3, 5);
myFraction.show();
// 3/5
```

Next we would like to be able to create two `Fraction` objects and then add them together using the standard "+" notation. At this point, if we try to add two fractions, we get the following:

```js
var f1 = new Fraction(1, 2);
var f2 = new Fraction(1, 4);
f1+f2;
"[object Object][object Object]"
```

Since we cannot overload operators in JavaScript, we can fix this by providing the `Fraction` class with a new `plus` method:

```js
plus(fraction) {
    let newnum = this.num * fraction.den + this.den * fraction.num;
    let newden = this.den * fraction.den;

    return new Fraction(newnum, newden);
}
```

```js
var f1 = new Fraction(1, 2);
var f2 = new Fraction(1, 4);
f3 = f1.plus(f2);
f3.show();
// 6/8
```

The `plus` method works as we desire, but one thing could be better. Note that 6/8 is the correct result \(1/4 + 1/2\) but that it is not in the "lowest terms" representation. The best representation would be 3/4. In order to be sure that our results are always in the lowest terms, we need a helper function that knows how to reduce fractions. This function will need to look for the greatest common divisor, or GCD. We can then divide the numerator and the denominator by the GCD and the result will be reduced to lowest terms.

The best-known algorithm for finding a greatest common divisor is Euclid’s Algorithm. It states that the greatest common divisor of two integers _m_ and _n_ is _n_ if _n_ divides _m_ evenly. However, if _n_ does not divide _m_ evenly, then the answer is the greatest common divisor of _n_ and the remainder of _m_ divided by _n_. So we will simply provide an iterative implementation of it.

> Note that this implementation of the GCD algorithm only works when the denominator is positive. This is acceptable for our fraction class because we have said that a negative fraction will be represented by a negative numerator.

```js
gcd(n = this.num, d = this.den) {
    while (m%n != 0) {
        let oldm = m;
        let oldn = n;

        m = oldn;
        n = oldm%oldn;
    }

    return n;
}
```

```js
var f1 = new Fraction(20, 10);
console.log( f1.gcd() );
// 10
```

Now we can use this function to help reduce any fraction. To put a fraction in lowest terms, we will divide the numerator and the denominator by their greatest common divisor. So, for the fraction 6/8, the greatest common divisor is 2. Dividing the top and the bottom by 2 creates a new fraction, 3/4:

```js
plus(fraction) {
    let newnum = this.num * fraction.den + this.den * fraction.num;
    let newden = this.den * fraction.den;
    let common = this.gcd(newnum, newden);

    return new Fraction( Math.trunc(newnum/common), Math.trunc(newden/common) );
}
```

```js
var f1 = new Fraction(1, 4);
var f2 = new Fraction(1, 2);
var f3 = f1.plus(f2);
f3.show();
// 3/4
```

> `Math.trunc()` is a new ES6 function. It work like `Math.floor()` but work for negative numbers too.

Our `Fraction` object now has two very useful methods. An additional group of methods that we need to include in our example Fraction class will allow two fractions to compare themselves to one another. Assume we have two Fraction objects, `f1` and `f2`. `f1==f2` will only be True if they are references to the same object. Two different objects with the same numerators and denominators would not be equal under this implementation. This is called **shallow equality**.

```js
var f1 = new Fraction(1, 4);
var f2 = new Fraction(1, 4);
f1==f2;
// false

var f1 = new Fraction(1, 4);
var f2 = f1;
f1==f2;
// true
```

We can create **deep equality** by the same value, not the same reference. So we will create a new method called `equal` to compares two objects and returns `True` if their values are the same, `False` otherwise.

```js
equal(fraction) {
    let firstNum = this.num * fraction.den;
    let secondNum = fraction.num * this.den;

    return firstNum == secondNum;
}
```

```js
var f1 = new Fraction(1, 4);
var f2 = new Fraction(1, 4);
f1.equal(f2);
// true

var f1 = new Fraction(1, 4);
var f2 = new Fraction(2, 8);
f1.equal(f2);
// true
```

Let's wrap it together:

```js
class Fraction {
  constructor(top, bottom) {
    this.num = top;
    this.den = bottom;
  }

  plus(fraction) {
    let newnum = this.num * fraction.den + this.den * fraction.num;
    let newden = this.den * fraction.den;
    let common = this.gcd(newnum, newden);

    return new Fraction( Math.trunc(newnum/common), Math.trunc(newden/common) );
  }

  gcd(n = this.num, d = this.den) {
    while (n%d != 0) {
      let oldm = n;
      let oldn = d;

      n = oldn;
      d = oldm%oldn;
    }

    return d;
  }

  equal(fraction) {
    let firstNum = this.num * fraction.den;
    let secondNum = fraction.num * this.den;

    return firstNum == secondNum;
  }

  show() {
    console.log(`${this.num}/${this.den}`);
  }
}
```

To make sure you understand how operators are implemented in Python classes, and how to properly write methods, write some methods to implement `*`, `/`, and `-` . Also implement comparison operators `>` and `<`.

## 1.14.2 Inheritance: Logic Gates and Circuits

Our final section will introduce another important aspect of object-oriented programming. **Inheritance** is the ability for one class to be related to another class in much the same way that people can be related to one another. Children inherit characteristics from their parents. But in Javascript, there is no `class` implementation. The `class` keyword introduced in ES6 is just a syntactical sugar. JavaScript remains prototype-based. When it comes to inheritance, JavaScript only has one construct: objects. Each object has an internal link to another object called its **prototype**. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. null, by definition, has no prototype, and acts as the final link in this **prototype chain**.

While this is often considered to be one of JavaScript's weaknesses, the prototypal inheritance model is in fact more powerful than the classic model. It is, for example, fairly trivial to build a classic model on top of a prototypal model. We refer to a child classes as **subclasses** and **superclasses**.

By organizing classes in this hierarchical fashion, object-oriented programming languages allow previously written code to be extended to meet the needs of a new situation. In addition, by organizing data in this hierarchical manner, we can better understand the relationships that exist. We can be more efficient in building our abstract representations.

To explore this idea further, we will construct a **simulation**, an application to simulate digital circuits. The basic building block for this simulation will be the logic gate. These electronic switches represent boolean algebra relationships between their input and their output. In general, gates have a single output line. The value of the output is dependent on the values given on the input lines.

AND gates have two input lines, each of which can be either 0 or 1 \(representing `False` or `True`, repectively\). If both of the input lines have the value 1, the resulting output is 1. However, if either or both of the input lines is 0, the result is 0.  
OR gates also have two input lines and produce a 1 if one or both of the input values is a 1. In the case where both input lines are 0, the result is 0.

NOT gates differ from the other two gates in that they only have a single input line. The output value is simply the opposite of the input value. If 0 appears on the input, 1 is produced on the output. Similarly, 1 produces 0.

By combining these gates in various patterns and then applying a set of input values, we can build circuits that have logical functions. In order to implement a circuit, we will first build a representation for logic gates. Logic gates are easily organized into a class inheritance hierarchy. At the top of the hierarchy, the `LogicGate` class represents the most general characteristics of logic gates: namely, a label for the gate and an output line. The next level of subclasses breaks the logic gates into two families, those that have one input line and those that have two.

We can now start to implement the classes by starting with the most general, `LogicGate`. As noted earlier, each gate has a label for identification and a single output line. In addition, we need methods to allow a user of a gate to ask the gate for its label.

The other behavior that every logic gate needs is the ability to know its output value. This will require that the gate perform the appropriate logic based on the current input. In order to produce output, the gate needs to know specifically what that logic is. This means calling a method to perform the logic computation. Here is the complete class:

```js
class LogicGate {
  constructor(n) {
    this.label = n;
    this.output = null;
  }

  getLabel() {
    return this.label;
  }

  getOutput() {
    this.output = this.performGateLogic();
    return this.output;
  }
}
```

At this point, we will not implement the `performGateLogic` function. The reason for this is that we do not know how each gate will perform its own logic operation. Those details will be included by each individual gate that is added to the hierarchy. This is a very powerful idea in object-oriented programming. We are writing a method that will use code that does not exist yet. The parameter `this` is a reference to the actual gate object invoking the method. Any new logic gate that gets added to the hierarchy will simply need to implement the `performGateLogic` function and it will be used at the appropriate time. Once done, the gate can provide its output value. This ability to extend a hierarchy that currently exists and provide the specific functions that the hierarchy needs to use the new class is extremely important for reusing existing code.

We categorized the logic gates based on the number of input lines. The AND gate has two input lines. The OR gate also has two input lines. NOT gates have one input line. The `BinaryGate` class will be a subclass of `LogicGate` and will add two input lines. The `UnaryGate` class will also subclass `LogicGate` but will have only a single input line. In computer circuit design, these lines are sometimes called "pins" so we will use that terminology in our implementation.

```js
class BinaryGate extends LogicGate {
    constructor(n) {
        this.pinA = null;
        this.pinB = null;
    }

    getPinA() {
        return
    }
}
```



