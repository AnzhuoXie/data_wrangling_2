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
