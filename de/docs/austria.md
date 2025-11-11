Das OpenPLZ API-Datenverzeichnis für [Österreich](https://de.wikipedia.org/wiki/%C3%96sterreich) umfasst Straßennamen, Postleitzahlen, Ortsnamen und Verwaltungseinheiten (Gemeinden, Bezirke und Bundeländer).

## Verwaltungsstruktur

Die Verwaltungsstruktur in Österreich basiert auf einer föderalen Ordnung, die in mehrere Ebenen gegliedert ist. Jede Ebene hat klar definierte Kompetenzen und Aufgaben, die durch die Verfassung geregelt sind.

**Bund**

:   Die oberste Verwaltungseinheit des Staates. Der Bund verfügt über eine zentrale Regierung und ist für übergeordnete Angelegenheiten wie Außenpolitik, Verteidigung und Justiz verantwortlich.

**Bundesländer**

:   Die föderalen Einheiten unterhalb des Bundes, bestehend aus 9 Bundesländern. Jedes Bundesland hat eine eigene Verfassung, eine Landesregierung und einen Landtag. Die Länder besitzen eigenständige Kompetenzen, insbesondere in Bereichen wie Bildung und Kultur.

**Bezirke**

:   Eine mittlere Verwaltungsebene zwischen den Ländern und Gemeinden, bestehend aus politischen Bezirken. Bezirke haben keine eigene Gesetzgebung, sondern dienen der Verwaltung von Aufgaben, die über die Gemeindekompetenzen hinausgehen. Bezirksverwaltungsbehörden sind entweder Bezirkshauptmannschaften oder Magistrate in Statutarstädten.

**Gemeinden**

:   Die kleinste Verwaltungseinheit mit Selbstverwaltungskompetenz. Es gibt rund 2.000 Gemeinden in Österreich. Jede Gemeinde besitzt eine gewählte Gemeindeverwaltung, die von einem Bürgermeister geleitet wird.

**Statutarstädte**

:   Städte, die sowohl die Aufgaben einer Gemeinde als auch eines Bezirks wahrnehmen. Es gibt 15 Statutarstädte in Österreich, darunter Wien, das zugleich ein Bundesland ist.

## Abfrage Bundesländer

Die neun österreichischen Bundesländer werden über den folgenden API-Endpunkt abgefragt:

!!! info ""
    
	**`openplzapi.org/at/FederalProvinces`**
    
	:    Liste aller Bundesländer in Österreich

Pro Bundesland werden folgende Attribute geliefert:

+ `key (string)`: Bundeslandkennziffer (1-stellig)
+ `name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die komplette Liste der Bundesländer: 

``` 
GET https://openplzapi.org/at/FederalProvinces
```

## Abfrage Bezirke

Die Abfrage der politischen Bezirke erfolgt über folgenden API-Endpunkt:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{Bundeslandkennziffer}/Districts`**

    :    Liste aller Bezirke in einem Bundesland. Als Parameter wird die Bundeslandkennziffer (1-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).
  

Pro Bezirk werden folgende Attribute geliefert:

+ `key (string)`: Bezirkskennziffer (3-stellig)
+ `code (string)`: Bezirkskodierung (3-stellig)
+ `name (string)`: Bezirksname
+ `federalProvince.key (string)`: Bundeslandkennziffer (1-stellig)
+ `federalProvince.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Liste der Bezirke in Wien (Bundeslandkennziffer: `7`): 

```
GET https://openplzapi.org/at/FederalProvinces/7/Districts
```

## Abfrage Gemeinden

Die Abfrage der Gemeinden erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{Bundeslandkennziffer}/Municipalities`**

    :    Liste aller Gemeinden in einem Bundesland. Als Parameter wird die Bundeslandkennziffer (1-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/at/Districts/{Bezirksschlüssel}/Municipalities`**

    :    Liste aller Gemeinden in einem Bezirk. Als Parameter wird die Bezirkskennziffer **oder** die Bezirkscodierung (beide 3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Gemeinde werden folgende Attribute geliefert:

+ `key (string)`: Gemeindekennziffer (5-stellig)
+ `code (string)`: Gemeindecode (5-stellig)
+ `name (string)`: Name der Gemeinde
+ `status (string)`: Status der Gemeinde. Mögliche Werte:
    + `Markt`
	+ `Kreisfreie Stadt`
    + `Stadtkreis`
    + `Stadt`
    + `Kreisangehörige Gemeinde`
    + `Gemeindefreies Gebiet (bewohnt)`
    + `Gemeindefreies Gebiet (unbewohnt)`
    + `Große Kreisstadt`
+ `postalCode (string)`: Postleitzahl des Gemeindeamtes
+ `multiplePostalCodes (bool)`: Umfasst die Gemeinde mehr als eine Postleitzahl?
+ `district.key (string)`: Bezirkskennziffer (3-stellig)
+ `district.code (string)`: Bezirkskodierung (3-stellig)
+ `district.name (string)`: Bezirksname
+ `federalProvince.key (string)`: Bundeslandkennziffer (1-stellig)
+ `federalProvince.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Liste der Gemeinden in Wien (Bundeslandkennziffer: `7`): 

```
GET https://openplzapi.org/at/FederalProvinces/7/Municipalities
```

## Abfrage Postleitzahlen und Orte

Die Abfrage der Postleitzahlen und Orte erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/at/FederalProvinces/{Bundeslandkennziffer}/Localities`**

    :    Liste aller Orte in einem Bundesland. Als Parameter wird die Bundeslandkennziffer (1-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/at/Districts/{Bezirksschlüssel}/Localities`**

    :    Liste aller Orte in einen Bezirk. Als Parameter wird die Bezirkskennziffer **oder** die Bezirkscodierung (beide 3-stellig) benötigt. Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/at/Localities?postalCode={Postleitzahl}&name={Ortsname}`**

    :    Sucht alle Orte, die zur Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `postalCode` und `name` können zusammen oder jeweils exklusiv genutzt werden. Beide Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

Pro Ort werden folgende Attribute geliefert:

+ `key (string)`: Ortschaftskennziffer
+ `name (string)`: Name des Ortes
+ `postalcode (string)`: Postleitzahl des Ortes
+ `municipality.key (string)`: Gemeindekennziffer (5-stellig)
+ `municipality.code (string)`: Gemeindecode (5-stellig)
+ `municipality.name (string)`: Name der Gemeinde
+ `district.key (string)`: Bezirkskennziffer (3-stellig)
+ `district.code (string)`: Bezirkskodierung (3-stellig)
+ `district.name (string)`: Bezirksname
+ `federalProvince.key (string)`: Bundeslandkennziffer (1-stellig)
+ `federalProvince.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Postleitzahl *1010*: 

```
GET https://openplzapi.org/at/Localities?postalCode=1010
```

Hier eine Beispielabfrage für alle deutschen Postleitzahlen, die mit *10* beginnen. Der [reguläre Ausruck](regex.md) `^10` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/at/Localities?postalCode=%5E10
```

## Abfrage Straßen

Die Abfrage der Straßen erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/at/Streets?name={Straßenname}&postalCode={Postleitzahl}&locality={Ortsname}`**

    :    Sucht alle Straßen, die zum Straßennamen und/oder der Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `name`, `postalCode` und `locality` können zusammen oder jeweils exklusiv genutzt werden. Alle drei Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/at/FullTextSearch?searchTerm={Suchbegriff}`**

    :    Sucht alle Straßen mittels [Volltextsuche](fulltextsearch.md) über Straßenname, Postleitzahl und Ortsname. Die Abfrage unterliegt einem [Paging](paging.md).

Pro Straße werden folgende Attribute geliefert:

+ `key (string)`: Straßenkennziffer
+ `name (string)`: Name der Straße
+ `postalcode (string)`: Postleitzahl des Ortes
+ `locality (string)`: Name des Ortes
+ `municipality.key (string)`: Gemeindekennziffer (5-stellig)
+ `municipality.code (string)`: Gemeindecode (5-stellig)
+ `municipality.name (string)`: Name der Gemeinde
+ `district.key (string)`: Bezirkskennziffer (3-stellig)
+ `district.code (string)`: Bezirkskodierung (3-stellig)
+ `district.name (string)`: Bezirksname
+ `federalProvince.key (string)`: Bundeslandkennziffer (1-stellig)
+ `federalProvince.name (string)`: Name des Bundeslandes

Hier eine Beispielabfrage für die Straße *Alexander-Poch-Platz*: 

```
GET https://openplzapi.org/at/Streets?name=Alexander-Poch-Platz
```

Hier eine Beispielabfrage für alle Plätze in Wien, die mit *A* anfangen und mit *Platz* aufhören. Der [reguläre Ausruck](regex.md) `^A.*Platz$` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/at/Streets?name=%5EA.%2APlatz%24&locality=Wien
```

Hier eine Volltextsuche mit dem Suchbegriff `Wien Alfred Dallinger Platz`. Der Suchbegriff ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/at/FullTextSearch?searchTerm=Wien%20Alfred%20Dallinger%20Platz
```