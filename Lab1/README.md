# Tabular Q-Learning :
In this Lab, we use tabular Q-Learning ([Problem 1](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem1.ipynb)) and "Policy improvement" ([Problem 2](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem2.ipynb)) to solve the Frozen Lake environment from OpenAI.

## Table of contents
- [Introduction](#introduction)
- [Models](#models)
    1. [Q-Learning](#q-learning)

## Introduction

Winter is here. You and your friends were tossing around a frisbee at the park
    when you made a wild throw that left the frisbee out in the middle of the lake.
    The water is mostly frozen, but there are a few holes where the ice has melted.
    If you step into one of those holes, you'll fall into the freezing water.
    At this time, there's an international frisbee shortage, so it's absolutely imperative that
    you navigate across the lake and retrieve the disc.
    However, the ice is slippery, so you won't always move in the direction you intend.
    The surface is described using a grid like the following

        SFFF
        FHFH
        FFFH
        HFFG

    S : starting point, safe
    F : frozen surface, safe
    H : hole, fall to your doom
    G : goal, where the frisbee is located

    The episode ends when you reach the goal or fall in a hole.
    You receive a reward of 1 if you reach the goal, and zero otherwise.
    
    FrozenLake-v0 defines "solving" as getting average reward of 0.78 over 100 consecutive trials.
    
 
## Models
Both models proposed below to solve this environment use the fact that our state space and action space are small enough so we can use tabular implementation of the Dynamic Programming algorithm.
### Q-learning
Tabular Q-learning algorithm uses TD(0) to improve the estimate of the Q-value after each steps. As a reminder, Q-value is solution of the Bellman equation defined below :

![first formula](https://latex.codecogs.com/svg.latex?%5Cinline%20%5Cfn_cm%20%5Clarge%20Q%28s%2Ca%29%20%3D%20R%28s%2Ca%29%20&plus;%20%5Cgamma%5Cmathbb%7BE%7D%5B%5Cunderset%7Ba%27%7D%7B%5Ctextrm%7Bmax%20%7D%7DQ%28s%27%2Ca%27%29%7Cs%2Ca%5D)

