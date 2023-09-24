**OpenPLZ API** ist ein kleines [Open Data-Projekt](https://opendatahandbook.org/guide/de/what-is-open-data/), das ein öffentliches Strassenverzeichnis für Deutschland, Österreich und die Schweiz über eine offene REST-API-Schnittstelle verfügbar macht. Folgende Daten sind abrufbar:

+ Deutschland: 
    + Straßenname 
    + Postleitzahl und Ort
    + Gemeinde (inklusive Angaben zu Kreis, Bezirk und Bundesland)
+ Österreich: 
    + Straßenname 
    + Postleitzahl und Ort
    + Gemeinde (inklusive Angaben zu Bezirk und Bundesland)
+ Schweiz: 
    + Straßenname 
    + Postleitzahl und Ort
    + Gemeinde (inklusive Angaben zu Bezirk und Kanton)

## Los geht's

Der einfachste Weg, die API zu nutzen, ist der Weg über die Kommandozeile. Wir werden in diesem Kapitel mit der Kommandozeilenanwendung [curl](https://curl.se/) arbeiten. 

Unter Linux ist `curl` in der Regel vorinstalliert. Unter Windows ist `curl` als Alias des Cmdlet [Invoke-WebRequest](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest) definiert, kann also via Powershell genutzt werden. Die hier verwendeten Befehlsfolgen variieren leicht, daher werden sie für Powershell 7 (Windows) und Bash (Linux) getrennt angegeben.

### Verwaltungseinheiten

Pro Land können subnationale Verwaltungseinheiten (z.B. Bundesländer, Schweizer Kantone, Bezirke, Kreise oder Gemeinden) abgefragt werden. Grundlage für die Filterung ist stets der offizielle Schlüssel (key) der Verwaltungseinheit.

Hier eine Beispielabfrage für die Liste der deutschen Bundesländer: 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/FederalStates' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/FederalStates' -H 'accept: text/json' | json_pp
    ```

Hier eine Beispielabfrage für die Liste aller österreichischen Gemeinden im Bundesland *Niederösterreich* (Schlüssel "3"): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/at/FederalProvinces/3/Municipalities' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/at/FederalProvinces/3/Municipalities' -H 'accept: text/json' | json_pp
    ```

Hier eine Beispielabfrage für die Liste aller schweizerischen Bezirke im Kanton *Aargau* (Schlüssel "19"): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/ch/Cantons/19/Districts' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/ch/Cantons/19/Districts' -H 'accept: text/json' | json_pp
    ```

### Postleitzahlen und Orte

Orte können an Hand ihres Namens oder ihrer Postleitzahl gesucht werden. Die Suche kann sehr flexibel mittels regulären Ausdrücken gestaltet werden. Es wird der [POSIX Regular Expressions Syntax](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions) unterstützt.

Hier eine Beispielabfrage für die deutsche Postleitzahl *13156*: 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156' -H 'accept: text/json' | json_pp
    ```

Hier eine Beispielabfrage für alle deutschen Postleitzahlen, die mit *13* beginnen: 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=^13' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=^13' -H 'accept: text/json' | json_pp
    ```

Ortsabfragen unterliegen einer Pagination, d.h. das Resultat wird in adressierbaren Datenblöcken zurückgeliefert. Standardmäßig wird nur der erste Block bzw. die erste Seite mit maximal 50 Orte zurückgeliefert. Dies kann aber durch Angabe der optionalen Parameter `page` und `pageSize` beeinflusst werden. 

Hier das erste Beispiel mit expliziter Pagination (zweite Seite mit maximal 20 Orte): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156&page=2&pageSize=20' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156&page=2&pageSize=20' -H 'accept: text/json' | json_pp
    ```

### Straßen

Straßen können an Hand ihres Namens, ihrer Postleitzahl oder ihres Ortsnamens gesucht werden. Die Suche kann sehr flexibel mittels regulären Ausdrücken gestaltet werden. Es wird der [POSIX Regular Expressions Syntax](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions) unterstützt.

Hier eine Beispielabfrage für die deutsche Straße *Grabbeallee* (gibt es nur einmal in Berlin): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee' -H 'accept: text/json' | json_pp
    ```

Hier eine Beispielabfrage für alle Straßen in Berlin, die mit *G* anfängt und mit *allee* aufhört. Der reguläre Ausruck `^G.*allee$` ist [URL-kodiert](https://emn178.github.io/online-tools/url_encode.html): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin' -H 'accept: text/json' | json_pp
    ```
	
Straßenabfragen unterliegen einer Pagination, d.h. das Resultat wird in adressierbaren Datenblöcken zurückgeliefert. Standardmäßig wird nur der erste Block bzw. die erste Seite mit maximal 50 Straßen zurückgeliefert. Dies kann aber durch Angabe der optionalen Parameter `page` und `pageSize` beeinflusst werden. 

Hier das erste Beispiel mit expliziter Pagination (zweite Seite mit maximal 20 Straßen): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee&page=2&pageSize=20' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee&page=2&pageSize=20' -H 'accept: text/json' | json_pp
    ```

## Tipps und Tricks

Um die Bildschirmausgabe von `curl` in eine Datei zu schreiben, kann der Parameter `-o` genutzt werden. Das folgende Beispiel speichert alle Kantone der Schweiz in eine JSON-formartierte Textdatei. 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/ch/Cantons' -H 'accept: text/json' -o 'cantons.json'
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/ch/Cantons' -H 'accept: text/json' -o 'cantons.json'
    ```
