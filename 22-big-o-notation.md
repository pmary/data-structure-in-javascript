# 2.2 Big-O Notation

When trying to characterize an algorithm’s efficiency in terms of execution time, independent of any particular program or computer, it is important to quantify the number of operations or steps that the algorithm will require. If each of these steps is considered to be a basic unit of computation, then the execution time for an algorithm can be expressed as the number of steps required to solve the problem. Deciding on an appropriate basic unit of computation can be a complicated problem and will depend on how the algorithm is implemented.

A good basic unit of computation for comparing the summation algorithms shown earlier might be to count the number of assignment statements performed to compute the sum. In the function `sumOfN`, the number of assignment statements is 1 \(_theSum=0_\) plus the value of n \(the number of times we perform _theSum = theSum + i_\). We can denote this by a function, call it T, where _T_\(_n_\) = 1 + _n_. The parameter _n_ is often referred to as the "size of the problem", and we can read this as "T\(n\) is the time it takes to solve a problem of size n, namely 1+n steps".

In the summation functions given above, it makes sense to use the number of terms in the summation to denote the size of the problem. We can then say that the sum of the first 100,000 integers is a bigger instance of the summation problem than the sum of the first 1,000. Because of this, it might seem reasonable that the time required to solve the larger case would be greater than for the smaller case. Our goal then is to show how the algorithm’s execution time changes with respect to the size of the problem.



