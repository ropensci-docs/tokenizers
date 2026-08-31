# Changelog

## tokenizers 0.3.0

CRAN release: 2022-12-22

- Remove the `tokenize_tweets()` function, which is no longer supported.

## tokenizers 0.2.3

CRAN release: 2022-09-23

- Bug fixes and performance enhancements.

## tokenizers 0.2.1

CRAN release: 2018-03-29

- Add citation information to JOSS paper.

## tokenizers 0.2.0

CRAN release: 2018-03-21

### Features

- Add the
  [`tokenize_ptb()`](https://docs.ropensci.org/tokenizers/reference/ptb-tokenizer.md)
  function for Penn Treebank tokenizations
  ([@jrnold](https://github.com/jrnold))
  ([\#12](https://github.com/ropensci/tokenizers/issues/12)).
- Add a function
  [`chunk_text()`](https://docs.ropensci.org/tokenizers/reference/chunk_text.md)
  to split long documents into pieces
  ([\#30](https://github.com/ropensci/tokenizers/issues/30)).
- New functions to count words, characters, and sentences without
  tokenization
  ([\#36](https://github.com/ropensci/tokenizers/issues/36)).
- New function `tokenize_tweets()` preserves usernames, hashtags, and
  URLS ([@kbenoit](https://github.com/kbenoit))
  ([\#44](https://github.com/ropensci/tokenizers/issues/44)).
- The [`stopwords()`](https://rdrr.io/pkg/stopwords/man/stopwords.html)
  function has been removed in favor of using the **stopwords** package
  ([\#46](https://github.com/ropensci/tokenizers/issues/46)).
- The package now complies with the basic recommendations of the **Text
  Interchange Format**. All tokenization functions are now methods. This
  enables them to take corpus inputs as either TIF-compliant named
  character vectors, named lists, or data frames. All outputs are still
  named lists of tokens, but these can be easily coerced to data frames
  of tokens using the `tif` package.
  ([\#49](https://github.com/ropensci/tokenizers/issues/49))
- Add a new vignette “The Text Interchange Formats and the tokenizers
  Package” ([\#49](https://github.com/ropensci/tokenizers/issues/49)).

### Bug fixes and performance improvements

- `tokenize_skip_ngrams` has been improved to generate unigrams and
  bigrams, according to the skip definition
  ([\#24](https://github.com/ropensci/tokenizers/issues/24)).
- C++98 has replaced the C++11 code used for n-gram generation, widening
  the range of compilers `tokenizers` supports
  ([@ironholds](https://github.com/ironholds))
  ([\#26](https://github.com/ropensci/tokenizers/issues/26)).
- `tokenize_skip_ngrams` now supports stopwords
  ([\#31](https://github.com/ropensci/tokenizers/issues/31)).
- If tokenisers fail to generate tokens for a particular entry, they
  return `NA` consistently
  ([\#33](https://github.com/ropensci/tokenizers/issues/33)).
- Keyboard interrupt checks have been added to Rcpp-backed functions to
  enable users to terminate them before completion
  ([\#37](https://github.com/ropensci/tokenizers/issues/37)).
- [`tokenize_words()`](https://docs.ropensci.org/tokenizers/reference/basic-tokenizers.md)
  gains arguments to preserve or strip punctuation and numbers
  ([\#48](https://github.com/ropensci/tokenizers/issues/48)).
- [`tokenize_skip_ngrams()`](https://docs.ropensci.org/tokenizers/reference/ngram-tokenizers.md)
  and
  [`tokenize_ngrams()`](https://docs.ropensci.org/tokenizers/reference/ngram-tokenizers.md)
  to return properly marked UTF8 strings on Windows
  ([@patperry](https://github.com/patperry))
  ([\#58](https://github.com/ropensci/tokenizers/issues/58)).
- `tokenize_tweets()` now removes stopwords prior to stripping
  punctuation, making its behavior more consistent with
  [`tokenize_words()`](https://docs.ropensci.org/tokenizers/reference/basic-tokenizers.md)
  ([\#76](https://github.com/ropensci/tokenizers/issues/76)).

## tokenizers 0.1.4

CRAN release: 2016-08-29

- Add the
  [`tokenize_character_shingles()`](https://docs.ropensci.org/tokenizers/reference/shingle-tokenizers.md)
  tokenizer.
- Improvements to documentation.

## tokenizers 0.1.3

CRAN release: 2016-08-18

- Add vignette.
- Improvements to n-gram tokenizers.

## tokenizers 0.1.2

CRAN release: 2016-04-14

- Add stopwords for several languages.
- New stopword options to
  [`tokenize_words()`](https://docs.ropensci.org/tokenizers/reference/basic-tokenizers.md)
  and
  [`tokenize_word_stems()`](https://docs.ropensci.org/tokenizers/reference/stem-tokenizers.md).

## tokenizers 0.1.1

CRAN release: 2016-04-04

- Fix failing test in non-UTF-8 locales.

## tokenizers 0.1.0

CRAN release: 2016-04-02

- Initial release with tokenizers for characters, words, word stems,
  sentences paragraphs, n-grams, skip n-grams, lines, and regular
  expressions.
