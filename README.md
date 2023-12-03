---
Name: Siddharth Nachaloor
Topic: 1D unconstrained optimization algorithms. Parabolic interpolation, Newton's method, etc. How they work, rates of convergence, why they work, pros and cons of the various different methods.
Title: A Closer Look at How Optimization Methods Work
---
# Optimization

## Table of Contents
- [Introduction](#Overview)
- [Background](#Background)
- [Penalty Function Method Overview](#Penalty-Function-Method-Overview)
- [Common Applications](#Common-Applications)
- [Formulation](#Formulation)
- [Penalty Function Options](#Penalty-Function-Options)
- [References](#References)

## What is Optimization?
Optimization is all about finding the maximum or minimum of a function depending on the problem. There may or may not be an added constraint for these problems. When dealing with optimization, you are usually dealing with interesting points in a scenario. It's akin to finding the best or worst case scenario of a situation. 

How would we go about doing this? Well, let's say we have the area of a rectangle modeled by $f(x) = ab$, where a and b are the length and width of the rectangle. Then, let's say we are also interested in the perimeter of the rectangle, which can be modeled by $g(x) = 2a + 2b$. If we wanted to maximize the perimeter, given that the area has to equal 60, what would a and b have to be? This is considered an optimization problem. 

To solve optimization problems, you must set the derivative of the function equal to 0. This will give you the max or min of the function since the slope of the tangent line at that point would be 0. Let's do that for this example:

Since ab = 60, b = 60/a. We will plug this into our perimeter equation:


$g(a) = 2a + 120/a$\
$g'(a) = 2 - 120/a^2$


Setting this to 0 we get:

$g'(a) = 2 - 120/a^2 = 0$\
$2 = 120/a^2$\
$2a^2 = 120$\
$a^2 = 60$\
$a = sqrt(60) \approx 7.746$


Now that we know a, let's plug that into the equation for b:

$b = 60/a = 60/7.746 = 7.746$

So, we now know that the maximum perimeter is $g(7.746, 7.746) = 2(7.746) + 2(7.746) = 30.984$. The area is $f(7.746, 7.746) = (7.746)(7.746) = 60$.

This is just one, simple example of optimization. There's so much more to explore!

## 1D Unconstrained Optimization and Parabolic Interpolation
Unconstrained Optimization is when all feasible point, which are in a Constraint set S, is just all real numbers. It means there are no specific values that x is limited to. For the previous example, the rectangle area equaling 60 acted as a constraint for the perimeter function. We will be focusing on unconstrained optimization for the remainder of this article.

Functions might also have min and maxes in certain ranges, that are not the min or max in the entire range of the function. These are local extrema. Local optimization deals with finding the x's that are local minima or maxima. Global Optimization deals with finding the x's that are global minima or maxima.

The main thing is to set the derivative (or gradient) equal to 0 to find the extrema of a function. The global ones are harder to find, but nonetheless we use several methods to find these critical points.

1D (or one dimensional) optimization is optimization of functions of one variable. We can tell whether the function is unimodal on an interval if the function is first strictly decreasing then strictly increasing after a certain x* value. It can also go from decreasing to increasing. This x* value is a critical point. 

Parabolic Interpolation involves fitting a parabolic function to a polynomial. It starts with using three function values to estimate a parabola. For example, you can use some start point x = a, then y = b, and z = c, where b is the midpoint between a and c. You can use any three points, but this is a good start. After that, you take the minimum of the quadratic formed by the three points as the new minimum of the function. This new minimum replaces the oldest point chosen. This counts as 1 iteration.

An iteration is the nth time doing a process. Usually, the more iterations, the more accurate the optimization method can get. We usually repeat iterations until some convergence criteria is met. This could be an error estimate near 0.

General idea of Optimization:

$$
\begin{align}
\ f'(x) = 0 \\
\end{align}
$$

to get critical points of f(x).

Let's take a look at Newton's method, a popular optimization method:

![](general_iteration.PNG)

**Newton's Method** [1]
1. XXXX
2. XXXX
3. XXXX
4. XXXX
5. XXXX

XXXXXXX
![](global_local.PNG)

XXXXX


## Other algorithms for Unconstrained Optimization (Steepest Descent Method, Secant Method, etc.)
XXXX included in the [Formulation](#Formulation) Section.

XXXX is shown below [2]:

![](exterior_vs_interior.PNG)

In the BLANK method, XXXX a necessary feature of the solution method [2].

## Another Algorithm
XXXX

$$
\begin{align}
\phi(x,r) = f(x) + P(h(x),g(x),r) \\
\end{align}
$$

where XXXX $f(x)$ value.

**Other Algorithm** [1]
1. Start with an initial design point, **$x_0$**
2. Set the initial penalty parameter, **$p_0$**
3. Determine which constraints are violated given the current design variable values
4. Construct **$\phi(x,r)$** using the current design variables and penalty parameter
5. Find search direction as **$d_i = \nabla \phi(x,r)$**
6. Express the new design variables in terms of step length (still unknown) and search direction: $x_{i+1} = x_i + \alpha * d_i$
7. Substitute this expression into **$\phi(x,r)$** and find a step size to minimize phi using any unconstrained optimization method
8. Substitute the found step size into the expression for $x_i$ to find new design variable values
9. Update the penalty parameter as $r_{k+1} = C * r_i$ where C is a constant
10. Repeat until optimum is reached

The above iterative process ends when none of the constraints are violated. As a result, this method doesn’t necessarily find interior extremes, but rather just extremes that occur on the boundary between the feasible and infeasible regions. Whether the algorithm converges on a result (and how fast this convergence occurs) is dependent on the choice of penalty function. A comparison of choices for penalty functions and more detail on steps three and four are given in the following section, [Penalty Function Options](#Penalty-Function-Options).

This process is often put into practice in code, as several iterations are necessary to reach the feasible region:

```
$$
x_i = x_0
p_i = C*f(x_i)				{Where C is between 1.1 and 2.0)
while h(x_i) >= 0, g(x_i) \= 0		{While constraints are violated}
  P(h,g,r) =penalty function		{Construct chosen penalty function}
  phi = f + P
  d = gradient(phi) @ x_i
  x_new = x_i + alpha*d			{Write x_new symbolically}
  phi = phi(x_new)			{Plug symbolic representation into phi}
  alpha* = solve(diff(phi) = 0)		{Solve to minimize pseudo-objective function}
  x_new = x_new(alpha*)			{Update design variables}
  r_new = C*r_i				{Update penalty parameter}
end
$$
```

## Real-life Applications
XXXXX

XXX used in combination with [genetic algorithms](https://towardsdatascience.com/introduction-to-genetic-algorithms-including-example-code-e396e98d8bf3) to XXXX and robustness [9,10].

### Beyond 1D Optimization; What's the next step?
XXXXX

XXXXX


XXXX

> *Theorem:* Let $x_k$ be a sequence generated by the quadratic exterior penalty method. Then, any limit point of the sequence is a solution to the inequality constrained minimization problem  [14].

Note that this indicates the final solution will satisfy the constraints as the number of iterations approaches infinity, not that it will necessarily be the optimum solution available on the edge of the feasible region. Commenting on the optimality of the limit point is more challenging, and requires additional assumptions about the chosen tolerances and penalty parameters for the given problem [13]. We can additionally note that conditioning of this problem is given by the Hessian of $\phi$. This provides the needed justification for the use of an increasingly large penalty parameter in order to avoid an ill-conditioned problem.

### Adaptive Penalty Function
This type of penalty function incorporates even more information about the iterative process, using knowledge of the ongoing success of the solver. The search for an optimal solution can be divided into intervals over $N_f$ generations. Whether or not the best solution was found in the previous interval informs the value of the next penalty function multiplier, $\lambda$, using constants, $\beta_1$ & $\beta_2$, guiding the search towards attractive regions or away from areas that have already been searched for an optimum [11].

$$
\begin{align}
P = \sum_{i=1}^m \lambda_k d_i^k \\
\lambda_{i+1} = \lambda_k \beta_1 \ if \ previous \ interval \ has \ infeasible \ best \ solution\\
\lambda_{i+1} = \lambda_k / \beta_2 \ if \ previous \ interval \ has \ feasible \ best \ solution\\
\lambda_{i+1} = \lambda_k \ otherwise\\
\end{align}
$$


## References (APA)

1. XXXX
2. XXXX
3. XXXX
4. XXXX
5. XXXX
6. XXXX
7. XXXX
8. XXXX
9. XXXX
10. XXXX
11. XXXX
12. XXXX
13. XXXX
14. XXXX
