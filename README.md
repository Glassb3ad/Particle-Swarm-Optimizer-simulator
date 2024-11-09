﻿# Particle Swarm Optimizer simulator

This repository includes:

1. Particle Swarm Optimizer (PSO) for resoslving optimization problems that seek to find global minimum. This PSO implementation can optimize problems with n-dimensional search space so its not restricted to 1 or 2 dimensions.
2. Visualization tools for making simulation videos showing how PSO solves optimization problems with 1,2 or 3 dimensional search space.

## General

PSO is a method for solving various optimization problems. An optimization problem involves finding the best possible solution for a given task. Typically, we treat tasks as functions and define the best solution as the input that the function maps to the desired output. In this case, we seek to find the input for which the function produces the smallest output. This is referred to as the global minimum.

The set of possible solutions is called the search space, and it is often bound but not finite. For example, the search space might consist of real numbers in the range from 0 to 1. Solving the optimization task for function F is to find 𝑥 from the search space such that there is no 𝑦 in the search space for which F(x)>F(y).

PSO is a nature-inspired algorithm that mimics birds' flocking behavior. The basic idea is to create a swarm of particles that move through the search space according to simple rules, and eventually, the population organizes itself around the optimal solution. Thus, PSO is a form of self-organization. The swarm's ability to find the optimal solution can be seen as an emergent property since no individual in the swarm has this ability on its own.

Each particle in the swarm represents an input to the function. It remembers its best position, and its movement is influenced by its personal best position, the global best position (i.e., the best position any particle has visited), and by random disturbances. The use of randomness is what makes PSO a stochastic algorithm. The value or fitness of position p is F(p), where F is the objective function. The particles move for a given number of iterations, after which the global best is hopefully a good enough, if not the best, solution

## Does PSO show intelligent behavior?

## PSO implementation

The implementation rests heavily on Particle class that provides all methods for controlling particle's state. The other heavy lifter is particleSwarmOptimization() function which both updates swarm's state and records its history in order to visualize how swarm searches for solution.

### particleSwarmOptimization()

1. initialize swarm with generateInitialSwarm()
2. calculate initial global best
3. record initial swarm state
4. While iteration limit is not reached:
   1. for each particle P in swarm:
      1. update velocity
      2. move particle in search space
      3. update personal best
   2. update global best
   3. record swarm state
5. return history and global best

particleSwarmOptimization() accepts inertia, cognitive and social parameters. They are hyperparameters used in the most central operation of algorithm: velocity update

### Particle class

The most central method in Particle class is updateVelocity() which does what it says. The equation for calculating new velocity is a sum of three parts: inertia, cognitive and social part.

1. Intertia
2. congnitive
3. social

## Demonstrations

The following PSO demonstrations have constant inertia and cognitive and social coefficients. Only swarm sizes and iteration counts vary. All videos generated with tools implemented in this repository.

### 1d schwefel function

A relatively small swarm quickly converges near the optimal solution.

https://github.com/user-attachments/assets/517655ba-0ab4-4749-a2ee-b1a474cc5967

### 2d schwefel function

When searching optimal solution for 2d schwefel function, small swarm has a high risk to get stuck in local minima (global minima marked by blue star):

https://github.com/user-attachments/assets/0f38689a-576e-40b7-8201-f55a10e1e062

But larger swarm almost certainly finds the global minimum from the search space. In the following swarm begins swarming around a local minimum but then some particles doing global search start registering better solution and eventually swarm moves towards the global minimum.

https://github.com/user-attachments/assets/5c596fce-c57c-4cd6-8a93-4d8a81eda4eb

### Banana function

With banana function (also known as Rosenbrock function) the swarm quickly locates the global minimum but it takes many iterations until particles stop doing global searches and swarm stabilizes around the optimal solution

https://github.com/user-attachments/assets/55229e3b-0f76-4d15-b6b3-18eb99d9d8e8

### 3d schwefel function

PSO works well in 3d search space. At first swarm is stuck in local minimum but in the end the global minimum is found

https://github.com/user-attachments/assets/408262bb-af77-4032-b91c-90d7245ce0ee

## Development

run tests: python -m unittest discover tests

tests might take some time due to using PSO with big swarms and high iteration count.
