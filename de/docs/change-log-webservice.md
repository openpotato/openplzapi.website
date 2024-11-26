# Änderungslog - Web-Service  

Der OpenPLZ API Web-Service ist [Open Source](https://github.com/openpotato/openplzapi) unter GitHub. Dort kann die detailierte [Commit-Historie](https://github.com/openpotato/openplzapi/commits/develop/) eingesehen werden. Dieses Änderungslog dient als zusammenfassender Überblick der Änderungen.

Wir halten uns dabei weitestgehend an die Empfehlungen aus dem Community-Projekt [Keep a Changelog](https://keepachangelog.com/de).

### Unveröffentlicht

Erste offizielle Version 1.0 noch in diesem Jahr. Die API-Schnitstelle wird dann als v1 versioniert und bekommt ab dann keine Breaking Changes mehr.

### 0.0.6 <small>_ 25. November 2024</small>

**Hinzugefügt:** 

+ Neue API-Endpunkte `FullTextSearch` zur Volltextsuche über Straße, Ort und Postleitzahl für alle Länder.
+ Zusätzliche Paging-Informationen `x-page`, `x-page-size`, `x-total-pages`und `x-total-count` in den HTTP-Response-Headers der API-Antworten (gilt nur für Endpunkte mit Pagination). 
+ Support für [RFC 9457](https://www.rfc-editor.org/rfc/rfc9457) (Problem Details for HTTP APIs)

**Korrigiert:**

+ Fehlerhafte URL für API-Endpunkt `li/Communes` korrigiert (war zuvor `li/Cantons/Communes`).

### 0.0.5 <small>_ 20. September 2024</small>

**Hinzugefügt:** 

+ `Street`-Entitäten für Deutschland enthalten jetzt zusätzliche Angaben zu Stadtbezirk (Borough) und/oder Stadtteil (Suburb) (soweit in OpenStreetMap vorhanden).
+ Support für Straßen und Postleitzahlen aus Liechtenstein.

**Geändert:**

+ Aktualisierung der Datenquellen.

### 0.0.4 <small>_ 23. November 2023</small>

**Hinzugefügt:**

+ Neue API-Endpunkte für `Locality`-Entitäten.
+ Pagination für fast alle API-Endpunkte.

**Geändert:**

+ Update auf .NET 8.

### 0.0.3 <small>_ 27. September 2023</small>

**Hinzugefügt:**

+ CSV als zusätzliches Ausgabeformat.

**Geändert:**

+ Aktualisierung der Datenquellen.

### 0.0.2 <small>_ 05. Februar 2023</small>

**Hinzugefügt:**

+ `Street`-Entitäten und `Locality`-Entitäten enthalten jetzt ausführlichere Angaben zu Gemeinden, Kreisen, Bezirken und Bundesländern bzw. Kantonen.
+ [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)-Unterstützung hinzugefügt.

### 0.0.1 <small>_ 09. Dezember 2022</small>

Erste Veröffentlichung.