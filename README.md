[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/43851024-320ba930-9aff-11e8-8493-ee547c6af349.gif "Trained Agent"

# Deep Reinforcement Learning Nanodegree Project 2: Continuous Control

## Introduction

![Trained Agent][image1]

The files in this repository implement a DDPQ agent acting in the [Reacher](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#reacher) environment. The basic idea is that the agent controls a double-jointed arm with the goal of moving it to a moving target location.

This implementation works with two versions of this environment:
- The first version contains a single agent. This is considered solved when the agent has an average score of +30 over 100 consecutive episodes.
- The second version contains 20 identical agents, each with its own copy of the environment. This is considered solved when the agents  get an average score of +30 (over 100 consecutive episodes, and over all agents).

The shared mechanics of this environment are as follows:

- *Rewards*: +0.1 for each time step where the agent's hand is in the goal location.
- *State space*: 33 variables (includes position, rotation, velocity, and angular velocities of the arm)
- *Action space*: Vector of 4 numbers, corresponding to torque applicable to two joints. Each value in this vector should be between -1 and 1.

The contents in the `Continuous_Control.ipynb` file solve the second version of this environment.

## Getting Started

1. Clone this repository.

2. Download the environment from one of the links below. You need only select the environment that matches your operating system:
    - **_Version 1: One (1) Agent_**
        - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
        - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
        - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
        - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)

    - **_Version 2: Twenty (20) Agents_**
        - Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
        - Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
        - Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
        - Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)
    
    (_For AWS_) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux_NoVis.zip) (version 1) or [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux_NoVis.zip) (version 2) to obtain the "headless" version of the environment. You will **not** be able to watch the agent without enabling a virtual screen, but you will be able to train the agent. (_To watch the agent, you should follow the instructions to [enable a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md), and then download the environment for the **Linux** operating system above._)

3. Place the downloaded file(s) in the folder you cloned this repo to and unzip (or decompress) the file.

4. Create a Python environment for this project. I recommend using `conda` or `venv`.

5. Activate that environment and install dependencies: 
    ```
    pip install -r requirements.txt
    ```

## Instructions

1. Open the `Continuous_Control.ipynb` notebook and adjust the path to your desired environment file based on its name and where you placed it.

2. You are ready to start interacting with the environment.
    - Use the cells in sections 1, 2 and 3 to initialize and explore the environment
    - Run the cells in section 4 to train the agent. Feel free to change the hyperparameters in `ddpg_agent.py` to see if you can improve training.
    - Run the cells in section 5 to test the agent.