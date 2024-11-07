---
title: Brief Review of Probability
summary: A brief overview of fundamental probability concepts, together with visualization practice. Advanced topics are still under construction.
date: 2024-07-01
authors: L. H. Huang
tags: ["Study Notes", "Physics"]
features:
  math:
    enable: true
---

# Probability Basics

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
\begin{align}
    P(X = x)
\end{align}

- A discrete random variable $X$ gives the probability that $X$ takes on a specific value $x$
- Examples: Bernoulli distribution, Binomial distribution, and Geometric distribution

#### Cumulative Distribution Functions (CDF)
\begin{align}
    F_X(x) = P(X \leq x)
\end{align}

- The accumulated probability up to $x$ that the random variable $X$ can achieve. It provides a complete picture of the distribution of $X$ from $-\infty$ to $\infty$.
- Properties
    1. Non-decreasing: $F_X(x_1) \leq F_X(x_2)$ if $x_1 \leq x_2$.
    2. Limits: $\lim_{x \to -\infty} F_X(x) = 0$; $\lim_{x \to \infty} F_X(x) = 1$
    3. Right-Continuity: $\lim_{h \to 0^+} F_X(x + h) = F_X(x)$.

#### Probability Density Functions (PDF)
\begin{align}
    &f_X(a \leq x \leq b)=\int_a^b f_X(x) dx \\
    &\int_{-\infty}^{\infty} f_X(x) dx = 1
\end{align}

- A continuous random variable $X$, denoted as $f_X(x)$, is a function that describes the relative likelihood of $X$ taking on a specific value $x$.

**Example 1:**
Fair Six-Sided Die (Discrete Random Variable)

![image](https://hackmd.io/_uploads/H1VQznL_0.png)


<details>  
<summary>Script Achive</summary>

```
import numpy as np
import matplotlib.pyplot as plt

x_values = np.arange(1, 7)
pmf_values = np.ones(6) / 6
cdf_values = np.cumsum(pmf_values)

plt.figure(figsize=(5.5, 4))

plt.subplot(1, 1, 1)
plt.bar(x_values, pmf_values, width=0.5, label='PMF', alpha=0.5) 
plt.title('Fair six-sided die')
plt.xlabel('Outcome')
plt.ylabel('Probability (PMF)')
plt.legend(loc='upper left')
plt.xticks(x_values)
plt.xlim(0.5, 6.5)
plt.yticks(np.arange(0, 1.1, 1/6), ['0', '1/6', '2/6', '3/6', '4/6', '5/6', '1']) 

plt.twinx()
plt.step(np.concatenate([[0], x_values]), np.concatenate([[0], cdf_values]), where='post', color='orange', label='CDF')
plt.ylabel('Cumulative Probability (CDF)')
plt.yticks(np.arange(0, 1.1, 1/6), ['0', '1/6', '2/6', '3/6', '4/6', '5/6', '1']) 
plt.ylim(0, 1.1)
plt.legend(loc='upper right')

plt.tight_layout()
plt.show()
```

</details>

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

![image](https://hackmd.io/_uploads/Hybq428OA.png)

<details>  
<summary>Script Achive</summary>

```
import numpy as np
import matplotlib.pyplot as plt

lam = 0.5
x = np.linspace(0, 10, 1000)
pdf = lam * np.exp(-lam * x)
cdf = 1 - np.exp(-lam * x)


fig, ax1 = plt.subplots(figsize=(5.5, 4))
ax1.set_xlabel('x')
ax1.set_ylabel('Probability Density Function (PDF)')
ax1.plot(x, pdf, label='PDF')

ax2 = ax1.twinx()
ax2.set_ylabel('Cumulative Probability (CDF)')
ax2.plot(x, cdf, color='red', label='CDF')

plt.title('Exponential Distribution: PDF and CDF')
fig.legend(loc='center')
fig.tight_layout()
plt.show()
```

</details>

# What is moment?

When I looked back to review some basic concepts of probability theory, I found it is difficult to understand the terms "**Moment**". In physics, moments refer to quantities like moments of inertia and dipole moments, while in statistics, moments relate to measures like expectation and variance. But why is it called a moment?

## Why "moment"?

I first asked ChatGPT: Why are distribution's moments called "moments"? And it gave me a rather general explanation: 
> The term "moments" in the context of statistics is **derived from the concept of moments in physics**, particularly the moments of inertia. Just as physical moments describe **the distribution of mass around a point or axis**, statistical moments describe **the distribution  of probability around a central value**. 

Ok now I know the terms "moment" in statistics is borrowed from physics and it somehow describes distribution (?). Wait a moment! Why is it called "moment" in Physics? Why this word "moment"? Clearly I am not the only one having this question[$^{1}$](https://gregorygundersen.com/blog/2020/04/11/moments/)[$^{, 2}$](https://stats.stackexchange.com/questions/17595/whats-so-moment-about-moments-of-a-probability-distribution)[$^{, 3}$](https://www.ptt.cc/bbs/Statistics/M.1639188552.A.309.html). In [$\text{Ref 1}$](https://gregorygundersen.com/blog/2020/04/11/moments/), the author started with the same question and wrote a very interesting discussion on it. Here I quote the first paragraph: 

> ...According to Wiktionary, the words “moment” and “momentum” are doublets or etymological twins, meaning that they are two words in a language with the same etymological root. Both come from the Latin word “**movimentum**,” meaning to move, set in motion, or change. Today, a “moment” often refers to an instant in time, but we can guess at the connection to movement. For example, we might say things like, “It was a momentous occasion,” or, “The game was her big moment.” In both cases, the notion of **time and change are intertwined**.

According to [wikitionery](https://en.wiktionary.org/wiki/moment), moment in mathematics means:
* An infinitesimal **change** in a varying quantity; an increment or decrement.
* A **quantitative measure** of the shape of a set of points

The second moment in physics, known as the moment of inertia, measures the distribution of mass around an axis and its resistance to rotational acceleration. This concept of mass distribution is likely why the term "moment" is used in statistics to describe probability distributions. I think it is more clear to understand through formal mathematical equations, listed in the table below. 

## Comparison 

| Moment      | Physics Concept              | Formula in Physics                       | Statistics Concept         | Formula in Statistics                                            |
|-------------|------------------------------|------------------------------------------|----------------------------|------------------------------------------------------------------|
| Zeroth      | Total Mass                   | $M = \int dm$                     | Total Probability          | $\int_{-\infty}^{\infty} f_X(x) dx = 1$                   |
| First       | Center of Mass               | $\bar{x} = \frac{1}{M} \int x_i dm$ | Mean         | $\int_{-\infty}^{\infty} (x-\mu) f_X(x) dx$     |
| Second      | Moment of Inertia            | $I = \int (x_i-\bar{x})^2 dm$                 | Variance                   | $\int_{-\infty}^{\infty} (x-\mu)^2 f_X(x) dx$                    |

The zeroth moment describes the entirety of the quantity (total mass vs. total probability). The first moment describes the average (mean position vs. mean value). The second moment describes the distribution shape (moment of inertia vs. variance), detailing how the object is shaped and how the distribution spreads.

## Further confusion 矩vs動差

Before going to next section, I would like to address the translation of "moment" in Mandarin. Unlike in English, where the term "moment" is used in both physics and statistics, there are two different translations: 矩 for physics and 動差 for statistics.

> * **矩**：方形; 直角曲尺; 法則、常規。
> Refers to a square; a right-angle ruler; principles or conventions.
> * **力矩**：力的垂直分量的大小與力的作用線距決定力所圍繞的點的距離的外積
> Moment of force: The product of the magnitude of the perpendicular component of the force and the distance of the line of action of a force from the point around which it is being determined.
> * **轉動慣量**：物體對於其旋轉運動的慣性大小的量度; 轉動慣量決定對於這物體繞著這轉軸進行某種角加速度運動所需要施加的力矩
> Moment of inertia: A measure of an object's inertia regarding its rotational motion; the moment of inertia determines the torque needed to achieve a certain angular acceleration around the axis.
> * **電偶極矩**：正電荷分佈與負電荷分佈的分離狀況，即電荷系統的整體極性
> Electric dipole moment: The separation of positive and negative charge distributions, i.e., the overall polarity of the charge system.

From the above translations, it is evident that "矩" originally referred to geometric shapes or right angles. When translating "moment of force," it was possibly chosen to describe the perpendicular component of the force in relation to the axis, following the "right-hand rule." The translation of other physical terms is not consistent, but generally describes a "measure" or "scale" used to *quantify* the distribution of a physical quantity— like directly using "慣量" for the moment of inertia. 

For "力矩," the term "動差" seems to better describe the moment of force. "動差" literally includes "動" (movement, rotation, change) and "差" (difference, distance), which aligns well with the definition of moment: the force causing rotation multiplied by the distance to the axis of rotation. 

The etymology of the translation is unclear, but a post on a [BBS](https://www.ptt.cc/bbs/Statistics/M.1639188552.A.309.html)  reflects similar confusion, with comments suggesting that `reading the original English text rather than relying on Chinese translations`. I might have agreed with this perspective few years ago, but the confusion surrounding this terminology is not entirely a translation issue. But translation does bring more confusion.


# Moments of Distributions

## Definitions
The $n^{th}$ moment is defined as 

\begin{align}
\mathbb{E}[(X - c)^n] = \int_{-\infty}^{\infty} (x - c)^n f(x) \, dx
\end{align}

- When $c = 0$: This formula simplifies to the **$n^{th}$ raw moment**, providing information about the shape of the distribution relative to the origin (zero)
\begin{align}
\mathbb{E}[X^n] = \int_{-\infty}^{\infty} x^n f(x) dx
\end{align}

- When $c = \mu$: The mean $\mu$ of $X$, the formula gives the **$n^{th}$ central moment**, prioviding information about the shape of the distribution relative to its mean. 
\begin{align}
\mu_n =\mathbb{E}[(X -  \mu)^n] = \int_{-\infty}^{\infty} (x -  \mu)^n f(x) dx
\end{align} Central moments provide information about the shape of the distribution relative to its mean. 

**Standardized moments**: a dimensionless form to express moments of a probability distribution and provide a way to compare distributions with different scales. Usually for higher order of moment.
\begin{align}
\bar{\mu_n} = \frac{\mu_n}{\sigma^n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n}
\end{align} where $\mathbb{E}[(X - \mu)^n]$ is the $n$-th central moment of $X$ and $\sigma$ is the standard deviation of $X$, which is the square root of the variance. 

### $0^{th} \text{ moment}$: Total Probability (*Mass*)
\begin{align}
\mu_0 = \bar{\mu_n} = \mathbb{E}[(X - \mu)^0] = \mathbb{E}[1] = 1
\end{align} 


![image](https://hackmd.io/_uploads/H140o86d0.png)

### $1^{st} \text{ moment}$: Expectation (Mean) (*Mean position*)
\begin{align}
\mu_1 = \mu = \begin{cases} 
\sum_{x} x p(x) \quad \text{ (discrete)} \\
\int_{-\infty}^{\infty} x f(x) dx  \quad \text{ (continuous)}
\end{cases}
\end{align} 

![image](https://hackmd.io/_uploads/SyO_60JtR.png)


### $2^{nd} \text{ moment}$: Variance (*Spread*)
\begin{align}
\mu_2 = \sigma^2 = \mathbb{E}[(X - \mu)^2] = \int_{-\infty}^{\infty} (x -  \mu)^2 f(x) dx \\
\text{Standard deviation } \sigma = \sqrt{\mu_2} = \sqrt{\mathbb{E}[(X - \mu)^2]}
\end{align} 

![image](https://hackmd.io/_uploads/SJ-opAkFA.png)

### $3^{rd} \text{ standardized moment}$: Skewness (*Asymmetry*)
    - A skewness of 0 indicates a symmetric distribution.
    - A positive skewness indicates a distribution with a longer right tail (right-skewed).
    - A negative skewness indicates a distribution with a longer left tail (left-skewed).

\begin{align}
\bar{\mu_3} = \frac{\mu_3}{\sigma^3}\frac{\mathbb{E}[(X - \mu)^3]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^3}
\end{align} 

![image](https://hackmd.io/_uploads/SyEfpAJK0.png)

**Checkpoint**
**Why using standardized moment instead of central moment?**
:  To compare across different datasets regardless of their scale.
**Why using standard deviation instead of mean value?**
: Normalized by distribution shape instead distribution position.

Moments are not dimensionless—they have units that depend on the power $n$ of the units of $X$. To make moments comparable across different scales and units, we standardize them. The standardized $n^{th}$ moments is obtained by dividing the $n^{th}$ central moment central moment by a normalization factor. 
\begin{align}
\bar{\mu_n} = \frac{\mathbb{E}[(X - \mu)^n]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^n} [=] \frac{X^n}{\sqrt{X^2}^{n}} [=] X^0 \quad \text{dimensionless quantity}
\end{align} Recall that the mean provides a measure of central tendency. It tells us where the center of a distribution is located and based on it we calculate the second moment (how does the distribution spread) and the third moment (how does the distirbution look like). While the mean provides information about the center, it doesn’t directly address the scale of dispersion or how asymmetrically the data are distributed. Therefore, using the standard deviation (which accounts for spread) makes more sense for normalizing moments like skewness and kurtosis.

<p>
  <img src="https://hackmd.io/_uploads/BkeIlyeYC.png", style="width: 70%;"/>
</p>


### $4^{th} \text{ standardized moment}$: Kurtosis (*Tailedness*) (κυρτός)

(Too interesting)

A statistical measure that quantifies textremity of a distribution's tails compared to a normal distribution. Specifically, it assesses the propensity for extreme values (極端值) or **outliers**(離群值), reflecting how sharply a distribution peaks and how heavy its tails are. 

\begin{align}
\text{Kurtosis } \quad & \bar{\mu_4} = \frac{\mu_4}{\sigma^4}\frac{\mathbb{E}[(X - \mu)^4]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^4} \\
\text{Excess Kurtosis } \quad  & \bar{\mu_4}_{excess} =\bar{\mu_4}-3
\end{align} 

<p>
  <img src="https://hackmd.io/_uploads/HkCnPbgK0.png", style="width: 70%;"/>
</p>

#### Outliers and extreme value

Outliers can skew the mean and standard deviation. Extreme values affect the shape of the data distribution.
![image](https://hackmd.io/_uploads/SkvgFZxY0.png)
[(Source)](https://web.pdx.edu/~stipakb/download/PA551/boxplot.html)

#### Bound with skewness

A theoretical bound connecting kurtosis and skewness is given by:

how to approach to extreme case?

4. normal distribution
5. Excess Kurtosis 
6. Maximum entropy
7. Limitations of Kurtosis
8. Comparison with 4th cumulant 

## Cumulants
## Moment-Generating and Characteristic Functions
### Moment-Generating Function**
  - Definition
  - Properties
### Characteristic Function**
  - Definition
  - Properties

## Some Distributions 

### Basic Discrete Distributions:
- Bernoulli
- Geometric
- Binomial Distribution
- Poisson Distribution

### Basic Continuous Distributions:
- Uniform
- Exponential
- Normal Distribution

### Specialized Continuous Distributions:
- Laplace distribution
- Cauchy distribution
- Rayleigh Distribution
- Gumbel Distribution

### Advanced Continuous Distributions:
- Weibull Distribution
- Gamma Distribution
- Beta Distribution
- Chi-Squared Distribution
- Error Function (erf)

### Physics and Statistical Mechanics Distributions:
- Gibbs distribution
- Boltzmann Distribution
- Maxwell-Boltzmann Distribution
- Fermi-Dirac Distribution

### Tailored and Complex Distributions:
- Exponential-Logarithmic Distribution
- Pareto distribution
- Power Law Distribution

## Multivariate Distributions
- **Joint Distributions**
  - Joint Probability Mass Functions (Discrete)
  - Joint Probability Density Functions (Continuous)
  - Joint Cumulative Distribution Functions
- **Marginal Distributions**
  - Marginal Probability Mass Functions
  - Marginal Probability Density Functions
  - Marginal Cumulative Distribution Functions

### Specific Multivariate Distributions
- **Multivariate Normal Distribution**
  - Definition
  - Properties
- **Matrix Normal Distribution**
  - Definition
  - Properties

Reference
---


https://cs229.stanford.edu/section/cs229-prob.pdf
https://gregorygundersen.com/blog/2020/04/11/moments/
https://www.itl.nist.gov/div898/handbook/eda/section3/eda35b.htm
