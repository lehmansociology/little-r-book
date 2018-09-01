---
output:
  html_document: default
  word_document: default
---
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
# The length() function gives you the total rows and na.omit() ensures that you 
# are not counting NAs, since they are not in the calculation of var(). 
var(chickwts$weight, na.rm = TRUE)*  
                         (length(na.omit(chickwts$weight)) - 1)/
                         length(chickwts$weight)
```

```
## [1] 6009.65
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
# Calculate the population variance and take the square root. See the next
# section.

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
# MODE
# Notice that you must use all upper case. This is because there is
# already a function called mode in base r that does something 
# completely unrelated.
lehmansociology::MODE(chickwts$feed)
```

```
## $dataframe
## [1] "soybean"
```

```r
# Variance for a population
# This is similar to the VARP function in most spreadsheets
lehmansociology::varp(chickwts$weight)
```

```
## [1] 6009.65
```

```r
# Standard deviation for a population 
# This is similar to the STDEVP
lehmansociology::sdp(chickwts$weight)
```

```
## [1] 77.52194
```

## These are from the Janitor package

Since it is a package you must load it.
For producing single variable frequencies use tabyl().
It is usually used with the `%>%` or "pipe" operator from the maggritr  package. 


```r
library(janitor)
```

```
## Warning: package 'janitor' was built under R version 3.4.4
```

```r
library(magrittr)
chickwts %>% tabyl(feed)
```

```
## Warning: package 'bindrcpp' was built under R version 3.4.4
```

```
##       feed  n   percent
##     casein 12 0.1690141
##  horsebean 10 0.1408451
##    linseed 12 0.1690141
##   meatmeal 11 0.1549296
##    soybean 14 0.1971831
##  sunflower 12 0.1690141
```

Janitor uses adorn_ functions to add extra details or formatting to tables. 

```r
chickwts %>% tabyl(feed) %>% 
             adorn_pct_formatting()
```

```
##       feed  n percent
##     casein 12   16.9%
##  horsebean 10   14.1%
##    linseed 12   16.9%
##   meatmeal 11   15.5%
##    soybean 14   19.7%
##  sunflower 12   16.9%
```

The lehmansociology package includes extra adorn_ functions for cumulative distributions.


```r
library(lehmansociology)
chickwts %>% tabyl(weight)  %>%
            adorn_cumulative() %>%
            adorn_cumulative_percentages() 
```

```
##  weight  n    percent cum freq    cum pct
##     108  1 0.01408451        1 0.01408451
##     124  1 0.01408451        2 0.02816901
##     136  1 0.01408451        3 0.04225352
##     140  1 0.01408451        4 0.05633803
##     141  1 0.01408451        5 0.07042254
##     143  1 0.01408451        6 0.08450704
##     148  1 0.01408451        7 0.09859155
##     153  1 0.01408451        8 0.11267606
##     158  1 0.01408451        9 0.12676056
##     160  1 0.01408451       10 0.14084507
##     168  1 0.01408451       11 0.15492958
##     169  1 0.01408451       12 0.16901408
##     171  1 0.01408451       13 0.18309859
##     179  1 0.01408451       14 0.19718310
##     181  1 0.01408451       15 0.21126761
##     193  1 0.01408451       16 0.22535211
##     199  1 0.01408451       17 0.23943662
##     203  1 0.01408451       18 0.25352113
##     206  1 0.01408451       19 0.26760563
##     213  1 0.01408451       20 0.28169014
##     216  1 0.01408451       21 0.29577465
##     217  1 0.01408451       22 0.30985915
##     222  1 0.01408451       23 0.32394366
##     226  1 0.01408451       24 0.33802817
##     227  1 0.01408451       25 0.35211268
##     229  1 0.01408451       26 0.36619718
##     230  1 0.01408451       27 0.38028169
##     242  1 0.01408451       28 0.39436620
##     243  1 0.01408451       29 0.40845070
##     244  1 0.01408451       30 0.42253521
##     248  2 0.02816901       32 0.45070423
##     250  1 0.01408451       33 0.46478873
##     257  2 0.02816901       35 0.49295775
##     258  1 0.01408451       36 0.50704225
##     260  2 0.02816901       38 0.53521127
##     263  1 0.01408451       39 0.54929577
##     267  1 0.01408451       40 0.56338028
##     271  2 0.02816901       42 0.59154930
##     283  1 0.01408451       43 0.60563380
##     295  1 0.01408451       44 0.61971831
##     297  1 0.01408451       45 0.63380282
##     303  1 0.01408451       46 0.64788732
##     309  1 0.01408451       47 0.66197183
##     315  1 0.01408451       48 0.67605634
##     316  1 0.01408451       49 0.69014085
##     318  2 0.02816901       51 0.71830986
##     320  1 0.01408451       52 0.73239437
##     322  1 0.01408451       53 0.74647887
##     325  1 0.01408451       54 0.76056338
##     327  1 0.01408451       55 0.77464789
##     329  1 0.01408451       56 0.78873239
##     332  1 0.01408451       57 0.80281690
##     334  1 0.01408451       58 0.81690141
##     339  1 0.01408451       59 0.83098592
##     340  1 0.01408451       60 0.84507042
##     341  1 0.01408451       61 0.85915493
##     344  1 0.01408451       62 0.87323944
##     352  1 0.01408451       63 0.88732394
##     359  1 0.01408451       64 0.90140845
##     368  1 0.01408451       65 0.91549296
##     379  1 0.01408451       66 0.92957746
##     380  1 0.01408451       67 0.94366197
##     390  1 0.01408451       68 0.95774648
##     392  1 0.01408451       69 0.97183099
##     404  1 0.01408451       70 0.98591549
##     423  1 0.01408451       71 1.00000000
##   Total 71 1.00000000       71 1.00000000
```
You can add adorn_cum_pct_formatting to put the proportions into percent format.


```r
chickwts %>% tabyl(weight)  %>%
            adorn_pct_formatting() %>%
            adorn_cumulative() %>%
            adorn_cumulative_percentages() %>%
            adorn_cum_pct_formatting()
```

```
##    weight  n percent cum freq   cum pct
## 1     108  1    1.4%        1 1.408451%
## 2     124  1    1.4%        2      2.8%
## 3     136  1    1.4%        3      4.2%
## 4     140  1    1.4%        4      5.6%
## 5     141  1    1.4%        5      7.0%
## 6     143  1    1.4%        6      8.5%
## 7     148  1    1.4%        7      9.9%
## 8     153  1    1.4%        8     11.3%
## 9     158  1    1.4%        9     12.7%
## 10    160  1    1.4%       10     14.1%
## 11    168  1    1.4%       11     15.5%
## 12    169  1    1.4%       12     16.9%
## 13    171  1    1.4%       13     18.3%
## 14    179  1    1.4%       14     19.7%
## 15    181  1    1.4%       15     21.1%
## 16    193  1    1.4%       16     22.5%
## 17    199  1    1.4%       17     23.9%
## 18    203  1    1.4%       18     25.4%
## 19    206  1    1.4%       19     26.8%
## 20    213  1    1.4%       20     28.2%
## 21    216  1    1.4%       21     29.6%
## 22    217  1    1.4%       22     31.0%
## 23    222  1    1.4%       23     32.4%
## 24    226  1    1.4%       24     33.8%
## 25    227  1    1.4%       25     35.2%
## 26    229  1    1.4%       26     36.6%
## 27    230  1    1.4%       27     38.0%
## 28    242  1    1.4%       28     39.4%
## 29    243  1    1.4%       29     40.8%
## 30    244  1    1.4%       30     42.3%
## 31    248  2    2.8%       32     45.1%
## 32    250  1    1.4%       33     46.5%
## 33    257  2    2.8%       35     49.3%
## 34    258  1    1.4%       36     50.7%
## 35    260  2    2.8%       38     53.5%
## 36    263  1    1.4%       39     54.9%
## 37    267  1    1.4%       40     56.3%
## 38    271  2    2.8%       42     59.2%
## 39    283  1    1.4%       43     60.6%
## 40    295  1    1.4%       44     62.0%
## 41    297  1    1.4%       45     63.4%
## 42    303  1    1.4%       46     64.8%
## 43    309  1    1.4%       47     66.2%
## 44    315  1    1.4%       48     67.6%
## 45    316  1    1.4%       49     69.0%
## 46    318  2    2.8%       51     71.8%
## 47    320  1    1.4%       52     73.2%
## 48    322  1    1.4%       53     74.6%
## 49    325  1    1.4%       54     76.1%
## 50    327  1    1.4%       55     77.5%
## 51    329  1    1.4%       56     78.9%
## 52    332  1    1.4%       57     80.3%
## 53    334  1    1.4%       58     81.7%
## 54    339  1    1.4%       59     83.1%
## 55    340  1    1.4%       60     84.5%
## 56    341  1    1.4%       61     85.9%
## 57    344  1    1.4%       62     87.3%
## 58    352  1    1.4%       63     88.7%
## 59    359  1    1.4%       64     90.1%
## 60    368  1    1.4%       65     91.5%
## 61    379  1    1.4%       66     93.0%
## 62    380  1    1.4%       67     94.4%
## 63    390  1    1.4%       68     95.8%
## 64    392  1    1.4%       69     97.2%
## 65    404  1    1.4%       70     98.6%
## 66    423  1    1.4%       71    100.0%
## 67  Total 71       -       71    100.0%
```

Piping to the `knitr::kable()` function will create a more polished table, In additon if knit to PDF 
`kable()` can add a title using the `caption=` option.


```r
chickwts %>% tabyl(weight)  %>%
            adorn_pct_formatting() %>%
            adorn_cumulative() %>%
            adorn_cumulative_percentages() %>%
            adorn_cum_pct_formatting() %>%
            knitr::kable(caption = "Weights of chicks")
```



Table: (\#tab:unnamed-chunk-10)Weights of chicks

weight     n  percent    cum freq  cum pct   
-------  ---  --------  ---------  ----------
108        1  1.4%              1  1.408451% 
124        1  1.4%              2  2.8%      
136        1  1.4%              3  4.2%      
140        1  1.4%              4  5.6%      
141        1  1.4%              5  7.0%      
143        1  1.4%              6  8.5%      
148        1  1.4%              7  9.9%      
153        1  1.4%              8  11.3%     
158        1  1.4%              9  12.7%     
160        1  1.4%             10  14.1%     
168        1  1.4%             11  15.5%     
169        1  1.4%             12  16.9%     
171        1  1.4%             13  18.3%     
179        1  1.4%             14  19.7%     
181        1  1.4%             15  21.1%     
193        1  1.4%             16  22.5%     
199        1  1.4%             17  23.9%     
203        1  1.4%             18  25.4%     
206        1  1.4%             19  26.8%     
213        1  1.4%             20  28.2%     
216        1  1.4%             21  29.6%     
217        1  1.4%             22  31.0%     
222        1  1.4%             23  32.4%     
226        1  1.4%             24  33.8%     
227        1  1.4%             25  35.2%     
229        1  1.4%             26  36.6%     
230        1  1.4%             27  38.0%     
242        1  1.4%             28  39.4%     
243        1  1.4%             29  40.8%     
244        1  1.4%             30  42.3%     
248        2  2.8%             32  45.1%     
250        1  1.4%             33  46.5%     
257        2  2.8%             35  49.3%     
258        1  1.4%             36  50.7%     
260        2  2.8%             38  53.5%     
263        1  1.4%             39  54.9%     
267        1  1.4%             40  56.3%     
271        2  2.8%             42  59.2%     
283        1  1.4%             43  60.6%     
295        1  1.4%             44  62.0%     
297        1  1.4%             45  63.4%     
303        1  1.4%             46  64.8%     
309        1  1.4%             47  66.2%     
315        1  1.4%             48  67.6%     
316        1  1.4%             49  69.0%     
318        2  2.8%             51  71.8%     
320        1  1.4%             52  73.2%     
322        1  1.4%             53  74.6%     
325        1  1.4%             54  76.1%     
327        1  1.4%             55  77.5%     
329        1  1.4%             56  78.9%     
332        1  1.4%             57  80.3%     
334        1  1.4%             58  81.7%     
339        1  1.4%             59  83.1%     
340        1  1.4%             60  84.5%     
341        1  1.4%             61  85.9%     
344        1  1.4%             62  87.3%     
352        1  1.4%             63  88.7%     
359        1  1.4%             64  90.1%     
368        1  1.4%             65  91.5%     
379        1  1.4%             66  93.0%     
380        1  1.4%             67  94.4%     
390        1  1.4%             68  95.8%     
392        1  1.4%             69  97.2%     
404        1  1.4%             70  98.6%     
423        1  1.4%             71  100.0%    
Total     71  -                71  100.0%    


Janitor is also used to create cross tabs (see Chapter 5).

## From the RMisc package (Confidence intervals)

You can use the `CI()` function from the Rmisc package to obtain confidence intervals.


```r
library(Rmisc)
```

```
## Loading required package: lattice
```

```
## Loading required package: plyr
```

```r
CI(chickwts$weight, ci = 0.95)
```

```
##    upper     mean    lower 
## 279.7896 261.3099 242.8301
```

## From the resample package (bootstrap confidence intervals)

Obtaining bootstrap confidence intervals for a single mean would build on the `bootstrap()` function from the 
resample library.  It takes two steps. First obtaining a large  number of samples from your sample.  You also
have to specify what statistic you want to estimate the confidence interval for. This can be anything
(`mean()`, `median()`, `sd()` or even a function you create).  You can also specify the 
number of replications; with today's computer power there is no reason to use a low number unless you have
a huge (100,000s) sample size.

Save the result in an object and then use the `CI.bca()` function to obtain the level of confidence interval you
want. There are also other CI methods available.




```r
library(resample)
bootstrap_results  <- bootstrap(chickwts, mean(weight, na.rm = TRUE), R = 10000)
CI.bca(bootstrap_results, probs = c(0.025, 0.975))
```

```
##                                2.5%    97.5%
## mean(weight, na.rm = TRUE) 243.0763 279.7887
```




## Conclusion

This chapter presents just a handful of R functions and their many options As you gain experience using
R you should read the help files, vignettes and online resources to learn more.

