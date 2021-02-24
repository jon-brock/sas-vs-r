SAS vs. R - An Introduction
================

-   [Loading Packages](#loading-packages)
-   [Importing a dataset](#importing-a-dataset)

![](banner.jpg)

------------------------------------------------------------------------

Welcome! This training is intended for those individuals who have
experience performing data cleaning and analysis in SAS, but want to
learn and develop similar skills in R. Get ready to have fun!

Here are some key things that you need to know about R:

1.  It is an object-oriented environment.  
2.  It can be run by itself, but most people use an IDE, such as R
    Studio, for easier work flows.  
3.  It can utilize many different `packages` that contain their own set
    of functions.  
4.  It is open-source and free!

I’m going to teach you to use R based on a “tidy” mindset, as
popularized by Hadley Wickham. His book, **R for Data Science**, is an
invaluable resource and is also free [online](https://r4ds.had.co.nz/).
The diagram below illustrates the general work flow for keeping your
code tidy.

![](https://rstudio-education.github.io/tidyverse-cookbook/images/data-science-workflow.png)

Let’s jump right into it!

------------------------------------------------------------------------

## Loading Packages

First, you’ll want to load your required packages for you to do your
work. You load your packages individually by using the R function
`library()`. To start, we will only use one package: `tidyverse`.

``` r
library(tidyverse)
```

If you do not have the `tidyverse` package installed, or any other
package you may need, you can install the package using the function
`install.package()` and typing `"package name"` inside the parentheses.
Be sure to include double-quotation marks around the package name.

The great thing about the `tidyverse` package is that it includes a
bundle of eight packages commonly used for data importing, wrangling,
and visualizing.

The eight packages are:

| Package   | What it can help you do                      |                                     Cheatsheets                                     |
|-----------|----------------------------------------------|:-----------------------------------------------------------------------------------:|
| `ggplot2` | plotting/visualizations                      | [pdf](https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf) |
| `tibble`  | working with tibbles (a type of data frame)  |                                         N/A                                         |
| `tidyr`   | data cleaning                                |                                         N/A                                         |
| `readr`   | importing different data types               |      [pdf](https://github.com/rstudio/cheatsheets/raw/master/data-import.pdf)       |
| `purrr`   | iterations and repeated tasks                |         [pdf](https://github.com/rstudio/cheatsheets/raw/master/purrr.pdf)          |
| `dplyr`   | data cleaning and manipulation               |  [pdf](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf)   |
| `stringr` | working with character (or string) variables |        [pdf](https://github.com/rstudio/cheatsheets/raw/master/strings.pdf)         |
| `forcats` | working with factor variables                |        [pdf](https://github.com/rstudio/cheatsheets/raw/master/factors.pdf)         |

There are other cheatsheets available
[here](https://rstudio.com/resources/cheatsheets/). Three other
cheatsheets that will be of particular value to you as a new user of R
include:

| Package     | What it can help you do               |                                Cheatsheets                                 |
|-------------|---------------------------------------|:--------------------------------------------------------------------------:|
| `lubridate` | working with times and dates          |   [pdf](https://github.com/rstudio/cheatsheets/raw/master/lubridate.pdf)   |
| `rmarkdown` | generating markdown documents         | [pdf](https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf) |
| `R studio*` | how to use R Studio (\*not a package) |  [pdf](https://github.com/rstudio/cheatsheets/raw/master/rstudio-ide.pdf)  |

------------------------------------------------------------------------

## Importing a dataset

In SAS, when importing a dataset, your would code like this:

    proc import out = jeopardy
                datafile = "/Users/jonbrock/Downloads/jeopardy.xlsx
                dbms = excel replace;
    run;

Using R, you will need to use a specific function to import data
depending upon the file type. In this case, we are importing an `xlsx`
file and will need to use both a specific package (`readxl`) and
function (`read_xlsx()`). The package reference guide is
[here](https://readxl.tidyverse.org/reference/index.html).

``` r
# Import the .xlsx file
jeopardy <- readxl::read_xlsx('./data/jeopardy.xlsx')

# Print the first ten observations in the dataset
head(jeopardy)
```

    ## # A tibble: 6 x 7
    ##   `Show Number` `Air Date`          Round  Category   Value Question      Answer
    ##           <dbl> <dttm>              <chr>  <chr>      <chr> <chr>         <chr> 
    ## 1          4680 2004-12-31 00:00:00 Jeopa… HISTORY    200   "For the las… Coper…
    ## 2          4680 2004-12-31 00:00:00 Jeopa… ESPN's TO… 200   "No. 2: 1912… Jim T…
    ## 3          4680 2004-12-31 00:00:00 Jeopa… EVERYBODY… 200   "The city of… Arizo…
    ## 4          4680 2004-12-31 00:00:00 Jeopa… THE COMPA… 200   "In 1963, li… McDon…
    ## 5          4680 2004-12-31 00:00:00 Jeopa… EPITAPHS … 200   "Signer of t… John …
    ## 6          4680 2004-12-31 00:00:00 Jeopa… 3-LETTER … 200   "In the titl… the a…

Great! We know that our data was imported correctly. But it sure does
look messy! Let’s tidy this a bit. Let’s run the same import code but
clean up the variable names using `janitor::clean_names()`.

``` r
# Import the .xlsx file
jeopardy <- readxl::read_xlsx('./data/jeopardy.xlsx') %>% 
    janitor::clean_names()

# Print the first ten observations in the dataset
head(jeopardy)
```

    ## # A tibble: 6 x 7
    ##   show_number air_date            round  category    value question       answer
    ##         <dbl> <dttm>              <chr>  <chr>       <chr> <chr>          <chr> 
    ## 1        4680 2004-12-31 00:00:00 Jeopa… HISTORY     200   "For the last… Coper…
    ## 2        4680 2004-12-31 00:00:00 Jeopa… ESPN's TOP… 200   "No. 2: 1912 … Jim T…
    ## 3        4680 2004-12-31 00:00:00 Jeopa… EVERYBODY … 200   "The city of … Arizo…
    ## 4        4680 2004-12-31 00:00:00 Jeopa… THE COMPAN… 200   "In 1963, liv… McDon…
    ## 5        4680 2004-12-31 00:00:00 Jeopa… EPITAPHS &… 200   "Signer of th… John …
    ## 6        4680 2004-12-31 00:00:00 Jeopa… 3-LETTER W… 200   "In the title… the a…

We’ve now cleaned our variable names to remove any punctuation or
spaces, which are things that will make your life a nightmare as you
develop more code. If we wanted to see what the variables names are, or
get a quick “glimpse” at our variables, their data types, and the first
few observations, we can run the following codes as needed:

``` r
# View variable names
names(jeopardy)
```

    ## [1] "show_number" "air_date"    "round"       "category"    "value"      
    ## [6] "question"    "answer"

``` r
# Glimpse part of the dataset
glimpse(jeopardy)
```

    ## Rows: 216,930
    ## Columns: 7
    ## $ show_number <dbl> 4680, 4680, 4680, 4680, 4680, 4680, 4680, 4680, 4680, 4680…
    ## $ air_date    <dttm> 2004-12-31, 2004-12-31, 2004-12-31, 2004-12-31, 2004-12-3…
    ## $ round       <chr> "Jeopardy!", "Jeopardy!", "Jeopardy!", "Jeopardy!", "Jeopa…
    ## $ category    <chr> "HISTORY", "ESPN's TOP 10 ALL-TIME ATHLETES", "EVERYBODY T…
    ## $ value       <chr> "200", "200", "200", "200", "200", "200", "400", "400", "4…
    ## $ question    <chr> "For the last 8 years of his life, Galileo was under house…
    ## $ answer      <chr> "Copernicus", "Jim Thorpe", "Arizona", "McDonald's", "John…

``` r
# View the structure of the dataset
str(jeopardy)
```

    ## tibble [216,930 × 7] (S3: tbl_df/tbl/data.frame)
    ##  $ show_number: num [1:216930] 4680 4680 4680 4680 4680 4680 4680 4680 4680 4680 ...
    ##  $ air_date   : POSIXct[1:216930], format: "2004-12-31" "2004-12-31" ...
    ##  $ round      : chr [1:216930] "Jeopardy!" "Jeopardy!" "Jeopardy!" "Jeopardy!" ...
    ##  $ category   : chr [1:216930] "HISTORY" "ESPN's TOP 10 ALL-TIME ATHLETES" "EVERYBODY TALKS ABOUT IT..." "THE COMPANY LINE" ...
    ##  $ value      : chr [1:216930] "200" "200" "200" "200" ...
    ##  $ question   : chr [1:216930] "For the last 8 years of his life, Galileo was under house arrest for espousing this man's theory" "No. 2: 1912 Olympian; football star at Carlisle Indian School; 6 MLB seasons with the Reds, Giants & Braves" "The city of Yuma in this state has a record average of 4,055 hours of sunshine each year" "In 1963, live on \"The Art Linkletter Show\", this company served its billionth burger" ...
    ##  $ answer     : chr [1:216930] "Copernicus" "Jim Thorpe" "Arizona" "McDonald's" ...

------------------------------------------------------------------------
