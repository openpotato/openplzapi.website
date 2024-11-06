## Data

The current dataset (see also [data sources](sources.md)):

Country                   | Data source            | Release
--------------------------|------------------------|--------
:flag_de: - Germany       | Municipality directory | July 2024
:flag_de: - Germany       | Street directory       | 2024-09-17
:flag_at: - Austria       | Municipality directory | 2024-09-12
:flag_at: - Austria       | Street directory       | 2024-09-12
:flag_ch: - Switzerland   | Municipality directory | 2024-03-01
:flag_ch: - Switzerland   | Street directory       | 2024-09-18
:flag_li: - Liechtenstein | Municipality directory | March 1996
:flag_li: - Liechtenstein | Street directory       | 2024-09-18

## Web Service

The OpenPLZ API Web Service is [Open Source](https://github.com/openpotato/openplzapi) on GitHub.
The detailed [commit history](https://github.com/openpotato/openplzapi/commits/develop/) can be viewed there. This change log serves as a summarised overview of the changes.

We largely adhere to the recommendations from the community project [Keep a Changelog](https://keepachangelog.com).

### Unreleased

First official version 1.0 later this year. The API interface will then be versioned as v1 and will no longer receive any breaking changes from then on.

### 0.0.6 <small>_ September 26, 2024</small>

**Added:** 

+ New API endpoints `FullTextSearch` for full-text search via street, location and postal code for all countries.
+ Additional paging information `x-page`, `x-page-size`, `x-total-pages` and `x-total-count` in the HTTP response headers of the API (only applies to endpoints with pagination). 

**Fixed:**

+ Fixed incorrect URL for API endpoint `li/Communes` (was previously `li/Cantons/Communes`).

### 0.0.5 <small>_ September 20, 2024</small>

**Added:** 

- Street entities for Germany now contain additional information on borough and/or suburb (if available in OpenStreetMap)
- Support for streets and postal codes from Liechtenstein

**Changed:**

+ Update of the data sources.

### 0.0.4 <small>_ November 23, 2023</small>

**Added:** 

- New API endpoints for `Locality` entities
- Paging for nearly all API endpoints

**Changed:**

- Update to .NET 8

### 0.0.3 <small>_ September 27, 2023</small>

**Added:** 

- CSV as additional output format

**Changed:**

+ Update of the data sources.

### 0.0.2 <small>_ February 05, 2023</small>

**Added:** 

- `Street` entities and `Locality` entities now contain more detailed information on municipalities, districts and federal states or cantons.
+ [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) support added.

### 0.0.1 <small>_ December 09, 2022</small>

First publication