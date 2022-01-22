# Apuntes Expresiones Regulares

Tablas

<pre>
Boundary Matches	Description
^	Matches the beginning of a line.
$	Matches the end of a line.
\b	Matches a word boundary.
\B	Matches a non-word boundary.
\A	Matches the beginning of the input text.
\G	Matches the end of the previous match.
\Z	Matches the end of the input text except the final terminator, if any
\z	Matches the end of the input text.
</pre>

~~~
Predefined Characters classes	Description
.	Matches any single character. May or may not match line terminators.
\d	Matches any digit from 0 to 9
\D	Matches any non-digit character [^0-9]
\s	Matches any white space character like space, tab, line break, carriage return etc.
\S	Matches any non-white space character.
\w	Matches any word character.
\W	Matches any non-word character.
~~~

~~~
Characters	Description
\\	The backslash character
\t	The tab character (‘\u0009’)
\n	The newline (line feed) character (‘\u000A’)
\r	The carriage-return character (‘\u000D’)
\f	The form-feed character (‘\u000C’)
\e	The escape character (‘\u001B’)
~~~

~~~
Characters classes	Description
[abc]	It is called the simple class.Matches a or b or c in the class.
[^abc]	Matches any character except a or b or c.
[a-zA-Z]	Matches character from a to z or A to Z. This is called a range.
[a-d[m-p]]	Matched character from from a to d or from m to p. This is known as union.
[a-z&&[def]]	Matches d or e or f. This is known as intersection(between a to z and def).
[a-z&&[^bc]]	Matches from a to z except characters b and c. This is known as subtraction.
[a-z&&[^m-p]]	Matches from a to z except from m to p. This is also know
~~~

~~~
Greedy	Reluctant	Possesive	Description
X?	X??	X?+	Matches X once, or not at all.
X*	X*?	X*+	Matches X zero or more times.
X+	X+?	X++	Matches X one or more times.
X{n}	X{n}?	X{n}+	Matches X exactly n times.
X{n,}	X{n,}?	X{n,}+	Matches X at least n times.
X{n,m}	X{n,m}?	X{n,m}+	Matches X, at least n but not more than m time.
~~~

~~~
Logical operators	Description
XY	X followed by Y
X|Y	Either X or Y
~~~

<pre>
Character       Description
    ^           Matches the beginning of the input text
    ?           Matches the previous character zero or one times
    .           Matches any single character, excluding newline
    ()          Used to group patterns
    []          Matches any character from the enclosed set of characters
    [^]         Matches any character that is not in the enclosed set of characters
    {,y}        Matches the previous character up to and including y times.
    {x,}        Matches the previous character x or more times.
    {x,y}       Matches the previous character between x and y times inclusive
    {x}         Matches the previous character exactly x times.
    *           Matches the previous character zero or more times
    \b          Matches a word boundary
    \B          Matches excluding a word boundary
    \c          Matches carriage return character
    \D          Matches any character excluding numeric digits
    \d          Matches any numeric digit
    \e          Matches escape character
    \n          Matches newline character
    \S          Matches any non-whitespace character
    \s          Matches any whitespace character
    \t          Matches tab character
    \w          Matches any alphanumeric character
    \W          Matches any non-alphanumeric character.
    +           Mathes thes previous character one or more times
    $           Matches the end of the input text
</pre>



Ejemplos de Expresiones Regulares

Para Fechas
~~~
(?<Month>\d{1,2})/(?<Day>\d{1,2})/(?<Year>(?:\d{4}|\d{2}))
~~~


Para url en concreto o determinadas
~~~
^(https://)?plataformaintegracion\.com/(GestionUsuarios|O2D|AD|Ariadna/WSColabora)$

~~~





~~~


~~~