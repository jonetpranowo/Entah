PERCOBAAN
================
Lilik Pranowo
March 22, 2017

I have checked your code and I when compare with the alternative code that I made using "dplyr" package the results are the same.

Here is the alternative code using "dplyr" package:

Read the data
=============

``` r
dat <- read.csv("ArrestMini.csv")
```

Create new variables: "DATE" and "TIME" from variables "ARRESTTIME"
===================================================================

``` r
dat1 <- dat %>% 
  separate(ARRESTTIME, c('DATE', 'TIME'), sep = 'T')
```

Aggregate council districts that is affected by crime on the day --&gt; I save it as "Arrest\_Daily"
====================================================================================================

``` r
Arrest_Daily <- dat1 %>%
  mutate(Date = as.Date(DATE, "%m/%d/%Y")) %>%
  group_by(DATE) %>%
  summarize(CASES = n(), NUM_COUNCIL = n_distinct(COUNCIL_DISTRICT)) %>%
  arrange(DATE) 
```

View Arrest\_Daily
==================

``` r
Arrest_Daily
```

    ## # A tibble: 212 × 3
    ##          DATE CASES NUM_COUNCIL
    ##         <chr> <int>       <int>
    ## 1  2014-11-16     3           1
    ## 2  2015-05-29     1           1
    ## 3  2015-11-04     2           1
    ## 4  2016-02-12     1           1
    ## 5  2016-02-17     1           1
    ## 6  2016-03-03     1           1
    ## 7  2016-04-04     1           1
    ## 8  2016-04-08     1           1
    ## 9  2016-04-10     1           1
    ## 10 2016-04-12     2           1
    ## # ... with 202 more rows

Plot
