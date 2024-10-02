# Regular Expressions

In the OpenPLZ API, search entries for street names, postcodes or place names can optionally be defined using **regular expressions**. The OpenPLZ API supports POSIX base regular expressions (BRE).

## What are regular expressions?

Regular expressions (often abbreviated as regex) are a text search tool. They make it possible to search for and find specific patterns in character strings. Regular expressions can be used to perform complex search operations by specifying the type of characters or text structures to be searched for.

## POSIX Basic Regular Expressions

[POSIX Basic Regular Expressions (BRE)](https://pubs.opengroup.org/onlinepubs/9799919799/) are the more traditional form of regular expressions used in Unix-like operating systems. They provide a robust and efficient way to search, match and manipulate strings. In contrast to extended regular expressions (ERE), many special characters in BRE must be escaped with a backslash (`\`) to take on their special meanings. This leads to some syntactic differences between BRE and other forms of regular expressions.

BRE syntax is relatively minimalist, with several metacharacters and constructs to define matching rules. The basic components of BRE syntax are discussed below.

### Literal characters

A literal character is simply a character that matches itself. Most characters are treated as literal characters unless they are metacharacters (e.g. `*`, `.`, `^`) that have special meanings. To find a literal meta character, you must escape it with a backslash (`\`).

Example:

+ `abc` matches the character string "abc" exactly.

### Meta characters and special characters in BRE

<h4>Start anchor of a line</h4>

The caret symbol `^` is used to match the start of a line or character string.
  
Example:
  
+ `^abc` only matches "abc" if it is at the start of a line.

<h4>End of a line</h4>

The dollar sign `$` matches the end of a line or string.
  
Example:

+ `abc$` only matches "abc" if it is at the end of a line.

<h4>Matches any character</h4>

The full stop `.` is used to match any character except the line break.
  
Example:

+ `a.c` matches any three-character string beginning with "a" and ending with "c", with any character in between (e.g. "abc", "a5c").

<h4>Null or more repetitions</h4>

The asterisk `*` matches the previous element zero or more times.
  
Example:

+ `ab*c` matches "ac", "abc", "abbc", "abbbc" etc.

<h4>Matches a character from a set</h4>

Parenthesis expressions `[]` (also known as character classes) allow you to define a set of characters that you want to match at a specific position in the string.
  
Examples:

+ `[abc]` matches "a", "b" or "c".
+ `[0-9]` matches any digit between 0 and 9.
  
Special cases for expressions in brackets:

+ A caret (`^`) at the beginning of a parenthesis expression negates the character selection, meaning that it matches any character except those listed.

    Example: 
	
	+ `[^abc]` matches any character except "a", "b" or "c".
  
+ A hyphen (`-`) can be used to specify a range of characters.
    
	Example: 
	
	+ `[a-z]` matches any lowercase letter.

<h4>Masking characters</h4>

In BRE, meta characters such as `*`, `.`, `^` and `$` lose their special meanings if they are escaped with a backslash `\`.
  
Examples:

+ `\*` matches a literal asterisk.
+ `\\` matches a literal backslash.

### Repetition operators

<h4>Exactly match `m` occurrences</h4>

`\{m\}` matches exactly `m` occurrences of the previous element.
  
Example:

+ `a\{3\}` matches exactly three occurrences of "a" (i.e. "aaa").

<h4>Match between `m` and `n` occurrences</h4>

`\{m,n\}` matches between `m` and `n` occurrences of the previous element.
  
Example:

+ `a\{2,4\}` matches between two and four occurrences of "a" (i.e. "aa", "aaa" or "aaaa").

<h4>Match at least `m` occurrences</h4>

`\{m,\}` matches `m` or more occurrences of the previous element.
  
Example:

+ `a\{2,\}` matches at least two occurrences of "a" (i.e. "aa", "aaa", "aaaa" etc.).

### Grouping and back-references

<h4>Grouping</h4>

Brackets `\(` and `\)` are used to group parts of the pattern. The grouped part of the pattern is treated as a single element.

Example:

+ `\(ab\)*` matches zero or more occurrences of "ab".

<h4>Back reference</h4>

A backreference refers to a previously grouped sub-expression. In BRE, backreferences are represented by `\n`, where `n` is a number representing the `n`th group in the pattern. The backreference matches the same text as the corresponding group.

Example:

+ `\(abc\)\1` matches "abcabc", as `\1` refers to the first grouped expression "abc".

### Anchors

Anchors in BRE are used to match positions and not characters.

+ `^`: Matches the beginning of a line.
+ `$`: Matches the end of a line.

### Masked meta characters

Some of the metacharacters in BRE must be escaped, which is different from other regular expression syntaxes. For example:

+ `\{` and `\}` must be escaped to represent repetitions.
+ Brackets `\(` and `\)` are used for grouping.

### Examples

Here are some examples to demonstrate how BRE works in practice:

<h4>Date format</h4>

Muster: `\([0-9]\{2\}\)\([0-9]\{2\}\)\([0-9]\{4\}\)`

This pattern matches a date format where:

+ The first two digits represent the day.
+ The second two digits represent the month.
+ The last four digits represent the year.

Example of a match: "25092024" (stands for 25 September 2024).

<h4>Phone number</h4>

Muster: `\([0-9]\{3\}\)-[0-9]\{3\}-[0-9]\{4\}`

This pattern matches a phone number in the format `XXX-XXX-XXXX`, where `X` is a digit.

Example of a match: "123-456-7890".

<h4>Repeated words</h4>

Pattern: `\(word\)\1`

This pattern matches the word "word" repeated twice in a row, e.g. "wordword".
