## OpenPLZ API Data

Der aktuelle Datenbestand (siehe auch [Datenquellen](sources.md)):

Land        | Datenquelle         | Veröffentlichung
------------|---------------------|-----------------
Deutschland | Gemeindeverzeichnis | Juli 2023
Deutschland | Straßenverzeichnis  | 26.09.2023
Österreich  | Gemeindeverzeichnis | 21.09.2023
Österreich  | Straßenverzeichnis  | 21.09.2023
Schweiz     | Gemeindeverzeichnis | 01.01.2023
Schweiz     | Straßenverzeichnis  | 22.09.2023

## OpenPLZ API Service

### 0.0.4 <small>_ 23. November 2023</small>

- Neue API-Endpunkte für `Locality`-Entitäten
- Paging für fast alle API-Endpunkte
- Update auf .NET 8
- Fehlerkorrekturen

### 0.0.3 <small>_ 27. September 2023</small>

- CSV als zusätzliches Ausgabeformat
- Aktualisierung der Datenquellen
- Fehlerkorrekturen

### 0.0.2 <small>_ 05. Februar 2023</small>

- Breaking API change: `Street`-Entitäten und `Locality`-Entitäten enthalten jetzt ausführlichere Angaben zu Gemeinden, Kreisen, Bezirken und Bundesländern bzw. Kantonen.
- CORS-Unterstützung hinzugefügt
- Fehlerkorrekturen und Refactoring

### 0.0.1 <small>_ 09. Dezember 2022</small>

- Erste Veröffentlichung