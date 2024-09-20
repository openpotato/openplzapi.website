## OpenPLZ API Data

Der aktuelle Datenbestand (siehe auch [Datenquellen](sources.md)):

Land                    | Datenquelle         | Veröffentlichung
------------------------|---------------------|-----------------
:flag_de: Deutschland   | Gemeindeverzeichnis | Juli 2024
:flag_de: Deutschland   | Straßenverzeichnis  | 17.09.2024
:flag_at: Österreich    | Gemeindeverzeichnis | 12.09.2024
:flag_at: Österreich    | Straßenverzeichnis  | 12.09.2024
:flag_ch: Schweiz       | Gemeindeverzeichnis | 01.03.2024
:flag_ch: Schweiz       | Straßenverzeichnis  | 18.09.2024
:flag_li: Liechtenstein | Gemeindeverzeichnis | März 1996
:flag_li: Liechtenstein | Straßenverzeichnis  | 18.09.2024

## OpenPLZ API Service

### 0.0.5 <small>_ 20. September 2024</small>

- API change: `Street`-Entitäten für Deutschland enthalten jetzt zusätzliche Angaben zu Stadtbezirk (Borough) und/oder Stadtteil (Suburb) (soweit in OpenStreetMap vorhanden)
- Support für Straßen und Postleitzahlen aus Liechtenstein
- Fehlerkorrekturen und Refactoring

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