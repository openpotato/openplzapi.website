# Full text search

For each country supported in the OpenPLZ API project there is a special API endpoint for **full text search**.

## What is full-text search?

Full-text search in relational databases allows text in one or more columns to be searched based on the actual meaning of the words rather than a simple string match. The aim is to return the most relevant results possible when searching for specific terms - similar to a search engine.

For example, a search for "Monchengladbach" will also return results for "Mönchengladbach". 

You can also enter the street, postal code and/or location in any order. The search entry 

```
Berlin Pariser Platz
```

returns the same result as

```
Pariser Platz, Berlin
```

## How exactly does the full-text search work?

We use the PostgreSQL full-text search in the background, more precisely the function [`websearch_to_tsquery`](https://www.postgresql.org/docs/current/textsearch-controls.html#TEXTSEARCH-PARSING-QUERIES). This function allows the input of unformatted text and converts it into the appropriate target format for PostgreSQL:

+ Text that is not in inverted commas is converted to terms separated by `&` operators, as when processed by `plainto_tsquery`.

+ Text in ‘inverted commas’ is converted into terms separated by `<->` operators, as if they were being processed by `phraseto_tsquery`.

+ An `OR` is converted to the `|` operator.

+ A hyphen `-` is converted into the operator `!`.

+ Other special characters, e.g. full stop, comma, exclamation mark etc. are ignored.

## Where can I find the full text search?

The following API endpoints allow a full text search via street name, postal code and location name:

+ `at/FullTextSearch`
+ `ch/FullTextSearch`
+ `de/FullTextSearch`
+ `li/FullTextSearch`

It's best just to try it out.
