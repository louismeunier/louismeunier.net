---
title: "calculus"
description: "miscellaneous calculus-related visuals and code"
---

<u class="subtitle">chain rule tree diagrams</u>

<div class="image-wrapper">
<img src="/images/treegraph.png" style="height:250px!important;"/>
</div>

How I make trees to visualize the chain rule of derivatives (in Mathematica). I used the `MaTeX` package to render the labels as latex, but this could be replace with just normal text strings.

```mathematica
(* mathematica *)
<< MaTeX`
Graph[
 {
  Labeled[1, MaTeX["z", FontSize -> 16]],
  Labeled[2, MaTeX["x", FontSize -> 16]],
  Labeled[3, MaTeX["y", FontSize -> 16]],
  Labeled[4, MaTeX["s", FontSize -> 16]],
  Labeled[5, MaTeX["t", FontSize -> 16]],
  Labeled[6, MaTeX["s", FontSize -> 16]],
  Labeled[7, MaTeX["t", FontSize -> 16]]
  },
 {
  1 <-> 2,
  2 <-> 4,
  1 <-> 3,
  2 <-> 5,
  3 <-> 6,
  3 <-> 7
  },
 EdgeLabels -> {
   1 <-> 2 -> 
    MaTeX["\\frac{\partial z}{\partial x}", FontSize -> 16],
   2 <-> 4 -> 
    MaTeX["\\frac{\partial x}{\partial s}", FontSize -> 16],
   1 <-> 3 -> 
    MaTeX["\\frac{\partial z}{\partial y}", FontSize -> 16],
   2 <-> 5 -> 
    MaTeX["\\frac{\partial x}{\partial t}", FontSize -> 16],
   3 <-> 6 -> 
    MaTeX["\\frac{\partial y}{\partial s}", FontSize -> 16],
   3 <-> 7 -> MaTeX["\\frac{\partial y}{\partial t}", FontSize -> 16]
   },
 GraphLayout -> "LayeredEmbedding",
 EdgeStyle -> {
   1 <-> 2 -> Red,
   2 <-> 4 -> Red,
   1 <-> 3 -> Red,
   2 <-> 5 -> Gray,
   3 <-> 6 -> Red,
   3 <-> 7 -> Gray
   },
 VertexSize -> 0.05,
 VertexStyle -> LightPurple
]
```