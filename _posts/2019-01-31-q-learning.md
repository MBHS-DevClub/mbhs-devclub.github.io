---
layout: post
title: Q-Learning
tags: [rl]
excerpt_separator: <!--more-->
---

## Background

Last time, we learned about the concepts behind reinforcement learning. This week, we will review the ideas and implement an example.

### Concept Review

The key ideas from last time are agents and environments. In each step, an **agent** takes **actions** that affect the **environment**. Then, the environment gives **rewards** to the agent and provides snapshots in the form of **states**.

![](https://i.imgur.com/48O2aJQ.png)

Reinforcement learning (RL) just refers goal-oriented algorithms that **learn** how to achieve attain some goal over many steps.

### Policy and Q

This week, we need to introduce two new pieces of vocabulary.

A **policy** is the strategy that the agent employs to determine the next action based on the current state. It maps *states* to *actions*, the actions that promise the highest reward.

**Q-value** refers to the long-term return of taking an action in a state. The Q-values are staored in a **Q-table**, where the rows are states and columns are potential actions. **Q** is much like policy, except that it maps *action-state pairs* to *rewards*.

> Let's use the example of chess. A policy could be an opening book that showed the best move in a common board position. The book maps from states (boards) to actions (piece moves). Meanwhile, suppose we decided instead to assign values to the pieces and rate each move by how well it improves the player's material. This would be Q, as it is a way to assign value to a action in a given state.

We calculate Q with the Bellman equation. It represents the sum of both the immediate and future rewards for a given state and action pair.

![](https://i.imgur.com/VsP7imb.png)

> The discount factor (γ) is just a way to change how much weight we give to future value. This allows us to perform sums of infinite future steps and give greater weight to immediate awards.

How do we update values of Q?

### Q-Learning

Most well-known uses of RL like AlphaGo are instances of *deep* reinforcement learning. A neural network is trained to estimate the Q-values of a given state and action.

Today, we're going implement *simple* reinforcement learning using a algorithm called **Q-learning**. This algorithm seeks to fill in the Q-table by repeatedly iterating over all state-action pairs and updating the Q-values.

![](https://i.imgur.com/W1VClRb.png)

#### Step 1. Initialize Q-Table

Create a the Q-table, a table of state-action pairs, and intiialize all of the cells. For example, we can set all of hte original Q-values to 0.

#### Step 2. Choose and Perform an Action

We now need to take steps to train our model. We only stop taking actions when we are done training.

One issue we want to recall from last time is the tradeoff between **Exploration** and **Exploitation**. We want our agent to exploit the environment and recieve lots of rewards, but we also want the agent to explore the environment for rewards yet to be discovered. 

> Recall the example of the cat and mouse grid world. If the mouse only tried to exploit, it would eat all of the small cheese and recieve +1 reward. But, if it explored more, it could discover the big cheese, and recieve +50 reward, which is better.

![](https://i.imgur.com/0rgLAW0.png)

One way we can resolve this is with the **epsilon greedy strategy**. Let's define a variable called epsilon (ε). You can think of it as uncertainty. In the beginning, the value of epsilon is high, so the agent will randomly explore the environment. 

As the agent explores more, epsilon decreases. It will become more confident in Q-values, so it will begin to exploit.

#### Step 3. Evaluate and Update

The agent takes an action, recieves a reward, and percieves the outcome. Now we need to calculate the Q-value for that state-action pair.

We revisit the Bellman equation, except with the addition of a learning rate (α).

![](https://i.imgur.com/1IH18wn.png)

As the agent navigates the world, we keep updating each of the values.

## Appication

### Scenario

Twenty years from now, Gautom loses tenure and becomes a cab driver. But, he's asleep on the job since he stays up all night. What he needs is a self-driving cab.

#### Agent and Environment

Our cab is driving on a 5 by 5 grid world and can travel in any direction (north, south, east, west). There are four locations (R, G, B, Y) where the cab can pick up and drop off passengers. There are also walls, and if the cab tries to drive through it wall, it won't move.

![](https://i.imgur.com/q8LYHec.png)

> Who is the agent? What is the environment? What is the action space (all available actions)? What is the state space (all the possible states?)

#### Rewards

Our goal is to create a cab that can pick up the passenger and bring it to the correct destination as fast as possible and without crashes. To award the cab, we will grant the following:

* A large positive award for a successful dropoff. (+20)
* A penalty for a dropoff at a wrong location. (-10)
* A penalty for an illegal pickup or dropoff move. (-10)
* A slight penalty for driving into a wall. (-1)
* A slight penalty for each time-step the cab takes. (-1)

#### Q-learning

For our Q-table, we need to first determine all the action-state pairs. We can define the action space as follows:

| Index | Move |
|:-:|---------|
| 0 | south   |
| 1 | north   |
| 2 | east    |
| 3 | west    |
| 4 | pickup  |
| 5 | dropoff |

The state space varies on where the cab is (the 25 grid squares), where the destination is (4 dropoff spaces), and where the passenger is (4 dropoff spaces *or* in the cab).

\begin{equation}5 * 5 * 4 * 5 = 500 \end{equation}

So there are 500 possible states. Our table will have the 500 states as rows, and 6 moves as columns. Each value is initialized to zero.

| Action:   | 0 | 1 | 2 | 3 | 4 | 5 |
|-----------|---|---|---|---|---|---|
| State 0   | 0 | 0 | 0 | 0 | 0 | 0 |
| State 1   | 0 | 0 | 0 | 0 | 0 | 0 |
| State 2   | 0 | 0 | 0 | 0 | 0 | 0 |
| ...       |   |   |   |   |   |   |
| State 599 | 0 | 0 | 0 | 0 | 0 | 0 |
| State 600 | 0 | 0 | 0 | 0 | 0 | 0 |

### OpenAI Gym

Creating this environment would take a long time. Fortunately, OpenAI Gym has this exact environment already built for us. 

Gym provides different game environments which we can plug into our code and test an agent. The library takes care of API for providing all the information that our agent would require, like possible actions, score, and current state. We just need to focus just on the algorithm part for our agent.

If you're interested in applying what we will learn today to different environments, you can check out their website [here](https://gym.openai.com/envs/#classic_control). They have a host of different environments, from simple physics engines to Atari games.

![](https://i.imgur.com/4kGem3e.png)


### Implementation

Let's hop right in! Find the colab [here](https://colab.research.google.com/drive/1PdATRBhqSuBM3_x13eY89Vtt7LIA0OKB#scrollTo=4VnvXjiaR0mo).
