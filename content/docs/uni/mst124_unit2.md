+++
title = "MST124 Unit 2 - Graphs and equations"
date = 2021-10-30
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
+++

# Introduction
**Mathematical modelling** is the use of mathematics to represent and study real-life situations.

# 1 Plotting graphs
## 1.2 Graphs of equations
A point $(x, y)$ is said to **satisfy** an equation if the equation is true for the point's values of $x$ and $y$.

A collection of points that satisfy an equation does not change when the equation is rearranged.

If the equation has the property that it can be rearranged to express $y$ as a formula in terms of $x$ then the line or curve is called the **graph**.

**Line segment** is a finite part of a line forming graph of an equation.

# 2 Straight-line graphs
## 2.1 Gradients and intercepts of straight lines
### Gradients
A line that slopes *up* from left to right has a positive gradient.
A line that slopes *down* from left to right has a negative gradient.
The greater the **magnitude** of the gradient of a line, the steeper the line.

### Calculating gradients
The gradient of the straight line through the points $(x_1, y_1)$ and $(x_2, y_2)$, where $x_1 \ne x_2$, is given by
$$
\text{gradient} = \frac{rise}{run} = \frac{y_2 - y_1}{x_2 - x_1}
$$

Gradient of a horizontal line is $0$, gradient of vertical line is undefined.

### Intercepts
**x-intercept** is the value of $x$ where a line crosses the $x$-axis.
**y-intercept** is the value of $y$ where a line crosses the $y$-axis.

## 2.2 Straight lines and their equations
For any value of $m$, the points $(x, y)$ that satisfy the equation $y = mx$ are the points that lie on the straight line through the origin with gradient $m$.

For any constant $c$ the graph of the equation $y = mx + c$ is obtained by moving the graph of the equation $y = mx$ vertically by $c$ units.

Hence, the graph of the equation $y = mx + c$ is the straight line with gradient $m$ and $y$-intercept $c$.

**Linear equation** is any equation that can be rearranged into the form of $y = mx + c$.

### Equations of horizontal and vertical lines
Horizontal line with $x$-intercept $c$ has gradient $0$ and equation $y = 0x + c$; thus $y = c$.

Vertical line doesn't have gradient, thus doesn't have an equation of the form $y = mx + c$. However, every point on a vertical line has the same $x$-coordinate so the line has an equation of the form $x = d$. The constant $d$ is the $x$-intercept.

The equation of the $x$-axis is $y = 0$ and the equation of the $y$-axis is $x = 0$.

### Drawing a line from its equation
The formula for gradient is
$$
m = \frac{y - y_1}{x - x_1}
$$
Hence the equation of the straight line with gradient $m$ that passes through the point $(x_1, y_1)$ is
$$
y - y_1 = m(x - x_1)
$$

## 2.3 Parallel and perpendicular lines
Two straight lines are **parallel** if they never cross, even when extended infinitely far in each direction. Such lines have **same gradient**.

Two lines are **perpendicular** if they are at right angles to each other.

### Gradients of perpendicular lines
The gradients of any two perpendicular lines (not parallel to the axes) have product $-1$.

If two perpendicular lines are parallel to the axes, then one of them is parallel to the $y$-axis and hence has undefined gradient.

## 2.4 Applications of straight-line graphs
**Linear** model is a model that has an equation $y = mx + c$ and thus can be be represented using straight-line graph.

The gradient of the graph is the **rate of change** of the quantity on the vertical axis **with respect to** the quantity on the horizontal axis.

# 3 Intersection of lines
**Point of intersection** is a point at which two lines cross.

## 3.2 Solving simultaneous equations
### Substitution method
#### Strategy
1. Rearrange one of the equations, if necessary, to obtain a formula for one unknown in terms of the other.
2. Use the formula to substitute for this unknown in the other equation.
3. You now have an equation in one unknown. Solve it to find the value of that unknown.
4. Substitute this value into an equation involving both unknowns to find the value of the other unknown.

### Elimination method
#### Strategy
1. Multiply one or both of the equations by suitable numbers, if necessary, to obtain two equations that can be added or subtracted to eliminate one of the unknowns.
2. Add or subtract the equations in one unknown. Solve it to find the value of that unknown.
3. You now have an equation in one unknown. Solve it to find the value of that unknown.
4. Substitute this value into an equation involving both unknowns to find the value of the other unknown.

## 3.3 The number of solutions of simultaneous equations
 If the two lines have different gradients then they intersect at a single point.
 If the two lines have the same gradient but different $y$-intercepts then they are parallel and hence do not intersect.
 If the two lines have the same gradient and the same $y$-intercept then the graphs of the two equations are identical and hence there are infinitely many solutions.
 
 # 4 Quadratics
 Quadratic equation is an equation of the form
 $$
 y = ax^{2}+ bx + c
 $$
 where $a$, $b$ and $c$ are constants and $a \ne 0$.
 
 ## 4.1 Quadratic graphs
 **Parabola** is the shape of quadratic equation.
 If $a$ is positive then the parabola is **u-shaped**.
 if $a$ is negative then the parabola is **n-shaped**.
 In both cases, the parabola has a vertical *axis of symmetry*.
 The **vertex** is the lowest point on the u-shaped parabola and the highest point on the n-shaped parabola.
 
 A parabola can have two, one or no $x$-intercepts. There is always exactly one $y$-intercept because there is always exactly one value of $y$ for each value of $x$.
 
 ## 4.2 Factorising quadratic expressions
 **Factorisation** is a process of writing a quadratic as a product of two linear expressions.
 
 ### Factorising quadratics in which $x^2$ has coefficient 1
 #### Strategy
 1. Start by writing
$$
x^{2}+ bx + c = (x ~~~~~)(x ~~~~~)
	$$
2. Find the factor pairs of $c$ (including both positive and negative factors).
3. Choose a factor pair with sum $b$.
4. Write your factor pair $p$, $q$ in position:
$$
x^{2}+bx+c=(x +p)(x + q)
	$$
	
### Factorising quadratics in which $x^2$ doesn't have coefficient 1
#### Strategy
1. Take out any numerical common factors. If the coefficient of $x^2$ is negative, also take out the factor $-$. Then apply the steps bellow to the quadratic inside the brackets.
2. Find the positive factor pairs of $a$, the coefficient of $x^{2}$. For each such factor pair $d$, $e$ write down a framework $(dx~~~~~)(ex~~~~~)$.
3. Find all the factor pairs of $c$, the constant term (including both positive and negative factors).
4. For each framework and each factor pair of $c$, write the factor pair in the gaps in the framework in both possible ways.
5. For each of the resulting cases, calculate the term in $x$ that you obtain when you multiply out the brackets.
6. Identify the case where this term is $bx$, if there is such a case. This is the required factorisation.

### Quadratics with no constant term
Can be factorised by taking out $x$ as a common factor, e.g.:
$$
x^{2}+ 4x = x(x + 4)
$$

### Difference of two squares
Is an expression of the form $A^{2}- B^2$ where $A$ and $B$ are subexpressions. This expression can easily be factorised as:
$$
A^{2}- B^{2} = (A + B)(A - B)
$$

## 4.3 Solving quadratic equations by factorisation
### Simplifying a quadratic equation
* If necessary, rearrange the equation so that all the non-zero terms are on the same side.
* If the coefficient of $x^2$ is negative, then multiply the equation through by $-1$ to make this coefficient positive.
* If the coefficients have a common factor, then divide the equation through by this factor.
* If any of the coefficients are fractions, then multiply the equation through by a suitable number to clear them.

Then the equation can be solved using factorisation (if possible) and using the fact that if product of two or more numbers is 0, then at least one of the numbers must be 0.

A quadratic equation with only one solution is said to have a **repeated solution**.

## 4.4 Expressing a quadratic in completed-square form
The **complete square form** of a quadratic $ax^{2} + bx + c$ is
$$
a(x + r)^{2} + s
$$
where $a$, $r$ and $s$ are constants.

### Completing the square in a quadratic
#### Of the form $x^{2}+ bx$
1. Write down $(x~~~~~)^2$, filling the gap with the number that's half of $b$, the coefficient of $x$ (including its $+$ or $-$ sign).
2. Subtract the square of the number that you wrote in the gap.

#### Of the form $x^{2}+ bx + c$
1. Use the earlier strategy to complete the square in the subexpression $x^{2} + bx$.
2. Collect the constant terms.

#### Of the form $ax^{2} + bx + c$, where $a \ne 1$
1. Rewrite the quadratic with the coefficient $a$ taken out of the expression $ax^2 + bx$ as a factor. This generates a pair of brackets.
2. Use the earlier strategy to complete the square in the simple quadratic inside the brackets. This generates a second pair of brackets, inside the first pair.
3. Multiply out the *outer* brackets.
4. Collect the constant terms.

## 4.6 The quadratic formula
The solutions of the quadratic equation $ax^{2} + bx + c = 0$ are
$$
x = \frac{ -b \pm \sqrt{b^{2} - 4ac} }{2a}
$$

## 4.7 The number of solutions of a quadratic equation
A quadratic equation can have two, one or zero solutions that are real numbers. Those are known as *real solutions*.

The value of the expression $b^{2} - 4ac$ in the quadratic formula is called **discriminant** and determines how many solution a quadratic equation has.

### The number of real solutions of a quadratic equation
The quadratic equation $ax^{2} + bx + c = 0$ has:
* two real solutions if $b^{2} - 4ac > 0$  (the discriminant is positive)
* one real solution if $b^{2} - 4ac = 0$ (the discriminant is zero)
* no real solution if $b^{2} - 4ac < 0$ (the discriminant is negative). 

## 4.9 Sketching quadratic graphs
### Properties of the graph of $y = ax^{2} + bx + c$, where $a \ne 0$
1. The graph is a parabola with a vertical axis of symmetry.
2. If $a$ is positive it is u-shaped; if $a$ is negative it is n-shaped.
3. It has two, one or no $x$-intercepts.
4. It has one $y$-intercept.

### To sketch the graph of $y = ax^{2} + bx + c$, where $a \ne 0$
1. Find whether the parabola is u-shaped or n-shaped.
2. Find its intercepts, axis of symmetry and vertex.
3. Plot the features found, and hence sketch the parabola.
4. Label the parabola with its equation, intercepts and the coordinates of the vertex.