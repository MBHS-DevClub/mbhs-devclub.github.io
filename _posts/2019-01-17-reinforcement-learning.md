---
layout: post
title: Reinforcement Learning
tags: [rl]
excerpt_separator: <!--more-->
---

<div style="text-align:center"><img src ="https://thumbs.gfycat.com/RashFlippantIbadanmalimbe-size_restricted.gif" height="350"/></div>


## Introduction

### Background

So far, we have touched on supervised and unsupervised learning. Today, we're going to explore a third type: reinforcement learning.

<div style="text-align:center; margin:auto;">
<table style="width:100%">
  <tr>
    <th>Supervised Learning</th>
    <th>Unsupervised Learning</th> 
    <th>Reinforcement Learning</th>
  </tr>
  <tr>
    <td>y = f(x)</td>
    <td>f(x)</td>
    <td>f(x) = z</td>
  </tr>
</table>
</div>

**Supervised Learning**
In supervised learning we were interested in finding (fitting) a function $f$ based on a set of $x$ and $y$ values. 

**Unsupervised Learning**
Given some set of $x$ values, find a function $f$ that can elucidate connections in the data.

**Reinforcement Learning**
Find a function $f$ knowing some $x$, $y$, $z$.

### Example

Welcome to grid world. You, the player, can move up, down, left and right, notated U, N, L, R. If you land on a green tile, you win a point. If you land on a red tile, you lose a point.

<div style="text-align:center"><img src ="https://i.imgur.com/NkcPep1.png" height="350"/></div>

#### Objective 1 - Hard

Find a five move path that can score the most points. This should be easy.

> UURRR or RRUUR

#### Objective 2 - Harder

Let's add some uncertainty.

When you choose a move, there is 80% chance that the chosen move is taken. There is also a 20% chance that you turn left (10%) or right (10%) before moving.

Now, how reliable is our previous sequence, UURRR?

The easy answer is just to calculate the chance that something will go wrong.

> 0.8^5 = 0.32768

But, there's another path. From UURRR, you could *accidentally* perform RRUUR and reach your goal. The chance of this happening is much smaller.

> 0.1^4*(0.8) + 0.8^5 = 0.0008 + 0.32768 =  0.32776

So, now that we have our task, how do we represent it?

## Representation ##

All reinforcement algorithms are premised off an agent interacting an environment.

![](https://i.imgur.com/48O2aJQ.png)

**Agent**: The "thing" that attempts the task. Usually a program.
**Environment**: The "physics" engine of the task. Responsible for giving out the states, rewards and the possible actions to take.
**State**: A snapshot of the current environment, the information given to the agent.
**Reward**: A value. The agent attempts to maximize the cumulative sum of rewards over time.
**Action**: Options that an agent could choose to influence the environment.

### Representing Grid World ###

Each of these compenents can be applied to grid world.

**Agent**: Player
**Environment**: Grid World
**State**:

* Player Position
* Grid Contents

> Note: The state is subjective. The inputs could entered in different ways.

**Reward**: Points
**Action**: Move Up, Move Down, Move Left, Move Right

But, how do we represent uncertainty?

## Mathematical Background ##

The Markov Decision Process, or MDP, is a way to formalize actions in the face of ucnertainty. Before we get to MDP, we need to first understand Markov Chains.

### Markov Process 

We're going to start with an easier example. Suppose that we want to represent the weather. Our Markov Chain could look like this.

![](https://i.imgur.com/TNElFQF.png)

There are two parts to this diagram:

* **State:** The circles, Sunny and Rainy
* **Transition Function:** The lines that connect the cicles.
 
Transition function takes two arguments, a origin and destination state, and returns the probability of such transition.

> P(dest | origin) = prob

In this weather example, we can represent the transition function as a table:

| origin | dest | p(dest\|origin)|
| -------- | -------- | -------- |
| Sunny     | Sunny     | 0.8     |
| Sunny     | Rainy     | 0.2     |
| Rainy     | Sunny     | 0.7     |
| Rainy     | Rainy     | 0.3     |


When take a sample of the chain, you would get a certain chain of events.

> For example: Sunny, Sunny, Sunny, Sunny, Rainy, Sunny, Rainy ...

This sequence is called the **history**.

One important principle of Markov chains is that the states satisfy the **Markov Property**. The Markov Property states that each state encapsulates all the information possible. 
In other words, any additional history beyond that states does not affect the next outcome.

Mathematially, this could expressed as:

![](https://i.imgur.com/acSyYjb.png)

In most real life applications, the Markov Property may not be always satisfied. That would mean that some of the theoretical guarantees on some algorithms would no longer hold. Fortunately, most algorithms do fine with states that don't satsify the markov property.

### Markov Reward Process

Now, lets add in a new value, reward.

![](https://i.imgur.com/lBhyPBV.png)

Like the last chain, we have states and a transition function. But, now there is an additional scalar value that is collected when transversing.

The history of this process is slightly more complicated. Here is an example sequence:

Class 1, Class 2, -.2, Class 3, -.2, Pass, -.2, Pass, 10, Sleep

In this example, there is an definitive **starting state** and **terminal state**.
(Markov Chains could also have both of these states, too)

The total reward of a certain sequence is simply the sum of all the rewards.

You could also use discounting while summing the rewards.

When discouting, a certain ratio, called the discounting ratio, is applied when moving from state to state.

Using the previous example with a a discounting ratio of k = 0.9:

> discounted sum = 0.9 ^ 0 * -.2 + 0.9 ^ 1 * -.2 + 0.9 ^ 2 * -.2 + 0.9 ^ 3 * 10 = 6.748

So, the amount of reward decays by a power of the discounting ratio.

There are two primary uses of the discounting ratio:
* Allow situations with infinite length episodes (process that don't have terminal states) to have a sum of rewards
* Prioritize rewards gained in the short term

#### Value functions

A central component of RL is the concept of **value functions**.

A **state-value** function keeps track of the **expected value** of the **sum of rewards from the state**.

### Markov Decison Process

Now, we have reached the **Markov Decision Process**, the third iteration of the markov process.

Here, we include an **action** in addition to the **state**, **action** and **reward** in the Markov Reward Process (MRP).

![](https://i.imgur.com/wEn50Lv.png)

Now, at each state, an certain agent chooses the actions to take, influencing the transition function. In this scenario, the action dictates, absolutely, the next state. In some other examples, the action might specify a certain **probability distribution** of destination states.

## Exploration vs Exploitation

One of the key problems in RL is the tension between exploration and exploitation.

Take a look at the diagram below:

![](https://i.imgur.com/0rgLAW0.png)

Here, we have an diagram of an cat and mouse grid world.

The mouse attempts to collect as much as cheese as possible, given a certain time constraint. It is blind, that is, without moving around, the mouse does not know of any potential cheeses.

There are two types of cheeses: small cheese (+1) and big cheese (+50).

The cat, a bit lazy, stays on his square. If the mouse is on the same square on the cat, the mouse dies (-1000 reward).

The mouse faces a problem. In the beginning, he would get a sizeable amount of reward collecting the nearby cheeses. However, to get more, the mouse needs to go out further, **risking the cat** and **forsaking his dependable supply of small cheeses**.

**Exploitation** is the concept of maximizing the rewards of the current situtation. In this situation, eating the small cheese is considered **exploitation**. **Exploration**, on the other hand, is to take suboptimal actions to discover new information, perhaps leading to a greater reward.


## Basic Techniques

There are many types of RL algorithms, but we are going to focus on the three most fundemental ones: **Dynamic Programming (DP)**, **Monte Carlo (MC)**, and **Temporal Difference (TD)**.

Dymamic Programming is used when the model dynamics of the environment is **known**.

Monte Carlo and TD is used the when the environment is **unknown**.

### Dynamic Programming

In dynamic programming, we are given the entire state-transition function, P(S', R| S, A), or in other words, the entire dynamics of the environment: how states change and how rewards are handed out.

In the conventional DP, we keep track of the value function of each state, iterating through the values until our value functions converges.

An analogy looks like this:

$$ x = \sqrt{x + 56} $$

To solve this equation, we could square both sides, and solve for x.

But, what if its hard to solve for x? We could try iteration, where we start with a certain value, and then repeatedly plugin the result back into the original equation

$$ x_{t+1} = \sqrt{x_{t} + 56} $$

**Desmos Demo**


### Continous vs Episodic Tasks

* Episodic: 
* Continuous

### Monte Carlo and Temporal Difference

In **Monte Carlo**, you sample an entire episode, and recieve a certain sum of rewards. Then, using this sum of rewards at the very end, you update the value functions of each situation.

In **Temporal Difference**, instead of waiting till the very end, you update based on the predictions of the next scenario. This concept of basing prediction on predictions is called **bootstrapping**.

![](https://i.imgur.com/gztT76k.png)


![](https://i.imgur.com/VoO21iR.png)



