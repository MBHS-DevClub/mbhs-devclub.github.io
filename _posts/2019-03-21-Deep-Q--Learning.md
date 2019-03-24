---
layout: post
title: Deep Q-Learning
tags: [rl]
excerpt_separator: <!--more-->
---

## Introduction

### Background

In March of 2016, Google's AlphaGo smacked a Chinese Go master named Lee Sedol. This was unprecedented, and the underlying technology was **Deep Q-Learning**.

![](https://i.imgur.com/rQqiYOK.png)

### Plan

The last time we covered q-learning was towards the end of January. Today, we're going to revisit the topic. Instead of a simple Q-learning algorithm, we're going to advance into deep Q-learning.

First, we will review what we know about reinforcement learning and Q-learning. Second, we wil learn about deep Q-learning. Third, we're going to look at a particular environment from OpenAI. Finally, we're going to implement deep Q-learning with Keras.

## Background

### Review


remember the idea behind reinforcement learning


![](https://i.imgur.com/48O2aJQ.png =400x)

two key terms are policy and Q.

policy is a particular strategy...

q is an evaluation of that...

![](https://i.imgur.com/VsP7imb.png)


this is the idea behind q-learning

![](https://i.imgur.com/W1VClRb.png =600x)

we're still going to adhere to this structure.

### Deep Q-Learning

Here's the idea. Instead of a table of Q-values, the agent will use a neural network. The network will accept the state as the input and return an action to take.

![](https://i.imgur.com/tfmCcKo.png =400x)


## Application

### Scenario

After Gautom successfully designed his taxi cab AI, he starting goofing off during work. One of his stunts was riding *on top* of his taxi. Below, we can see a low-resolution image of him in action.

![](https://cdn-images-1.medium.com/max/1600/1*oMSg2_mKguAGKy1C64UFlw.gif)

Our goal is really simple. As the taxi, we want to maximize the amount of time Gautom can stand on top of the taxi without him falling. Ideally, we'd like to be able to never drop him.

### Components

Who's the agent?

The environment?

What is the observation space?

What about the action space?

How can we dispense rewards?

Why might simple Q-learning *not* work?

### Design

Recall the structure of a neural network.

![](https://i.imgur.com/9enGnpN.png)

The input layer with be the observation space, and the output layer will be the action space. Our network will have three hidden layers.

The first two hidden layers layers will deploy ReLU activation functions.

![](https://i.imgur.com/g6nqh8f.png =400x)

The final hidden layer will use a linear activiation function.

![](https://i.imgur.com/U2YrtGC.png =400x)

We're going to use the Mean Squared Error (MSE) loss function. 

![](https://i.imgur.com/IdczDBa.png =400x)


Finally, for gradient descent, we'll be using an Adam Optimizer. Studies have demonstrated that it generally is the best algorithm. If you're interested, the procedure is below.

![](https://i.imgur.com/MR4T3zA.png =500x)

### Implementation

The notebook can be found [here](https://colab.research.google.com/drive/1l1swesXldH25hR7MntJ3Z3Griex8LerL).
