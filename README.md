---
Name: Siddharth Nachaloor
Topic: 1D unconstrained optimization algorithms. Parabolic interpolation, Newton's method, etc. How they work, rates of convergence, why they work, pros and cons of the various different methods.
Title: A Closer Look at How Optimization Methods Work
---
# Optimization

## Table of Contents
- [What is Optimization](#Overview)
- [1D Unconstrained Optimization and Parabolic Interpolation](#Background)
- [Optimization Algorithms](#Penalty-Function-Method-Overview)
- [More Algorithms](#Penalty-Function-Method-Overview)
- [Real-life Applications](#Common-Applications)
- [What's the next step? Beyond 1D Optimization](#Formulation)
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

## Algorithms for Unconstrained Optimization (Newton's Method, Steepest Descent Method)

Let's take a look at Newton's method, a popular optimization method:

**Newton's Method**
1. Select initial guess $x_0$
2. Find $f(x_0)$
3. Find $f'(x_0)$
4. Find $f''(x_0)$
5. Find next guess $x_{k+1} = x_k - \frac{f'(x_0)}{f''(x_0)}$
6. Rinse and repeat with new $x$ until $f(x_k)$ doesn't change much

Let's do an example with $f(x) = \frac{x^3}{6} - x^2 + x$ and 3 iterations:\
We will try to find the local minimum with minimum guess $x_0 = 3$

This is our function and its derivatives:
$f(x) = \frac{x^3}{6} - x^2 + x$,\
$f'(x) = \frac{x^2}{2} - 2x + 1$, and\
$f''(x) = x - 2$

Newton's method provides the next term with the formula: $x_{n+1} = x_{n} - \frac{f'(x_{n})}{f''(x_{n})}$

Given $x_0 = 3$, we have
$f(3) = \frac{(3)^3}{6} - (3)^2 + (3) = 1.5$,\
$f'(3) = \frac{(3)^2}{2} - 2(3) + 1 = -0.5$, and\
$f''(3) = (3) - 2 = 1$

So, $x_{1} = 3 - \frac{-0.5}{1} = 3.5$

With $x_1 = 3.5$, we have
$f(3.5) = \frac{(3.5)^3}{6} - (3.5)^2 + (3.5) = -1.604$,\
$f'(3.5) = \frac{(3.5)^2}{2} - 2(3.5) + 1 = 0.125$, and\
$f''(3.5) = (3.5) - 2 = 1.5$

So, $x_{2} = 3.5 - \frac{0.125}{1.5} = 3.417$

With $x_2 = 3.417$, we have
$f(3.417) = \frac{(3.417)^3}{6} - (3.417)^2 + (3.417) = -1.609$,\
$f'(3.417) = \frac{(3.417)^2}{2} - 2(3.417) + 1 = 0.00347$, and\
$f''(3.417) = (3.417) - 2 = 1.417$

So, $x_{3} = 3.417 - \frac{0.00347}{1.417} = 3.414$

If $x_{3}$ is a local minima of $f(x)$, then $f'(x_{3}) = 0.$

$f'(x_{3}) = \frac{(3.414)^2}{2} - 2(3.414) + 1 = 3e-6 \approx 0$\
$f(x_{3}) = \frac{(3.414)^3}{6} - (3.414)^2 + (3.414) = -1.609$

Thus, the local minimum is $f(x) = -1.609$ and occurs at $x_{3} = 3.414$!

Steepest Descent Method
1. Find $\nabla f(x)$
2. Select initial guess $x_0$ 
3. Plug into $f(x)$
4. Find next guess $x_{k+1} = x_k - \alpha_k \nabla f(x_k)$
5. Rinse and repeat with new $x$ until $f(x_k)$ doesn't change much

## Other Algorithms

There are other algorithms that are used for optimization. Let's look at the Secant Method.

**Secant Method**
1. Select an initial guess, **$x_0$**
2. Select an initial guess, **$x_1$**
3. Plug in $x_0$ into $f'(x)$
4. Find new guess $x_{n+1} = x_n - f'(x_n)*\frac{x_n-x_{n-1}}{f'(x_n)-f'(x_{n-1}}$
5. Rinse and Repeat until you get close to 0.

The above process is similar to the previous methods we discussed. These optimization methods start with an intitial guess. They all go slightly towards the solution for each iteration until a convergence criteria is met.

This can be especially powerful when typed out in programming code, as that will allow the method to go through so many iterations.


## Real-life Applications
XXXXX

XXX used in combination with [genetic algorithms](https://towardsdatascience.com/introduction-to-genetic-algorithms-including-example-code-e396e98d8bf3) to XXXX and robustness [9,10].

## Beyond 1D Optimization; What's the next step?
XXXXX

XXXXX


XXXX

> *Theorem:* Let $x_k$ be a sequence generated by the quadratic exterior penalty method. Then, any limit point of the sequence is a solution to the inequality constrained minimization problem  [14].

Note that this indicates the final solution will satisfy the constraints as the number of iterations approaches infinity, not that it will necessarily be the optimum solution available on the edge of the feasible region. Commenting on the optimality of the limit point is more challenging, and requires additional assumptions about the chosen tolerances and penalty parameters for the given problem [13]. We can additionally note that conditioning of this problem is given by the Hessian of $\phi$. This provides the needed justification for the use of an increasingly large penalty parameter in order to avoid an ill-conditioned problem.

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
