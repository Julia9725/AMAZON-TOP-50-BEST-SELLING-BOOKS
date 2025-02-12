# AMAZON-TOP-50-BEST-SELLING-BOOKS

# INTRODUCTION
   Amazon is a e-commerce website were millions of different types of items are sold. Interestingly, Books was the first product sold on amazon by Jeff Bezos before he became the world’s richest person. Here, we will take a look at top 50 best selling books of amazon to derive some useful insights from them.
# BUSINESS PROBLEM
As a data analyst, Amazon marketing team and senior managers want me to run a descriptive analysis to find out some useful insights which can help them in effectively managing Books inventory so that they never run out of stock for most in demand books and I am also expected to find out if price has anything to do with a book being bestseller multiple times.

# ASSUMPTIONS

The information is still current and can be used to derive insights, which Amazon’s business team can further use to make strategic plans.
The company isn’t currently using any of the suggested solutions in the report.

# Work description
I will be analysing the data base Amazon Top 50 Bestselling Books, between 2019 and 2022, using R programming.

At the end I hop to answer the following questions:
* Which Genre is preferred more by customers?
* In non-fiction and fiction genre which author’s book has been bestseller multiple times?
* Which are the most in demand books that have been bestseller multiple times in different years?
* Are there any books from this 50 top selling books which have less than 4 ratings?
* Does price have any impact on the number of times a book has been bestseller?
* How is the ratings of this books by genre?

# PROCESS

1. Installing and loading common packages and libraries
 ```r
# This R environment comes with many helpful analytics packages installed

library(tidyverse)
library(ggplot2)
```
2. Data Importation
```r
bestsellers <- read.csv("'/kaggle/input/amazon-top-50-bestselling-books-2009-2019/bestsellers_with_categories_2022_03_27.csv')
```


#How many rows are in data frame?
```r
ncol(bestbook)
7
```

#List of column names
```r
colnames(bestsellers)
'Name''Author''User Rating''Reviews''Price''Year''Genre'
 ```
#How many rows are in data frame?
```r
nrow(bestsellers)
550
```
#See the first 6 rows of data frame.
```r
head(bestsellers)
# A tibble: 6 × 7
  Name               Author `User Rating` Reviews Price  Year Genre
  <chr>              <chr>          <dbl>   <dbl> <dbl> <dbl> <chr>
1 10-Day Green Smoo… JJ Sm…           4.7   17350     8  2016 Non fiction
2 11/22/63: A Novel  Steph…           4.6    2052    22  2011 Fiction
3 12 Rules for Life… Jorda…           4.7   18979    15  2018 Non fictio
4 1984 (Signet Clas… Georg…           4.7   21424     6  2017 Fiction
5 5,000 Awesome Fac… Natio…           4.8    7665    12  2019 Non fiction
6 A Dance with Drag… Georg…           4.4   12643    11  2011 Fiction

```

#See list of columns and data types (numeric, character, etc)
```r
str(bestsellers)
spc_tbl_ [550 × 7] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
 $ Name       : chr [1:550] "10-Day Green Smoothie Cleanse" "11/22/63: A Novel" "12 Rules for Life: An Antidote to Chaos" "1984 (Signet Classics)" ...
 $ Author     : chr [1:550] "JJ Smith" "Stephen King" "Jordan B. Peterson" "George Orwell" ...
 $ User Rating: num [1:550] 4.7 4.6 4.7 4.7 4.8 4.4 4.7 4.7 4.7 4.6 ...
 $ Reviews    : num [1:550] 17350 2052 18979 21424 7665 ...
 $ Price      : num [1:550] 8 22 15 6 12 11 30 15 3 8 ...
 $ Year       : num [1:550] 2016 2011 2018 2017 2019 ...
 $ Genre      : chr [1:550] "Non Fiction" "Fiction" "Non Fiction" "Fiction" ...
 - attr(*, "spec")=
  .. cols(
  ..   Name = col_character(),
  ..   Author = col_character(),
  ..   `User Rating` = col_double(),
  ..   Reviews = col_double(),
  ..   Price = col_double(),
  ..   Year = col_double(),
  ..   Genre = col_character()
  .. )
 - attr(*, "problems")=<externalptr>
```
# cleaning data

#Checking for duplicated data
```
sum(duplicated(bestsellers))
[1] 0

```
#Checking for missing data
```
sum(is.na(bestsellers))
0
```
#Checking if there are any nulls within the data.
```
anyNA(bestsellers)
FALSE
```



