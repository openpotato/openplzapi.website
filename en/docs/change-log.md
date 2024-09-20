## OpenPLZ API Data

The current dataset (see also [data sources](sources.md)):

Country                 | Data source            | Release
------------------------|------------------------|--------
:flag_de: Germany       | Municipality directory | July 2024
:flag_de: Germany       | Street directory       | 2024-09-17
:flag_at: Austria       | Municipality directory | 2024-09-12
:flag_at: Austria       | Street directory       | 2024-09-12
:flag_ch: Switzerland   | Municipality directory | 2024-03-01
:flag_ch: Switzerland   | Street directory       | 2024-09-18
:flag_li: Liechtenstein | Municipality directory | March 1996
:flag_li: Liechtenstein | Street directory       | 2024-09-18

## OpenPLZ API Service

### 0.0.5 <small>_ September 20, 2024</small>

- API change: Street entities for Germany now contain additional information on borough and/or suburb (if available in OpenStreetMap)
- Added support for streets and postal codes from Liechtenstein
- Bug fixes and refactoring

### 0.0.4 <small>_ November 23, 2023</small>

- New API endpoints for `Locality` entities
- Paging for nearly all API endpoints
- Update to .NET 8
- Bug fixes

### 0.0.3 <small>_ September 27, 2023</small>

- CSV as additional output format
- Updating of data sources
- Bug fixes

### 0.0.2 <small>_ February 05, 2023</small>

- Breaking API change: `Street` entities and `Locality` entities now contain more detailed information on municipalities, districts and federal states or cantons.
- Added CORS support
- Bug fixes and refactoring

### 0.0.1 <small>_ December 09, 2022</small>

- First publication