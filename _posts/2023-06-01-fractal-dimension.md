---
layout: post
title: Fractal Dimension
description: An index for characterizing fractal patterns or sets by quantifying their complexity as a ratio of the change in detail to the change in scale.
date: 2023-06-01
author: L. H. Huang
tags: ["Study Notes", "Physics", "Polymer"]
features:
  math:
    enable: true
---

* **Fractal**: Self-similar. A geometric shape containing detailed structure at arbitrarily small scales, usually having a fractal dimension strictly exceeding the topological dimension.

* **Fractal dimension**: An index for characterizing fractal patterns or sets by quantifying their complexity as a ratio of the change in detail to the change in scale.

\begin{align}
 N &= r^D &\\
 D &= \frac{\log N}{\log r} \\
\quad \\
 N &\text{: Number of miniature pieces in the final figure}\\
 r &\text{: Scaling factor}\\
 D &\text{: Fractal dimension}
\end{align}

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/rk1t0ZEuR.png" width="500">
</div>

Example 1:
> The object is divided into $N=9$ self-similar pieces. Each piece is scaled down by a factor of $r = 3$. Then the fractal dimension is, $D = \frac{\log 9}{\log 3} = 2$, indicating that the fractal is essentially a two-dimensional object (like a plane)

Example 2:
> A wire with diameter of $H$ is scaled by a factor of $r$. As $r>>H$, then the wire is considered as a 1-D wire with unit mass. When $r<<H$, then the wire is scaled down 3-dimensionally.


## Regular Fractal

### Koch curve

Each iteration divides the line segment into 4 self-similar pieces, $N=4$. Each piece is scaled down by a factor of $r=3$. The fractial dimension and perimeter of Koch curve are calculated as

\begin{align}
 D &= \frac{\log 4}{\log 3} \approx 1.2619\\
 P &= \left(\frac{4}{3}\right)^{i+1} \qquad (i \rightarrow \infty, P \rightarrow \infty)
\end{align}

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/HkO6w7NOA.png" width="500">
    <img src="https://hackmd.io/_uploads/B1meJQN_R.png" width="500">
</div>

     
### Sierpinski Triangle

For each iteration ($i$), the triangle is subdivided into $N=3^i$ smaller triangles, each scaled down by a factor of $r=2^i$ in linear dimension. The fractial dimension and area of Sierpinski Triangle are calculated as
\begin{align}
 D &= \frac{\log 3}{\log 2} \approx 1.585\\
 A &= \left(\frac{3}{4}\right)^{i+1}
\end{align}

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/Hy6S_mNuA.png" width="500">
    <img src="https://hackmd.io/_uploads/BJcfV7V_A.png" width="500">
</div>



### Menger Sponge

For each iteration ($i$), the triangle is subdivided into $N=20^i$ smaller triangles, each scaled down by a factor of $r=3^i$ in linear dimension. The fractial dimension and area of Sierpinski Triangle are calculated as
\begin{align}
 D &= \frac{\log 20}{\log 3} \approx 2.7268\\
 V &= \left(\frac{1}{3}\right)^i
\end{align}

<div style="text-align:center;">
    <img src="https://hackmd.io/_uploads/rkaMomEOC.png" width="500">
</div>

## Polymers are random fractals

Referecne
---
Fig 1.9 in p.8 is cute.
https://en.wikipedia.org/wiki/Fractal
https://en.wikipedia.org/wiki/Fractal_dimension
https://larryriddle.agnesscott.org/ifs/siertri/area.htm

```
import matplotlib.pyplot as plt
import numpy as np

############################### 
# Set the number of iterations#

iterations = 10

###############################

def koch_curve(iterations):
    points = np.array([[0, 0], [1, 0]])
    segments = 1
    perimeter = 1  

fractal_dimensions = []
segments_counts = []
perimeters = []

# length of a segment
def segment_length(p1, p2):
    return np.sqrt((p2[0] - p1[0])**2 + (p2[1] - p1[1])**2)

def iterate(points):
    new_points = []
    new_perimeter = 0
    for i in range(len(points) - 1):
        p1 = points[i]
        p2 = points[i + 1]
        dx = p2[0] - p1[0]
        dy = p2[1] - p1[1]
        
        # Divide segment into three parts
        pA = p1
        pB = p1 + np.array([dx / 3, dy / 3])
        pC = p1 + np.array([2 * dx / 3, 2 * dy / 3])
        pD = p2
        
        # Calculate the peak of the equilateral triangle
        pE = pB + np.array([dx / 3 * np.cos(np.pi / 3) - dy / 3 * np.sin(np.pi / 3),
                            dx / 3 * np.sin(np.pi / 3) + dy / 3 * np.cos(np.pi / 3)])
        
        new_points.extend([pA, pB, pE, pC, pD])
        
        # Calculate the length of the modified segment
        new_perimeter += segment_length(pA, pB) + segment_length(pB, pE) + segment_length(pE, pC) + segment_length(pC, pD)
    
    return np.array(new_points), new_perimeter

N_0 = 0
for i in range(iterations):
    points, new_perimeter = iterate(points)
    segment = len(points) - 1  # Number of segments
    
    if i == 0:
        N_0 = segment
    
    segments = N_0 ** (i + 1)
    fractal_dimension = np.log(segments) / np.log(3**(i + 1))
    
    perimeter += new_perimeter
    
    # Store data for plotting
    segments_counts.append(segments)
    fractal_dimensions.append(fractal_dimension)
    perimeters.append(perimeter)

    # Plotting the Koch curve at each iteration
    plt.figure(figsize=(10, 2))
    plt.plot(points[:, 0], points[:, 1], 'b-', linewidth=0.2)
    plt.title(f"Koch Curve - Iteration {i + 1}: N = {segments}, D = {fractal_dimension:.2f}, Perimeter = {perimeter:.2f}")

    plt.axis('equal')
    plt.axis('off')
    plt.show()

# Plotting
fig, ax1 = plt.subplots(figsize=(10, 6))

ax1.set_xlabel('Iteration')
ax1.set_ylabel('Fractal Dimension (D)', color='b')
ax1.plot(np.arange(1, iterations + 1), fractal_dimensions, marker='o', linestyle='-', color='b')
ax1.tick_params(axis='y', labelcolor='b')

ax2 = ax1.twinx()
ax2.set_ylabel('Number of Segments (N)', color='g')
ax2.plot(np.arange(1, iterations + 1), segments_counts, marker='s', linestyle='-', color='g')
ax2.tick_params(axis='y', labelcolor='g')

ax3 = ax1.twinx()
ax3.spines['right'].set_position(('outward', 60))  # move the third axis to the right
ax3.set_ylabel('Perimeter', color='r')
ax3.plot(np.arange(1, iterations + 1), perimeters, marker='^', linestyle='-', color='r')
ax3.tick_params(axis='y', labelcolor='r')

plt.title('Koch Curve Properties vs Iteration')
plt.tight_layout()
plt.show()

koch_curve(iterations)
    

```

```
import matplotlib.pyplot as plt
import numpy as np

############################### 
# Set the number of iterations#

iterations = 10

###############################

def sierpinski_triangle(iterations):
	points = np.array([[0, 0], [1, 0], [0.5, np.sqrt(3)/2]]) #initial triangle

triangles = [points] # vertices of the triangles

iterations_list = list(range(1, iterations + 1))
fractal_dimensions = []
segments_counts = []
areas = []

def midpoint(p1, p2):
    return (p1 + p2) / 2

def calculate_properties(iterations):
    fractal_dimension = np.log(3) / np.log(2)      
    segments_count = 3 ** iterations
    area = (np.sqrt(3) / 4) * (0.5 ** (2 * iterations))
    return fractal_dimension, segments_count, area

for iteration in iterations_list:
    fractal_dimension, segments_count, area = calculate_properties(iteration)
    fractal_dimensions.append(fractal_dimension)
    segments_counts.append(segments_count)
    areas.append(area)
	
    plt.figure(figsize=(8, 6))

    for triangle in triangles:
        plt.plot(np.append(triangle[:, 0], triangle[0, 0]), np.append(triangle[:, 1], triangle[0, 1]), 'b-', linewidth=0.8)
    plt.title(f"Sierpinski Triangle - Iteration {iteration}, N = {segments_count}, D = {fractal_dimension:.2f}, Area = {area:.2e}")
    plt.axis('equal')
    plt.axis('off')
    plt.show()

    # Generating new triangles for the next iteration
    new_triangles = []
    for triangle in triangles:
        mid1 = midpoint(triangle[0], triangle[1])
        mid2 = midpoint(triangle[1], triangle[2])
        mid3 = midpoint(triangle[2], triangle[0])

        t1 = np.array([triangle[0], mid1, mid3])
        t2 = np.array([mid1, triangle[1], mid2])
        t3 = np.array([mid3, mid2, triangle[2]])
        
        new_triangles.extend([t1, t2, t3])
    
    triangles = new_triangles

fig, ax1 = plt.subplots(figsize=(10, 6))

ax1.plot(iterations_list, fractal_dimensions, 'b-', marker='o', label='Fractal Dimension')
ax1.set_xlabel('Iteration')
ax1.set_ylabel('Fractal Dimension', color='b')
ax1.tick_params(axis='y', labelcolor='b')

ax2 = ax1.twinx()
ax2.plot(iterations_list, segments_counts, 'g-', marker='s', label='Number of Segments')
ax2.set_ylabel('Number of Segments', color='g')
ax2.tick_params(axis='y', labelcolor='g')

ax3 = ax1.twinx()
ax3.spines['right'].set_position(('outward', 60))  # Offset the third axis
ax3.plot(iterations_list, areas, 'r-', marker='^', label='Area')
ax3.set_ylabel('Area', color='r')
ax3.tick_params(axis='y', labelcolor='r')

fig.tight_layout()
plt.title('Sierpinski Triangle Properties vs Iteration')
plt.show()

sierpinski_triangle(iterations)

```