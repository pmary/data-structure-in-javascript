# 2.1 What is Algorithm Analysis

If you ask two developers to solve the same problem you will certainly end with two differents programs. This raise an interesting question. How do you know which one is better than the other?

In order to answer this question, we need to remember that there is an important difference between a program and the underlying algorithm that the program is representing. As we stated in Chapter 1, an algorithm is a generic, step-by-step list of instructions for solving any instance of a problem. A program, on the other hand, is an algorithm that has been encoded into some programming language. There may be many programs for the same algorithm, depending on the programmer and the programming language being used.

To explore this difference further, consider the function shown below. This function solves a familiar problem, computing the sum of the first n integers. The algorithm uses the idea of an accumulator variable that is initialized to 0. The solution then iterates through the n integers, adding each to the accumulator.

```js
function sumOfN(n) {
   var theSum = 0
   for (var i = 0; i < (n + 1); i++) {
      theSum = theSum + i;
   }

   return theSum;
}

console.log(sumOfN(10));
```

Now look at the function below. At first glance it may look strange, but upon further inspection you can see that this function is essentially doing the same thing as the previous one. The reason this is not obvious is poor coding. We did not use good identifier names to assist with readability, and we used an extra assignment statement during the accumulation step that was not really necessary.

```js
function foo(tom) {
    var fred = 0;
    for (var bill = 0; bill < (tom + 1); bill++) {
       var barney = bill;
       fred = fred + barney;
    }
    
    return fred;
}

console.log(foo(10));
```

The question we raised earlier asked whether one function is better than another. The answer depends on your criteria. The function `sumOfN` is certainly better than the function `foo` if you are concerned with readability. In fact, you have probably seen many examples of this in your introductory programming course since one of the goals there is to help you write programs that are easy to read and easy to understand. In this course, however, we are also interested in characterizing the algorithm itself. \(We certainly hope that you will continue to strive to write readable, understandable code\).

Algorithm analysis is concerned with comparing algorithms based upon the amount of computing resources that each algorithm uses. We want to be able to consider two algorithms and say that one is better than the other because it is more efficient in its use of those resources or perhaps because it simply uses fewer. From this perspective, the two functions above seem very similar. They both use essentially the same algorithm to solve the summation problem.

At this point, it is important to think more about what we really mean by computing resources. There are two different ways to look at this. One way is to consider the amount of space or memory an algorithm requires to solve the problem. The amount of space required by a problem solution is typically dictated by the problem instance itself. Every so often, however, there are algorithms that have very specific space requirements, and in those cases we will be very careful to explain the variations.

As an alternative to space requirements, we can analyze and compare algorithms based on the amount of time they require to execute. This measure is sometimes referred to as the "execution time" or "running time" of the algorithm. One way we can measure the execution time for the function Á is to do a benchmark analysis. This means that we will track the actual time required for the program to compute its result. In JavaScript, we can benchmark a function by noting the starting time and ending time with respect to the system we are using. We can use the `performance.now()` method to returns a DOMHighResTimeStamp, measured in milliseconds, accurate to one thousandth of a millisecond. By calling this function twice, at the beginning and at the end, and then computing the difference, we can get an exact number of seconds \(fractions in most cases\) for execution.

```js
function sumOfN(n) {
   var start = performance.now();
   var theSum = 0
   
   for (var i = 0; i < (n + 1); i++) {
      theSum = theSum + i;
   }
   
   var end = performance.now();
   console.log(`Computed in ${end-start} milliseconds`);
   return theSum;
}

console.log(sumOfN(10));
// Computed in 0.05500000016763806 milliseconds
```

In the code above you can see that the `sumOfN` function now log the time elapsed between the start and then end of it's execution. If we perform 5 invocations of the function, each computing the sum of the first 10,000 integers, we get the following:

```js
for (let i = 0; i < 5; i++) {
    sumOfN(10000);
}
// Computed in 0.05499999993480742 milliseconds
// Computed in 0.0849999999627471 milliseconds
// Computed in 0.05499999993480742 milliseconds
// Computed in 0.08500000019557774 milliseconds
// Computed in 0.01500000013038516 milliseconds
```



