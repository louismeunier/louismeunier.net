---
title: "⨋ calculus"
description: "miscellaneous calculus-related visuals and code"
---

<u class="subtitle">Newton's method animation</u>

Newton's method animated to find the root of a function, $f(x)=x^3-2x^2-x+2$, with an initial estimate of $x = 0.15$.

$$
x_n = x_{n-1} - \frac{f(x_{n-1})}{f'(x_{n-1})}
$$

<div class="image-wrapper">
<img src="/images/newtonsmethod.gif">
</div>

```julia
# Julia
begin
    using LaTeXStrings, Plots;
	f(x) = x^3-2x^2-x+2
	g(x) = 3x^2-4x-1

	max_est = 6
	true_value = 1
	z = ones(max_est)
	z[1] = 0.15
	
	for i=2:max_est
		z[i] = z[i-1] - f(z[i-1])/g(z[i-1])
	end

	newtons_methods_animation = @animate for i = 1:max_est
	    plot(
			f,
			-1, 2,
			framestyle=:origin,
			legend=:none,
		)
		plot!(
			[z[i]],
			[0],
			color=:red, marker=:circle, markersize=5,
		)
        if (i > 1)
            est(x) = (
                g(z[i-1])*(x-z[i-1])
                )+f(z[i-1])
            plot!(est)
            plot!(
                [z[i-1], z[i-1]],
                [0, f(z[i-1])],
                color=:pink
            )
            plot!(
                [z[i-1]],
                [0],
                color=:red, 
                marker=:circle, 
                markersize=5,
            )
            annotate!(
                [z[i-1]],
                [-0.2],
                latexstring("x_{", i-1, "}"),
            ) 
        end
        plot!(
            [z[i], z[i]],
            [0, f(z[i])],
            color=:purple
        )
        annotate!(
            [z[i]],
            [0.2],
            latexstring("x_{", i, "}"),
        )
		annotate!(
			1.5,1.5, 
			text(
				latexstring("x_", string(i), " = ", string(round(z[i],digits=3)))
			)
		)
		annotate!(
			1.5, 1, 
			text(
				latexstring("\\% error = ", string(round(100*(abs(true_value - z[i]))/true_value, digits=3)))
			)
		)
		ylims!(-1,2.5)
	end 
	gif(newtons_methods_animation, "tutorial_heatmap_anim.gif", fps = 1)
end
```

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