template
================
ASHLEY ROMO
2023-09-24

Let’s import the `FAS_litters.csv` csv using a realtive path

``` r
library(tidyverse) 
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
#load data in a dataframe by using read_csv("datafile pathname"). This requires tidyverse to be loaded first.The pathname is within the project you are under. 

litters_df = read_csv("data/FAS_litters.csv") 
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#change variable names to snake case 
#janitor::clean_names(dataframe) replaces that dataframe with an updated version with snake case variable names (upper case converted to lowercase, spaces converted to underscores, special characters get removed). The code janitor::clean_names(dataframe) says inside the janitor package, use the functon clean_names. 

litters_df = janitor::clean_names(litters_df) 
# note: janitor is a package in R that has many functions. You can load the entire package like you did with tideverse. It would look like this: library(janitor). 
```

Import the same dataset using an absolute path.

``` r
litters_df_abs = read_csv("/Users/ashleyromo/Desktop/P8105/data_wrangling_i/data/FAS_litters.csv") 
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df) 

#if you move the location of the fodler with the data, the absolute path no longer works, which why it is always better to use relative paths.
```
