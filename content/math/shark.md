---
title: "🦈 \"the shark question\""
description: ""
---

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