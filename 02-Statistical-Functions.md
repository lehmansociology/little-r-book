# Statistical Functions (for one variable)

Here are some basic statistical functions you should really know by heart. 
Most of them are obvious if you think about them.
You should also know the formula or other calculation procedures for these.

These will be presented using the $ format and some commonly used sample data sets. The na.rm option is included because 
you are always safer using it.

## These are from core R

That means the base and stats packages.


```r
# Mean
mean(chickwts$weight, na.rm = TRUE)
```

```
## [1] 261.3099
```

```r
# Variance (for a sample)
var(chickwts$weight, na.rm = TRUE)
```

```
## [1] 6095.503
```

```r
# Variance (for a population)
# There is no simple function for this.  The code below shows one possible way
# The length() function gives you the total rows and na.omit() ensures that you are not counting NAs, since
# they are not in the calculation of var(). 
var(chickwts$weight, na.rm = TRUE)*(length(na.omit(chickwts$weight)/(length(na.omit(chickwts$weight)) - 1)))
```

```
## [1] 432780.7
```

```r
# Standard deviation (for a sample)
sd(chickwts$weight, na.rm = TRUE)
```

```
## [1] 78.0737
```

```r
# Note there is no simple conversion from sample standard deviation
# to population standard deviation.
# Calculate the population variance and take the square root.

# Median
median(chickwts$weight, na.rm = TRUE)
```

```
## [1] 258
```

```r
# Quantiles (you specify which ones you want)
quantile(chickwts$weight, probs = c(.25, .50, .75), na.rm = TRUE)
```

```
##   25%   50%   75% 
## 204.5 258.0 323.5
```

```r
# Minimum
min(chickwts$weight, na.rm = TRUE)
```

```
## [1] 108
```

```r
# Maximum 
max(chickwts$weight, na.rm = TRUE)
```

```
## [1] 423
```

```r
# Table
# This is normally used for factor variables
table(chickwts$feed, useNA = "ifany")
```

```
## 
##    casein horsebean   linseed  meatmeal   soybean sunflower 
##        12        10        12        11        14        12
```
Also you should know that the summary() function can be used on almost object and will give you results depending on what that 
object is.


```r
summary(chickwts)
```

```
##      weight             feed   
##  Min.   :108.0   casein   :12  
##  1st Qu.:204.5   horsebean:10  
##  Median :258.0   linseed  :12  
##  Mean   :261.3   meatmeal :11  
##  3rd Qu.:323.5   soybean  :14  
##  Max.   :423.0   sunflower:12
```


```r
summary(chickwts$weight)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   108.0   204.5   258.0   261.3   323.5   423.0
```

```r
summary(chickwts$feed)
```

```
##    casein horsebean   linseed  meatmeal   soybean sunflower 
##        12        10        12        11        14        12
```

## These are from lehmansociology

Since that is a package you either need to load it with library() or use the notation we use here.


```r
# Mode
lehmansociology::MODE(chickwts$feed)
```

```
## $dataframe
## [1] "soybean"
```

```r
# Frequency
lehmansociology::frequency(chickwts$feed)
```

```
##  Values    Freq Percent
##  casein    12   16.9   
##  horsebean 10   14.1   
##  linseed   12   16.9   
##  meatmeal  11   15.5   
##  soybean   14   19.7   
##  sunflower 12   16.9   
##  Total     71   100
```


