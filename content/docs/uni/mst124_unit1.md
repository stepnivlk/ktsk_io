+++
title = "MST124 Unit 1 - Algebra"
date = 2021-10-12
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
+++

# 1 Numbers
## 1.1 Types of numbers
* Natural numbers (positive integers) - $1, 2, 3, ...$
* Integers - $..., -3, -2, -1, 0, 1, 2, 3, ...$
* Rational numbers - $\frac{3}{4}, 2\frac{1}{3}, 4, -4, -\frac{8}{7}, 0.16, 7.374$
* Real numbers - every point on a number line corresponds to a real number
	* Some points corresponds to rational numbers - $\frac{2}{3}$
	* Some points to irrational numbers - $\sqrt{2}, \pi$

Every rational number can be written in decimal form by dividing nominator by the denominator.
**Terminating** rational number has finite number of digits after decimal point - $0.125$
**Recurring** has a blog of one or more digits after the decimal point that repeat indefinitely - $0.126 126 126 ...$

Decimal numbers that are neither terminating nor recurring - those that are infinitely long but have no block of digits that repeat indefinitely - are the irrational numbers.

Hence, the rational numbers are decimal numbers that terminate or recur. The irrational numbers are the decimal numbers with an infinite number of digits after the decimal point but with no block of digits that repeats indefinitely.

## 1.2 Working with numbers
The $\approx$  symbol can be used as an alternative to explicitly writing the rounding in brackets behind a number.

### Four mathematical words
* The **sum** of two or more numbers is the result of adding them.
• The **product** of two or more numbers is the result of multiplying
them.
• A **diﬀerence** of two numbers is the result of subtracting one
from the other.
• A **quotient** of two numbers is the result of dividing one by the
other.

## 1.3 Integers
If an integer $a$ divides exactly into another integer $b$, then we say that
* $b$ is a **multiple** of $a$, or
* $b$ is **divisible** by $a$, or
* $a$ is a **factor** or **divisor** of $b$.

**Factor pair** of an integer is a pair of its factors that multiple together to give the integer.

### Strategy to find the positive factor pairs of a positive integer
* Try dividing the integer by each of the numbers $1, 2, 3, 4, ...$ in turn. Write down a factor pair when one is found.
* Stop when you get a factor pair that you have already.

**Prime** number is an integer greater than 1 whose only factors are 1 and itself.

**Composite** number is an integer greater than 1 that isn't a proime number.

### The fundamental theorem of arithmetic
Every integer greater than 1 can be written as a product of prime factors in just one way (except that you can change the order of the factors).

**Prime factorisation** of an integer greater than 1 is any expression that shows it written as a product of prime factors. E.g.: $504 = 2^3 \times 3^2 \times 7$.

### Strategy to find the prime factorisation of an integer greater than 1
* Repeatedly factor out the prime 2 until you obrain a number that isn't divisble by 2
* Repeatedly factor out the prime 3 until you obrain a number that isn't divisble by 3
* Repeatedly factor out the prime 5 until you obrain a number that isn't divisble by 5
Continue the process with each of the successive primes. Stop when you have a product of primes.
Write the factorisation with the primes in increasing order, using index notation.

**Common multiple** of two or more integers is a number that is a multiple of all of them.
**Least common multiple (LCM)** of two or more integers is the smallest positive integers that is a multiple of all of them.
**Common factor** of two or more integers is a number that is a factor ofo all of them.
**Highest common factor (HCF)** of two or more integers is the largest positive number that is a factor of all of them.

### Strategy to ﬁnd the lowest common multiple or highest common factor of two or more integers greater than 1
• Find the prime factorisations of the numbers.
• To ﬁnd the LCM, multiply together the highest power of each
prime factor occurring in any of the numbers.
• To ﬁnd the HCF, multiply together the lowest power of each
prime factor common to all the numbers.

*Euclid's algorithm* is an efficient method for finding LCMs and HCFs without having to find prime factorisation first.

# 2 Algebraic expressions
## 2.1 Algebraic terminology
**Expression** is an arrangement of letters, numbers and/or mathematical symbols, which is such that if numbers are substituted for any letters present, then you can work out hte value of the arrangement.
**Algebraic expression** contains letters.

A letter can be either
* **variable**
* **unknown**
* **constant**


An **equation** is made up of two expressions with an equals sign in between them, e.g.: $x + 2x = 3x$.

**Terms** are the quantities that are added in an expression.
**Constant** is a term without variable.
**Coefficient** is a fixed value in a term of a form $\text{a fixed value} \times \text{a combination of variables}$.

## 2.2 Simplifying algebraic expressions
If two or more terms of an expression differ only in the value of their coefficients, then you can combine them into a single term - the process called **collect like terms**.

### Strategy to simplify a term
1. Find the overall sign and write it at the front.
2. Simplify the rest of the coefficient and write it next.
3. Write any remaining parts of the term in an appropriate order; for example, letters are usually ordered alphabetically. Use index notation to avoid writing letters (or other items) more than once.

### Strategy to simplify an expression with more than one term
1. Indentify the terms. Each term after the first starts with a plus or minus sign that isn't inside brackets.
2. Simplify each term. Include the sign (plus or minus) at the start of each term.
3. Collect any like terms.

## 2.3 Multiplying out brackets
**Expansion** is the form of an expression when the brackets are multiplied out.
**Multiplier** is the subexpression that multiplies the brackets.

### Strategy to multiply out brackets
Multiply each term inside the brackets by the multiplier.

### Strategy to remove brackets with a plus or minus sign in front
* If the sign is plus, keep the sign of each term inside the brackets the same.
* If the sign is minus, change the sign of each term inside the brackets.

For any expressions $A$ and $B$, the negative of $A - B$ is $B - A$.
E.g.: $-(n - 3n^2) = 3n^2 - n$

Multiplying an expression that contains several terms by a second expression is the same as multiplying *each term* of the first expression by the second expression.
Similarly, dividing an expression that contains several terms by a second expression is the same as dividing *each term* of the first expression by the second expression.

### Strategy to multiply out brackets in an expression with more than one term
1. Identify the terms.
2. Multiply out the brackets in each term. Include the sign at the start of each resulting term.
3. Collect any like terms

### Difference of two squares
For any expressions $A$ and $B$,
$$
(A + B)(A - B) = A^2 - B^2
$$
The expression on RHS is called the **difference of two squares**.

### Squaring brackets
For any expressions $A$ and $B$,
$$
\begin{align}
(A + B)^2 = A^2 + 2AB + B^2 \\\\[1em]
(A - B)^2 = A^2 - 2AB + B^2 \\\\[1em]
\end{align}
$$

# 3 Algebraic factors, multiples and fractions
## 3.1 Factors and multiples of algebraic expressions
For example, the equation $a^2b = a \times ab$ shows that both $a$ and $ab$ are **factors** of $a^2b$ and it also shows that $a^2b$ is a **multiple** of both $a$ and $ab$.

**Common factor** of two or more algebraic expressions is an expression that's a factor of all of them.
**Common multiple** of two or more algebraic pexressions is an expression that's a multiple of all of them.
**Highest common factor** is a multiple of all other common factors.
**Lowes common multiple** is a common multiple that is a factor of all other common multiples.

## 3.2 Taking out common factors
**Factorising** an expression means writing it as the product of two or more expressions, neither of which is 1 (and, usually, neither of which is −1).

### Strategy to take out a common factor from an expression
1. Find a common factor of the terms (usually the highest common factor).
2. Write the common factor in front of a pair of brackets.
3. Write what's left of each term inside the brackets.

## 3.3 Algebraic fractions
### Strategy to add or subtract algebraic fractions
1. Make sure that the fractions have the same denominator - if necessary, rewrite each fraction as equivalent fraction to achieve this.
2. Add or subtract the numerators.
3. Simplify the answer if possible.

### Strategy to multiply or divide algebraic fraction
* To multiply two or more algebraic fractions, multiply the numerators together and multiply the denominators together.
* To divide an algebraic fraction, multiply by its reciprocal.
Simplify the answer if possible.

# 4 Roots and powers
## 4.1 Roots of numbers
For every even natural number $n$, every positive number has exactly two real $n$th roots (a positive one and a negative one), every negative number has no real $n$th roots, and the number $0$ has exactly one $n$th root (itself). For every odd natural number $n$, every real number has exactly one real $n$th root.

Most roots of numbers are irrational numbers. In particular, the square root of any natural number that isn’t a perfect square is irrational.

**Surd** is a numerical expression that contains one or more irrational roots of numbers.

## 4.2 Manipulating surds
The square root of a product of numbers is tha same as the product of the square roots of the numbers, and similarly for a quotient:
$$
\sqrt{ab} = \sqrt{a} \sqrt{b}~,~~ \sqrt{\frac{a}{b}} = \frac{\sqrt{a}}{\sqrt{b}}
 $$
 
 Multiplying by a **conjugate** of denominator is useufl when a denominator of a fraction contains a sum of two terms, either or both of which is a trational number multiplied by an irrational square root. Conjugate is an expression that is given by changing the sign of one of the terms. This is useful since $(A + B)(A - B) = A^2 - B^2$.
 E.g.
$$
\begin{align}
\frac{5}{4\sqrt{7} + \sqrt{2}} &= \\\\[1em]
\frac{5\times(4\sqrt{7} - \sqrt{2})}{ (4\sqrt{7} + \sqrt{2})(4\sqrt{7} - \sqrt{2}) } &= \\\\[1em]
\frac{20\sqrt{7} - 5\sqrt{2}}{110} \\\\[1em]
\end{align}
$$

## 4.3 Working with powers
### Index laws for a single base
To multiply two powers with the same base, add the indices:
$$
a^mb^n = a^{m + n}
$$
To divide two powers with the same base, subtract the indices:
$$
\frac{a^m}{a^n} = a^{m - n}
$$
To find a power of w a power, multiply the indices:
$$
(a^m)^n = a^{mn}
$$
A number raised to the power of 0 is 1:
$$
a^0 = 1
$$
A number raised to a negative power is the reciprocal of the number raised to the corresponding positive power:
$$
a^{-n} = \frac{1}{a^n}
$$

### Index laws for two bases
A power of a product of numbers is the same as the product of the same powers of the numbers, and similarly for a power of a quotient:
$$
\begin{align}
(ab)^n = a^nb^n \\\\[1em]
(\frac{a}{b})^n = \frac{a^n}{b^n}
\end{align}
$$

### Converting between fractional indices and roots
$$
\begin{align}
a^{\frac{1}{n}} = \sqrt[n]{a} \\\\[1em]
a^{\frac{m}{n}} = (\sqrt[n]{a})^m = \sqrt[n]{a^m}
\end{align}
$$

# 5 Equations
## 5.1 Terminology for equations
**Identity** is an equation that is satisfied by *all* possible values of its variables. E.g $x(x + y) = x^2 + xy$.

## 5.2 Rearranging equations
### Strategy to rearrange an equation
* Rearrange the expressions on one or both sides.
* Swap the sides
* Do the same thing to both sides.

### Doing the same thing to both sides of an equations
* Add something.
* Subract something.
* Multiply by something (non-zero).
* Divide by something (non-zero).
* Raise to a power (non-zero).

**Multiplying through** is a process of multiplying each term no both sides of an equation by something.
**Dividing through** is a process of dividing each term no both sides of an equation by something.
**Clearing** is a process of muliplying through by appropriate number to remove a fraction from equation.

### Cross-multiplying
If $A$, $B$, $C$ and $D$ are expressions, then the equations
$$
\frac{A}{B} = \frac{C}{D} ~~ \text{and} ~~ AD = BC
$$
are equivalent (provided that $B$ and $D$ are never zero).

## 5.3 Solving linear equations in one unknown
Use the rules for rearranging equations to obtain successive equivalent equations. Aim to obtain an equation in which the unknown is alone on one side, with only a number on the other side. To achieve that, do the following, in order.
1. Clear any fractions and multiply out any brackets.  To clear fractions, multiply through by a suitable expression.
2. Add or subtract terms on both sides to get all the terms in the unknown on one side, and all the other terms on the other side. Collect like terms.
3. Divide both sides by the coefficient of the unknown.

## 5.4 Making a variable the subject of an equation
**Formula** is an equation with a subject.

### Strategy to make a variable the subject of an equation
(this works for some equations but not all)
1. Clear any fractions and multiply out any brackets.
2. Add or subtract terms on both sides to get all the terms in the unknown on one side, and all the other terms on the other side. Collect like terms.
3. If more than one term contains the required subject, then take it out as a common factor.
4. Divide both sides by the expression that multiplies the required subject.