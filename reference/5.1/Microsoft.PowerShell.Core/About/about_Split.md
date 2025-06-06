---
description: Explains how to use the Split operator to split one or more strings into substrings.
Locale: en-US
ms.date: 01/09/2025
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_split?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Split
---
# about_Split

## Short description

Explains how to use the Split operator to split one or more strings into
substrings.

## Long description

The Split operator splits one or more strings into substrings. You can
change the following elements of the Split operation:

- Delimiter. The default is whitespace, but you can specify characters,
  strings, patterns, or script blocks that specify the delimiter. The Split
  operator in PowerShell uses a regular expression in the delimiter,
  rather than a simple character.
- Maximum number of substrings. The default is to return all substrings. If
  you specify a number less than the number of substrings, the remaining
  substrings are concatenated in the last substring.
- Options that specify the conditions under which the delimiter is matched,
  such as SimpleMatch and Multiline.

## Syntax

The following diagram shows the syntax for the -split operator.

The parameter names do not appear in the command. Include only the parameter
values. The values must appear in the order specified in the syntax diagram.

```
-split <String>
-split (<String[]>)
<String> -split <Delimiter>[,<Max-substrings>[,"<Options>"]]
<String> -split {<ScriptBlock>} [,<Max-substrings>]
```

You can substitute `-isplit` or `-csplit` for `-split` in any binary Split
statement (a Split statement that includes a delimiter or script block). The
`-isplit` and `-split` operators are case-insensitive. The `-csplit` operator
is case-sensitive, meaning that case is considered when the delimiter rules
are applied.

## Parameters

### \<String\> or \<String[]\>

Specifies one or more strings to be split. If you submit multiple strings, all
the strings are split using the same delimiter rules.

Example:

```
-split "red yellow blue green"
red
yellow
blue
green
```

### \<Delimiter\>

The characters that identify the end of a substring. The default delimiter is
whitespace, including spaces and non-printable characters, such as newline
(\`n) and tab (\`t). When the strings are split, the delimiter is omitted from
all the substrings. Example:

```powershell
"Lastname:FirstName:Address" -split ":"
Lastname
FirstName
Address
```

By default, the delimiter is omitted from the results. To preserve all or part
of the delimiter, enclose in parentheses the part that you want to preserve.
If the `<Max-substrings>` parameter is added, this takes precedence when your
command splits up the collection. If you opt to include a delimiter as part of
the output, the command returns the delimiter as part of the output; however,
splitting the string to return the delimiter as part of output does not count
as a split.

Examples:

```powershell
"Lastname:FirstName:Address" -split "(:)"
Lastname
:
FirstName
:
Address

"Lastname/:/FirstName/:/Address" -split "/(:)/"
Lastname
:
FirstName
:
Address
```

### `<Max-substrings>`

Specifies the maximum number of substrings returned by the split operation. The
default is all substrings split by the delimiter. If there are more
substrings, they are concatenated to the final substring. If there are fewer
substrings, all substrings are returned. A value of 0 returns all the
substrings.

Example:

```powershell
$c = "Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune"
$c -split ",", 5
```

```Output
Mercury
Venus
Earth
Mars
Jupiter,Saturn,Uranus,Neptune
```

If you submit more than one string (an array of strings) to the `-split`
operator, the `Max-substrings` limit is applied to each string separately.

```powershell
$c = 'a,b,c','1,2,3,4,5'
$c -split ',', 3

a
b
c
1
2
3,4,5
```

`<Max-substrings>` does not specify the maximum number of objects that are
returned. In the following example, `<Max-substrings>` is set to 3.
This results in three substring values, but a total of five strings
in the resulting output. The delimiter is included after the splits until the
maximum of three substrings is reached. Additional delimiters in the final
substring become part of the substring.

```powershell
'Chocolate-Vanilla-Strawberry-Blueberry' -split '(-)', 3
```

```Output
Chocolate
-
Vanilla
-
Strawberry-Blueberry
```

Negative values return the amount of substrings requested starting
from the end of the input string.

> [!NOTE]
> Support for negative values was added in PowerShell 7.

```powershell
$c = "Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune"
$c -split ",", -5
```

```Output
Mercury,Venus,Earth,Mars
Jupiter
Saturn
Uranus
Neptune
```

### \<ScriptBlock\>

An expression that specifies rules for applying the delimiter. The expression
must evaluate to $true or $false. Enclose the script block in braces.

Example:

```powershell
$c = "Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune"
$c -split {$_ -eq "e" -or $_ -eq "p"}
```

```Output
M
rcury,V
nus,
arth,Mars,Ju
it
r,Saturn,Uranus,N

tun
```

### \<Options\>

Enclose the option name in quotation marks. Options are valid only when the
\<Max-substrings\> parameter is used in the statement.

The syntax for the Options parameter is:

```
"SimpleMatch [,IgnoreCase]"

"[RegexMatch] [,IgnoreCase] [,CultureInvariant]
[,IgnorePatternWhitespace] [,ExplicitCapture]
[,Singleline | ,Multiline]"
```

The SimpleMatch options are:

- **SimpleMatch**: Use simple string comparison when evaluating the
  delimiter. Cannot be used with RegexMatch.
- **IgnoreCase**: Forces case-insensitive matching, even if the -csplit
  operator is specified.

The RegexMatch options are:

- **RegexMatch**: Use regular expression matching to evaluate the
  delimiter. This is the default behavior. Cannot be used with
  SimpleMatch.
- **IgnoreCase**: Forces case-insensitive matching, even if the -csplit
  operator is specified.
- **CultureInvariant**: Ignores cultural differences in language when
  evaluating the delimiter. Valid only with RegexMatch.
- **IgnorePatternWhitespace**: Ignores unescaped whitespace and comments marked
  with the hash character (`#`). Valid only with RegexMatch.
- **Multiline**: Multiline mode forces `^` and `$` to match the beginning end
  of every line instead of the beginning and end of the input string.
- **Singleline**: Singleline mode treats the input string as a *SingleLine*. It
  forces the `.` character to match every character (including newlines),
  instead of matching every character EXCEPT the newline `\n`.
- **ExplicitCapture**: Ignores non-named match groups so that only explicit
  capture groups are returned in the result list. Valid only with RegexMatch.

## UNARY and BINARY SPLIT OPERATORS

The unary split operator (`-split <string>`) has higher precedence than a
comma. As a result, if you submit a comma-separated list of strings to the
unary split operator, only the first string (before the first comma) is split.

Use one of the following patterns to split more than one string:

- Use the binary split operator (\<string[]\> -split \<delimiter\>)
- Enclose all the strings in parentheses
- Store the strings in a variable then submit the variable to the split
  operator

Consider the following example:

```
PS> -split "1 2", "a b"
1
2
a b
```

```
PS> "1 2", "a b" -split " "
1
2
a
b
```

```
PS> -split ("1 2", "a b")
1
2
a
b
```

```
PS> $a = "1 2", "a b"
PS> -split $a
1
2
a
b
```

## Examples

The following statement splits the string at whitespace.

```powershell
-split "Windows PowerShell 2.0`nWindows PowerShell with remoting"
```

```Output

Windows
PowerShell
2.0
Windows
PowerShell
with
remoting
```

The following statement splits the string at any comma.

```powershell
"Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune" -split ','
```

```Output
Mercury
Venus
Earth
Mars
Jupiter
Saturn
Uranus
Neptune
```

The following statement splits the string at the pattern "er".

```powershell
"Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune" -split 'er'
```

```Output
M
cury,Venus,Earth,Mars,Jupit
,Saturn,Uranus,Neptune
```

The following statement performs a case-sensitive split at the letter "N".

```powershell
"Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune" -csplit 'N'
```

```Output
Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,
eptune
```

The following statement splits the string at "e" and "t".

```powershell
"Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune" -split '[et]'
```

```Output
M
rcury,V
nus,
ar
h,Mars,Jupi

r,Sa
urn,Uranus,N
p
un
```

The following statement splits the string at "e" and "r", but limits the
resulting substrings to six substrings.

```powershell
"Mercury,Venus,Earth,Mars,Jupiter,Saturn,Uranus,Neptune" -split '[er]', 6
```

```Output
M

cu
y,V
nus,
arth,Mars,Jupiter,Saturn,Uranus,Neptune
```

The following statement splits a string into three substrings.

```powershell
"a,b,c,d,e,f,g,h" -split ",", 3
```

```Output
a
b
c,d,e,f,g,h
```

The following statement splits a string into three substrings
starting from the end of the string.

```powershell
"a,b,c,d,e,f,g,h" -split ",", -3
```

```Output
a,b,c,d,e,f
g
h
```

The following statement splits two strings into three substrings.
(The limit is applied to each string independently.)

```powershell
"a,b,c,d", "e,f,g,h" -split ",", 3
```

```Output
a
b
c,d
e
f
g,h
```

The following statement splits each line in the here-string at the first
digit. It uses the Multiline option to recognize the beginning of each line
and string.

The 0 represents the "return all" value of the Max-substrings parameter. You
can use options, such as Multiline, only when the Max-substrings value is
specified.

```powershell
$a = @'
1The first line.
2The second line.
3The third of three lines.
'@
$a -split "^\d", 0, "Multiline"
```

```Output

The first line.

The second line.

The third of three lines.
```

The following statement uses the backslash character to escape the dot (.)
delimiter.

With the default, RegexMatch, the dot enclosed in quotation marks (".") is
interpreted to match any character except for a newline character. As a
result, the Split statement returns a blank line for every character except
newline.

```powershell
"This.is.a.test" -split "\."
```

```Output
This
is
a
test
```

The following statement uses the SimpleMatch option to direct the -split
operator to interpret the dot (.) delimiter literally.

The 0 represents the "return all" value of the Max-substrings parameter. You
can use options, such as SimpleMatch, only when the Max-substrings value is
specified.

```powershell
"This.is.a.test" -split ".", 0, "SimpleMatch"
```

```Output
This
is
a
test
```

The following statement splits the string at one of two delimiters, depending
on the value of a variable.

```powershell
$i = 1
$c = "LastName, FirstName; Address, City, State, Zip"
$c -split $(if ($i -lt 1) {","} else {";"})
```

```Output
LastName, FirstName
 Address, City, State, Zip
```

## See also

- [Split-Path](xref:Microsoft.PowerShell.Management.Split-Path)
- [about_Operators](about_Operators.md)
- [about_Comparison_Operators](about_Comparison_Operators.md)
- [about_Join](about_Join.md)
