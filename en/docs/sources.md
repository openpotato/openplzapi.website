The data basis for **OpenPLZ API** is completely based on public sources of the countries as well as on data of the [OpenStreetMap project](https://www.openstreetmap.de/). The sources are listed in detail below.

## Germany

### Municipality directory

The [Federal Statistical Office (Destatis)](https://www.destatis.de) provides the *Gemeindeleitdatei GV100* for download. This file contains information on all regional units of Germany (federal states, administrative districts, counties, associations of municipalities and municipalities). The GV100 file is a text file with a fixed record structure of 220 digits that is updated regularly.

Source:

+ [List of Municipalities (GV-ISys)](https://www.destatis.de/EN/Themes/Countries-Regions/Regional-Statistics/OnlineListMunicipalities/_inhalt.html)

### Street directory

In Germany, there is no freely accessible database to obtain all postcodes and/or street names in Germany. There are commercial services that offer such data, but they cost money and may not become Open Data. 

An alternative is the community-run [OpenStreetMap project](https://www.openstreetmap.org/). Every week, a new and complete copy of all data in OpenStreetMap is made available both as a compressed XML file and in [PBF format (Protocolbuffer Binary Format)](https://wiki.openstreetmap.org/wiki/PBF_Format). All info on this can be found at [https://planet.openstreetmap.org](https://planet.openstreetmap.org). The database file is very large, so OpenPLZ API works with a regional extract for Germany. The streets are extracted with all relevant information from the OpenStreetMap data and linked with the data from the GV-ISys. The result is a CSV file that has been given its place [in the following GitHub repo](https://github.com/openpotato/openplzapi.data) and is updated regularly.

Source:

+ [OpenStreetMap data for Germany](https://download.geofabrik.de/europe/germany.html)

## Austria

### Municipality directory

The [Bundesanstalt Statistik Österreich (STATISTIK AUSTRIA)](https://www.statistik.at/en/) provides downloads for regional breakdown.

Sources:

+ [Political districts and federal provinces](https://www.statistik.at/verzeichnis/reglisten/polbezirke.pdf)
+ [Municipalities](https://www.statistik.at/verzeichnis/reglisten/gemliste_knz.pdf)

### Street directory

The [Bundesanstalt Statistik Österreich (STATISTIK AUSTRIA)](https://www.statistik.at/en/) also provides the complete street directory, updated weekly.

Source:

+ [Street directory](https://www.statistik.at/statistik.at/strassen)

## Switzerland

### Municipal directory

The [Federal Statistical Office](https://www.bfs.admin.ch/bfs/en/home.html) provides downloads for regional breakdown.

Source:

+ [Municipal directory (including districts and cantons)](https://www.bfs.admin.ch/bfs/de/home/grundlagen/agvch.html)

### Street directory

The [Federal Office of Topography](https://www.swisstopo.admin.ch/en/home.html) provides the complete, regularly updated street directory.

Source:

+ [Street directory](https://www.swisstopo.admin.ch/en/geodata/official-geographic-directories/street-directory.html)

