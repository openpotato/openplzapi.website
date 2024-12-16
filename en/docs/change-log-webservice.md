# Änderungslog - Web-Service  

The OpenPLZ API Web Service is [Open Source](https://github.com/openpotato/openplzapi) on GitHub. The detailed [commit history](https://github.com/openpotato/openplzapi/commits/develop/) can be viewed there. This change log serves as a summarised overview of the changes.

We largely adhere to the recommendations from the community project [Keep a Changelog](https://keepachangelog.com).

## 1.0.0 <small>_ December 16, 2024</small>

**Added:** 

+ Added HTTP Access-Control-Expose-Headers response header

**Changed:**

+ Breaking API change: Missing paging endpoint for `at/Districts/{key}/Localities`

**Fixed:**

+ Bug fix for Swiss CSV response format

## 0.1.0 <small>_ December 02, 2024</small>

**Changed:**

+ Update to .NET 9
+ Breaking API change: Communes, districts and cantons for Switzerland have now all been given the properties `HistoricalCode` and `ShortName`. The `Code` property for cantons has been removed.
+ Refactoring of the source for the Swiss commune directory. The API of the Federal Statistical Office (FSO) is now accessed directly.

## 0.0.6 <small>_ November 25, 2024</small>

**Added:** 

+ New API endpoints `FullTextSearch` for full-text search via street, location and postal code for all countries.
+ Additional paging information `x-page`, `x-page-size`, `x-total-pages` and `x-total-count` in the HTTP response headers of the API (only applies to endpoints with pagination). 
+ Support for [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457) (Problem Details for HTTP APIs)

**Fixed:**

+ Fixed incorrect URL for API endpoint `li/Communes` (was previously `li/Cantons/Communes`).

## 0.0.5 <small>_ September 20, 2024</small>

**Added:** 

+ Street entities for Germany now contain additional information on borough and/or suburb (if available in OpenStreetMap)
+ Support for streets and postal codes from Liechtenstein

**Changed:**

+ Update of the data sources.

## 0.0.4 <small>_ November 23, 2023</small>

**Added:** 

+ New API endpoints for `Locality` entities
+ Paging for nearly all API endpoints

**Changed:**

+ Update to .NET 8

## 0.0.3 <small>_ September 27, 2023</small>

**Added:** 

+ CSV as additional output format

**Changed:**

+ Update of the data sources.

## 0.0.2 <small>_ February 05, 2023</small>

**Added:** 

+ `Street` entities and `Locality` entities now contain more detailed information on municipalities, districts and federal states or cantons.
+ [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) support added.

## 0.0.1 <small>_ December 09, 2022</small>

First publication