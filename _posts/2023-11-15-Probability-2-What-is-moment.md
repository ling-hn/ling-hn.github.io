---
layout: post
title: Revisit Probability - What is "Moment"?
description: When I looked back to review some basic concepts of probability theory, I found it is difficult to understand the term "Moment".
date: 2023-11-15
author: L. H. Huang
tags: ["Study Notes", "Physics"]
features:
  math:
    enable: true
---

When I looked back to review some basic concepts of probability theory, I found it is difficult to understand the terms "**Moment**". In physics, moments refer to quantities like moments of inertia and dipole moments, while in statistics, moments relate to measures like expectation and variance. But why is it called a moment?

#### Why "moment"?

I first asked ChatGPT: Why are distribution's moments called "moments"? And it gave me a rather general explanation: 
> The term "moments" in the context of statistics is **derived from the concept of moments in physics**, particularly the moments of inertia. Just as physical moments describe **the distribution of mass around a point or axis**, statistical moments describe **the distribution  of probability around a central value**. 

Ok now I know the terms "moment" in statistics is borrowed from physics and it somehow describes distribution (?). Wait a moment! Why is it called "moment" in Physics? Why this word "moment"? Clearly I am not the only one having this question.[^1][^2][^3] In Ref 1, the author started with the same question and wrote a very interesting discussion on it. Here I quote the first paragraph: 

> ...According to Wiktionary, the words “moment” and “momentum” are doublets or etymological twins, meaning that they are two words in a language with the same etymological root. Both come from the Latin word “**movimentum**,” meaning to move, set in motion, or change. Today, a “moment” often refers to an instant in time, but we can guess at the connection to movement. For example, we might say things like, “It was a momentous occasion,” or, “The game was her big moment.” In both cases, the notion of **time and change are intertwined**.

According to [wikitionery](https://en.wiktionary.org/wiki/moment), moment in mathematics means:
* An infinitesimal **change** in a varying quantity; an increment or decrement.
* A **quantitative measure** of the shape of a set of points

The second moment in physics, known as the moment of inertia, measures the distribution of mass around an axis and its resistance to rotational acceleration. This concept of mass distribution is likely why the term "moment" is used in statistics to describe probability distributions. I think it is more clear to understand through formal mathematical equations, listed in the table below. 

#### Comparison 

| Moment      | Physics Concept              | Formula in Physics                       | Statistics Concept         | Formula in Statistics                                            |
|-------------|------------------------------|------------------------------------------|----------------------------|------------------------------------------------------------------|
| Zeroth      | Total Mass                   | $$M = \int dm$$                     | Total Probability          | $$\int_{-\infty}^{\infty} f_X(x) dx = 1$$                   |
| First       | Center of Mass               | $$\bar{x} = \frac{1}{M} \int x_i dm$$ | Mean         | $$\int_{-\infty}^{\infty} (x-\mu) f_X(x) dx$$     |
| Second      | Moment of Inertia            | $$I = \int (x_i-\bar{x})^2 dm$$                 | Variance                   | $$\int_{-\infty}^{\infty} (x-\mu)^2 f_X(x) dx$$                    |

The zeroth moment describes the entirety of the quantity (total mass vs. total probability). The first moment describes the average (mean position vs. mean value). The second moment describes the distribution shape (moment of inertia vs. variance), detailing how the object is shaped and how the distribution spreads.

#### Further confusion 矩vs動差

Before closing the discussion, I would like to address the translation of "moment" in Mandarin. Unlike in English, where the term "moment" is used in both physics and statistics, there are two different translations: 矩 for physics and 動差 for statistics.

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

The etymology of the translation is unclear, but a post on a [BBS](https://www.ptt.cc/bbs/Statistics/M.1639188552.A.309.html)  reflects similar confusion, with comments suggesting that *reading the original English text rather than relying on Chinese translations*. I might have agreed with this perspective few years ago, but the confusion surrounding this terminology is not entirely a translation issue. But translation does bring more confusion.


#### Reference

[^1]: https://gregorygundersen.com/blog/2020/04/11/moments/
[^2]:https://stats.stackexchange.com/questions/17595/whats-so-moment-about-moments-of-a-probability-distribution
[^3]: https://www.ptt.cc/bbs/Statistics/M.1639188552.A.309.html