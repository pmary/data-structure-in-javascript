#Arrays

 Let's start with the most common data structure: The array.
Event if you didn’t study computer science in school, you should be familiar with it.
Arrays are among the oldest and most important data structures. They are used by almost every program and built-in in every programming language, which makes them usually very efficient. As we will see later, they are also used to implement many other data structures, such as lists and strings.
In this chapter we explore how it work in JavaScript and when to use them.

##Arrays in JavaScript
 An array consist of a collection of elements (values or variables), each identified by an array index or key. In other words, its a linear list-like object.

 If you are more familiar with Java, C++ or C#, JavaScript can seem to be a strange language. For example, every object is an associative array. In fact, the associative array is the fundamental data structure in JavaScript. This is so powerful it can be used to implement object or just about any other data structure. When JavaScript was first released it didn't have a dedicated Array data structure. Why? Because it didn't need one (and in many ways it still doesn't). But to make JavaScript easier to use from the perspective of another language it does have an Array object. Here is why looking at the Array object can be confusing. Try to not forget that every data structure in JavaScript is an object. Or more accurately, an associative array.
Because they are objects, they are not as efficient as in other programming languages.

##Using Arrays
 The array object prototype has methods to perform traversal and mutation operations.

##Create an array
 The easiest and most efficient way to create an array is to assign the [ ] operator to a variable:

```javascript
var fruits = [];
```

This give you an Array instance inheriting from `Array.prototype`. This new array is empty, we can verify it by calling the length property:  

```javascript
console.log(fruits.length);
> 0
```

But we can also create a non-empty array by declaring our variables inside the [ ] operator: 

```javascript
var fruits = ['banana', 'cherry', 'strawberry'];
console.log(fruits.length);
> 3
```

Note that in JavaScript, array elements can be of different type: 

```javascript
var myArray = ['whale', 42, null, false];
```

You can also use the Array constructor with the same logic: 

```javascript
var fruits = new Array();
console.log(fruits.length);
> 0

var fruits = new Array('banana', 'cherry', 'strawberry');
console.log(fruits.length);
> 3
```
But I suggest you to not use this approach, especially since it doesn’t work properly if there is a single value that is a number:

```javascript
new Array(4);
> [undefined × 4]
```



### ES6 - New methods to create an Array instance
#### Array.from()  
 
 In ES6, you can now create a new Array instance from an array-like or iterable object by using the `Array.from()` method.  
For example, to create an array from a string:

```javascript
var fruits = Array.from("banana"); 
console.log(fruits);
> ["b", "a", "n", "a", "n", "a"]
```

#### Array.of()  

 With this method, you can create an array of elements, regardless of their number or type.
 
```javascript
var fruits = Array.of('banana', 'cherry', 'strawberry', 42);
console.log(fruits);
> ["banana", "cherry", "strawberry", 42]
```

## Operations on array elements

You can access to an array element using the [ ] operator by its index:

```javascript
var fruits = ['banana', 'cherry', 'strawberry'];
console.log( fruits[1] );
> cherry
```

You can also access sequentially to all the elements by using the `for` loop:

```javascript
var fruits = ['banana', 'cherry', 'strawberry'];
for (var i = 0; i < fruits.length; ++i) {
  console.log( fruits[i], i );
}
> banana 0
> cherry 1
> strawberry 2
```

You can use as well the `forEach` method: 

```javascript
var fruits = ['banana', 'cherry', 'strawberry'];
fruits.forEach(function (item, index, array) {
  console.log(item, index);
});
> banana 0
> cherry 1
> strawberry 2
```

An important difference between the `for` loop and the `forEach` method is that, with the former, you may break out of the loop, using the `break` statement.

```javascript
var fruits = ['banana', 'cherry', 'strawberry'];
for (var i = 0; i < fruits.length; ++i) {
  console.log( fruits[i], i )
  if (fruits[i] === 'cherry' ) {
    // Stop the loop execution
    break;
  }
}
> banana 0
> cherry 1
```

_If you try to use a `break` within a `forEach` loop, you will get the following error `Uncaught SyntaxError: Illegal break statement`._

Furthermore, the `forEach` method is much more expressive, about 95% slower, than the `for` statement. You can check it yourself right here: [www.jsperf.com/fast-array-foreach](http://jsperf.com/fast-array-foreach).

