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

## Data visualization

You've already been able to answer some questions about the data through dplyr, but you've engaged with them just as a table (such as one showing the life expectancy in the US each year). Often a better way to understand and present such data is as a graph. Here you'll learn the essential skill of data visualization, using the ggplot2 package. Visualization and manipulation are often intertwined, so you'll see how the dplyr and ggplot2 packages work closely together to create informative graphs.

<div align="middle">

> **Document:** ["Slides - Data visualization"](./Slides/Chapter 02 - Data visualization.pdf)

</div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 02 - Lecture 01 - Visualizing with ggplot2.mp4" type="video/mp4"/>

</div>

### Variable assignment

Throughout the exercises in this chapter, you'll be visualizing a subset of the gapminder data from the year 1952. First, you'll have to load the ggplot2 package, and create a `gapminder_1952` dataset to visualize.

#### Instructions
* *Load the* `ggplot2` *package after the gapminder and dplyr packages.*
* *Filter* `gapminder` *for observations from the year 1952, and assign it to a new dataset* `gapminder_1952` *using the assignment operator (*`<-`*).*

```r
# Load the ggplot2 package as well
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

# Create gapminder_1952
gapminder_1952 <- gapminder %>%
  filter(year == 1952)
```

**Great! If you typed** `gapminder_1952` **now, you'd see the filtered dataset.**

### Comparing population and GDP per capita

In the video you learned to create a scatter plot with GDP per capita on the x-axis and life expectancy on the y-axis (the code for that graph is shown here). When you're exploring data visually, you'll often need to try different combinations of variables and aesthetics.

#### Instructions
*Change the scatter plot of* `gapminder_1952` *so that (*`pop`*) is on the x-axis and GDP per capita (*`gdpPercap`*) is on the y-axis.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Change to put pop on the x-axis and gdpPercap on the y-axis
ggplot(gapminder_1952, aes(x = pop, y = gdpPercap)) +
  geom_point()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

**Great work on your first graph! Each point represents a country: can you guess which country any of the points are?**

### Comparing population and life expectancy

In this exercise, you'll use `ggplot2` to create a scatter plot from scratch, to compare each country's population with its life expectancy in the year 1952.

#### Instructions
*Create a scatter plot of* `gapminder_1952` *with population (*`pop`*) is on the x-axis and life expectancy (*`lifeExp`*) on the y-axis.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Create a scatter plot with pop on the x-axis and lifeExp on the y-axis
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) + 
  geom_point()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

**Great! You might notice the points are crowded towards the left side of the plot, making them hard to distinguish. This next video will help solve that problem.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 02 - Lecture 02 - Log scales.mp4" type="video/mp4"/>

</div>

### Putting the x-axis on a log scale

You previously created a scatter plot with population on the x-axis and life expectancy on the y-axis. Since population is spread over several orders of magnitude, with some countries having a much higher population than others, it's a good idea to put the x-axis on a log scale.

#### Instructions
*Add a* `filter()` *line after the pipe (*`%>%`*) to extract only the observations from the year 1957. Remember that you use* `==` *to compare two values.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Change this plot to put the x-axis on a log scale
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) +
  geom_point() +
  scale_x_log10()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

**Great! Notice the points are more spread out on the x-axis. This makes it easy to see that there isn't a correlation between population and life expectancy.**

### Putting the x- and y- axes on a log scale

Suppose you want to create a scatter plot with population on the x-axis and GDP per capita on the y-axis. Both population and GDP per-capita are better represented with log scales, since they vary over many orders of magnitude.

#### Instructions
*Create a scatter plot with population (*`pop`*) on the x-axis and GDP per capita (*`gdpPercap`*) on the y-axis. Put **both** the x and y axes on a log scale.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Scatter plot comparing pop and gdpPercap, with both axes on a log scale
ggplot(gapminder_1952, aes(x = pop, y = gdpPercap)) +
  geom_point() + 
  scale_x_log10() +
  scale_y_log10()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

**Great! Notice that the y-axis goes from 1e3 (1000) to 1e4 (10,000) to 1e5 (100,000) in equal increments.**

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 02 - Lecture 03 - Additional aesthetics.mp4" type="video/mp4"/>

</div>

### Adding color to a scatter plot

In this lesson you learned how to use the color aesthetic, which can be used to show which continent each point in a scatter plot represents.

#### Instructions
*Create a scatter plot with population (*`pop`*) on the x-axis, life expectancy (*`lifeExp`*) on the y-axis, and with continent (*`continent`*) represented by the color of the points. Put the x-axis on a log scale.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Scatter plot comparing pop and lifeExp, with color representing continent
ggplot(gapminder_1952, aes(x = pop, y = lifeExp, color = continent)) +
  geom_point() +
  scale_x_log10()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

**Good work! What differences can you see between continents, in terms of their population and life expectancy?**

### Adding size and color to a plot

In the last exercise, you created a scatter plot communicating information about each country's population, life expectancy, and continent. Now you'll use the size of the points to communicate even more.

#### Instructions
*Modify the scatter plot so that the size of the points represents each country's GDP per capita (*`gdpPercap`*).*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Add the size aesthetic to represent a country's gdpPercap
ggplot(gapminder_1952, aes(x = pop, y = lifeExp, color = continent, size = gdpPercap)) +
  geom_point() +
  scale_x_log10()
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**Good work! Are you able to guess which point represents your own country?**

<div>

<div align="middle">

<video width="80%" controls src="./Videos/Chapter 02 - Lecture 04 - Faceting.mp4" type="video/mp4"/>

</div>

### Creating a subgraph for each continent

You've learned to use faceting to divide a graph into subplots based on one of its variables, such as the continent.

#### Instructions
*Create a scatter plot of* `gapminder_1952` *with the x-axis representing population (*`pop`*), the y-axis representing life expectancy (*`lifeExp`*), and faceted to have one subplot per continent (*`continent`*). Put the x-axis on a log scale.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

gapminder_1952 <- gapminder %>%
  filter(year == 1952)

# Scatter plot comparing pop and lifeExp, faceted by continent
ggplot(gapminder_1952, aes(x = pop, y = lifeExp)) +
  geom_point() +
  scale_x_log10() + 
  facet_wrap(~ continent)
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

**Great work! Faceting is a powerful way to understand subsets of your data separately.**

### Faceting by year

All of the graphs in this chapter have been visualizing statistics within one year. Now that you're able to use faceting, however, you can create a graph showing **all** the country-level data from 1952 to 2007, to understand how global statistics have changed over time.

#### Instructions
*Create a scatter plot of the* `gapminder` *data:*
* *Put GDP per capita (*`gdpPercap`*) on the x-axis and life expectancy (*`lifeExp`*) on the y-axis, with continent (*`continent`*) represented by color and population (*`pop`*) represented by size.*
* *Put the x-axis on a log scale.*
* *Facet by the* `year` *variable.*

```r
library(gapminder)
library(dplyr)
library(ggplot2)

# Scatter plot comparing gdpPercap and lifeExp, with color representing continent
# and size representing population, faceted by year
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  geom_point() +
  scale_x_log10() +
  facet_wrap(~ year)
```

![](Chapter_02_-_Practice_-_Data_visualization_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

**Awesome! That's a lot of information you're now able to share in one graph.**  
**You have finished the chapter "Data visualization"!**
