# AutoComplete

N-Gram Model -> Languague Model -> predict suffix 

An n-gram is just a sequence of characters constructed by taking a substring of a given string. To understand why this is important, we need to talk about analyzers, tokenizers and token filters.

When you index documents with Elasticsearch, it uses them to build an inverted index. This is basically a dictionary containing a list of terms (a.k.a. "tokens"), together with references to the documents in which those terms appear. Each field in the mapping (whether the mapping is explicit or implicit) is associated with an "analyzer", and an analyzer consists of a "tokenizer" and zero or more "token filters." The analyzer is responsible for transforming the text of a given document field into the tokens in the lookup table used by the inverted index. When a text search is performed, the search text is also analyzed (usually), and the resulting tokens are compared against those in the inverted index; if matches are found, the referenced documents are returned.

For example, given the document above, if the "studio" field is analyzed using the standard analyzer (the default, when no analyzer is specified), then the text "Walt Disney Video" would be transformed into the tokens ["walt", "disney", "video"], and so a search for the term "disney" would match one of the terms listed for that document, and the document would be returned.

The "nGram" tokenizer and token filter can be used to generate tokens from substrings of the field value. There are edgeNGram versions of both, which only generate tokens that start at the beginning of words ("front") or end at the end of words ("back"). I will be using nGram token filter in my index analyzer below.
