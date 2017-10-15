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

## Using summarize


## Other approaches

