+++
title = "MU123 Unit 13 Notes"
date = 2021-08-05

[taxonomies]
categories = ["uni", "math"]
+++


# Introduction
Exponential growth or decay happens when the numbers increase or decrease by the same factor at each stage.

# 1 Exponential growth and decay
## 1.1 Doubling and halving
Exponential growth is growth that arises by repeated multiplication by the same number.
**Starting number** is a number that is started with.
**Scale factor** is a multiplier.
For exponential growth, the scale factor must be greater than 1.

In general, if the starting value is $a$ and the scale factor $b$ then:
* The initial value is $a$
* After 1 step, the value is $a \times b = ab$
* After 2 steps, the value is $a \times b \times b = ab^2$
* After 3 steps, the value is $a \times b \times b \times b = ab^3$

Hence after $n$ steps, the value is $ab^n$.

## 1.2 Multiplying by a scale factor

## 1.3 Discreete and continuous exponential growth and decay
A variable $y$ is said to **change exponentially** with respect to a variable $x$ if the relationship between $x$ and $y$ is given by an equation of the form
$$
y = ab^x
$$
where $a$ and $b$ are positive constants, with $b$ not equal to $1$.

If $b > 1$, then $y$ **grows exponentially**.
If $0 < b < 1$, then $y$ **decays exponentially**.

If the change happens in steps ($x$ takes values from a range of equally spaced numbers, such as the non-negative integers), then it is **discreete exponential change** (also called **geometric change**).

If the change happens continuosly ($x$ takes values from an interval of real numbers, such as the non-negative real numbers), then it is **continuous exponential change**.

The curve formed by exponential equation $y = ab^x$ is called an **exponential curve**.

## 1.4 Using continuos exponential models

## 1.5 Exponential models from data
**Linear regression** is the process of fitting the best straight line to a set of data points.
**Exponential regression** is similar process used to fit the best exponential curve to a set of data points.

# 2 Working with exponential growth and decay
## 2.1 Growth and decay to particular sizes
## 2.2 Growth and decay over different lengths of time
**Discrete exponential change over different numbers of steps.**
Suppose that a quantity changes by the scale factor $b$ at each step.
Then every $i$ steps it changes by the scale factor $b^i$.

**Continuous exponential change over different time periods**
Suppose that a qunatity is subject to continuous exponential change by the scale factor $b$ every year.

Then over any time interval of length $i$ years, it changes by the scale factor $b^i$.

(The same is true if time is measured in any other unit, such as weeks, days or minutes.)

# 3 Exponential curves
TODO(p24): Check Unit 3
## Graphs of equations of the form $y = ab^x$
* If $a > 0$ then the graph lies entirely above the $x$-axis. If also
	* $b > 1$, then the graph is an exponential growth curve
	* $0 < b < 1$, then the graph is an exponential decay curve
	* $b = 1$, then the graph is a horizontal line
* If $a < 0$ then the graph lies entirely below the $x$-axis and is neither an exponential growth curve nor an exponential decay curve
* The $x$-axis is an asymptote (except when $a = 0$ or $b = 1$)
* The $y$-intercept is $a$
* The closer the value of $b$ is to $1$ (and the closer the value of $a$ is to $0$) the flatter is the graph

## 3.3 Euler's number $e$
Irrational number usually denoted by letter $e$, approximately $2.71828...$.
When $e$ is a value on of $b$ in exponential function then the gradient of $1$ is given at $(0, 1)$.

# 4 Logarithms
Equations like
$$
170 \times 1.23^t = 7~000~000~000
$$
where the unknown is in an exponent, are known as **exponential equations**.
Solving such an equation involves the use of *logarithms*, (*logs* for short).

## 4.1 A brief history of logarithms
Logarithms were invented by John Napier in 16th century to solve the problem of multiplication and division of large numbers in astronavigation.

He used the $a^m \times a^n = a^{m + n}$ law to turn multiplication problem into addition one. 

So, in ordert to multipy e.g. 287 and 37 the numbers need to be rewritten as a common base to a power of something:
$$
287 \times 37 \approx 10^{2.4579} \times 10^{1.5682} \\\\
= 10^{2.4579 + 1.5682} \\\\
= 10^{4.0261} \\\\
\approx 10619
$$

However, there is still problem of finding the correct powers of ten for the numbers to be multiplied, and of turning the power of ten obtained as the answer back into an ordinary number.

The problem was solved by drawing up sets of tables to be used whenever such calculation arised. The tables gave the power of ten corresponding to each number that might need to be multiplied - called the **logarithms** of the numbers.

The tables were also used to find the ordinary number corresponding to each ower - **antilogarithms** of the powers.

## 4.2 Logarithms to base 10
As mentioned, the logarithm of a number is the power to which 10 must be raised to give the number. Such logarithms are called **logarithms to base** since 10 has been chosen as the base.

Logarithms to base 10 are also called **common logarithms**.

Following common logarithm (in mathematical notation):
$$
\log_{10}100 = 2
$$
is described as "the logarithm to base 10 of 100 equals 2".

It also applies that following statements
$10^2 = 100$ and $\log_{10}100 = 2$
are equivalent.

In summary, **logarithms to base 10** of a number $x$, denoted by $\log_{10}x$, is the power to which you have to raise $10$ to get the answer $x$. 

The subscript 10 can be omitted when
* it is understood that a logarithm is a common logarithm.
* When the notation is used in an equation involing logarithms that is true no matter what the base is.

Raising 10 to a number and finding the logarithm of a number to base 10 are **inverse operations**.

## 4.4 Logarithms to other bases
The **logarithm to base** $b$ of a number $x$, denoted by $\log_bx$, is the power to which you have to raise the base $b$ to get the anser $x$. So the two equations
$x = b^y$ and $y = log_bx$
are equivalent.

Given that
* The base $b$ must be positive and not equal to 1.
* Only positive numbers have logarithms, but logarithsm themselves can be any number

Euler's number $e$ is often used as a base for logarithms, called **natural logarithms**. The notation $\ln$ is usually used in place of $\log_e$, hence, e.g. the natural logarithm of 5 is written as
$$
\ln5
$$

Hence the **natural logarithm** of a number $x$, denoted by $\ln x$, is the power to which you have to rase the base $e$ to get the answer $x$. So the two equations
$x = e^y$ and $y = \ln x$
are equivalent.

### Logarithm of the number one and logarithm of the base
For any base $b$,
$\log_b1=0$ and $\log_bb=1$

# 5 Working with logarithms
## 5.1 Three logarithm laws
### Rule for addition of logarithms
$$
\log x + \log y = \log(xy)
$$

#### Formal proof
Suppose that the numbers $x$ and $y$ can be written as $b^m$ and $b^n$, that is
$x = b^m$ and $y = b^n$
Then
$m = \log_bx$ and $n = \log_by$
The product $xy$ can be written as
$xy = b^m \times b^n = b^{m + n}$
This means that the power to which $b$ must be raised to give $xy$ is $m + n$, that is
$\log_b(xy) = m + n = \log_bx + \log_by$
which is the logarithm law above.

### Rule for subtraction of logarithms
$$
\log x - \log y = log (\frac{x}{y})
$$

#### Formal proof
$$
x = b^m ~~~ y = b^n \\\\[1em]
m = \log_bx ~~~ n = \log_by \\\\[1em]
\frac{x}{y} = \frac{b^m}{b^n} = b^{m - n} \\\\[1em]
\log_b(\frac{x}{y}) = m - n = \log_bx - \log_by \\\\
$$

### Rule for a multiple of a logarithm
$$
n \log x = \log (x^n)
$$

#### Formal proof
Suppose that
$$
x = b^m \\\\[1em]
m = \log_bx \\\\[1em]
$$
The power $x^n$ can be written as
$$
x^n = (b^m)^n = b^{m + n} \\\\[1em]
$$
Hence the power to which $b$ must be raised to give $x^n$ is $mn$, that is
$$
\log_b(x^n) = mn = n\log_bx
$$
Which is the logarithm law above.

## 5.2 Solving exponential equations by taking logs
Exponential equations is an equation where the unknown is in an exponent, e.g.
$$
170 \times 1.23^t = 7 000 000 000
$$

Basic procedure for solving such equations is to take the logarithm of both sides and then applying the logarithm law $\log(x^n) = n\log x$.

This method works the best when one side of the equation consists only of a number raised to an exponent containing unknown. An equation of different form shoud be rearranged.

### Logarithmic identity
$$
\ln(e^x) = x
$$
and
$$
e^{\ln x} = x
$$
These hold for bases other than $e$.

## 5.3 Doubling and halving times
For any quantity that is subject to continuous exponential growth over time, there will be a particular length of time in which its size always doubles. This length of time is called its **doubling time**.

A quantity that is subject to continous exponential decay has **halving time**.


### Summarized
Suppose that a quantity is subject to continuous exponential change by scale factor $b$ every year.
If the quantity grows (that is, if $b > 1$), then its doubling time in years is the solution $i$ of the equation
$$
b^i = 2
$$
If the quantity decays (that is, if $0 < b < 1$), then its halving time (half-life) in years is the solution $i$ of the equation
$$
b^i = \frac{1}{2}
$$

## 5.4 Graphs of logarithmic functions
A function with a rule of the form $y = \log_bx$ is called a **logarithmic function**.
A graph of the function $y = \log_bx$ is the inverse of $y = b^x$