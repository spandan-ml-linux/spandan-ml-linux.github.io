---
title:  "Gaussians, Multivariate Gaussians and Halluciantions from such distributions"
author: spandan
categories: [ Basics, Machine Learning ]
tags: [cover, intro]
description: "Gaussians : Simple yet so very important"
featured: false
hidden: false
layout: post
image: assets/images/Gaussian.png
comments: false
---
The curves given above are known as Gaussians. This post aims to discuss what they are, what they mean and to gain intuitive intuitions into what they signify. We shall further learn to hallucinate sample points from such curves and look at what likelihood means. These concepts are fundamental to machine learning and statistics in general.

Networks such as Generative Adversarial Networks(GANs) depend on these fundamental concepts and one shouldn't dive into such networks without first understanding these concepts and gain an insight into randomness and information.

Let's first simply look at Gaussians as a curve in mathematics, and then we will try to come to the concept of it being a probability distribution and infer what that means. The equation goes as follows :

$$ \begin{equation}
      \label{GaussianEq}
            p(x) = {1 \over \sqrt{2\pi\sigma^2}} \hspace{0.1cm} e^{- {1 \over 2 \sigma^2}(x - \mu)^2}
    \end{equation} $$
 
 
where \\( \mu \\)= mean of all values of x and \\(\sigma \\)= the standard variance of all values of x. We shall show these later

Let us have a look at this curve and draw inferences on its nature. 

![Gaussian normal](https://i.imgur.com/T3mzcsF.png)

The highest point of this curve corresponds to \\( x = \mu \\) . We have taken a special case where \\( \mu = 0 \\) and \\( \sigma = 1 \\). In such a case, these are known as normalized Gaussians. Notice the cover figure of the post, the position of the different peaks are the means of those curves. \\( \sigma \\) tells us distribuited the data is away from the mean. So, the more spread out the curve, the higher is the value of \\( \sigma \\). 

Note that $$ \int_{-\infty}^{+\infty} p(x) dx = 1 $$. This means that the fucntion is a Probability Distribution Function. If we have a set of values of x that are Gaussian distributed, ie $$ \textbf{x} : \{x_1, x_2, x_3, \dots\}$$ , then we mean to say that their occurence that a sample from **x** being some \\( x_k\\) follows the probability as per the curve depeinding on them mean of x \\( \mu_x \\) and the standard deviation \\( \sigma_x \)). \\( \mu \\) and \\( \sigma \\) are the only two parameters needed to get this distribution and hence they are together referred to as the **sufficient statistics.** 

Looking at Machine learning from this point of view, we are all looking to develop models that find the "sufficient statistics" for realizing a function. 

### Simulation or Hallucination

From what has already been discussed, we should be able to infer the meaning of a distribution and its points. But, quite often in machine learning, we have to sample values from a given Gaussian distribution to get an array of certain dimensions. Eg: make an array of 100 numbers such that they are from the Gaussian given by mean=0 and standard deviation=0.2. This process of sampling is called **Simulation or Hallucination.** 

It may be denoted as $$ \textbf{x} \sim N(\mu, \sigma^2) $$. 
To Understand this let us look as the Cumulative Distribution function which is as shown :

$$ \begin{equation}
      \label{CDF}
            F(x) = P(X \leq x) = \int_{-\infty}^{x} p(u) du
    \end{equation} $$
 
 Graphically, 
 
 ![CDF](https://i.imgur.com/MVQJfhz.png)
