# Wolpertinger Agents, written in tinygrad

They're fast! They're snazzy! They're Wolpertinger Agents, written in tinygrad!

# Quickstart
tinygrad version of Wolpertinger Training with DDPG (paper: Deep Reinforcement Learning in Large Discrete Action Spaces).
It is compatible with both continuous and discrete control of OpenAI gym.
In continuous case, I discretize the action space to use the wolpertinger-DDPG training algorithm.

# Usage

* In Pendulum-v0 (continuous control), discretize the continuous action space to a discrete action spaces with 200000 actions.
```python main.py --env 'Pendulum-v0' --max-actions 200000```
* In CartPole-v1 (discrete control), --max-actions is not needed.
```python main.py --env 'CartPole-v1'```

(Huge shoutout to [ChangyWen](https://github.com/ChangyWen) for his [implementation of this in PyTorch](https://github.com/ChangyWen/wolpertinger_ddpg/tree/master))

# What are Wolpertinger Agents?

Wolpertinger Agents are an approach to handling reinforcement learning problems with large discrete action spaces. Here's an explanation geared towards software engineers:

## Key Concepts

Wolpertinger Agents address two main challenges:

1. Generalizing over large action spaces
2. Achieving sub-linear time complexity relative to the number of actions

The approach combines elements of actor-critic methods with approximate nearest neighbor search to efficiently handle problems with up to millions of discrete actions.

## Architecture

The Wolpertinger architecture consists of two main components:

1. **Action Generation**
   - An actor network (fθπ) that produces a "proto-action" in continuous space
   - An approximate nearest neighbor search to find k closest discrete actions

2. **Action Refinement**
   - A critic network (QθQ) that evaluates the Q-values of the k selected actions
   - Selection of the highest-valued action among the k candidates

## Key Features

- **Continuous Embedding**: Actions are embedded in a continuous space, allowing for generalization[1].
- **Logarithmic-time Lookup**: Approximate nearest neighbor search enables efficient action selection[1].
- **Policy Gradient Training**: The architecture is trained using Deep Deterministic Policy Gradient (DDPG)[1].

## Algorithm Overview

1. The actor network produces a proto-action in continuous space.
2. K-nearest neighbor search finds the k closest discrete actions.
3. The critic network evaluates these k actions.
4. The highest-valued action is selected and applied to the environment.

## Advantages

- Scales to very large action spaces (demonstrated on tasks with up to one million actions)[1].
- Combines the generalization capabilities of value-based methods with the efficiency of actor-based approaches[1].
- Allows for a trade-off between policy quality and execution speed by adjusting the k parameter[1].

## Implementation Considerations

- Requires a meaningful embedding of discrete actions in continuous space.
- Performance depends on the quality of the approximate nearest neighbor search.
- The choice of k affects the balance between computation time and policy quality.

Wolpertinger Agents provide a novel approach to handling large discrete action spaces in reinforcement learning, making it possible to apply RL techniques to previously intractable problems in areas like recommender systems, industrial control, and language models[1].


