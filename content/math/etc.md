---
title: "Etc"
description: "Random scripts/snippets/mathing"
weight: 1000
image: /images/wcaraster.png
---

{{< upbutton >}}

<div class="image-wrapper">
<img src="/images/wcaraster.png">
</div>

Raster map representing distance from nearest WCA competition (USA)


<div class="links">
<a class="fake-button" target="_blank" href="https://gist.github.com/louismeunier/4897b653f2c40411d25ab6082a75df35">
<button class="btn btn-info">source code</button>
</a>
</div>


<!-- ```r
# raster map of us with points from wca competitions
library("sf")
library("rgdal")
library("raster")
library("RMySQL")

# competition data from sql
mysqlconnection = dbConnect(RMySQL::MySQL(),
                            dbname='wca_dev',
                            host='localhost',
                            port=3306,
                            user='root',
                            password='password')

all_comps = dbGetQuery(mysqlconnection, "select id, latitude/1000000 as lat, longitude/1000000 as lon from competitions")

# shp file
us_shp <- read_sf("/users/louismeunier/downloads/cb_2018_us_state_20m/cb_2018_us_state_20m.shp")

# only want cont. us
continental <- us_shp[!us_shp$NAME %in% c("Alaska", "Hawaii", "Puerto Rico"), ]

# rasterize
r <- raster(ncol=100, nrow=100)
extent(r) <- extent(continental)
rr <- rasterize(continental, r)

coords <- cbind(all_comps$lon, all_comps$lat)

D <- distanceFromPoints(object=rr, xy=coords)

# ignore points outside cont. us
D[which(is.na(rr[]))] <- NA

plot(D, xaxt='n', yaxt='n')
points(coords, pch=19, cex=0.25)
lines(continental)

# get max point
D.dataframe <- data.frame(rasterToPoints(D))
D.dataframe.sorted <- D.dataframe[order(D.dataframe$layer),]
maxpoint <- D.dataframe[D.dataframe$layer ==max(D.dataframe$layer),]
points(maxpoint$x, maxpoint$y, pch=19, cex=1, col='red')
``` -->

Interactive normal distribution PDF plot

<div class="links">
<a class="fake-button" target="_blank" href="https://gist.github.com/louismeunier/a8199ce43dea4152d1f35fd526f59d88">
<button class="btn btn-info">source code</button>
</a>
</div>

<!-- ```mathematica
% interactive normal distribution plot, playing around with manipulate function
Manipulate[
 Show[
  Plot[
   PDF[NormalDistribution[\[Mu], \[Sigma]], x], 
   {x, -10, 10}, 
   AxesOrigin -> {0, 0},
   PlotRange -> {-0.1, 0.5},
   PlotLabel -> 
    "\[ScriptCapitalN](" <> ToString[\[Mu]] <> "," <> 
     ToString[\[Sigma]] <> ")",
   PlotStyle -> Directive[Gray, Thickness[0.007]]
   ],
  Plot[
   {PDF[NormalDistribution[\[Mu], \[Sigma]], x], 0}, 
   	{x, T, 10}, 
   	Filling -> 1 -> {2},
   FillingStyle -> RGBColor[255/255, 148/255, 112/255, 0.8],
   PlotRange -> {-0.1, 0.5},
   PlotStyle -> None
   ]
  ],
 {{\[Mu], 0., Dynamic["\[Mu]=" <> ToString[\[Mu]]]}, -10., 10., 0.2},
 {{\[Sigma], 1., Dynamic["\[Sigma]=" <> ToString[\[Sigma]]]}, 1., 5., 
  0.1},
 {{T, \[Mu], Dynamic["T=" <> ToString[T]]}, \[Mu] - 2.5*\[Sigma], 
  2.5*\[Sigma] + \[Mu], 0.1},
 Delimiter,
 Item[Dynamic[Style["p-value=" <> ToString[Round[
       NIntegrate[
        PDF[NormalDistribution[\[Mu], \[Sigma]], x] // Evaluate, {x, 
         T, Infinity}]
       , 0.001]], FontSize -> 15]], Alignment -> Center]
 ]
 ``` -->

<a href="https://diversityinmath.ssmu.ca/">McGill Diversity in Math</a> logo (roughly) remade in Mathematica


<div class="links">
<a class="fake-button" target="_blank" href="https://gist.github.com/louismeunier/8a49a140bad105116aa22d177b2968a9">
<button class="btn btn-info">source code</button>
</a>
</div>

 <!-- ```mathematica
% diversity in math logo made in mathematica!
% just a mobius strip with fancy colors...
x[r_, \[Theta]_] := (1 + r/2 Cos[\[Theta]/2]) Cos[\[Theta]]
y[r_, \[Theta]_] := (1 + r/2 Cos[\[Theta]/2]) Sin[\[Theta]]
z[r_, \[Theta]_] := (r/2 Sin[\[Theta]/2]) 

ParametricPlot3D[
 {
  x[r, \[Theta]],
  -y[r, \[Theta]],
  0.75*z[r, \[Theta]]
  },
 {r, -1, 1}, {\[Theta], 0, 2 \[Pi]},
 PlotStyle -> Red, Mesh -> {10, 1}, MeshStyle -> Black, 
 MeshShading -> {RGBColor["#CE0000"], RGBColor["#FF0000"], 
   RGBColor["#FF5252"]}, MeshFunctions -> {#5 &}, Boxed -> False, 
 Axes -> False, Background -> Black
 ]
``` -->

Henon map in MatLab (single initial condition)
$$x_{n+1} = 1 - ax_{n}^2+y_n$$
$$y_{n+1}=bx_n$$


<div class="links">
<a class="fake-button" target="_blank" href="https://gist.github.com/louismeunier/3a85877f82f2da993c4f39b0d04588c7">
<button class="btn btn-info">source code</button>
</a>
</div>


<!-- ```matlab
% henon map plotter
% initial condition

x1=0;
y1=0;

% parameters
a=1.4;
b=0.3;

xs = zeros(10000);
ys = zeros(10000);
xs(1)=x1;
ys(1)=y1;

figure;
hold on;
axis([-2 2 -2 2]);
plot(xs(1), ys(1), '--.', Color='red')
for n=2:10000
 
    xs(n)=1-a*xs(n-1)^2+ys(n-1);
    ys(n)=b*xs(n-1);
    plot(xs(n), ys(n), '--.', Color='black')
    pause(0.01);
end

hold off;
``` -->