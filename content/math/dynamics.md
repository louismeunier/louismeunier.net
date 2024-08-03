---
title: "dynamics"
description: "Dynamics-related code, simulations"
weight: 1
---

## Baker's Map
<div class="image-wrapper">
<img src="/images/bakersmap.gif" alt="Baker's Map Gif"/>
</div>

Animation of the Baker's Map, obtained by iterating 
$$F(x,y) = \begin{cases}
(2x, \frac{y}{2}) & 0 \leq x < \frac{1}{2}\\
(2-2x, 1 - \frac{y}{2}) & \frac{1}{2} \leq x < 1
\end{cases}$$

on the unit square; it essentially flattens the square then folds it back onto itself. 

The animation above shows the effect of applying this map repeatedly to 1000 random points in the square. Coded in <a href="https://gist.github.com/louismeunier/74ab6e2062666e158fad80e43d3fcd14">Mathematica</a>.