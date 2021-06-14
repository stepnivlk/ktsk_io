+++
title = "MU123 Unit 9 Notes"
date = 2021-06-14

[taxonomies]
categories = ["uni", "math"]
+++

# 1 Number patterns and algebra
## 1.1 Arithmetic sequences
Sum of a sequence of natural numbers can be rewritten as a sum of pairs of numbers:
$$
1 + 2 + ... + 99 + 100 = (1 + 100) + (2 + 99) + ... + (50 + 51)
$$
There are 50 pairs, each of them having a sum of $101$, so:
$$
1 + 2 + ... + 99 + 100 = 50 \times 101 = 5050
$$

In case of a sum of successive odd numbers the sum is always the square of how many odd numbers I add, e.g. $1 + 3 + 5 + 7 = 16 = 4^2$ . For $n$ numbers the formula is $n^2$.

Formula for $n$ successive natural numbers is:
$$
1 + 2 + ... + n = \frac{1}{2}n(n + 1)
$$
The numbers given by the formula are called **triangular numbers**.

Any list of numbers is called a **sequence**
* $1, 2, 3, ..., 100$ is **finite** sequence
* $1, 2, 3, ...$ is **infinite** sequence

The numbers in a sequence are called the **terms** of the sequence.
**Arithmetic** sequence is a sequence where the **difference** between consequtive terms is constant, e.g.: $1, 2, 3, ...$ is a arithmetic sequence with difference of 1,
To specify an arithemtic sequence we can give the first term denoted by $a$, the difference denoted by $d$. If the sequence is finite the number of terms is denoted by $n$.

The $n$th term of an arithmetic sequence with first term $a$ and difference $d$ is given by the formula
$$
n\text{th term} = a + (n  - 1)d
$$

The number of terms $n$ of a finite arithmetic sequence with first term $a$, last term $L$ and non-zero difference $d$ is given by the formula:
$$
n = \frac{L - a}{d}  + 1
$$

The sum of the finite arithmetic sequence with first term $a$, difference $d$ and numbers of term $n$ is given by the formula:
$$
S = \frac{1}{2}n(2a + (n - 1)d)
$$
An alternative formula involving the last term $L$:
$$
S = \frac{1}{2}n(a + L)
$$

# 2 Multiplying out pairs of brackets
## 2.1 Pairs of brackets
> Strategy to multiply out two brackets
>
> Multiply each term inside the first bracket  by each term inside the second bracket, and add the resulting terms.

## 2.2 Squaring brackets
$$
(x + p)^2 = (x + p)(x + p) \\\\
= x^2 + xp + px + p^2 \\\\
= x^2 + 2px + p^2
$$

Hence the general formula:
$$
(x + p)^2 = x^2 + 2px + p^2
$$
and
$$
(x - p)^2 = x^2 - 2px + p^2
$$

## 2.3 Differences of two squares
$$
(x - p)(x + p) = x^2 + xp - px - p^2
$$
Hence:
$$
(x - p)(x + p) = x^2 - p^2
$$

# 3 Quadratic expressions and equations
## 3.1 Quadratic expressions
An expression of the form $ax^2 + bx + c$, where $a, b, c$ are numbers and $a \ne 0$ is called a **quadratic expression** in $x$. $a, b, c$ are called the **coefficients** of the quadratic.

## 3.2 Quadratic equations
An equation that can be expressed in the form:
$$
ax^2 + bx + c = 0
$$
is called a **quadratic equation** in $x$.

## 3.3 Solving simple quadratic equations
An equation of the form $x^2 = d$, where $d > 0$ has two solutions $x = \pm \sqrt{d}$.

Equations as $x^2 + 1 = 0$ have no solution among the real numbers.

## 3.4 Factorising quadratics of the form $x^2 + bx + c$
Fill in the gaps in the brackets on the right-hand side of the equation
$$
x^2 + bx + c = (x...)(x...)
$$
with two numbers whose product is $c$ and whose sum is $b$.
I can search systematically by writing down all the factor pairs of $c$ and choosing (if possible) a pair whose sum is $b$.

## 3.5 Solving quadratic equations by factorisation
If the product of two or more numbers is 0, then at least one of the numbers must be 0.
Hence in an equation as $(x - 2)(x - 3) = 0$ either $x - 2$ or $x - 3$ is 0. If $x - 2 = 0$ then $x = 2$, if $x - 3 = 0$  then $x - 3$ so the equation has two solutions.

### Strategy to solve $x^2 + bx + c = 0$ by factorisation
1. Find a factorisation: $x^2 + bx + c = (x + p)(x + p)$
2. Then $(x + p)(x + p) = 0$, so $x + p = 0$ or $x + q = 0$
	and  hence the solutions are $x = -p$ and $x = -q$.
	
When the two solutions are same it's said that equation has a **repeated solution**.

## 3.6 Factorising quadratics of the form $ax^2 + bx + c$
E.g. following quadratic expression;
$$
2x^2 - x - 6
$$
Where:
$$
a = 2\\\\
b = -1\\\\
c = -6
$$

> Find two numbers whose product is $ac$ and whose sum is $b$.

The numbers are $3$ and $-4$.

> Rewrite the quadratic expression, splitting the term in $x$ using the above factor pair.

$$
2x^2 - x - 6 = 2x^2 +3x -4x - 6
$$

> Group the four terms in pairs and take out common factors to give the required factorisation.

$$
2x^2 - x - 6 = 2x^2 +3x -4x - 6 \\\\
= x(2x + 3) -2(2x + 3) \\\\
= (x - 2)(2x + 3)
$$

### Simplify a quadratic equation
* If the coefficient of $x^2$ is negative, then multiply the equation through by $-1$ to make this coefficient positive.
* If the coefficients have a common factor, then divide the equation through by this factor.
* If any of the coefficients are fractions, then multiply the equation through by a suitable number to clear them.

# 4 Manipulating algebraic fractions
$\frac{a}{b}$ is equivalent to $\frac{a(a + 1)}{b(b + 1)}$ and common factor can be cancelled out as usual.