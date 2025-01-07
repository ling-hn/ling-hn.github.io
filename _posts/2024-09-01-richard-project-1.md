---
layout: post
title: Richard Project -  Soloman Equations and Runge-Kutta 4th order Method
description: The Solomon equations describe the time evolution of the magnetization components of a system of interacting spins.
date: 2024-09-01
author: L. H. Huang
tags: ["Study Notes", "Richard", "Python"]
features:
  math:
    enable: true
---

The Solomon equations describe the time evolution of the magnetization components of a system of interacting spins. The given Solomon equations for a system of two interacting spins $$I$$and $$S$$are:

$$
\begin{aligned}
\frac{dI_z}{dt} &= -\rho_I ( \langle I_z \rangle - I_z^0 ) - \sigma_{IS} ( \langle S_z \rangle - S_z^0 ) - \delta_I 2I_z S_z \\
\frac{dS_z}{dt} &= -\rho_S ( \langle S_z \rangle - S_z^0 ) - \sigma_{IS} ( \langle I_z \rangle - I_z^0 ) - \delta_S 2I_z S_z \\
\frac{d(2I_z S_z)}{dt} &= -\rho_{IS} 2I_z S_z - \delta_I ( \langle I_z \rangle - I_z^0 ) - \delta_S ( \langle S_z \rangle - S_z^0 ) \\
\end{aligned}
$$

- $$I_z^0$$ and $$S_z^0$$ are the equilibrium values for the z-magnetization of the $$I$$and $$S$$spins, respectively.
- $$2I_z S_z$$represents the heteronuclear, longitudinal two-spin order. This term reflects the imbalance in the occupancy of the four energy levels of the coupled $$IS$$system.
- $$\rho_I$$and $$\rho_S$$: Longitudinal relaxation rates for the $$I$$and $$S$$spins.
- $$\sigma_{IS}$$: Cross-relaxation rate between the two spins.
- $$\rho_{IS}$$: Two-spin order decay rate.
- $$\delta_I$$and $$\delta_S$$: Cross-correlation rates due to DD-CSA.

Define $$\Delta I_z = \langle I_z \rangle - I_z^0$$and $$\Delta S_z = \langle S_z \rangle - S_z^0$$

$$
\begin{aligned}
\frac{d}{dt} \begin{bmatrix} 
\langle I_z \rangle - I_z^0 \\ 
\langle S_z \rangle - S_z^0 \\ 
2I_z S_z 
\end{bmatrix} = -\begin{bmatrix} 
\rho_I & \sigma_{IS} & \delta_I \\ 
\sigma_{IS} & \rho_S & \delta_S \\ 
\delta_I & \delta_S & \rho_{IS} 
\end{bmatrix} \begin{bmatrix} 
\Delta I_z \\ 
\Delta S_z \\ 
2I_z S_z 
\end{bmatrix}
\end{aligned}
$$

Given that $$\frac{dI_z^0}{dt} = 0$$and $$\frac{dS_z^0}{dt} = 0$$, it is indeed correct to write the differential equations directly in terms of $$I_z$$, $$S_z$$, and $$2I_z S_z$$without explicitly considering the equilibrium values $$I_z^0$$and $$S_z^0$$in the differentiation. 

$$
\begin{aligned}
\frac{d}{dt} \begin{bmatrix} 
I_z \\ 
S_z \\ 
2I_z S_z 
\end{bmatrix} = -\begin{bmatrix} 
\rho_I & \sigma_{IS} & \delta_I \\ 
\sigma_{IS} & \rho_S & \delta_S \\ 
\delta_I & \delta_S & \rho_{IS} 
\end{bmatrix} \begin{bmatrix} 
\Delta I_z \\ 
\Delta S_z \\ 
2I_z S_z 
\end{bmatrix}
\end{aligned}
$$

Rewrite the equation in form of $$\frac{d\mathbf{M}}{dt} = \mathbf{A} \mathbf{M}(t) + \mathbf{B}$$, 

$$
\begin{aligned}
\frac{d}{dt} \begin{bmatrix} 
I_z \\ 
S_z \\ 
2I_z S_z 
\end{bmatrix} = -\begin{bmatrix} 
\rho_I & \sigma_{IS} & \delta_I \\ 
\sigma_{IS} & \rho_S & \delta_S \\ 
\delta_I & \delta_S & \rho_{IS} 
\end{bmatrix} \begin{bmatrix} 
I_z \\ 
S_z \\ 
2I_z S_z 
\end{bmatrix}+
\begin{bmatrix} 
\rho_I I_z^0 + \sigma_{IS} S_z^0 \\ 
\sigma_{IS} I_z^0 + \rho_S S_z^0 \\ 
\delta_I I_z^0 + \delta_S S_z^0 
\end{bmatrix}
\end{aligned}
$$

We start from here. 

$$
\quad
$$

$$
\quad
$$

### Goal: Estimation the cross relaxation rates

Ideally we can get longitudinal relaxation rates, $$\rho_I$$and $$\rho_S$$, and two-spin order decay rate, $$\rho_{IS}$$, from regular measurements. To evaluate the weight of cross-relaxation effect, we estimate the parameter $$\delta_I$$, $$\delta_S$$, and $$\sigma_{IS}$$ by fitting the time-dependent data of $$I_z(t)$$, $$S_z(t)$$, and $$2I_zS_z(t)$$using a system of differential equations solved by the Runge–Kutta method and minimized using the Nelder–Mead simplex method.[Kuprov, 2004]

- **$$\sigma_{IS}$$: Cross-relaxation rate between the two spins.**
- **$$\delta_I$$and $$\delta_S$$: Cross-correlation rates due to DD-CSA.**


The `solve_ivp` function from SciPy is used to solve the system of differential equations numerically. We employ the 4th-order Runge–Kutta method (`RK45`) with a high tolerance ($$10^{-10}$$) for accuracy.[Kuprov, 2004]

```$$python
sol = solve_ivp(solomon_eqns, [0, 60], [Iz_data[0], Sz_data[0], izsz_data[0]], args=(sigma_IS, delta_I, delta_S), t_eval=t_Iz, method='RK45', rtol=1e-10) 
```

Least squares error minimization is a common method for parameter estimation where the goal is to minimize the sum of squared differences between observed data and model predictions. In weighted least squares, each term in the sum is divided by a weight, which can be used to handle heteroscedasticity (different variances in the data). The objective function is defined as the weighted least squares error between the model predictions and the observed data: $$\text{Error} = \sum_{i=1}^n \left( \frac{I_z^{\text{model}}(t_i) - I_z^{\text{data}}(t_i)}{w_i} \right)^2$$ where $$w_i$$ is the weight (assumed 1 for simplicity here). 

```$$python
def objective(params):
    sigma_IS, delta_I, delta_S = params
    sol = solve_ivp(solomon_eqns, [0, 60], [Iz_data[0], Sz_data[0], izsz_data[0]], args=(sigma_IS, delta_I, delta_S), t_eval=t_Iz, method='RK45', rtol=1e-10)    
    # Interpolate results to match observed data points
    Iz_model = np.interp(t_Iz, sol.t, sol.y[0])    
    # Calculate weighted least squares error
    error = np.sum((Iz_data - Iz_model)**2)    
    return error
```

Nelder–Mead Simplex Method is an optimization algorithm used to find the minimum or maximum of a function in a multidimensional space. It iteratively updates a simplex, a geometric figure with $$n+1$$ vertices in $$n$$-dimensional space, to explore the parameter space. The method does not require derivatives, making it suitable for problems where the objective function is not smooth or has discontinuities. The `minimize` function from SciPy's `optimize` module is used to find the value of $$\delta_S$$that minimizes the objective function. The Nelder–Mead simplex algorithm is used due to its robustness in handling non-linear optimization problems without the need for gradient information.

```$$python
# Use Nelder-Mead method to minimize the objective function
result = minimize(objective, initial_guess, method='Nelder-Mead', options={'xatol': 1e-4, 'disp': True})
```

$$
\quad
$$

---

$$
\quad
$$

#### ***Evaluation of Fitting Quality***

Mean Absolute Error (MAE) for understanding the fit quality and general model accuracy. The covariance matrix (or parameter uncertainties) to assess the precision of the parameter estimates.

#### Reliability of fitted parameters

Nelder-Mead iteratively adjusts the parameters to minimize the objective function, which in this case is the sum of squared residuals (least squares error) between observed and modeled $$I_z$$values. Nelder-Mead alone doesn’t directly provide error bars for the parameters. However, you can evaluate the uncertainty (error bars) using the covariance matrix approach **after** finding the optimal parameters.

After obtaining optimized parameters, the covariance matrix provides information about the uncertainty (standard errors) of these parameters. The covariance matrix is computed from the Jacobian of the residuals around the optimal parameters. The diagonal elements of this matrix represent the variance of each parameter, giving the standard error upon taking the square root.

1. Objective Function
   The objective function to minimize is defined as:
   $$\text{Error} = \sum_{i=1}^n (I_z^{\text{data}}(t_i) - I_z^{\text{model}}(t_i))^2$$,    where $$I_z^{\text{model}}$$is obtained by solving the differential equations using the parameters $$\sigma_{IS}$$, $$\delta_I$$, and $$\delta_S$$.
   
2. Residuals
   After obtaining the optimal parameters $$\theta = (\sigma_{IS}, \delta_I, \delta_S)$$, compute the residuals:   $$r_i(\theta) = I_z^{\text{data}}(t_i) - I_z^{\text{model}}(t_i)$$  for each data point $$i$$.
   
 3. Jacobian Matrix Calculation
   The Jacobian matrix $$J$$of the residuals with respect to the parameters is calculated using finite differences. For a parameter $$\theta_j$$: $$J_{ij} = \frac{\partial r_i}{\partial \theta_j} \approx \frac{r_i(\theta + \epsilon \, e_j) - r_i(\theta)}{\epsilon}$$ where $$\epsilon$$is a small perturbation, and $$e_j$$is a unit vector in the direction of $$\theta_j$$. This results in a Jacobian matrix $$J$$with dimensions $$n \times p$$, where $$n$$is the number of data points and $$p$$is the number of parameters.
   
4. Covariance Matrix of Parameters
   The covariance matrix $$\mathbf{C}$$ of the parameters is estimated by: $$\mathbf{C} = (J^T J)^{-1}$$ where $$J^T$$is the transpose of the Jacobian matrix $$J$$.
   
5. Error Bars (Standard Errors)
   The error (standard deviation) for each parameter is given by the square root of the corresponding diagonal element of the covariance matrix: $$\text{Error for } \theta_j = \sqrt{\mathbf{C}_{jj}}$$ where $$\mathbf{C}_{jj}$$is the $$j$$-th diagonal element of $$\mathbf{C}$$.

```$$python
# Updated residuals function that takes all parameters as input
def residuals_full(params):
    sigma_IS, delta_I, delta_S = params
    sol = solve_ivp(solomon_eqns, [0, 60], [Iz_data[0], Sz_data[0], izsz_data[0]], args=(sigma_IS, delta_I, delta_S), 
                    t_eval=t_Iz, method='RK45', rtol=1e-10)
    Iz_model = np.interp(t_Iz, sol.t, sol.y[0])
    return Iz_data - Iz_model  # Returns a vector of residuals

# Calculate the Jacobian matrix for all parameters simultaneously
jacobian_matrix = np.zeros((len(Iz_data), len(initial_guess)))
for i in range(len(initial_guess)):
    # Create a partial derivative function for each parameter
    perturbed_params = initial_guess.copy()
    perturbed_params[i] += epsilon
    jacobian_matrix[:, i] = (residuals_full(perturbed_params) - residuals_full([sigma_IS_est, delta_I_est, delta_S_est])) / epsilon

# Calculate the covariance matrix and standard errors
cov_matrix = np.linalg.inv(jacobian_matrix.T @ jacobian_matrix)
std_errors = np.sqrt(np.diag(cov_matrix))
```

#### Mean Absolute Error (MAE)

The Mean Absolute Error measures the average magnitude of errors in the predictions made by the model. Given $$N$$  data points $$(x_i, y_i)$$ where $$y_i$$  is the observed value and $$\hat{y}_i$$  is the model's predicted value at $$x_i$$ , the MAE is:
$$\text{MAE} = \frac{1}{N} \sum_{i=1}^N \left| y_i - \hat{y}_i \right|$$ where $$y_i$$  is the actual observed data point and $$\hat{y}_i$$  is the predicted value from the model.

MAE represents the average absolute deviation between the observed values and the model predictions. Since it is an absolute measure, it is less sensitive to outliers than metrics like the Mean Squared Error (MSE). A lower MAE indicates a model with better average accuracy.

```$$python
def mae(observed, predicted):
    return np.mean(np.abs(observed - predicted))
mae_Iz = round(mae(Iz_data, Iz_model_full), 2)
mae_Sz = round(mae(Sz_data, Sz_model_full), 2)
mae_izsz = round(mae(izsz_data, izsz_model_full), 2)
```


$$
\quad
$$

$$
\quad
$$

#### Misc Tests

***Test #1.1: Dependence on $$\sigma_{IS}$$***

$$\sigma_{IS}$$is the cross-relaxation rate between the two spins. If $$\sigma_{IS}$$= 0, it means the polarization transfer is purely driven by CSA. 

![image](https://hackmd.io/_uploads/BJ6zQzzqC.png)

***Test #1.2: Dependence on $$\sigma_{IS}$$***

The goal is to find $$\delta_S$$, the cross-correlation rates due to DD-CSA. Let's fix $$\sigma_{IS}$$= 0 to see the dependence on $$\delta_S$$. In (Kuprov, 2004), $$\delta_S = 0.3$$. 
![image](https://hackmd.io/_uploads/SkiIvGGcR.png)

#### Test #2: Integration methods

**Conclusion: Just stay with Richard.**

![image](https://hackmd.io/_uploads/SJSAMfM5A.png)

***1. Runge-Kutta 4th Order Method (Implemented using `solve_ivp`)***

For an ODE $$\frac{dy}{dt} = f(t, y)$$, RK4 estimates the solution $$y(t)$$over a small interval $$[t, t+h]$$using the following steps:

$$
\begin{aligned}
k_1 &= h f(t_n, y_n) \\
k_2 &= h f\left(t_n + \frac{h}{2}, y_n + \frac{k_1}{2}\right) \\
k_3 &= h f\left(t_n + \frac{h}{2}, y_n + \frac{k_2}{2}\right) \\
k_4 &= h f(t_n + h, y_n + k_3) \\
y_{n+1} &= y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4)
\end{aligned}
$$

The method adapts the step size $$h$$to control the error, ensuring the solution remains within a relative error tolerance of $$10^{-10}$$.

***2. ODE Integration using `odeint`***

`odeint`odeint is a function from `scipy.integrate` that integrates a system of ordinary differential equations $$\frac{dy}{dt} = f(t, y)$$.


***3. Eigenproblem Analytical Solution***

$$
\begin{aligned}
\text{Differential equation:} & \quad \frac{d\mathbf{M}}{dt} = \mathbf{A} \mathbf{M}(t) + \mathbf{B} \\
\text{Eigenvalue Decomposition:} & \quad \mathbf{A} = \mathbf{V} \Lambda \mathbf{V}^{-1} \\
\text{Homogeneous Solution:} & \quad \frac{d\mathbf{M}_h}{dt} = \mathbf{A} \mathbf{M}_h \\
& \quad \mathbf{M}_h(t) = \mathbf{V} e^{\Lambda t} \mathbf{V}^{-1} \mathbf{M}_0 \\
\text{Particular Solution:} & \quad \mathbf{A} \mathbf{M}_p + \mathbf{B} = 0 \\
& \quad \mathbf{M}_p = -\mathbf{A}^{-1} \mathbf{B} \\
\text{Total Solution:} & \quad \mathbf{M}(t) = \mathbf{M}_h(t) + \mathbf{M}_p
\end{aligned}
$$


#### Reference

* Kuprov, I., & Hore, P. J. (2004). Chemically amplified 19F–1H nuclear Overhauser effects. Journal of Magnetic Resonance, 168(1), 1-7.
* Forster, M. J. (1991). Comparison of compuational methods for simulating nuclear Overhauser effects in NMR spectroscopy. Journal of computational chemistry, 12(3), 292-300.
* Guenneau, F., Mutzenhardt, P., Assfeld, X., & Canet, D. (1998). Carbon-13 chemical shielding parameters in liquid hexafluorobenzene determined by NMR relaxation measurements. The Journal of Physical Chemistry A, 102(36), 7199-7205.