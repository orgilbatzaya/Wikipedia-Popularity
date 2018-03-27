PROJECT TITLE
================
Duke Squirrels
03/22/18

Section 1. Introduction
-----------------------

### Question

What makes a person on Wikipedia popular?

### Data

The data that we obtained contains information regarding famous figures throughout history. The data came from <https://www.kaggle.com/mit/pantheon-project/data> which originated from The Massachusetts Institute of Technology, about a year ago. The data is based off of metrics from many wikipedia pages. We felt that this data is credible given that it was processed and compiled from an institution as reputable as MIT. The variables within the data are as follows: `full_name`, `sex`, `birth_year`, `city`, `state`, `country`, `continent`, `latitude`, `longitude`, `occupation`, `industry`, `domain`, `article_langauges`, `page_views`, `average_views`, and `historical_popularity_index`.

For our question, we will be focusing on these particular variables: `full_name`, `birth_year`, `latitude`, `longitude`, `occupation`, `sex`, and `industry`.

Section 2. Data analysis plan
-----------------------------

### Linear Modelling

We will use linear modelling with multiple variables to predict the popularity metrics. The explanatory variables could be sex, birth\_year, city, country, article languages, and occuption. We will do backwards selection to reach a model that will maximally explain numeric metrics like page views, and historical popularity index. We can also segment this across several time periods since something that was popular in a certain time period would likely have different things about it that made readers want to learn about it. For example, what made Roman period might be occupations or industries relating to war and politics. We can also segment by geographical region so we can understand what made things popular in certain regions because the factors would likely be different. For example, the maths and sciences were huge in the middle east in the middle ages and it would be interesting to quantify this.

### Mapping

The outcomes we are expecting are proportions of men and women in the top 5 industries across time. The explanatory variables in this scenario are `sex`, while the response is the proportion in the industries.

We will be using `sex` and `industry` to compare groups of historical figures across time.

Add preliminary exploratory data analysis here:

The statistical method that we believe will be useful includes finding the proportions of each industry grouped by sex.

The results from the statistical method needed to support our hypothesized answer...

### Hypothesis Testing

Finally, we can use hypothesis testing to validate our results on what makes someone/industry/occupation popular. We can ask questions like: is the popularity index for women lower than that of men? Does America have the most popular filmmakers? Was war more prevalent in the past or present?

Section 3. Data
---------------

    ## Warning: running command 'timedatectl' had status 1

    ## Observations: 11,341
    ## Variables: 17
    ## $ article_id                  <int> 308, 22954, 1095706, 25664190, 783...
    ## $ full_name                   <chr> "Aristotle", "Plato", "Jesus Chris...
    ## $ sex                         <chr> "Male", "Male", "Male", "Male", "M...
    ## $ birth_year                  <int> -384, -427, -4, -469, -356, 1452, ...
    ## $ city                        <chr> "Stageira", "Athens", "Judea", "At...
    ## $ state                       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA...
    ## $ country                     <chr> "Greece", "Greece", "Israel", "Gre...
    ## $ continent                   <chr> "Europe", "Europe", "Asia", "Europ...
    ## $ latitude                    <dbl> 40.33333, 37.96667, 32.50000, 37.9...
    ## $ longitude                   <dbl> 23.50000, 23.71667, 34.90000, 23.7...
    ## $ occupation                  <chr> "Philosopher", "Philosopher", "Rel...
    ## $ industry                    <chr> "Philosophy", "Philosophy", "Relig...
    ## $ domain                      <chr> "Humanities", "Humanities", "Insti...
    ## $ article_languages           <int> 152, 142, 214, 137, 138, 174, 192,...
    ## $ page_views                  <int> 56355172, 46812003, 60299092, 4030...
    ## $ average_views               <int> 370758, 329662, 281771, 294213, 35...
    ## $ historical_popularity_index <dbl> 31.9938, 31.9888, 31.8981, 31.6521...
