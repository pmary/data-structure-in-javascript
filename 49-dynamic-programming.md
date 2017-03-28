# 4.9 Dynamic Programming

The dynamic programming \(or dynamic optimization\) is a method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions. The next time the same subproblem occurs, instead of recomputing its solution, one simply looks up the previously computed solution, thereby saving computation time at the expense of a \(hopefully\) modest expenditure in storage space.

This kind of algorithms are often used for optimization. A dynamic programming algorithm will examine the previously solved subproblems and will combine their solutions to give the best solution for the given problem. In comparison, a greedy algorithm treats the solution as some sequence of steps and picks the locally optimal choice at each step. Using a greedy algorithm does not guarantee an optimal solution, because picking locally optimal choices may result in a bad global solution, but it is often faster to calculate. Note that some greedy algorithms \(such as Kruskal's or Prim's for minimum spanning trees\) are proven to lead to the optimal solution.

