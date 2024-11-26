Das OpenPLZ API-Datenverzeichnis für die [Schweiz](https://de.wikipedia.org/wiki/Schweiz) umfasst Straßennamen, Postleitzahlen, Ortsnamen und Verwaltungseinheiten (Gemeinden, Bezirke und Kantone).

## Verwaltungstruktur

Die Verwaltungsstruktur der Schweiz basiert auf einem stark ausgeprägten Föderalismus. Sie ist in drei Ebenen unterteilt, die jeweils eigene Kompetenzen und Verantwortungsbereiche besitzen.

**Bund**

:   Die oberste Verwaltungseinheit des Schweizer Bundesstaates. Der Bund ist für übergeordnete Aufgaben wie Außenpolitik, Landesverteidigung und die schweizerische Rechtsordnung zuständig. Die Legislative wird durch die Bundesversammlung (Nationalrat und Ständerat) gebildet, die Exekutive durch den Bundesrat.

**Kantone**

:   Die föderalen Einheiten unterhalb des Bundes, bestehend aus 26 Kantonen (20 Vollkantone und 6 Halbkantone). Jeder Kanton besitzt eine eigene Verfassung, eine Regierung, ein Parlament und Gerichte. Die Kantone haben weitreichende Autonomie, insbesondere in den Bereichen Bildung, Gesundheitswesen und Polizei.

**Gemeinden**

:   Die kleinste Verwaltungseinheit mit umfassenden Selbstverwaltungsrechten. Es gibt rund 2.000 Gemeinden in der Schweiz, wobei die Anzahl durch Fusionen kontinuierlich abnimmt. Gemeinden sind für lokale Angelegenheiten wie die Raumplanung, Schulwesen und Wasserversorgung verantwortlich. Sie besitzen eigene Behörden, meist bestehend aus einem Gemeinderat und einer Gemeindeverwaltung.

## Abfrage Kantone

Die 26 Schweizer Kantone werden über den folgenden API-Endpunkt abgefragt:

!!! info ""
    
	**`openplzapi.org/ch/Cantons`**
    
	:    Liste aller Kantone in der Schweiz

Pro Kanton werden folgende Attribute geliefert:

+ `key (string)`: Kantonsnummer (max. 2-stellig)
+ `code (string)`: Kantonskürzel (2-stellig)
+ `name (string)`: Kantonsname

Hier eine Beispielabfrage für die komplette Liste der Kantone: 

``` 
GET https://openplzapi.org/ch/Cantons
```

## Abfrage Bezirke

Die Abfrage der Bezirke erfolgt über folgenden API-Endpunkt:

!!! info ""

    **`openplzapi.org/at/Cantons/{Kantonsnummer}/Districts`**

    :    Liste aller Bezirke in einem Kanton. Als Parameter wird die Kantonsnummer (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).
  
Pro Bezirk werden folgende Attribute geliefert:

+ `key (string)`: Bezirksnummer (max. 4-stellig)
+ `name (string)`: Bezirksname
+ `canton.key (string)`: Kantonsnummer (max. 2-stellig)
+ `canton.code (string)`: Kantonskürzel (2-stellig)
+ `canton.name (string)`: Kantonsname

Hier eine Beispielabfrage für die Liste der Bezirke im Kanton Freiburg (Kantonsnummer: `10`): 

```
GET https://openplzapi.org/ch/Cantons/10/Districts
```

## Abfrage Gemeinden

Die Abfrage der Gemeinden erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/ch/Cantons/{Bundeslandkennziffer}/Communes`**

    :    Liste aller Gemeinden in einem Kanton. Als Parameter wird die Kantonsnummer (1-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/ch/Districts/{Bezirksschlüssel}/Communes`**

    :    Liste aller Gemeinden in einem Bezirk. Als Parameter wird die Bezirksnummer (3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Gemeinde werden folgende Attribute geliefert:

+ `key (string)`: Gemeindenummer (max. 4-stellig)
+ `name (string)`: Amtlicher Gemeindename
+ `shortName (string)`: Gemeindename, kurz
+ `district.key (string)`: Bezirksnummer (max. 4-stellig)
+ `district.name (string)`: Bezirksname
+ `canton.key (string)`: Kantonsnummer (max. 2-stellig)
+ `canton.code (string)`: Kantonskürzel (2-stellig)
+ `canton.name (string)`: Kantonsname

Hier eine Beispielabfrage für die Liste der Gemeinden im Kanton Freiburg (Kantonsnummer: `10`): 

```
GET https://openplzapi.org/ch/Cantons/10/Communes
```

## Abfrage Postleitzahlen und Orte

Die Abfrage der Postleitzahlen und Orte erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/ch/Cantons/{Kantonsnummer}/Localities`**

    :    Liste aller Orte in einem Kanton. Als Parameter wird die Kantonsnummer (1-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/ch/Districts/{Bezirksnummer}/Localities`**

    :    Liste aller Orte in einen Bezirk. Als Parameter wird die Bezirksnummer (beide 3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/ch/Localities?postalCode={Postleitzahl}&name={Ortsname}`**

    :    Sucht alle Orte, die zur Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `postalCode` und `name` können zusammen oder jeweils exklusiv genutzt werden. Beide Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

Pro Ort werden folgende Attribute geliefert:

+ `key (string)`: Ortschaftskennziffer
+ `name (string)`: Name des Ortes
+ `postalcode (string)`: Postleitzahl des Ortes
+ `commune.key (string)`: Gemeindenummer (max. 4-stellig)
+ `commune.name (string)`: Amtlicher Gemeindename
+ `commune.shortName (string)`: Gemeindename, kurz
+ `district.key (string)`: Bezirksnummer (max. 4-stellig)
+ `district.name (string)`: Bezirksname
+ `canton.key (string)`: Kantonsnummer (max. 2-stellig)
+ `canton.code (string)`: Kantonskürzel  (2-stellig)
+ `canton.name (string)`: Kantonsname

Hier eine Beispielabfrage für die Postleitzahl *8001*: 

```
GET https://openplzapi.org/ch/Localities?postalCode=8001
```

Hier eine Beispielabfrage für alle Schweizer Postleitzahlen, die mit *80* beginnen. Der [reguläre Ausruck](regex.md) `^80` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/ch/Localities?postalCode=%5E80
```

## Abfrage Straßen

Die Abfrage der Straßen erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/ch/Streets?name={Straßenname}&postalCode={Postleitzahl}&locality={Ortsname}`**

    :    Sucht alle Straßen, die zum Straßennamen und/oder der Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `name`, `postalCode` und `locality` können zusammen oder jeweils exklusiv genutzt werden. Alle drei Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/ch/FullTextSearch?searchTerm={Suchbegriff}`**

    :    Sucht alle Straßen mittels [Volltextsuche](fulltextsearch.md) über Straßenname, Postleitzahl und Ortsname. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Straße werden folgende Attribute geliefert:

+ `key (string)`: Straßenschlüssel
+ `name (string)`: Name der Straße
+ `status (string)`: Straßenstatus. Mögliche Werte sind:
    + `Planned`
	+ `Real`
    + `Outdated`
+ `postalcode (string)`: Postleitzahl des Ortes
+ `locality (string)`: Name des Ortes
+ `commune.key (string)`: Gemeindenummer (max. 4-stellig)
+ `commune.name (string)`: Amtlicher Gemeindename
+ `commune.shortName (string)`: Gemeindename, kurz
+ `district.key (string)`: Bezirksnummer (max. 4-stellig)
+ `district.name (string)`: Bezirksname
+ `canton.key (string)`: Kantonsnummer (max. 2-stellig)
+ `canton.code (string)`: Kantonskürzel  (2-stellig)
+ `canton.name (string)`: Kantonsname

Hier eine Beispielabfrage für die Straße *Bederstrasse* (gibt es nur einmal in Zürich): 

```
GET https://openplzapi.org/ch/Streets?name=Bederstrasse
```

Hier eine Beispielabfrage für alle Straßen in Zürich, die mit *B* anfangen und mit *strasse* aufhören. Der [reguläre Ausruck](regex.md) `^B.*strasse$` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/ch/Streets?name=%5EB.*strasse%24&locality=Z%C3%BCrich
```

Hier eine Volltextsuche mit dem Suchbegriff `Zürich Bederstrasse`. Der Suchbegriff ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/ch/FullTextSearch?searchTerm=Z%C3%BCrich%20Bederstrasse
```