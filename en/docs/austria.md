The OpenPLZ API data directory for [Austria](https://en.wikipedia.org/wiki/Austria) includes street names, postal codes, localities, and administrative divisions (municipalities, districts, and federal states).

## Administrative Structure

Austria's administrative structure is based on a federal system divided into multiple levels. Each level has clearly defined competencies and responsibilities regulated by the constitution.

**Federation (Bund)**

:   The highest administrative unit of the state. The federation has a central government and is responsible for overarching matters such as foreign policy, defense, and justice.

**Federal Provinces (Bundesländer)**

:   The federal units below the federation, consisting of 9 states. Each state has its own constitution, government, and state parliament. The states have independent competencies, particularly in areas such as education and culture.

**Districts (Bezirke)**

:   An intermediate administrative level between states and municipalities, consisting of political districts. Districts do not have legislative power but manage tasks exceeding municipal responsibilities. District administrative authorities are either district commissions (Bezirkshauptmannschaften) or magistrates in statutory cities.

**Municipalities (Gemeinden)**

:   The smallest administrative units with self-governing authority. There are around 2,000 municipalities in Austria. Each municipality has an elected local administration led by a mayor.

**Statutory Cities (Statutarstädte)**

:   Cities that fulfill the responsibilities of both a municipality and a district. Austria has 15 statutory cities, including Vienna, which is both a city and a federal state.

## Requesting Federal Provinces

The nine federal provinces of Austria can be queried through the following API endpoint:

!!! info ""
    
    **`openplzapi.org/at/FederalProvinces`**
    
    :    List of all federal provinces in Austria.

For each federal province, the following attributes are provided:

+ `key (string)`: Federal province code (1-digit)
+ `name (string)`: Name of the federal province

Example request for the complete list of federal provinces:

``` 
GET https://openplzapi.org/at/FederalProvinces
```

## Requesting Districts

Districts in Austria can be queried through the following API endpoint:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{stateCode}/Districts`**

    :    List of all districts within a federal province. A province code (1-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each district, the following attributes are provided:

+ `key (string)`: District code (3-digit)
+ `code (string)`: District coding (3-digit)
+ `name (string)`: Name of the district
+ `federalProvince.key (string)`: Province code (1-digit)
+ `federalProvince.name (string)`: Name of the federal province

Example request for districts in Vienna (Province Code: `7`)

```
GET https://openplzapi.org/at/FederalProvinces/7/Districts
```

## Requesting Municipalities

Municipalities in Austria can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{stateCode}/Municipalities`**

    :    List of all municipalities within a federal province. A province code (1-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/at/Districts/{districtCode}/Municipalities`**

    :    List of all municipalities within a district. A district code **or** district coding (both 3-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each municipality, the following attributes are provided:

+ `key (string)`: Municipality code (5-digit)
+ `code (string)`: Municipality coding (5-digit)
+ `name (string)`: Name of the municipality
+ `postalCode (string)`: Postal code of the municipal office
+ `multiplePostalCodes (bool)`: Does the municipality cover multiple postal codes?
+ `district.key (string)`: District code (3-digit)
+ `district.code (string)`: District coding (3-digit)
+ `district.name (string)`: Name of the district
+ `federalProvince.key (string)`: Province code (1-digit)
+ `federalProvince.name (string)`: Name of the federal province

Example request for municipalities in Vienna (Province Code: `7`)

```
GET https://openplzapi.org/at/FederalProvinces/7/Municipalities
```

## Requesting Postal Codes and Localities

Postal codes and localities in Austria can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{stateCode}/Localities`**

    :    List of all localities within a federal province. A province code (1-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/at/Districts/{districtCode}/Localities`**

    :    List of all localities within a district. A district code **or** district coding (both 3-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/at/Localities?postalCode={postalCode}&name={localityName}`**

    :    Searches for all localities that match the postal code and/or locality name. The parameters `postalCode` and `name` can be used together or independently. Both parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

For each locality, the following attributes are provided:

+ `key (string)`: Locality code
+ `name (string)`: Name of the locality
+ `postalcode (string)`: Postal code of the locality
+ `municipality.key (string)`: Municipality code (5-digit)
+ `municipality.code (string)`: Municipality coding (5-digit)
+ `municipality.name (string)`: Name of the municipality
+ `district.key (string)`: District code (3-digit)
+ `district.code (string)`: District coding (3-digit)
+ `district.name (string)`: Name of the district
+ `federalProvince.key (string)`: Province code (1-digit)
+ `federalProvince.name (string)`: Name of the federal province

Example request for postal code *1010*

```
GET https://openplzapi.org/at/Localities?postalCode=1010
```

Example request for all postal codes starting with *10*. The [regular expression](regex.md) `^10` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/at/Localities?postalCode=%5E10
```

## Requesting Streets

Streets in Austria can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/at/Streets?name={streetName}&postalCode={postalCode}&locality={localityName}`**

    :    Searches for all streets matching the street name and/or postal code and/or locality name. The parameters `name`, `postalCode`, and `locality` can be used together or independently. All three parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

    **`openplzapi.org/at/FullTextSearch?searchTerm={searchTerm}`**

    :    Searches for streets using [full-text search](fulltextsearch.md) across street name, postal code, and locality name. The query is subject to [paging](paging.md).

For each street, the following attributes are provided:

+ `key (string)`: Street code
+ `name (string)`: Name of the street
+ `postalcode (string)`: Postal code of the locality
+ `locality (string)`: Name of the locality
+ `municipality.key (string)`: Municipality code (5-digit)
+ `municipality.code (string)`: Municipality coding (5-digit)
+ `municipality.name (string)`: Name of the municipality
+ `district.key (string)`: District code (3-digit)
+ `district.code (string)`: District coding (3-digit)
+ `district.name (string)`: Name of the district
+ `federalProvince.key (string)`: Province code (1-digit)
+ `federalProvince.name (string)`: Name of the federal province

Example request for the street *Alexander-Poch-Platz*

```
GET https://openplzapi.org/at/Streets?name=Alexander-Poch-Platz
```

Example request for all streets in Vienna starting with *A* and ending with *Platz*. The [regular expression](regex.md) `^A.*Platz$` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/at/Streets?name=%5EA.%2APlatz%24&locality=Wien
```

Example full-text search with the term `Wien Alfred Dallinger Platz`. The search term is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/at/FullTextSearch?searchTerm=Wien%20Alfred%20Dallinger%20Platz
```