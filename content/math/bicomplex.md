---
title: "the discrete variational bicomplex"
description: "Research done between May and December, 2024"
weight: -2
---

<div style="font-size:1.1em";>
$$
J^\infty (E) \hookrightarrow \Omega^{0,0} (E) \overset{\mathsf{d}_H}{\to} \Omega^{0,1} (E) \overset{\mathsf{d}_H}{\to}\cdots \overset{\mathsf{d}_H}{\to}\Omega^{0,p} (E) \overset{\pi^0}{\to} \mathcal{F}^0 \overset{\delta}{\to} \mathcal{F}^1 \overset{\delta}{\to} \cdots
$$
</div>

Conservation laws are ubiquitous in the study of differential equations. They often represent fundamental physical quantities, and can lead to stability and existence results for possible solutions. We researched the concept of conservation laws for discrete difference equations, such as those that arise from finite difference discretizations of partial differential equations. The goal was to study the relationship between such discrete conservation laws and their continuous counterparts. We approached this by considering the variational bicomplex, a double chain complex which in the smooth case is defined on the infinite jet bundle of a fibered manifold, and provides a natural algebraic setting for studying conservation laws. By constructing an appropriate counterpart structure over a discrete space, we aimed to be able to fundamentally understand discrete conservation laws and moreover contrast the smooth and discrete theory.
<!-- 
The variational bicomplex is a double chain complex defined on the infinite jet bundle of a fibered manifold, $\pi : E \to M$. Differential equations on $E$ can naturally be thought of as smooth, real-valued functions on the jet bundle and thus live in various subspaces of the bicomplex. Of particular interest is the outer edge portion of the complex, the so-called Euler-Lagrange complex:
$$
J^\infty (E) \hookrightarrow \Omega^{0,0} (E) \overset{\mathsf{d}_H}{\to} \Omega^{0,1} (E) \overset{\mathsf{d}_H}{\to}\cdots \overset{\mathsf{d}_H}{\to}\Omega^{0,p} (E) \overset{\pi^0}{\to} \mathcal{F}^0 \overset{\delta}{\to} \mathcal{F}^1 \overset{\delta}{\to} \cdots
$$
The space $\mathcal{F}^0$ is in natural bijection with the space of differential functions on $E$ modulo total divergences, $\mathsf{d}_H$.

As such, it is the natural place where Lagrangians of variational problems live, and thus where one develops a variational calculus. Indeed, the map $\delta : \mathcal{F}^0 \to \mathcal{F}^1$ gives rise to the Euler-Lagrange operator, $\mathsf{E} = \sum_{\alpha, I} (-D_x)^I \frac{\partial}{\partial u_I^\alpha}$. -->

<div style="display:flex; flex-direction:column; text-align: center;">
    <div>
        <p><a href="/images/MATH470Report-LouisMeunier.pdf" target="_blank">Paper (long)</a> <em>(The Discrete Variational Bicomplex)</em></p>
        <p><a href="/images/discretevariational-paper-short.pdf" target="_blank">Paper (short)</a> <em>(Conservation Laws: from Differential to Difference)</em></p>
         <!-- <p><a href="" target="_blank">Presentation</a> <em>The D</em></p> -->
    </div>
</div>

<!-- <div style="position:fixed;"> -->
Funded by the McGill SURA grant during the summer of 2024. Continued for course credit as part of McGill's MATH470 (Honours Research Project) course.
<!-- </div> -->