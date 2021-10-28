+++
title = "Complex numbers Notes"
date = 2021-05-02
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
+++


# Imaginary numbers
Quadratic equations as $x^2 = -1$ don't have any *real number* solution.
The solution exists in the **complex** number system.

Backbone of which is the **imaginary unit** $i$. For which following is true:
* $i = \sqrt{-1}$
* $i^2 = -1$

By taking multiples of $i$, I can create infinitely many **pure imaginary numbers**, e.g. $3i$, $i\sqrt{5}$, $-12i$.

By squaring an imaginary number I can explore how those relate to the real numbers:
$$
(3i)^2 = 3^2i^2 = 9i^2
$$

Now I can apply the fact that $i^2 = -1$:

$$
9i^2 = 9(-1) = -9
$$

Meaning $3i$ is square root of $-9$

## Simplifying pure imaginary numbers
As proved $\sqrt{-9}$ simplifies to $3i$ and following though process can be applied:
The square root of $-9$ is an imaginary number. The square root of $9$ is $3$, so the square root of *negative* $9$ is $3$ *imaginary units*, or $3i$

More formally:
$$
\text{For}~ a > 0,  \sqrt{-a} = i\sqrt{a}
$$

## Powers of $i$
Basic power line can be devised:
$$
\begin{aligned}
i^0 &= 1 \\\\
i^1 &= i \\\\
i^2 &= -1 \\\\
i^3 &= i^2 \times i = (-1)(i) = -i \\\\
i^4 &= i^3 \times i = (-i)(i)  = (-1)(i)(i) = (-1)(-1) = 1 \\\\
i^5 &= i^4 \times i = 1 \times i = i \\\\
i^6 &= i^5 \times i = -1 \\\\
i^7 &= i^6 \times i = -i \\\\
i^8 &= i^7 \times i = 1 \\\\
\end{aligned}
$$

Results can be summarised in following table:

| $i^1$ | $i^2$ | $i^3$ | $i^4$ | $i^5$ | $i^6$ | $i^7$ | $i^8$ |
| --    | --    | --    | --    | --    | --    | --    | --    |
| $i$   | $-1$  | $-i$  | $1$   | $i$   | $-1$  | $-i$    | 1    |

Hence it appearst that powers of $i$ cycle through the sequence of $i, -1, -i, 1$.

Properties of exponents can be used to devise larger powers of $i$, e.g.:
$$
i^{20} = i^{4\times5} = (i^4)^5 = 1^5 = 1
$$
Hence:
$$
i^{20} = 1
$$

The fact that $i$ raised to a multiple of $4$ is $1$ (along with properties of exponents) can be used to find large powers of $i$.

## Roots of negative numbers
Square roots of negative numbers can be simplified followingly:
$$
\sqrt{-20} = \sqrt{-1 \times 4 \times 5} = i\sqrt{4 \times 5} = 2i\sqrt{5}
$$

## $i$ as the principal root of $-1$
Consider following application of the $\sqrt{ab} = \sqrt{a} \times \sqrt{b}$ rule on the $i$:

GIven $i = \sqrt{-1}$ I can state:
$$
-1 = i \times i = \sqrt{-1} \times \sqrt{-1} = \sqrt{-1 \times -1} = \sqrt{1} = 1
$$
Which is obviosly not truthy. In reality the $\sqrt{ab} = \sqrt{a} \times \sqrt{b}$ rule **cannot be applied** when both $a$ and $b$ are negative.

# Complex numbers
Combination of real and imaginary numbers, e.g. $z = 5 + 3i$ which has following parts:
Real:
$$
Re(z) = 5
$$
Imaginary:
$$
Im(z) = 3
$$

The number can be plotted with $Re$ on $x$ axis and $Im$ on $y$ axis:
![complex_plot.png](:/e0e4b2bfff13476988e5e745801aeb66)

More formally a complex number is any number that can be written as $a + bi$.

## Classifying complex numbers
An imaginary number is a complex nuimber $a + bi$ where $a = 0$.
A real number is a complex number $a + bi$ where $b = 0$.

Hence following hiearchy:
```
-------------------------
|  Complex numbers      |
|                       |
| ----------------      |
| | Real numbers |      |
| ----------------      |
|                       |
| --------------------- |
| | Imaginary numbers | |
| --------------------- | 
-------------------------
```

## Simplifying complex numbers
Let's consider:
$$
2 + 3i + 7i^2 + 5i^3 + 9i^4
$$

I already know that:
$$ 
\begin{aligned}
i^2 = -1 \\\\
i^3 = -i \\\\
i^4 = 1
\end{aligned}
$$ 

Hence:
$$
\begin{aligned}
2 + 3i + 7(-1) + 5(-i)+ 9(1) = \\\\
2 + 3i - 7 -5i + 9 = \\\\
4 - 2i
\end{aligned}
$$

## Adding complex numbers
E.g.:
$$
\begin{aligned}
(5 + 2i) + (3 - 7i) = \\\\
5 + 3 + 2i - 7i = \\\\
8 - 5i
\end{aligned}
$$

## Subtracting complex numbers
E.g.:
$$
\begin{aligned}
(2 - 3i) - (6 - 18i) = \\\\
2 - 3i - 6 + 18i = \\\\
-4 + 15i
\end{aligned}
$$

## Distance of complex numbers
E.g. distance between:
$$
\begin{aligned}
z = 2 + 3i \\\\
w = -5 -i
\end{aligned}
$$

Can be calculated using Pythagoras theorem:
![complex_distance.png](:/3c8cf700b648464283597c0ffe920c0e)

## Midpoint of complex numbers
Is the half of real and complex parts separately:
$$
\begin{aligned}
z = 2 + 3i \\\\
w = -5 -i \\\\
\end{aligned}
$$

$$
\begin{aligned}
a = (\frac{2 + (-5)}{2}) + (\frac{3 + (- 1)}{2})i \\\\
a = -\frac{3}{2} + i
\end{aligned}
$$

## Multiplying complex numbers
### A real number by a complex number
Use a distributive property:
$$
-4(13 + 5i) = -4(13) + (-4)(5i) = -52 - 20i
$$

### A pure imaginary number by a complex number
$$
2i(3 - 8i) = 2i(3) - 2i(8i) = 6i - 16i^2
$$

Use the fact that $i^2 = -1$:
$$
6i - 16i^2 = 6i - 16(-1) = 6i + 16 = 16 + 6i
$$

### Two complex numbers
Multiply each term in the first number by each term in the second number:

$$
\begin{aligned}
(1 + 4i)(5 + i) = \\\\
(1)(5) + (1)(i) + (4i)(5) + (4i)(i) = \\\\
5 + i + 20i + 4i^2 = \\\\
5 + 21i + 4i^2 = \\\\
5 + 21i + 4(-1) = \\\\
5 + 21i - 4 = \\\\
1 + 21i
\end{aligned}
$$
