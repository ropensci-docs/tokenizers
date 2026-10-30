# Basic tokenizers

These functions perform basic tokenization into words, sentences,
paragraphs, lines, and characters. The functions can be piped into one
another to create at most two levels of tokenization. For instance, one
might split a text into paragraphs and then word tokens, or into
sentences and then word tokens.

## Usage

``` r
tokenize_characters(
  x,
  lowercase = TRUE,
  strip_non_alphanum = TRUE,
  simplify = FALSE
)

tokenize_words(
  x,
  lowercase = TRUE,
  stopwords = NULL,
  strip_punct = TRUE,
  strip_numeric = FALSE,
  simplify = FALSE
)

tokenize_sentences(x, lowercase = FALSE, strip_punct = FALSE, simplify = FALSE)

tokenize_lines(x, simplify = FALSE)

tokenize_paragraphs(x, paragraph_break = "\n\n", simplify = FALSE)

tokenize_regex(x, pattern = "\\s+", simplify = FALSE)
```

## Arguments

- x:

  A character vector or a list of character vectors to be tokenized. If
  `x` is a character vector, it can be of any length, and each element
  will be tokenized separately. If `x` is a list of character vectors,
  where each element of the list should have a length of 1.

- lowercase:

  Should the tokens be made lower case? The default value varies by
  tokenizer; it is only `TRUE` by default for the tokenizers that you
  are likely to use last.

- strip_non_alphanum:

  Should punctuation and white space be stripped?

- simplify:

  `FALSE` by default so that a consistent value is returned regardless
  of length of input. If `TRUE`, then an input with a single element
  will return a character vector of tokens instead of a list.

- stopwords:

  A character vector of stop words to be excluded.

- strip_punct:

  Should punctuation be stripped?

- strip_numeric:

  Should numbers be stripped?

- paragraph_break:

  A string identifying the boundary between two paragraphs.

- pattern:

  A regular expression that defines the split.

## Value

A list of character vectors containing the tokens, with one element in
the list for each element that was passed as input. If `simplify = TRUE`
and only a single element was passed as input, then the output is a
character vector of tokens.

## Examples

``` r
song <-  paste0("How many roads must a man walk down\n",
                "Before you call him a man?\n",
                "How many seas must a white dove sail\n",
                "Before she sleeps in the sand?\n",
                "\n",
                "How many times must the cannonballs fly\n",
                "Before they're forever banned?\n",
                "The answer, my friend, is blowin' in the wind.\n",
                "The answer is blowin' in the wind.\n")

tokenize_words(song)
#> [[1]]
#>  [1] "how"         "many"        "roads"       "must"        "a"          
#>  [6] "man"         "walk"        "down"        "before"      "you"        
#> [11] "call"        "him"         "a"           "man"         "how"        
#> [16] "many"        "seas"        "must"        "a"           "white"      
#> [21] "dove"        "sail"        "before"      "she"         "sleeps"     
#> [26] "in"          "the"         "sand"        "how"         "many"       
#> [31] "times"       "must"        "the"         "cannonballs" "fly"        
#> [36] "before"      "they're"     "forever"     "banned"      "the"        
#> [41] "answer"      "my"          "friend"      "is"          "blowin"     
#> [46] "in"          "the"         "wind"        "the"         "answer"     
#> [51] "is"          "blowin"      "in"          "the"         "wind"       
#> 
tokenize_words(song, strip_punct = FALSE)
#> [[1]]
#>  [1] "how"         "many"        "roads"       "must"        "a"          
#>  [6] "man"         "walk"        "down"        "before"      "you"        
#> [11] "call"        "him"         "a"           "man"         "?"          
#> [16] "how"         "many"        "seas"        "must"        "a"          
#> [21] "white"       "dove"        "sail"        "before"      "she"        
#> [26] "sleeps"      "in"          "the"         "sand"        "?"          
#> [31] "how"         "many"        "times"       "must"        "the"        
#> [36] "cannonballs" "fly"         "before"      "they're"     "forever"    
#> [41] "banned"      "?"           "the"         "answer"      ","          
#> [46] "my"          "friend"      ","           "is"          "blowin"     
#> [51] "'"           "in"          "the"         "wind"        "."          
#> [56] "the"         "answer"      "is"          "blowin"      "'"          
#> [61] "in"          "the"         "wind"        "."          
#> 
tokenize_sentences(song)
#> [[1]]
#> [1] "How many roads must a man walk down Before you call him a man?"        
#> [2] "How many seas must a white dove sail Before she sleeps in the sand?"   
#> [3] "How many times must the cannonballs fly Before they're forever banned?"
#> [4] "The answer, my friend, is blowin' in the wind."                        
#> [5] "The answer is blowin' in the wind."                                    
#> 
tokenize_paragraphs(song)
#> [[1]]
#> [1] "How many roads must a man walk down Before you call him a man? How many seas must a white dove sail Before she sleeps in the sand?"                       
#> [2] "How many times must the cannonballs fly Before they're forever banned? The answer, my friend, is blowin' in the wind. The answer is blowin' in the wind. "
#> 
tokenize_lines(song)
#> [[1]]
#> [1] "How many roads must a man walk down"           
#> [2] "Before you call him a man?"                    
#> [3] "How many seas must a white dove sail"          
#> [4] "Before she sleeps in the sand?"                
#> [5] "How many times must the cannonballs fly"       
#> [6] "Before they're forever banned?"                
#> [7] "The answer, my friend, is blowin' in the wind."
#> [8] "The answer is blowin' in the wind."            
#> 
tokenize_characters(song)
#> [[1]]
#>   [1] "h" "o" "w" "m" "a" "n" "y" "r" "o" "a" "d" "s" "m" "u" "s" "t" "a" "m"
#>  [19] "a" "n" "w" "a" "l" "k" "d" "o" "w" "n" "b" "e" "f" "o" "r" "e" "y" "o"
#>  [37] "u" "c" "a" "l" "l" "h" "i" "m" "a" "m" "a" "n" "h" "o" "w" "m" "a" "n"
#>  [55] "y" "s" "e" "a" "s" "m" "u" "s" "t" "a" "w" "h" "i" "t" "e" "d" "o" "v"
#>  [73] "e" "s" "a" "i" "l" "b" "e" "f" "o" "r" "e" "s" "h" "e" "s" "l" "e" "e"
#>  [91] "p" "s" "i" "n" "t" "h" "e" "s" "a" "n" "d" "h" "o" "w" "m" "a" "n" "y"
#> [109] "t" "i" "m" "e" "s" "m" "u" "s" "t" "t" "h" "e" "c" "a" "n" "n" "o" "n"
#> [127] "b" "a" "l" "l" "s" "f" "l" "y" "b" "e" "f" "o" "r" "e" "t" "h" "e" "y"
#> [145] "r" "e" "f" "o" "r" "e" "v" "e" "r" "b" "a" "n" "n" "e" "d" "t" "h" "e"
#> [163] "a" "n" "s" "w" "e" "r" "m" "y" "f" "r" "i" "e" "n" "d" "i" "s" "b" "l"
#> [181] "o" "w" "i" "n" "i" "n" "t" "h" "e" "w" "i" "n" "d" "t" "h" "e" "a" "n"
#> [199] "s" "w" "e" "r" "i" "s" "b" "l" "o" "w" "i" "n" "i" "n" "t" "h" "e" "w"
#> [217] "i" "n" "d"
#> 
```
