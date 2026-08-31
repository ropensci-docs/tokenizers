# The Text Interchange Formats and the tokenizers Package

The [Text Interchange Formats](https://github.com/ropenscilabs/tif) are
a set of standards defined at an [rOpenSci](https://ropensci.org/)
sponsored [meeting in London](https://textworkshop17.ropensci.org/) in
2017. The formats allow R text analysis packages to target defined
inputs and outputs for corpora, tokens, and document-term matrices. By
adhering to these recommendations, R packages can buy into an
interoperable ecosystem.

The TIF recommendations are still a draft, but the tokenizers package
implements its recommendation to accept both of the corpora formats and
to output one of its recommended tokens formats.

Consider these two recommended forms of a corpus. One (`corpus_c`) is a
named character vector; the other (`corpus_d`) is a data frame. They
both include a document ID and the full text for each item. The data
frame format obviously allows for the use of other metadata fields
besides the document ID, whereas the other format does not. Using the
coercion functions in the tif package, one could switch back and forth
between these formats. Tokenizers also supports a corpus formatted as a
named list where each element is a character vector of length one
(`corpus_l`), though this is not a part of the draft TIF standards.

``` r

# Named list
(corpus_l <- list(man_comes_around = "There's a man goin' 'round takin' names",
                  wont_back_down = "Well I won't back down, no I won't back down",
                  bird_on_a_wire = "Like a bird on a wire"))
#> $man_comes_around
#> [1] "There's a man goin' 'round takin' names"
#> 
#> $wont_back_down
#> [1] "Well I won't back down, no I won't back down"
#> 
#> $bird_on_a_wire
#> [1] "Like a bird on a wire"

# Named character vector
(corpus_c <- unlist(corpus_l))
#>                               man_comes_around 
#>      "There's a man goin' 'round takin' names" 
#>                                 wont_back_down 
#> "Well I won't back down, no I won't back down" 
#>                                 bird_on_a_wire 
#>                        "Like a bird on a wire"

# Data frame
(corpus_d <- data.frame(doc_id = names(corpus_c), text = unname(corpus_c),
                        stringsAsFactors = FALSE))
#>             doc_id                                         text
#> 1 man_comes_around      There's a man goin' 'round takin' names
#> 2   wont_back_down Well I won't back down, no I won't back down
#> 3   bird_on_a_wire                        Like a bird on a wire
```

All of the tokenizers in this package can accept any of those formats
and will return an identical output for each.

``` r

library(tokenizers)

tokens_l <- tokenize_ngrams(corpus_l, n = 2)
tokens_c <- tokenize_ngrams(corpus_c, n = 2)
tokens_d <- tokenize_ngrams(corpus_c, n = 2)

# Are all these identical?
all(identical(tokens_l, tokens_c),
    identical(tokens_c, tokens_d),
    identical(tokens_l, tokens_d))
#> [1] TRUE
```

The output of all of the tokenizers is a named list, where each element
of the list corresponds to a document in the corpus. The names of the
list are the document IDs, and the elements are character vectors
containing the tokens.

``` r

tokens_l
#> $man_comes_around
#> [1] "there's a"   "a man"       "man goin"    "goin round"  "round takin"
#> [6] "takin names"
#> 
#> $wont_back_down
#> [1] "well i"     "i won't"    "won't back" "back down"  "down no"   
#> [6] "no i"       "i won't"    "won't back" "back down" 
#> 
#> $bird_on_a_wire
#> [1] "like a"  "a bird"  "bird on" "on a"    "a wire"
```

This format can be coerced to a data frame of document IDs and tokens,
one row per token, using the coercion functions in the tif package. That
tokens data frame would look like this.

    #>              doc_id       token
    #> 1  man_comes_around   there's a
    #> 2  man_comes_around       a man
    #> 3  man_comes_around    man goin
    #> 4  man_comes_around  goin round
    #> 5  man_comes_around round takin
    #> 6  man_comes_around takin names
    #> 7    wont_back_down      well i
    #> 8    wont_back_down     i won't
    #> 9    wont_back_down  won't back
    #> 10   wont_back_down   back down
