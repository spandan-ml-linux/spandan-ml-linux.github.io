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

To sample from the Gaussian distribution, we will use the PDF, CDF and a random number generator(RNG). RNG functions are implemented in all popular programming languages. We will use a random number geneator $rng(x) \in [0,1]$. This follows a uniform distribution and all values are equiprobable.

Let us now have a look at the process.

![Sampling](https://i.imgur.com/7TrphpU.png)

For a single output of the RNG, say 0.65, we would project it on to the CDF and take the corresponding value of $$x$$. Notice how a large portion of the rng numbers would project itself onto the linear section of the graph and thus be closer to the mean, as controlled by the variance. We are consistent with our PDF in this approach.

### Expectation , Monte Carlo convergence and a reference to Information

The Expectation of a PDF refers to the most likely result of a single simulation of a PDF.  For Gaussian distributions, this is easily visualizable from the graph that the mean is the expected value. if we encounter any random variable **x**,  it is by the expectation that we define the mean.

$$ \begin{equation}
      \label{expectation}
            \mathbb{E}(x) = \int_{-\infty}^{x} x p(x) dx = \mu = {1 \over N} \Sigma_{i=1}^N X^{(i)}
    \end{equation} $$
  
  The second equality to the summation os only valid for large values of $$N$$ in which case the sum converges to the integral for random variables. This is known as the **Monte Carlo convergence**. 
  
Gaussians also have importance from the perspective of adding information to models. In the frequency domain, Gaussians are just a line parallel to the X-axis and are familiar to communication Engineers as AWGN. It does not discriminate but adds equally with all frequency components of a signal. **Thus, in Generative models, the use of Gaussians further indicates the addition of the minimum possible bias to the model.**

### Covariance and multivariate Gaussians 

Covariance of two R.Vs X and Y tell us to what extent X and Y are Linearly related.

$$
\begin{equation}
    \label{covariance}
        cov[X,Y] = \mathbb{E[(X- \mathbb{E}[X])(Y- \mathbb{E}[Y])} = \mathbb{E}[XY]-\mathbb{E}[X]\mathbb{E}[Y]
\end{equation}
$$

Note : $$ cov[X,X] = Var[X] = \sigma^2(X) $$
