Die Datengrundlage für **OpenPLZ API** basiert komplett auf öffentlichen Quellen der Länder sowie auf Daten des [OpenStreetMap-Projekts](https://www.openstreetmap.de/). Im folgenden werden die Quellen im Detail aufgeführt.

## Deutschland

### Gemeindeverzeichnis

Das [Statistische Bundesamt (Destatis)](https://www.destatis.de) stellt die *Gemeindeleitdatei GV100* zum Download bereit. Diese Datei enthält Informationen zu allen Regionaleinheiten Deutschlands (Bundesländer, Regierungsbezirke, Kreise, Gemeindeverbände und Gemeinden). Die Gemeindeleitdatei GV100 ist eine Textdatei mit einer festen Satzstruktur von 220 Stellen, die regelmäßig aktualisiert wird.

Quelle:

+ [Gemeindeverzeichnis-Informationssystem GV-ISys](https://www.destatis.de/DE/Themen/Laender-Regionen/Regionales/Gemeindeverzeichnis/_inhalt.html)

### Straßenverzeichnis

In Deutschland gibt es keine frei zugängliche Datenbank, um alle Postleitzahlen und/oder Straßennamen Deutschlands zu erhalten. Es gibt zwar kommerzielle Dienste, die derartige Daten anbieten, aber diese kosten Geld und dürfen nicht im Sinne von Open Data verwendet werden. 

Als Alternative bietet sich das gemeinschaftlich betriebene [OpenStreetMap-Projekt](https://www.openstreetmap.org/) an. Jede Woche wird eine neue und vollständige Kopie aller Daten in OpenStreetMap sowohl als komprimierte XML-Datei als auch im [PBF-Format (Protocolbuffer Binary Format)](https://wiki.openstreetmap.org/wiki/PBF_Format) zur Verfügung gestellt. Alle Infos dazu finden sich unter [Planet OSM](https://planet.openstreetmap.org). Die Datenbankdatei ist sehr groß, daher arbeitet OpenPLZ API mit einem regionalen Auszug für Deutschland. Die Straßen werden mit allen relevanten Informationen aus den OpenStreetMap-Daten extrahiert und mit den Daten aus dem GV-ISys verknüpft. Das Ergebnis ist eine CSV-Datei, die ihren Platz [im folgenden GitHub-Repo](https://github.com/openpotato/openplzapi.data) bekommen hat und regelmäßig aktualisiert wird.

Quelle:

+ [OpenStreetMap-Daten für Deutschland](https://download.geofabrik.de/europe/germany.html)

## Österreich

### Gemeindeverzeichnis

Die [Bundesanstalt Statistik Österreich (STATISTIK AUSTRIA)](https://www.statistik.at/) stellt Downloads zur regionalen Gliederung bereit.

Quellen:

+ [Politische Bezirke und Bundesländer](https://www.statistik.at/verzeichnis/reglisten/polbezirke.pdf)
+ [Gemeinden](https://www.statistik.at/verzeichnis/reglisten/gemliste_knz.pdf)

### Straßenverzeichnis

Die [Bundesanstalt Statistik Österreich (STATISTIK AUSTRIA)](https://www.statistik.at/) stellt auch das komplette, wöchentlich aktualisierte Straßenverzeichnis bereit.

Quelle:

+ [Straßenverzeichnis](https://www.statistik.at/statistik.at/strassen)

## Schweiz

### Gemeindeverzeichnis

Das [Bundesamt für Statistik](https://www.bfs.admin.ch) stellt Downloads zur regionalen Gliederung bereit.

Quelle:

+ [Gemeindeverzeichnis (inklusive Bezirke und Kantone)](https://www.bfs.admin.ch/asset/de/31265302)

### Straßenverzeichnis

Das [Bundesamt für Landestopografie](https://www.swisstopo.admin.ch/de/home.html) stellt das komplette, regelmäßig aktualisierte Straßenverzeichnis bereit.

Quelle:

+ [Straßenverzeichnis](https://www.swisstopo.admin.ch/de/geodata/amtliche-verzeichnisse/strassenverzeichnis.html)

## Liechtenstein

### Gemeindeverzeichnis

Die Liste der Gemeinden ergibt sich aus dem Liechtensteiner Gemeindegesetz vom 20. März 1996.

Quellen:

+ [Gemeindegesetz (GemG)](https://www.gesetze.li/konso/1996076000)
+ [Wikipedia: Verwaltungsgliederung Liechtensteins](https://w.wiki/BEPn)

### Straßenverzeichnis

Das [Schweizer Bundesamt für Landestopografie](https://www.swisstopo.admin.ch/de/home.html) stellt das komplette, regelmäßig aktualisierte Straßenverzeichnis auch für Liechtenstein bereit.

Quelle:

+ [Straßenverzeichnis](https://www.swisstopo.admin.ch/de/geodata/amtliche-verzeichnisse/strassenverzeichnis.html)
