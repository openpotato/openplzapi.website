# Reguläre Ausdrücke

In der OpenPLZ API können Sucheingaben zu Straßennamen, Postleitzahlen oder Ortsnamen optional durch **reguläre Ausdrücke** definiert werden. Die OpenPLZ API unterstützt POSIX-Basisreguläre Ausdrücke (BRE).

## Was sind reguläre Ausdrücke?

Reguläre Ausdrücke (englisch: Regular Expressions, oft abgekürzt als Regex) sind ein Werkzeug zur Textsuche. Sie ermöglichen es, bestimmte Muster in Zeichenketten zu suchen und zu finden. Mit regulären Ausdrücken können komplexe Suchoperationen durchgeführt werden, indem man festlegt, welche Art von Zeichen oder Textstrukturen gesucht werden sollen.

## POSIX-Basisreguläre Ausdrücke

[POSIX-Basisreguläre Ausdrücke (BRE)](https://pubs.opengroup.org/onlinepubs/9799919799/) sind die traditionellere Form von regulären Ausdrücken, die in Unix-ähnlichen Betriebssystemen verwendet werden. Sie bieten eine robuste und effiziente Möglichkeit, Zeichenfolgen zu durchsuchen, abzugleichen und zu manipulieren. Im Gegensatz zu erweiterten regulären Ausdrücken (ERE) müssen viele Sonderzeichen in BRE mit einem Rückwärtsschrägstrich (`\`) maskiert werden, um ihre speziellen Bedeutungen anzunehmen. Dies führt zu einigen syntaktischen Unterschieden zwischen BRE und anderen Formen regulärer Ausdrücke.

Die BRE-Syntax ist relativ minimalistisch, mit mehreren Metazeichen und Konstrukten zur Definition von Übereinstimmungsregeln. Im Folgenden werden die grundlegenden Komponenten der BRE-Syntax behandelt.

### Literale Zeichen

Ein literales Zeichen ist einfach ein Zeichen, das sich selbst entspricht. Die meisten Zeichen werden als literale Zeichen behandelt, es sei denn, sie sind Metazeichen (z. B. `*`, `.`, `^`), die spezielle Bedeutungen haben. Um ein literales Metazeichen zu finden, müssen Sie es mit einem Rückwärtsschrägstrich (`\`) maskieren.

Beispiel:

+ `abc` stimmt genau mit der Zeichenfolge "abc" überein.

### Metazeichen und Sonderzeichen in BRE

<h4>Startanker einer Zeile</h4>

Das Caret-Symbol `^` wird verwendet, um den Anfang einer Zeile oder Zeichenfolge abzugleichen.
  
Beispiel:
  
+ `^abc` stimmt nur mit "abc" überein, wenn es am Anfang einer Zeile steht.

<h4>Ende einer Zeile</h4>

Das Dollarzeichen `$` stimmt mit dem Ende einer Zeile oder Zeichenfolge überein.
  
Beispiel:

+ `abc$` stimmt nur mit "abc" überein, wenn es am Ende einer Zeile steht.

<h4>Übereinstimmung mit einem beliebigen Zeichen</h4>

Der Punkt `.` wird verwendet, um mit einem beliebigen Zeichen außer dem Zeilenumbruch übereinzustimmen.
  
Beispiel:

+ `a.c` stimmt mit jeder dreistelligen Zeichenfolge überein, die mit "a" beginnt und mit "c" endet, wobei jedes beliebige Zeichen dazwischen liegt (z. B. "abc", "a5c").

<h4>Null oder mehr Wiederholungen</h4>

Das Sternchen `*` stimmt mit dem vorherigen Element null oder mehrmals überein.
  
Beispiel:

+ `ab*c` stimmt mit "ac", "abc", "abbc", "abbbc" usw. überein.

<h4>Übereinstimmung mit einem Zeichen aus einer Menge</h4>

Klammerausdrücke `[]` (auch bekannt als Zeichenklassen) ermöglichen es Ihnen, eine Menge von Zeichen zu definieren, mit denen Sie an einer bestimmten Position in der Zeichenfolge übereinstimmen möchten.
  
Beispiele:

+ `[abc]` stimmt mit "a", "b" oder "c" überein.
+ `[0-9]` stimmt mit jeder Ziffer zwischen 0 und 9 überein.
  
Sonderfälle bei Klammerausdrücken:

+ Ein Caret (`^`) am Anfang eines Klammerausdrucks negiert die Zeichenauswahl, was bedeutet, dass es mit jedem Zeichen außer den aufgelisteten übereinstimmt.

    Beispiel: 
	
	+ `[^abc]` stimmt mit jedem Zeichen außer "a", "b" oder "c" überein.
  
+ Ein Bindestrich (`-`) kann verwendet werden, um einen Zeichenbereich anzugeben.
    
	Beispiel: 
	
	+ `[a-z]` stimmt mit jedem Kleinbuchstaben überein.

<h4>Maskierungszeichen</h4>

In BRE verlieren Metazeichen wie `*`, `.`, `^` und `$` ihre speziellen Bedeutungen, wenn sie mit einem Rückwärtsschrägstrich `\` maskiert werden.
  
Beispiele:

+ `\*` stimmt mit einem literalen Sternchen überein.
+ `\\` stimmt mit einem literalen Rückwärtsschrägstrich überein.

### Wiederholungsoperatoren

<h4>Genau `m` Vorkommen übereinstimmen</h4>

`\{m\}` stimmt mit genau `m` Vorkommen des vorherigen Elements überein.
  
Beispiel:

+ `a\{3\}` stimmt genau mit drei Vorkommen von "a" überein (d. h. "aaa").

<h4>Zwischen `m` und `n` Vorkommen übereinstimmen</h4>

`\{m,n\}` stimmt mit zwischen `m` und `n` Vorkommen des vorherigen Elements überein.
  
Beispiel:

+ `a\{2,4\}` stimmt mit zwischen zwei und vier Vorkommen von "a" überein (d. h. "aa", "aaa" oder "aaaa").

<h4>Mindestens `m` Vorkommen übereinstimmen</h4>

`\{m,\}` stimmt mit `m` oder mehr Vorkommen des vorherigen Elements überein.
  
Beispiel:

+ `a\{2,\}` stimmt mit mindestens zwei Vorkommen von "a" überein (d. h. "aa", "aaa", "aaaa" usw.).

### Gruppierung und Rückverweise

<h4>Gruppierung</h4>

Klammern `\(` und `\)` werden verwendet, um Teile des Musters zu gruppieren. Der gruppierte Teil des Musters wird als einzelnes Element behandelt.

Beispiel:

+ `\(ab\)*` stimmt mit null oder mehr Vorkommen von "ab" überein.

<h4>Rückverweis</h4>

Ein Rückverweis bezieht sich auf einen zuvor gruppierten Unterausdruck. In BRE werden Rückverweise durch `\n` dargestellt, wobei `n` eine Zahl ist, die die `n`-te Gruppe im Muster repräsentiert. Der Rückverweis stimmt mit dem gleichen Text wie die entsprechende Gruppe überein.

Beispiel:

+ `\(abc\)\1` stimmt mit "abcabc" überein, da sich `\1` auf den ersten gruppierten Ausdruck "abc" bezieht.

### Anker

Anker in BRE werden verwendet, um Positionen und nicht Zeichen abzugleichen.

+ `^`: Stimmt mit dem Anfang einer Zeile überein.
+ `$`: Stimmt mit dem Ende einer Zeile überein.

### Maskierte Metazeichen

Einige der Metazeichen in BRE müssen maskiert werden, was sich von anderen regulären Ausdrucks-Syntaxen unterscheidet. Zum Beispiel:

+ `\{` und `\}` müssen maskiert werden, um Wiederholungen darzustellen.
+ Klammern `\(` und `\)` werden zur Gruppierung verwendet.

### Beispiele

Hier sind einige Beispiele, um zu demonstrieren, wie BRE in der Praxis funktioniert:

<h4>Datumsformat</h4>

Muster: `\([0-9]\{2\}\)\([0-9]\{2\}\)\([0-9]\{4\}\)`

Dieses Muster stimmt mit einem Datumsformat überein, bei dem:

+ Die ersten beiden Ziffern den Tag darstellen.
+ Die zweiten beiden Ziffern den Monat darstellen.
+ Die letzten vier Ziffern das Jahr darstellen.

Beispiel für eine Übereinstimmung: "25092024" (steht für 25. September 2024).

<h4>Telefonnummer</h4>

Muster: `\([0-9]\{3\}\)-[0-9]\{3\}-[0-9]\{4\}`

Dieses Muster stimmt mit einer Telefonnummer im Format `XXX-XXX-XXXX` überein, wobei `X` eine Ziffer darstellt.

Beispiel für eine Übereinstimmung: "123-456-7890".

<h4>Wiederholte Wörter</h4>

Muster: `\(Wort\)\1`

Dieses Muster stimmt mit dem Wort "Wort" überein, das zweimal hintereinander wiederholt wird, z. B. "WortWort".
