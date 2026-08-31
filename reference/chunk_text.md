# Chunk text into smaller segments

Given a text or vector/list of texts, break the texts into smaller
segments each with the same number of words. This allows you to treat a
very long document, such as a novel, as a set of smaller documents.

## Usage

``` r
chunk_text(x, chunk_size = 100, doc_id = names(x), ...)
```

## Arguments

- x:

  A character vector or a list of character vectors to be tokenized into
  n-grams. If `x` is a character vector, it can be of any length, and
  each element will be chunked separately. If `x` is a list of character
  vectors, each element of the list should have a length of 1.

- chunk_size:

  The number of words in each chunk.

- doc_id:

  The document IDs as a character vector. This will be taken from the
  names of the `x` vector if available. `NULL` is acceptable.

- ...:

  Arguments passed on to
  [`tokenize_words`](https://docs.ropensci.org/tokenizers/reference/basic-tokenizers.md).

## Details

Chunking the text passes it through
[`tokenize_words`](https://docs.ropensci.org/tokenizers/reference/basic-tokenizers.md),
which will strip punctuation and lowercase the text unless you provide
arguments to pass along to that function.

## Examples

``` r
if (FALSE) { # \dontrun{
chunked <- chunk_text(mobydick, chunk_size = 100)
length(chunked)
chunked[1:3]
} # }
```
