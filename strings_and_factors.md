Strings and Factors
================

``` r
string_vec = c("my", "name", "is", "anderson")

str_detect(string_vec, 'a')
```

    ## [1] FALSE  TRUE FALSE  TRUE

``` r
str_detect(string_vec, 'anderson')  #detect whether every observations in string_vec has anderson
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
str_replace(string_vec, 'anderson', 'Anderson') #replace the second argument with the third argument
```

    ## [1] "my"       "name"     "is"       "Anderson"

``` r
string_vec = c(
  "i think we all rule for participating",
  "i think i have been caught",
  "i think this will be quite fun actually",
  "it will be fun, i think"
  )

str_detect(string_vec, 'i think')
```

    ## [1] TRUE TRUE TRUE TRUE

``` r
str_detect(string_vec, '^i think')  # detect whether 'i think' is in the beginning of observation
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
str_detect(string_vec, 'i think$')  # detect whether 'i think' is in the end of observation
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
string_vec = c(
  "Y'all remember Pres. HW Bush?",
  "I saw a green bush",
  "BBQ and Bushwalking at Molonglo Gorge",
  "BUSH -- LIVE IN CONCERT!!"
  )

str_detect(string_vec, '[Bb]ush')  #both thing in bracket are ok to match
```

    ## [1]  TRUE  TRUE  TRUE FALSE

``` r
string_vec = c(
  '7th inning stretch',
  '1st half soon to begin. Texas won the toss.',
  'she is 5 feet 4 inches tall',
  '3AM - cant sleep :('
  )

str_detect(string_vec, '^[0-9][a-zA-Z]')
```

    ## [1]  TRUE  TRUE FALSE  TRUE

``` r
string_vec = c(
  'Its 7:11 in the evening',
  'want to go to 7-11?',
  'my flight is AA711',
  'NetBios: scanning ip 203.167.114.66'
  )

str_detect(string_vec, '7.11')  # the dot matchs everything 
```

    ## [1]  TRUE  TRUE FALSE  TRUE

``` r
str_detect(string_vec, '7\\.11') # let regular expression know that i want the literate dot not special character.
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
string_vec = c(
  'The CI is [2, 5]',
  ':-]',
  ':-[',
  'I found the answer on pages [6-7]' 
  )

str_detect(string_vec, '\\[')
```

    ## [1]  TRUE FALSE  TRUE  TRUE

## Factors

``` r
factor_vec = factor(c("male", "male", "female", "female"))

factor_vec
```

    ## [1] male   male   female female
    ## Levels: female male

``` r
as.numeric(factor_vec)
```

    ## [1] 2 2 1 1

What happen if i relevel …

``` r
factor_vec = fct_relevel(factor_vec, 'male')

factor_vec
```

    ## [1] male   male   female female
    ## Levels: male female

``` r
as.numeric(factor_vec)
```

    ## [1] 1 1 2 2
