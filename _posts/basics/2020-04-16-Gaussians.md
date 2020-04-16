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
 where \\( \mu = mean of all values of x and \sigma = the standard variance of all values of x \\). We shall show these later

Let us have a look at this curve and draw inferences on its nature. 

![Gaussian normal](https://i.imgur.com/T3mzcsF.png)

The highest point of this curve corresponds to \\( x = \mu \\) 
