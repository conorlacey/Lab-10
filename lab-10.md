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

``` r
m_bty_rank <- lm(evals$score ~ evals$gender + evals$rank)
summary(m_bty_rank)
```

    ## 
    ## Call:
    ## lm(formula = evals$score ~ evals$gender + evals$rank)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.7941 -0.3418  0.1011  0.4105  0.9781 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             4.19887    0.05954  70.520  < 2e-16 ***
    ## evals$gendermale        0.16760    0.05272   3.179  0.00158 ** 
    ## evals$ranktenure track -0.10476    0.07450  -1.406  0.16033    
    ## evals$ranktenured      -0.17699    0.06373  -2.777  0.00570 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5366 on 459 degrees of freedom
    ## Multiple R-squared:  0.03292,    Adjusted R-squared:  0.0266 
    ## F-statistic: 5.208 on 3 and 459 DF,  p-value: 0.001519

The linear model is:

score = 4.2 + .17(gender) + -0.1(tenure_tack) + -.17(tenured)

Looking at m_bty_rank, we can notice a few things. The intercept
indicates the predicted average evaluation score of female teaching
professors. The gender slope indicates professor’s average evaluation
score increases by .17 if they are male. The tenure_track slope
indicates that tenure_track professors decrease in their predicted
average evaluation score by -.1. The tenured slope indicates that
tenured professors decrease in their predicated average evaluation score
by -.17.

### Exercise 11

Total number of students in the class. I can’t think of any reason why
number of students would be related to evaluation scores.

### Exercise 12

``` r
m_cls_students <- lm(evals$score ~ evals$cls_students)
summary(m_cls_students)
```

    ## 
    ## Call:
    ## lm(formula = evals$score ~ evals$cls_students)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -1.8666 -0.3677  0.1281  0.4300  0.8336 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        4.1643491  0.0314034 132.608   <2e-16 ***
    ## evals$cls_students 0.0001881  0.0003373   0.558    0.577    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5443 on 461 degrees of freedom
    ## Multiple R-squared:  0.0006744,  Adjusted R-squared:  -0.001493 
    ## F-statistic: 0.3111 on 1 and 461 DF,  p-value: 0.5773

Haha! I was right.

### Exercise 13

cls_perc_eval should not be included. cls_did_eval is essentially the
same variable except it is not in percent form, it is instead a count of
students who completed the evaluation. However, using a count versus
using a percent seems arbitrary for linear models considering they are
both describing the magnitude of students who completed the evaluation.
As a result, I think we can take this one out because it would be doing
the same thing as cls_did_eval.

### Exercise 14

``` r
attach(evals)
m_allvars <- lm(score ~ rank + ethnicity + gender + language + age +cls_did_eval +
                  cls_students + cls_level + cls_profs + cls_credits + bty_avg) 
summary(m_allvars)
```

    ## 
    ## Call:
    ## lm(formula = score ~ rank + ethnicity + gender + language + age + 
    ##     cls_did_eval + cls_students + cls_level + cls_profs + cls_credits + 
    ##     bty_avg)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.81081 -0.31219  0.08483  0.37165  0.95661 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.957168   0.208299  18.998  < 2e-16 ***
    ## ranktenure track      -0.097165   0.082662  -1.175 0.240439    
    ## ranktenured           -0.041744   0.065533  -0.637 0.524454    
    ## ethnicitynot minority  0.167748   0.077699   2.159 0.031381 *  
    ## gendermale             0.185994   0.051880   3.585 0.000374 ***
    ## languagenon-english   -0.140321   0.108539  -1.293 0.196737    
    ## age                   -0.006753   0.003099  -2.179 0.029842 *  
    ## cls_did_eval           0.006908   0.002304   2.998 0.002864 ** 
    ## cls_students          -0.004059   0.001395  -2.910 0.003793 ** 
    ## cls_levelupper        -0.005692   0.056590  -0.101 0.919922    
    ## cls_profssingle        0.009144   0.051449   0.178 0.859015    
    ## cls_creditsone credit  0.517234   0.117531   4.401 1.35e-05 ***
    ## bty_avg                0.065052   0.016660   3.905 0.000109 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.5065 on 450 degrees of freedom
    ## Multiple R-squared:  0.1553, Adjusted R-squared:  0.1328 
    ## F-statistic: 6.895 on 12 and 450 DF,  p-value: 1.688e-11

``` r
detach(evals)
```

### Exercise 15

``` r
attach(evals)
m_allvars <- lm(score ~ ethnicity + gender + language + age + cls_did_eval +
                  cls_students + cls_credits + bty_avg) 
summary(m_allvars)
```

    ## 
    ## Call:
    ## lm(formula = score ~ ethnicity + gender + language + age + cls_did_eval + 
    ##     cls_students + cls_credits + bty_avg)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -1.84932 -0.31610  0.06814  0.37118  0.94225 
    ## 
    ## Coefficients:
    ##                        Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            3.827108   0.172412  22.197  < 2e-16 ***
    ## ethnicitynot minority  0.174664   0.074734   2.337 0.019866 *  
    ## gendermale             0.186761   0.050638   3.688 0.000253 ***
    ## languagenon-english   -0.169595   0.103940  -1.632 0.103442    
    ## age                   -0.005222   0.002616  -1.996 0.046521 *  
    ## cls_did_eval           0.007057   0.002257   3.127 0.001878 ** 
    ## cls_students          -0.004164   0.001353  -3.078 0.002212 ** 
    ## cls_creditsone credit  0.540358   0.105292   5.132 4.26e-07 ***
    ## bty_avg                0.066005   0.016483   4.004 7.26e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.505 on 454 degrees of freedom
    ## Multiple R-squared:  0.1526, Adjusted R-squared:  0.1377 
    ## F-statistic: 10.22 on 8 and 454 DF,  p-value: 3.622e-13

``` r
detach(evals)
```

The linear model is:

score = 3.83 + non_minority(.17) + male(.19) + non-English(-.17) +
age(-.005) + cls_did_eval(0.007) + cls_students(-0.004) + credit(0.54) +
bty_avg(0.066)
