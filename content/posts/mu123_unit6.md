+++
title = "MU123 Unit 6 Notes"
date = 2021-04-25

[taxonomies]
categories = ["uni", "math"]
+++

# Introduction
* Extends Unit 2 with connections between algebra and graphs.
* Explores relationships between two quantities.
* Relationships corresponding to straight lines only

# 1 Plotting graphs
* Useful to illustrate an equation or formula with two variables
	* Formula is an equation with a subject - a variable that appears by itself on one side of the equals sign and not at all on the other side.

## 1.1 Graph axes and coordinates
* Two axes - x and y.
* Aeach axis has scale markings and arrows.
* Distance between two consecutive integers on an axis is reffered to as 1 unit.
* Axis are often extended to include negative numbers.
* Each point plottend on a graph is represented by the **coordinates**.
	* First number represents position along the x-axis from 0
	* Second number position along the y-axis from 0
	* The two numbers are called *x*- and *y*-coordinates
	* Also known as the **Cartesian coordinate system**
	* Alternatives labels (and units) can be used too

## 1.2 Graphs of equations
When an equation, e.g.: $y = \frac{1}{2}x + 3$ is plotted into a line we say it's the **equation** of the line.
Checking whether some coordinates lie on the line $y = \frac{1}{2}x + 3$ is checking whether whether the coordinates of the point **satisfy** the equation.

In practical formulas, where variables are letters other than *x* and *y* the subject is known as the **dependent variable**. Its value depends on the value of th other, **independent variable**.
Indpendent variable should be on the horizontal axis and the depenedent on the vertical - **against** the independent variable.
In the table of values, the indendent variable should be in the first line.

Relationships plotted on straight line are called **linear relationships**.

## 1.3 Scatterplots
Is a graph plotted for two quantities for which I don't know an equation relating them. Plotted points are reffered to as **data points**.
When data points approximatelly form a straight line it can be modelled into it. For which an equation can be devised.

# 2 Characteristics of straight-line graphs
## 2.1 Gradient
Measures the steepnes of a line. Gradient of the line is the number of units it moves vertically as it moves 1 unit horizontally to the right.
Gradient is often not obvious to find. One approach is to pick two points on the line and consider what happens when "cursor" is moved from left-hand point to the right-hand point.
The increase in the:
* *x*-coordinate is called **run**.
* *y*-coordinate is called **rise**.

The gradient of the line can be calculated by dividing the rise by the run:
$$
\text{gradient} = \frac{\text{increase in y}}{\text{increase in x}} = \frac{\text{rise}}{\text{run}}
$$

> **The sign of the gradient**
> Lines that slope up from left to right have a *positive* gradient.
> Lines that slope down from left to right have a *negative* gradient.

Run (*x* increase) and rise (*y* increase) can be calculated by subtracting the respective coordinate of the left-hand point from the respective coordinate of the right-hand point.

Steepnes of a line depends not only on its gradient but also on the scales used on the axes.

### Horizontal and vertical lines
The gradient of every horizontal line is **zero** since the rise between any two points on a horizontal line is zero.
The gradient of every vertical line is **undefined** since the run is zero and it's not possible to divide any rise number by zero.

## 2.2 A formula for gradient
First point on the line can be represented as $(x_1, y_1)$ and second as $(x_2, y_2)$. 1, 2 are **subscripts**. Hence the gradient calculation can be generalised as:
$$
\text{gradient} = \frac{\text{rise}}{\text{run}} = \frac{y_2 - y_1}{x_2 - x_1}
$$
It doesn't matter which point I take to be $(x_1, y_1)$ and which $(x_2, y_2)$

**Paralel** are such lines that never cross, even when extended infinitely. Hence those lines have to have the same gradient (except for vertical lines with undefined gradient).

## 2.3 Interpreting gradients
Gradients for graphs that illustrate a relationship between real-life quantities should contain units in a form of *y*-unit / *x*-unit. When units are the same they cancel out so the gradient has no units.

The gradient can be thought of as the **rate of change** of *y* with respect to *x*.

To save time the units can be quoted in calculations e.g.:
$$
\frac{150}{6} = 25~\text{cm/day}
$$
That is not strictly correct though.

> **Interpreting the sign of the gradient of a graph**
> * A *positive* indicates that the quantity on the vertical axis *increases* as the quantity on the horizontal axis increases.
> * A *negative* indicates that the quantity on the vertical axis *decreases* as the quantity on the horizontal axis increases.
> * A *zero* indicates that the quantity on the vertical axis *remains constant* as the quantity on the horizontal axis increases.

## 2.4 Intercepts
The value on the axis scale where a straight-line graph one of the graph axes.
*x*-intercept is the value of *x* when *y = 0* and the *y*-intercept is the value of *y* when *x = 0*.

# 3 Equations of straight lines
## 3.1 Lines that pass through the origin
In general, each line that passes through the origin has the equation:
$$
y = \text{gradient} \times x
$$
With the exception of the vertical lines since it doesn't have a gradient.

The statement can be generalised as:
The straight line that passes through the origin and has gradient $m$ has equation $y = mx$.

## 3.2 Direct proportion
The relationship between two quantities when, if one quantity is multiplied or divided by a number then the second quantity is also multiplied or divided by same number.
E.g. number of miles is directly proportional to the equivalent number of kilometers.

If two quantities $x$ and $y$ are directly proportional to each other, then the relationship between them is described  by an equation of the form
$$
y = kx
$$
where $k$ is a non-zero number, known as the **constant of proportionality**.
The statement '$y$ is directly proportional to $x$' is sometimes written as
$$
y \propto x
$$

**Constant** in an equation or expression is a quantity that doesn't change when the values of the variables change.

A graph represents directly proportional quantities when it's a **straight line through the origin**. That means the constant of proprtionality is a gradient.

## 3.3 The general equation of a straight line
Nearly every straight line graph can be described by an equation of the form
$$
y = mx + c
$$
where gradient $m$ and $y$-intercept $c$ are constants. The exeception being vertical lines.


**Equations of horizontal and vertical lines**
The horizontal line with $y$-intercept $a$ has equation $y = a$.
The vertical line with $x$-interceept $a$ has equation $x = a$.

## 3.4 Drawing lines from their equations
When a graph illustrates an equation it should label the line.

## 3.5 Finding the equations of lines
1. Find the gradient $m$ of the line and substitute it into the general equation $y = mx + c$.
2. Substitute the coordinates of a point on the line into the equation of the line from step 1 and solve it fo find the value of the $y$-intercept $c$.
3. Use the values of $m$ and $c$ to write down the equation of the line.

# 4 Linear models from data
## 4.1 Regression lines
Collected data can be plotted on the graph and possibly modelled by straight line.
The way how a line fits the data can be meassured followingly:
* Measure the vertical distances from the points to the line
* Square each of these distances
* Add up the squared distances

The smaller the sum the better the fit of the line. There is always just one line for which the sum is the smallest - the **regression line**.

The process of estimating a value within the *range* of the data is called **interpolation**.
Estimating a value outside of the data *range* is called **extrapolation** and it can be unreliable. In general it is unwise to extrapolate too far from the range of dataset.

## 4.2 Correlation coefficients
Measures how accurate a prediction provided by a regression line is likely to be. It's calcluated from data pair and denoted by $r$.
It indicates how well the regression line fits the data pairs.
The coefficient is always between -1 and 1, inclusive.
When it's possitive the regression line has a positive gradient and it's called **possitive correlation**. Negative has a negative gradient and is called **negative correlation**.

The correlation coefficient is exactly 1 or exactly -1 when all the data points lie exactly on the regression line, it's called **perfect correlation**.
Strong correlation is when the data points are close to the regression line.
The closer the coefficient is to zero the **weaker** is the correlation.