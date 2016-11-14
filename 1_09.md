# 1.9 Getting Started with Data

JavaScript is object-oriented to the core. It means that data is the focal point of the problem-solving process. This is also a prototype-based language and contains no class statement, such as is found in C++ or Java.  

> In JavaScript we don't have to define the type of a variable. This type is deducted from the value stored and may change as the program is running. It is said that JavaScript is a **dynamically** typed language. Other languages like C or Java required the definition of variable types. This is called **static** typing.

## 1.9.1 Built-in Data Types  
According to the latest ECMAScript release, these are the seven data types:  
- String
- Number
- Boolean
- Object
- Symbol (new in ECMAScript 6)
- Null
- Undefined

### 1.9.1.1 Primitive values  
#### String   
A String value is a zero or more Unicode characters. They are useful for holding data that can be represented in text form.  

Some of the most-used operations on strings are to check their **length**, to build and concatenate them using the + and **+= string operators**, checking for the existence or location of substrings with the **indexOf()** method, or extracting substrings with the **substring()** method.  

You include string literals in your scripts by enclosing them in single or double quotation marks:  

```javascript
var myVar = 'Hello';
var otherVar = "World";
```  

They can also be created using the String global object directly:  

```javascript
var myVar = String(42);
console.log(myVar); // "42"
```  

#### Number  
In JavaScript, there is no distinction between integer and floating-point values; a JavaScript number can be either (internally, JavaScript represents all numbers as floating-point values).  
The standard arithmetic operations, +, -, \*, and / can be used with parentheses forcing the order of operations away from normal operator precedence.  
Other very useful operation is the remainder (modulo) operator, %.  

> **Good to know**: The exponentiation operator \*\* is part of the ECMAScript 2016 (ES7), finalized in June 2016. It will eventually be implanted in all browsers but for the moment check the support before you use it.  

```javascript
console.log( 2+3*4 ); // 14
console.log( (2+3)*4 ); //20
console.log( 2**10 ); // 1024
console.log( 6/3 ); // 2
console.log( 7/3 ); // 2.3333333333333335
console.log( 7%3 ); // 1
console.log( 3/6 ); // 0.5
console.log( 3%6 ); // 3
console.log( 2**100 ); // 1.2676506002282294e+30
```

#### Boolean  
Pretty standard across all languages, booleans are `true` and `false`. They're often used for conditional statements.

```javascript
var myBool = new Boolean(false);
var myBool2 = true;
```

Since the variable type is dependent to it's value in JavaScript, the following will not be booleans:
```javascript
var notABoolean1 = "true"; //string
var notABoolean2 = 1; //integer
```

#### Symbol  
This is new in ECMAScript 6, there is no EcmaScript 5 equivalent. A Symbol is a primitive data type whose instances are unique and immutable. In some programming languages they are also called atoms.  
With Reflect, and Proxy, Symbol is one of the three new APIs that allow us to do metaprogramming.

You can find more abour symbols on my blog: [Metaprogramming with ES2016 #1 - Symbol](http://pierremary.com/metaprogramming-with-es2016/)

#### Null  
The value null is what you get when a variable has been defined but has no type or value. We can use it for exemple to assign a default value to a new variable: 

```javascript
var fool = null;
console.log(foo); // null
```

#### Undefined  
This is a very specific type returned when a variable is used without being declare before

Unfedefined is a very specific constant that is returned when a variable is not declared or when it is declared with no value assigned.

```javascript
var foo;
console.log(foo); // undefined

console.log(bar); // throws a ReferenceError
```

### 1.9.1.2 Object  
JavaScript is designed on a simple object-based paradigm. An object is a collection of properties, and a property is an association between a name (or key) and a value. A property's value can be a function, in which case the property is known as a method. In addition to objects that are predefined in the browser, you can define your own objects.