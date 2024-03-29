---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 8
---

### Weighted Graphs

### Minimum Spanning Trees

We can get the MSTs using algorithms like Prim's Algorithm and Krushkal's Algorithm.  I am going to talk about some of the extensions of this problem. Here are some of the interesting ones:
* _Maximum spanning trees_ - The maximum spanning tree of any graph can be found by simply negating the weights of all edges and running Prim’s or Kruskal’s algorithm. The most negative spanning tree in the negated graph is the maximum spanning tree in the original.
* _Minimum product spanning trees_ – Suppose we seek the spanning tree that minimizes the product of edge weights, assuming all edge weights are positive. Since lg(a · b) = lg(a) + lg(b), the minimum spanning tree on a graph whose edge weights are replaced with their logarithms gives the minimum product spanning tree on the original graph.
* _Minimum bottleneck spanning tree_ – Sometimes we seek a spanning tree that minimizes the maximum edge weight over all possible trees. In fact, every minimum spanning tree has this property. The proof follows directly from the correctness of Kruskal’s algorithm.
Such bottleneck spanning trees have interesting applications when the edge weights are interpreted as costs, capacities, or strengths. A less efficient but conceptually simpler way to solve such problems might be to delete all “heavy” edges from the graph and ask whether the result is still connected. These kinds of tests can be done with BFS or DFS.


### Shortest Path

_Guru Mantra_ : **Try to design graphs, not algorithms**
Context - Suppose we are given a directed graph whose weights are on the vertices instead of the edges. Thus, the cost of a path from x to y is the sum of the weights of all vertices on the path. Give an efficient algorithm for finding shortest paths on vertex-weighted graphs.
Solution: There are two approaches here:
* Adapt the algorithm we have for edge-weighted graphs (Dijkstra’s) to the new vertex-weighted domain. It should be clear that this will work. We replace any reference to the weight of any directed edge (x, y) with the weight of the destination vertex y. This can be looked up as needed from an array of vertex weights.
* Other way to keep the algorithm intact and instead concentrate on constructing an edge-weighted graph on which Dijkstra’s algorithm will give the desired answer. Set the weight of each directed edge (i, j) in the input graph to the cost of vertex j. Dijkstra’s algorithm now does the job.

