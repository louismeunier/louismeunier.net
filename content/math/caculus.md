---
title: "⨋ calculus"
description: "miscellaneous calculus-related visuals and code"
---

<u class="subtitle">Visualizing a parametrically defined curve orthogonal to a surface</u>

The curve $F$ is defined parametrically by $x(t) = \frac{2(t^3+2)}{3}$, $y(t) = 2t^2$, and $z(t) = 3t-2$. The surface $G$ is defined implicitly as $15 = x^2+2y^2+3z^2$. $F$ is perpendicular to $G$ at $P = (2,2,1)$. We can prove this by finding the gradient of the two functions; if the two functions are truly perpendicular at this point, then the gradients should simply by multiples of each other.

$$\nabla \vec{G}(t) = \langle 2t^2, 4t, 3\rangle$$

$$\nabla \vec{F}(x,y,z) = \langle 2x, 4y, 6z\rangle$$

At the point $P$, $t = 1$, so we can find the gradients at $P$:

$$\nabla \vec{G}(1) = \langle 2, 4, 3\rangle$$

$$\nabla \vec{F}(2,2,1) = \langle 4, 8, 6\rangle$$

Clearly, $\nabla \vec{G}(1) = 2\nabla \vec{F}(2,2,1)$, indicating these two gradients are in the same direction, and as such, the curve $F$ is perpendicular to the surface $G$ at $P$. This can be understandably difficult to reason, so the following visualization may help.

{{< plotly json="/math/perpendicularparametric.json" height="550px" modebar="false">}}

```julia
# julia
# MATH150 Assignment 5, Problem 9a
begin
using Plots; plotly()
# general "settings"
t_range = range(0.95, stop=1.05, length = 100)
P = [2,2,1]
# F, a curve defined parametrically
x(t) = 2(t^3+2)/3
y(t) = 2t^2
z(t) = 3t-2

F_x_range = x.(t_range)
F_y_range = y.(t_range)
F_z_range = z.(t_range)

plot(F_x_range, F_y_range, F_z_range, color=RGBA(0,0,255,0.5), linewidth=3, label="F", legend=false)

# G
g(x,y) = sqrt((15-x^2-2y^2)/3)
G_x_range = range(1.9, stop=2.1, length = 100)
G_y_range = range(1.9, stop=2.1, length = 100)
# G_z_range = g.(G_x_range, G_y_range)
surface!(G_x_range, G_y_range, g, color=RGBA(255,0,0,0.5), linewidth=3, label="G", legend=true)
# plotting the point of interest
plot!(
    [2],[2],[1],
    marker = (:circle, 1, 0.8, :black),
    label = "P(2,2,1)"
)

# I multiply each vector by a scalar to make them fit within the bounds of the functions
scalar = 0.01
# plot the gradient of G
grad_G_x(t) = 2t^2
grad_G_y(t) = 4t
grad_G_z(t) = 3
# note that t = 1 at P = (2,2,1)
plot!(
    [P[1], P[1]+scalar*grad_G_x(1)],
    [P[2], P[2]+scalar*grad_G_y(1)], 
    [P[3], P[3]+scalar*grad_G_z(1)],
    color=:green,
    linewidth=6,
    label="grad G(2,2,1)"
)

# plot the gradient of F
grad_F_x(x,y,z) = 2x
grad_F_y(x,y,z) = 4y
grad_F_z(x,y,z) = 6z

plot!(
    [2, 2+scalar*grad_F_x(P[1],P[2],P[3])],
    [2, 2+scalar*grad_F_y(P[1],P[2],P[3])], 
    [1, 1+scalar*grad_F_z(P[1],P[2],P[3])],
    color=:orange,
    linewidth=6,
    label="grad F(2,2,1)"
)
end
```



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

<u class="subtitle">"the shark problem"</u>
From the James Stewart Calculus book (pg. 985, no. 2).

*"Marine biologists have determined that when a shark detects the presence of blood in the water, it will swim in the direction in which the concentration of the blood increases most rapidly. Based on certain tests, the concentration of blood (in parts per million) at a point $P(x,y)$ on the surface of seawater is approximated by $$C(x,y) = e^{\frac{-(x^2+2y^2)}{10^4}}$$ where $x$ and $y$ are measured in meters in a rectangular coordinate system with the blood source at the origin."*

The graph below represents the situation, where $T(x)$ is the function of the direction that the shark will take given a particular starting point $P(x_0,y_0)$.
<div class="image-wrapper">
<img src="/images/shark-question.png">
</div>

```julia 
begin
    using Plots, LaTeXStrings; pyplot() 
    # initial condition
    x_0 = 8
    y_0 = -2
    # the "concentration of blood" on the surface of the water
    C(x,y) = ℯ^(-(x^2+2y^2)/(10^4))
    x_range = -10:0.1:10
    y_range = -10:0.1:10
    C_range = [C(x,y) for x in x_range, y in y_range]
    contourf(
        x_range,
        y_range,
        C_range, 
        color=:vikO,
        levels=20,
        dpi=300
    )

    t(x) = (y_0/(x_0)^2)*x^2
    t_range = t.(x_range)
    z_path_range = C.(x_range, t_range)
    plot!(
        x_range,
        t_range,
        color=:gray,
        linewidth = 2,
        label=L"T(x)"
    )
    plot!(
        [x_0],
        [y_0],
        color = :black,
        markersize = 4,
        marker = :circle,
        label = L"P(x_0, y_0)"
    )
    xlims!(-10,10)
    ylims!(-10,10)
end
```