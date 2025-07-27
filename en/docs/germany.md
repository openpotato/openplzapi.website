The OpenPLZ API data directory for [Germany](https://en.wikipedia.org/wiki/Germany) includes street names, postal codes, localities, and administrative divisions (municipalities, municipal associations, districts, government regions, and federal states).

## Administrative Structure

Germany's administrative structure is based on a federal system governed by the Basic Law (Grundgesetz). It is divided into several levels, each with specific competencies and responsibilities.

**Federation (Bund)**

:   The highest level of administration and legislation in Germany. The federation is responsible for overarching matters such as foreign policy, defense, and monetary order. Legislation is carried out by the Bundestag and Bundesrat, while the executive branch is headed by the federal government.

**Federal States (Bundesländer)**

:   The federal units below the federation, consisting of 16 federal states. Each state has its own constitution, government, and state parliament. The states have exclusive competencies, particularly in areas such as education, police, and cultural affairs.

**Government Regions (Regierungsbezirke)**

:   A middle level of administration positioned between the state and district levels in some federal states. Government regions exist in only four of the 16 federal states and primarily coordinate state administration. They do not have independent legislative powers.

**Districts (Kreise)**

:   A municipal administrative unit between government regions (where applicable) and municipalities.
    
    The main types of districts:
    
    + Rural districts (Landkreise)
    + Urban districts (kreisfreie Städte), which perform the functions of both districts and municipalities.

**Municipalities (Gemeinden)**

:   The smallest administrative units with extensive self-governing rights. Municipalities are responsible for local administration and are led by an elected municipal council and usually a mayor.

**Municipal Associations (Gemeindeverbände)**

:   Associations of municipalities formed to jointly carry out specific tasks. Municipal associations, such as administrative communities or special-purpose associations, are typically limited to particular administrative functions.

## Requesting Federal States

The 16 federal states of Germany can be queried through the following API endpoint:

!!! info ""
    
    **`openplzapi.org/de/FederalStates`**
    
    :    List of all federal states in Germany.

For each federal state, the following attributes are provided:

+ `key (string)`: Regional code (2-digit)
+ `name (string)`: Name of the federal state
+ `seatOfGovernment (string)`: Seat of government of the federal state

Example reqeust for the complete list of federal states:

``` 
GET https://openplzapi.org/de/FederalStates
```

## Requesting Government Regions

Government regions can be queried through the following API endpoint:

!!! info ""

    **`openplzapi.org/de/FederalStates/{stateCode}/GovernmentRegions`**

    :    List of all government regions within a federal state. A state code (2-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each government region, the following attributes are provided:

+ `key (string)`: Regional code (3-digit)
+ `name (string)`: Name of the government region
+ `administrativeHeadquarters (string)`: Administrative headquarters of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

!!! note "Government Regions"

    Please note that government regions exist only in four federal states: **Baden-Württemberg**, **Bavaria**, **Hesse**, and **North Rhine-Westphalia**. In **Lower Saxony**, **Rhineland-Palatinate**, and **Saxony**, government regions have been officially abolished but are still included in the municipal directory for statistical purposes and can therefore be queried here.

Example request for government tegions in Bavaria (State Code: `09`)

```
GET https://openplzapi.org/de/FederalStates/09/GovernmentRegions
```

## Requesting Districts

Districts can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/de/FederalStates/{stateCode}/Districts`**

    :    List of all districts within a federal state. A state code (2-digit) is required as a parameter. The query is subject to [paging](paging.md).
  
    **`openplzapi.org/de/GovernmentRegions/{regionCode}/Districts`**

    :    List of all districts within a government region. A region code (3-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each district, the following attributes are provided:

+ `key (string)`: Regional code (5-digit)
+ `name (string)`: Name of the district
+ `type (string)`: Type of the district. Possible values:
    + `Kreisfreie Stadt` (urban district)
    + `Stadtkreis` (city district)
    + `Kreis` (district)
    + `Landkreis` (rural district)
    + `Regionalverband` (regional association)
+ `administrativeHeadquarters (string)`: Administrative headquarters of the district
+ `governmentRegion.key (string)`: Regional code of the government region (3-digit)
+ `governmentRegion.name (string)`: Name of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

Example request for districts in Rhineland-Palatinate (State Code: `07`)

```
GET https://openplzapi.org/de/FederalStates/07/Districts
```

## Requesting Municipalities

Municipalities can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/de/FederalStates/{stateCode}/Municipalites`**

    :    List of all municipalities within a federal state. A state code (2-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{regionCode}/Municipalites`**

    :    List of all municipalities within a government region. A region code (3-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/Districts/{districtCode}/Municipalites`**

    :    List of all municipalities within a district. A district code (5-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each municipality, the following attributes are provided:

+ `key (string)`: Regional code (8-digit)
+ `name (string)`: Name of the municipality
+ `type (string)`: Type of the municipality. Possible values:
    + `Markt` (market town)
    + `Kreisfreie Stadt` (urban district)
    + `Stadtkreis` (city district)
    + `Stadt` (town)
    + `Kreisangehörige Gemeinde` (municipality within a district)
    + `Gemeindefreies Gebiet (bewohnt)` (unincorporated area, inhabited)
    + `Gemeindefreies Gebiet (unbewohnt)` (unincorporated area, uninhabited)
    + `Große Kreisstadt` (large district town)
+ `postalCode (string)`: Postal code of the administrative seat (if multiple postal codes exist)
+ `multiplePostalCodes (bool)`: Does the municipality include more than one postal code?
+ `association.key (string)`: Combination of the district regional code and the municipal association key (9-digit)
+ `association.name (string)`: Name of the municipal association
+ `district.key (string)`: District regional code (5-digit)
+ `district.name (string)`: Name of the district
+ `governmentRegion.key (string)`: Regional code of the government region (3-digit)
+ `governmentRegion.name (string)`: Name of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

Example request for municipalities in Rhineland-Palatinate (State Code: `07`):

```
GET https://openplzapi.org/de/FederalStates/07/Municipalites	
```

## Requesting Municipal Associations

Municipal associations can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/de/FederalStates/{stateCode}/MunicipalAssociations`**

    :    List of all municipal associations within a federal state. A state code (2-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{regionCode}/MunicipalAssociations`**

    :    List of all municipal associations within a government region. A region code (3-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/Districts/{districtCode}/MunicipalAssociations`**

    :    List of all municipal associations within a district. A district code (5-digit) is required as a parameter. The query is subject to [paging](paging.md).

For each municipal association, the following attributes are provided:

+ `key (string)`: Combination of the district regional code and the municipal association key (9-digit)
+ `name (string)`: Name of the municipal association
+ `type (string)`: Type of the municipal association. Possible values:
    + `Amt`
    + `Samtgemeinde` (joint municipality)
    + `Verbandsgemeinde` (collective municipality)
    + `Verwaltungsgemeinschaft` (administrative community)
    + `Kirchspielslandgemeinde` (church parish land municipality)
    + `Verwaltungsverband` (administrative association)
    + `VG Trägermodell` (VG sponsor model)
    + `Erfüllende Gemeinde` (fulfilling municipality)
+ `administrativeHeadquarters (string)`: Administrative headquarters of the municipal association
+ `district.key (string)`: Regional code of the district (5-digit)
+ `district.name (string)`: Name of the district
+ `governmentRegion.key (string)`: Regional code of the government region (3-digit)
+ `governmentRegion.name (string)`: Name of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

Example request for municipal associations in Bavaria (State Code: `09`)

```
https://openplzapi.org/de/FederalStates/09/GovernmentRegions
```

## Requesting Postal Codes and Localities

Postal codes and localities can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/de/FederalStates/{key}/Localities`**

    :    List of all localities within a federal state. A state code (2-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{regionCode}/Localities`**

    :    List of all localities within angovernment region. A region code (3-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/Districts/{districtCode}/Localities`**

    :    List of all localities within a district. A district code (5-digit) is required as a parameter. The query is subject to [paging](paging.md).

    **`openplzapi.org/de/Localities?postalCode={postalCode}&name={localityName}`**

    :    Searches for all localities that match the postal code and/or locality name. The parameters `postalCode` and `name` can be used together or independently. Both parameters also support [regular expressions](regex.md). The query is subject to [paging](paging.md).

For each locality, the following attributes are provided:

+ `name (string)`: Name of the locality
+ `postalcode (string)`: Postal code of the locality
+ `municipality.key (string)`: Regional code of the municipality (8-digit)
+ `municipality.name (string)`: Name of the municipality
+ `district.key (string)`: Regional code of the district (5-digit)
+ `district.name (string)`: Name of the district
+ `governmentRegion.key (string)`: Regional code of the government region (3-digit)
+ `governmentRegion.name (string)`: Name of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

Example request for postal code *13156*

```
GET https://openplzapi.org/de/Localities?postalCode=13156
```

Example request for all German postal codes starting with *13*. The regular expression `^13` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/de/Localities?postalCode=%5E13
```

## Requesting Streets

Streets can be queried through the following API endpoints:

!!! info ""

    **`openplzapi.org/de/Streets?name={streetName}&postalCode={postalCode}&locality={localityName}`**

    :    Searches for all streets matching the street name and/or postal code and/or locality name. The parameters `name`, `postalCode`, and `locality` can be used together or independently. All three parameters support [regular expressions](regex.md). The query is subject to [paging](paging.md).

    **`openplzapi.org/de/FullTextSearch?searchTerm={searchTerm}`**

    :    Searches for streets using [full-text search](fulltextsearch.md) across street name, postal code, and locality name. The query is subject to [paging](paging.md).

For each street, the following attributes are provided:

+ `name (string)`: Name of the street
+ `postalcode (string)`: Postal code of the locality
+ `locality (string)`: Name of the locality
+ `borough (string)`: Name of the borough or city district, if applicable
+ `suburb (string)`: Name of the suburb, if applicable
+ `municipality.key (string)`: Regional code of the municipality (8-digit)
+ `municipality.name (string)`: Name of the municipality
+ `district.key (string)`: Regional code of the district (5-digit)
+ `district.name (string)`: Name of the district
+ `governmentRegion.key (string)`: Regional code of the government region (3-digit)
+ `governmentRegion.name (string)`: Name of the government region
+ `federalState.key (string)`: State code (2-digit)
+ `federalState.name (string)`: Name of the federal state

Example request for the street *Grabbeallee* (unique in Berlin):

```
GET https://openplzapi.org/de/Streets?name=Grabbeallee
```

Example request for all streets in Berlin starting with *G* and ending with *allee*. The regular expression `^G.*allee$` is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin
```

Example full-text search with the term `Berlin Pariser Platz`. The search term is [URL-encoded](url-encoding.md):

```
GET https://openplzapi.org/de/FullTextSearch?searchTerm=Berlin%20Pariser%20Platz
```