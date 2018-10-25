---
layout: post
title: Classification
tags: [ai, ml, logReg]
excerpt_separator: <!--more-->
---

Before you begin, follow along on our [notebook companion](https://colab.research.google.com/drive/1Z2ntlVydT75fDj-V-w8LI-_90K32WIzb).

# Classification

Last week, we learned about linear regression. For any set of inputs, it returned a continuous, numeric output. Using our model, we could predict the price of ice cream for any given temperature.

But, what if we didn't want to return a quantity? What if wanted to predict discrete values? What if, instead of the price of the ice cream, we wanted to predict whether or not we could afford it? For this lecture, we will focus on **mutually exclusive** and **binary** values.

Some common scenarios could be...

* ... deciding if it is necessary to study for a test or not.

* ... deciding whether to perform a surgery.

## An Initial Exploration
We could try by extending our linear regression. Let's train our linear model to return a **score**, and if the score meets a **cutoff**, we would return one value. Or else, the other value would be returned.

```if w_0 + w_1x_1 + w_2x_2 >= c:
  return 1
else:
  return 0
 ```

<div style="text-align:center"><img src ="https://i.imgur.com/UXeru5y.png" /></div>

This is a good start, but what we really want  is a model that returns **the probabilites of each action being the correct one**.

Examples:

* There is a 20% that studying is required 

* There is a 90% chance that surgery is proper for the situation

Just using linear regression to figure out the probability would not work, because the function is unbounded: **it just a straight line (or surface) that goes up and up and up . . .**

If only we could squash the probabilities between 0 and 1 . . .

## Logistic Regression

Now, enter the great and beloved logistic equation!

<div style="text-align:center"><img src ="https://i.imgur.com/cRjU634.png" /></div>

This is just the function we need to keep our probabilities between 0 and 1. 

Remember asymptotes? This function has two: 0 as x approaches `-inf` and 1 as x approaches `+inf`.

Now, lets try running logistic regression on our previous data:

<div style="text-align:center"><img src ="https://i.imgur.com/7sQNw8V.png" /></div>

Think of the bottom access as the score, or how confident the algorithm is. In practice, multiple features could combined into this one "score" metric.

## Naive Bayes
**Why is Naive Bayes important?**
Naive Bayes still stays relevant today just because of how well it works. We went over stochastic and deterministic models before. Nowadays, stochastic models ---Neural Networks--- are dominating the field. However, Naive Bayes is still used by many different programs such as, marking which emails are spam, classifying news articles, and determining whether a piece of text is positive or negative, etc.

<div style="text-align:center"><img src ="https://i.postimg.cc/HxrLwDmf/Screen-Shot-2018-10-25-at-12-24-37-PM.png" /></div>

Naive Bayes algorithms in some cases today, still outperform algorithms that *in theory* should work better. There are a couple of different theories and explanations as to why. 

#### Conjoint Probability

Conjoint probability aims to determine the probability of one event, *given* some other event.


Going back to our previous examples, this could entail....

* ... deciding if it is necessary to study for a test or not *given* which materials we studied.

* ... deciding whether to perform a surgery *given* that certain medical facts about the patient.


We're going to use an analogy. Suppose we have a waterfall with two streams, a red stream and a blue stream, where some water from each stream is diverted.

<div style="text-align:center"><img src ="https://i.imgur.com/D8EhY65.png?0" /></div>

> Credits to Arbital

Of the entire waterfall:
* 80 gallons per second flow from the blue stream.
* 20 gallon per second flow from ther red stream.
* 90% of the red water reaches the bottom.
* 30% of the blue water reaches the bottom.

<div style="text-align:center"><img src ="https://i.imgur.com/wK6cg5z.png" /></div>

The question we're asking is: **what percent of the water at the bottom came from the red stream?**

#### Representation

We denote this conditional property with a vertical line:

$$
P(A\:\&\:B) = P(A)*P(B|A)
$$

Basically, everything after the line has to be true. 

Conditional probability is simply the idea of calculating probability, knowing that something is true---or a set of factors is true. A common example is heart disease.

In predicting heart disease, we know that many different factors go into it's calculation. For example, age, gender, race, etc. The way we would express this is:

$$
P(A|B)
$$

#### Derivation

Here's how we derive Baye's Theorem.

First, the probability of A and B occuring must be *commmunitive*:

$$
P(A\:\&\:B) = P(B\:\&\:A)
$$

$$
P(A)*P(B|A) = P(B)*P(A|B)
$$

Now we simply divide:

$$
P(A|B) = \frac{P(A)*P(B|A)}{P(B)}
$$

The analogous implication? The percentage of water at the bottom originating from the red stream is the amount of water from the red stream as a whole, multiplied by the percent of the red stream that reaches the bottom, divided by the total amount that reaches the bottom.


















