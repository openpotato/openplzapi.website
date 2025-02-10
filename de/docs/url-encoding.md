# URL-Kodierung

URLs dürfen nur eine begrenzte Menge an Zeichen enthalten, die in [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986) definiert sind. Sonderzeichen oder Nicht-ASCII-Zeichen (z.B. deutsche Umlaute) müssen kodiert werden, um Konflikte oder Missverständnisse zu vermeiden. 

## Was ist URL-Kodierung?

URL-Kodierung ist ein Verfahren, um spezielle Zeichen in einer URL in ein sicheres Format zu konvertieren. Das ist wichtig, weil URLs nur bestimmte Zeichen enthalten dürfen, wie Buchstaben (`A-Z`, `a-z`), Zahlen (`0-9`) und einige Symbole (`-`, `_`, `.`). 

Zeichen, die diese Regel nicht erfüllen, wie Leerzeichen, `#` oder nicht-englische Buchstaben (`ä`, `ë`, `à`), müssen kodiert werden. Andere Zeichen (z.B. `/`, `?`, `&`) haben eine feste Bedeutung für URLs und dürfen nur kodiert als Parameterwerte in einer Abfrage genutzt werden.

Bei der Kodierung wird jedes Zeichen durch eine Kombination ersetzt aus:

1. Einem **Prozentzeichen (`%`)**.
2. Zwei **hexadezimalen Ziffern**, die den ASCII- oder UTF-8-Wert des Zeichens darstellen.

Im Kontext von OpenPLZ API betrifft dies vor allem die Werte und [regulären Ausdrücke](regex.md) in den URL-Parametern `searchTerm`, `name`, `postalCode` und `locality`.

## Welche Zeichen müssen kodiert werden?

1. Sonderzeichen und Leerzeichen:

    + Ein Leerzeichen wird zu `%20`.  
    + `&` wird zu `%26`.  
    + `=` wird zu `%3D`.
    + etc.

2. Nicht-englische Buchstaben (Umlaute, Akzente usw.):

    + `ä` wird zu `%C3%A4`.  
    + `ö` wird zu `%C3%B6`.  
    + `à` wird zu `%C3%A0`.  
    + `ë` wird zu `%C3%AB`.
    + etc.

3. Andere spezielle Symbole:

    + `#` wird zu `%23`.  
    + `+` wird zu `%2B`.  
    + `/` wird zu `%2F`.
    + etc.

!!! note "Leerzeichen"

    Statt mit `%20` kann ein Leerzeichen auch durch ein Pluszeichen (`+`) repräsentiert werden. 

## Beispiel

Das folgende OpenPLZ API-Beispiel liefert alle Straßen für `München` zurück, deren Postleitzahl mit `808` beginnt:

+ Im Orginal: 
  
    ```
    GET https://openplzapi.org/de/Streets?postalcode=^808&locality=München
    ```

+ Mit URL-Kodierung: 

    ```
    GET https://openplzapi.org/de/Streets?postalcode=%5E808&locality=M%C3%BCnchen
    ```
    Hier wurden der Zirkumflex `^` des [regulären Ausdrucks](regex.md) mit `%5E` sowie der Umlaut `ü` in "München" mit `%C3%BC` kodiert.

## Werkzeug

Das folgende Werkzeug hilft dir dabei, einen beliebigen Wert zu kodieren. Tippe dazu den Text in das erste Textfeld ein und klicke auf "Kodieren".

<input class="md-input md-input--stretch" type="text" id="inputText" placeholder="Hier Text eingeben" oninput="handleInputChange()">

<button class="md-button" id="encodeButton" onclick="encodeText()">Kodieren</button>
  
Das URL-kodierte Ergebnis siehst Du hier:
	
<input class="md-input md-input--stretch" type="text" id="outputText" readonly>

<script>
  function handleInputChange() {
    const outputField = document.getElementById('outputText');
    outputField.value = '';
  }
  function encodeText() {
    const inputField = document.getElementById('inputText');
	const encodedText = encodeURIComponent(inputField.value);
    document.getElementById('outputText').value = encodedText;
  }
</script>

## Kodierungslisten

### Lateinische Zeichen mit Akzenten und Diakritika

Zeichen   | URL-Kodierung | Zeichen   | URL-Kodierung
--------- | ------------- | --------- | -------------
À         | `%C3%80`      | Á         | `%C3%81`
Â         | `%C3%82`      | Ã         | `%C3%83`
Ä         | `%C3%84`      | Å         | `%C3%85`
Æ         | `%C3%86`      | Ç         | `%C3%87`
È         | `%C3%88`      | É         | `%C3%89`
Ê         | `%C3%8A`      | Ë         | `%C3%8B`
Ì         | `%C3%8C`      | Í         | `%C3%8D`
Î         | `%C3%8E`      | Ï         | `%C3%8F`
Ð         | `%C3%90`      | Ñ         | `%C3%91`
Ò         | `%C3%92`      | Ó         | `%C3%93`
Ô         | `%C3%94`      | Õ         | `%C3%95`
Ö         | `%C3%96`      | Ø         | `%C3%98`
Ù         | `%C3%99`      | Ú         | `%C3%9A`
Û         | `%C3%9B`      | Ü         | `%C3%9C`
Ý         | `%C3%9D`      | Þ         | `%C3%9E`
ß         | `%C3%9F`      | à         | `%C3%A0`
á         | `%C3%A1`      | â         | `%C3%A2`
ã         | `%C3%A3`      | ä         | `%C3%A4`
å         | `%C3%A5`      | æ         | `%C3%A6`
ç         | `%C3%A7`      | è         | `%C3%A8`
é         | `%C3%A9`      | ê         | `%C3%AA`
ë         | `%C3%AB`      | ì         | `%C3%AC`
í         | `%C3%AD`      | î         | `%C3%AE`
ï         | `%C3%AF`      | ð         | `%C3%B0`
ñ         | `%C3%B1`      | ò         | `%C3%B2`
ó         | `%C3%B3`      | ô         | `%C3%B4`
õ         | `%C3%B5`      | ö         | `%C3%B6`
ø         | `%C3%B8`      | ù         | `%C3%B9`
ú         | `%C3%BA`      | û         | `%C3%BB`
ü         | `%C3%BC`      | ý         | `%C3%BD`
þ         | `%C3%BE`      | ÿ         | `%C3%BF`

### Sonderzeichen

Zeichen     | Bedeutung                    | URL-Kodierung
----------- | ---------------------------- | -------------
Leerzeichen |                              | `%20`
!           | Ausrufezeichen               | `%21`
"           | Anführungszeichen (doppelt)  | `%22`
\#          | Hash-Zeichen                 | `%23` 
$           | Dollar-Zeichen               | `%24`
%           | Prozentzeichen               | `%25`
&           | Kaufmännisches Und           | `%26`
'           | Apostroph                    | `%27`
(           | Klammer auf                  | `%28`
)           | Klammer zu                   | `%29`
\*          | Sternchen                    | `%2A`
+           | Pluszeichen                  | `%2B`
,           | Komma                        | `%2C`
-           | Bindestrich                  | `%2D`
.           | Punkt                        | `%2E`
/           | Schrägstrich                 | `%2F`
:           | Doppelpunkt                  | `%3A`
;           | Semikolon                    | `%3B`
<           | Kleiner-als-Zeichen          | `%3C`
=           | Gleichheitszeichen           | `%3D`
>           | Größer-als-Zeichen           | `%3E`
?           | Fragezeichen                 | `%3F`
@           | At-Zeichen                   | `%40`
\[          | Eckige Klammer auf           | `%5B`
\\          | Rückschrägstrich             | `%5C`
]           | Eckige Klammer zu            | `%5D`
^           | Zirkumflex                   | `%5E`
_           | Unterstrich                  | `%5F`
\`          | Backtick                     | `%60`
{           | Geschweifte Klammer auf      | `%7B`
\|          | Vertikaler Strich            | `%7C`
}           | Geschweifte Klammer zu       | `%7D`
~           | Tilde                        | `%7E`
