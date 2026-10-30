# Count words, sentences, characters

Count words, sentences, and characters in input texts. These functions
use the `stringi` package, so they handle the counting of Unicode
strings (e.g., characters with diacritical marks) in a way that makes
sense to people counting characters.

## Usage

``` r
count_words(x)

count_characters(x)

count_sentences(x)
```

## Arguments

- x:

  A character vector or a list of character vectors. If `x` is a
  character vector, it can be of any length, and each element will be
  tokenized separately. If `x` is a list of character vectors, each
  element of the list should have a length of 1.

## Value

An integer vector containing the counted elements. If the input vector
or list has names, they will be preserved.

## Examples

``` r
count_words(mobydick)
#> mobydick 
#>   219415 
count_sentences(mobydick)
#> mobydick 
#>    29076 
count_characters(mobydick)
#> mobydick 
#>  1235185 
```
