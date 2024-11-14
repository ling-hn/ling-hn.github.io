---
title: Understanding Kurtosis and Its Implications
summary: 
date: 2023-11-30
authors: L. H. Huang
tags: ["Study Notes", "Physics"]
features:
  math:
    enable: true
---

## Fourth standardized moment: Kurtosis (κυρτός)

### Definition
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

#### The fourth standardized moment of normal distribution is 3

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

---

### Kurtosis in the Context of Distribution Types

- **Excess kurtosis > 0**: The distribution is **leptokurtic (高狹峰)** (has heavier tails than a normal distribution).
- **Excess kurtosis < 0**: The distribution is **platykurtic (低擴峰)** (has lighter tails than a normal distribution).
- **Excess kurtosis = 0**: The distribution is **mesokurtic (常態峰)** (similar tails to a normal distribution).

<p>
  <img src="https://hackmd.io/_uploads/HkCnPbgK0.png", style="width: 70%;"/>
</p>

> * Normal Distribution (Mesokurtic): $f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(x - \mu)^2}{2 \sigma^2}}$
> * Gamma Distribution (Leptokurtic): $f(x) = \frac{(x - \text{loc})^{\alpha - 1} e^{-(x - \text{loc}) / \text{scale}}}{\text{scale}^\alpha \, \Gamma(\alpha)}$, where $\alpha = 2.5$, $\text{loc} = 0$, and $\text{scale} = 1$.
> * Exponential Distribution (Platykurtic):$f(x) = \frac{1}{\text{scale}} e^{-x / \text{scale}}$, where $\text{scale} = 1$

---

### Outliers and extreme value

Outliers can skew the mean and standard deviation. Extreme values affect the shape of the data distribution.
![image](https://hackmd.io/_uploads/SkvgFZxY0.png)
[(Source)](https://web.pdx.edu/~stipakb/download/PA551/boxplot.html)

The folloing example demonstrates the impact that outliers can have on a dataset’s statistical measures:
* Mean and variance are sensitive to outliers, as extreme values shift the average and increase spread.
* Skewness is affected by the presence of asymmetrically placed outliers, leading to a leftward skew in this case.
* Kurtosis increases sharply with outliers, reflecting heavier tails and more extreme values.

![image](https://hackmd.io/_uploads/rkf0iwmzkx.png)

---

### Bound with skewness

A theoretical bound that connects kurtosis and skewness is given by **Pearson’s inequality**, which provides a minimum kurtosis value for a given level of skewness. Specifically, this bound states:
$$
\bar{\mu_4} \geq 1 + \bar{\mu_3}^2
$$

This bound serves as a constraint on the possible values of kurtosis for a given skewness, meaning:

- **Low Skewness**: If skewness is close to zero, indicating a symmetric distribution, then kurtosis must be at least 1. This minimum is consistent with the normal distribution's kurtosis of 3 (or excess kurtosis of 0).
- **High Skewness**: For distributions with high skewness, kurtosis must increase as well, indicating heavier tails or more extreme values to accommodate the asymmetry. This is commonly seen in distributions with high outliers.

![image](https://hackmd.io/_uploads/rJmZ3iQfJl.png)

### Practical Analysis of Kurtosis
   - **Visualizing Kurtosis**: 
       - Q-Q plots, histograms, and other visualization methods to complement kurtosis analysis.
   - **Calculating Kurtosis in Python**: 
       - Code snippets using libraries like SciPy or Pandas for calculating and interpreting kurtosis.
   - **Considerations in High-Kurtosis and Low-Kurtosis Data**: How outliers and data quality impact kurtosis measurements and interpretation.

### Advanced Concepts Related to Kurtosis
   - **Maximum Entropy Principle**:
       - Explanation of maximum entropy and how the normal distribution achieves it under certain conditions.
       - Relevance of maximum entropy in real-world data, where deviations often signal processes that affect tail heaviness.
   - **The 4th Cumulant**:
       - Difference between moments and cumulants.
       - How the 4th cumulant relates to kurtosis and provides insights into the underlying distribution shape.

### Limitations of Kurtosis in Practice
   - **Data Anomalies and Outliers**: Understanding when kurtosis reflects actual data characteristics versus when it may be distorted by anomalies.
   - **Dependency on Context**: Recognizing that kurtosis alone doesn’t tell the full story and should be used alongside other metrics for a complete analysis.

### Practical Applications and Case Studies
   - **Financial Risk Analysis**: Using kurtosis to assess tail risk and the likelihood of extreme market movements.
   - **Quality Control and Engineering**: Application of kurtosis in detecting deviations in production processes or product measurements.
   - **Environmental and Social Sciences**: Evaluating kurtosis in datasets with inherently skewed or tailed distributions (e.g., income distribution, pollution levels).

