---
description: Lists the reserved words that cannot be used as identifiers because they have a special meaning in PowerShell.
Locale: en-US
ms.date: 07/02/2024
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_reserved_words?view=powershell-7.6&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Reserved_Words
---
# about_Reserved_Words

## Short description

Lists the reserved words that cannot be used as identifiers because they
have a special meaning in PowerShell.

## Long description

There are certain words that have special meaning in PowerShell. When these
words appear without quotation marks, PowerShell attempts to apply their
special meaning rather than treating them as character strings. To use these
words as parameter arguments in a command or script without invoking their
special meaning, enclose the reserved words in quotation marks.

The following are the reserved words in PowerShell:

```
assembly         exit            process
base             filter          public
begin            finally         return
break            for             sequence
catch            foreach         static
class            from (*)        switch
command          function        throw
configuration    hidden          trap
continue         if              try
data             in              type
define (*)       inlinescript    until
do               interface       using
dynamicparam     module          var (*)
else             namespace       while
elseif           parallel        workflow
end              param
enum             private

(*) These keywords are reserved for future use.
```

Several language keywords, including `foreach`, `if`, `for`, and `while`, have
their own help articles. To view them, type `Get-Help about_` and add the
keyword. For example, to get information about the `foreach` statement, type:

```powershell
Get-Help about_Foreach
```

For information about the `filter` statement or the `return` statement syntax,
type:

```powershell
Get-Help about_Functions
```

For information about other reserved words, type:

```powershell
Get-Help <Reserved_Word>
```

> [!NOTE]
> Not every reserved word has its own help article. If `Get-Help` does not
> return an article, you can search for articles that talk about the reserved
> word using the following command:
>
> ```powershell
> Get-Help <Reserved_Word> -Category:HelpFile
> ```

## See also

- [about_Command_Syntax](about_Command_Syntax.md)
- [about_Language_Keywords](about_Language_Keywords.md)
- [about_Parsing](about_Parsing.md)
- [about_Quoting_Rules](about_Quoting_Rules.md)
- [about_Script_Blocks](about_Script_Blocks.md)
- [about_Special_Characters](about_Special_Characters.md)
