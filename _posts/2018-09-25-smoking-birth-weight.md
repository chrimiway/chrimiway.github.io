---
layout:     post
title:      case study: what affects birth weight?
subtitle:   
date:       2018-09-25
author:     Zhenhua Wang
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - case study
---

Let's first load the data and create a summary table for this data set

``` r
smoke = read.csv("smoking.csv")
#names(smoke)
summary(smoke)
```

    ##        id            date        gestation         bwt.oz     
    ##  Min.   :  15   Min.   :1350   Min.   :148.0   Min.   : 55.0  
    ##  1st Qu.:5477   1st Qu.:1444   1st Qu.:272.0   1st Qu.:108.0  
    ##  Median :6734   Median :1540   Median :279.0   Median :119.0  
    ##  Mean   :6032   Mean   :1536   Mean   :278.5   Mean   :118.4  
    ##  3rd Qu.:7587   3rd Qu.:1627   3rd Qu.:286.0   3rd Qu.:129.0  
    ##  Max.   :9263   Max.   :1714   Max.   :338.0   Max.   :174.0  
    ##      parity           mrace            mage            med       
    ##  Min.   : 0.000   Min.   :0.000   Min.   :15.00   Min.   :0.000  
    ##  1st Qu.: 1.000   1st Qu.:0.000   1st Qu.:23.00   1st Qu.:2.000  
    ##  Median : 2.000   Median :2.000   Median :26.00   Median :2.000  
    ##  Mean   : 1.953   Mean   :2.995   Mean   :27.29   Mean   :2.932  
    ##  3rd Qu.: 3.000   3rd Qu.:7.000   3rd Qu.:31.00   3rd Qu.:4.000  
    ##  Max.   :11.000   Max.   :9.000   Max.   :45.00   Max.   :7.000  
    ##       mht           mpregwt           inc            smoke       
    ##  Min.   :53.00   Min.   : 87.0   Min.   :0.000   Min.   :0.0000  
    ##  1st Qu.:62.00   1st Qu.:113.0   1st Qu.:2.000   1st Qu.:0.0000  
    ##  Median :64.00   Median :125.0   Median :3.000   Median :0.0000  
    ##  Mean   :64.07   Mean   :128.5   Mean   :3.681   Mean   :0.4638  
    ##  3rd Qu.:66.00   3rd Qu.:140.0   3rd Qu.:5.000   3rd Qu.:1.0000  
    ##  Max.   :72.00   Max.   :220.0   Max.   :9.000   Max.   :1.0000

It seems no weird data in this dataset, and even no unknown values. Since I think that mother's age, age at termination of pregnancy, parity, income, have natural order in it, I should treat them as continous variables. For easy interpretation, I will fisrt mean-center *date*, *mht*, *mpregwt*, *mage*.

``` r
smoke$date_cent = smoke$date - mean(smoke$date)
smoke$mht_cent = smoke$mht - mean(smoke$mht)
smoke$mpregwt_cent = smoke$mpregwt - mean(smoke$mpregwt)
smoke$mage_cent = smoke$mage - mean(smoke$mage)
```

Let's start exploratory data analysis. First, I would like to see is there any relationships between birth weight and other continuous predictors.

``` r
plot(bwt.oz ~ date_cent, data = smoke)
```

![](./assignment3_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
plot(bwt.oz ~ parity, data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-3-2.png)

``` r
plot(bwt.oz ~ mage_cent, data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-3-3.png)

``` r
plot(bwt.oz ~ mht_cent, data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-3-4.png)

``` r
plot(bwt.oz ~ mpregwt_cent, data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-3-5.png)

``` r
plot(bwt.oz ~ inc, data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-3-6.png)

In the plots above, we could find out that most variables have fanning.

We then check the relationships between birth weight and categorical variables

``` r
boxplot(bwt.oz ~ as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
boxplot(bwt.oz ~ as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-4-2.png)

``` r
boxplot(bwt.oz ~ as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-4-3.png)

Not too much useful information.

We, then, could investigate about the interaction between those predictors.

``` r
#smoke
xyplot(bwt.oz ~ date_cent | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
xyplot(bwt.oz ~ parity | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-2.png)

``` r
xyplot(bwt.oz ~ mage_cent | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-3.png)

``` r
xyplot(bwt.oz ~ mht_cent | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-4.png)

``` r
xyplot(bwt.oz ~ mpregwt_cent | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-5.png)

``` r
xyplot(bwt.oz ~ inc | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-6.png)

``` r
bwplot(bwt.oz ~ as.factor(med) | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-7.png)

``` r
bwplot(bwt.oz ~ as.factor(mrace) | as.factor(smoke), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-8.png)

``` r
#mrace
xyplot(bwt.oz ~ date_cent | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-9.png)

``` r
xyplot(bwt.oz ~ parity | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-10.png)

``` r
xyplot(bwt.oz ~ mage_cent | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-11.png)

``` r
xyplot(bwt.oz ~ mht_cent | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-12.png)

``` r
xyplot(bwt.oz ~ mpregwt_cent | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-13.png)

``` r
xyplot(bwt.oz ~ inc | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-14.png)

``` r
bwplot(bwt.oz ~ as.factor(smoke) | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-15.png)

``` r
bwplot(bwt.oz ~ as.factor(med) | as.factor(mrace), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-16.png)

``` r
#med
xyplot(bwt.oz ~ date_cent | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-17.png)

``` r
xyplot(bwt.oz ~ parity | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-18.png)

``` r
xyplot(bwt.oz ~ mage_cent | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-19.png)

``` r
xyplot(bwt.oz ~ mht_cent | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-20.png)

``` r
xyplot(bwt.oz ~ mpregwt_cent | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-21.png)

``` r
xyplot(bwt.oz ~ inc | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-22.png)

``` r
bwplot(bwt.oz ~ as.factor(smoke) | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-23.png)

``` r
bwplot(bwt.oz ~ as.factor(mrace) | as.factor(med), data = smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-5-24.png)

``` r
round(cor(smoke[, 2:12]), 3)
```

    ##             date gestation bwt.oz parity  mrace   mage    med    mht
    ## date       1.000     0.065  0.092  0.080  0.056  0.065 -0.066 -0.066
    ## gestation  0.065     1.000  0.395 -0.133 -0.146 -0.031  0.064  0.061
    ## bwt.oz     0.092     0.395  1.000  0.041 -0.130  0.044  0.038  0.188
    ## parity     0.080    -0.133  0.041  1.000  0.149  0.524 -0.201 -0.043
    ## mrace      0.056    -0.146 -0.130  0.149  1.000  0.014 -0.079 -0.165
    ## mage       0.065    -0.031  0.044  0.524  0.014  1.000  0.134 -0.005
    ## med       -0.066     0.064  0.038 -0.201 -0.079  0.134  1.000  0.115
    ## mht       -0.066     0.061  0.188 -0.043 -0.165 -0.005  0.115  1.000
    ## mpregwt    0.025     0.069  0.182  0.151  0.023  0.146 -0.054  0.460
    ## inc        0.067     0.027  0.002  0.009 -0.122  0.297  0.217  0.071
    ## smoke     -0.079    -0.058 -0.249  0.011 -0.114 -0.070 -0.138  0.041
    ##           mpregwt    inc  smoke
    ## date        0.025  0.067 -0.079
    ## gestation   0.069  0.027 -0.058
    ## bwt.oz      0.182  0.002 -0.249
    ## parity      0.151  0.009  0.011
    ## mrace       0.023 -0.122 -0.114
    ## mage        0.146  0.297 -0.070
    ## med        -0.054  0.217 -0.138
    ## mht         0.460  0.071  0.041
    ## mpregwt     1.000 -0.005 -0.049
    ## inc        -0.005  1.000  0.007
    ## smoke      -0.049  0.007  1.000

From the plots above we can see that *med* interacts with *inc*, *mrace* interacts with *mht*, *smoke* interacts with *mrace*, *smoke* interacts with *med* and *mrace* interacts with *med*.

We first build a base case and then create a model with this interaction.

``` r
reg1 = lm(bwt.oz ~ as.factor(smoke) + as.factor(mrace) + as.factor(med) + date_cent +
           parity + mage_cent + mht_cent + mpregwt_cent + inc, data = smoke);

plot(y = reg1$residuals, x = smoke$date_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
plot(y = reg1$residuals, x = smoke$parity)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-2.png)

``` r
plot(y = reg1$residuals, x = smoke$mage_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-3.png)

``` r
plot(y = reg1$residuals, x = smoke$mht_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-4.png)

``` r
plot(y = reg1$residuals, x = smoke$mpregwt_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-5.png)

``` r
plot(y = reg1$residuals, x = smoke$inc)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-6.png)

``` r
boxplot(reg1$residuals ~ smoke$med)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-7.png)

``` r
boxplot(reg1$residuals~smoke$smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-8.png)

``` r
boxplot(reg1$residuals~smoke$mrace)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-6-9.png)

From the residual plots above, we could find out that there are some quadratic trends in *parity*, *pregnent weight* and *height*. Therefore, we could then add quadratic terms for those variables.

``` r
smoke$parity2 = smoke$parity^2
smoke$mpregwt_cent2 = smoke$mpregwt_cent^2
smoke$mht_cent2 = smoke$mht_cent^2

reg2 = lm(bwt.oz ~ as.factor(smoke) + as.factor(mrace) + as.factor(med) + date +
           parity + parity2 + mage_cent + mht_cent + mht_cent2 + mpregwt_cent + mpregwt_cent2 + inc, data = smoke)
anova(reg2)
```

    ## Analysis of Variance Table
    ## 
    ## Response: bwt.oz
    ##                   Df Sum Sq Mean Sq F value    Pr(>F)    
    ## as.factor(smoke)   1  17544 17544.0 64.0408 4.023e-15 ***
    ## as.factor(mrace)   9  12482  1386.9  5.0627 1.113e-06 ***
    ## as.factor(med)     6   1300   216.6  0.7907  0.577259    
    ## date               1   1472  1472.2  5.3740  0.020678 *  
    ## parity             1   1718  1718.4  6.2726  0.012450 *  
    ## parity2            1   2518  2517.7  9.1904  0.002507 ** 
    ## mage_cent          1     80    80.0  0.2922  0.588987    
    ## mht_cent           1   9575  9575.0 34.9515 4.907e-09 ***
    ## mht_cent2          1    978   978.2  3.5707  0.059150 .  
    ## mpregwt_cent       1   2800  2799.6 10.2192  0.001442 ** 
    ## mpregwt_cent2      1   1032  1032.4  3.7686  0.052556 .  
    ## inc                1    380   379.8  1.3863  0.239360    
    ## Residuals        843 230941   274.0                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

After do an ANOVO for the new model, we can see that those quadratic terms are significant to the model.

Next, we could try the interaction terms mentions above.

``` r
reg_inter = lm(bwt.oz ~ as.factor(mrace) + as.factor(med) + as.factor(smoke)
                + date
                + parity + parity2
                + mage_cent
                + as.factor(mrace) * (mht_cent + mht_cent2)
                + mpregwt_cent + mpregwt_cent2
                + as.factor(smoke) * inc 
                + as.factor(med) * inc
                + as.factor(smoke) * as.factor(med)
                + as.factor(med) * as.factor(mrace)
                , data = smoke); #summary(reg_inter)
```

After doing ANOVA for the new model with interaction, we can see that the interaction between *smoke* and *mht^2*, *smoke* and *inc*, *med* and *smoke* is not significant. Therefore, we could safely remove these terms from our model.

``` r
reg_inter2 = lm(bwt.oz ~ as.factor(mrace) + as.factor(med) + as.factor(smoke)
                + date
                + parity + parity2
                + mage_cent
                + as.factor(mrace) * mht_cent + mht_cent2
                + mpregwt_cent + mpregwt_cent2
                + as.factor(med) * inc
                + as.factor(med) * as.factor(mrace)
                , data = smoke); #summary(reg_inter2)
```

``` r
plot(y = reg2$residuals, x = smoke$date_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-1.png)

``` r
plot(y = reg2$residuals, x = smoke$parity)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-2.png)

``` r
plot(y = reg2$residuals, x = smoke$mage_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-3.png)

``` r
plot(y = reg2$residuals, x = smoke$mht_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-4.png)

``` r
plot(y = reg2$residuals, x = smoke$mpregwt_cent)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-5.png)

``` r
plot(y = reg2$residuals, x = smoke$inc)
abline(0,0)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-6.png)

``` r
boxplot(reg2$residuals~smoke$med)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-7.png)

``` r
boxplot(reg2$residuals~smoke$smoke)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-8.png)

``` r
boxplot(reg2$residuals~smoke$mrace)
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-10-9.png)

The residual plots between each predictor variables shows that this model is reasonablely well for this dataset.

We could then show the summary of the final model.

``` r
summary(reg_inter2)
```

    ## 
    ## Call:
    ## lm(formula = bwt.oz ~ as.factor(mrace) + as.factor(med) + as.factor(smoke) + 
    ##     date + parity + parity2 + mage_cent + as.factor(mrace) * 
    ##     mht_cent + mht_cent2 + mpregwt_cent + mpregwt_cent2 + as.factor(med) * 
    ##     inc + as.factor(med) * as.factor(mrace), data = smoke)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -54.233  -9.273   0.000   9.615  54.040 
    ## 
    ## Coefficients: (16 not defined because of singularities)
    ##                                     Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)                        1.720e+02  5.330e+01   3.228 0.001298
    ## as.factor(mrace)1                 -9.494e+01  5.538e+01  -1.714 0.086841
    ## as.factor(mrace)2                 -2.190e+00  6.581e+00  -0.333 0.739346
    ## as.factor(mrace)3                 -5.339e+01  5.084e+01  -1.050 0.293991
    ## as.factor(mrace)4                 -1.399e+01  3.971e+01  -0.352 0.724765
    ## as.factor(mrace)5                 -1.791e+00  3.929e+00  -0.456 0.648684
    ## as.factor(mrace)6                  1.760e+01  4.055e+01   0.434 0.664360
    ## as.factor(mrace)7                 -6.328e+01  4.901e+01  -1.291 0.197016
    ## as.factor(mrace)8                 -1.411e+01  6.704e+00  -2.105 0.035588
    ## as.factor(mrace)9                 -7.309e-01  6.409e+00  -0.114 0.909238
    ## as.factor(med)1                   -8.022e+01  5.286e+01  -1.517 0.129557
    ## as.factor(med)2                   -7.015e+01  5.273e+01  -1.330 0.183832
    ## as.factor(med)3                   -6.739e+01  5.325e+01  -1.266 0.206032
    ## as.factor(med)4                   -6.748e+01  5.280e+01  -1.278 0.201576
    ## as.factor(med)5                   -6.300e+01  5.286e+01  -1.192 0.233731
    ## as.factor(med)7                   -8.359e+01  4.466e+01  -1.872 0.061623
    ## as.factor(smoke)1                 -9.493e+00  1.187e+00  -7.998 4.48e-15
    ## date                               1.293e-02  5.408e-03   2.390 0.017083
    ## parity                             3.454e+00  7.984e-01   4.327 1.71e-05
    ## parity2                           -4.232e-01  1.044e-01  -4.053 5.55e-05
    ## mage_cent                         -1.653e-01  1.356e-01  -1.219 0.223070
    ## mht_cent                           6.671e-01  3.934e-01   1.696 0.090303
    ## mht_cent2                          7.847e-02  6.826e-02   1.150 0.250697
    ## mpregwt_cent                       1.405e-01  4.117e-02   3.413 0.000676
    ## mpregwt_cent2                     -1.531e-03  8.707e-04  -1.759 0.078994
    ## inc                               -1.106e+01  7.657e+00  -1.444 0.149127
    ## as.factor(mrace)1:mht_cent         2.392e+00  1.502e+00   1.592 0.111698
    ## as.factor(mrace)2:mht_cent         1.940e+00  1.542e+00   1.258 0.208757
    ## as.factor(mrace)3:mht_cent        -4.967e-01  1.184e+00  -0.419 0.675109
    ## as.factor(mrace)4:mht_cent        -4.806e-01  1.170e+00  -0.411 0.681318
    ## as.factor(mrace)5:mht_cent         2.187e+00  7.755e-01   2.821 0.004913
    ## as.factor(mrace)6:mht_cent         1.132e+00  2.424e+00   0.467 0.640762
    ## as.factor(mrace)7:mht_cent         5.972e-02  6.334e-01   0.094 0.924907
    ## as.factor(mrace)8:mht_cent        -3.916e+00  2.171e+00  -1.803 0.071703
    ## as.factor(mrace)9:mht_cent         1.311e+00  1.733e+00   0.757 0.449550
    ## as.factor(med)1:inc                1.358e+01  7.706e+00   1.762 0.078382
    ## as.factor(med)2:inc                1.082e+01  7.671e+00   1.410 0.158961
    ## as.factor(med)3:inc                1.099e+01  7.771e+00   1.414 0.157766
    ## as.factor(med)4:inc                1.095e+01  7.685e+00   1.425 0.154486
    ## as.factor(med)5:inc                9.431e+00  7.681e+00   1.228 0.219907
    ## as.factor(med)7:inc                1.227e+01  2.425e+01   0.506 0.613081
    ## as.factor(mrace)1:as.factor(med)1  1.160e+02  5.660e+01   2.050 0.040682
    ## as.factor(mrace)2:as.factor(med)1 -4.063e+01  1.767e+01  -2.299 0.021778
    ## as.factor(mrace)3:as.factor(med)1  5.945e+01  5.117e+01   1.162 0.245699
    ## as.factor(mrace)4:as.factor(med)1  6.352e+00  4.011e+01   0.158 0.874222
    ## as.factor(mrace)5:as.factor(med)1 -9.358e-01  6.603e+00  -0.142 0.887328
    ## as.factor(mrace)6:as.factor(med)1 -1.559e+00  4.047e+01  -0.039 0.969278
    ## as.factor(mrace)7:as.factor(med)1  6.066e+01  4.921e+01   1.233 0.218026
    ## as.factor(mrace)8:as.factor(med)1 -3.480e+00  1.727e+01  -0.202 0.840347
    ## as.factor(mrace)9:as.factor(med)1 -6.127e+00  1.351e+01  -0.453 0.650323
    ## as.factor(mrace)1:as.factor(med)2  9.672e+01  5.549e+01   1.743 0.081703
    ## as.factor(mrace)2:as.factor(med)2  1.156e+01  1.082e+01   1.068 0.286044
    ## as.factor(mrace)3:as.factor(med)2  5.516e+01  5.089e+01   1.084 0.278735
    ## as.factor(mrace)4:as.factor(med)2  1.844e+01  3.987e+01   0.463 0.643839
    ## as.factor(mrace)5:as.factor(med)2  1.788e+00  4.892e+00   0.365 0.714900
    ## as.factor(mrace)6:as.factor(med)2 -1.623e+01  4.025e+01  -0.403 0.686897
    ## as.factor(mrace)7:as.factor(med)2  5.571e+01  4.913e+01   1.134 0.257120
    ## as.factor(mrace)8:as.factor(med)2 -9.450e+00  7.936e+00  -1.191 0.234113
    ## as.factor(mrace)9:as.factor(med)2 -4.469e+00  1.024e+01  -0.436 0.662599
    ## as.factor(mrace)1:as.factor(med)3  1.079e+02  5.794e+01   1.863 0.062822
    ## as.factor(mrace)2:as.factor(med)3         NA         NA      NA       NA
    ## as.factor(mrace)3:as.factor(med)3         NA         NA      NA       NA
    ## as.factor(mrace)4:as.factor(med)3  7.625e-01  4.145e+01   0.018 0.985326
    ## as.factor(mrace)5:as.factor(med)3  6.583e+00  8.969e+00   0.734 0.463168
    ## as.factor(mrace)6:as.factor(med)3 -9.124e+00  4.188e+01  -0.218 0.827607
    ## as.factor(mrace)7:as.factor(med)3  3.577e+01  4.954e+01   0.722 0.470528
    ## as.factor(mrace)8:as.factor(med)3  1.035e+00  1.302e+01   0.079 0.936669
    ## as.factor(mrace)9:as.factor(med)3 -3.773e+00  1.802e+01  -0.209 0.834260
    ## as.factor(mrace)1:as.factor(med)4  8.652e+01  5.559e+01   1.556 0.120001
    ## as.factor(mrace)2:as.factor(med)4 -1.377e+01  9.355e+00  -1.472 0.141367
    ## as.factor(mrace)3:as.factor(med)4  5.012e+01  5.112e+01   0.980 0.327237
    ## as.factor(mrace)4:as.factor(med)4  1.400e+01  4.043e+01   0.346 0.729205
    ## as.factor(mrace)5:as.factor(med)4  1.540e-01  5.732e+00   0.027 0.978568
    ## as.factor(mrace)6:as.factor(med)4 -2.512e+01  4.350e+01  -0.577 0.563873
    ## as.factor(mrace)7:as.factor(med)4  5.138e+01  4.912e+01   1.046 0.295883
    ## as.factor(mrace)8:as.factor(med)4 -1.126e+01  7.615e+00  -1.479 0.139484
    ## as.factor(mrace)9:as.factor(med)4         NA         NA      NA       NA
    ## as.factor(mrace)1:as.factor(med)5  7.362e+01  5.571e+01   1.322 0.186699
    ## as.factor(mrace)2:as.factor(med)5         NA         NA      NA       NA
    ## as.factor(mrace)3:as.factor(med)5  5.796e+01  5.163e+01   1.123 0.261937
    ## as.factor(mrace)4:as.factor(med)5  1.260e+01  4.089e+01   0.308 0.757956
    ## as.factor(mrace)5:as.factor(med)5         NA         NA      NA       NA
    ## as.factor(mrace)6:as.factor(med)5 -1.978e+01  4.151e+01  -0.477 0.633723
    ## as.factor(mrace)7:as.factor(med)5  6.031e+01  4.933e+01   1.223 0.221865
    ## as.factor(mrace)8:as.factor(med)5         NA         NA      NA       NA
    ## as.factor(mrace)9:as.factor(med)5         NA         NA      NA       NA
    ## as.factor(mrace)1:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)2:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)3:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)4:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)5:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)6:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)7:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)8:as.factor(med)7         NA         NA      NA       NA
    ## as.factor(mrace)9:as.factor(med)7         NA         NA      NA       NA
    ##                                      
    ## (Intercept)                       ** 
    ## as.factor(mrace)1                 .  
    ## as.factor(mrace)2                    
    ## as.factor(mrace)3                    
    ## as.factor(mrace)4                    
    ## as.factor(mrace)5                    
    ## as.factor(mrace)6                    
    ## as.factor(mrace)7                    
    ## as.factor(mrace)8                 *  
    ## as.factor(mrace)9                    
    ## as.factor(med)1                      
    ## as.factor(med)2                      
    ## as.factor(med)3                      
    ## as.factor(med)4                      
    ## as.factor(med)5                      
    ## as.factor(med)7                   .  
    ## as.factor(smoke)1                 ***
    ## date                              *  
    ## parity                            ***
    ## parity2                           ***
    ## mage_cent                            
    ## mht_cent                          .  
    ## mht_cent2                            
    ## mpregwt_cent                      ***
    ## mpregwt_cent2                     .  
    ## inc                                  
    ## as.factor(mrace)1:mht_cent           
    ## as.factor(mrace)2:mht_cent           
    ## as.factor(mrace)3:mht_cent           
    ## as.factor(mrace)4:mht_cent           
    ## as.factor(mrace)5:mht_cent        ** 
    ## as.factor(mrace)6:mht_cent           
    ## as.factor(mrace)7:mht_cent           
    ## as.factor(mrace)8:mht_cent        .  
    ## as.factor(mrace)9:mht_cent           
    ## as.factor(med)1:inc               .  
    ## as.factor(med)2:inc                  
    ## as.factor(med)3:inc                  
    ## as.factor(med)4:inc                  
    ## as.factor(med)5:inc                  
    ## as.factor(med)7:inc                  
    ## as.factor(mrace)1:as.factor(med)1 *  
    ## as.factor(mrace)2:as.factor(med)1 *  
    ## as.factor(mrace)3:as.factor(med)1    
    ## as.factor(mrace)4:as.factor(med)1    
    ## as.factor(mrace)5:as.factor(med)1    
    ## as.factor(mrace)6:as.factor(med)1    
    ## as.factor(mrace)7:as.factor(med)1    
    ## as.factor(mrace)8:as.factor(med)1    
    ## as.factor(mrace)9:as.factor(med)1    
    ## as.factor(mrace)1:as.factor(med)2 .  
    ## as.factor(mrace)2:as.factor(med)2    
    ## as.factor(mrace)3:as.factor(med)2    
    ## as.factor(mrace)4:as.factor(med)2    
    ## as.factor(mrace)5:as.factor(med)2    
    ## as.factor(mrace)6:as.factor(med)2    
    ## as.factor(mrace)7:as.factor(med)2    
    ## as.factor(mrace)8:as.factor(med)2    
    ## as.factor(mrace)9:as.factor(med)2    
    ## as.factor(mrace)1:as.factor(med)3 .  
    ## as.factor(mrace)2:as.factor(med)3    
    ## as.factor(mrace)3:as.factor(med)3    
    ## as.factor(mrace)4:as.factor(med)3    
    ## as.factor(mrace)5:as.factor(med)3    
    ## as.factor(mrace)6:as.factor(med)3    
    ## as.factor(mrace)7:as.factor(med)3    
    ## as.factor(mrace)8:as.factor(med)3    
    ## as.factor(mrace)9:as.factor(med)3    
    ## as.factor(mrace)1:as.factor(med)4    
    ## as.factor(mrace)2:as.factor(med)4    
    ## as.factor(mrace)3:as.factor(med)4    
    ## as.factor(mrace)4:as.factor(med)4    
    ## as.factor(mrace)5:as.factor(med)4    
    ## as.factor(mrace)6:as.factor(med)4    
    ## as.factor(mrace)7:as.factor(med)4    
    ## as.factor(mrace)8:as.factor(med)4    
    ## as.factor(mrace)9:as.factor(med)4    
    ## as.factor(mrace)1:as.factor(med)5    
    ## as.factor(mrace)2:as.factor(med)5    
    ## as.factor(mrace)3:as.factor(med)5    
    ## as.factor(mrace)4:as.factor(med)5    
    ## as.factor(mrace)5:as.factor(med)5    
    ## as.factor(mrace)6:as.factor(med)5    
    ## as.factor(mrace)7:as.factor(med)5    
    ## as.factor(mrace)8:as.factor(med)5    
    ## as.factor(mrace)9:as.factor(med)5    
    ## as.factor(mrace)1:as.factor(med)7    
    ## as.factor(mrace)2:as.factor(med)7    
    ## as.factor(mrace)3:as.factor(med)7    
    ## as.factor(mrace)4:as.factor(med)7    
    ## as.factor(mrace)5:as.factor(med)7    
    ## as.factor(mrace)6:as.factor(med)7    
    ## as.factor(mrace)7:as.factor(med)7    
    ## as.factor(mrace)8:as.factor(med)7    
    ## as.factor(mrace)9:as.factor(med)7    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 16.12 on 790 degrees of freedom
    ## Multiple R-squared:  0.2741, Adjusted R-squared:  0.2024 
    ## F-statistic: 3.824 on 78 and 790 DF,  p-value: < 2.2e-16

TODO: interpretations!

Then, we could calculate the leverage and cook distance in order to analyse the influence of leverages.

``` r
library(MASS)
```

    ## 
    ## Attaching package: 'MASS'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     select

``` r
leverage = hatvalues(reg_inter2)
cooks = cooks.distance(reg_inter2)
smoke2 = cbind(smoke, leverage, cooks)
hist(leverage, main = "Leverage values for bwt regression")
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-12-1.png)

``` r
smoke2[smoke2$leverage > .8,]
```

    ##       id date gestation bwt.oz parity mrace mage med mht mpregwt inc smoke
    ## 30   818 1369       258    115      4     0   26   7  62     130   2     0
    ## 34  6987 1529       259    113      1     0   38   7  64     128   3     0
    ## 100  798 1414       272    110      2     8   25   1  60      90   2     0
    ## 113 2664 1537       273    111      4     7   43   0  62     138   2     0
    ## 140 7518 1593       275    124      1     6   28   7  61     116   1     0
    ## 161 9016 1660       276    118      1     6   34   4  64     116   3     0
    ## 217 7035 1481       280    110      3     1   39   0  67     125   0     0
    ## 235 7729 1645       281    128      3     9   28   3  63     150   2     0
    ## 457 6746 1475       309    114      0     3   27   0  62     118   2     0
    ## 467 6241 1379       223     68      1     7   32   0  66     149   5     1
    ## 496  207 1481       255     92      3     4   25   7  65     125   1     1
    ## 499 4639 1569       256     81      4     2   30   1  64     148   5     1
    ## 510 6122 1713       263    146     10     6   39   0  53     110   3     1
    ## 708 5689 1362       281    122      3     1   42   3  63     103   2     1
    ##        date_cent     mht_cent mpregwt_cent  mage_cent parity2
    ## 30  -167.4234753  -2.06904488    1.5212888 -1.2945915      16
    ## 34    -7.4234753  -0.06904488   -0.4787112 10.7054085       1
    ## 100 -122.4234753  -4.06904488  -38.4787112 -2.2945915       4
    ## 113    0.5765247  -2.06904488    9.5212888 15.7054085      16
    ## 140   56.5765247  -3.06904488  -12.4787112  0.7054085       1
    ## 161  123.5765247  -0.06904488  -12.4787112  6.7054085       1
    ## 217  -55.4234753   2.93095512   -3.4787112 11.7054085       9
    ## 235  108.5765247  -1.06904488   21.5212888  0.7054085       9
    ## 457  -61.4234753  -2.06904488  -10.4787112 -0.2945915       0
    ## 467 -157.4234753   1.93095512   20.5212888  4.7054085       1
    ## 496  -55.4234753   0.93095512   -3.4787112 -2.2945915       9
    ## 499   32.5765247  -0.06904488   19.5212888  2.7054085      16
    ## 510  176.5765247 -11.06904488  -18.4787112 11.7054085     100
    ## 708 -174.4234753  -1.06904488  -25.4787112 14.7054085       9
    ##     mpregwt_cent2    mht_cent2 leverage cooks
    ## 30      2.3143197 4.280947e+00        1   NaN
    ## 34      0.2291644 4.767195e-03        1   NaN
    ## 100  1480.6112127 1.655713e+01        1   NaN
    ## 113    90.6549411 4.280947e+00        1   NaN
    ## 140   155.7182323 9.419036e+00        1   NaN
    ## 161   155.7182323 4.767195e-03        1   NaN
    ## 217    12.1014314 8.590498e+00        1   NaN
    ## 235   463.1658732 1.142857e+00        1   NaN
    ## 457   109.8033876 4.280947e+00        1   NaN
    ## 467   421.1232956 3.728588e+00        1   NaN
    ## 496    12.1014314 8.666774e-01        1   NaN
    ## 499   381.0807179 4.767195e-03        1   NaN
    ## 510   341.4627662 1.225238e+02        1   NaN
    ## 708   649.1647225 1.142857e+00        1   NaN

``` r
hist(cooks, main = "Cook's distances for bwt regression")
```

![](assignment3_files/figure-markdown_github/unnamed-chunk-12-2.png)

``` r
smoke2[smoke2$cooks > .04,]
```

    ##         id date gestation bwt.oz parity mrace mage med mht mpregwt inc
    ## NA      NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## 32    6225 1407       258     85      1     5   41   3  67     137   7
    ## NA.1    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.2    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.3    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.4    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.5    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.6    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.7    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.8    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.9    NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.10   NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.11   NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.12   NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ## NA.13   NA   NA        NA     NA     NA    NA   NA  NA  NA      NA  NA
    ##       smoke date_cent mht_cent mpregwt_cent mage_cent parity2
    ## NA       NA        NA       NA           NA        NA      NA
    ## 32        0 -129.4235 2.930955     8.521289  13.70541       1
    ## NA.1     NA        NA       NA           NA        NA      NA
    ## NA.2     NA        NA       NA           NA        NA      NA
    ## NA.3     NA        NA       NA           NA        NA      NA
    ## NA.4     NA        NA       NA           NA        NA      NA
    ## NA.5     NA        NA       NA           NA        NA      NA
    ## NA.6     NA        NA       NA           NA        NA      NA
    ## NA.7     NA        NA       NA           NA        NA      NA
    ## NA.8     NA        NA       NA           NA        NA      NA
    ## NA.9     NA        NA       NA           NA        NA      NA
    ## NA.10    NA        NA       NA           NA        NA      NA
    ## NA.11    NA        NA       NA           NA        NA      NA
    ## NA.12    NA        NA       NA           NA        NA      NA
    ## NA.13    NA        NA       NA           NA        NA      NA
    ##       mpregwt_cent2 mht_cent2  leverage      cooks
    ## NA               NA        NA        NA         NA
    ## 32         72.61236  8.590498 0.3027659 0.08533599
    ## NA.1             NA        NA        NA         NA
    ## NA.2             NA        NA        NA         NA
    ## NA.3             NA        NA        NA         NA
    ## NA.4             NA        NA        NA         NA
    ## NA.5             NA        NA        NA         NA
    ## NA.6             NA        NA        NA         NA
    ## NA.7             NA        NA        NA         NA
    ## NA.8             NA        NA        NA         NA
    ## NA.9             NA        NA        NA         NA
    ## NA.10            NA        NA        NA         NA
    ## NA.11            NA        NA        NA         NA
    ## NA.12            NA        NA        NA         NA
    ## NA.13            NA        NA        NA         NA

``` r
smoke3 = smoke[smoke$id != 7722, ]
smoke3 = smoke3[smoke$id != 6122, ]
reg5 = lm(bwt.oz ~ as.factor(smoke) + as.factor(mrace) + as.factor(med) + date +
           parity + parity2 + mage_cent + mht_cent + mht_cent2 + mpregwt_cent + mpregwt_cent2 + inc, data = smoke3); summary(reg5)
```

    ## 
    ## Call:
    ## lm(formula = bwt.oz ~ as.factor(smoke) + as.factor(mrace) + as.factor(med) + 
    ##     date + parity + parity2 + mage_cent + mht_cent + mht_cent2 + 
    ##     mpregwt_cent + mpregwt_cent2 + inc, data = smoke3)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -56.271  -9.467  -0.229   9.976  49.498 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       95.2381035 11.0540005   8.616  < 2e-16 ***
    ## as.factor(smoke)1 -9.1824897  1.1715140  -7.838 1.38e-14 ***
    ## as.factor(mrace)1 -2.1762196  2.9714883  -0.732 0.464149    
    ## as.factor(mrace)2 -7.2485460  4.0074083  -1.809 0.070841 .  
    ## as.factor(mrace)3  2.1333379  2.6955209   0.791 0.428912    
    ## as.factor(mrace)4 -0.2255318  2.6518127  -0.085 0.932243    
    ## as.factor(mrace)5 -0.6733773  1.8783667  -0.358 0.720066    
    ## as.factor(mrace)6  3.7556731  3.5234808   1.066 0.286775    
    ## as.factor(mrace)7 -9.3375975  1.6373085  -5.703 1.63e-08 ***
    ## as.factor(mrace)8 -7.0918517  3.1231481  -2.271 0.023415 *  
    ## as.factor(mrace)9 -3.5278871  4.3898830  -0.804 0.421832    
    ## as.factor(med)1    6.4614146  7.8345419   0.825 0.409756    
    ## as.factor(med)2    8.8162773  7.7259943   1.141 0.254145    
    ## as.factor(med)3    8.9142321  8.0326168   1.110 0.267422    
    ## as.factor(med)4    9.4546793  7.7578520   1.219 0.223291    
    ## as.factor(med)5    8.8634729  7.7946108   1.137 0.255809    
    ## as.factor(med)7   -3.4853766 11.2728206  -0.309 0.757258    
    ## date               0.0124625  0.0053619   2.324 0.020348 *  
    ## parity             2.4237384  0.8035652   3.016 0.002636 ** 
    ## parity2           -0.2022186  0.1074329  -1.882 0.060143 .  
    ## mage_cent         -0.1371965  0.1331458  -1.030 0.303108    
    ## mht_cent           0.9115411  0.2787322   3.270 0.001118 ** 
    ## mht_cent2          0.1013487  0.0607083   1.669 0.095403 .  
    ## mpregwt_cent       0.1489533  0.0399282   3.731 0.000204 ***
    ## mpregwt_cent2     -0.0017005  0.0008571  -1.984 0.047571 *  
    ## inc               -0.3046699  0.2734221  -1.114 0.265476    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 16.46 on 841 degrees of freedom
    ##   (1 observation deleted due to missingness)
    ## Multiple R-squared:  0.1828, Adjusted R-squared:  0.1585 
    ## F-statistic: 7.523 on 25 and 841 DF,  p-value: < 2.2e-16

I then fit a model without these I then fit a model without these high cook distance and high leverage point. The results shows that the model did not change. These points only have very tiny influence on the model. Therefore, I would stick to the original model.
