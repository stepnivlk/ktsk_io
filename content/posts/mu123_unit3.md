+++
title = "MU123 Unit 3 Notes"
date = 2021-02-21

[taxonomies]
categories = ["uni", "math"]
+++

# 1 Natural numbers
Positive integers `1, 2, 3, 4...`
[Some include zero, some not](https://en.wikipedia.org/wiki/Natural_number).

## 1.1 Multiples
A result of multiplying a natural number by natural number. E.g. multiples of 8 are $8, 16, 24, 32$

Thus multiples are numbers into which 8 divides exactly.

### Common multiple
is a multiple of all the numbers in question. Lowest common multiple (LCM) is the smallest number that is a multiple of numbers in question

## 1.2 Factors
A natural number that divides a number exactly into a second natural number, e.g. 2 is factor of 10.
Alternatively we can say 10 is divisible by 2.

Related to multiples since 2 is a factor of 10 is same as 10 is a multiple of 2.

All natural numbers > 1 have at least two factors - itself and 1.

Factors can be arranged into factor pairs - $1,10$; $2,5$.

> **Strategy to find factors of a number**
> * Try 1,2,3,4... in turn. When factor is found, write it down with the other factor in the pair
> * Stop when you reach already found factor pair

### Common factors
is a factor of all the numbers in question. The highest common factor (HCF) is the largest number that is a factor of numbers in question.

## 1.3 Prime numbers
Natural numbers that have **exactly** two factors - 1 and itself, e.g. $2, 3, 5, 7, 11, 13, \ldots$.

### Sieve of Eratosthenes
An algorithm for finding all the prime numbers up to a certain number.
![sieveofera](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)
* Create a range of $2..n$ where $n$ is a certain number
* Mark all the numbers that are multiples of 2 and are $>= 2^2$
* Move to next unmarked number - 3 and mark its multiples that are $>= 3^2$
* ...
* All the unmarked numbers are primes

Python impelementation [src](https://www.geeksforgeeks.org/sieve-of-eratosthenes/):
```python
def SieveOfEratosthenes(n):
 
    # Create a boolean array 
    # "prime[0..n]" and initialize
    #  all entries it as true.
    # A value in prime[i] will
    # finally be false if i is 
    # Not a prime, else true.
    prime = [True for i in range(n+1)]
    p = 2
    while (p * p <= n):
 
        # If prime[p] is not 
        # changed, then it is a prime
        if (prime[p] == True):
 
            # Update all multiples of p
            for i in range(p * p, n+1, p):
                prime[i] = False
        p += 1
 
    # Print all prime numbers
    for p in range(2, n+1):
        if prime[p]:
            print p,
```
Resources
* [https://www.geeksforgeeks.org/sieve-of-eratosthenes/](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
* [https://cp-algorithms.com/algebra/sieve-of-eratosthenes.html](https://cp-algorithms.com/algebra/sieve-of-eratosthenes.html)
* [https://www.baeldung.com/cs/sieve-of-eratosthenes](https://www.baeldung.com/cs/sieve-of-eratosthenes)

### Mersenne primes
$$
2^n - 1 ~\text{for natural number} ~n
$$
It can be proven that if $2^n - 1$ is prime then $n$ must be a prime.

Resources
* [https://en.wikipedia.org/wiki/Mersenne_prime](https://en.wikipedia.org/wiki/Mersenne_prime)
* [https://www.mersenne.org/](https://www.mersenne.org/)
* [https://primes.utm.edu/mersenne/](https://primes.utm.edu/mersenne/)

## 1.4 Prime factors
A natural number > 1 that is not prime is called a **composite number**, e.g.: $4, 6, 8, 9, 10\ldots$.
A composite number can often be written as a product of even more factors forming a **factor tree**:
{% mermaid() %}
graph TD;
    two1((2))
    two2((2))
    two3((2))
    three1((3))
    three2((3))
    five1((5))
	
    360-->20;
    360-->18;
    20-->4;
    20-->five1;
	18-->three1;
	18-->6;
	4-->two1;
	4-->two2;
	6-->two3;
	6-->three2;
{% end %}

Hence we can say $360 = 2^3 \times 3^2 \times 5$. All of the factors here are primes.

I could've started with different nodes, e.g. $360 = 10 \times 36$, but the result would've been the same.

The process of writing a natural number as a product of factors > 1 is called **factorisation**.

> **The fundamental theorem of arithmetic**
>
> Every natural number > 1 can be written as product of prime numbers in **just one way**.

The **prime factorisation** of a natural number is the product of prime factors that is equal to it, e.g.:
$$
2 = 2 \qquad 3 = 3 \qquad 4 = 2^2 \\\\
5 = 5 \qquad 6 = 2 \times 3 \qquad 7 = 7 \\\\
8 = 2^3 \qquad 9 = 3^2 \qquad 10 = 2 \times 5
$$

Because of the fundamental theorem of aithmetic we can say that prime numbers are the **building blocks of natural numbers**.

For prime factorisation it may be helpful to be systematic and follow:
$$
\text{the smallest possible prime} \times \text{a number}
$$
And iterate for each composite number in the factor tree, e.g.:

{% mermaid() %}
graph TD;
    two1((2))
    two2((2))
    three1((3))
    three2((3))
    seven1((5))
	
	252-->two1;
    252-->126;
	126-->two2;
	126-->63;
	63-->three1;
	63-->21;
	21-->three2;
	21-->seven1;
{% end %}

There's no other way to find prime factors of a number $n$ then trying all the primes < $n$.
So multiplying two large primes is a quick process but expensive to reverse.
This fact is a base to secure encryption systems.

### Finding LCM and HCF using prime factors
* Find the prime factorisation of the numbers.
* To find the LCM, multiply together the highest ower of each prime factor occuring in any of the numbers.
* To find the HCF, multiply together the lowest power of each prime factor common to all the numbers.

## 1.5 Powers
### Index laws
So far I've used these
$$
\begin{aligned}
a^m \times a^n &= a^{m+n} \qquad \frac{a^m}{a^n} = a^{m-n} \\\\
(a^m)^n &= a^{mn} \\\\
(a \times b)^n &= a^n \times b^n \qquad (\frac{a}{b})^n = \frac{a^n}{b^n}
\end{aligned}
$$

# 2 Rational numbers
Include natural numbers among others.

Is a number that can be written as a fraction of two integers: $\frac{integer}{integer}$.

Following numbers can be written in this form:
* Fraction as $\frac{3}{4}$
* Mixed number as $5\frac{3}{4}$ since it can be converted to top-heavy fraction: $\frac{23}{4}$
* Whole number: $7 = \frac{7}{1}$
* Decimal number with finite number of digits after decimal points: $0.42 = \frac{42}{100}$
* Some decimal numbers with infinite numbers after decimal point: $0.333\ldots = \frac{1}{3}$
* The negative of any above: $-4 = \frac{-4}{1}$

### Irrational numbers
* $\pi$
* $\sqrt{2}$

### Rational numbers as decimals
Every rational number can be converted to decimal, e.g.: $\frac{5}{8} = 5 \div 8 = 0.625$
There are two possible outcomes of the division:
* decimal number with finite digits after d.p. - **terminating decimal**
	* $0.625$ is terminating
* decimal with block of indefinitely repeating digits after d.p - **recurring decimal**
	* $\frac{2}{3} = 0.6666\ldots$ is recurring
	* Can be denoted with $0.1\overline{23}$.

**Thus rational numbers can be redefined as**
> Decimal numbers that are terminating or recurring.

I can convert terminating to fraction so I can prove first part of the statement but I can't prove the second yet.


## 2.2 Adding and subtracting fractions

* Only when there's a same denominator - fractions are of a same type.
* When there's different denominator - find common one (LCM).
* Always simplify.

## 2.3 Multiplying and dividing fractions

### Multiplying

* Multiply the numerators together and multiply the denominators together.

### Dividing

* Multiple the fraction by its reciprocal 

#### Reciprocal
A number and its reciprocal multiply together to give 1.
E.g.:
$0.25 ~\text{is rec of} ~4$,since $0.25 \times 4 = 1$
$\frac{3}{2} ~\text{is rec of} ~\frac{2}{3}$,since $\frac{3}{2} \times \frac{2}{3} = 1$

Alternatively, it is 1 divided by given number. 

To find a reciprocal of fraction turn it upside down.
E.g.:
$\text{rec of}~\frac{3}{4}~\text{is}~\frac{4}{3}$

## 2.4 Negative indices
The previous positive power of a number $n$ is equal to current positive power divided by $n$, e.g.:
$4^3 = \frac{4^4}{4}$

Thus $4^0$ has to be a number I get when dividing $\frac{4^1}{4} = 1$.
Similarly $4^{-1}$ has to be a number I get when dividing $\frac{4^0}{4} = \frac{1}{4}$.

We can build whole scale of the pattern

| $4^{-3}$ | $4^{-2}$ | $4^{-1}$ | $4^0$ | $4^1$ | $4^2$ | $4^3$ |
|---       | ---      | ---      | ---   | ---   | ---   | ---   |
| $\frac{1}{4^3}$ | $\frac{1}{4^2}$ | $\frac{1}{4}$ | $1$ | $4$ | $16$ | $64$ |

The meaning of negative and zero indices works with all the index laws I've seen so far.

Index laws can be expand by following rules based on previous observations:

* A non-zero number raised to the power zero is 1:
$$
a^0 = 1
$$
* A non-zero number raised to a negative power is the reciprocal of the number raised to the corresponding positive power:
$$
a^{n - 1} = \frac{1}{a^n}
$$

Interestingly:
$$
a^{-1} = \frac{1}{a}
$$
Hence, raising a number to the power of $-1$ is the same as finding its reciprocal.

E.g.:
$$
(\frac{2}{3})^{-1} = 1 \times \frac{3}{2} = \frac{3}{2}
$$

## 2.5 Scientific notation
* Also called **standard form**.
* A number between 1 and 10 (excluded) multiplied by a power of 10.

# 3 Irrational numbers and real numbers
## 3.1 What is an irrational number?
Decimals with infinite number of digits afterthe decimal point but no repeating block of digits.

Following number is not terminating nor recurring:
$$
0.010,010,001,000,010,000,01\ldots
$$

*TODO: What if the repeating block is just really big?*

Here $x$ is not rational:

$$
x^2 = 2 \\\\
\sqrt{2} = x
$$


---
The fact that $\sqrt{2}$ is irrational can be proven by **contradiction** followingly.

Suppose there's a rational number whose square is $2$. Hence it can be written as
$$
\frac{\text{integer}}{\text{integer}}
$$
Consider it being cancelled down to the simplest form as:
$$
\frac{m}{n}
$$
So $m$ and $n$ don't have any common factor.
The square of $\frac{m}{n}$ is 2, so:
$$
(\frac{m}{n})^2 = 2 \\\\
\frac{m^2}{n^2} = 2
$$
It follow that
$$
\frac{m^2}{n^2} \times n^2 = 2 \times n^2 \\\\
m^2 = 2n^2
$$
$2n^2$ has to be even since it's a product of 2 and whole number. Meaning $m^2$ has to be even too, that means $m$ has to be even as well.
That means that $m = 2r$ for some integer $r$.
When substituting to the original equation we get:
$$
(2r)^2 = 2n^2 \\\\
4r^2 = 2n^2 \\\\
$$
It follow that
$$
\frac{4r^2}{2} = \frac{2n^2}{2} \\\\
2r^2 = n^2
$$

The integer $n^2$ is even hence $n$ has to be even too.
So both $m$ and $n$ are even. But that's **impossible** since $m$ and $n$ don't have any common factor.

---

The irrational numbers together with the rational numbers form the **real numbers**.

I can think about various categories of numbers as layers:
```
Real(
	Irrational,
	Rational(
		Integers(
			Natural
		)
	)
)
```
plus complex, that will come later on.

## 3.2 Roots of numbers
A number that when multiplied by itself gives the original number.
Every positive number has two square roots - a positive one and a negative one.

Square roots of two numbers can be used to find the square root of the product or a quotient.

For example, numbers 16 and 49 have square roots of 4 and 7.
I can apply index law $(a \times b)^n = a^n \times b^n$ to those:
$$
(4 \times 7)^2 = 4^2 \times 7^2 \\\\
(4 \times 7)^2 = 16 \times 49
$$
That implies:
$$
\sqrt{16 \times 49} = \sqrt{16} \times \sqrt{49}
$$

This can be generalized into following laws:
$$
\sqrt{a \times b} = \sqrt{a} \times \sqrt{b} \qquad \sqrt{\frac{a}{b}} = \frac{\sqrt{a}}{\sqrt{b}}
$$

Obviously, these laws apply to any root.

## 3.3 Surds
Numbers that are not perfect square have irrational roots. Hence following roots are irrational:
$$
\sqrt{7}, \sqrt{8}, \sqrt{10}, \sqrt{11}
$$
Since such number can be only approximated as a decimal it should be left as is in calculations, e.g.:
$$
x = 2 \times \sqrt{5}
$$
such expressions are called **surds** - it contains one or more irrational roots of numbers.
Surds are usually written concisely as formulas, number before surd when multiplied:
$$
y = 2\sqrt{5}
$$
In the simplest form:
$$
\sqrt{12} = \sqrt{4 \times 3} = \sqrt{4} \times \sqrt{3} = 2\sqrt{3}
$$
This is obviously possible when some of a numbers under the root are perfect squares. Thus the goal when simplifying is to find some perfect square multiplied some other number giving the original number bellow the root.

### Multiplying roots
* Multiply numbers together
* Multiply roots together
* Simplify the root

### Dividing roots
Use following laws
$$
\sqrt{a \times b} = \sqrt{a} \times \sqrt{b} \qquad \sqrt{\frac{a}{b}} = \frac{\sqrt{a}}{\sqrt{b}}
$$

Sometimes, I should expand an integer to a multiplication of surds in order to simplify the quotient:
$$
\frac{2}{\sqrt{2}} = \frac{\sqrt{2} \times \sqrt{2}}{\sqrt{2}} = \frac{1 \times \sqrt{2}}{1} = \sqrt{2}
$$

### Adding and substracting roots
It's usually not possible to add or substract different roots, thus 
$$
\sqrt{a} + \sqrt{b} \not= \sqrt{a + b}
$$

I can only add or substract roots that are the same.

> **To simplify surds**
>
> * Simplify roots of integers with square factors.
> * Simplify products and quotients of roots.
> * Add or subtract roots that are the same.

## 3.4 Fractional indices
Index laws can be applied to fractional indices too, e.g. let's consider the power $5^\frac{1}{2}$

By applying
$$
a^m \times a^n = a ^{m + n}
$$
I get
$$
5^\frac{1}{2} \times 5^\frac{1}{2} = 5^{\frac{1}{2} + \frac{1}{2}} = 5^1 = 5
$$
Hence
$$
5^\frac{1}{2} = \sqrt{5}
$$

It can be generalized in the following index law
$$
a^\frac{1}{n} = \sqrt[n]{a}
$$

This rule toegher with other index laws can be used to give a meaning to any fractional index.

E.g. in combination with
$$
(a^m)^n = a^{mn}
$$

I can do following operation
$$
5^\frac{4}{3} = 5^{\frac{1}{3} \times 4} = (5^{\frac{1}{3}})^4 = (\sqrt[3]{5})^4
$$

This combination can be generalized to yet another index law
$$
a^\frac{m}{n} = (\sqrt[n]{a})^m
$$

Interestingly the square root laws I saw before:
$$
\sqrt{a \times b} = \sqrt{a} \times \sqrt{b} \qquad \sqrt{\frac{a}{b}} = \frac{\sqrt{a}}{\sqrt{b}}
$$
Can be deduced by applying $n = \frac{1}{2}$ to following index laws:
$$
(a \times b)^n = a^n \times b^n \qquad (\frac{a}{b})^n = \frac{a^n}{b^n}
$$

> Irrational indices are also valid but I will encounter those later on.

# 4 Ratios
## 4.1 What is a ratio?
Comparition of multiple ordered quantities, e.g.: $3:5 ~ 2:10:7$

Sometimes it's useful to convert a ratio to a $number:1$ form to e.g.
* Compare multiple ratios.
* Find approximate ratios.
To reach such a form I can divide both numbers by second number, e.g.:
$$
7 : 11 = \frac{7}{11} : \frac{11}{11} = 0.636 : 1 ~\text{(3 d.p.)}
$$