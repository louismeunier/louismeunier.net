---
title: "Remarks"
description: "Things I find interesting"
weight: 0
---

## A Special Spherical Integral
I recently had to deal with the following integral (in computing the Fourier transform of the surface measure of a sphere):
$$
I = \int_{\partial B(x, t)} e^{i z \cdot y} \mathsf{d}y,
$$ where $\partial B(x, t) \subset \mathbb{R}^d$ the surface of the $d$-ball centered at $x \in \mathbb{R}^d$ with radius $t > 0$, and $z \cdot y$ the usual Euclidean "dot" product; namely $x, t,$ and $z$ are all fixed. Finding a "nice" closed form for the expression proceeds as follows. First, we translate so the integral is about the origin, by sending $y \mapsto y - x$, $$
I = \int_{\partial B(0, t)} e^{i z \cdot y} e^{i z \cdot x} \mathsf{d}y = e^{i z \cdot x} \int_{\partial B(0, t)} e^{i z \cdot y} \mathsf{d} y =: e^{i z \cdot x} \cdot I(z).
$$ Next, notice that $I(z)$ is rotationally symmetric. Namely, if $A : \mathbb{R}^d \to \mathbb{R}^d$ is a rotation matrix, then $$
I(A z) = \int_{\partial B(0, t)} \exp{(i (A z) \cdot y)} \enspace{} \mathsf{d} y = \int_{\partial B(0, t)} \exp{(i z \cdot A^{\ast} y )} \enspace{} \mathsf{d} y,
$$ where $A^{\ast}$ the hermitian adjoint of $A$; rotation matrices are unitary, so $A^{\ast} = A^{-1}$. Changing variables by letting $u := A^{-1} y$, then, the new domain of integration remains $\partial B(0, t)$ since $A$ a rotation, and since $\det (A^{-1}) =\det (A)^{-1} = 1$, the resulting Jacobian of the transformation is unity. Thus, we find $I(A z) = I(z)$ indeed.

From this observation, then, we may assume without loss of generality that $z$ is a scalar of the usual basis vector, $e_1$, namely say $z = |z| \cdot e_1$, with $|\cdot|$ the Euclidean norm. With this, $$
I(z) = \int_{\partial B(0, t)} \exp{(i |z| y_1)} \mathsf{d} y,
$$ with $y = (y_1, \dots, y_d)$. Finally, rewriting this exponential using Euler's formula and writing the integral using [$d$-dim spherical coordinates](https://en.wikipedia.org/wiki/N-sphere#Spherical_coordinates), we find (identifying $y_1 = t \cos \phi_1$) $$
I(z) = \int_0^\pi \cdots \int_0^{2\pi} [\cos (|z| t \cos (\phi_1)) + i \sin(|z| t \cos (\phi_1))] \times \\\
\hspace{7em} t^{d - 1} \sin^{d - 2} (\phi_1) \cdots \sin (\phi_{d - 2}) \mathsf{d} \phi_1 \cdots \mathsf{d} \phi_{d - 1} \\\
= 2\pi t^{d - 1}  \left[\prod_{j=1}^{d - 3} \int_{0}^\pi \sin^j (\phi) \mathsf{d} \phi\right] \times \\\ 
\left[\int_0^\pi \cos{(|z| t \cos \phi) \sin^{d - 2} (\phi) \mathsf{d} \phi} + \int_0^\pi i \sin{(|z| t \cos \phi) \sin^{d - 2} (\phi) \mathsf{d} \phi} \right].
$$ The iterated product term simplifies using a well-known Gamma-function identity $$
\prod_{j=1}^{d - 3} \int_{0}^\pi \sin^j (\phi) \mathsf{d} \phi= \pi^{(d - 3)/2} \prod_{j=1}^{d - 3} \frac{\Gamma(\frac{j + 1}{2})}{\Gamma(\frac{j+2}{2})} = \frac{\pi^{(d - 3)/2}}{\Gamma(\frac{d - 1}{2})},
$$ and the right-most integral is identically zero, since the sin terms are symmetric about $\pi/2$. Finally, the first integral term is, up to a constant depending only on $d$, $t$, and $|z|$, equal to the Bessel function $J_{\frac{d - 2}{2}} (t |z|)$ (see [here](https://dn790007.ca.archive.org/0/items/treatiseontheory00watsuoft/treatiseontheory00watsuoft.pdf), section 3.3). All together, and explicitly writing out this constant, we find $$
I(z) = 2 \pi t^{d - 1} \cdot \frac{\pi^{(d - 3)/2}}{\Gamma(\frac{d - 1}{2})} \cdot  \frac{\Gamma(\frac{1}{2}) \Gamma(\frac{d - 1}{2})}{(\frac{1}{2} t |z|)^{(d - 2)/2}} J_{\frac{d - 2}{2}} (t |z|) = (2 \pi)^{d/2} \frac{t^{d/2}}{|z|^{\frac{d - 2}{2}}} \cdot J_{\frac{d - 2}{2}} (t |z|),
$$ from which we arrive finally at a relatively-nice formula $$
I = (2 \pi)^{d/2} \frac{t^{d/2}}{|z|^{(d - 2)/2}} e^{i z \cdot x} \cdot J_{\frac{d - 2}{2}} (t |z|).
$$ Throughout, we tacitly assumed $d > 2$. Indeed, if $d = 1$, the "unit ball" is just the open interval $(x - t, x + t)$ and so the surface of such a ball is the set ${x -t, x+ t}$, so $$
I = e^{i z \cdot y}\rvert_{y= x - t}^{x + t} = e^{i z (x + t)} - e^{i z (x - t)} 
= e^{i z x} [e^{i z t} - e^{- i z t}] \\\ =2 i e^{i z x} \sin(x) = 2 i \cos(x z) \sin(x) - 2 \sin(x) \sin(x z).
$$

% If $d = 2$, integrating over ("around") the circle centered at $x$ of radius $t$

