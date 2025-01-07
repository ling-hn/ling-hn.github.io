---
layout: post
title: Revisit Probability - Understanding Kurtosis (κυρτός)
description: Kurtosis, the fourth standardized moment in statistics.
date: 2024-07-01
author: L. H. Huang
tags: ["Study Notes", "Physics"]
features:
  math:
    enable: true
---

#### Definition
A statistical measure that quantifies textremity of a distribution's tails compared to a normal distribution. Specifically, it assesses the propensity for **extreme values** (極端值) or **outliers** (離群值), reflecting how sharply a distribution peaks and how heavy its tails are. 

$$
\text{Kurtosis } \quad  \bar{\mu_4} = \frac{\mu_4}{\sigma^4}\frac{\mathbb{E}[(X - \mu)^4]}{\left(\sqrt{\mathbb{E}[(X - \mu)^2]} \right)^4}
$$

The kurtosis of a distribution indicates the degree to which it has **heavy tails** and a **sharp peak** relative to a normal distribution. Higher kurtosis means heavier tails and potentially more outliers, while lower kurtosis indicates lighter tails and fewer extreme values.
   
$$
\text{Excess Kurtosis } \quad   \bar{\mu_4}_{excess} =\bar{\mu_4}-3
$$

#### Why Subtract 3?

For a normal distribution, $\bar{\mu_4} = 3$. This value serves as a reference point for comparing the kurtosis of other distributions. Thus, the kurtosis of a normal distribution is defined as "baseline" or "standard" kurtosis.

**The fourth standardized moment of normal distribution is 3.**

$$\mathbb{E}[Z^4] = \int_{-\infty}^{\infty} z^4 f_Z(z) \, dz$$ , where $$f_Z(z) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}}$$

Thus, we can write:

$$
\mathbb{E}[Z^4] = \int_{-\infty}^{\infty} z^4 \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}} \, dz
$$

Because $$Z$$ is symmetric around 0,  we can simplify the integral by calculating it only for $$z \geq 0$$ and then doubling the result:

$$
\mathbb{E}[Z^4] = 2 \int_{0}^{\infty} z^4 \frac{1}{\sqrt{2 \pi}} e^{-\frac{z^2}{2}} \, dz
$$

Let $$u = \frac{z^2}{2}$$, so $$z^2 = 2u$. Then $$z = \sqrt{2u}$$, $$dz = \frac{1}{\sqrt{2u}} \, du$$, and $$z^4 = (2u)^2 = 4u^2$$.

$$
\mathbb{E}[Z^4] = 2 \int_{0}^{\infty} 4u^2 \frac{1}{\sqrt{2 \pi}} e^{-u} \cdot \frac{1}{\sqrt{2u}} \, du = \frac{4}{\sqrt{2 \pi}} \int_{0}^{\infty} u^{3/2} e^{-u} \, du
$$

The integral $$\int_{0}^{\infty} u^{3/2} e^{-u} \, du$$ is a form of the **gamma function** $$\int_{0}^{\infty} u^{k-1} e^{-u} \, du = \Gamma(k)$$, so that

$$
\int_{0}^{\infty} u^{3/2} e^{-u} \, du = \Gamma\left(\frac{5}{2}\right) = \frac{3 \sqrt{\pi}}{4}
$$

Substitue back we get, 

$$
\mathbb{E}[Z^4] = \frac{4}{\sqrt{2 \pi}} \cdot \frac{3 \sqrt{\pi}}{4} = 3
$$

$$
\quad
$$

---

$$
\quad
$$

#### Kurtosis in the Context of Distribution Types

- **Excess kurtosis > 0**: The distribution is **leptokurtic (高狹峰)** (has heavier tails than a normal distribution).
- **Excess kurtosis < 0**: The distribution is **platykurtic (低擴峰)** (has lighter tails than a normal distribution).
- **Excess kurtosis = 0**: The distribution is **mesokurtic (常態峰)** (similar tails to a normal distribution).

![image](https://hackmd.io/_uploads/HkCnPbgK0.png)

> * Normal Distribution (Mesokurtic): $$f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$$
> * Gamma Distribution (Leptokurtic): $$f(x) = \frac{(x - \text{loc})^{\alpha - 1} e^{-(x - \text{loc}) / \text{scale}}}{\text{scale}^\alpha \, \Gamma(\alpha)}$$, where $$\alpha = 2.5$, $\text{loc} = 0$, and $\text{scale} = 1$$.
> * Exponential Distribution (Platykurtic):$$f(x) = \frac{1}{\text{scale}} e^{-x / \text{scale}}$$, where $$\text{scale} = 1$$

#### Outliers and extreme value

Outliers can skew the mean and standard deviation. Extreme values affect the shape of the data distribution.
![image](https://hackmd.io/_uploads/SkvgFZxY0.png)
[(Source)](https://web.pdx.edu/~stipakb/download/PA551/boxplot.html)

The folloing example demonstrates the impact that outliers can have on a dataset’s statistical measures:
* Mean and variance are sensitive to outliers, as extreme values shift the average and increase spread.
* Skewness is affected by the presence of asymmetrically placed outliers, leading to a leftward skew in this case.
* Kurtosis increases sharply with outliers, reflecting heavier tails and more extreme values.

![image](https://hackmd.io/_uploads/rkf0iwmzkx.png)

#### Bound with skewness

A theoretical bound that connects kurtosis and skewness is given by **Pearson’s inequality**, which provides a minimum kurtosis value for a given level of skewness. Specifically, this bound states:
$$
\bar{\mu_4} \geq 1 + \bar{\mu_3}^2
$$

This bound serves as a constraint on the possible values of kurtosis for a given skewness, meaning:

- **Low Skewness**: If skewness is close to zero, indicating a symmetric distribution, then kurtosis must be at least 1. This minimum is consistent with the normal distribution's kurtosis of 3 (or excess kurtosis of 0).
- **High Skewness**: For distributions with high skewness, kurtosis must increase as well, indicating heavier tails or more extreme values to accommodate the asymmetry. This is commonly seen in distributions with high outliers.

![image](https://hackmd.io/_uploads/rJmZ3iQfJl.png)


$$
\quad
$$

#### Probability Plot

A **P–P plot** (Probability–Probability plot) is used to compare two cumulative distribution functions (CDFs), $$F(z)$$ and $$G(z)$$, by plotting their values against each other as the variable $z$ ranges from $$-\infty$$ to $$+\infty$$. This plot helps to assess how closely two distributions match, or to visually assess whether a dataset follows a specific distribution (e.g., normal, exponential, etc.).

Take the above sample for example, let the one without outlier be $$F(z)$$ (In this case, normal distribution) and the other with outlier be $$G(z)$$. We calculate the CDF of both $$F(z)$$ and $$G(z)$$ with proper range of $$z$$ values over the domain of the data ([$$-\infty$$, $$+\infty$$] or [$${X}_{min}$$, $${X}_{max}$$]). The CDF always lies in the range $$[0, 1]$$. For each $$z$$, the P-P plot plots the pair $$(F(z), G(z))$$ and a 45° line for comparison, $$(F(z)= G(z))$$.

![image](https://hackmd.io/_uploads/r1R-6zcz1e.png)

**Common Types of P-P Plots**

| Distribution  | **PDF**  | **CDF** |
|-----|-----|-----|
| Normal | $$f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}$$                                                                      | $$F(x) = \frac{1}{2} \left[ 1 + \text{erf} \left( \frac{x - \mu}{\sqrt{2}\sigma} \right) \right]$$              |
| Exponential | $$f(x) = \lambda e^{-\lambda x}$$                                                                                                              | $$F(x) = 1 - e^{-\lambda x}$$                                                                                  |
| Weibull  | $$f(x) = \frac{c}{\lambda} \left( \frac{x}{\lambda} \right)^{c-1} e^{-\left( \frac{x}{\lambda} \right)^c}$$                                          | $$F(x) = 1 - e^{-\left( \frac{x}{\lambda} \right)^c}$$                                                         |

![image](https://hackmd.io/_uploads/S1y4fQ5zyg.png)

> (1) Empirical distributions is created by `numpy` using 1,000 random sampling. Ex. `data_normal = np.random.normal(loc=0, scale=1, size=1000)`
> (2) Theoretical distributions is created from `scipy.stats` by (`norm`, `expon`,`weibull_min(1.5)`) . 

**Case Studies**


![image](https://hackmd.io/_uploads/rJgOa79Mkg.png)

|  | Skewness | Kurtosis |
| -------- | -------- | -------- |
| Case 1: Normal    | 0.12     | 0.07     |
| Case 2: Right-skewed ( Concave upward )     | 0.07     | 0.61    |
| Case 3: Left-skewed (Concave downward)     | -0.72     | 0.18     |
| Case 4: Heavy tails (leptokurtic)     | 1.64     | 34.43     |
| Case 5: Light tails (platykurtic)     | -0.03     |-1.19     |
| Case 6: Outliers     |-2.83    | 71.64     |


$$
\quad
$$

#### Quantile-Quantile Plot

Both P-P (Probability-Probability) plots and Q-Q (Quantile-Quantile) plots are graphical tools for assessing how closely a dataset matches a theoretical distribution or how two distributions compare. While P-P plots compare cumulative probabilities (CDFs), Q-Q plots compare quantiles. 

**Quantile (分位數)**
A quantile is a cutoff value such that a given percentage of the data lies below it. For example: The $$50^{\text{th}}$$ quantile (median) is the value below which 50% of the data lies.

To plot QQ-plot, first we sort the $$n$$ data points: $$x_1, x_2, \ldots, x_n$$ in ascending order: $$x_{(1)} \leq x_{(2)} \leq \ldots \leq x_{(n)}$$. These are the **empirical quantiles**. Then assign a cumulative probability $$p_i$$ to each data point: $$p_i = \frac{i - 0.5}{n}, \quad i = 1, 2, \ldots, n$$. For the same cumulative probabilities $$p_i$$, compute the **theoretical quantiles** from the specified theoretical distribution using its inverse CDF: $$Q_i^{\text{theoretical}} = F_{\text{theoretical}}^{-1}(p_i)$$. Finally pair quantiles: For each $$i$$, create a pair of points $$(Q_i^{\text{theoretical}}, x_{(i)})$$. These pairs will form the Q-Q plot.

By Python, this can be calculated directly by `from scipy.stats import probplot` 

![image](https://hackmd.io/_uploads/HkXloEcfJe.png)


$$
\quad
$$

#### Advanced Concepts Related to Kurtosis (To be continued)

   - **Maximum Entropy Principle**:
       The **Maximum Entropy Principle** provides a theoretical foundation for why the normal distribution is often assumed in many real-world applications, as it represents the most unbiased distribution given limited information. However, **kurtosis** reveals how data deviates from this assumption, especially in terms of tail behavior and the likelihood of extreme values. Understanding these deviations helps analysts identify underlying factors that influence the data, and adjust models accordingly to capture the full range of outcomes, especially in scenarios involving high risk or uncertainty.
       
   - **The 4th Cumulant**:
       The 4th cumulant, $$\kappa_4$$, isolates the excess kurtosis of a distribution, offering a clear measure of how its shape deviates from normality. While the 4th moment provides a general view of tails and peak, the cumulant refines this understanding by focusing on intrinsic distribution characteristics. This makes the 4th cumulant a valuable tool in areas like statistical testing, model validation, and risk analysis.
