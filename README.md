# Place Adjectives and Demonyms handling for Solr and Lucene

The goal of this project is to implement libraries for accurate handling of place adjectives and demonyms 
for applications that use Lucene or Lucene-based search systems like Solr and ElasticSearch.

## What are Place Adjectives and Demonyms?

**Place Adjectives** are adjectival forms of place names, used in sentences to indicate something *of that place*. 
For example, *Australian* for *Australia* is used in a sentence like *"The Australian weather is wonderful."*

**Demonyms** are words used for people of a certain nationality or ethnicity, like *Americans*, *Indians*, or *Italians*.

Sometimes, place adjectives and demonyms are the same - for example, *Australian* - and sometimes different - 
for example, *Swedish* and *Swedes*.

Read these articles for more information on these concepts:

- [Wikipedia article on Demonyms](https://en.wikipedia.org/wiki/Demonym) 

- [Wikipedia article on Adjectival and Demonymic forms of place names](https://en.wikipedia.org/wiki/List_of_adjectival_and_demonymic_forms_of_place_names)


## What problems does this project solve?

- Applications sometimes want to map place adjectives or demonyms in search queries to their related places, or vice versa.

  For example, a search query with an place adjective, like *"swedish history"*, should match a title like *"A History of Sweden"*.
  
  Conversely, a search query with a place, like *"sweden history"*, should match a title like *"A History of medieval Swedish people"*.
    
  The former is a *stemming* operation, while the latter is more of a synonimizing operation.

- Unfortunately, popular English stemmers don't handle this mapping well. KStemmer is the only one that handles some cases, 
  but not all. Some examples:
  
  | *word* | Porter | KStemmer | English minimal | Hunspell | Snowball |
  | --- | --- | --- | --- | --- | --- |
  | swedish | :no_entry_sign: swedish | :white_check_mark: sweden | :no_entry_sign: swedish | :no_entry_sign: swedish | :no_entry_sign: swedish |
  | welsh | :no_entry_sign: welsh | :no_entry_sign: welsh | :no_entry_sign: welsh | :no_entry_sign: welsh | :no_entry_sign: welsh | 
  | indian | :no_entry_sign: indian | :no_entry_sign: indian | :no_entry_sign: indian | :no_entry_sign: indian | :no_entry_sign: indian | 
  | american | :no_entry_sign: american | :white_check_mark: america | :no_entry_sign: american | :no_entry_sign: american | :no_entry_sign: american | 
  | british | :no_entry_sign: british | :white_check_mark: britain | :no_entry_sign: british | :no_entry_sign: british | :no_entry_sign: british | 
  
  None of them support the reverse operation - mapping place names to their adjectives or demonyms.
