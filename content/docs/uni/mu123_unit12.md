+++
title = "MU123 Unit 12 Notes"
date = 2021-07-13
draft = false
template = "docs/page.html"

[extra]
toc = true
top = false
+++


# Introduction
**Trigonometry** is branch of mathematics that is concerned with methods of using triangles to find unknown lengths and unknown angles.

# 1 Right-angled triangles
Introduction of trigonometric rations sine, cosine and tanget.

## 1.1 Sine, cosine and tangent
Suppose that $\theta$ is an acute angle in a right-angled triangle in which the lengths of the hypotenuse, opposite and adjacent sides are represented by hyp, opp and adj, respectively.

The **sine** of the angle $\theta$ is
$$
\text{sin}~\theta = \frac{\text{opp}}{\text{hyp}}
$$
The **cosine** of the angle $\theta$ is
$$
\text{cos}~\theta = \frac{\text{adj}}{\text{hyp}}
$$
The **tangent** of the angle $\theta$ is
$$
\text{tan}~\theta = \frac{\text{opp}}{\text{adj}}
$$

Hence the acronym: **SOH CAH TOA**

## 1.2 Finding unknown angles
$$
\arcsin(x) = \sin^{-1}(x)
$$

## 1.4 Useful trigonometric ratios and identities
It's possible to deduct ratios of certain triangles.
E.g. in an equilateral triangle (interior angles of $60^\circ$) with each side of 2 units in which a vertical line divides the base of the triangle into two equal parts following can be deducted:
$$
\cos 60^\circ = \frac{1}{2}
$$
The length $x$ of the third side of this right-angled triangle can be calculated:
$$
\begin{align}
1^2 + x^2 &= 2^2 \\\\
x^2 &= 4 - 1 = 3 \\\\
x &= \sqrt{3}
\end{align}
$$
Hence:
$$
\begin{align}
\sin60^\circ &= \frac{\sqrt{3}}{2} \\\\
\tan60^\circ &= \frac{\sqrt{3}}{1} = \sqrt{3} \\\\
\end{align}
$$

Following table can be devised

|$\theta$|$\sin\theta$|$\cos\theta$|$\tan\theta$
| --- | --- | --- | ---
|$30^\circ$|$\frac{1}{2}$|$\frac{\sqrt{3}}{2}$|$\frac{1}{\sqrt{3}}$
|$45^\circ$|$\frac{1}{\sqrt{2}}$|$\frac{1}{\sqrt{2}}$|$1$
|$60^\circ$|$\frac{\sqrt{3}}{2}$|$\frac{1}{2}$|$\sqrt{3}$


### Identities
$$
\begin{align}
\cos\theta &= \sin(90^\circ - \theta) \\\\
\sin\theta &= \cos(90^\circ - \theta) \\\\
\tan\theta &= \frac{\sin\theta}{\cos\theta} \\\\
\sin^2\theta + \cos^2\theta &= 1
\end{align}
$$

# 2 Solving general triangles
## 2.1 The Sine Rule
$$
\frac{a}{\sin A} = \frac{b}{\sin B} = \frac{c}{\sin C}
$$
or
$$
\frac{\sin A}{a} = \frac{\sin B}{b} = \frac{\sin C}{c}
$$

## 2.2 The Cosine Rule
$$
\begin{align}
a^2 &= b^2 + c^2 - 2bc\cos A \\\\
b^2 &= c^2 + a^2 - 2ca \cos B \\\\
c^2 &= a^2 + b^2 - 2ab \cos C
\end{align}
$$

### The methods of solving a triangle
{% mermaid() %}
graph TD
	l1(Does the triangle contain a right angle?)
	l2a(Does the problem only involve lengths?)
	l2b(Do you know a length and the angle opposite?)
	l3a(Pythagoras' theorem)
	l3b(Trigonometric ratios)
	l3c(Sine rule)
	l3d(Cosine rule)
	
	l1 -- Y --> l2a
	l1 -- N --> l2b
	
	l2a -- Y --> l3a
	l2a -- N --> l3b
	
	l2b -- Y --> l3c
	l2b -- N --> l3d
{% end %}

## 2.4 A formula for the area of a triangle
The area of a triangle with two sides of lengths $a$ and $b$, and included angle $\theta$ , is
$$
\text{area} = \frac{1}{2}ab\sin\theta
$$

# 3 Trigonometric functions
### Sign of an angle
A general angle is a measure of rotation around a point, measured in degrees. Positive angles give anticlockwise rotations, and negative angles give clockwise rotations.

### Sine and cosine of a general angle
For a general angle $\theta$, let $P$ be the point on the unit circle obtained by a rotation of $\theta$ around the origin from the positive $x$-axis, and suppose that $P$ has coordinates $(x, y)$. Then
$$
\cos \theta = x ~~\text{and}~~ \sin \theta = y
$$

### Tangent of a general angle
For a general angle $\theta$,
$$
\tan \theta = \frac{\sin \theta}{\cos \theta}
$$
provided that $\cos \theta \ne 0$.

# 4 Radians
One **radian** is the angle subtended at the centre of a circle by an arc that is the same length as the radius.

So the number of radians in a full turn is
$$
\frac{2\pi r}{r} = 2\pi
$$
Hence
$$
2\pi ~\text{radians} = 360^\circ
$$
This gives
$$
1~\text{radian} = \frac{360^\circ}{2\pi} = \frac{180^\circ}{\pi} \approx 57^\circ
$$

### Converting between degrees and radians
Angle in radians $= \frac{\pi}{180} \times$ angle in degrees. 
Angle in degrees $= \frac{180}{\pi} \times$ angle in radians.