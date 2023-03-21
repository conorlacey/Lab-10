Lab 10 - Grading the professor, Pt. 2
================
Conor Lacey
03/21/2023

### Load packages and data

``` r
suppressWarnings(library(tidyverse))
suppressWarnings(library(tidymodels))
suppressWarnings(library(openintro))
```

### Exercise 1

``` r
m_bty <- lm(evals$score~evals$bty_avg)
summary(m_bty)
```

    ## 
    ## Call:
    ## lm(formula = evals$score ~ evals$bty_avg)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.9246 -0.3690  0.1420  0.3977  0.9309 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)    3.88034    0.07614   50.96  < 2e-16 ***
    ## evals$bty_avg  0.06664    0.01629    4.09 5.08e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5348 on 461 degrees of freedom
    ## Multiple R-squared:  0.03502,    Adjusted R-squared:  0.03293 
    ## F-statistic: 16.73 on 1 and 461 DF,  p-value: 5.083e-05

The linear model is:

score = 3.88 + 0.07(bty_avg)

The R^2 value is:

0.035

The Adjusted R^2 is:

0.033

### Exercise 2

``` r
m_bty_gen <- lm(evals$score~evals$bty_avg+evals$gender)
summary(m_bty_gen)
```

    ## 
    ## Call:
    ## lm(formula = evals$score ~ evals$bty_avg + evals$gender)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8305 -0.3625  0.1055  0.4213  0.9314 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       3.74734    0.08466  44.266  < 2e-16 ***
    ## evals$bty_avg     0.07416    0.01625   4.563 6.48e-06 ***
    ## evals$gendermale  0.17239    0.05022   3.433 0.000652 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5287 on 460 degrees of freedom
    ## Multiple R-squared:  0.05912,    Adjusted R-squared:  0.05503 
    ## F-statistic: 14.45 on 2 and 460 DF,  p-value: 8.177e-07

The linear model is:

score = 3.74 + 0.07(bty_avg) + 0.17(gender)

The R^2 value is:

0.06

The Adjusted R^2 is:

0.06
