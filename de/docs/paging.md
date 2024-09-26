# Paging

Die meisten API-Endpunkte im OpenPLZ API-Projekt implementieren das sogenannte **Paging**.

## Was ist Paging?

Paging in Web-Diensten ist eine Technik, um die Ergebnisse großer Datenmengen in kleinere, handhabbare Teile zu unterteilen. Anstatt alle Ergebnisse einer Abfrage auf einmal zu senden, wird der Inhalt in Seiten (pages) aufgeteilt, sodass ein Client sequentiell oder nach Bedarf auf verschiedene Seiten zugreifen kann.

## Warum Paging?

Beginnen wir mit einem Beispiel. Die folgende Abfrage:

```
GET https://openplzapi.org/de/Streets?locality=Berlin
```

würde ohne Paging 15335 Straßen zurückliefern. Das ist eine ganze Menge und würde den Server unverhältnismäßig belasten, die Netzwerklatenz erhöhen und die Antwortzeiten verlängern. Besser ist es, diese Daten häppchenweise, in sogenannten Seiten (pages) zu übertagen. Wie groß das Häppchen, also die Seite sein soll, kannst Du beim Aufruf konfigurieren. 

## Wie genau funktioniert Paging?

Paging wird durch spezielle URL-Parametern im API-Aufruf konfiguriert. Damit wird angegeben, welche Seite von Ergebnissen der Client sehen möchte und wie viele Ergebnisse pro Seite angezeigt werden sollen. Die URL-Parameter heißen:

1. `page`: Der Index der Seite, die angefordert wird.
2. `pageSize`: Die Anzahl der Elemente pro Seite.

Dieser Aufruf liefert die ersten 10 Adressen für Berlin zurück:

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=1&pageSize=10
```

Der nächste Aufruf liefert die folgenden 10 Adressen für Berlin zurück:

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=2&pageSize=10
```

Wird der URL-Parameter `page` beim Aufruf weggelassen, gilt der Standardwert `page=1`. Wird der URL-Parameter `pageSize` beim Aufruf weggelassen, gilt der Standardwert `pageSize=50`. Der Aufruf

```
GET https://openplzapi.org/de/Streets?locality=Berlin
```

entspricht also dem Aufruf

```
GET https://openplzapi.org/de/Streets?locality=Berlin&page=1&pageSize=50
```

Die Maximalgröße für eine Seite ist 50.

## Woher weiß ich wieviel Pages es gibt?

Bei einer erfolgreichen Antwort eines API-Aufrufs werden in den [HTTP-Response-Headers](https://developer.mozilla.org/docs/Web/HTTP/Headers) zusätzliche Informationen mitgeliefert. Schauen wir uns eine typische Response-Header-Liste an:

```
content-security-policy: default-src https: data: 'unsafe-inline' 
content-type: text/json; charset=utf-8 
date: Thu,26 Sep 2024 09:26:48 GMT 
permissions-policy: accelerometer=(),camera=(),geolocation=(),gyroscope=(),magnetometer=(),microphone=(),payment=(),usb=(),interest-cohort=() 
referrer-policy: strict-origin-when-cross-origin 
server: nginx 
strict-transport-security: max-age=2592000 
x-content-type-options: nosniff 
x-frame-options: SAMEORIGIN  
x-page: 1 
x-page-size: 10 
x-total-count: 15335 
x-total-pages: 1534 
```

Interessant sind für uns hier die letzten vier Werte:

1. `x-page`: Der Index der Seite, die angefordert wurde.
2. `x-page-size`: Die Anzahl der Elemente pro Seite.
3. `x-total-count`: Die Gesamtzahl der Elemente für diese Anfrage.
4. `x-total-pages`: Die Anzahl der Seiten für diese Anfrage.

Diese Werte werden bei allen API-Endpunkten, die Paging implementieren zurückgeliefert.

!!! note "Warum nicht im JSON-Payload?"

    Die OpenPLZ API liefert die Paging-Metadaten in den HTTP-Response-Headers zurück. Es gibt andere Implementationen, die liefern diese Information als Teil des JSON-Payloads, welcher die eigentliche Antwort repräsentiert, zurück. Wir haben uns dagegen entscheiden, weil wir nicht nur JSON sondern auch CSV als Payload-Format unterstützen.

## API-Endpunkte ohne Paging

Einige API-Endpunkte implementieren kein Paging, da die resultierende Datenmenge überschaubar ist:

+ `at/FederalProvinces`
+ `ch/Cantons`
+ `de/FederalStates`
+ `li/Communes`

