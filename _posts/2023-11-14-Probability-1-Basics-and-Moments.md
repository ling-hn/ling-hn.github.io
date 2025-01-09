---
layout: post
title: Revisit Probability (1) - Brief Review of Probability
description: A brief overview of fundamental probability concepts, together with visualization practice. 
date: 2023-11-14
author: L. H. Huang
tags: ["Study Notes", "Physics", "Python"]
features:
  math:
    enable: true
---

- **Probability**
  - A measure of the "likelihood" that an event will occur. 
  - The uncertainty of outcomes of a random phenomenon or experiment.

- **Random Variables**
  - A variable that takes on different values as a result of random outcomes of a random experiment or process.
  - A function that maps each outcome $$\omega$$ in the sample space $$\Omega$$ to a real number $$X(\omega)$$, assigning a numerical value to each outcome of the experiment
  - Types of Random Variables
      - Discrete Random Variables: countable number of distinct values
      - Continuous Random Variables: an uncountably infinite number of possible values within or interval

#### Probability Mass Functions (PMF) 

$$
P(X = x)
$$

- A discrete random variable $$X$$ gives the probability that $$X$$ takes on a specific value $$x$$
- Examples: Bernoulli distribution, Binomial distribution, and Geometric distribution

#### Cumulative Distribution Functions (CDF)

$$
F_X(x) = P(X \leq x)
$$

- The accumulated probability up to $$x$$ that the random variable $$X$$ can achieve. It provides a complete picture of the distribution of $$X$$ from $$-\infty$$ to $$\infty$$.
- Properties
    1. Non-decreasing: $$F_X(x_1) \leq F_X(x_2)$$ if $$x_1 \leq x_2$$.
    2. Limits: $$\lim_{x \to -\infty} F_X(x) = 0$$; $$\lim_{x \to \infty} F_X(x) = 1$$
    3. Right-Continuity: $$\lim_{h \to 0^+} F_X(x + h) = F_X(x)$$.

#### Probability Density Functions (PDF)

$$
    f_X(a \leq x \leq b)=\int_a^b f_X(x) dx
$$

$$
    \int_{-\infty}^{\infty} f_X(x) dx = 1
$$

- A continuous random variable $$X$$, denoted as $$f_X(x)$$, is a function that describes the relative likelihood of $$X$$ taking on a specific value $$x$$.

**Example 1:**
Fair Six-Sided Die (Discrete Random Variable)

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/H1VQznL_0.png" width="500">
</div>

**Example 2** 

The exponential distribution with rate parameter $$\lambda > 0$$ has the PDF: $$f_X(x) = \begin{cases} 
\lambda e^{-\lambda x}, & \text{if } x \geq 0 \\
0, & \text{if } x < 0
\end{cases}$$

The CDF $$F_X(x)$$ for the exponential distribution is:
$$F_X(x) = \begin{cases}
1 - e^{-\lambda x}, & \text{if } x \geq 0 \\
0, & \text{if } x < 0
\end{cases}$$

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/Hybq428OA.png" width="500">
</div>


### Moments of Distributions

The $$n^{th}$$ moment is defined as 

$$
\mathbb{E}[(X - c)^n] = \int_{-\infty}^{\infty} (x - c)^n f(x) \, dx
$$

- When $$c = 0$$: This formula simplifies to the **$$n^{th}$$ raw moment**, providing information about the shape of the distribution relative to the origin (zero)

$$
\mathbb{E}[X^n] = \int_{-\infty}^{\infty} x^n f(x) dx
$$

- When $$c = \mu$$: The mean $$\mu$$ of $$X$$, the formula gives the **$$n^{th}$$ central moment**, prioviding information about the shape of the distribution relative to its mean. 

$$
\mu_n =\mathbb{E}[(X -  \mu)^n] = \int_{-\infty}^{\infty} (x -  \mu)^n f(x) dx
$$

Central moments provide information about the shape of the distribution relative to its mean. 

**Standardized moments**: a dimensionless form to express moments of a probability distribution and provide a way to compare distributions with different scales. Usually for higher order of moment.

$$
\bar{\mu_n} = \frac{\mu_n}{\sigma^n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n}
$$

where $$\mathbb{E}[(X - \mu)^n]$$ is the $$n$$-th central moment of $$X$$ and $$\sigma$$ is the standard deviation of $$X$$, which is the square root of the variance. 

$$
\quad
$$


#### Zeroth Moment: Total Probability (*Mass*)

$$
\mu_0 = \bar{\mu_n} = \mathbb{E}[(X - \mu)^0] = \mathbb{E}[1] = 1
$$

![image](https://hackmd.io/_uploads/Bk4Qwrzf1x.png)

$$
\quad
$$


#### First moment: Expectation (Mean) (*Mean position*)

$$
\mu_1 = \mu = \begin{cases} 
\sum_{x} x p(x) \quad \text{ (discrete)} \\
\int_{-\infty}^{\infty} x f(x) dx  \quad \text{ (continuous)}
\end{cases}
$$

![image](https://hackmd.io/_uploads/Sk3WYBGMke.png)

> (a) Normal distribution: $$f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$$ where mean $$\mu = 0.5$$ and standard deviation $$\sigma = 1$$
> (b) Gamma Distribution:$$f(x) = \frac{x^{k-1} e^{-x/\theta}}{\theta^k \Gamma(k)}$$, where shape parameter$$k = 2$$, scale parameter $$\theta = 0.25$$, and mean $$k \cdot \theta = 0.5$$.


$$
\quad
$$

#### Second moment: Variance (*Spread*)
$$
\mu_2 = \sigma^2 = \mathbb{E}[(X - \mu)^2] = \int_{-\infty}^{\infty} (x -  \mu)^2 f(x) dx
$$
$$
\text{Standard deviation } \sigma = \sqrt{\mu_2} = \sqrt{\mathbb{E}[(X - \mu)^2]}
$$

![image](https://hackmd.io/_uploads/r1QiYrMMkg.png)

> (a) Normal distribution: $$f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$$ where mean $$\mu = 0.5$$ and standard deviation $$\sigma = 0.25, 1, 4. $$
> (b) Exponential Distribution**: $$f(x) = \lambda e^{-\lambda x}$$, where rate parameters $$\lambda = 1, 2, 4$$, and variance (displayed in the legend as $$\sigma^2$$) for each case is $$\sigma^2 = 1 / \lambda^2$$, which corresponds to $$0.0625$$, $$0.25$$, and $$1$$.

$$
\quad
$$


#### Third standardized moment: Skewness (*Asymmetry*)
- A skewness of 0 indicates a symmetric distribution.
- A positive skewness indicates a distribution with a longer right tail (right-skewed).
- A negative skewness indicates a distribution with a longer left tail (left-skewed).

$$
\bar{\mu_3} = \frac{\mu_3}{\sigma^3}\frac{\mathbb{E}[(X - \mu)^3]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^3}
$$

![image](https://hackmd.io/_uploads/S1aQz8zGJe.png)

> ***Discrete Distributions***
> * Binomial Distribution: $$P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k}$$, where $$n = 20$$ and $$p = 0.5$$ (Symmetric) and $$p=0.9$$ (Negatively Skewed).
> * Poisson Distribution (Approximate Positive Skew): $$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$$ the probability of a given number of events occurring within a fixed interval, with an average rate of 5 events ($$\lambda = 5$$).
> 
> ***Continuous Distributions***
> Normal Distribution: $$f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$$, where $$\mu = 0$$ and $$\sigma = 2$$. 
> 
> Skewed Distribution: $$f(x) = \frac{2}{\sigma \sqrt{2 \pi}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} \Phi\left(\alpha \frac{x - \mu}{\sigma}\right)$$, where $$\alpha = 5 or -5$$ is the skewness parameter for right-skewed (positively skewed) and left-skewed (negatively skewed), respectively.
> 
> ```python
> positive_skew_dist = stats.skewnorm(a=5, loc=-5, scale=4).pdf(x)
> negative_skew_dist = stats.skewnorm(a=-5, loc=5, scale=4).pdf(x)
> ```
> - **`a`**: controls the skewness of the distribution.
> - **`loc`** and **`scale`**: These are used to shift (center) and stretch (spread) the distribution.


**Checkpoint**

* Why using standardized moment instead of central moment?
:  To compare across different datasets regardless of their scale.

* Why using standard deviation instead of mean value?
: Normalized by distribution shape instead distribution position.

Moments are not dimensionless—they have units that depend on the power $$n$$ of the units of $$X$$. To make moments comparable across different scales and units, we standardize them. The standardized $$n^{th}$$ moments is obtained by dividing the $$n^{th}$$ central moment central moment by a normalization factor. 

$$
\bar{\mu_n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n} [=] \frac{X^n}{\sqrt{X^2}^{n}} [=] X^0 \quad \text{dimensionless quantity}
$$

Recall that the mean provides a measure of central tendency. It tells us where the center of a distribution is located and based on it we calculate the second moment (how does the distribution spread) and the third moment (how does the distirbution look like). While the mean provides information about the center, it doesn’t directly address the scale of dispersion or how asymmetrically the data are distributed. Therefore, using the standard deviation (which accounts for spread) makes more sense for normalizing moments like skewness and kurtosis.


<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/BkeIlyeYC.png" width="500">
</div>

> This figure demonstrates how scaling affects the spread and raw moments (such as the third central moment) of a distribution without altering its shape or normalized skewness. Recall $$\mu_1 = \frac{1}{n} \sum_{i=1}^{n} x_i$$, $$\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}$$, $$\mu_{3} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^3$$, and finally $$\bar{\mu_3} = \gamma = \frac{\mu_3}{\sigma^3}$$.

$$
\quad
$$

---

$$
\quad
$$

***Revisit Probability***

[(1) Brief Review of Probability](/2023/11/14/Probability-1-Basics-and-Moments)\\
[(2) What is "Moment"?](/2023/11/15/Probability-2-What-is-moment)\\
[(3) Understanding Kurtosis (κυρτός)](/2024/07/01/Probability-3-Kurtosis)

$$
\quad
$$

---

$$
\quad
$$

#### Reference

* https://cs229.stanford.edu/section/cs229-prob.pdf
* https://gregorygundersen.com/blog/2020/04/11/moments/
* https://www.itl.nist.gov/div898/handbook/eda/section3/eda35b.htm