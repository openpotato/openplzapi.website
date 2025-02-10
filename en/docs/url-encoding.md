# URL Encoding

URLs can only contain a limited set of characters as defined in [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986). Special characters or non-ASCII characters (e.g., German umlauts) must be encoded to avoid conflicts or misinterpretation.

## What is URL Encoding?

URL encoding is a method to convert special characters in a URL into a safe format. This is essential because URLs are restricted to specific characters, such as letters (`A-Z`, `a-z`), numbers (`0-9`), and a few symbols (`-`, `_`, `.`).

Characters that do not meet this rule, such as spaces, `#`, or non-English letters (`ä`, `ë`, `à`), must be encoded. Other characters (e.g., `/`, `?`, `&`) have specific meanings in URLs and can only be used as encoded values in query parameters.

Encoding replaces each character with a combination of:

1. A **percent sign (`%`)**.
2. Two **hexadecimal digits**, representing the ASCII or UTF-8 value of the character.

For the OpenPLZ API, this primarily concerns the values and [regular expressions](regex.md) used in the URL parameters `searchTerm`, `name`, `postalCode`, and `locality`.

## Which Characters Must Be Encoded?

1. **Special Characters and Spaces:**  

    + A space becomes `%20`.  
    + `&` becomes `%26`.  
    + `=` becomes `%3D`.  
    + etc.

2. **Non-English Letters (Umlauts, Accents, etc.):**  

    + `ä` becomes `%C3%A4`.  
    + `ö` becomes `%C3%B6`.  
    + `à` becomes `%C3%A0`.  
    + `ë` becomes `%C3%AB`.  
    + etc.

3. **Other Special Symbols:**  

    + `#` becomes `%23`.  
    + `+` becomes `%2B`.  
    + `/` becomes `%2F`.  
    + etc.

!!! note "Spaces"

    A space can also be represented by a plus sign (`+`) instead of `%20`.

## Example

The following OpenPLZ API example returns all streets in `München` where the postal code starts with `808`:

+ Original: 

    ```
    GET https://openplzapi.org/de/Streets?postalcode=^808&locality=München
    ```

+ With URL encoding: 

    ```
    GET https://openplzapi.org/de/Streets?postalcode=%5E808&locality=M%C3%BCnchen
    ```
    Here, the circumflex `^` in the [regular expression](regex.md) is encoded as `%5E`, and the umlaut `ü` in "München" is encoded as `%C3%BC`.

## Tool

The following tool helps you to encode any value. To do this, type the text into the first text field and click on ‘Encode’.

<input class="md-input md-input--stretch" type="text" id="inputText" placeholder="Enter text here" oninput="handleInputChange()">

<button class="md-button" id="encodeButton" onclick="encodeText()">Encode</button>
  
You can see the URL encoded result here:
	
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

## Encoding Tables

### Latin Characters with Accents and Diacritics

Character | URL Encoding  | Character | URL Encoding
--------- | ------------- | --------- | ------------
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

### Special Characters

Character | Meaning                      | URL Encoding
--------- | ---------------------------- | ------------
Space     |                              | `%20`
!         | Exclamation mark             | `%21`
"         | Double quotation mark        | `%22`
\#        | Hash symbol                  | `%23`
$         | Dollar sign                  | `%24`
%         | Percent sign                 | `%25`
&         | Ampersand                    | `%26`
'         | Apostrophe                   | `%27`
(         | Open parenthesis             | `%28`
)         | Close parenthesis            | `%29`
\*        | Asterisk                     | `%2A`
+         | Plus sign                    | `%2B`
,         | Comma                        | `%2C`
-         | Hyphen                       | `%2D`
.         | Period                       | `%2E`
/         | Forward slash                | `%2F`
:         | Colon                        | `%3A`
;         | Semicolon                    | `%3B`
<         | Less-than sign               | `%3C`
=         | Equal sign                   | `%3D`
>         | Greater-than sign            | `%3E`
?         | Question mark                | `%3F`
@         | At sign                      | `%40`
\[        | Open square bracket          | `%5B`
\\        | Backslash                    | `%5C`
]         | Close square bracket         | `%5D`
^         | Caret (circumflex)           | `%5E`
_         | Underscore                   | `%5F`
\`        | Backtick                     | `%60`
{         | Open curly brace             | `%7B`
\|        | Vertical bar                 | `%7C`
}         | Close curly brace            | `%7D`
~         | Tilde                        | `%7E`
