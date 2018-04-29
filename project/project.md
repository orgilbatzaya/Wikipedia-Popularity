PROJECT TITLE
================
Duke Squirrels
04/19/2018

Your project goes here! Before you submit, make sure your chunks are turned off with `echo = FALSE`.

Introduction
------------

The data that we obtained contains information regarding historical figures. We downloaded the data from Kaggle, but the data was collected by the Massachusetts Institute of Technology about a year ago. The data is based off of metrics from many wikipedia pages and believe the variables in the dataframe can be used to extrapolate what makes a historical figure "popular" by Wikipedia standards. For our write-up, we chose to focus on the variables `full_name`, `birth_year`, `latitude`, `longitude`, `occupation`, `sex`, and `industry`. By the end of our data analysis, we aim to derive the perfect combination of variables that lead to a high popularity index, which is recorded in the dataframe.

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

##### Reference

<http://www.dummies.com/programming/r/how-to-remove-rows-with-missing-data-in-r/>

### Section 3 - Linear Modeling

#### Create a linear model to estimate historical popularity index by sex, article languages, & domain

### Question 7

    ##                          term    estimate
    ## 1                 (Intercept) 17.76900799
    ## 2                     sexMale  1.64681208
    ## 3        domainBusiness & Law  0.29532744
    ## 4           domainExploration  0.81049401
    ## 5            domainHumanities  1.75170260
    ## 6          domainInstitutions  1.15094275
    ## 7         domainPublic Figure  1.10625828
    ## 8  domainScience & Technology  1.02891915
    ## 9                domainSports -4.14464358
    ## 10          article_languages  0.07184644

The linear model, based on the output, is:

`(historical_popularity_index) = 17.769(intercept) + 1.647(sexMale) + 0.295(domainBusiness & Law) + 0.810(domainExploration) + 1.752(domainHumanities) + 1.151(domaintInstitutions) + 1.106(domainPublic Figure) + 1.029(domainScience & Technology) - 4.1446(domainSports) + 0.072(article_languages)`

### Question 9

Conclusion
----------

### Question 2

#### Create a map showing the concentration of popular historical figures around the world

![](project_files/figure-markdown_github/Italy-1.png)
