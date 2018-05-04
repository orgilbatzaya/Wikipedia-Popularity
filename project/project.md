Wikipedia Popularity
================
Duke Squirrels
04/19/2018

Load Packages
-------------

Load Data
---------

Introduction
------------

The data that we obtained contains information regarding historical figures. We downloaded the data from Kaggle, but the data was collected by the Massachusetts Institute of Technology about a year ago. The data is based off of metrics from many wikipedia pages and believe the variables in the dataframe can be used to extrapolate what makes a historical figure "popular" by Wikipedia standards.
By the end of our data analysis, we aim to derive the perfect combination of variables that lead to a high popularity index, which is recorded in the dataframe.

It is important to note that the dataframe has been updated as recently as last year and the last historical figure's birth year recorded was 2005, suggesting that though the dataframe has not added a historical figure born after the year 2005, there is still currently data being collected on the ones already in the dataframe (ie page views, article languages, etc.).

### Section 1- Introduction to the Data

    ## [1] 17

    ## [1] 10279

    ## # A tibble: 10 x 4
    ##     rank full_name           birth_year historical_popularity_index
    ##    <int> <chr>                    <int>                       <dbl>
    ##  1     1 Aristotle                 -384                        32.0
    ##  2     2 Plato                     -427                        32.0
    ##  3     3 Jesus Christ                -4                        31.9
    ##  4     4 Socrates                  -469                        31.7
    ##  5     5 Alexander the Great       -356                        31.6
    ##  6     6 Leonardo da Vinci         1452                        31.5
    ##  7     7 Julius Caesar             -100                        31.1
    ##  8     8 Homer                     -800                        31.1
    ##  9     9 Pythagoras                -570                        31.1
    ## 10    10 Archimedes                -287                        31.0

There are 17 variables and 10,279 observations (with all NAs removed in the new dataframe). Before removing the NAs, the full dataframe had 11,341 observations.

In addition, we decided to rank the historical figures to based off of their `historical_popularity_index`

### Section 2 - How the Variable `Domain` Affects `Historical_Popularity_Index`

    ## # A tibble: 8 x 2
    ##   domain                   n
    ##   <chr>                <int>
    ## 1 Arts                  2767
    ## 2 Institutions          2753
    ## 3 Sports                1707
    ## 4 Science & Technology  1315
    ## 5 Humanities            1227
    ## 6 Public Figure          319
    ## 7 Business & Law         103
    ## 8 Exploration             88

    ## # A tibble: 6 x 2
    ##   continent         n
    ##   <chr>         <int>
    ## 1 Europe         6073
    ## 2 North America  2351
    ## 3 Asia           1021
    ## 4 Africa          362
    ## 5 South America   352
    ## 6 Oceania         120

Looking at simply the number of historical figures in each of the domain categories, it becomes easier to see which domain has the most number of historical figures. When looking at the number of historical figures by continent, Europe is the continent with the most historical figures across the ~5000 year timespan of the data with more historical figures than all other continents combined.

![](project_files/figure-markdown_github/distribution-of-index-1.png)

    ## # A tibble: 8 x 4
    ##   domain                mean median    sd
    ##   <chr>                <dbl>  <dbl> <dbl>
    ## 1 Arts                  21.8   22.4  3.06
    ## 2 Business & Law        22.3   22.6  2.36
    ## 3 Exploration           23.5   23.4  2.85
    ## 4 Humanities            24.3   24.3  2.21
    ## 5 Institutions          23.6   23.8  2.37
    ## 6 Public Figure         22.4   22.8  3.03
    ## 7 Science & Technology  23.4   23.2  1.83
    ## 8 Sports                17.7   17.3  2.86

To get a better understanding of our dataset, we created a faceted histogram that shows the distribution of the historical popularity index scores for the historical figures across all of the domains in the dataset and ran summary statistics on the dataframe as a whole. The visual lets us see the true distribution of historical figures across all of the domains, letting us know which areas are the most popular and have produced the most historical figures.

We think this visual is important because it gives us a glimpse of how historical popularity index varies across the domains. We will comtinue looking at other variables to see if they contribute into the historical popularity index score.

### Section 3 - How the Variable `Sex` Affects `Historical_Popularity_Index`

    ## # A tibble: 2 x 3
    ##   sex        n  prop
    ##   <chr>  <int> <dbl>
    ## 1 Female  1427 0.139
    ## 2 Male    8852 0.861

Based on the filtered dataframe, there are 1,427 women and 8,852 men that are considered historical figures of the total 10,279 historical figures. There are about 6.2 times as many historical men than women overall in the data. The timeframe of this data starts at -3500, or 3500 BCE, and ends at 2005, spanning about 5000 years. This means that a mere 13.9% of women in the entire timeframe are considered historical figures.

### Simple Linear Regression - For All Figures

    ##          term  estimate
    ## 1 (Intercept) 20.802384
    ## 2     sexMale  1.553512

Here we estimated the historical popularity index using the `sex` variable using a simple linear regression. The slope for the categorical variable `sexMale` is 1.55, suggesting that historical figures who are men have, on average, an increase in their overall popularity index of 1.55 as long as all other variables are held constant.

The linear model, based on the output, is:

`(historical_popularity_index) = 20.8(intercept) + 1.55(sexMale)`

    ## [1] 0.02538845

We found that the r-squared for the linear model `m_pop` is 2.54%, which suggests that 2.54% of the variability of the data can be explained by the linear model and that the model does not fit our data very well. In the next few steps, we will continue to re-evaluate our model to determine what combination of variables result in a high or low popularity index score.

### Simple Linear Regression - For All Figures Born After 1920

    ## # A tibble: 2 x 3
    ##   sex        n  prop
    ##   <chr>  <int> <dbl>
    ## 1 Female  1053 0.196
    ## 2 Male    4309 0.804

For historical figures born after 1920, there are about 4 times as many male historical figures than female figures. This is intriguing because in this 85 year timeframe from 1920 - 2005, we have 1053 historical women out of a total of 1427 women in the entire timeframe.

    ##          term   estimate
    ## 1 (Intercept) 19.6057504
    ## 2     sexMale  0.5687071

In the previous model, we predicted the `historical_popularity_index` by `sex` across the entire ~5000 year time period of the data. The result was that historical figures who were men had, on average and with all other variables held constant, a popularity index score that was 1.55 points higher than that of women who were historical figures. However, in this model, we thought it would be interesting to analyze the 85 year timeframe after the year 1920, when women were given the right to vote in the U.S. and when, later in the century, women across the world where also granted greater rights. As a result, women made up about 20% of the historical figures as opposed to making up 13.9% of the historical figure population in the previous analysis.

The resulting linear model that only looked at the historical figures after 1920 is as follows:

`(historical_popularity_index) = 19.6(intercept) + 0.569(sexMale)`

The slope of the `sexMale` variable decreased significantly from the previous analysis. This shows that time is a factor that affects the historical popularity index of women specifically.

### Section 4 - How the Variable `Article_Languages` Affects `Historical_Popularity_Index`

![](project_files/figure-markdown_github/visualizing-index-by-popularity-1.png)

    ## # A tibble: 1 x 4
    ##   full_name    historical_popularity_index article_languages country
    ##   <chr>                              <dbl>             <int> <chr>  
    ## 1 Jesus Christ                        31.9               214 Israel

Because there are so many historical figures from Europe, there is a lot of clustering near the 50-60 language marker. Additionally, Europe and Asia's slopes are very similar. This could be because Europe has 6,073 figures with pages translated into 50 or more languages and very high popularity index scores or that Asia has 1,021 popular historical figures, but those figures have pages that have been translated into much more than 50 languages. For example, there is a historical figure that is an outlier considering Asia's spread in the visual. By filtering the data for the figure with a page translated into more than 200 languages, we identified this individual as Jesus Christ, whose Wikipedia page has been translated into 214 different languages.

    ## # A tibble: 1 x 4
    ##   full_name   historical_popularity_index article_languages country      
    ##   <chr>                             <dbl>             <int> <chr>        
    ## 1 Corbin Bleu                        18.9               193 United States

Interestingly, one of the historical figures has a low popularity index score, an outlier, but his/her wikipedia page has been translated into almost 200 different languages. After filtering the data to locate the point that had a popularity index score less than 20 and an article that was translated into more than 175 languages, we derived that the outlier historical figure from North America is Corbin Bleu, the actor from High School Musical.

After looking at how the variables `domain`, `sex`, and `article_languages` each affect historical popularity index, we see that they do play a role. To summarize our results and check to see if other variables affect the historical popularity index all at once, we will use a multiple linear regression full model.

### Multiple Linear Regression

    ##                                        term     estimate
    ## 1                               (Intercept) 19.904940468
    ## 2                                   sexMale  1.430356106
    ## 3                      domainBusiness & Law  0.334560092
    ## 4                         domainExploration  0.275254286
    ## 5                          domainHumanities  1.097207712
    ## 6                        domainInstitutions  0.397500049
    ## 7                       domainPublic Figure  0.763276129
    ## 8                domainScience & Technology  0.778088066
    ## 9                              domainSports -4.201724123
    ## 10                        article_languages  0.089262210
    ## 11                            continentAsia  1.234794023
    ## 12                          continentEurope  2.062914933
    ## 13                   continentNorth America  1.321529547
    ## 14                         continentOceania  0.979711141
    ## 15                   continentSouth America  2.677561833
    ## 16                               birth_year -0.001813092
    ## 17          article_languages:continentAsia -0.023467037
    ## 18        article_languages:continentEurope -0.020964963
    ## 19 article_languages:continentNorth America -0.022734323
    ## 20       article_languages:continentOceania -0.030285172
    ## 21 article_languages:continentSouth America -0.038432329

Here we estimated the historical popularity index using the `sex`, `domain`, `birth_year`, `article_languages`, and `continent` variables. We also included the interaction between continent and article languages. We would interpret the slope the same way we did with the simple linear regression above that had the `sex` variable only.

The linear model, based on the output, is:

`(historical_popularity_index) = 19.9(intercept) + 1.43(sexMale) + 0.335(domainBusiness & Law) + 0.275  (domainExploration) + 1.097(domainHumanities) + 0.398(domainInstitutions) + 0.763(domainPublic Figure) + 0.778(domainScience & Technology) - 4.20(domainSports) + 0.0893(article_languages) + 1.235 (continentAsia) + 2.063(continentEurope) + 1.322(continentNorth America ) + 0.980(continentOceania) + 2.68(continentSouth America) - 0.0235(article_languages:continentAsia) - 0.0209(article_languages:continentEurope) - 0.0227(article_languages:continentNorth America) - 0.0303(article_languages:continentOceania) - 0.0384(article_languages:continentSouth America) - 0.001813092(birth_year)`

    ## [1] 0.6347138

### Backwards Selection with AIC

    ## Start:  AIC=14673.49
    ## historical_popularity_index ~ sex + domain + article_languages + 
    ##     continent + birth_year + continent * article_languages
    ## 
    ##                               Df Sum of Sq   RSS   AIC
    ## <none>                                     42672 14674
    ## - article_languages:continent  5      76.8 42749 14682
    ## - sex                          1    2179.4 44851 15184
    ## - birth_year                   1    6089.7 48761 16043
    ## - domain                       7   28066.2 70738 19855

    ##                                        term     estimate
    ## 1                               (Intercept) 19.904940468
    ## 2                                   sexMale  1.430356106
    ## 3                      domainBusiness & Law  0.334560092
    ## 4                         domainExploration  0.275254286
    ## 5                          domainHumanities  1.097207712
    ## 6                        domainInstitutions  0.397500049
    ## 7                       domainPublic Figure  0.763276129
    ## 8                domainScience & Technology  0.778088066
    ## 9                              domainSports -4.201724123
    ## 10                        article_languages  0.089262210
    ## 11                            continentAsia  1.234794023
    ## 12                          continentEurope  2.062914933
    ## 13                   continentNorth America  1.321529547
    ## 14                         continentOceania  0.979711141
    ## 15                   continentSouth America  2.677561833
    ## 16                               birth_year -0.001813092
    ## 17          article_languages:continentAsia -0.023467037
    ## 18        article_languages:continentEurope -0.020964963
    ## 19 article_languages:continentNorth America -0.022734323
    ## 20       article_languages:continentOceania -0.030285172
    ## 21 article_languages:continentSouth America -0.038432329

    ## [1] 43846.03

### The perfect historical popularity index

Based on the full and selected models, to have the highest popularity index score, one should: be a man, study in the domain of the humanities, and live somewhere in the continent of South America.

### Distance

    ## # A tibble: 90,000 x 3
    ##    distance name.arts               name.sci                     
    ##       <dbl> <chr>                   <chr>                        
    ##  1       0. Wolfgang Amadeus Mozart Christian Doppler            
    ##  2       0. Johann Sebastian Bach   Ernst Karl Abbe              
    ##  3       0. Richard Wagner          Gottfried Wilhelm von Leibniz
    ##  4       0. Claude Monet            Antoine Lavoisier            
    ##  5       0. Claude Monet            Rudolf Diesel                
    ##  6       0. Claude Monet            Pierre Curie                 
    ##  7       0. Claude Monet            Antoine Henri Becquerel      
    ##  8       0. Claude Monet            Jacques Lacan                
    ##  9       0. Claude Monet            Vilfredo Pareto              
    ## 10       0. Claude Monet            Augustin Louis Cauchy        
    ## # ... with 89,990 more rows

    ## # A tibble: 739 x 3
    ## # Groups:   name.arts [300]
    ##    name.arts               closest name.sci                     
    ##    <chr>                     <dbl> <chr>                        
    ##  1 Wolfgang Amadeus Mozart     0.  Christian Doppler            
    ##  2 Michelangelo               15.3 Luca Pacioli                 
    ##  3 Johann Sebastian Bach       0.  Ernst Karl Abbe              
    ##  4 Ludwig van Beethoven       23.2 Hermann Emil Fischer         
    ##  5 Vincent van Gogh           46.0 Gerardus Mercator            
    ##  6 Pablo Picasso             114.  Pomponius Mela               
    ##  7 Raphael                    42.3 Luca Pacioli                 
    ##  8 Albrecht Dürer             15.6 Georg Ohm                    
    ##  9 Salvador Dalí              60.4 François Arago               
    ## 10 Richard Wagner              0.  Gottfried Wilhelm von Leibniz
    ## # ... with 729 more rows

    ## # A tibble: 90,000 x 3
    ##    distance name.arts             name.hum       
    ##       <dbl> <chr>                 <chr>          
    ##  1       0. Praxiteles            Plato          
    ##  2       0. Praxiteles            Socrates       
    ##  3       0. Sandro Botticelli     Dante Alighieri
    ##  4       0. Giotto di Bondone     Dante Alighieri
    ##  5       0. Donatello             Dante Alighieri
    ##  6       0. Filippo Brunelleschi  Dante Alighieri
    ##  7       0. Jean-Baptiste Lully   Dante Alighieri
    ##  8       0. Cimabue               Dante Alighieri
    ##  9       0. Andrea del Verrocchio Dante Alighieri
    ## 10       0. Paolo Uccello         Dante Alighieri
    ## # ... with 89,990 more rows

    ## # A tibble: 932 x 3
    ## # Groups:   name.arts [300]
    ##    name.arts            closest name.hum           
    ##    <chr>                  <dbl> <chr>              
    ##  1 Praxiteles               0.  Plato              
    ##  2 Praxiteles               0.  Socrates           
    ##  3 Thespis                 61.5 Pythagoras         
    ##  4 Ozzy Osbourne           36.4 William Shakespeare
    ##  5 Edward Elgar            38.4 William Shakespeare
    ##  6 Sandro Botticelli        0.  Dante Alighieri    
    ##  7 Giotto di Bondone        0.  Dante Alighieri    
    ##  8 Donatello                0.  Dante Alighieri    
    ##  9 Filippo Brunelleschi     0.  Dante Alighieri    
    ## 10 Fra Angelico            24.1 Dante Alighieri    
    ## # ... with 922 more rows

Conclusion
----------
