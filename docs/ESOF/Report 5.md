Selected Feature
----------------
The implemented feature responds to a user request made in [issue number 11579](https://github.com/elastic/elasticsearch/issues/11579). regarding the [Term Suggester part of the REST API](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-suggesters-term.html), multiple users commented on a need for the system to give appropriate feedback as to whether an exact match to a term in the input was found in the documents. In its current state, given a result to a suggest query that returned no possible options, it is impossible to differentiate those that did so due the inexistence of any similar terms (similar terms are defined in relation to the max edit distance allowed, the default and max value of which is 2) from those those that found an exact match, but no inexact ones. In short, only terms with an edit distance of 1 or 2 are returned. This may be problematic for some users as the result of the query can be ambiguous as not enough information is returned.

Implementation
--------------
In order to maintain existing behaviour and avoid unexpected behaviour, the feature, dubbed Exact Matching, was implemented as an option, given in the HTTP request and turned off by default. It was based on existing options present in the Suggest API such as *max_edits* and *prefix_length*. In the example presented in the issue above, it would used as:

    GET /test_es_suggest/_suggest
    {
      "Suggest": {
          "term": {
            "field": "word",
            "suggest_mode": "popular",
            "size": 2,
            "prefix_len": 1,
            "analyzer": "default",
            "exact_matching": true
          },
          "text": "Software"
        }
    }

The result, is, as expected:

    "Suggest": [
          {
             "text": "software",
             "offset": 0,
             "length": 8,
             "options": [
                {
                   "text": "software",
                   "score": 1,
                   "freq": 1
                }
             ]
          }
       ]
It is immediately apparent that the term "software" is present in the system, where it would otherwise not be.

The use of an option, turned off by default, means that the changes made do not affect users that are unaware of or opt not to use it. The value of 1 in the *score* field distinctly marks those results that are a consequence of the change, allowing knowing users to use it appropriately and distinguish it from the default behaviour, as this value is impossible to achieve otherwise (being the similarity between the searched term and the options presented, which, by default, are never identical to the term itself).

For the Exact Matching itself, methods and classes from the Lucene library were primarily used.

An effort was made to retain the style of the existing codebase and the larger block of code was refactored and incapsulated in its own method so as to preserve the size and struture of the method in which the changes were originally made.

Edited files: TermSuggester.java, SuggestUtils.java, TermSuggestionBuilder.java, DirectSpellCheckerSettings.java
