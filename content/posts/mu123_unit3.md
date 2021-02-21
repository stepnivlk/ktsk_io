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
