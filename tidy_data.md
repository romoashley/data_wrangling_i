Tidy data
================
ASHLEY ROMO
2023-09-26

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

## PULSE data

``` r
pulse_df = 
  haven::read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names() |> 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit",
    values_to = "bdi_score",
    names_prefix = "bdi_score_"
  ) |> 
  mutate(
    visit = replace(visit, visit == "bl", "00m")
  )
    
# pivot_longer() says what are the columns that are in wide format and need to be converted to long format and what are you going to name the resulting columns that come of this. Then " bid_scor_bl:bdi_score_12m" is going to take each of these put them in a column thats is observation time. Its going to put the numbers in each row and put them in their own column. names_to is the name you will name the columns you are going to turn in a variable. 
#value_to is the variable name of the columns the individual numbers are going to map to. 
#names_prefix is geting ride off the prefeix listed

# replace is saying in visit, everytime visit is "bl" replace it to "00m"
```

## Learning Assessment

``` r
weight_df =
  haven::read_sas("data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names() |> 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit",
    values_to = "score",
    names_prefix = "bdi_score_"
  ) |> 
  mutate(
    visit = replace(visit, visit == "bl", "00,")
  )
```

Import / lengthen the litters dataset.

``` r
litters_df=
  read_csv("data/FAS_litters.csv") |> 
  janitor::clean_names() |> 
  select(litter_number, gd0_weight, gd18_weight) |> 
  pivot_longer(
    gd0_weight:gd18_weight,
    names_to = "gd",
    values_to = "weight",
    names_prefix = "gd"
  ) |> 
  mutate(
    gd = case_match(
      gd,
      "gd0_weight"~ 0,
      "gd18_weight" ~ 18,
    )
  )
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
#case_match is going into the gd column and chaing everywhere it sees 0_weight to 0 and 18_weight to 18
```

## LoTR

Import LoTR words data

``` r
fellowship_df =
  readxl::read_excel("data/LotR_Words.xlsx", range = "B3:D6") |> 
  mutate(movie = "fellowship")

two_towers_df =
  readxl::read_excel("data/LotR_Words.xlsx", range = "F3:H6") |> 
  mutate(movie = "two towers")

return_of_the_king_df =
  readxl::read_excel("data/LotR_Words.xlsx", range = "J3:L6") |> 
  mutate(movie = "return of the king")

#now, we are going to merge data

lotr_df =
  bind_rows(fellowship_df, two_towers_df, return_of_the_king_df) |> 
  janitor::clean_names() |> 
  pivot_longer(
    male : female,
    names_to = "gendr",
    values_to = "word"
  ) |> 
  relocate(movie)
```
