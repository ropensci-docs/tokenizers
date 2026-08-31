# Penn Treebank Tokenizer

This function implements the Penn Treebank word tokenizer.

## Usage

``` r
tokenize_ptb(x, lowercase = FALSE, simplify = FALSE)
```

## Arguments

- x:

  A character vector or a list of character vectors to be tokenized into
  n-grams. If `x` is a character vector, it can be of any length, and
  each element will be tokenized separately. If `x` is a list of
  character vectors, each element of the list should have a length of 1.

- lowercase:

  Should the tokens be made lower case?

- simplify:

  `FALSE` by default so that a consistent value is returned regardless
  of length of input. If `TRUE`, then an input with a single element
  will return a character vector of tokens instead of a list.

## Value

A list of character vectors containing the tokens, with one element in
the list for each element that was passed as input. If `simplify = TRUE`
and only a single element was passed as input, then the output is a
character vector of tokens.

## Details

This tokenizer uses regular expressions to tokenize text similar to the
tokenization used in the Penn Treebank. It assumes that text has already
been split into sentences. The tokenizer does the following:

- splits common English contractions, e.g. `don't` is tokenized into
  `do n't` and `they'll` is tokenized into -\> `they 'll`,

- handles punctuation characters as separate tokens,

- splits commas and single quotes off from words, when they are followed
  by whitespace,

- splits off periods that occur at the end of the sentence.

This function is a port of the Python NLTK version of the Penn Treebank
Tokenizer.

## References

[NLTK
TreebankWordTokenizer](https://www.nltk.org/_modules/nltk/tokenize/treebank.html#TreebankWordTokenizer)

## Examples

``` r
song <- list(paste0("How many roads must a man walk down\n",
                    "Before you call him a man?"),
             paste0("How many seas must a white dove sail\n",
                    "Before she sleeps in the sand?\n"),
             paste0("How many times must the cannonballs fly\n",
                    "Before they're forever banned?\n"),
             "The answer, my friend, is blowin' in the wind.",
             "The answer is blowin' in the wind.")
tokenize_ptb(song)
#> [[1]]
#>  [1] "How"    "many"   "roads"  "must"   "a"      "man"    "walk"   "down"  
#>  [9] "Before" "you"    "call"   "him"    "a"      "man"    "?"     
#> 
#> [[2]]
#>  [1] "How"    "many"   "seas"   "must"   "a"      "white"  "dove"   "sail"  
#>  [9] "Before" "she"    "sleeps" "in"     "the"    "sand"   "?"     
#> 
#> [[3]]
#>  [1] "How"         "many"        "times"       "must"        "the"        
#>  [6] "cannonballs" "fly"         "Before"      "they"        "'re"        
#> [11] "forever"     "banned"      "?"          
#> 
#> [[4]]
#>  [1] "The"    "answer" ","      "my"     "friend" ","      "is"     "blowin"
#>  [9] "'"      "in"     "the"    "wind"   "."     
#> 
#> [[5]]
#> [1] "The"    "answer" "is"     "blowin" "'"      "in"     "the"    "wind"  
#> [9] "."     
#> 
tokenize_ptb(c("Good muffins cost $3.88\nin New York. Please buy me\ntwo of them.",
  "They'll save and invest more.",
  "Hi, I can't say hello."))
#> [[1]]
#>  [1] "Good"    "muffins" "cost"    "$"       "3.88"    "in"      "New"    
#>  [8] "York."   "Please"  "buy"     "me"      "two"     "of"      "them"   
#> [15] "."      
#> 
#> [[2]]
#> [1] "They"   "'ll"    "save"   "and"    "invest" "more"   "."     
#> 
#> [[3]]
#> [1] "Hi"    ","     "I"     "ca"    "n't"   "say"   "hello" "."    
#> 
```
