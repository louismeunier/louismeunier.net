---
title: "⬜️ visualizing tangent planes"
description: "graphs and code of tangent planes of functions"
---

<u class="subtitle">tangent plane of a function of $x$ and $y$</u>

Finding the tangent plane of: $$f(x,y) = 4x^2+4xy+y^2+2x+5y+3$$ at: $$(x_0,y_0,z_0) = (-3,1,27)$$

$$
t(x,y) - z_0 = \frac{\partial f}{\partial x}(x,y)(x-x_0) + \frac{\partial f}{\partial y}(x,y)(y-y_0)
$$
$$t(x,y) = -18x-5y-22$$

{{< plotly json="/math/testgraph.json" height="550px" modebar="false">}}

```julia
# Julia
begin
	using  Plots;
	
	plotly()

	transparent_red = RGBA(200/255,60/255,60/255,200/255)
	transparent_gray = RGBA(30/255,30/255,30/255,230/255)
	
	abc(x,y) = 4x^2+4x*y+y^2+2x+5y+3

	x_range = range(-10,stop=10,length=100)
	
	surface(
		x_range,
		x_range,
		abc,
		color = transparent_red,
		label = "f(x,y)",
		legend = :none
	)
	
	surface!(
		x_range,
		x_range,
		(x,y) -> -18x-5y-22,
		color = transparent_gray,
		label = "t(x,y)"
	)
	
	plot!(
		[-3], [1], [27], 
		color=:blue, 
		marker=:circle, 
		markersize=2, 
		label = "point"
	)
end
```

<u class="subtitle">tangent plane of a parametric function</u>

Given a sphere defined parametrically as a function $F(x,y,z)$:

$$x = r\cos\theta\sin\phi$$
$$y = r\cos\theta\cos\phi$$
$$z = r\sin\theta$$
 
where $r$ is the radius of the sphere, $\theta$ is the polar angle (along the $x-z$ plane), and $\phi$ is the azimuthal angle (along the $x-y$ plane). Since $x$, $y$, and $z$ are all functions of $\theta$ and $\phi$, we can define a vector function $G(\theta,\phi)$:

$$G(\theta,\phi) = \langle x(\theta,\phi), y(\theta,\phi), z(\theta,\phi)\rangle$$
$$=\langle r\cos\theta\sin\phi,\cos\theta\cos\phi,r\sin\theta \rangle$$

Taking the derivative of $G$ with respect to $\theta$ and $\phi$:

$$G_{\theta} = \langle -r\sin\theta\sin\phi, -r\sin\theta\cos\phi, r\cos\theta\rangle$$
$$G_{\phi} = \langle r\cos\theta\cos\phi, -r\cos\theta\sin\phi, 0\rangle$$

These functions represent vectors, clearly, and are tangent to the sphere at some point, say, $P(\theta_0, \phi_0)$. Intuitively, we can find the equation for a normal line to the sphere at $P$ by taking the cross product of $G_{\theta}$ and $G_{\phi}$, as this yields the vector normal to both:

$$G_{\perp} = G_{\theta}\times G_{\phi} = \langle r^2 \cos \theta \sin \theta \sin \phi, -r^2 \cos \theta \sin \theta \cos \phi, -r^2 \cos^2 \theta\rangle$$

The tangent plane to the sphere at $P$, intuitively, is also normal to this vector. Thus, we can find an equation for the plane by taking the dot product of the normal vector with the corresponding $(x_0,y_0,z_0)$ to $P$:

$$0 = G_{\perp} \cdot \langle x-x_0, y-y_0, z-z_0 \rangle$$

$$0 = r^2 \cos \theta \sin \theta \sin \phi (x-x_0) -r^2 \cos \theta \sin \theta \cos \phi (y-y_0) -r^2 \cos^2 \theta (z-z_0) $$

Rearranging for $z$ as a function of $x$ and $y$:

$$z = \frac{r^2 \cos \theta \sin \theta \sin \phi (x-x_0) -r^2 \cos \theta \sin \theta \cos \phi (y-y_0)}{r^2 \cos^2 \theta} -z_0 $$

For instance, take $P = (x,y,z) = (1,1,\sqrt{2})$. The tangent plane at this point, simplified:

$$z = \frac{1}{2}x + \frac{1}{2}y - \sqrt{2}$$

{{< plotly json="/math/tangent_plane_sphere.json" height="550px" modebar="false">}}

```julia
# Julia
begin
    using Plots; plotly()

    # radius of the sphere
    r = 2
    # point to find the tangent at
    x_0 = 1
    y_0 = 1
    # working with square roots is a little finicky... 
    z_0 = -sqrt(2)

    # parametric equations of the sphere in terms of theta and phi
	x_sphere(theta, phi) = r*cos(theta) * sin(phi) 
	y_sphere(theta, phi) = r*cos(theta) * cos(phi) 
	z_sphere(theta, phi) = r*sin(theta)
    # the corresponding theta and phi to the point (x_0, y_0, z_0)
    theta_param = asin(z_0/r)
    phi_param = acos(y_0 / (r * cos(theta_param)))
	
    # range of theta and phi to plot the sphere
	theta_range =range(-2pi, stop=2pi, length=100)
	phi_range = range(-2pi, stop=2pi, length=100)
    # plot ranges for sphere
	x_range_sphere = [x_sphere(t, p) for t in theta_range, p in phi_range]
	y_range_sphere = [y_sphere(t, p) for t in theta_range, p in phi_range]
	z_range_sphere = [z_sphere(t, p) for t in theta_range, p in phi_range]
    # sphere plot
	surface(
        x_range_sphere, 
        y_range_sphere, 
        z_range_sphere, 
        label="Sphere", 
        color=RGBA(172/255, 39/255, 245/255, 1),
        legend=:none
    )

    # derivatives the parametric equations of the sphere:
    # in terms of theta
    d_theta_x(theta, phi) = -r*sin(theta) * sin(phi)
    d_theta_y(theta, phi) = -r*sin(theta) * cos(phi)
    d_theta_z(theta, phi) = r*cos(theta)
    # in terms of phi
    d_phi_x(theta, phi) = r*cos(theta) * cos(phi)
    d_phi_y(theta, phi) = -r*cos(theta) * sin(phi)
    d_phi_z(theta, phi) = 0

    # a vector of "d_theta" of the sphere at the point (x_0, y_0, z_0)
    d_theta_vec = [
        d_theta_x(theta_param, phi_param), 
        d_theta_y(theta_param, phi_param), 
        d_theta_z(theta_param, phi_param)
    ]
    # a vector of "d_phi" of the sphere at the point (x_0, y_0, z_0)
    d_phi_vec = [
        d_phi_x(theta_param, phi_param), 
        d_phi_y(theta_param, phi_param), 
        d_phi_z(theta_param, phi_param)
    ]
    # plotting the respective tangent vectors
    plot!(
        [x_0-d_theta_vec[1], x_0], 
        [y_0-d_theta_vec[2], y_0], 
        [-z_0+d_theta_vec[3], -z_0],
        label="Tangent Vector, theta", 
        color=RGBA(0/255, 255, 0/255, 1)
    )
    plot!(
        [x_0, x_0 + d_phi_vec[1]], 
        [y_0, y_0 + d_phi_vec[2]], 
        [-z_0, -z_0 + d_phi_vec[3]], 
        label="Tangent Vector, phi", 
        color=RGBA(255, 0/255, 0/255, 1)
    )

    # the cross product of the two vectors above
    # this returns the line normal to the sphere at the point (x_0, y_0, z_0)
    d_cross = cross( d_theta_vec, d_phi_vec )
    plot!(
        [x_0, x_0+d_cross[1]], 
        [y_0,  y_0+d_cross[2]], 
        [-z_0,  -z_0-d_cross[3]], 
        label="Normal Vector", 
        color=RGBA(0/255, 0/255, 255, 1)
    )
    # the tangent plane: dot product of the cross product
    tangent_plane(x,y) = (
        d_cross[1]*(x-x_0) + 
        d_cross[2]*(y-y_0) - 
        d_cross[3]*z_0
    )/d_cross[3]
    # range of the tangent to plot
	x_range_tangent = range(-3, stop=3, length=100)
	y_range_tangent = range(-3, stop=3, length=100)
    z_range_tangent = [tangent_plane(a,b) for a in x_range_tangent, b in y_range_tangent]
    # plot tangent
	surface!(
        x_range_tangent, 
        y_range_tangent, 
        z_range_tangent, 
        label="Tangent Plane",
        color=RGBA(0, 0, 0, 0.3)
    )
end
```