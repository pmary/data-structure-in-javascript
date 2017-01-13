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

> Server side, `performance.now()` is not available. You should use process.hrtime\(\) instead. It returns the current high-resolution real time in a \[seconds, nanoseconds\] tuple Array.

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

Node.JS version

```js
function sumOfN(n) {
   var start = process.hrtime();
   var theSum = 0

   for (var i = 0; i < (n + 1); i++) {
      theSum = theSum + i;
   }

   var end = process.hrtime(start);
   end = end[0] * 1000000 + end[1] / 1000;
   console.log(`Computed in ${end} milliseconds`);
   return theSum;
}

console.log(sumOfN(10));
// Computed in 128.915 milliseconds
```

In the code above you can see that the `sumOfN` function now log the time elapsed between the start and then end of it's execution. If we perform 5 invocations of the function, each computing the sum of the first 10,000 integers, we get the following:

```js
for (let i = 0; i < 5; i++) {
    sumOfN(10000);
}
// Computed in 14.96 milliseconds
// Computed in 14.791 milliseconds
// Computed in 13.868 milliseconds
// Computed in 13.997 milliseconds
// Computed in 14.462 milliseconds
```

We discover that the time is fairly consistent and it takes on average about 14.4156 milliseconds to execute that code. What if we run the function adding the first 100,000 integers?

```js
for (let i = 0; i < 5; i++) {
    sumOfN(100000);
}
// Computed in 152.101 milliseconds
// Computed in 174.257 milliseconds
// Computed in 153.963 milliseconds
// Computed in 158.269 milliseconds
// Computed in 153.325 milliseconds
```

In this case, the average is 158.3829, about 10 times the previous. For `n` equal to 1,000,000 we get:

```js
for (let i = 0; i < 5; i++) {
    sumOfN(100000);
}
// Computed in 1451.723 milliseconds
// Computed in 1487.598 milliseconds
// Computed in 1498.227 milliseconds
// Computed in 1436.73 milliseconds
// Computed in 1459.882 milliseconds
```

This time we found the average is 1466.8319,  again, it's close to 10 times the previous.

Now, consider the code below. It shows a different means of solving the summation problem. This function, takes advantage of a closed equation $$\sum_{i=1}^{n} i = \frac {(n)(n+1)}{2}$$ to compute the sum of the first `n` integers without iterating.

```js
function sumOfN2(n) {
   var start = performance.now();
   
   var result = (n*(n+1))/2;
   
   var end = performance.now();
   
   console.log(`Computed in ${end-start} milliseconds`);
   
   return result;
}

console.log(sumOfN2(10));
```

If we do the same benchmark measurement for `sumOfN2`, using five different values for `n` \(10,000, 100,000, 1,000,000, 10,000,000, and 100,000,000\), we get the following results:

```js
// 10,000 => 0.4638ms
// 100,000 => 0.5874ms
// 1,000,000 => 0.5040ms
// 10,000,000 => 0.5166ms
// 100,000,000 => 0.4958ms
```

There are two important things to notice about this output. First, the times recorded above are shorter than any of the previous examples. Second, they are very consistent no matter what the value of `n`. It appears that sumOfN2 is hardly impacted by the number of integers being added.

But what does this benchmark really tell us? Intuitively, we can see that the iterative solutions seem to be doing more work since some program steps are being repeated. This is likely the reason it is taking longer. Also, the time required for the iterative solution seems to increase as we increase the value of `n`. However, there is a problem. If we ran the same function on a different computer or used a different programming language, we would likely get different results. It could take even longer to perform `sumOfN2` if the computer were older.

We need a better way to characterize these algorithms with respect to execution time. The benchmark technique computes the actual time to execute. It does not really provide us with a useful measurement, because it is dependent on a particular machine, program, time of day, compiler, and programming language. Instead, we would like to have a characterization that is independent of the program or computer being used. This measure would then be useful for judging the algorithm alone and could be used to compare algorithms across implementations.

