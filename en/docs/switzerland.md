The OpenPLZ API data directory for [Switzerland](https://en.wikipedia.org/wiki/Switzerland) includes street names, postal codes, localities, and administrative divisions (communes, districts, and cantons).

## Administrative Structure

Switzerland's administrative structure is characterised by a strong federalist system. It is divided into three levels, each with distinct competencies and responsibilities.

**Confederation (Bund)**

:   The highest administrative unit of the Swiss federal state. The Confederation is responsible for overarching matters such as foreign policy, national defense, and the Swiss legal system. The legislature is formed by the Federal Assembly (National Council and Council of States), and the executive branch is led by the Federal Council.

**Cantons (Kantone)**

:   The federal units below the Confederation, consisting of 26 cantons (20 full cantons and 6 half-cantons). Each canton has its own constitution, government, parliament, and courts. Cantons have significant autonomy, particularly in education, healthcare, and policing.

**Communes (Gemeinden)**

:   The smallest administrative units with extensive self-governing authority. There are approximately 2,000 communes in Switzerland, though the number is steadily decreasing due to mergers. Communes manage local affairs such as spatial planning, schools, and water supply. They are governed by local authorities, typically including a local council and an administrative office.

## Requesting Cantons

The 26 Swiss cantons can be queried through the following API endpoint:

!!! info ""
    
    **`openplzapi.org/ch/Cantons`**
    
    :    List of all cantons in Switzerland.

For each canton, the following attributes are provided:

+ `key (string)`: Bfs code of the canton (max. 2 digits)
+ `historicalCode (string)`: Historical code of the canton
+ `name (string)`: Canton name
+ `shortName (string)`: Canton abbreviation (2 digits)

Example request for the complete list of cantons:

``` 
GET https://openplzapi.org/ch/Cantons
```

## Requesting Districts

Districts can be queried through the following API endpoint:

!!! info ""

    **`openplzapi.org/ch/Cantons/{cantonKey}/Districts`**

    :    List of all districts in a canton. The canton number (up to 2 digits) is required as a parameter. The query is subject to [paging](paging.md).

For each district, the following attributes are provided:

+ `key (string)`: Bfs code of the district (max. 4 digits)
+ `historicalCode (string)`: Historical code of the district
+ `name (string)`: District name
+ `shortName (string)`: District name, short
+ `canton.key (string)`: Bfs code of the canton (max. 2 digits)
+ `canton.name (string)`: Canton name
+ `canton.shortName (string)`: Canton abbreviation (2 digits)

Example request for districts in the canton of Fribourg (Canton Key: `10`):

```
GET https://openplzapi.org/ch/Cantons/10/Districts
```

## Requesting Communes

Communes can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/ch/Cantons/{cantonKey}/Communes`**

    :    List of all communes in a canton. The canton number (up to 2 digits) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/ch/Districts/{districtKey}/Communes`**

    :    List of all communes in a district. The district number (up to 4 digits) is required as a parameter. The query is subject to [paging](paging.md).

For each commune, the following attributes are provided:

+ `key (string)`: Bfs code of the commune (max. 4 digits)
+ `historicalCode (string)`: Historical code of the commune
+ `name (string)`: Official commune name
+ `shortName (string)`: Commune name, short
+ `district.key (string)`: Bfs code of the district (max. 4 digits)
+ `district.name (string)`: District name
+ `district.shortName (string)`: District name, short
+ `canton.key (string)`: Bfs code of the canton (max. 2 digits)
+ `canton.name (string)`: Canton name
+ `canton.shortName (string)`: Canton abbreviation (2 digits)

Example request for communes in the canton of Fribourg (Canton Key: `10`):

```
GET https://openplzapi.org/ch/Cantons/10/Communes
```

## Requesting Postal Codes and Localities

Postal codes and localities can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/ch/Cantons/{cantonKey}/Localities`**

    :    List of all localities in a canton. The canton number (up to 2 digits) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/ch/Districts/{districtKey}/Localities`**

    :    List of all localities in a district. The district number (up to 4 digits) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/ch/Localities?postalCode={postalCode}&name={localityName}`**

    :    Searches for all localities that match the postal code and/or locality name. The parameters `postalCode` and `name` can be used together or independently. Both parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

For each locality, the following attributes are provided:

+ `key (string)`: Locality code
+ `name (string)`: Locality name
+ `postalcode (string)`: Postal code of the locality
+ `commune.key (string)`: Bfs code of the commune (max. 4 digits)
+ `commune.name (string)`: Official commune name
+ `commune.shortName (string)`: Commune name, short
+ `district.key (string)`: Bfs code of the district (max. 4 digits)
+ `district.name (string)`: District name
+ `district.shortName (string)`: District name, short
+ `canton.key (string)`: Bfs code of the canton (max. 2 digits)
+ `canton.name (string)`: Canton name
+ `canton.shortName (string)`: Canton abbreviation (2 digits)

Example request for postal code *8001*:

```
GET https://openplzapi.org/ch/Localities?postalCode=8001
```

Example request for all Swiss postal codes starting with *80*. The regular expression `^80` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/ch/Localities?postalCode=%5E80
```

## Requesting Streets

Streets can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/ch/Streets?name={streetName}&postalCode={postalCode}&locality={localityName}`**

    :    Searches for all streets matching the street name and/or postal code and/or locality name. The parameters `name`, `postalCode`, and `locality` can be used together or independently. All three parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

    **`openplzapi.org/ch/FullTextSearch?searchTerm={searchTerm}`**

    :    Searches for streets using [full-text search](fulltextsearch.md) across street name, postal code, and locality name. The query is subject to [paging](paging.md).

For each street, the following attributes are provided:

+ `key (string)`: Street key
+ `name (string)`: Street name
+ `status (string)`: Street status. Possible values:
    + `Planned`
    + `Real`
    + `Outdated`
+ `postalcode (string)`: Postal code of the locality
+ `locality (string)`: Locality name
+ `commune.key (string)`: Bfs code of the commune (max. 4 digits)
+ `commune.name (string)`: Official commune name
+ `commune.shortName (string)`: Commune name, short
+ `district.key (string)`: Bfs code of the district (max. 4 digits)
+ `district.name (string)`: District name
+ `district.shortName (string)`: District name, short
+ `canton.key (string)`: Bfs code of the canton (max. 2 digits)
+ `canton.name (string)`: Canton name
+ `canton.shortName (string)`: Canton abbreviation (2 digits)

Example request for the street *Bederstrasse* (unique in Zurich):

```
GET https://openplzapi.org/ch/Streets?name=Bederstrasse
```

Example request for all streets in Zurich starting with *B* and ending with *strasse*. The regular expression `^B.*strasse$` is [URL-encoded](url-encoding.md):


```
GET https://openplzapi.org/ch/Streets?name=%5EB.*strasse%24&locality=Z%C3%BCrich
```

Example full-text search with the term `Zürich Bederstrasse`. The search term is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/ch/FullTextSearch?searchTerm=Z%C3%BCrich%20Bederstrasse
```