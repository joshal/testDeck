---
title       : Predicting fuel efficiency from vehicle weight
subtitle    : Data meets automobile engineering
author      : Joshal
job         : Student, Developing Data Products
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js       # {highlight.js, prettify, highlight}
hitheme     : tomorrow           # 
widgets     : [mathjax, interactive]          # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

# The Problem

 * [Going green](http://www.fueleconomy.gov/) is good, knowing how to go green is better!
 * A lot of [research](http://www.nasa.gov/offices/ipp/centers/dfrc/news_events/SS-Truck-Aerodynamics.html#.U5abm3Wx15Q) is being carried out to improve fuel economy 
 * With so many options to choose from, buying a fuel efficient vehicle can be a tough choice
 * **Question:** Can we predict the miles per gallon of an automobile from it's weight?

---

# The Solution: The Data Model

 * Historical data on car fuel economy given it's weight is available
 * Sophisticated prediction models can be computed fast given today's computing power
 * We fit a linear prediction model to the given data of car weight and MPG
 * The least squares fit to the solution contains the line $Y = \hat \beta_0 + \hat \beta_1 X$ where,
    $$\hat \beta_1 = Cor(Y, X) \frac{Sd(Y)}{Sd(X)} ~~~ \hat \beta_0 = \bar Y - \hat \beta_1 \bar X$$
    
    
    ```r
    data(mtcars)
    
    mpg <- mtcars$mpg  # Predictor
    weight <- mtcars$wt  # Input
    beta1 <- sd(mpg)/sd(weight) * cor(mpg, weight)
    beta0 <- mean(mpg) - mean(weight) * beta1
    
    # Compute the linear model fit
    fit <- lm(mpg ~ wt, data = mtcars)
    
    summary(fit)
    ```
    
    
    Call:
    lm(formula = mpg ~ wt, data = mtcars)
    
    Residuals:
       Min     1Q Median     3Q    Max 
    -4.543 -2.365 -0.125  1.410  6.873 
    
    Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
    (Intercept)   37.285      1.878   19.86  < 2e-16 ***
    wt            -5.344      0.559   -9.56  1.3e-10 ***
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    
    Residual standard error: 3.05 on 30 degrees of freedom
    Multiple R-squared:  0.753,	Adjusted R-squared:  0.745 
    F-statistic: 91.4 on 1 and 30 DF,  p-value: 1.29e-10


---

# The interactive tool: A Shiny app

 * We have the capacity to predict the MPG (as $Y$ in the model) from the weight (as $X$ in the model)
 * Imagine a GUI tool which can help a customer know the fuel consumption of a vehicle
 * We present a very user-friendly web tool using a Shiny app in R proramming language:
 https://joshal.shinyapps.io/code/
 * The data is predicted using the `mtcars` dataset available in R

---

# Conclusion

 * We have addressed a unique and interesting problem of predicting fuel consumption of a vehcile
 * We presented a solution by providing an easy-to-use tool built using Shiny
 * We observe that fuel efficincy decreases as the weight of a vehicle increases
 
