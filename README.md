# PD-World

### Introduction
Reinforcement learning (RL) is a component of machine learning which concentrates on teaching agents to make judgments on the basis of a reward signal. Q-learning is a prominent reinforcement learning technique which stores the predicted reward for each state-action combination in a Q-table. Q-learning is an off-policy learning algorithm that uses the ‘optimal approach’ behavior i.e. the greedy approach. The greedy approach is one that gives the maximum Q-value for the state - it directly learns the optimal policy. In contrast, SARSA follows the action of the current policy and updates its q-values according to this rule. Unlike the greedy approach of Q-learning, SARSA learns the ‘near’ optimal policy, making it a more conservative approach. Q-learning appears impracticable for applications with large state spaces since the Q-table expands exponentially with the number of states. That is, as the number of states increases, the size of the Q-table storing the Q-values for each state-action pair multiplies exponentially. On the other hand, with SARSA, the Q-table storing the Q-values is expanded proportionally (linear growth) with the number of actions currently accessible in each state. This is then added to the Q-value of the current state-action pair. We will compare the findings of running both these reinforcement learning techniques further in this report. The major difference is the way these two approaches update their Q-values.

This report outlines the design and implementation of a reinforcement learning framework for solving a 3 dimensional grid world problem. The objective of the system is to direct a robot agent from the beginning point to a destination position in a grid world while avoiding obstacles. Furthermore, the system is built utilizing modular software development techniques and implemented via python.

### Constraints 
This project consists of two agents - one male (M), and one female (F). The goal is to find a path by moving the male and female agents together, in such a way that the final path created is free of any blockages whilst keeping the two agents separated at all times - both agents cannot be in the same position at the same time. In this project both agents will be working on the same path at the same time creating one final ‘attractive path’. The agents can only move in the following six directions - left, right, up, down, forward and backward.

### Q-table design 
The Q-table is a structure holding the predicted rewards for each action in every state. The Q-table implemented includes four states (normal, risky, pickup and dropoff) and six potential actions (up, down, left, right, forward, backward). To store the q-values for each cell, our approach employs a hashmap within a hashmap; in which the outer hashmap’s key denotes the cell’s classification, and the inner hashmap contains the q-value for each neighboring block in every direction. Each entry in the Q-table indicates the probable reward for a certain action in a specific condition. The Q-table is initialized with values that are randomly generated and is updated via the agent's interactions with the environment utilizing the Q-learning process. Essentially, the Q-learning algorithm adjusts the Q-table by calculating the projected reward of every action in a given state based on the environment's rewards and the expected rewards in the following state.

### Single Q-Table Approach
A joint action learning involves a single Q-table for both male and female agents, which is modified based on the joint operations performed by both agents. In this strategy, we first choose an operator for each agent, and then we conduct the chosen two operators; due to joint actions, this leads to better coordination (taking into consideration the influence of each agent's decisions on the joint reward) and potentially enhanced performance. A joint Q-table can also minimize the number of state-action combinations that must be learnt because the same Q-values can be utilized for actions involving both agents. The disadvantage is limited flexibility since both agents are managed by a single Q-Table, the learning process may be constrained in respect to its ability to adjust to modifications in the environment or the behavior of the other agent. Issues can arise if one agent’s action has a possible negative impact on the other agent’s reward, the agents may obstruct each other. 
