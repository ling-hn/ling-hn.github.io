---
layout: post
title: Brief Review of Probability
description: A brief overview of fundamental probability concepts, together with visualization practice. Advanced topics are still under construction.
date: 2023-11-14
author: L. H. Huang
tags: ["Study Notes", "Physics"]
features:
  math:
    enable: true
---

- **Probability**
  - A measure of the "likelihood" that an event will occur. 
  - The uncertainty of outcomes of a random phenomenon or experiment.

- **Random Variables**
  - A variable that takes on different values as a result of random outcomes of a random experiment or process.
  - A function that maps each outcome $\omega$ in the sample space $\Omega$ to a real number $X(\omega)$, assigning a numerical value to each outcome of the experiment
  - Types of Random Variables
      - Discrete Random Variables: countable number of distinct values
      - Continuous Random Variables: an uncountably infinite number of possible values within or interval

#### Probability Mass Functions (PMF) 
$$P(X = x)$$

- A discrete random variable $X$ gives the probability that $X$ takes on a specific value $x$
- Examples: Bernoulli distribution, Binomial distribution, and Geometric distribution

#### Cumulative Distribution Functions (CDF)
$$
    F_X(x) = P(X \leq x)
$$

- The accumulated probability up to $x$ that the random variable $X$ can achieve. It provides a complete picture of the distribution of $X$ from $-\infty$ to $\infty$.
- Properties
    1. Non-decreasing: $F_X(x_1) \leq F_X(x_2)$ if $x_1 \leq x_2$.
    2. Limits: $\lim_{x \to -\infty} F_X(x) = 0$; $\lim_{x \to \infty} F_X(x) = 1$
    3. Right-Continuity: $\lim_{h \to 0^+} F_X(x + h) = F_X(x)$.

#### Probability Density Functions (PDF)
$$
    f_X(a \leq x \leq b)=\int_a^b f_X(x) dx
$$
$$
    \int_{-\infty}^{\infty} f_X(x) dx = 1
$$

- A continuous random variable $X$, denoted as $f_X(x)$, is a function that describes the relative likelihood of $X$ taking on a specific value $x$.

**Example 1:**
Fair Six-Sided Die (Discrete Random Variable)

<p>
  <img src="https://hackmd.io/_uploads/H1VQznL_0.png", style="width: 70%;"/>
</p>

**Example 2** 

The exponential distribution with rate parameter $\lambda > 0$ has the PDF: $f_X(x) = \begin{cases} 
\lambda e^{-\lambda x}, & \text{if } x \geq 0 \\
0, & \text{if } x < 0
\end{cases}$

The CDF $F_X(x)$ for the exponential distribution is:
$F_X(x) = \begin{cases}
1 - e^{-\lambda x}, & \text{if } x \geq 0 \\
0, & \text{if } x < 0
\end{cases}$

<p>
  <img src="https://hackmd.io/_uploads/Hybq428OA.png", style="width: 70%;"/>
</p>

### Moments of Distributions

#### Definitions
The $n^{th}$ moment is defined as 

$$
\mathbb{E}[(X - c)^n] = \int_{-\infty}^{\infty} (x - c)^n f(x) \, dx
$$

- When $c = 0$: This formula simplifies to the **$n^{th}$ raw moment**, providing information about the shape of the distribution relative to the origin (zero)
$$
\mathbb{E}[X^n] = \int_{-\infty}^{\infty} x^n f(x) dx
$$

- When $c = \mu$: The mean $\mu$ of $X$, the formula gives the **$n^{th}$ central moment**, prioviding information about the shape of the distribution relative to its mean. 
$$
\mu_n =\mathbb{E}[(X -  \mu)^n] = \int_{-\infty}^{\infty} (x -  \mu)^n f(x) dx
$$Central moments provide information about the shape of the distribution relative to its mean. 

**Standardized moments**: a dimensionless form to express moments of a probability distribution and provide a way to compare distributions with different scales. Usually for higher order of moment.
$$
\bar{\mu_n} = \frac{\mu_n}{\sigma^n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n}
$$where $\mathbb{E}[(X - \mu)^n]$ is the $n$-th central moment of $X$ and $\sigma$ is the standard deviation of $X$, which is the square root of the variance. 

---

#### Zeroth Moment: Total Probability (*Mass*)
$$
\mu_0 = \bar{\mu_n} = \mathbb{E}[(X - \mu)^0] = \mathbb{E}[1] = 1
$$

![image](https://hackmd.io/_uploads/Bk4Qwrzf1x.png)

---

#### First moment: Expectation (Mean) (*Mean position*)
$$
\mu_1 = \mu = \begin{cases} 
\sum_{x} x p(x) \quad \text{ (discrete)} \\
\int_{-\infty}^{\infty} x f(x) dx  \quad \text{ (continuous)}
\end{cases}
$$

![image](https://hackmd.io/_uploads/Sk3WYBGMke.png)

> (a) Normal distribution: $f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$ where mean $\mu = 0.5$ and standard deviation $\sigma = 1$
> (b) Gamma Distribution:$f(x) = \frac{x^{k-1} e^{-x/\theta}}{\theta^k \Gamma(k)}$, where shape parameter$k = 2$, scale parameter $\theta = 0.25$, and mean $k \cdot \theta = 0.5$.


---

#### Second moment: Variance (*Spread*)
$$
\mu_2 = \sigma^2 = \mathbb{E}[(X - \mu)^2] = \int_{-\infty}^{\infty} (x -  \mu)^2 f(x) dx
$$
$$
\text{Standard deviation } \sigma = \sqrt{\mu_2} = \sqrt{\mathbb{E}[(X - \mu)^2]}
$$

![image](https://hackmd.io/_uploads/r1QiYrMMkg.png)

> (a) Normal distribution: $f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$ where mean $\mu = 0.5$ and standard deviation $\sigma = 0.25, 1, 4. $
> (b) Exponential Distribution**: $f(x) = \lambda e^{-\lambda x}$, where rate parameters $\lambda = 1, 2, 4, and variance (displayed in the legend as $\sigma^2$) for each case is $\sigma^2 = 1 / \lambda^2$, which corresponds to $0.0625$, $0.25$, and $1$.

---

#### Third standardized moment: Skewness (*Asymmetry*)
- A skewness of 0 indicates a symmetric distribution.
- A positive skewness indicates a distribution with a longer right tail (right-skewed).
- A negative skewness indicates a distribution with a longer left tail (left-skewed).

$$
\bar{\mu_3} = \frac{\mu_3}{\sigma^3}\frac{\mathbb{E}[(X - \mu)^3]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^3}
$$

![image](https://hackmd.io/_uploads/S1aQz8zGJe.png)

> ##### Discrete Distributions
> * Binomial Distribution: $P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k}$, where $n = 20$ and $p = 0.5$ (Symmetric) and $p=0.9$ (Negatively Skewed).
> * Poisson Distribution (Approximate Positive Skew): $P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$ the probability of a given number of events occurring within a fixed interval, with an average rate of 5 events ($\lambda = 5$).
> 
> ##### Continuous Distributions
> Normal Distribution: $f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$, where $\mu = 0$ and $\sigma = 2$. 
> 
> Skewed Distribution: $f(x) = \frac{2}{\sigma \sqrt{2 \pi}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} \Phi\left(\alpha \frac{x - \mu}{\sigma}\right)$, where $\alpha = 5 or -5$ is the skewness parameter for right-skewed (positively skewed) and left-skewed (negatively skewed), respectively.
> 
> ```python
> positive_skew_dist = stats.skewnorm(a=5, loc=-5, scale=4).pdf(x)
> negative_skew_dist = stats.skewnorm(a=-5, loc=5, scale=4).pdf(x)
> ```
> - **`a`**: controls the skewness of the distribution.
> - **`loc`** and **`scale`**: These are used to shift (center) and stretch (spread) the distribution.

---

**Checkpoint**

##### Why using standardized moment instead of central moment?
:  To compare across different datasets regardless of their scale.
##### Why using standard deviation instead of mean value?
: Normalized by distribution shape instead distribution position.

Moments are not dimensionless—they have units that depend on the power $n$ of the units of $X$. To make moments comparable across different scales and units, we standardize them. The standardized $n^{th}$ moments is obtained by dividing the $n^{th}$ central moment central moment by a normalization factor. 
$$
\bar{\mu_n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n} [=] \frac{X^n}{\sqrt{X^2}^{n}} [=] X^0 \quad \text{dimensionless quantity}
$$Recall that the mean provides a measure of central tendency. It tells us where the center of a distribution is located and based on it we calculate the second moment (how does the distribution spread) and the third moment (how does the distirbution look like). While the mean provides information about the center, it doesn’t directly address the scale of dispersion or how asymmetrically the data are distributed. Therefore, using the standard deviation (which accounts for spread) makes more sense for normalizing moments like skewness and kurtosis.

<p>
  <img src="https://hackmd.io/_uploads/BkeIlyeYC.png", style="width: 70%;"/>
</p>

> This figure demonstrates how scaling affects the spread and raw moments (such as the third central moment) of a distribution without altering its shape or normalized skewness. Recall $\mu_1 = \frac{1}{n} \sum_{i=1}^{n} x_i$, $\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}$, $\mu_{3} = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^3$, and finally $\bar{\mu_3} = \gamma = \frac{\mu_3}{\sigma^3}$.

---

#### Fourth standardized moment: Kurtosis (*Tailedness*) (κυρτός)

*(Too interesting, I may write another note on this.)*

A statistical measure that quantifies textremity of a distribution's tails compared to a normal distribution. Specifically, it assesses the propensity for **extreme values** (極端值) or **outliers** (離群值), reflecting how sharply a distribution peaks and how heavy its tails are. 

$$
\text{Kurtosis } \quad  \bar{\mu_4} = \frac{\mu_4}{\sigma^4}\frac{\mathbb{E}[(X - \mu)^4]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^4}
$$

The kurtosis of a distribution indicates the degree to which it has **heavy tails** and a **sharp peak** relative to a normal distribution. Higher kurtosis means heavier tails and potentially more outliers, while lower kurtosis indicates lighter tails and fewer extreme values.
   
$$
\text{Excess Kurtosis } \quad   \bar{\mu_4}_{excess} =\bar{\mu_4}-3
$$

##### Why Subtract 3?

For a normal distribution, [$\bar{\mu_4} = 3$](#Appendix). This value serves as a reference point for comparing the kurtosis of other distributions. Thus, the kurtosis of a normal distribution is defined as "baseline" or "standard" kurtosis.

- **Excess kurtosis > 0**: The distribution is **leptokurtic (高狹峰)** (has heavier tails than a normal distribution).
- **Excess kurtosis < 0**: The distribution is **platykurtic (低擴峰)** (has lighter tails than a normal distribution).
- **Excess kurtosis = 0**: The distribution is **mesokurtic (常態峰)** (similar tails to a normal distribution).

<p>
  <img src="https://hackmd.io/_uploads/HkCnPbgK0.png", style="width: 70%;"/>
</p>

> * Normal Distribution (Mesokurtic): $f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$
> * Gamma Distribution (Leptokurtic): $f(x) = \frac{(x - \text{loc})^{\alpha - 1} e^{-(x - \text{loc}) / \text{scale}}}{\text{scale}^\alpha \, \Gamma(\alpha)}$, where $\alpha = 2.5$, $\text{loc} = 0$, and $\text{scale} = 1$.
> * Exponential Distribution (Platykurtic):$f(x) = \frac{1}{\text{scale}} e^{-x / \text{scale}}$, where $\text{scale} = 1$


##### Outliers and extreme value

Outliers can skew the mean and standard deviation. Extreme values affect the shape of the data distribution.
![image](https://hackmd.io/_uploads/SkvgFZxY0.png)
[(Source)](https://web.pdx.edu/~stipakb/download/PA551/boxplot.html)

The folloing example demonstrates the impact that outliers can have on a dataset’s statistical measures:
* Mean and variance are sensitive to outliers, as extreme values shift the average and increase spread.
* Skewness is affected by the presence of asymmetrically placed outliers, leading to a leftward skew in this case.
* Kurtosis increases sharply with outliers, reflecting heavier tails and more extreme values.

![image](https://hackmd.io/_uploads/rkf0iwmzkx.png)

---

##### Bound with skewness

A theoretical bound that connects kurtosis and skewness is given by **Pearson’s inequality**, which provides a minimum kurtosis value for a given level of skewness. Specifically, this bound states:
$$
\bar{\mu_4} \geq 1 + \bar{\mu_3}^2
$$

This bound serves as a constraint on the possible values of kurtosis for a given skewness, meaning:

- **Low Skewness**: If skewness is close to zero, indicating a symmetric distribution, then kurtosis must be at least 1. This minimum is consistent with the normal distribution's kurtosis of 3 (or excess kurtosis of 0).
- **High Skewness**: For distributions with high skewness, kurtosis must increase as well, indicating heavier tails or more extreme values to accommodate the asymmetry. This is commonly seen in distributions with high outliers.

![image](https://hackmd.io/_uploads/rJmZ3iQfJl.png)

How to approach to extreme case? (Continue in a separate article)


#### Appendix
---
##### The fourth standardized moment of normal distribution is 3

$\mathbb{E}[Z^4] = \int_{-\infty}^{\infty} z^4 f_Z(z) \, dz$ , where $f_Z(z) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}}$
Thus, we can write:
$$
\mathbb{E}[Z^4] = \int_{-\infty}^{\infty} z^4 \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}} \, dz
$$
Because $Z$ is symmetric around 0,  we can simplify the integral by calculating it only for $z \geq 0$ and then doubling the result:
$$
\mathbb{E}[Z^4] = 2 \int_{0}^{\infty} z^4 \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}} \, dz
$$
Let $u = \frac{z^2}{2}$, so $z^2 = 2u$. Then $z = \sqrt{2u}$, $dz = \frac{1}{\sqrt{2u}} \, du$, and $z^4 = (2u)^2 = 4u^2$.
$$
\mathbb{E}[Z^4] = 2 \int_{0}^{\infty} 4u^2 \frac{1}{\sqrt{2 \pi}} e^{-u} \cdot \frac{1}{\sqrt{2u}} \, du = \frac{4}{\sqrt{2 \pi}} \int_{0}^{\infty} u^{3/2} e^{-u} \, du
$$
The integral $\int_{0}^{\infty} u^{3/2} e^{-u} \, du$ is a form of the **gamma function** $\int_{0}^{\infty} u^{k-1} e^{-u} \, du = \Gamma(k)$, so that
$$
\int_{0}^{\infty} u^{3/2} e^{-u} \, du = \Gamma\left(\frac{5}{2}\right) = \frac{3 \sqrt{\pi}}{4}
$$
Substitue back we get, 
$$
\mathbb{E}[Z^4] = \frac{4}{\sqrt{2 \pi}} \cdot \frac{3 \sqrt{\pi}}{4} = 3
$$

#### Reference
---

https://cs229.stanford.edu/section/cs229-prob.pdf
https://gregorygundersen.com/blog/2020/04/11/moments/
https://www.itl.nist.gov/div898/handbook/eda/section3/eda35b.htm