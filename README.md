# Road Network Redesign with Linear Programming

## Introduction

Consider the problem "maximizing network connectivity subjected to various feasibility constraints", we apply linear programming as the solution
method. In this project, we provide a simple example to demonstrate the viability of this approach, and discuss possible extensions of the algorithms to accommodate more complicated cases.

## Unconstrained Problem 

Consider the example in Brelsford et al. (2018) [1] in which the city of Harare tries to improve the infrastructure access of a slum. We morph the problem into “finding the best place(s) to build/upgrade roads to improve the connectivity between the inner loop (slum,red) and the outer loop (highway,green), illustrated in Fig. 2. Let the black dotted lines represent road connections that do not currently exist, or in dire need of upgrades. We want to search for the best selection of the dotted lines to maximize some measure of connectivity.

![alt text](https://github.com/johnyangyue/tsp-based-urban-planning/blob/figs/tsp_sample_init.jpg?raw=true)
