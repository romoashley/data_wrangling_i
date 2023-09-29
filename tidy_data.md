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