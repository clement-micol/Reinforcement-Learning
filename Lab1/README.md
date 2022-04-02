# Tabular Q-Learning :
In this Lab, we use tabular Q-Learning ([Problem 1](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem1.ipynb)) and "Policy improvement" ([Problem 2](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem2.ipynb)) to solve the Frozen Lake environment from OpenAI.

## Table of contents
- [Introduction](#introduction)
- [Models](#models)
    1. [Q-Learning](#q-learning)
    2. [Policy Improvement](#policy-improvement)
- [Performace](#performance)

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
<p align="center">
    
<img src="https://render.githubusercontent.com/render/math?math={Q(s,a) = R(s,a) %2b \mathbb{E}[\underset{a'}{\textrm{max }} Q(s',a') |s,a]}#gh-light-mode-only">
<img src="https://render.githubusercontent.com/render/math?math={\color{white}Q(s,a) = R(s,a) %2b \mathbb{E}[\underset{a'}{\textrm{max }} Q(s',a') |s,a]}#gh-dark-mode-only">
    
</p>
<div style='vertical-align:middle; display:inline;'>
Therefore at each iteration, we are going to compute a target <img src="https://render.githubusercontent.com/render/math?math={z_t}#gh-light-mode-only"/>
<img src="https://render.githubusercontent.com/render/math?math={\color{white}z_t}#gh-dark-mode-only"/> such that <img src="https://render.githubusercontent.com/render/math?math={Q(s_t,a_t) \approx z_t}#gh-light-mode-only"/>
<img src="https://render.githubusercontent.com/render/math?math={\color{white}Q(s_t,a_t) \approx z_t}#gh-dark-mode-only"/>. The desired target is the result of TD-Learning :</div>

<br>
<p align="center">
    <img src="https://render.githubusercontent.com/render/math?math={z_t = r_t  %2b \underset{a}{\textrm{max}}Q(s_{t+1},a)-Q(s_t,a_t)}#gh-light-mode-only"/>
    <img src="https://render.githubusercontent.com/render/math?math={\color{white}z_t = r_t  %2b \underset{a}{\textrm{max}}Q(s_{t+1},a)-Q(s_t,a_t)}#gh-dark-mode-only"/>
 </p>
 
 Therefore at each time steps, we improve our estimation of the Q-value by computing:
 <br>
 <p align="center">
    <img src="https://render.githubusercontent.com/render/math?math={Q_t(s_t,a_t) = Q_t(s_t,a_t) %2b \alpha z_t}#gh-light-mode-only"/>
    <img src="https://render.githubusercontent.com/render/math?math={\color{white}Q_t(s_t,a_t) = Q_t(s_t,a_t) %2b \alpha z_t}#gh-dark-mode-only"/>
 </p>
 <div style='vertical-align:middle; display:inline;'>
 The action <img src="https://render.githubusercontent.com/render/math?math={a_t}#gh-light-mode-only"/> <img src="https://render.githubusercontent.com/render/math?math={\color{white}a_t}#gh-dark-mode-only"/> is taken according to the <img src="https://render.githubusercontent.com/render/math?math={\epsilon}#gh-light-mode-only"/> <img src="https://render.githubusercontent.com/render/math?math={\color{white}\epsilon}#gh-dark-mode-only"/>-greedy policy. In our case, <img src="https://render.githubusercontent.com/render/math?math={\epsilon}#gh-light-mode-only"/> <img src="https://render.githubusercontent.com/render/math?math={\color{white}\epsilon}#gh-dark-mode-only"/> is decreasing linearly with the number of episodes ran.</div>
 
 ### Policy Improvement
 Policy improvement has a weird implementation. Supposedly, we should run TD learning to compute the Q-value of the current policy and take the argmax of the Q-value to upgrade our new policy. But from the tests I ran, this algorithm doesn't work at all for this environment (and may be for all environment). Instead, I decided to update the policy every 100 steps according to the computed Q-value. Also, I don't reset my Q-value at each iteration of policy improvement. In other terms, we have the following algorithms :
 ```code
 init pi, gamma, lr, Q
 for k in 1,...,N:
    for episode in 1,...,num_episodes:
        for t in 1,...,max_iter:
            a_t = pi[s_t]
            s', r_t, d = take action a_t
            z_t = r_t + gamma*max(Q(s',a)) - Q(s_t,a_t)
            Q(s_t,a_t) += lr*z_t
        update pi every tau episode :
            pi[s] = argmax Q(s,a)
 ```
 ## Performance
 We show below the performance of our model :
 
 |Q-Learning | Policy Improvement|
 |:----------:|:---------------------:|
 |<img src = https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/figs/Training-Moving-Avg-Rwd-Q.svg width=450> | <img src=https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/figs/Training-Moving-Avg-Rwd-PI.svg width=450> |
 |<img src = https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/figs/Evaluation-Moving-Avg-Rwd-Q.svg width=450> | <img src=https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/figs/Evaluation-Moving-Avg-Rwd-PI.svg width=450> |
    
