# Transfer Learning
Let's just start off with an intuitive understanding of what transfer learning is by asking the following questions:

*What happens when we try to learn things?*

*Are we starting from ground zero?*

<img src="https://hci-kdd.org/wordpress/wp-content/uploads/2017/08/Transfer-Learning-the-next-success-Andrew-Ng-845x321.jpg" alt="Quote" class="center">

## Introduction
The *Deep Learning Book* by Ian Goodfellow et al. defines transfer learning as follows:

> Situation where what has been learned in one setting is exploited to improve generalization in another setting.

Basically, the goal of transfer learning is to leverage the knowledge learned in a prior task to improve learning in a target task.

<img src="https://cdn-images-1.medium.com/max/1600/1*9GTEzcO8KxxrfutmtsPs3Q.png" alt="Quote" class="center">

The example we will explore today revolves around ImageNet and MobileNet.

But first let's check out an application of transfer learning: [google's teachable machine](https://teachablemachine.withgoogle.com/).
## Background
What is ImageNet?
<img src="https://miro.medium.com/max/1200/1*v64BvvzbeJvhSen1X7IPNA.jpeg" alt="Quote" class="center">
<br />
Why is it so popular?

<img src="https://thegradient.pub/content/images/2018/07/image_1.png" alt="Quote" class="center">
<br />

What is MobileNet?
<img src="https://www.researchgate.net/profile/Gustav_Von_Zitzewitz/publication/324476862/figure/fig7/AS:614545865310213@1523530560584/Winner-results-of-the-ImageNet-large-scale-visual-recognition-challenge-LSVRC-of-the.png" alt="Quote" class="center">

A review of convolutional neural networks:

<iframe width="100%" height="500px" class="center" src="https://www.youtube.com/embed/Gu0MkmynWkw">
</iframe>

<br></br>

Good sites to mess around with convolutional neural networks and visualize the layers: http://scs.ryerson.ca/~aharley/vis/conv/

## Transfer Learning Methods
There are three main that should be used.

<img src="https://cdn-images-1.medium.com/max/1600/1*mEHO0-LifV7MgwXSpY9wyQ.png" alt="Quote" class="center">

**Inductive Transfer Learning**: This is what we will be doing today. Basically, we know what we have looked at and we know what we want to look at.

## The Path to Hotdog Not Hotdog
Let's start off by gathering the pictures from ImageNet. Open a new colab journal and enter the following code:
``` shell
!pip install imagenetscraper
```
Then to download the photos into a given directory:
``` shell
# Usage: imagenetscraper [OPTIONS] SYNSET_ID [OUTPUT_DIR]
# Options:
# -c, --concurrency INTEGER  Number of concurrent downloads (default: 8).
# -s, --size WIDTH,HEIGHT    If specified, images will be rescaled to the
#                            given size.
# -q, --quiet                Suppress progress output.
# -h, --help                 Show this message and exit.
# --version                  Show the version and exit.
# 
!imagenetscraper n07697537 hotdog
!imagenetscraper n00021265 nothotdog
```

## Extensions
Let's play with flask!