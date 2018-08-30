# Statistics for Multiple Variables

Most of the time we want to look at the relationship between two or more variables.

R has several different ways of working with multiple variables. 

## Using formula notation

In R a "forumula" is created using the `~`  operator, which is found on the top left of the keyboard. 

In these examples the formula operator always works like this:
`dependent_variable ~ independent_variable` 
and if you have multiple independent_variables use a `+` to add them on the right.

*Crosstab using lehmansociology*

```r
lehmansociology::crosstab(tension ~ wool, data = warpbreaks)
```

```
## tension ~ wool
##         A  B 
## L       9  9 
## M       9  9 
## H       9  9 
## Total N 27 27
```

*Ordinary Linear Model*  
(This means it has an interval dependent variable.)


```r
lm(raises ~ critical, data = attitude)
```

```
## 
## Call:
## lm(formula = raises ~ critical, data = attitude)
## 
## Coefficients:
## (Intercept)     critical  
##      35.025        0.396
```

*Generalized Linear Model*
(In this case a logistic regression.)  
(in this code a dichtomous dependent variable is created using the cut() functions.)  


```r
USJudgeRatings$RTEN_d <- cut(USJudgeRatings$RTEN, median(USJudgeRatings$RTEN))

glm(RTEN_d ~ INTG, data = USJudgeRatings, family = binomial())
```

```
## 
## Call:  glm(formula = RTEN_d ~ INTG, family = binomial(), data = USJudgeRatings)
## 
## Coefficients:
## (Intercept)         INTG  
##     -29.387        4.325  
## 
## Degrees of Freedom: 42 Total (i.e. Null);  41 Residual
## Null Deviance:	    26.62 
## Residual Deviance: 8.603 	AIC: 12.6
```

*Parametric t test*

```r
t.test(extra ~ group, data = sleep)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  extra by group
## t = -1.8608, df = 17.776, p-value = 0.07939
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -3.3654832  0.2054832
## sample estimates:
## mean in group 1 mean in group 2 
##            0.75            2.33
```



## Using group_by 

Another way to look at the relationship between variables is to compare values of statistics for different groups.  In this case
one way to do this is with the group_by function from the `dplyr` package. 

Once you group your data there are a number of other functions within dplyr and in other packages that will use the groups
ro organiza the results


```r
library(magrittr)
iris %>% dplyr::group_by(Species)  %>%
         dplyr::summarize(mean_sepal_length = mean(Sepal.Length),
                          median_sepal_legth = median(Sepal.Length),
                          Upper_CI = mean(Sepal.Length) + 1.96*sd(Sepal.Length),
                          Lower_CI = mean(Sepal.Length) - 1.96*sd(Sepal.Length)
                          )
```

```
## Warning: package 'bindrcpp' was built under R version 3.4.4
```

```
## # A tibble: 3 x 5
##   Species    mean_sepal_length median_sepal_legth Upper_CI Lower_CI
##   <fct>                  <dbl>              <dbl>    <dbl>    <dbl>
## 1 setosa                  5.01               5.00     5.70     4.32
## 2 versicolor              5.94               5.90     6.95     4.92
## 3 virginica               6.59               6.50     7.83     5.34
```


```r
iris %>% dplyr::group_by(Species)  %>% skimr::skim()
```


**Skim summary statistics**

<table style='width: auto;' class='table table-condensed'>
 <thead>
  <tr>
   <th style="text-align:right;"> n_obs </th>
   <th style="text-align:right;"> n_cols </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 150 </td>
   <td style="text-align:right;"> 5 </td>
  </tr>
</tbody>
</table>




**Variable type: numeric**

variable       Species       missing   complete    n   mean     sd    p0    p25    p50    p75   p100  hist  
-------------  -----------  --------  ---------  ---  -----  -----  ----  -----  -----  -----  -----  ------
Sepal.Length   setosa              0         50   50   5.01   0.35   4.3   4.80   5.00   5.20    5.8  ▃▃▇▅▁ 
Sepal.Length   versicolor          0         50   50   5.94   0.52   4.9   5.60   5.90   6.30    7.0  ▂▇▆▃▃ 
Sepal.Length   virginica           0         50   50   6.59   0.64   4.9   6.23   6.50   6.90    7.9  ▁▃▇▃▂ 
Sepal.Width    setosa              0         50   50   3.43   0.38   2.3   3.20   3.40   3.68    4.4  ▁▃▇▅▂ 
Sepal.Width    versicolor          0         50   50   2.77   0.31   2.0   2.52   2.80   3.00    3.4  ▁▅▆▇▂ 
Sepal.Width    virginica           0         50   50   2.97   0.32   2.2   2.80   3.00   3.18    3.8  ▂▆▇▅▁ 
Petal.Length   setosa              0         50   50   1.46   0.17   1.0   1.40   1.50   1.58    1.9  ▁▃▇▃▁ 
Petal.Length   versicolor          0         50   50   4.26   0.47   3.0   4.00   4.35   4.60    5.1  ▂▂▇▇▆ 
Petal.Length   virginica           0         50   50   5.55   0.55   4.5   5.10   5.55   5.88    6.9  ▃▇▇▃▂ 
Petal.Width    setosa              0         50   50   0.25   0.11   0.1   0.20   0.20   0.30    0.6  ▇▂▂▁▁ 
Petal.Width    versicolor          0         50   50   1.33   0.20   1.0   1.20   1.30   1.50    1.8  ▅▇▃▆▁ 
Petal.Width    virginica           0         50   50   2.03   0.27   1.4   1.80   2.00   2.30    2.5  ▂▇▆▅▇ 



