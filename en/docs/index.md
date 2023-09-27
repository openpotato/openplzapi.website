**OpenPLZ API** is a small [Open Data project](https://opendatahandbook.org/guide/de/what-is-open-data/) that makes a public street directory for Germany, Austria and Switzerland available via an open REST API interface. The following data can be retrieved:

+ Germany: 
    + Street name 
    + Postal code and locality 
    + Municipality (including details of district, government region and federal state)
+ Austria: 
    + Street name 
    + Postal code and locality 
    + Municipality (including details of district and federal province)
+ Switzerland: 
    + Street name 
    + Postal code and locality 
    + Municipality (including details of district and canton)

## Lets's start

The easiest way to use the API is via the command line. We will work with the command line application [curl](https://curl.se/) in this chapter. 

Under Linux, `curl` is usually pre-installed. Under Windows, `curl` is defined as an alias of the [Invoke-WebRequest](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest) cmdlet, so it can be used via Powershell. The command sequences used here vary slightly, so they are given separately for Powershell 7 (Windows) and Bash (Linux).

### Administrative units

Subnational administrative units (e.g. federal states, Swiss cantons, districts or municipalities) can be queried per country. The basis for filtering is always the official key of the administrative unit.

Here is an example query for the list of German federal states: 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/FederalStates' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/FederalStates' -H 'accept: text/json' | json_pp
    ```

Here is an example query for the list of all Austrian municipalities in the federal province of *Niederösterreich* (key "3"): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/at/FederalProvinces/3/Municipalities' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/at/FederalProvinces/3/Municipalities' -H 'accept: text/json' | json_pp
    ```

Here is an example query for the list of all Swiss districts in the canton of *Aargau* (key "19"): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/ch/Cantons/19/Districts' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/ch/Cantons/19/Districts' -H 'accept: text/json' | json_pp
    ```

### Postal codes and localities

Localities can be searched by name or postal code. The search can be designed very flexibly using regular expressions. The [POSIX Regular Expressions Syntax](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions) is supported.

Here is an example query for the German postal code *13156*: 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCodePattern=13156' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCodePattern=13156' -H 'accept: text/json' | json_pp
    ```

Here is an example query for all German postal codes beginning with *13*:  

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCodePattern=^13' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCodePattern=^13' -H 'accept: text/json' | json_pp
    ```

Queries for localities are subject to pagination, i.e. the result is returned in addressable data blocks. By default, only the first block or the first page with a maximum of 50 localities is returned. However, this can be influenced by specifying the optional parameters `page` and `pageSize`. 

Here is the first example with explicit pagination (second page with a maximum of 20 localities): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156&page=2&pageSize=20' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Localities?postalCode=13156&page=2&pageSize=20' -H 'accept: text/json' | json_pp
    ```

### Streets

Streets can be searched by name, postal code or locality name. The search can be designed very flexibly using regular expressions. The [POSIX Regular Expressions Syntax](https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions) is supported.

Here is an example query for the German street *Grabbeallee* (exists only once in Berlin): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?namePattern=Grabbeallee' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?namePattern=Grabbeallee' -H 'accept: text/json' | json_pp
    ```

Here is an example query for all streets in Berlin, starting with *G* and ending with *allee*. The regular expression `^G.*allee$` is [URL encoded](https://emn178.github.io/online-tools/url_encode.html): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?name=%5EG.*allee%24&locality=Berlin' -H 'accept: text/json' | json_pp
    ```

Queries for streets are subject to pagination, i.e. the result is returned in addressable data blocks. By default, only the first block or the first page with a maximum of 50 streets is returned. However, this can be influenced by specifying the optional parameters `page` and `pageSize`. 

Here is the first example with explicit pagination (second page with a maximum of 20 streets): 

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee&page=2&pageSize=20' -H 'accept: text/json' | ConvertFrom-Json | ConvertTo-Json
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/de/Streets?name=Grabbeallee&page=2&pageSize=20' -H 'accept: text/json' | json_pp
    ```

## Tips and tricks

To write the screen output of curl to a file, the parameter -o can be used. The following example saves all Swiss cantons into a JSON-formatted text file.

=== "Powershell 7"

    ``` powershell
    curl -X GET 'https://openplzapi.org/ch/Cantons' -H 'accept: text/json' -o 'cantons.json'
    ```

=== "Bash"

    ``` bash
    curl -X GET 'https://openplzapi.org/ch/Cantons' -H 'accept: text/json' -o 'cantons.json'
    ```

