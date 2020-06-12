# DRLND Project 2 Report (Continuous Control)

## Introduction

For this project, I decided to work on solving the version of the Reacher environment with 20 agents. I chose to implement the DDPG algorithm, based on a [previous implementation](https://github.com/MarcioPorto/deep-reinforcement-learning/tree/master/ddpg-pendulum) for the `Pendulum` Gym environment. The decision to use DDPG was based on the fact that it extends the power of the popular DQN algorithm to environments with continuous action spaces, such as this. However, there are many other policy-based algorithms that might work well for solving this kind of environment, including: TRPO, PPO, and A3C.

## Learning Algorithm

[DDPG](https://arxiv.org/pdf/1509.02971.pdf) was introduced as an actor-critic method that performs well in environments with a continuous action space, which is a known limitation of the popular DQN algorithm. It improves on the deterministic policy gradient (DPG) algorithm by using a neural network to take advantage of generalization and function approximation.

The algorithm consists of two different types of neural networks: an actor and a critic. The actor network is used as an approximate for the optimal deterministic policy. As a result, only one action is returned for each state, which is considered to be the best action at that state. The critic, on the other hand, learns how to evaluate the optimal action-value function by using actions from the actor. The main idea of the algorithm is that the actor calculates a new target value that is used to train the action-value function in the critic. 

It's important to clarify that DDPG actually makes use of 4 different neural networks in its implementation: a local actor and a target actor, as well as a local critic and a target critic. Additionally, there are two other important features of the algorithm. The first is that it also uses a replay buffer, just like DQN. The second is that it uses soft updates as the mechanism to update the weights of the target networks. This mechanism replaces the fixed update every C time steps which was used in the original version of DQN, and often leads to better convergence. However, soft updates are not exclusive to DDPG and can also be used in other algorithms such as DQN.

My implementation of the algorithm described above makes use of the following hyperparameters, which are also used in the original DDPG paper:

```
BUFFER_SIZE      # replay buffer size
BATCH_SIZE       # minibatch size
GAMMA            # discount factor
TAU              # for soft update of target parameters
LR_ACTOR         # learning rate of the actor 
LR_CRITIC        # learning rate of the critic
WEIGHT_DECAY     # L2 weight decay
```

As described above, the model architecture for this DDPG consists of two types of networks: an actor and a critic. Their structure in this implementation follows the networks described in the original paper very closely. Each consists of 3 fully-connected layers. The first two layers of each network use the `ReLU` activation function. The output layer for the actor uses a `Tanh` activation, since an action in the Reacher environment consist of a tuple of 4 different numbers between -1 and 1. By using `Tanh`, the actor network outputs a different continuous value between -1 and 1 for each index in the action tuple. This allows DDPG to succeed in environemnts with continuous action spaces. The critic network does not make use of an activation function in the output layer.

## Training and Results

![Plot of Rewards](https://github.com/MarcioPorto/drlnd-continuous-control/blob/master/plot_of_rewards.png)

As shown in the plot above and in the `Continuous_Control.ipynb` notebook, my agent is able to solve the environment after 134 episodes, and eventually settles at an average score near 33 after 250 episodes.

In the training process, I initially tried to closely follow the architecture and hyperparameter values from the original paper. However, after many different trials, I found my optimal configuration to have the following hyperparameters:

```
BUFFER_SIZE = int(1e5)  # (1e6 in original paper)
BATCH_SIZE = 128        # (64 in original paper)
GAMMA = 0.99
TAU = 1e-3 
LR_ACTOR = 1e-4 
LR_CRITIC = 1e-3 
WEIGHT_DECAY = 0        # (1e-2  in original paper)
```

As for the actual structure of the neural network, I found my optimal configuration to have 600 and 450 nodes in the first two layers, respectively. These numbers are different from the 400 and 300 nodes used for those layers, respectivaly, in the original paper.

Lastly, In order to arrive at my final algorithm for the agent, I also had to change the original `OUNoise` class from the one used in the `Pendulum` environment implementation. The old `sample()` method used `random.random()` to generate the noise, but I found it to work much better when sampling from a Gaussian distribution using `np.random.normal()`.

## Future Work Ideas

I would like to have the chance to look at the performance of other algorithms in this environment such as TRPO, PPO and A3C, which have already been mentioned. Additionally, [this paper](https://arxiv.org/pdf/1604.06778.pdf) might serve as an inspiration for other algorithms to try in the future for environments like this. 

It would also be interesting in applying multi-agent learning techniques from the last section of this class to this competitive environment.