Reading data from the web
================

## Scrape a table

I want the first table from [this
page](http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm)

read in the html

``` r
url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

drug_use_html = read_html(url)
```

extract the table(s); focus on the first one

``` r
tabl_marj = 
  drug_use_html %>% 
  html_nodes(css = "table") %>% 
  first() %>%    ## last():extract the last one; nth():extract the nth one
  html_table()  %>%  ## convert the html format into table format
  slice(-1)  %>%   ## slice function at rows, and this means get rid of the fisrt row
  as_tibble()     ## convert the format to tibble format
```

## Star Wars movie info

I want the data from [here](https://www.imdb.com/list/ls070150896/)

``` r
url = "https://www.imdb.com/list/ls070150896/"

swm_html = read_html(url)
```

grab elements that I want.

``` r
title_vec = 
  swm_html %>% 
  html_nodes(css = '.lister-item-header a') %>% 
  html_text()    ## Convert into the text format

gross_rev_vec = 
  swm_html %>% 
  html_nodes(css = '.text-small:nth-child(7) span:nth-child(5)') %>% 
  html_text()

runtime_vec = 
  swm_html %>% 
  html_nodes(css = '.runtime') %>% 
  html_text()

swm_df = 
  tibble(
    title = title_vec,
    gross_rev = gross_rev_vec,
    runtime = runtime_vec
  )
```

## Get some water data

This is coming from an API

``` r
nyc_water = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") %>% 
  content('parsed')
```

    ## Rows: 43 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
nyc_water_json = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.json") %>% 
  content('text') %>% 
  jsonlite::fromJSON() %>% 
  as_tibble()
```

## BRFSS

Same process, different data

``` r
brfss_2010 = 
  GET('https://chronicdata.cdc.gov/resource/acme-vg9e.csv',
      query = list('$limit' = 2000)) %>%  ##by default, it only retrive 1000 data, and we can use the query parameter to set the number of data we want 
  content('parsed')
```

    ## Rows: 2000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Some data aren’t so nice

Let’s look at Pokemon…

``` r
pokemon_data =
  GET('https://pokeapi.co/api/v2/pokemon/ditto') %>% 
  content

pokemon_data$name
```

    ## [1] "ditto"

``` r
pokemon_data$height
```

    ## [1] 3

``` r
pokemon_data$abilities
```

    ## [[1]]
    ## [[1]]$ability
    ## [[1]]$ability$name
    ## [1] "limber"
    ## 
    ## [[1]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/7/"
    ## 
    ## 
    ## [[1]]$is_hidden
    ## [1] FALSE
    ## 
    ## [[1]]$slot
    ## [1] 1
    ## 
    ## 
    ## [[2]]
    ## [[2]]$ability
    ## [[2]]$ability$name
    ## [1] "imposter"
    ## 
    ## [[2]]$ability$url
    ## [1] "https://pokeapi.co/api/v2/ability/150/"
    ## 
    ## 
    ## [[2]]$is_hidden
    ## [1] TRUE
    ## 
    ## [[2]]$slot
    ## [1] 3

## Cloding thoughts
