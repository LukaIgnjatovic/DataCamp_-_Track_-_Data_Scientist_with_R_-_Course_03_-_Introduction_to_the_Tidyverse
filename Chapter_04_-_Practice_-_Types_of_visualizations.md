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

## Types of visualizations

You've learned to create scatter plots with ggplot2. In this chapter you'll learn to create line plots, bar plots, histograms, and boxplots. You'll see how each plot needs different kinds of data manipulation to prepare for it, and understand the different roles of each of these plot types in data analysis.

<div align="middle">

> **Document:** ["Slides - Grouping and summarizing"](./Slides/Chapter 04 - Types of visualizations.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 01 - Line plots.mp4" type="video/mp4"/>

</div>

### Visualizing median GDP per capita over time

A line plot is useful for visualizing trends over time. In this exercise, you'll examine how the median GDP per capita has changed over time.

#### Instructions
* *Use* `group_by()` *and* `summarize()` *to find the median GDP per capita within each year, calling the output column* `medianGdpPercap`*. Use the assignment operator* `<-` *to save it to a dataset called* `by_year`*.*
* *Use the* `by_year` *dataset to create a line plot showing the change in median GDP per capita over time. Be sure to use* `expand_limits(y = 0)` *to include 0 on the y-axis.*

```r
library(gapminder)
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
library(ggplot2)

# Summarize the median gdpPercap by year, then save it as by_year
by_year <- gapminder %>%
  group_by(year) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a line plot showing the change in medianGdpPercap over time
ggplot(by_year, aes(x = year, y = medianGdpPercap)) + 
  geom_line() + 
  expand_limits(y = 0)
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

**Great! Looks like median GDP per capita across countries has gone up over time.**

### Visualizing median GDP per capita by continent over time

In the last exercise you used a line plot to visualize the increase in median GDP per capita over time. Now you'll examine the change within each continent.

#### Instructions
* *Use* `group_by()` *and* `summarize()` *to find the median GDP per capita within each year and continent, calling the output column* `medianGdpPercap`*. Use the assignment operator* `<-` *to save it to a dataset called* `by_year_continent`*.*
* *Use the* `by_year_continent` *dataset to create a line plot showing the change in median GDP per capita over time, with color representing continent. **Be sure** to use* `expand_limits(y = 0)` *to include 0 on the y-axis.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

# Summarize the median gdpPercap by year & continent, save as by_year_continent
by_year_continent <- gapminder %>%
  group_by(year, continent) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a line plot showing the change in medianGdpPercap by continent over time
ggplot(by_year_continent, aes(x = year, y = medianGdpPercap, color = continent)) + 
  geom_line() + 
  expand_limits(y = 0)
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

**Excellent work! Take a look at the plot: did the growth in median GDP per capita differ between continents?**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 02 - Bar plots.mp4" type="video/mp4"/>

</div>

### Visualizing median GDP per capita by continent

A bar plot is useful for visualizing summary statistics, such as the median GDP in each continent.

#### Instructions
* *Use* `group_by()` *and* `summarize()` *to find the median GDP per capita within each continent in the year 1952, calling the output column* `medianGdpPercap`*. Use the assignment operator* `<-` *to save it to a dataset called* `by_continent`*.*
* *Use the* `by_continent` *dataset to create a bar plot showing the median GDP per capita in each continent.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

# Summarize the median gdpPercap by year and continent in 1952
by_continent <- gapminder %>%
  filter(year == 1952) %>%
  group_by(continent) %>%
  summarize(medianGdpPercap = median(gdpPercap))

# Create a bar plot showing medianGdp by continent
ggplot(by_continent, aes(x = continent, y = medianGdpPercap)) + 
  geom_col()
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

**Excellent! That's three kinds of plots you're now able to make with** `ggplot2`**.**

### Visualizing GDP per capita by country in Oceania

You've created a plot where each bar represents one continent, showing the median GDP per capita for each. But the x-axis of the bar plot doesn't have to be the continent: you can instead create a bar plot where each bar represents a country.

In this exercise, you'll create a bar plot comparing the GDP per capita between the two countries in the Oceania continent (Australia and New Zealand).

#### Instructions
* *Filter for observations in the **Oceania** continent in the year 1952. Save this as* `oceania_1952`*.*
* *Use the* `oceania_1952` *dataset to create a bar plot, with country on the x-axis and* `gdpPercap` *on the y-axis.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

# Filter for observations in the Oceania continent in 1952
oceania_1952 <- gapminder %>%
  filter(continent == "Oceania", year == 1952)

# Create a bar plot of gdpPercap by country
ggplot(oceania_1952, aes(x = country, y = gdpPercap)) + 
  geom_col()
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

**Good work! Looks like the GDP per capita of these two countries was similar in 1952.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 03 - Histograms.mp4" type="video/mp4"/>

</div>

### Visualizing population

A histogram is useful for examining the distribution of a numeric variable. In this exercise, you'll create a histogram showing the distribution of country populations in the year 1952.

#### Instructions
*Use the* `gapminder_1952` *dataset (code for generating that dataset is provided) to create a histogram of country population (*`pop`*) in the year 1952.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Create a histogram of population (pop)
ggplot(gapminder_1952, aes(x = pop)) + 
  geom_histogram()
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

**That's right! Notice that most of the distribution is in the smallest (leftmost) bins. In the next exercise you'll put the x-axis on a log scale.**

### Visualizing population with x-axis on a log scale

In the last exercise you created a histogram of populations across countries. You might have noticed that there were several countries with a much higher population than others, which causes the distribution to be very skewed, with most of the distribution crammed into a small part of the graph. (Consider that it's hard to tell the median or the minimum population from that histogram).

To make the histogram more informative, you can try putting the x-axis on a log scale.

#### Instructions
*Use the* `gapminder_1952` *dataset (code is provided) to create a histogram of country population (*`pop`*) in the year 1952, putting the x-axis on a log scale with* `scale_x_log10()`*.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Create a histogram of population (pop), with x on a log scale
ggplot(gapminder_1952, aes(x = pop)) + 
  geom_histogram() + 
  scale_x_log10()
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

**Great! Notice that on a log scale, the distribution of country populations is approximately symmetrical.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 04 - Boxplots.mp4" type="video/mp4"/>

</div>

### Comparing GDP per capita across continents

A boxplot is useful for comparing a distribution of values across several groups. In this exercise, you'll examine the distribution of GDP per capita by continent. Since GDP per capita varies across several orders of magnitude, you'll need to put the y-axis on a log scale.

#### Instructions
*Use the* `gapminder_1952` *dataset (code is provided) to create a boxplot comparing GDP per capita (*`gdpPercap`*) among continents. Put the y-axis on a log scale with* `scale_y_log10()`*.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Create a boxplot comparing gdpPercap among continents
ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) + 
  geom_boxplot() + 
  scale_y_log10()
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**Looks good! What continents had countries with the highest GDP per capita?**

### Adding a title to your graph

There are many other options for customizing a `ggplot2` graph, which you can learn about in other DataCamp courses. You can also learn about them from online resources, which is an important skill to develop.

As the final exercise in this course, you'll practice looking up `ggplot2` instructions by completing a task we haven't shown you how to do.

#### Instructions
*Add a title to the graph: **"Comparing GDP per capita across continents"**. Use a search engine, such as Google or Bing, to learn how to do so.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Add a title to this graph: "Comparing GDP per capita across continents"
ggplot(gapminder_1952, aes(x = continent, y = gdpPercap)) +
  geom_boxplot() +
  scale_y_log10() + 
  ggtitle("Comparing GDP per capita across continents")
```

![](Chapter_04_-_Practice_-_Types_of_visualizations_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

**Brilliant! Now you know how to look up additional methods for customizing graphs. That will be very useful in your career as an R user!**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 04 - Lecture 05 - Conclusions.mp4" type="video/mp4"/>

</div>

**You have finished the chapter "Types of visualizations"!**
