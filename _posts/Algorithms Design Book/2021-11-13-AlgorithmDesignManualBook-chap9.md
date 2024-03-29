---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 9
---

### Combinatorial Search

Recursion has been taught to us as part of the early lessons in programming. We know that it can be used to solve many problems but it has a lot of computational cost. To save cycles, we have techniques which can be used for removing some unnecessary paths. I was aware of techniques like pruning. But I have learnt many others from this book. Here are some of the cool ones:

### Backtracking
Run through all of the search space and Wham!! you get the answer.

### Best-First Search
This has been a useful technique that I've learned recently. By common sense, to speed up search it is better to explore your best options before the less promising choices. An excerpt from the book:

_Best-first search, also called branch and bound, assigns a cost to every partial solution we have generated. We use a priority queue to keep track of these partial solutions by cost, so the most promising partial solution can be easily identified and expanded. As in backtracking, we explore the next partial solution by testing if it is a solution and calling process solution if it is. We identify all ways to expand this partial solution by calling construct candidates, each of which gets inserted into the priority queue with its associated cost._

More Info [here](https://www.geeksforgeeks.org/best-first-search-informed-search/).

### The A* Heuristic
This heuristic is an extension of best-first search. Instead of only comparing the partial costs, we try to estimated the total costs using some smart guesses. Here our cost function is _f(n)_ which is calculated as follow:
$$
f(n) = g(n) + h(n)
$$
Here, _h(n)_  = the estimated movement cost from here to target and,
_g(n)_ = cost to move from the starting point to this point

An excerpt from the book:

_The idea is to use a lower bound on the cost of all possible partial solution extensions that is stronger than just the cost of the current partial tour. This will make promising partial solutions look more interesting than those that have the fewest vertices._

More Info [here](https://www.geeksforgeeks.org/a-search-algorithm/).

### Reverse Search
I have learnt about this trick while going through this [problem](https://onlinejudge.org/external/7/704.pdf)

Suppose we have to recurse for several steps(~n). It may be the case that about n/2 steps can be done in a feasible time as there are less cases to deal with. What we can do is backtrack from the target and create a tree of about n/2 depth. Similarly we can create a tree from src of about n/2 depth. Then we can find the shortest path from src to target by comparing the entries created in both trees.


it can be represented as something like this:


                    src
                    /  \
                   /    \
                  /      \
            some common entries which were reachable in both
                  \      /
                   \    /
                    \  /
                    target
