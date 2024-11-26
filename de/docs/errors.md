# Fehlermeldungen

Die OpenPLZ API liefert Fehlermeldungen als RFC 9457-formatierte JSON-Objekte zurück.

## Was ist RFC 9457?

[RFC 9457](https://www.rfc-editor.org/rfc/rfc9457) ist ein Standard der Internet Engineering Task Force (IETF), der ein strukturiertes Format zur Darstellung von Fehlern in HTTP-APIs definiert. 

## Problem Details

Im Zentrum von RFC 9457 steht das *Problem Details*-Objekt, ein JSON-Dokument, das bei Fehlern im Response-Body der API-Abfrage enthalten ist. OpenPLZ API implementiert es mit folgenden Feldern:

`type` (string)

:   Eine URI-Referenz, die den Typ des Fehlers identifiziert. Dies ist in der Regel ein Verweis auf die Spezifikation des HTTP-Statuscodes im Web.

    Beispiel: `"https://tools.ietf.org/html/rfc9110#section-15.5.1"`

`title` (string)

:   Eine kurze, menschenlesbare Zusammenfassung des Problems.

    Beispiel: `"One or more validation errors occurred."`

`status` (integer)

:   Der HTTP-Statuscode, der den Fehler beschreibt. Er sollte mit dem Statuscode im HTTP-Response-Header übereinstimmten.

    Beispiel: 400

`errors` (object)

:   (Optional) Eine JSON-Objekt mit weiteren Details zum Fehler.
   
    Beispiel: 
	```
	{
		"pageSize": [
		  "The field pageSize must be between 1 and 50."
		]
	}
	```

`traceId` (string)

:   Ein eindeutiger Identifikator, der zur Nachverfolgung in verteilten Systemen genutzt werden kann.

    Beispiel: `"00-abc123def456789ghi-xyz987uvw654321tqr-01"`

!!! note "Extension Members"

    Die Felder `type`, `title` und `status` sind wohldefiniert in RFC 9457. Die Felder `errors` und `traceId` sind sogenannte *Extension Members*, also eine Erweiterung der Standardfelder.

## Beispiel

Der API-Aufruf

``` 
https://openplzapi.org/de/Streets?name=Pariser%20Platz&locality=Berlin&page=1&pageSize=99
``` 

resultiert in folgender Fehlermeldung:

``` json
{
  "type": "https://tools.ietf.org/html/rfc9110#section-15.5.1",
  "title": "One or more validation errors occurred.",
  "status": 400,
  "errors": {
    "pageSize": [
      "The field pageSize must be between 1 and 50."
    ]
  },
  "traceId": "00-0274bb16dcdf462bf27a7faedeacc79f-05c5cd5b5d411f8e-00"
}
```

Die Analyse des Fehlers:

+ Der Server kann die Anfrage nicht bearbeiten, da der Aufruf nicht korrekt formuliert ist (HTTP-Fehler-Code 400: Bad Request).

+ Offensichtlich ist etwas bei der Validierung der Aufrufparameter passiert ("One or more validation errors occurred.").

+ Und ja, so ist es auch, der Parameter `pageSize` hat einen Wert (99) außerhalb der Gültigkeit (nur von 1-50).
