The OpenPLZ API data directory for [Liechtenstein](https://en.wikipedia.org/wiki/Liechtenstein) includes street names, postal codes, localities, and administrative divisions (municipalities).

## Administrative Structure

Liechtenstein's administrative structure is straightforward, reflecting the small size of the state. It consists of a few, manageable levels, centrally organised.

**Principality (Fürstentum)**

:   The state of Liechtenstein as the highest administrative unit and sovereign entity. Liechtenstein is a constitutional hereditary monarchy based on democratic and parliamentary principles. The state is governed by the Prince and the government.

**Municipalities (Gemeinden)**

:   The only subordinate administrative level, consisting of 11 municipalities. Municipalities are responsible for local administration and have competencies in areas such as construction and infrastructure. Each municipality is represented by a municipal council and a mayor.

**Regions (historical context)**

:   Informal groupings of municipalities that do not constitute an official administrative level. Traditionally, Liechtenstein is divided into two historical regions—Oberland and Unterland—which hold no administrative significance.

## Requesting Municipalities

The 11 municipalities of Liechtenstein can be queried through the following API endpoint:

!!! info ""
    
    **`openplzapi.org/li/Communes`**
    
    :    List of all municipalities in Liechtenstein.

For each municipality, the following attributes are provided:

+ `key (string)`: Municipality number (4-digit)
+ `name (string)`: Official name of the municipality
+ `electoralDistrict (string)`: Name of the electoral district. Possible values:
    + `Oberland` 
    + `Unterland`

Example request for all municipalities:

``` 
GET https://openplzapi.org/li/Communes
```

## Requesting Postal Codes and Localities

Postal codes and localities can be queried through the following API endpoint:

!!! info ""

    **`openplzapi.org/li/Localities?postalCode={postal code}&name={locality name}`**

    :    Searches for all localities matching the postal code and/or locality name. The parameters `postalCode` and `name` can be used together or independently. Both parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

For each locality, the following attributes are provided:

+ `name (string)`: Name of the locality
+ `postalcode (string)`: Postal code of the locality
+ `commune.key (string)`: Municipality number (4-digit)
+ `commune.name (string)`: Official name of the municipality

Example request for postal code *9490*:

```
GET https://openplzapi.org/li/Localities?postalCode=9490
```

Example request for all postal codes starting with *94*. The [regular expression](regex.md) `^94` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/li/Localities?postalCode=%5E94
```

## Requesting Streets

Streets can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/li/Streets?name={street name}&postalCode={postal code}&locality={locality name}`**

    :    Searches for all streets matching the street name and/or postal code and/or locality name. The parameters `name`, `postalCode`, and `locality` can be used together or independently. All three parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

    **`openplzapi.org/li/FullTextSearch?searchTerm={search term}`**

    :    Searches for streets using [full-text search](fulltextsearch.md) across street name, postal code, and locality name. The query is subject to [paging](paging.md).

For each street, the following attributes are provided:

+ `key (string)`: Street key
+ `name (string)`: Name of the street
+ `status (string)`: Street status. Possible values:
    + `Planned`
    + `Real`
    + `Outdated`
+ `postalcode (string)`: Postal code of the locality
+ `locality (string)`: Name of the locality
+ `commune.key (string)`: Municipality number (4-digit)
+ `commune.name (string)`: Official name of the municipality

Example request for the street *Alte Landstrasse*:

```
GET https://openplzapi.org/li/Streets?name=Alte%20Landstrasse
```

Example request for all streets in Vaduz starting with *Alte* and ending with *strasse*. The [regular expression](regex.md) `^Alte.*strasse$` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/li/Streets?name=%5EAlte.%2Astrasse%24&locality=Vaduz
```

Example full-text search with the term `Vaduz Alte Landstrasse`. The search term is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/li/FullTextSearch?searchTerm=Vaduz%20Alte%20Landstrasse
```