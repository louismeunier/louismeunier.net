---
title: "Basic Statistics in R"
description: "Compilation of functions, visualizations in R"
weight: 3
---

{{< upbutton >}}

Some simple statistics functions in R (based on the course [MATH204](https://www.mcgill.ca/study/2022-2023/courses/math-204)).

````r
# read data
data <- read.csv("data.csv")

# utilities for working with/summarize data
ncol(data) # number of columns
nrow(data) # number of rows
colnames(data) # column names
rownames(data) # row names (if they exist)
head(data) # get the first "few" rows of a dataframe
tail(data) # get the last "few" rows of a dataframe
summary(data) # get more information then you'd ever need
data[data$x == "something", ] # get all rows from data from matching certain parameter(s)


data.lm <- lm(y ~ x, data = data) # fit a linear model

# working with the model (also applies to non-linear models made this way)
data.lm # just displays the coefficients
summary(data.lm) # displays coefficients, their standard errors, t-statistics, and p-values, etc.
anova(data.lm) # analysis of variance; F-statistic, etc
confint(data.lm, level=1-0.01) # confidence intervals for the coefficients
predict(data.lm, newdata = data.frame(x = 1:10)) # predict y values for x = 1:10
# make sure the column in the newdata is named the same as the column passed to lm!
# using predict, you can either predict for an individual response or mean response
# just change the "interval" argument to "prediction" or "confidence" respectively

# a linear model can be added as a line to a plot
plot(y ~ x, data = data)
abline(data.lm, col = "red")

lines(data$x[sort(x, index.return=T)$ix], data.lm[ix], col="red") # a non-linear model can also be added to a plot (just a little more complicated)
# this can be made a little fancier with ggplot to add the confidence intervals
library(ggplot2)
ggplot(data, aes(x = x, y = y)) +
  geom_point() +
  geom_smooth(method = "lm", se = TRUE, color = "red")

# lm can also be used to fit a polynomial
lm(y ~ x + I(x^2), data = data) # I() is used to indicate that x^2 is a variable, not an operation
# or covariates
lm(y ~ x + z, data = data)
# or interactions
lm(y ~ x*z, data = data) # note that this is the same as lm(y ~ x + z + x:z, data = data)

# test statistics can also be manually found
alpha = 0.05
df = 10
# t-test
t.test(y ~ x, data=data) # 1-tailed
t.test(y ~ x, data=data, var.equal=T) # 2-tailed

qt(1 - alpha/2, df = df) # t-statistic for a 95% confidence interval with 10 degrees of freedom
2*pt(-abs(2.228), df = df) # p-value for a t-statistic of 2.262 with 10 degrees of freedom; two-tailed

# Z-test
qnorm(1 - alpha/2) # z-statistic for a 95% confidence interval
2*pnorm(-abs(1.96)) # p-value for a z-statistic of 1.96; two-tailed

# F-test
qf(1 - alpha, df1 = 1, df2 = df) # F-statistic for a 95% confidence interval with 1 and 10 degrees of freedom
aov(y ~ x, data=data) # another way of doing a global F-test; wrap with summary() to get more information

# residuals
residuals(data.lm) # get the residuals of a model
data.lm$residuals # same as above
library(MASS) # library that makes it easy to work with residuals
data.lm.stdres <- stdres(residuals(data.lm)) # standardized residuals

par(mfrow = c(1, 2))
hist(data.lm.stdres) # plot the standardized residuals
qqnorm(data.lm.stdres) # plot the standardized residuals against a normal distribution
qqline(data.lm.stdres) # plot the standardized residuals against a normal distribution
# plotting these side-by-side is a good way to check if the residuals are normally distributed

library(interactions)
interact_plot(data.lm, pred = x.1, modx = x.2) # plot interactions (assuming data.lm is a model with an interaction)

boxplot(y ~ x, data=data) # box-plot, helpful for qualitative data
aggregate(x = data$y, by = list(data$x), FUN = mean) # get the mean of y for each x

anova(mod_1, mod_2) # compare two models, mod_1 smaller than mod_2

chisq.test(x_1, x_2) # chi-squared test, for categorical data
qchisq(1 - alpha, df = df. lower.tail=T) # chi-squared significant value

fisher.test(x_1, x_2) # fisher's exact test, for categorical data
mcnemar.test(data, correct = FALSE) # mcnemar's test, for paired categorical data

wilcox.test(x_1, x_2, alternative="greater", correct = F) # wilcoxon rank sum test
wilcox.test(x_1, x_2, alternative="greater", correct = F, exact = F) # wilcoxon rank sum test, larger samples, approximates normal distribution

````
<!-- todo: anova, kw, spearman -->