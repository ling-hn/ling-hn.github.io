---
layout: post
title: Fractal Dimension
description: From regular fractal to polymer as random fractals
date: 2023-06-01
author: L. H. Huang
tags: ["Study Notes", "Physics", "Python"]
features:
  math:
    enable: true
---

* **Fractal**: Self-similar. A geometric shape containing detailed structure at arbitrarily small scales, usually having a fractal dimension strictly exceeding the topological dimension.

* **Fractal dimension**: An index for characterizing fractal patterns or sets by quantifying their complexity as a ratio of the change in detail to the change in scale.

$$
N = r^D 
$$

$$
D = \frac{\log N}{\log r}
$$

$$
\begin{align}
 N &\text{: Number of miniature pieces in the final figure}\\
 r &\text{: Scaling factor}\\
 D &\text{: Fractal dimension}
\end{align}
$$

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/rk1t0ZEuR.png" width="400">
</div>

Example 1:

The object is divided into $$N=9$$ self-similar pieces. Each piece is scaled down by a factor of $$r = 3$$. Then the fractal dimension is, $$D = \frac{\log 9}{\log 3} = 2$$, indicating that the fractal is essentially a two-dimensional object (like a plane)

Example 2:

A wire with diameter of $$H$$ is scaled by a factor of $$r$$. As $$r>>H$$, then the wire is considered as a 1-D wire with unit mass. When $$r<<H$$, then the wire is scaled down 3-dimensionally.


### Regular Fractal

#### Koch curve

Each iteration divides the line segment into 4 self-similar pieces, $N=4$. Each piece is scaled down by a factor of $r=3$. The fractial dimension and perimeter of Koch curve are calculated as

$$
\begin{align}
 D &= \frac{\log 4}{\log 3} \approx 1.2619\\
 P &= \left(\frac{4}{3}\right)^{i+1} \qquad (i \rightarrow \infty, P \rightarrow \infty)
\end{align}
$$

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/SJZWIbpU1g.png" width="800">
    <img src="https://hackmd.io/_uploads/B1meJQN_R.png" width="500">
</div>

     
#### Sierpinski Triangle

For each iteration ($$i$$), the triangle is subdivided into $$N=3^i$$ smaller triangles, each scaled down by a factor of $$r=2^i$$ in linear dimension. The fractial dimension and area of Sierpinski Triangle are calculated as

$$
\begin{align}
 D &= \frac{\log 3}{\log 2} \approx 1.585\\
 A &= \left(\frac{3}{4}\right)^{i+1}
\end{align}
$$

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/BJeZvWp8yg.png" width="800">
    <img src="https://hackmd.io/_uploads/BJcfV7V_A.png" width="500">
</div>



#### Menger Sponge

The **Menger Sponge** is a three-dimensional fractal constructed by iteratively removing cubic regions from a larger cube. It is an extension of the Sierpinski Triangle to three dimensions and demonstrates properties like self-similarity, infinite surface area, and a fractal dimension.

For each iteration ($$i$$), the cube in the Menger Sponge is subdivided into $$N=20^i$$ smaller cubes, each scaled down by a factor of $$r=3^i$$ in linear dimension. The fractal dimension and volume of the Menger Sponge are calculated as:


$$
\begin{align}
 D &= \frac{\log 20}{\log 3} \approx 2.7268\\
 V &= \left(\frac{20}{3^3}\right)^i \\
\end{align}
$$

- At $$i = 0$$, a solid cube.
- At $$i = 1$$, a cube with a hole in the center and through the faces.
- As $$i \to \infty$$, the structure becomes a complex, infinitely detailed sponge-like object.
- 
<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/Sk3cvbpLyg.png" width="800">
    <img src="https://hackmd.io/_uploads/S1enPbTU1g.png" width="500">
</div>

### Polymers are random fractals
(To be continued here)

#### Referecne

* Fig 1.9 in p.8 is cute.
* https://en.wikipedia.org/wiki/Fractal
* https://en.wikipedia.org/wiki/Fractal_dimension
* https://larryriddle.agnesscott.org/ifs/siertri/area.htm

