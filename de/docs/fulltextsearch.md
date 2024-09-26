# Volltextsuche

Für jedes im OpenPLZ API-Projekt unterstützte Land existiert ein spezieller API-Endpunkt zur **Volltextsuche**.

## Was ist Volltextsuche?

Die Volltextsuche in relationalen Datenbanken ermöglicht das Durchsuchen von Texten in einer oder mehreren Spalten auf der Grundlage der tatsächlichen Bedeutung der Wörter anstatt eines einfachen Zeichenfolgenabgleichs. Das Ziel ist, möglichst relevante Ergebnisse zurückzuliefern, wenn nach bestimmten Begriffen gesucht wird – ähnlich wie bei einer Suchmaschine.

Wer z.B. nach `Monchengladbach` sucht, der bekommt auch Ergebnisse zu `Mönchengladbach` zurückgeliefert. 

Zudem kann man bei der Eingabe Straße, Postleitzahl und/oder Ort in beliebiger Reihenfolge eintippen. Die Sucheingabe 

```
Berlin Pariser Platz
```

liefert das gleiche Ergebnis wie

```
Pariser Platz, Berlin
```

## Wie genau funktioniert die Volltextsuche?

Wir nutzen die Volltextsuche von PostgreSQL im Hintergrund, genauer gesagt die Funktion [`websearch_to_tsquery`](https://www.postgresql.org/docs/current/textsearch-controls.html#TEXTSEARCH-PARSING-QUERIES). Diese Funktion erlaubt die Eingabe von unformatierten Text und konvertiert diesen in das passende Zielformat für PostgreSQL:

+ Text, der nicht in Anführungszeichen steht, wird in Begriffe umgewandelt, die durch `&`-Operatoren getrennt sind, wie bei der Verarbeitung durch `plainto_tsquery`.

+ Text in "Anführungszeichen" wird in Begriffe umgewandelt, die durch `<->`-Operatoren getrennt sind, als ob sie von `phraseto_tsquery` verarbeitet würden.

+ Ein `OR` wird in den Operator `|` umgewandelt.

+ Ein Bindestrich `-` wird in den Operator `!` umgewandelt.

+ Sonstige Sonderzeichen, wie z.B. Punkt, Komma, Ausrufezeichen etc. werden ignoriert.

## Wo finde ich die Volltextsuche?

Die folgenden API-Endpunkte erlauben jeweils die Volltextsuche über Straßenname, Postleitzahl und Ortsname:

+ `at/FullTextSearch`
+ `ch/FullTextSearch`
+ `de/FullTextSearch`
+ `li/FullTextSearch`

Am besten einfach ausprobieren.



