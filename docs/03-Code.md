# Code

This chapter is going to review some basic code items that come up regularly.
You should memorize these.

## Assignment operator

` <- `
This is used to assign the value of whatever is on the right to the object on the left.

`a <- 4`
Means that a is now 4.

`b <- chickwts`
Means that b is now a data frame with all the data from chickwts.

## Combine function

`c()`  

This essential function lets you put a set of values into a vector. 

`a <- c(2, 3, 4, 5)`  
`b <- c("red", "yellow", "blue")`  
`c <- c(TRUE, FALSE, FALSE, TRUE)`  

Now a, b, and c refer to these sets of values.  

## Pipe operator

This is not part of the core of R, but it is widely used. It comes from the `magrittr` package.  

`%>%`

The way it works is that everything on the left becomes an input to what is done on the right.  This is supposed 
to be more like natural writing.  First do this, then do this, then do this.

The code below says: take the chickwts data, group the rows by the feed variable, then get the mean weight for each of
the feed types.


```r
 library(magrittr)
chickwts %>% dplyr::group_by(feed) %>% dplyr::summarize( mean=mean(weight)) 
```

```
## # A tibble: 6 x 2
##   feed       mean
##   <fct>     <dbl>
## 1 casein     324.
## 2 horsebean  160.
## 3 linseed    219.
## 4 meatmeal   277.
## 5 soybean    246.
## 6 sunflower  329.
```
Not all functions work with piped data.  


## Basic math operations

| Name  | Operator | Example |Result  |
|---|----|---|---|  
|Addition |`+`|`3 + 4 `| 7|  
|Subtraction|`-`|`4-3`| 1|
|Multiplication|`*`|`3*4`| 12|
|Division|`/`|`3/4`| 0.75|
|Raise to power| `^`| `3^4`|81|

## Comparison operators

| Name  | Operator | Example |Result  |
|---|----|---|---|  
| Equal to | `==`| `(2+3) == (3+3)`| FALSE|
| Not equal to | `!=`|`(2+3) == (3+3)`| FALSE|
| Greater than |`>`| `5 >2` | TRUE|
|Less than |`<`| `5 < 2` | FALSE|
|Greater than or equal to |`>=`| `2 >= 2` |TRUE|
|Less than or equal to |`<=`| `2 <= 3` |TRUE|

## AND and OR (logical operators)

As you start to do more complex things with recoding variables you
will often want to use two or more statements in combination.  For example
you may want to identify everyone 18 or over but who are also 65 or under. 

For these we use the logical operators.  The first set of examples are very simple.

|Name |Operator | Meaning | Example |Result|
|------|---------|------------------------|-------------------------|------|
|OR | `|`  | At least one statement is true | `7 == 6+1 | 7 == 8-1` |TRUE |
|OR | `|`  | At least one statement is true | `7 == 6+1 | 7 == 8+1` |TRUE |
|Exclusive OR | `xor(x,y)`  | Exactly one statement is true | `xor(7 == 6+1, 7 == 8-1)` |FALSE |
|Exclusive OR | `xor(x,y)`  | Exactly one statement is true | `xor(7 == 6+1, 7 == 8+1)` |TRUE |
|AND | `&`  | All statements are true | `7 == 6+1 & 7 == 8-1` |TRUE |
|AND | `&`  | All statements are true | `7 == 6+1 & 7 == 8+1` |FALSE |

If you know any other computer languages be aware that `|` and `&` and `||` and `&&`  work differently in R than you might expect.

