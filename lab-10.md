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

### Exercise 3

Looking at m_bty_gen, we can notice a few things. The intercept
indicates the predicted average evaluation score of female professors
with an average beauty rating of 0. The bty_avg slope indicates that for
every 1 point increase in bty_avg a professor’s estimated average
evaluation score increases by 0.07. The gender slope indicates that if a
professor is a male, their predicted average evaluation score will
increase by 0.17.

### Exericse 4

5.9% iof the variability in score can be explained by the m_bty_gen
model.

### Exercise 5

score = 3.91 + 0.07(bty_avg)

### Exercise 6

Male

### Exercise 7

``` r
evals %>% ggplot (aes(x = bty_avg, y = score, color = gender)) + 
  geom_smooth(method = lm, se = FALSE, fullrange = TRUE)
```

    ## `geom_smooth()` using formula = 'y ~ x'

![](lab-10_files/figure-gfm/male%20and%20female%20score~bty_avg-1.png)<!-- -->

Males typically have a stronger relationship between bty_avg and scores
than females.

### Exercise 8

The adjusted R^2 value for m_bty is smaller than m_bty_gen. The gender
variable helps by explaining more variance in the scores when we already
have information on the beauty score of the professor.

### Exercise 9

The addition of gender didn’t really change the bty_avg slope between
m_bty and m_bty_gen.

### Exercise 10
