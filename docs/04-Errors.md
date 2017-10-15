# Errors

This chapter is going to describe some commone error messages and how to solve them.


## Could not find function

Common causes
```r
# Use upper case when you should use lower case or lower case 
# when you should use upper case
Mean(chickwts$weight)
```
Error in Mean(chickwts$weight) : could not find function "Mean"

```r
# Wrong spelling
men(chickwts$weight)
```
Error in men(chickwts$weight) : could not find function "men"

Correct code for all of the above

```r
mean(chickwts$weight)
```

```
## [1] 261.3099
```

```r
# Need to load library (MODE() is from lehmansociology)
MODE(chickwts$feed)
```
Error in MODE(chickwts$feed) : could not find function "MODE"  

Correct code

```r
lehmansociology::MODE(chickwts$feed)
```

```
## $dataframe
## [1] "soybean"
```


## Problems with variables

*Error message:  *
argument is not numeric or logical: returning NA[1] NA  

All of the examples below give the same message.

```r
# Misspelled variable name
mean(chickwts$wieght)
```

```r
# Left out the variable name (only gave name of the data frame)
mean(chickwts)
```

```r
# Tried to calculate a mean on a factor (nominal or categorical variable)
mean(chickwts$feed)
```

## Problems with markdown

*Error Message:  *  

Error: unexpected symbol in "Started writing"
```r
Started writing inside the tick marks

```
Text goes outside the tick marks, code goes inside the tick marks.  
If you want text inside the tick marks in order to comment your code, start the line with a #.

Correct code

```r
# Started writing inside the tick marks

```
*Error:*  
Error in parse(text = x, srcfile = src) :  
  attempt to use zero-length variable name  
Calls: local ... evaluate -> parse_all -> parse_all.character -> parse  

This means you have something wrong with your tick marks around the code chunk. 
(In the example below the tick marks are in quotation marks so they will show.  Do not use quotation marks in your
markdown in this way. )
```
 '```{r}'
  # Differet number of tick marks
  mean(chickwts$weight)
  '``'
``
```

*Error: *  
Nothing happens. Code does not run.  

Code is outside of tick marks

mean(chickwts$weight)

  


## Other problems when knittng

*Error: Package inputenc Error: Unicode char  *  

This usually means you have a non-standard character in your text. It happens because you copy and pasted into
the file from another document and something went wrong with the paste.
The error message will tell you the character that is causing the problem. You should search your document for that
character.   




