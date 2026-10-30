# Character shingle tokenizers

The character shingle tokenizer functions like an n-gram tokenizer,
except the units that are shingled are characters instead of words.
Options to the function let you determine whether non-alphanumeric
characters like punctuation should be retained or discarded.

## Usage

``` r
tokenize_character_shingles(
  x,
  n = 3L,
  n_min = n,
  lowercase = TRUE,
  strip_non_alphanum = TRUE,
  simplify = FALSE
)
```

## Arguments

- x:

  A character vector or a list of character vectors to be tokenized into
  character shingles. If `x` is a character vector, it can be of any
  length, and each element will be tokenized separately. If `x` is a
  list of character vectors, each element of the list should have a
  length of 1.

- n:

  The number of characters in each shingle. This must be an integer
  greater than or equal to 1.

- n_min:

  This must be an integer greater than or equal to 1, and less than or
  equal to `n`.

- lowercase:

  Should the characters be made lower case?

- strip_non_alphanum:

  Should punctuation and white space be stripped?

- simplify:

  `FALSE` by default so that a consistent value is returned regardless
  of length of input. If `TRUE`, then an input with a single element
  will return a character vector of tokens instead of a list.

## Value

A list of character vectors containing the tokens, with one element in
the list for each element that was passed as input. If `simplify = TRUE`
and only a single element was passed as input, then the output is a
character vector of tokens.

## Examples

``` r
x <- c("Now is the hour of our discontent")
tokenize_character_shingles(x)
#> [[1]]
#>  [1] "now" "owi" "wis" "ist" "sth" "the" "heh" "eho" "hou" "our" "uro" "rof"
#> [13] "ofo" "fou" "our" "urd" "rdi" "dis" "isc" "sco" "con" "ont" "nte" "ten"
#> [25] "ent"
#> 
tokenize_character_shingles(x, n = 5)
#> [[1]]
#>  [1] "nowis" "owist" "wisth" "isthe" "stheh" "theho" "hehou" "ehour" "houro"
#> [10] "ourof" "urofo" "rofou" "ofour" "fourd" "ourdi" "urdis" "rdisc" "disco"
#> [19] "iscon" "scont" "conte" "onten" "ntent"
#> 
tokenize_character_shingles(x, n = 5, strip_non_alphanum = FALSE)
#> [[1]]
#>  [1] "now i" "ow is" "w is " " is t" "is th" "s the" " the " "the h" "he ho"
#> [10] "e hou" " hour" "hour " "our o" "ur of" "r of " " of o" "of ou" "f our"
#> [19] " our " "our d" "ur di" "r dis" " disc" "disco" "iscon" "scont" "conte"
#> [28] "onten" "ntent"
#> 
tokenize_character_shingles(x, n = 5, n_min = 3, strip_non_alphanum = FALSE)
#> [[1]]
#>  [1] "now"   "now "  "now i" "ow "   "ow i"  "ow is" "w i"   "w is"  "w is "
#> [10] " is"   " is "  " is t" "is "   "is t"  "is th" "s t"   "s th"  "s the"
#> [19] " th"   " the"  " the " "the"   "the "  "the h" "he "   "he h"  "he ho"
#> [28] "e h"   "e ho"  "e hou" " ho"   " hou"  " hour" "hou"   "hour"  "hour "
#> [37] "our"   "our "  "our o" "ur "   "ur o"  "ur of" "r o"   "r of"  "r of "
#> [46] " of"   " of "  " of o" "of "   "of o"  "of ou" "f o"   "f ou"  "f our"
#> [55] " ou"   " our"  " our " "our"   "our "  "our d" "ur "   "ur d"  "ur di"
#> [64] "r d"   "r di"  "r dis" " di"   " dis"  " disc" "dis"   "disc"  "disco"
#> [73] "isc"   "isco"  "iscon" "sco"   "scon"  "scont" "con"   "cont"  "conte"
#> [82] "ont"   "onte"  "onten" "nte"   "nten"  "ntent" "ten"   "tent"  "ent"  
#> 
```
