---
title: "DataCamp - Introduction to the Tidyverse"
author: "[Luka Ignjatovi&#263;](https://github.com/LukaIgnjatovic)"
output:
  html_document:
    highlight: tango
    theme: united
    toc: yes
    toc_depth: 4
    keep_md: true
  md_document:
    toc: true
    toc_depth: 4
---

## Data wrangling

In this chapter, you'll learn to do three things with a table: filter for particular observations, arrange the observations in a desired order, and mutate to add or change a column. You'll see how each of these steps lets you answer questions about your data.

<div align="middle">

> **Document:** ["Slides - Data wrangling"](./Slides/Chapter 01 - Data wrangling.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 01 - Lecture 01 - The gapminder dataset.mp4" type="video/mp4"/>

</div>

### Loading the gapminder and dplyr packages

Before you can work with the gapminder dataset, you'll need to load two R packages that contain the tools for working with it, then display the `gapminder` dataset so that you can see what it contains.

To your right, you'll see two windows inside which you can enter code: The `script.R` window, and the R Console. All of your code to solve each exercise must go inside `script.R`.

If you hit *Submit Answer*, your R script is executed and the output is shown in the R Console. DataCamp checks whether your submission is correct and gives you feedback. You can hit *Submit Answer* as often as you want. If you're stuck, you can ask for a hint or a solution.

You can use the R Console interactively by simply typing R code and hitting Enter. When you work in the console directly, your code will not be checked for correctness so it is a great way to experiment and explore.

#### Instructions
* *Use the* `library()` *function to load the* `dplyr` *package, just like we've loaded the* `gapminder` *package for you.*
* *Type* `gapminder`*, on its own line, to look at the gapminder dataset.*

```r
# Load the gapminder package
library(gapminder)

# Load the dplyr package
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
# Look at the gapminder dataset
gapminder
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
## # ... with 1,694 more rows
```

**Great job! Notice that you can see the gapminder dataset in the console output on the lower right. This is called 'printing' a dataset.**

### Understanding a data frame

Now that you've loaded the `gapminder` dataset, you can start examining and understanding it.

We've already loaded the `gapminder` and `dplyr` packages. Type `gapminder` in your R terminal, to the right, to display the object.

How many observations (rows) are in the dataset?

*Possible answers:*

* **1704**
* *6*
* *1694*
* *1952*

**Correct!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 01 - Lecture 02 - The filter verb.mp4" type="video/mp4"/>

</div>

### Filtering for one year

The `filter` verb extracts particular observations based on a condition. In this exercise you'll filter for observations from a particular year.

#### Instructions
*Add a* `filter()` *line after the pipe (*`%>%`*) to extract only the observations from the year 1957. Remember that you use* `==` *to compare two values.*

```r
library(gapminder)
library(dplyr)

# Filter the gapminder dataset for the year 1957
gapminder %>%
  filter(year == 1957)
```

```
## # A tibble: 142 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1957    30.3  9240934      821.
##  2 Albania     Europe     1957    59.3  1476505     1942.
##  3 Algeria     Africa     1957    45.7 10270856     3014.
##  4 Angola      Africa     1957    32.0  4561361     3828.
##  5 Argentina   Americas   1957    64.4 19610538     6857.
##  6 Australia   Oceania    1957    70.3  9712569    10950.
##  7 Austria     Europe     1957    67.5  6965860     8843.
##  8 Bahrain     Asia       1957    53.8   138655    11636.
##  9 Bangladesh  Asia       1957    39.3 51365468      662.
## 10 Belgium     Europe     1957    69.2  8989111     9715.
## # ... with 132 more rows
```

**That's right! Notice that all the observations in the output have the year 1957.**

### Filtering for one country and one year

You can also use the `filter()` verb to set two conditions, which could retrieve a single observation.

Just like in the last exercise, you can do this in two lines of code, starting with `gapminder %>%` and having the `filter()` on the second line. Keeping one verb on each line helps keep the code readable. Note that each time, you'll put the pipe `%>%` at the end of the first line (like `gapminder %>%`); putting the pipe at the beginning of the second line will throw an error.

#### Instructions
*Filter the* `gapminder` *data to retrieve only the observation from China in the year 2002.*

```r
library(gapminder)
library(dplyr)

# Filter for China in 2002
gapminder %>%
  filter(country == "China", year == 2002)
```

```
## # A tibble: 1 x 6
##   country continent  year lifeExp        pop gdpPercap
##   <fct>   <fct>     <int>   <dbl>      <int>     <dbl>
## 1 China   Asia       2002    72.0 1280400000     3119.
```

**Good work! This is a useful way to grab a single observation you're interested in.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 01 - Lecture 03 - The arrange verb.mp4" type="video/mp4"/>

</div>

### Arranging observations by life expectancy

You use `arrange()` to sort observations in ascending or descending order of a particular variable. In this case, you'll sort the dataset based on the `lifeExp` variable.

#### Instructions
* *Sort the* `gapminder` *dataset in ascending order of life expectancy (*`lifeExp`*).*
* *Sort the* `gapminder` *dataset in descending order of life expectancy.*

```r
library(gapminder)
library(dplyr)

# Sort in ascending order of lifeExp
gapminder %>%
  arrange(lifeExp)
```

```
## # A tibble: 1,704 x 6
##    country      continent  year lifeExp     pop gdpPercap
##    <fct>        <fct>     <int>   <dbl>   <int>     <dbl>
##  1 Rwanda       Africa     1992    23.6 7290203      737.
##  2 Afghanistan  Asia       1952    28.8 8425333      779.
##  3 Gambia       Africa     1952    30    284320      485.
##  4 Angola       Africa     1952    30.0 4232095     3521.
##  5 Sierra Leone Africa     1952    30.3 2143249      880.
##  6 Afghanistan  Asia       1957    30.3 9240934      821.
##  7 Cambodia     Asia       1977    31.2 6978607      525.
##  8 Mozambique   Africa     1952    31.3 6446316      469.
##  9 Sierra Leone Africa     1957    31.6 2295678     1004.
## 10 Burkina Faso Africa     1952    32.0 4469979      543.
## # ... with 1,694 more rows
```

```r
# Sort in descending order of lifeExp
gapminder %>%
  arrange(desc(lifeExp))
```

```
## # A tibble: 1,704 x 6
##    country          continent  year lifeExp       pop gdpPercap
##    <fct>            <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Japan            Asia       2007    82.6 127467972    31656.
##  2 Hong Kong, China Asia       2007    82.2   6980412    39725.
##  3 Japan            Asia       2002    82   127065841    28605.
##  4 Iceland          Europe     2007    81.8    301931    36181.
##  5 Switzerland      Europe     2007    81.7   7554661    37506.
##  6 Hong Kong, China Asia       2002    81.5   6762476    30209.
##  7 Australia        Oceania    2007    81.2  20434176    34435.
##  8 Spain            Europe     2007    80.9  40448191    28821.
##  9 Sweden           Europe     2007    80.9   9031088    33860.
## 10 Israel           Asia       2007    80.7   6426679    25523.
## # ... with 1,694 more rows
```

**That's right! Take a look at the countries with the highest and lowest life expectancy- is it similar to what you expected?**

### Filtering and arranging

You'll often need to use the pipe operator (`%>%`) to combine multiple dplyr verbs in a row. In this case, you'll combine a `filter()` with an `arrange()` to find the highest population countries in a particular year.

#### Instructions
*Use* `filter()` *to extract observations from just the year 1957, then use* `arrange()` *to sort in descending order of population (*`pop`*).*

```r
library(gapminder)
library(dplyr)

# Filter for the year 1957, then arrange in descending order of population
gapminder %>%
  filter(year == 1957) %>%
  arrange(desc(pop))
```

```
## # A tibble: 142 x 6
##    country        continent  year lifeExp       pop gdpPercap
##    <fct>          <fct>     <int>   <dbl>     <int>     <dbl>
##  1 China          Asia       1957    50.5 637408000      576.
##  2 India          Asia       1957    40.2 409000000      590.
##  3 United States  Americas   1957    69.5 171984000    14847.
##  4 Japan          Asia       1957    65.5  91563009     4318.
##  5 Indonesia      Asia       1957    39.9  90124000      859.
##  6 Germany        Europe     1957    69.1  71019069    10188.
##  7 Brazil         Americas   1957    53.3  65551171     2487.
##  8 United Kingdom Europe     1957    70.4  51430000    11283.
##  9 Bangladesh     Asia       1957    39.3  51365468      662.
## 10 Italy          Europe     1957    67.8  49182000     6249.
## # ... with 132 more rows
```

**Great work! A lot of the exercises in this course will involve combining multiple steps with the** `%>%` **operator.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 01 - Lecture 04 - The mutate verb.mp4" type="video/mp4"/>

</div>

### Using mutate to change or create a column

Suppose we want life expectancy to be measured in months instead of years: you'd have to multiply the existing value by 12. You can use the `mutate()` verb to change this column, or to create a new column that's calculated this way.

#### Instructions
* *Use* `mutate()` *to change the existing* `lifeExp` *column, by multiplying it by 12:* `12 * lifeExp`*.*
* *Use* `mutate()` *to add a new column, called* `lifeExpMonths`*, calculated as* `12 * lifeExp`*.*

```r
library(gapminder)
library(dplyr)

# Use mutate to change lifeExp to be in months
gapminder %>%
  mutate(lifeExp = lifeExp * 12)
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    346.  8425333      779.
##  2 Afghanistan Asia       1957    364.  9240934      821.
##  3 Afghanistan Asia       1962    384. 10267083      853.
##  4 Afghanistan Asia       1967    408. 11537966      836.
##  5 Afghanistan Asia       1972    433. 13079460      740.
##  6 Afghanistan Asia       1977    461. 14880372      786.
##  7 Afghanistan Asia       1982    478. 12881816      978.
##  8 Afghanistan Asia       1987    490. 13867957      852.
##  9 Afghanistan Asia       1992    500. 16317921      649.
## 10 Afghanistan Asia       1997    501. 22227415      635.
## # ... with 1,694 more rows
```

```r
# Use mutate to create a new column called lifeExpMonths
gapminder %>%
  mutate(lifeExpMonths = lifeExp * 12)
```

```
## # A tibble: 1,704 x 7
##    country     continent  year lifeExp      pop gdpPercap lifeExpMonths
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>         <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.          346.
##  2 Afghanistan Asia       1957    30.3  9240934      821.          364.
##  3 Afghanistan Asia       1962    32.0 10267083      853.          384.
##  4 Afghanistan Asia       1967    34.0 11537966      836.          408.
##  5 Afghanistan Asia       1972    36.1 13079460      740.          433.
##  6 Afghanistan Asia       1977    38.4 14880372      786.          461.
##  7 Afghanistan Asia       1982    39.9 12881816      978.          478.
##  8 Afghanistan Asia       1987    40.8 13867957      852.          490.
##  9 Afghanistan Asia       1992    41.7 16317921      649.          500.
## 10 Afghanistan Asia       1997    41.8 22227415      635.          501.
## # ... with 1,694 more rows
```

**That's right!**

### Combining filter, mutate, and arrange

In this exercise, you'll combine all three of the verbs you've learned in this chapter, to find the countries with the highest life expectancy, in months, in the year 2007.

#### Instructions
*In one sequence of pipes on the* `gapminder` *dataset:*

* `filter()` *for observations from the year 2007,*
* `mutate()` *to create a column* `lifeExpMonths`*, calculated as* `12 * lifeExp`*, and*
* `arrange()` *in descending order of that new column.*

```r
library(gapminder)
library(dplyr)

# Filter, mutate, and arrange the gapminder dataset
gapminder %>%
  filter(year == 2007) %>%
  mutate(lifeExpMonths = lifeExp * 12) %>%
  arrange(desc(lifeExpMonths))
```

```
## # A tibble: 142 x 7
##    country         continent  year lifeExp      pop gdpPercap lifeExpMonths
##    <fct>           <fct>     <int>   <dbl>    <int>     <dbl>         <dbl>
##  1 Japan           Asia       2007    82.6   1.27e8    31656.          991.
##  2 Hong Kong, Chi~ Asia       2007    82.2   6.98e6    39725.          986.
##  3 Iceland         Europe     2007    81.8   3.02e5    36181.          981.
##  4 Switzerland     Europe     2007    81.7   7.55e6    37506.          980.
##  5 Australia       Oceania    2007    81.2   2.04e7    34435.          975.
##  6 Spain           Europe     2007    80.9   4.04e7    28821.          971.
##  7 Sweden          Europe     2007    80.9   9.03e6    33860.          971.
##  8 Israel          Asia       2007    80.7   6.43e6    25523.          969.
##  9 France          Europe     2007    80.7   6.11e7    30470.          968.
## 10 Canada          Americas   2007    80.7   3.34e7    36319.          968.
## # ... with 132 more rows
```

**Great work! Notice how you can combine several dplyr operations to answer a more complicated question like this.**  
**You have finished the chapter "Data wrangling"!**
