# Tabular Q-Learning :
In this Lab, we use tabular Q-Learning ([Problem 1](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem1.ipynb)) and "Policy improvement" ([Problem 2](https://github.com/clement-micol/Reinforcement-Learning/blob/main/Lab1/Lab1_Problem2.ipynb)) to solve the Frozen Lake environment from OpenAI.

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
    
For both algorithms, our Reinforcement Model ended up to solve the game.
