# nddesolver
[![View Linear Neutral Delay Differential Equations solver on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/120458-linear-neutral-delay-differential-equations-solver)

**About the function**

sol=nddesolver(dydt, delay, preshape, interval, N, s) integrates a linear, homogeneous, delay differential equations of neutral type with constant coefficients and constant delay given by
                            y'(t)=a_1 y(t) + a_2 y(t-h) + a_3 y'(t-h),               t in [t_0, t_1]                                (1)
                            y(t) = phi(t)                                                          t in [t_0-h, t_0]
where

- t is the independent variable representing time,
- y(t-h) is the solution with delay h, and
- y'(t-h) is the derivative of the solution with delay h. 
- phi(t) is the history/preshape function

This function can be solved explicitly using a generalized Lambert W function called the Lambert W function [1]. This solution is given by
                           y(t)= C(-N)exp(λ(-N) t)+...+C(i)exp(λ(i) t)+...+C(N)exp(λ(N) t), i=-N,...,N
where

- λ(i) is a complex value dependent on the value of the Lambert W function, and
- C(I) is a real-valued coefficient of e^(λ(i) t) dependent on the preshape/history function.


**Examples**
Included in the files are two examples comparing the solutions of a first-order linear, homogeneous NDDE obtained using nddesolver, with its analytical solution.


**Input Arguments**

- dydt is the vector containing the coefficients of (1). 
- delay is the constant delay h in (1).  The value of h must be positive.
- preshape is the history function phi(t) on  
- interval is the interval of integration. The first element t_0 is the initial value of t. The second element t_1 is the final value of t. The value of t_0  must be less than t_1.
- N is the number of complex roots of the Lambert W function with positive imaginary parts. (See the function rlambertw below.)
- s is the step size of the values of t


**Output Arguments**

sol, returned as a structure containing the following fields:
- sol.x is the mesh on [t_0, t_1]
- sol.y is the approximation to y(t) the mesh points
- sol.c is a vector containing the coefficients C(I) from (2)
- sol.l is a vector containing all  computed using the function lambda
- sol.histx is the mesh on [t_0-h, t_0]
- sol.histy is the preshape function evaluated at sol.histx
- sol.psi is a matrix with elements 
- sol.cond is the condition number of sol.psi


**Other functions**

Also included in the files are the following functions:
- RA_solver finds the values of r and a for the Lambert W function
- lambda computes a vector of λ(i)'s, where each λ(i) satisfies the equation
               λ(i)=(1/h) W_{(r,i)} (a) - a_1
      (See [1] for the derivation of the formula.)
- rlambertw computes a vector of the values of the Lambert W function for some r and a (denoted  W_{(r,i)} (a))  where each  W_{(r,I)} (a) satisfies
             W_{(r,I)} (a) exp( W_{(r,I)} (a))  + r W_{(r,I)} (a) = a.
       (See [2] for reference.)


**Reference:**

[1] Jamilla, C., Mendoza, R., & Mező, I. (2020). Solutions of neutral delay differential equations using a generalized Lambert W function. Applied Mathematics and Computation, 382, 125334.https://doi.org/10.1016/j.amc.2020.125334

[2] Mező, I., & Baricz, Á. (2017). On the generalization of the Lambert 𝑊 function. Transactions of the American Mathematical Society, 369(11), 7917-7934. https://doi.org/10.1090/tran/6911
