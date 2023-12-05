---
Name: Siddharth Nachaloor
Topic: 22 - 1D unconstrained optimization algorithms. Parabolic interpolation, Newton's method, etc. How they work, rates of convergence, why they work, pros and cons of the various different methods.
Title: A Closer Look at How Optimization Methods Work
---
# Optimization

## Table of Contents
- [What is Optimization](#What-is-Optimization)
- [1D Unconstrained Optimization and Parabolic Interpolation](#1D-Unconstrained-Optimization-and-Parabolic-Interpolation))
- [Optimization Algorithms](#Algorithms-for-Unconstrained-Optimization-(Newton's-Method,-Steepest-Descent-Method))
- [More Algorithms](#Other-Algorithms)
- [Real-life Applications](#Real-life-Applications)
- [What's the next step? Beyond 1D Optimization](#What's-the-next-step?-Beyond-1D-Optimization)
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
4. Find new guess $x_{n+1} = x_n - f'(x_n)*\frac{x_n-x_{n-1}}{f'(x_n)-f'(x_{n-1})}$
5. Rinse and Repeat until you get close to 0.

The above process is similar to the previous methods we discussed. These optimization methods start with an intitial guess. They all go slightly towards the solution for each iteration until a convergence criteria is met.

This can be especially powerful when typed out in programming code, as that will allow the method to go through so many iterations.


## Real-life Applications
It's easy to look at these math problems I showed you, and think how is this useful in the real world? But it should be remembered that math can very easily be applied in situations. 

Let's say you are using an Uber in a big city. There are numerous other users who would be looking for an Uber as well. How does the app know which Uber to assign to each person. It is likely that it would be using optimization methods to find which drivers are closer to each person. It will also estimate times of arrival for each ride. Optimization can be applied in GPS systems to find the quickest route to a destination. This can also be applied in airports. The planes in an airport cannot occupy the same space for landing. This can be solved with optimization methods to make sure as many planes are on time and don't have other planes in their way. Optimization is also used extensively in the Supply Chain, Data, and Healthcare industries.

This website includes many other optimization applications I did not mention: [Optimization Applications](https://www.optimisationintherealworld.co.uk/).

## What's the next step? Beyond 1D Optimization 

This has been a cool discussion of Optimization, but what's next? 

For starters, you can explore 2D and higher-order optimization. There are complex algorithms out there to solve these kind of problems, and some that haven't been discovered yet! There is also constrained optimization, which is a large field on its own. With the rising popularity of AI and Machine Learning, there has been research on how Optimization is training neural networks, etc. There is so much more to explore in the field of optimization, as the real-world is your oyster!


## References
1. Admin. (2022, December 7). Secant method (definition, formula, steps, and examples). BYJUS. https://byjus.com/maths/secant-method/ 
2. Introduction to mathematical optimization - stanford university. (n.d.). https://web.stanford.edu/group/sisl/k12/optimization/MO-unit1-pdfs/1.1optimization.pdf 
3. Kovalev, L. (n.d.). Numerical methods with programming. Successive parabolic interpolation. https://drlvk.github.io/nm/section-parabolic-interpolation.html 
4. Mathematical Preparation for Finance. Softcover.io. (n.d.). https://www.softcover.io/read/bf34ea25/math_for_finance/multivariable_methods 
5. Method of Steepest Descent. Method of steepest descent. (n.d.). https://trond.hjorteland.com/thesis/node26.html 
6. Optimisation in the Real World. (2018, May 21). https://www.optimisationintherealworld.co.uk/ 
7. Optimization. Calculus I - optimization. (n.d.). https://tutorial.math.lamar.edu/classes/calci/optimization.aspx 
