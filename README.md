# Road Network Redesign with Linear Programming

## Introduction

Consider the problem "maximizing network connectivity subjected to various feasibility constraints", we apply linear programming as the solution
method. In this project, we provide a simple example to demonstrate the viability of this approach, and discuss possible extensions of the algorithms to accommodate more complicated cases.

## Unconstrained Problem 

Consider the example in Brelsford et al. (2018) [1] in which the city of Harare tries to improve the infrastructure access of a slum. We morph the problem into "finding the best place(s) to build/upgrade roads to improve the connectivity between the inner loop (slum,red) and the outer loop (highway,green)". Let the black dotted lines represent road connections that do not currently exist, or in dire need of upgrades. We want to search for the best selection of the dotted lines to maximize some measure of connectivity.

![alt text](https://github.com/johnyangyue/tsp-based-urban-planning/blob/b41bdefcebbc0d6c43812684eb976846bd2a65c7/figs/tsp_sample_init.png)

Given a network of nodes and vertices, suppose we treat the optimization task as a traveling salesman problem. And we measure the performance of a network using the minimum total traveling distance of an agent whose goal is to visit all nodes without repetition and return to the starting node. In an idealistic world where we don’t have any budget or regulatory constraints, information about existing network is redundant. We only need the location of all relevant nodes and the corresponding distance matrix (e.g. measured by Euclidean distances). Since the dimension of our toy example is low, we construct a brute force algorithm that calculate the total travel distance for all possible networks and yield the one with the shortest distance. Then, we can compare the optimal solution to existing network, and simply add/improve the connections and do not yet exist. On the left hand side of Fig. 3, we have the global best network that corresponds to the shortest total travel distance for an agent who wants to visit all nodes without repetition. On the right hand side, we merge the solution with existing network, and conclude that connection A-H, A-E, B-F, C-G, D-G, D-H should be added on top of the existing network.
