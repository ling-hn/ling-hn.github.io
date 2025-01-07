---
layout: post
title: Richard Project - Diagonalization of a Matrix
description: Is this High School Math?
date: 2024-09-02
author: L. H. Huang
tags: ["Study Notes", "Richard", "Math"]
features:
  math:
    enable: true
---

The scalar coupling in the Hamiltonian:

$$
H = \pi J 2I_z^A I_z^X
$$

In the basis $$\{I_x^A, 2I_y^A I_z^X\}$$, the time evolution of the density operator is governed by the Liouville equation:

$$
\sigma(t) = e^{Lt} \cdot P \cdot \sigma(0)
$$

where 

$$\sigma(t)=\begin{pmatrix} 
   I_x^A(\tau)  \\ 
   2I_y^A I_z^X(\tau)
   \end{pmatrix}; L = \begin{pmatrix} -\rho_{\text{in}}^t & \pi J \\ -\pi J & -\rho_{\text{anti}}^t \end{pmatrix}; P = \begin{pmatrix} -1 & 0 \\ 0 & -1 \end{pmatrix}$$

**Step 1: Diagonalization of \\(L = Q \Lambda Q^{-1}\\)**

(1) Find Eigenvalues by solving the characteristic equation, \\(\det(L - \lambda I) = 0.\\)

(2) Find Eigenvectors by solving $$ (L - \lambda_i I)\mathbf{v}_i = 0$$ for each eigenvalue $$\lambda_i$$, where 
$$\mathbf{v}_i = \frac{\mathbf{v}_i}{\|\mathbf{v}_i\|}=\begin{pmatrix} v_{i,1} \\v_{i,2} \end{pmatrix}$$

(3) Construct $$Q = \begin{bmatrix}
\mathbf{v}_1 & \mathbf{v}_2
\end{bmatrix} = \begin{bmatrix}
\begin{pmatrix} v_{1,1} \\v_{1,2} \end{pmatrix} & \begin{pmatrix} v_{2,1} \\v_{2,2} \end{pmatrix}
\end{bmatrix}$$

(4) Constrcut $$\Lambda = \begin{pmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{pmatrix}$$ 

(5) Construct $$Q^{-1} = \frac{1}{det(Q)}\begin{bmatrix}
v_{2,2} & -v_{1,2} \\ -v_{2,1} &v_{1,1} 
\end{bmatrix}$$ so that $$Q^{-1} Q = I$$

**Step 2: Substitute back to the equation**
   
$$
\sigma(t) = -Q e^{\Lambda t} Q^{-1} \begin{pmatrix} 
   I_x^A(\tau)  \\ 
   2I_y^A I_z^X(\tau)
   \end{pmatrix}
$$

**Step 3: Apply this matrix to the initial state vector to extract $$I_x^A(\tau)$$ and $$2I_y^A I_z^X(\tau)$$**
$$
I_x^A(\tau) = -\big[ Q e^{\Lambda t} Q^{-1} \begin{pmatrix} I_x^A(0) \\ 2I_y^A I_z^X(0) \end{pmatrix} \big]_1
$$
$$
2I_y^A I_z^X(\tau) = -\big[ Q e^{\Lambda t} Q^{-1} \begin{pmatrix} I_x^A(0) \\ 2I_y^A I_z^X(0) \end{pmatrix} \big]_2
$$

$$
\quad
$$

---

$$
\quad
$$

#### Step 1: Diagonalization of the Matrix $$L$$

To diagonalize this matrix, we need to find its eigenvalues and corresponding eigenvectors. 

**(1) Find the eigenvalues $$\lambda$$ by solving the characteristic equation:**

$$
\det(L - \lambda I) = 0 \\
$$

$$
\det\left(\begin{pmatrix} -\rho_{\text{in}}^t & \pi J \\ -\pi J & -\rho_{\text{anti}}^t \end{pmatrix} - \lambda \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}\right) = \det\begin{pmatrix} -\rho_{\text{in}}^t - \lambda & \pi J \\ -\pi J & -\rho_{\text{anti}}^t - \lambda \end{pmatrix} =0\\
$$

$$
\begin{aligned}
&(-\rho_{\text{in}}^t - \lambda)(-\rho_{\text{anti}}^t - \lambda) - (-\pi J)(\pi J) = 0\\
&\lambda^2 + (\rho_{\text{in}}^t + \rho_{\text{anti}}^t)\lambda + (\rho_{\text{in}}^t \rho_{\text{anti}}^t + \pi^2 J^2) = 0\\
&\lambda^2 + \Sigma \rho^t \lambda + (\rho_{\text{in}}^t \rho_{\text{anti}}^t + \pi^2 J^2) = 0 \text{ with } \Sigma \rho^t = \rho_{\text{in}}^t + \rho_{\text{anti}}^t\\
\lambda_{1,2} &= \frac{-\Sigma \rho^t \pm \sqrt{(\Sigma \rho^t)^2 - 4(\rho_{\text{in}}^t \rho_{\text{anti}}^t + \pi^2 J^2)}}{2}\\
&= \frac{-\Sigma \rho^t \pm \sqrt{(\rho_{\text{in}}^t + \rho_{\text{anti}}^t)^2 - 4(\rho_{\text{in}}^t \rho_{\text{anti}}^t + \pi^2 J^2)}}{2}\\
&= \frac{-\Sigma \rho^t \pm \sqrt{(\rho_{\text{in}}^t)^2 -2\rho_{\text{in}}^t \rho_{\text{anti}}^t+(\rho_{\text{anti}}^t)^2- 4 \pi^2 J^2}}{2}\\
&= \frac{-\Sigma \rho^t \pm \sqrt{(\rho_{\text{in}}^t - \rho_{\text{anti}}^t)^2- 4 \pi^2 J^2}}{2}\\
&= \frac{-\Sigma \rho^t \pm iC}{2} \\
&\text{ where } C = \sqrt{(\Delta \rho^t)^2- 4 \pi^2 J^2} \text{ and } \Delta \rho^t = \rho_{\text{anti}}^t - \rho_{\text{in}}^t
\end{aligned}
$$

$$
\quad
$$

**(2) To find the eigenvectors associated with the eigenvalues $$\lambda_1$$ and $$\lambda_2$$, we need to solve the equation:**

$$
(L - \lambda I) \mathbf{v} = 0 \text{ where } L = \begin{pmatrix} -\rho_{\text{in}}^t & \pi J \\ -\pi J & -\rho_{\text{anti}}^t \end{pmatrix} \text{ and } (\lambda_1, \lambda_2)
$$

* Substitute $$\lambda_1 = \frac{1}{2}(-\Sigma \rho^t + iC)$$:

$$
\begin{aligned}
&\begin{pmatrix} -\rho_{\text{in}}^t - \lambda_1 & \pi J \\ -\pi J & -\rho_{\text{anti}}^t - \lambda_1 \end{pmatrix} \begin{pmatrix} v_{1,1} \\ v_{1,2}\end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\begin{pmatrix} -\rho_{\text{in}}^t - \frac{1}{2}(-\Sigma \rho^t + iC) & \pi J \\ -\pi J & -\rho_{\text{anti}}^t - \frac{1}{2}(-\Sigma \rho^t + iC) \end{pmatrix} \begin{pmatrix} v_{1,1} \\ v_{1,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\quad \text{ Sub } \Sigma \rho^t = \rho_{\text{in}}^t + \rho_{\text{anti}}^t\\
&\begin{pmatrix} -\frac{1}{2}(\rho_{\text{in}}^t - \rho_{\text{anti}}^t + iC) & \pi J \\ -\pi J & -\frac{1}{2}(-\rho_{\text{in}}^t + \rho_{\text{anti}}^t + iC) \end{pmatrix} \begin{pmatrix} v_{1,1} \\ v_{1,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\quad \text{ Sub } \Delta \rho^t = \rho_{\text{anti}}^t - \rho_{\text{in}}^t\\
&\begin{pmatrix} -\frac{1}{2}(-\Delta \rho^t + iC) & \pi J \\ -\pi J & -\frac{1}{2}(\Delta \rho^t + iC) \end{pmatrix} \begin{pmatrix} v_{1,1} \\ v_{1,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
\end{aligned}
$$

$$\left\{
\begin{aligned}
-\frac{1}{2}(-\Delta \rho^t + iC) v_{1,1} + \pi J v_{1,2} &= 0 \quad &(1)\\
-\pi J v_{1,1} - \frac{1}{2}(\Delta \rho^t + iC) v_{1,2} &= 0 \quad &(2)
\end{aligned}
\right.$$

$$\text{ From (1), } v_{1,2} = \frac{1}{2\pi J}(-\Delta \rho^t + iC) v_{1,1} \rightarrow \mathbf{v}_1 = \begin{pmatrix} 1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) \end{pmatrix}$$

* Similarly, for $$\lambda_2 = \frac{1}{2}(-\Sigma \rho^t - iC)$$:

$$
\begin{aligned}
&\begin{pmatrix} -\rho_{\text{in}}^t - \lambda_2 & \pi J \\ -\pi J & -\rho_{\text{anti}}^t - \lambda_2 \end{pmatrix} \begin{pmatrix} v_{2,1} \\ v_{2,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\begin{pmatrix} -\rho_{\text{in}}^t - \frac{1}{2}(-\Sigma \rho^t - iC) & \pi J \\ -\pi J & -\rho_{\text{anti}}^t - \frac{1}{2}(-\Sigma \rho^t - iC) \end{pmatrix} \begin{pmatrix} v_{2,1} \\ v_{2,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\quad \text{ Sub } \Sigma \rho^t = \rho_{\text{in}}^t + \rho_{\text{anti}}^t\\
&\begin{pmatrix} -\frac{1}{2}(\rho_{\text{in}}^t - \rho_{\text{anti}}^t - iC) & \pi J \\ -\pi J & -\frac{1}{2}(-\rho_{\text{in}}^t + \rho_{\text{anti}}^t - iC) \end{pmatrix} \begin{pmatrix} v_{2,1} \\ v_{2,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}\\
&\quad \text{ Sub } \Delta \rho^t = \rho_{\text{anti}}^t - \rho_{\text{in}}^t\\
&\begin{pmatrix} -\frac{1}{2}(-\Delta \rho^t - iC) & \pi J \\ -\pi J & -\frac{1}{2}(\Delta \rho^t - iC) \end{pmatrix} \begin{pmatrix} v_{2,1} \\ v_{2,2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}
\end{aligned}
$$

$$\left\{
\begin{aligned}
-\frac{1}{2}(-\Delta \rho^t - iC) v_{2,1} + \pi J v_{2,2} &= 0 \quad (1)\\
-\pi J v_{2,1} - \frac{1}{2}(\Delta \rho^t - iC) v_{2,2} &= 0 \quad (2)
\end{aligned}
\right.$$

$$\rightarrow \mathbf{v}_2 = \begin{pmatrix} 1 \\ -\frac{1}{2\pi J}(\Delta \rho^t + iC) \end{pmatrix}$$


**(3) Construct** $$Q = \begin{bmatrix}
\mathbf{v}_1 & \mathbf{v}_2
\end{bmatrix} = \begin{bmatrix}
\begin{pmatrix} v_{1,1} \\v_{1,2} \end{pmatrix} & \begin{pmatrix} v_{2,1} \\v_{2,2} \end{pmatrix}
\end{bmatrix}$$

**(4) Constrcut $$\Lambda = \begin{pmatrix} \lambda_1 & 0 \\ 0 & \lambda_2 \end{pmatrix}$$**

**(5) Construct matrix of Eigenvectors**

The matrix $$Q$$, which diagonalizes $$L$$, is formed by placing these eigenvectors as columns:

$$
Q= \begin{pmatrix} 1 & 1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) & -\frac{1}{2\pi J}(\Delta \rho^t + iC) \end{pmatrix} \\
$$

The inverse of $$Q$$ can be calculated using the formula for the inverse of a 2x2 matrix: $${Q}^{-1} = \frac{1}{\det(Q)} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$

$$
\begin{aligned}
\det(Q) &= \left(1\right)\left(-\frac{1}{2\pi J}(\Delta \rho^t + iC)\right) - \left(1\right)\left(-\frac{1}{2\pi J}(\Delta \rho^t - iC)\right)\\
&= \frac{1}{2\pi J} \left[ -\Delta \rho^t - iC+ (\Delta \rho^t - iC) \right]\\
&= \frac{1}{2\pi J} \left[ -2iC \right]\\
&= -\frac{iC}{\pi J}\\
{Q}^{-1} &=- \frac{\pi J}{iC} \begin{pmatrix} -\frac{1}{2\pi J}(\Delta \rho^t + iC) & -1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) & 1 \end{pmatrix}
\end{aligned}
$$

$$
\quad
$$

---

$$
\quad
$$

#### **Step 2: Substitute back to the equation**

> Put it all together

$$
\begin{aligned}
\sigma(\tau) &= e^{L\tau} \cdot P \cdot \sigma(0)\\
&= Qe^{\Lambda \tau} {Q}^{-1} \cdot P \cdot\sigma(0)\\
&= \begin{pmatrix} 1 & 1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) & -\frac{1}{2\pi J}(\Delta \rho^t + iC) \end{pmatrix} \begin{pmatrix} e^{\lambda_1 \tau} & 0 \\ 0 & e^{\lambda_2 \tau} \end{pmatrix} \frac{-\pi J}{iC} \begin{pmatrix} -\frac{1}{2\pi J}(\Delta \rho^t + iC) & -1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) & 1 \end{pmatrix} \begin{pmatrix} -1 & 0 \\ 0 & -1 \end{pmatrix} \sigma(0)\\
&= \frac{\pi J}{iC} \begin{pmatrix} e^{\lambda_1 \tau} & e^{\lambda_2 \tau} \\ -\frac{1}{2\pi J}(\Delta \rho^t -iC) e^{\lambda_1 \tau} & -\frac{1}{2\pi J}(\Delta \rho^t + iC) e^{\lambda_2 \tau} \end{pmatrix} \begin{pmatrix} -\frac{1}{2\pi J}(\Delta \rho^t + iC) & -1 \\ -\frac{1}{2\pi J}(\Delta \rho^t - iC) & 1 \end{pmatrix} \sigma(0)\\
&= \frac{\pi J}{iC} \begin{pmatrix} a & b \\ c & d \end{pmatrix} \sigma(0)
\end{aligned}
$$

$$
\begin{aligned}
\quad a &=e^{\lambda_1 \tau} \left(-\frac{1}{2\pi J}(\Delta \rho^t + iC)\right) + e^{\lambda_2 \tau} \left(-\frac{1}{2\pi J}(\Delta \rho^t - iC)\right)\\
\quad b &= -e^{\lambda_1 \tau} + e^{\lambda_2 \tau}\\
\quad c &= -\frac{1}{2\pi J}(\Delta \rho^t - iC) e^{\lambda_1 \tau} \left(-\frac{1}{2\pi J}(\Delta \rho^t + iC)\right) + -\frac{1}{2\pi J}(\Delta \rho^t + iC) e^{\lambda_2 \tau} \frac{1}{2\pi J}(\Delta \rho^t - iC)\\
\quad &=\frac{1}{4\pi^2 J^2} \left[ e^{\lambda_1 \tau} (\Delta \rho^t + iC)(\Delta \rho^t - iC) + e^{\lambda_2 \tau} (\Delta \rho^t - iC)(\Delta \rho^t + iC) \right]\\
\qquad &\text{Given } \Delta \rho^t + iC)(\Delta \rho^t - iC) = (\Delta \rho^t)^2 + C^2 \\
\quad &= \frac{1}{4\pi^2 J^2} \left[ e^{\lambda_1 \tau} + e^{\lambda_2 \tau} \right] \left[ (\Delta \rho^t)^2 + C^2 \right] \\
\quad d &=\frac{1}{2\pi J} \left[e^{\lambda_1 \tau} (\Delta \rho^t - iC) - e^{\lambda_2 \tau} (\Delta \rho^t + iC) \right] \\
\end{aligned}
$$

$$
\begin{aligned}
\rightarrow \sigma(\tau) = \frac{\pi J}{iC} \begin{pmatrix} -\frac{1}{2\pi J} \left[ e^{\lambda_1 \tau} (\Delta \rho^t + iC) + e^{\lambda_2 \tau} (\Delta \rho^t - iC) \right] & -e^{\lambda_1 \tau} + e^{\lambda_2 \tau} \\ \frac{1}{4\pi^2 J^2} \left[ e^{\lambda_1 \tau} + e^{\lambda_2 \tau} \right] \left[ (\Delta \rho^t)^2 + C^2 \right] & \frac{1}{2\pi J} \left[ e^{\lambda_2 \tau} (\Delta \rho^t - iC) - e^{\lambda_1 \tau} (\Delta \rho^t + iC) \right] \end{pmatrix} \sigma(0)
\end{aligned}
$$

$$
\quad
$$

---

$$
\quad
$$

#### Step 3: Apply this matrix to the initial state vector

Let's rewrite the equation:

$$
   \begin{pmatrix} 
   I_x^A(\tau)  \\ 
   2I_y^A I_z^X(\tau)
   \end{pmatrix} = Q e^{\Lambda \tau} Q^{-1} \cdot P \begin{pmatrix} 
   I_x^A(0)  \\ 
   2I_y^A I_z^X(0)
   \end{pmatrix}.
$$

$$
\begin{aligned}
I_x^A(\tau) &= \text{(first row of \(Qe^{\Lambda \tau} {Q}^{-1} \cdot P\))} \cdot 
     I_x^A(0)   \\
     &=\frac{\pi J}{iC}\begin{pmatrix} 
     \frac{1}{2\pi J} \left[ e^{\lambda_1 \tau} (\Delta \rho^t - iC) - e^{\lambda_2 \tau} (\Delta \rho^t + iC) \right] & e^{\lambda_1 \tau} - e^{\lambda_2 \tau}
     \end{pmatrix} \cdot \begin{pmatrix} 
     I_x^A(0)  \\ 
     2I_y^A I_z^X(0)
     \end{pmatrix} \\
     &= \frac{1}{2\pi J} \frac{\pi J}{iC} \left[ e^{\lambda_1 \tau} (\Delta \rho^t - iC) - e^{\lambda_2 \tau} (\Delta \rho^t + iC) \right] I_x^A(0) + \left( e^{\lambda_1 \tau} - e^{\lambda_2 \tau} \right) 2I_y^A I_z^X(0) \\
     &\qquad \text{ Sub } e^{\lambda_1 \tau} = e^{\frac{\tau}{2}(-\Sigma \rho^t + iC)}, \quad e^{\lambda_2 \tau} = e^{\frac{\tau}{2}(-\Sigma \rho^t - iC)} \\
     &= \frac{1}{2iC}  \left[ e^{\frac{\tau}{2}(-\Sigma \rho^t + iC)} (\Delta \rho^t - iC) - e^{\frac{\tau}{2}(-\Sigma \rho^t - iC)} (\Delta \rho^t + iC) \right] I_x^A(0) + \left( e^{\lambda_1 \tau} - e^{\lambda_2 \tau} \right) 2I_y^A I_z^X(0) 
\end{aligned}
$$

Consider the terms in brackets:

$$
\begin{aligned}
&\left[ e^{\frac{\tau}{2}(-\Sigma \rho^t + iC)} (\Delta \rho^t - iC) - e^{\frac{\tau}{2}(-\Sigma \rho^t - iC)} (\Delta \rho^t + iC) \right] \\
&\quad = e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ (\Delta \rho^t - iC) e^{i\frac{C\tau}{2}} - (\Delta \rho^t + iC) e^{-i\frac{C\tau}{2}} \right] \\
&\quad = e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ (\Delta \rho^t - iC) \left(\cos\left(\frac{C\tau}{2}\right) + i\sin\left(\frac{C\tau}{2}\right)\right) - (\Delta \rho^t + iC) \left(\cos\left(\frac{C\tau}{2}\right) - i\sin\left(\frac{C\tau}{2}\right)\right) \right] \\
&\quad = e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ \Delta \rho^t \cos\left(\frac{C\tau}{2}\right) + i\Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - iC \cos\left(\frac{C\tau}{2}\right) - C \sin\left(\frac{C\tau}{2}\right) \right. - \left. \Delta \rho^t \cos\left(\frac{C\tau}{2}\right) + i\Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - iC \cos\left(\frac{C\tau}{2}\right) + C \sin\left(\frac{C\tau}{2}\right) \right] \\
&\quad = e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ 2i \Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - 2i C \cos\left(\frac{C\tau}{2}\right) \right] \\
&\quad = 2i e^{-\frac{\tau}{2} \Sigma \rho^t} \left( \Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - C \cos\left(\frac{C\tau}{2}\right) \right)
\end{aligned}
$$

> *$$e^{i\frac{C\tau}{2}} = \cos\left(\frac{C\tau}{2}\right) + i\sin\left(\frac{C\tau}{2}\right), \quad e^{-i\frac{C\tau}{2}} = \cos\left(\frac{C\tau}{2}\right) - i\sin\left(\frac{C\tau}{2}\right)$$


$$
\begin{aligned}
I_x^A(\tau) &= \frac{1}{2iC}  \left[2i e^{-\frac{\tau}{2} \Sigma \rho^t} \left( \Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - C \cos\left(\frac{C\tau}{2}\right) \right) \right] \\
&= \frac{1}{C}  e^{-\frac{\tau}{2} \Sigma \rho^t} \left( \Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - C \cos\left(\frac{C\tau}{2}\right) \right)  I_x^A(0)\\
&= -\frac{1}{C}  e^{-\frac{1}{2} \Sigma \rho^t \tau} \left( C \cos\left(\frac{1}{2}C\tau\right) - \Delta \rho^t \sin\left(\frac{1}{2}C\tau\right) \right)I_x^A(0)\\
2I_y^A I_z^X(\tau) &= \text{(second row of \(Qe^{\Lambda \tau} {Q}^{-1} \cdot P\))} \cdot \begin{pmatrix} 
     I_x^A(0)  \\ 
     2I_y^A I_z^X(0)
     \end{pmatrix}\\
     &= \begin{pmatrix} 
\frac{1}{4\pi^2 J^2} \left[ e^{\lambda_1 \tau} + e^{\lambda_2 \tau} \right] \left[ (\Delta \rho^t)^2 + C^2 \right] & -\frac{1}{2\pi J} \left[ e^{\lambda_2 \tau} (\Delta \rho^t + iC) - e^{\lambda_1 \tau} (\Delta \rho^t - iC) \right] 
     \end{pmatrix} \cdot \begin{pmatrix} 
     I_x^A(0)  \\ 
     2I_y^A I_z^X(0)
     \end{pmatrix} \\
     &= \frac{1}{4\pi^2 J^2} \left[ e^{\lambda_1 \tau} + e^{\lambda_2 \tau} \right] \left[ (\Delta \rho^t)^2 + C^2 \right] I_x^A(0)- \frac{1}{2\pi J} \left[ e^{\lambda_2 \tau} (\Delta \rho^t + iC) - e^{\lambda_1 \tau} (\Delta \rho^t - iC) \right] 2I_y^A I_z^X(0)
\end{aligned}
$$

Again here we neglect $$I_x^A(0)$$ term, and focus on the second bracket: 

$$
\begin{aligned}
&\quad \left[e^{\lambda_2 \tau} (\Delta \rho^t + iC) - e^{\lambda_1 \tau} (\Delta \rho^t - iC)\right] \\
&=\left[e^{\frac{\tau}{2}(-\Sigma \rho^t - iC)} (\Delta \rho^t + iC) - e^{\frac{\tau}{2}(-\Sigma \rho^t + iC)} (\Delta \rho^t - iC)\right] \\
&=\left[e^{-\frac{\tau}{2} \Sigma \rho^t} \left( e^{-\frac{iC\tau}{2}} (\Delta \rho^t + iC) - e^{\frac{iC\tau}{2}} (\Delta \rho^t - iC) \right)\right] \\
&=e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ \left(\cos\left(\frac{C\tau}{2}\right) - i\sin\left(\frac{C\tau}{2}\right)\right) (\Delta \rho^t + iC) - \left(\cos\left(\frac{C\tau}{2}\right) + i\sin\left(\frac{C\tau}{2}\right)\right) (\Delta \rho^t - iC) \right]\\
&=e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ \Delta \rho^t \cos\left(\frac{C\tau}{2}\right) - iC \cos\left(\frac{C\tau}{2}\right) - i\Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - C \sin\left(\frac{C\tau}{2}\right) \right. \left. - \Delta \rho^t \cos\left(\frac{C\tau}{2}\right) - iC \cos\left(\frac{C\tau}{2}\right) + i\Delta \rho^t \sin\left(\frac{C\tau}{2}\right) - C \sin\left(\frac{C\tau}{2}\right) \right] \\
&=e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ -2iC \cos\left(\frac{C\tau}{2}\right) - 2C \sin\left(\frac{C\tau}{2}\right) \right]\\
&=e^{-\frac{\tau}{2} \Sigma \rho^t} \cdot (-2C) \left[ i \cos\left(\frac{C\tau}{2}\right) + \sin\left(\frac{C\tau}{2}\right) \right] \\
&=-2C e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ i \cos\left(\frac{C\tau}{2}\right) + \sin\left(\frac{C\tau}{2}\right) \right]
\end{aligned}
$$

$$
\begin{aligned}
2I_y^A I_z^X(\tau) &=  -\frac{1}{2\pi J} \left[ e^{\lambda_2 \tau} (\Delta \rho^t + iC) - e^{\lambda_1 \tau} (\Delta \rho^t - iC) \right] 2I_y^A I_z^X(0)\\
&=  -\frac{1}{2\pi J} \left[ -2C e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ i \cos\left(\frac{C\tau}{2}\right) + \sin\left(\frac{C\tau}{2}\right) \right] \right] 2I_y^A I_z^X(0)
\end{aligned}
$$

$$
\quad
$$

---

$$
\quad
$$

![image](https://hackmd.io/_uploads/SJwMBwy30.png)

$$
\begin{aligned}
I_x^A(\tau) &= -\frac{1}{C}  e^{-\frac{1}{2} \Sigma \rho^t \tau} \left( C \cos\left(\frac{1}{2}C\tau\right) - \Delta \rho^t \sin\left(\frac{1}{2}C\tau\right) \right)I_x^A(0)\\
2I_y^A I_z^X(\tau) &=  -\frac{1}{2\pi J} \left[ -2C e^{-\frac{\tau}{2} \Sigma \rho^t} \left[ i \cos\left(\frac{C\tau}{2}\right) + \sin\left(\frac{C\tau}{2}\right) \right] \right] 2I_y^A I_z^X(0)
\end{aligned}
$$