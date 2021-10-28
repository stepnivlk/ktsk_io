+++
title = "MU123 Unit 10 Notes"
date = 2021-06-30
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
+++

# Introduction
Equation of the form:
$$
y = ax^2 +bx + c
$$
where $a$, $b$ and $c$ are constants with $a \ne 0$, are examined in this unit.
The *RHS* is a quadratic expression and graphs of these equations have a curved shape called *parabola*.

# 1 Introducing parabolas
## 1.1 Parabolas everywhere
### The free-fall equation
The relationship between the distance $d$ fallen by an object and the time $t$ that it has been falling is given by
$$
d = \frac{1}{2}gt^2
$$
where the constant $g$ is the acceleration  due to gravity, which is about $9.8 \text{m/s}^2$.
Or more compactly:
$$
d = 4.9t^2
$$

**Parabola** - a part of a parabola is formed by curved shape in the free-fall equation.
**Parabolic curve** - a curve whose shape is all or part of a parabola.

#### Definitions of a parabola
* A shape obtained when a plane "parallel" to the side of a cone intersects the cone.
* A shape of the graph of any equation of the form:
$$
y = ax^2 +bx + c
$$
where $a$, $b$ and $c$ are constants with $a \ne 0$. The free-fall equation has this form with $b = c = 0$.

The free-fall equation is only a **model** for the motion of a falling object. It's accurate when there are no other forces than gravity acting on the object.
In real life there actually are other forces, notably *air resistance* (*drag*) which slows down the falling object. After great enough distance the air resistance will cause the speed of falling object to stop increasing - to become constant. This is known as the *terminal velocity*.

**Quadratic model**
Any model based on an equation of form $y = ax^2 +bx + c$.

## 1.2 Projectiles
An object that is propelled through space by a force that ceases after launch.
**Trajectory** is the path a projectile follows.
**Ballistics** is the science of projectiles.

## 1.3 Stopping distances

# 2 Graphs of quadratic functions
Every parabola has an **axis of symmetry** cutting the parabola at exactly one point - the **vertex**.
A rule that takes input values and produces output values is called a **function**.

A function of the form $y = ax^2 + bx + c$ is called a **quadratic function**.

## 2.1 Graphs of equations of the form $y = ax^2$
The **magnitude** of $a$ affects how narrow the graph is. The larther the magnitude of $a$, the narrower the parabola becomes.

* **u-shaped** parabola is same way up as the graph of $y = x^2$.
* **n-shaped** parabola is the another way up, e.g. $y = -x^2$.

The vertex is $(0, 0)$.

## 2.2 Graphs of equations of the form $y = ax^2 + bx + c$
The graph has the same shape as the graph of $y = ax^2$, but shifted and crosses the $y$-axis at $(0, c)$.

## 2.3 The intercepts of a parabola
The graph of $y = ax^2 + box + c$ can have two, one or zero $x$-intercepts. There is always exactly one $y$-intercept.

## 2.4 Sketch graphs of quadratic functions
1. Find whether the parabola is u-shaped or n-shaped.
2. Find its intercepts, axis of symmetry and vertex.
3. Plot the features found, and hence sketch the parabola.
4. Lable the parabola with its equation, and make sure that the values of the intercepts and the coordinates of the vertex are indicated.

A formula for the axis of symmetry of a parabola with equation $y = ax^2 + bx + c$ is:
$$
x = - \frac{b}{2a}
$$

# 3 Solving quadratic equations

## 3.2 The quadratic formula
The solutions of the quadratic equation
$$
ax^2 + bx + c = 0
$$
are given by
$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

### Simplifying a quadratic equation
* If the coeficient of $x^2$ is negative, then multiply the equation through by $-1$ to make this coefficient positive.
* If the coefficients have a common factor, then divide the equation through by this factor.
* If any of the coefficients are fractions, then multiply the equation through by a suitable number to clear them.

## 3.3 The number of solutions of a quadratic equation
The value $b^2 - 4ac$ is called the **discriminant** of the quadratic expression $ax^2 + bx + c$. Such an equation has:
* two solutions if $b^2 - 4ac > 0$ (the discriminant is positive).
* one solution if $b^2 - 4ac = 0$ (the discriminant is zero).
* no solutions if $b^2 - 4ac < 0$ (the discriminant is negative).

## 3.4 Vertically-launched projectiles
If an object is launched upwards from an initial height $h_0$ with an initial speed $v_0$, then after time $t$ its height $h$ is given by
$$
h = -\frac{1}{2}gt^2 + v_0t + h_0
$$
where $g$ is the acceleration due to gravity, which is about $9.8\text{m}/\text{s}^2$.

# 4 Completing the square
Is a way to rearrange a quadratic expression.

## 4.1 Shifting parabolas
If a parabola with equation $y = ax^2$ is shifted right by $h$ units and up by $k$ units, then each point $(x, y)$ on the second parabola is a shift of the point $(x - h, y - k)$ on the first parabola. Hence the formula for second parabola is:
$$
y - k = a(x - h)^2
$$
Or equivalently:
$$
y = a(x - h)^2 + k
$$
Which can be further multiplied out to give the usual form $y = ax^2 + bx + c$.
Importantly the process works vice-versa too. Any equation of the form $y = ax^2 + bx + c$ where $a$, $b$ and $c$ are constants with $a \ne 0$, can be rearranged into the form $y = a(x - h)^2 + k$.

Every expression of the form $ax^2 + bx + c$, where $a \ne 0$, can be rearranged into the form
$$
a (x + \text{a number})^2 + \text{a number}
$$
where each of the two numbers in this expression can be positive, negative or zero.
This is called the **completed-square form**.

The parabola with equation
$$
y = a(x - h)^2 + k
$$
has vertex $(h, k)$.

## 4.2 Completing the square in quadratics of the form $x^2 + bx + c$
Where the coefficient of $x^2$ is 1 - the completed-square form looks like:
$$
( x + \text{a number} ) ^2 + \text{a number}
$$

### Completing the square in quadratics of the form $x^2 + bx$
In general:
$$
(x + p)^2 = x^2 + 2px + p^2
$$
The RHS expression is of the form $x^2 + bx$ plus an extra number. If I subtract this extra number from both sides and swap the sides, then I obtain:
$$
x^2 + 2px = (x + p)^2 - p^2
$$
The RHS expression is the completed-square form of the LHS expression with following properties:
* Constant term in the RHS bracket is half of the coefficient of the term in $x$ on LHS.
* The number that is subtracted on the RHS is the square of the constant term in the brackets.

### Completing the square in quadratics of the form $x^2 + bx + c$
1. Complete the square for the $x^2$ and $x$ terms as before.
2. Collect the constant terms.

E.g.:
$$
\begin{aligned}
x^2 + 8x + 10 = \\\\[0.6em]
(x + 4)^2 - 16 + 10 = \\\\[0.6em]
(x + 4)^2 - 6
\end{aligned}
$$

Hence the general strategy:
1. Rewrite the expression with the $x^2 + bx$ part changed to $(x + p)^2 - p^2$, where the number $p$ is half of $b$.
2. Collect the constant terms.

## 4.3 Solving quadratic equations by completing the square
1. Equations, where the coefficient of $x^2$ is greated than 1, should be divided through by given coefficient.
2. Complete the square.
3. Rearrange the equation so the square term and the constant are on different sides.
4. Take the square root of both sides.
5. Rearrange the equation to obtain $x$ by itself on one side.

### The derivation of the quadratic formula
The general quadratic equation $ax^2 + bx + c = 0$ can be rearranged to obtain $x$ by itself on the LHS by following the steps:

Divide through by the coefficient of $x^2$:
$$
x^2 + \frac{b}{a}x + \frac{c}{a} = 0
$$
Complete the square:
$$
(x + \frac{b}{2a})^2 - \frac{b^2}{4a^2} + \frac{c}{a} = 0 \\\\[1em]
$$
Get the constant terms on the right, combine them into a single fraction:
$$
\begin{aligned}
(x + \frac{b}{2a})^2  &=  \frac{b^2}{4a^2} - \frac{c}{a} \\\\[1em]
&= \frac{b^2}{4a^2} - \frac{4ac}{4a^2} \\\\[1em]
&= \frac{b^2 - 4ac}{4a^2}
\end{aligned}
$$
Take the square root of both sides:
$$
\begin{aligned}
x + \frac{b}{2a} &= \pm \sqrt{\frac{b^2 - 4ac}{4a^2}} \\\\[1em]
&= \pm \frac{\sqrt{b^2 - 4ac}}{2a}
\end{aligned}
$$
Get $x$ by itself on the LHS:
$$
\begin{aligned}
x &= -\frac{b}{2a} \pm \frac{\sqrt{b^2 - 4ac}}{2a} \\\\[1em]
&= \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
\end{aligned}
$$
This is the quadratic formula!

## 4.4 Completing the square in quadratics of the form $ax^2 + bx + c$
The common factor of $x^2$ and $x$ can be taken out of present, e.g.:

$$
2x^2 + 8x -7 = 2(x^2 +4x) - 7
$$

Then the square in the qudratic *inside the brackets* can be completed as usual.

When there is no common factor, the coefficient of $x^2$ can still be taken out, the process will create fractions though:

$$
2x^2 + 5x + 1 = 2(x^2 + \frac{5}{2}x) + 1
$$

### Strategy to complete the square in a qudratic of the form $ax + bx + c$
1. Rewrite the expression with the coefficient $a$ of $x^2$ taken out of the $ax^2 + bx$ part as a factor. This generates a pair of brackets.
2. Complete the square in the simple quadratic inside the brackets, remembering to keep it enclosed within its brackets. This generates a second pair of brackets, inside the first pair.
3. Multiply out the *outer* brackets.
4. Collect the constant terms.

# 5 Maximisation problems
Is the problem of finding the maximum value of a quantity and the circumstances under which it is obtained.

This section focuses on problems that can be modelled with a quadratic function, hence the solution is to find a vertex.

### Methods to find the vertex of a parabola from its equation
* Use the formula $x = -b / (2a)$ to find the $x$-coordinate, then substitute into the equation of the parabola to find the $y$-coordinate
* Find the $x$-intercepts (if there are any); then the value halfway between them is the $x$-coordinate of the vertex. Find the $y$-coordinate by substituting into the equation of the parabola.
* Complete the square: the parabola with equation $y = a(x - h)^2 + k$ has vertex $(h, k)$.
* Plot the parabola and read off the approximate coordinates of the vertex.

### Strategy to solve a maximisation problem
1. Identify the quantity to be maximised and the quantity that it depends on, and denote each quantity by a variable.
2. Find a formula for the variable to be maximised in terms of the variable that it depends on.
3. If this gives a quadratic function, then find the vertex of its graph.