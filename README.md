# tsp-solver

This is Traveling Salesman Problem (TSP) solver based on genetic algorithm.

## Quick theory
TSP is about finding the minimum Hamiltonian cycle in a complete weighted graph. The analogy to the salesman is that the salesman visits all cities (exactly once) and travels the shortest distance possible.The case in which the route from city A to B has the same length as the route from B to A is called the symmetric TSP problem (STSP), thus if we have $n$ cities, then the number of combinations of cities visited $k$ is described as: $\frac{(n-1)!}{2}$. Therefore, for 20 cities we have $\frac{19!}{2}\approx{10^{16}}$ possible combinations. This is a NP-hard optimization problem. In such a case, heuristic solutions are often used, which do not indicate the optimal solution but strive for it.

The genetic algorithm searches the solution space looking for the best route. So we encode the ID of the cities visited as the genotype. As a population, we understand a set of many such cocombinations (genotypes). By generation, in turn, we mean the population in each successive iteration. The algorithm proceeds as follows:
1. randomly initialize the population by drawing consecutively visited cities for different genotypes
2. sort the individuals in the population with respect to the criterion of route length
3. initialize a new population while retaining some of the old population (elitism)
4. draw two individuals from the population (parents) and create two new ones (children) by crossover
5. check the condition and carry out mutation
6. if the required number of generations is not reached, return to step 2

Different types of crossover can be used in the TSP problem. In this case, I decided to use cycle crossover (CX). It involves finding and swapping cycles in two genotypes. This action does not change the order in which the city sequences are visited, which keeps the information. Another way to keep the information in circulation is elitism used in point 3. This involves keeping a certain number of the best individuals for the next generation. This speeds up the algorithm, however, it creates the risk of getting stuck in the local minimum.

Consider the search space as a function of two variables. The graph of such a function can look similar to cartographic maps. There we have " ups" and " downs". To minimize such a function is to find the point with the least exposure. However, optimization algorithms often find a depression and assume that it is the global minimum. In genetic algorithms to prevent this a mutation mechanism is used. Its purpose is to introduce diversity into the genotype and, in a sense, to take it slightly out of balance. We can associate this action with the Dropout function in neural networks (although the two mechanisms work quite differently).

In my experiments, I used the datasets available [hear](https://www.math.uwaterloo.ca/tsp/vlsi).

## Resoults
<img src="https://github.com/Tymass/tsp-solver/assets/83314524/eac42cb8-f7dd-4c49-bd5e-49d6e378f893" width="100%" height="100%"><img src="https://github.com/Tymass/tsp-solver/assets/83314524/ddfd998c-4f7b-4c78-aaec-780708bbfae2" width="100%" height="100%">

A comparison of the result of the experiment and the optimal route shows that the algorithm is doing quite well. The error in this experiment was about 5%. The results for larger sets are similar, but the algorithm takes much longer to find the optimum. For 343 points it is already several hours.
