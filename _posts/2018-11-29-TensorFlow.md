---
layout: post
title: Basic Image Classification with TensorFlow
tags: [tensorflow, image_classification]
excerpt_separator: <!--more-->
---

> Follow along [here](https://colab.research.google.com/drive/1o6-_tz4B1k2tQG39rnrARhb4xMwtIXJx).

## Introduction


### Background

Trying to implement machine learning from scratch, like we did last lecture, is difficult and tedious. Instead of writing everything ourselves, we can look towards online resources.

TensorFlow is a machine learning **library**. It isn't an app or programming language, but rather a collection of pre-written code that can be referenced in your own code.

TensorFlow is a powerful library for machine learning. It is used by data scientists and developers alike for it's simplicity and power.

### Setting Up

To use TensorFlow, download the package from GitHub. The most recent version (1.12.0) can be found **[here](https://github.com/tensorflow/tensorflow/releases/tag/v1.12.0)**.

<div style="text-align:center"><img src ="https://i.imgur.com/yRzIspW.png" /></div>

The `.zip` file should contain a list of folder. Within the subfolder called `tensorflow`, you will find the libraries for the different programming languages.

<div style="text-align:center"><img src ="https://i.imgur.com/kNgPCRy.png" /></div>

The TensorFlow library is implemented with the same features in each language. For this lecture, we will demonstrate using the **Python** library.

### Keras

TensorFlow features useful **APIs**, or Application Program Interfaces. An API is just a framework for building software, like a toolbox.

Keras is just one of the APIs that is supported by TensorFlow. The API makes it fast and easy to build neural networks.

In this lecture, we are going to use Keras to build a simple neural network model in Python.

## Implementation

Our goal is to design a neural network that can classify clothing. Given pictures of articles of clothing, we want our model to identify it as a dress, coat, shirt, etc.

### Data Collection

To train and test our network, we first need a *lot* of labled pictures of clothing. Fortunately, the Fashion MNIST database happens to contain 70,000 labeled pictures of 28 x 28 resolution. You can find it **[here](https://www.kaggle.com/zalando-research/fashionmnist)**.

<div style="text-align:center"><img src="https://tensorflow.org/images/fashion-mnist-sprite.png"></div>

The images are labeled with numbers from 0 to 9. The labels are assigned as outlined in the table.

| Label | Article | 
| -------- | -------- | 
| 0     | T-Shirt     |
| 1     | Pants     |
| 2     | Pullover     |
| 3     | Dress     |
| 4     | Coat     |
| 5     | Sandal     |
| 6     | Shirt     |
| 7     | Sneaker     |
| 8     | Bag     |
| 9     | Ankleboot     |

Next, we need to split up our data into our training and test sets. Remember---if we *didn't* split up our data, then we would risk overfitting our model.

<div style="text-align:center"><img src="https://elitedatascience.com/wp-content/uploads/2017/06/Train-Test-Split-Diagram.jpg"></div>

We will take 60,000 images for training, and will use the remaining pictures for testing. Luckily for us, TensorFlow makes this distinction automatically.

### Setup

We will start our program by importing the libraries we want to reference.

```python
# TensorFlow and the Keras API
import tensorflow as tf
from tensorflow import keras

# Helper libraries
import numpy as np
import matplotlib.pyplot as plt
```

Next, we want to input our `fashion_mnist` data. Fortunately, TensorFlow's `load_data` method automatically formats the dataset into groups of training and testing data, as well as sets of images and labels.

```python
fashion_mnist = keras.datasets.fashion_mnist

(train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
```

>Try *train_images.shape*, what does this seem to do?

As shown, each picture is a collection of 784  pixels of varying brightnesses:

```python
#Challenge: add flexibility
plt.figure()
plt.imshow(train_images[1])
plt.colorbar()
plt.grid(False)
print("Image at index zero is a" + class_names[train_labels[1]] +".")
```

You can also use graphs to determine if your training data is correct before training:

```python
plt.figure(figsize=(10,10))
for i in range(25):
    plt.subplot(5,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(train_images[i], cmap=plt.cm.binary)
    plt.xlabel(class_names[train_labels[i]])
```

### Data Adjustment

Some of our data need to be adjusted. By default, the colors of the pixels are represented with a value from 0 to 255.

<div style="text-align:center"><img src="https://i.imgur.com/Ii4scZv.png"></div>

But, the neurons are supposed to accept and output values from 0 to 1. We can easily fix the data as follows.

```python
train_images = train_images / 255.0
test_images = test_images / 255.0
```

<div style="text-align:center"><img src="https://i.imgur.com/DoKkNop.png"></div>

The other problem is with our outputs. We want our model to return the name of the piece of clothing, not a number. To fix this, we can create an array that translates the index to the appropriate name.

```python
class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat', 'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']
```

### Layers

The next step is building our layers. Keras makes it easy to generate entire layers.

```python
model = keras.Sequential([
    keras.layers.Flatten(input_shape=(28, 28)),
    keras.layers.Dense(128, activation=tf.nn.relu),
    keras.layers.Dense(10, activation=tf.nn.softmax)
])
```

> TensorFlow uses a unique designation to give coders a smart and efficient machine learning experience. In tensorflow, our "nodes" are called tensors. More information **[here](https://www.tensorflow.org/guide/tensors)**.

Our program contains three layers in total:

```python
keras.layers.Flatten(input_shape=(28, 28)),
```

This first layer will be our "input" layer. It will turn our 2-dimensional array of pictures into a "flattened" 1-dimensional array.

<div style="text-align:center"><img src="http://www.superdatascience.com/wp-content/uploads/2018/08/CNN_Step3_Img1.png"></div>

---

```python
keras.layers.Dense(128, activation=tf.nn.relu),
```

Our first "Dense" layer will be next. This layer is "Dense" as the neural layers are all densely-connected. This layer has 128 tensors.

---

```python
keras.layers.Dense(10, activation=tf.nn.softmax)
```

Our last layer is a 10-node *softmax* layer. This would be our output layer, where each index is a logistic probability.

All of our layers, as shown, are compiled together in a sequential model (`keras.Sequential`)

### Model Parameters

Just before we get to training, we will need to compile our model. This is what it looks like:

```python
model.compile(optimizer=tf.train.AdamOptimizer(), 
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

Here, we are defining a few things:

* *Loss function*---This measures how accurate the model is during training. We want to minimize this function to "steer" the model in the right direction.
* *Optimizer*---This is how the model is updated based on the data it sees and its loss function.
* *Metrics*---Used to monitor the training and testing steps. The following example uses accuracy, the fraction of the images that are correctly classified.

### Training

In our [XOR implementation](https://devclub.ml/2018/11/08/xor-implementation.html), training our model was the most difficult part to code. With Keras, all we have to do is define our training data, and number of epochs.

```python
model.fit(train_images, train_labels, epochs=5)
#Try to determine what each output in the console display means.
```

It's really that simple.

### Evaluating our Model

Evaluating our model is the simple use of the `model.evaluate` command. This uses our remaining 10,000 data examples. Our program has never seen any of this data, but will still evaluate it at around 85% accuracy.

```python
test_loss, test_acc = model.evaluate(test_images, test_labels)
print('Test accuracy:', test_acc)
```

How do we know our model is slightly overfit?

### Visualizing our Predictions

Check in our [colab notebook](https://colab.research.google.com/drive/1o6-_tz4B1k2tQG39rnrARhb4xMwtIXJx) for the week to see how we can visualize our model predictions.

## Closing up shop

If you finish early, try to classify hand-written digits; think through each line for how the models differ.
