Das OpenPLZ API-Datenverzeichnis für [Liechtenstein](https://de.wikipedia.org/wiki/Liechtenstein) umfasst Straßennamen, Postleitzahlen, Ortsnamen und Verwaltungseinheiten (Gemeinden).

## Verwaltungsstruktur

Die Verwaltungsstruktur Liechtensteins ist klar gegliedert und orientiert sich an der Kleinheit des Staates. Sie besteht aus wenigen, überschaubaren Ebenen, die zentral organisiert sind.

**Fürstentum**

:   Der Staat Liechtenstein als oberste Verwaltungseinheit und souveräne Instanz. Liechtenstein ist eine konstitutionelle Erbmonarchie auf demokratischer und parlamentarischer Grundlage. Die Staatsführung erfolgt durch den Fürsten und die Regierung.

**Gemeinden**

:   Die einzige untergeordnete Verwaltungsebene, bestehend aus insgesamt 11 Gemeinden. Gemeinden sind für die lokale Verwaltung zuständig und verfügen über eigene Kompetenzen in Bereichen wie Bauwesen und Infrastruktur. Jede Gemeinde wird durch einen Gemeinderat und einen Vorsteher (Bürgermeister) vertreten.

**Regionen (historische Einordnung)**

:   Informelle Gruppierungen von Gemeinden, die keine offizielle Verwaltungsebene darstellen. Liechtenstein ist traditionell in zwei historische Regionen – Oberland und Unterland – aufgeteilt, die jedoch keine administrative Bedeutung haben.

## Abfrage Gemeinden

Die 11 liechtensteinischen Gemeinden werden über den folgenden API-Endpunkt abgefragt:

!!! info ""
    
	**`openplzapi.org/li/Communes`**
    
	:    Liste aller Gemeinden in Liechtenstein

Pro Gemeinde werden folgende Attribute geliefert:

+ `key (string)`: Gemeindenummer (4-stellig)
+ `name (string)`: Amtlicher Gemeindename
+ `electoralDistrict (string)`: Name des Wahlkreises. Mögliche Werte sind:
    + `Oberland` 
    + `Unterland`

Hier eine Beispielabfrage für die komplette Liste der Gemeinden: 

``` 
GET https://openplzapi.org/li/Communes
```

## Abfrage Postleitzahlen und Orte

Die Abfrage der Postleitzahlen und Orte erfolgt über folgenden API-Endpunkt:

!!! info ""

    **`openplzapi.org/li/Localities?postalCode={Postleitzahl}&name={Ortsname}`**

    :    Sucht alle Orte, die zur Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `postalCode` und `name` können zusammen oder jeweils exklusiv genutzt werden. Beide Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

Pro Ort werden folgende Attribute geliefert:

+ `name (string)`: Name des Ortes
+ `postalcode (string)`: Postleitzahl des Ortes
+ `commune.key (string)`: Gemeindenummer (4-stellig)
+ `commune.name (string)`: Amtlicher Gemeindename

Hier eine Beispielabfrage für die Postleitzahl *9490*: 

```
GET https://openplzapi.org/li/Localities?postalCode=9490
```

Hier eine Beispielabfrage für alle deutschen Postleitzahlen, die mit *94* beginnen. Der [reguläre Ausruck](regex.md) `^94` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/li/Localities?postalCode=%5E94
```

## Abfrage Straßen

Die Abfrage der Straßen erfolgt über folgende API-Endpunkte:

!!! info ""

    **`openplzapi.org/li/Streets?name={Straßenname}&postalCode={Postleitzahl}&locality={Ortsname}`**

    :    Sucht alle Straßen, die zum Straßennamen und/oder der Postleitzahl und/oder zum Ortsnamen passen. Die Parameter `name`, `postalCode` und `locality` können zusammen oder jeweils exklusiv genutzt werden. Alle drei Parameter unterstützen auch [regulären Ausdrücke](regex.md). Die Abfrage unterliegt einem [Paging](paging.md).

    **`openplzapi.org/li/FullTextSearch?searchTerm={Suchbegriff}`**

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
+ `commune.key (string)`: Gemeindenummer (4-stellig)
+ `commune.name (string)`: Amtlicher Gemeindename

Hier eine Beispielabfrage für die Straße *Alte Landstrasse*: 

```
GET https://openplzapi.org/li/Streets?name=Alte%20Landstrasse
```

Hier eine Beispielabfrage für alle Straßen in Vaduz, die mit *Alte* anfangen und mit *strasse* aufhören. Der [reguläre Ausruck](regex.md) `^Alte.*strasse$` ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/li/Streets?name=%5EAlte.%2Astrasse%24&locality=Vaduz
```

Hier eine Volltextsuche mit dem Suchbegriff `Vaduz Alte Landstrasse`. Der Suchbegriff ist [URL-kodiert](url-encoding.md): 

```
GET https://openplzapi.org/li/FullTextSearch?searchTerm=Vaduz%20Alte%20Landstrasse
```