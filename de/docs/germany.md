Das OpenPLZ API-Datenverzeichnis für [Deutschland](https://de.wikipedia.org/wiki/Deutschland) umfasst Straßennamen, Postleitzahlen, Ortsnamen und Verwaltungseinheiten (Gemeinden, Gemeindeverbände, Kreise, Regierungsbezirke und Bundesländer).

## Verwaltungsstruktur

Die Verwaltungsstruktur in Deutschland basiert auf einem föderalen System, das durch das Grundgesetz geregelt ist. Sie gliedert sich in mehrere Ebenen mit jeweils spezifischen Kompetenzen und Aufgaben.

**Bund**

:   Die oberste Ebene der Verwaltung und Gesetzgebung in Deutschland. Der Bund ist zuständig für übergeordnete Angelegenheiten wie Außenpolitik, Verteidigung und die Währungsordnung. Die Legislative wird durch den Bundestag und den Bundesrat, die Exekutive durch die Bundesregierung gebildet.

**Bundesländer**

:   Die föderalen Einheiten unterhalb des Bundes, bestehend aus 16 Bundesländern. Jedes Bundesland besitzt eine eigene Verfassung, eine Landesregierung und einen Landtag. Die Länder haben eigene Zuständigkeiten, insbesondere in Bereichen wie Bildung, Polizei und Kultur.
 
**Regierungsbezirke**

:   Eine mittlere Verwaltungsebene, die in einigen Bundesländern zwischen der Landes- und Kreisebene angesiedelt ist. Regierungsbezirke existieren nur noch in vier der 16 Bundesländer und dienen der Koordination der Landesverwaltung. Sie haben keine eigenständige Gesetzgebung.

**Kreise**

:   Eine kommunale Verwaltungseinheit, die zwischen den Regierungsbezirken (sofern vorhanden) und den Gemeinden liegt.
    
	Die wichtigsten Arten:
       
	+ Landkreise
    + Kreisfreie Städte (nehmen die Aufgaben von Kreisen und Gemeinden gleichzeitig wahr).
	
**Gemeinden**

:   Die kleinste Verwaltungseinheit mit umfassenden Selbstverwaltungsrechten. Gemeinden sind für die unmittelbare Verwaltung vor Ort zuständig. Sie verfügen über einen gewählten Gemeinderat und meist einen Bürgermeister als Verwaltungsleitung.

**Gemeindeverbände**

:   Zusammenschlüsse von Gemeinden zur gemeinsamen Erfüllung bestimmter Aufgaben. Gemeindeverbände, wie Verwaltungsgemeinschaften oder Zweckverbände, sind in der Regel auf spezifische administrative Funktionen begrenzt.

## Abfrage Bundesländer

Die Abfrage der 16 deutschen Bundesländer erfolgt über folgenden API-Endpunkt:

!!! info ""
    
	**`openplzapi.org/de/FederalStates`**
    
	:    Liste aller Bundesländer in Deutschland

Pro Bundesland werden folgende Attribute geliefert:

+ `key (string)`: Regionalschlüssel (2-stellig)
+ `name (string)`: Name des Bundeslandes
+ `seatOfGovernment (string)`: Regierungssitz des Bundeslandes

Hier eine Beispielabfrage für die komplette Liste der Bundesländer: 

``` 
GET https://openplzapi.org/de/FederalStates
```

## Abfrage Regierungsbezirke

Die Abfrage der Regierungsbezirke erfolgt über folgenden API-Endpunkt:

!!! info ""

    **`openplzapi.org/de/FederalStates/{Bundeslandschlüssel}/GovernmentRegions`**

    :    Liste aller Regierungsbezirke in einem Bundesland. Als Parameter wird ein Bundeslandschlüssel (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Regierungsbezirk werden folgende Attribute geliefert:

+ `key (string)`: Regionalschlüssel (3-stellig)
+ `name (string)`: Name des Regierungsbezirks
+ `administrativeHeadquarters (string)`: Verwaltungssitz des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

!!! note "Regierungsbezirke"

    Bitte beachte, dass es nur noch in vier Bundesländern Regierungsbezirke gibt: **Baden-Württemberg**, **Bayern**, **Hessen** und **Nordrhein-Westfalen**. In den Bundesländern **Niedersachen**, **Rheinland-Pfalz** und **Sachsen** sind die Regierungsbezirke offiziell abgeschafft, werden aber aus statistischen Gründen noch weiter im Gemeindeverzeichnis geführt und sind damit auch hier noch abrufbar.

Hier eine Beispielabfrage für die Liste der Regierungsbezirke in Bayern (Bundeslandschlüssel: `09`): 

```
GET https://openplzapi.org/de/FederalStates/09/GovernmentRegions
```

## Abfrage Kreise

Die Abfrage der Kreise erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/de/FederalStates/{Bundeslandschlüssel}/Districts`**

    :    Liste aller Kreise in einem Bundesland. Als Parameter wird ein Bundeslandschlüssel (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).
  
    **`openplzapi.org/de/GovernmentRegions/{Bezirksschlüssel}/Districts`**

    :    Liste aller Kreise in einem Regierungsbezirk. Als Parameter wird ein Bezirksschlüssel (3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md). 

Pro Kreis werden folgende Attribute geliefert:

+ `key (string)`: Regionalschlüssel (5-stellig)
+ `name (string)`: Name des Kreises
+ `type (string)`: Kennzeichen des Kreises. Mögliche Werte:
    + `Kreisfreie Stadt`
    + `Stadtkreis`
    + `Kreis`
    + `Landkreis`
    + `Regionalverband`
+ `administrativeHeadquarters (string)`: Sitz der Kreisverwaltung
+ `governmentRegion.key (string)`: Regionalschlüssel des Regierungsbezirks (3-stellig)
+ `governmentRegion.name (string)`: Name des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Liste der Kreise in Rheinland-Pfalz (Bundeslandschlüssel: `07`): 

```
GET https://openplzapi.org/de/FederalStates/07/Districts
```

## Abfrage Gemeinden

Die Abfrage der Gemeinden erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/de/FederalStates/{Bundeslandschlüssel}/Municipalites`**

    :    Liste aller Gemeinden in einem Bundesland. Als Parameter wird ein Bundeslandschlüssel (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{Bezirksschlüssel}/Municipalites`**

    :    Liste aller Gemeinden in einem Regierungsbezirk. Als Parameter wird ein Bezirksschlüssel (3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/Districts/{Kreisschlüssel}/Municipalites`**

    :    Liste aller Gemeinden in einen Kreis. Als Parameter wird ein Kreisschlüssel (5-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Gemeinde werden folgende Attribute geliefert:

+ `key (string)`: Regionalschlüssel (8-stellig)
+ `name (string)`: Name der Gemeinde
+ `type (string)`: Kennzeichen der Gemeinde. Mögliche Werte:
    + `Markt`
	+ `Kreisfreie Stadt`
    + `Stadtkreis`
    + `Stadt`
    + `Kreisangehörige Gemeinde`
    + `Gemeindefreies Gebiet (bewohnt)`
    + `Gemeindefreies Gebiet (unbewohnt)`
    + `Große Kreisstadt`
+ `postalCode (string)`: Postleitzahl des Verwaltungssitzes, falls mehrere Postleitzahlen vorhanden sind
+ `multiplePostalCodes (bool)`: Umfasst die Gemeinde mehr als eine Postleitzahl?
+ `association.key (string)`: Kombination aus Regionalschlüssel des Kreises und Schlüssel des Gemeindenverbandes (9-stellig)
+ `association.name (string)`: Name des Gemeindenverbandes
+ `district.key (string)`: Regionalschlüssel des Kreises (5-stellig)
+ `district.name (string)`: Name des Kreises
+ `governmentRegion.key (string)`: Regionalschlüssel des Regierungsbezirks (3-stellig)
+ `governmentRegion.name (string)`: Name des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Liste der Gemeinden in Rheinland-Pfalz (Bundeslandschlüssel: `07`): 

```
GET https://openplzapi.org/de/FederalStates/07/Municipalites	
```

## Abfrage Gemeindenverbände

Die Abfrage der Gemeindenverbände erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/de/FederalStates/{Bundeslandschlüssel}/MunicipalAssociations`**

    :    Liste aller Gemeindeverbände in einem Bundesland. Als Parameter wird ein Bundeslandschlüssel (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{Bezirksschlüssel}/MunicipalAssociations`**

    :    Liste aller Gemeindeverbände in einem Regierungsbezirk. Als Parameter wird ein Bezirksschlüssel (3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/Districts/{Kreisschlüssel}/MunicipalAssociations`**

    :    Liste aller Gemeindeverbände in einen Kreis. Als Parameter wird ein Kreisschlüssel (5-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Gemeindeverband werden folgende Attribute geliefert:

+ `key (string)`: Kombination aus Regionalschlüssel des Kreises und Schlüssel des Gemeindenverbandes (9-stellig)
+ `name (string)`: Name des Gemeindenverbandes
+ `type (string)`: Kennzeichen des Gemeindenverbandes. Mögliche Werte:
    + `Amt`
	+ `Samtgemeinde`
    + `Verbandsgemeinde`
    + `Verwaltungsgemeinschaft`
    + `Kirchspielslandgemeinde`
    + `Verwaltungsverband`
    + `VG Trägermodell`
    + `Erfüllende Gemeinde`
+ `administrativeHeadquarters (string)`: Verwaltungssitz des Gemeindeverbandes
+ `district.key (string)`: Regionalschlüssel des Kreises (5-stellig)
+ `district.name (string)`: Name des Kreises
+ `governmentRegion.key (string)`: Regionalschlüssel des Regierungsbezirks (3-stellig)
+ `governmentRegion.name (string)`: Name des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Liste der Gemeindenverbände in Bayern (Schlüssel: `09`): 

```
https://openplzapi.org/de/FederalStates/09/GovernmentRegions
```

## Abfrage Postleitzahlen und Orte

Die Abfrage der Postleitzahlen und Orte erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/de/FederalStates/{key}/Localities`**

    :    Liste aller Orte in einem Bundesland. Als Parameter wird ein Bundeslandschlüssel (2-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/GovernmentRegions/{Bezirksschlüssel}/Localities`**

    :    Liste aller Orte in einem Regierungsbezirk. Als Parameter wird ein Bezirksschlüssel (3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/Districts/{Kreisschlüssel}/Localities`**

    :    Liste aller Orte in einen Kreis. Als Parameter wird ein Kreisschlüssel (5-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/Localities?postalCode={Postleitzahl}&name={Ortsname}`**

    :    Sucht alle Orte, die zur Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `postalCode` und `name` können zusammen oder jeweils exklusiv genutzt werden. Beide Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

Pro Ort werden folgende Attribute geliefert:

+ `name (string)`: Name des Ortes
+ `postalcode (string)`: Postleitzahl des Ortes
+ `municipality.key (string)`: Regionalschlüssel der Gemeinde (8-stellig)
+ `municipality.name (string)`: Name der Gemeinde
+ `district.key (string)`: Regionalschlüssel des Kreises (5-stellig)
+ `district.name (string)`: Name des Kreises
+ `governmentRegion.key (string)`: Regionalschlüssel des Regierungsbezirks (3-stellig)
+ `governmentRegion.name (string)`: Name des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Postleitzahl *13156*: 

```
GET https://openplzapi.org/de/Localities?postalCode=13156
```

Hier eine Beispielabfrage für alle deutschen Postleitzahlen, die mit *13* beginnen. Der reguläre Ausruck `^13` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/de/Localities?postalCode=%5E13
```

## Abfrage Straßen

Die Abfrage der Straßen erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/de/Streets?name={Straßenname}&postalCode={Postleitzahl}&locality={Ortsname}`**

    :    Sucht alle Straßen, die zum Straßennamen und/oder der Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `name`, `postalCode` und `locality` können zusammen oder jeweils exklusiv genutzt werden. Alle drei Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/de/FullTextSearch?searchTerm={Suchbegriff}`**

    :    Sucht alle Straßen mittels [Volltextsuche](fulltextsearch.md) über Straßenname, Postleitzahl und Ortsname. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Straße werden folgende Attribute geliefert:

+ `name (string)`: Name der Straße
+ `postalcode (string)`: Postleitzahl des Ortes
+ `locality (string)`: Name des Ortes
+ `borough (string)`: Falls vorhanden, Name des Stadtbezirks oder Stadtteils
+ `suburb (string)`: Falls vorhanden, Name des Ortsteils
+ `municipality.key (string)`: Regionalschlüssel der Gemeinde (8-stellig)
+ `municipality.name (string)`: Name der Gemeinde
+ `district.key (string)`: Regionalschlüssel des Kreises (5-stellig)
+ `district.name (string)`: Name des Kreises
+ `governmentRegion.key (string)`: Regionalschlüssel des Regierungsbezirks (3-stellig)
+ `governmentRegion.name (string)`: Name des Regierungsbezirks
+ `federalState.key (string)`: Regionalschlüssel des Bundeslandes (2-stellig)
+ `federalState.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Straße *Grabbeallee* (gibt es nur einmal in Berlin): 

```
GET https://openplzapi.org/de/Streets?name=Grabbeallee
```

Hier eine Beispielabfrage für alle Straßen in Berlin, die mit *G* anfängen und mit *allee* aufhören. Der reguläre Ausruck `^G.*allee$` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin
```

Hier eine Volltextsuche mit dem Suchbegriff `Berlin Pariser Platz`. Der Suchbegriff ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/de/FullTextSearch?searchTerm=Berlin%20Pariser%20Platz
```