What makes for a good historical popularity index?
================
Duke Squirrels
04/19/2018

Your project goes here! Before you submit, make sure your chunks are turned off with `echo = FALSE`.

Load Packages
-------------

Load Data
---------

Introduction
------------

The data that we obtained contains information regarding historical figures. We downloaded the data from Kaggle, but the data was collected by the Massachusetts Institute of Technology about a year ago. The data is based off of metrics from many wikipedia pages and believe the variables in the dataframe can be used to extrapolate what makes a historical figure "popular" by Wikipedia standards. For our write-up, we chose to focus on the variables `full_name`, `birth_year`, `latitude`, `longitude`, `occupation`, `sex`, and `industry`. However, in our linear full model, we will select more than just these variables. By the end of our data analysis, we aim to derive the perfect combination of variables that lead to a high popularity index, which is recorded in the dataframe.

### Section 1- Introduction to the Data

    ## [1] 17

    ## [1] 10279

There are 17 variables and 10,279 observations (with all NAs removed in the new dataframe). Before removing the NAs, the full dataframe had 11,341 observations.

    ## # A tibble: 2 x 2
    ##   sex        n
    ##   <chr>  <int>
    ## 1 Female  1427
    ## 2 Male    8852

Based on the filtered dataframe, there are 1,427 women and 8,852 men that are considered historical figures.

![](project_files/figure-markdown_github/distribution-of-index-1.png)

    ## # A tibble: 1 x 3
    ##    mean median    sd
    ##   <dbl>  <dbl> <dbl>
    ## 1  22.1   22.9  3.37

To get a better understanding of our dataset, we created a histogram that shows the distribution of the historical popularity index scores for the historical figures and ran summary statistics. The median score was 22.8723 and the mean was 22.14023. The distribution is left skewed and unimodal.

##### Reference

<http://www.dummies.com/programming/r/how-to-remove-rows-with-missing-data-in-r/>

### Simple Linear Regression

    ##          term  estimate
    ## 1 (Intercept) 20.802384
    ## 2     sexMale  1.553512

Here we estimated the historical popularity index using the `sex` variable. The slope for the categorical variable `sexMale` is 1.55, suggesting that historical figures who are men have, on average, an increase in their overall popularity index of 1.55 as long as all other variables are held constant.

The linear model, based on the output, is:

`(historical_popularity_index) = 20.8(intercept) + 1.55(sexMale)`

    ## [1] 0.02538845

We found that the r-squared for the linear model `m_pop` is 2.54%, which suggests that 2.54% of the variability of the data can be explained by the linear model.

### Multiple Linear Regression

    ##                                        term    estimate
    ## 1                               (Intercept) 16.13336476
    ## 2                                   sexMale  1.51505537
    ## 3                      domainBusiness & Law  0.32594321
    ## 4                         domainExploration  0.56575963
    ## 5                          domainHumanities  1.49018106
    ## 6                        domainInstitutions  0.92757490
    ## 7                       domainPublic Figure  1.01544834
    ## 8                domainScience & Technology  0.86254971
    ## 9                              domainSports -4.37872010
    ## 10                        article_languages  0.10057213
    ## 11                            continentAsia  1.59712745
    ## 12                          continentEurope  2.22815622
    ## 13                   continentNorth America  1.46826358
    ## 14                         continentOceania  1.13423735
    ## 15                   continentSouth America  2.88294445
    ## 16          article_languages:continentAsia -0.02635754
    ## 17        article_languages:continentEurope -0.02759474
    ## 18 article_languages:continentNorth America -0.03508578
    ## 19       article_languages:continentOceania -0.04278132
    ## 20 article_languages:continentSouth America -0.05213559

Here we estimated the historical popularity index using the `sex`, `domain`, `article_languages`, and `continent` variables. We would interpret the slope the same way we did with the simple linear regression above that had the `sex` variable only.

The linear model, based on the output, is:

`(historical_popularity_index) = 16.13336476    (intercept) + 1.51505537(sexMale) + 0.32594321  (domainBusiness & Law) + 0.56575963  (domainExploration) + 1.49018106    (domainHumanities) + 0.92757490 (domainInstitutions) + 1.01544834(domainPublic Figure) + 0.86254971(domainScience & Technology) +   -4.37872010(domainSports) + 0.10057213  (article_languages) +   1.59712745  (continentAsia) + 2.22815622    (continentEurope) + 1.46826358(continentNorth America   ) +     1.13423735(continentOceania) + 2.88294445   (continentSouth America)`+ -0.02635754(article\_languages:continentAsia) + -0.02759474(article\_languages:continentEurope) + -0.03508578(article\_languages:continentNorth America) + -0.04278132(article\_languages:continentOceania) + -0.05213559(article\_languages:continentSouth America)

    ## [1] 0.582584

### Backwards Selection with AIC

    ## Start:  AIC=16042.73
    ## historical_popularity_index ~ sex + domain + article_languages + 
    ##     continent + continent * article_languages
    ## 
    ##                               Df Sum of Sq   RSS   AIC
    ## <none>                                     48761 16043
    ## - article_languages:continent  5       170 48931 16068
    ## - sex                          1      2448 51210 16544
    ## - domain                       7     35938 84699 21704

    ##                                        term    estimate
    ## 1                               (Intercept) 16.13336476
    ## 2                                   sexMale  1.51505537
    ## 3                      domainBusiness & Law  0.32594321
    ## 4                         domainExploration  0.56575963
    ## 5                          domainHumanities  1.49018106
    ## 6                        domainInstitutions  0.92757490
    ## 7                       domainPublic Figure  1.01544834
    ## 8                domainScience & Technology  0.86254971
    ## 9                              domainSports -4.37872010
    ## 10                        article_languages  0.10057213
    ## 11                            continentAsia  1.59712745
    ## 12                          continentEurope  2.22815622
    ## 13                   continentNorth America  1.46826358
    ## 14                         continentOceania  1.13423735
    ## 15                   continentSouth America  2.88294445
    ## 16          article_languages:continentAsia -0.02635754
    ## 17        article_languages:continentEurope -0.02759474
    ## 18 article_languages:continentNorth America -0.03508578
    ## 19       article_languages:continentOceania -0.04278132
    ## 20 article_languages:continentSouth America -0.05213559

    ## [1] 45215.27

### Visual

![](project_files/figure-markdown_github/unnamed-chunk-1-1.png)

Conclusion
----------

### Question 2

#### Create a map showing the concentration of popular historical figures around the world

![](project_files/figure-markdown_github/Italy-1.png)
