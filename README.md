# Road Network Redesign with Linear Programming

## Introduction

Consider the problem "maximizing network connectivity subjected to various feasibility constraints", we apply linear programming as the solution method. In this project, we provide a simple example to demonstrate the viability of this approach, and discuss possible extensions of the algorithms to accommodate more complicated cases.

## Unconstrained Problem 

Consider the example in Brelsford et al. (2018) [1] in which the city of Harare tries to improve the infrastructure access of a slum. We morph the problem into "finding the best place(s) to build/upgrade roads to improve the connectivity between the inner loop (slum,red) and the outer loop (highway,green)". Let the black dotted lines represent road connections that do not currently exist, or in dire need of upgrades. We want to search for the best selection of the dotted lines to maximize some measure of connectivity.

![alt text](https://github.com/johnyangyue/tsp-based-urban-planning/blob/b41bdefcebbc0d6c43812684eb976846bd2a65c7/figs/tsp_sample_init.png)

Given a network of nodes and vertices, suppose we treat the optimization task as a traveling salesman problem. And we measure the performance of a network using the minimum total traveling distance of an agent whose goal is to visit all nodes without repetition and return to the starting node. In an idealistic world where we don’t have any budget or regulatory constraints, information about existing network is redundant. We only need the location of all relevant nodes and the corresponding distance matrix (e.g. measured by Euclidean distances). Since the dimension of our toy example is low, we construct a brute force algorithm that calculate the total travel distance for all possible networks and yield the one with the shortest distance. Then, we can compare the optimal solution to existing network, and simply add/improve the connections and do not yet exist. On the left hand side of the figure below, we have the global best network that corresponds to the shortest total travel distance for an agent who wants to visit all nodes without repetition. On the right hand side, we merge the solution with existing network, and conclude that connection A-H, A-E, B-F, C-G, D-G, D-H should be added on top of the existing network.

![alt text](https://github.com/johnyangyue/tsp-based-urban-planning/blob/4aba539d86f89e4085e0fa27a3c716ad4f7c2c59/figs/tsp_unconstrained.png)

## Constrained Problem

Moving one step closer to a more realistic application, consider the constraint of “n additional roads” or “two nodes cannot be connected due to environmental regulations”. One way to solve the constrained problems is to modify the traveling salesman algorithm to accommodate the constraints. Alternatively, we can manipulate the distance matrix and transform the problems into unconstrained ones. Suppose we can only add/upgrade 2 connections, the steps are as follows:

• For each node pair in the distance matrix, set it as the true distance measure (e.g. Euclidean distance) if the corresponding nodes are currently well-connected (roads that exist and don’t need upgrades). Otherwise (roads that don’t exist or roads that exists but could use some upgrades), assign a extremely high (relative to the true distance measures) value to it.

• For each 2 candidate connections, change their cor- responding values in the distance matrix to the post- construction values.

• Run the traveling salesman algorithm and get the optimal network and the total travel distance.

• Choose the 2 candidate pairs that have the shortest total travel distance as the problem solution.

![alt text](https://github.com/johnyangyue/tsp-based-urban-planning/blob/4aba539d86f89e4085e0fa27a3c716ad4f7c2c59/figs/tsp_constrained.png)

The figure above shows the constrained problem solution in the context of our toy example. If only 2 new connections can be added, the node pairs we should connect that yield the shortest total travel distance are B-F and C-G.

## Possible Extensions

The standard traveling salesman problem does not allow repeated node visits. However, this could be an unrealistic restriction. Removing it could change the total travel distance of a network, and subsequently changes the optimal solution. We can also use alternative measures like k-complexity to evaluate network efficiency.

In addition, while the brute force algorithm can yield the global optimal solution, it is not ideal for high dimensional problems as traveling salesman is known to be an NP-Hard problem. Luckily, we can implement heuristic methods like the Savings algorithm [2] or Sweep algorithm [3] to reduce the computational complexity and obtain solutions that fall within a boundary of the global optimum.

Additional heuristics can be introduced to better constrain proposed road connections and upgrades based on a target budget. In order to decide whether to build or improve existing roads, a target ”monetary” loss function can be included to guide the road proposal and upgrades based on their unit cost with respect to their impact in reducing k-complexity values. That is, given a budget to spend on improvement, the method would prioritize decisions between infrastructure improvement (road upgrades) or new construction of infrastructure (connect nodes that the generative model was not capable of proposing).

## References

[1] Brelsford, Christa Martin, Taylor & Bettencourt, Lu ́ıs. (2017). Optimal reblocking as a practical tool for neighborhood development. Environ- ment and Planning B: Urban Analytics and City Science.

[2] G.ClarkeandJ.R.Wright,“Schedulingofvehicleroutingproblemfrom a central depot to a number of delivery points,” Operations Research, 12, 568-581, 1964.

[3] B. Gillett and L. Miller, “A heuristic algorithm for the vehicle dispatch problem,” Operations Research, 22, 340-349, 1974.



