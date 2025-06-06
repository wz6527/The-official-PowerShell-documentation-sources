---
description: Describes how to write comment-based help content for functions and scripts.
Locale: en-US
ms.date: 05/21/2025
no-loc: [.SYNOPSIS, .DESCRIPTION, .PARAMETER, .EXAMPLE, .INPUTS, .OUTPUTS, .NOTES, .LINK, .COMPONENT, .ROLE, .FUNCTIONALITY, .FORWARDHELPTARGETNAME, .FORWARDHELPCATEGORY, .REMOTEHELPRUNSPACE, .EXTERNALHELP]
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_comment_based_help?view=powershell-7.5&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Comment_Based_Help
---
# about_Comment_Based_Help

## Short description
Describes how to write comment-based help content for functions and scripts.

## Long description

You can write comment-based help content for functions and scripts by using
special help comment keywords.

The [Get-Help][06] cmdlet displays comment-based help in the same format in
which it displays the cmdlet help content that are generated from XML files.
Users can use all of the parameters of `Get-Help`, such as **Detailed**,
**Full**, **Examples**, and **Online**, to display the contents of
comment-based help.

You can also write XML-based help files for functions and scripts. To enable
the `Get-Help` cmdlet to find the XML-based help file for a function or script,
use the `.EXTERNALHELP` keyword. Without this keyword, `Get-Help` can't find
XML-based help content for functions or scripts.

This topic explains how to write help content for functions and scripts. For
information about how to display help content for functions and scripts, see
[Get-Help][06].

The [Update-Help][08] and [Save-Help][07] cmdlets work only on XML files.
Updatable Help doesn't support comment-based help content.

## Syntax for comment-based help

To create Comment-based help content, you can use either style of comments:
single-line comments or block comments.

The syntax for comment-based help is as follows:

```Syntax
# .<help keyword>
# <help content>
```

or

```Syntax
<#
    .<help keyword>
    <help content>
#>
```

Comment-based help is written as a series of comments. You can type a comment
symbol `#` before each line of comments, or you can use the `<#` and `#>`
symbols to create a comment block. All the lines within the comment block are
interpreted as comments.

All of the lines in a comment-based help topic must be contiguous. If a
comment-based help topic follows a comment that's not part of the help topic,
there must be at least one blank line between the last non-help comment line
and the beginning of the comment-based help.

Keywords define each section of comment-based help. Each comment-based help
keyword is preceded by a dot `.`. The keywords can appear in any order. The
keyword names aren't case-sensitive.

For example, the `.DESCRIPTION` keyword precedes a description of a function or
script.

```powershell
<#
.DESCRIPTION
Get-Function displays the name and syntax of all functions in the session.
#>
```

The comment block must contain at least one keyword. Some of the keywords, such
as `.EXAMPLE`, can appear many times in the same comment block. The help
content for each keyword begins on the line after the keyword and can span
multiple lines.

## Syntax for comment-based help in functions

Comment-based help for a function can appear in one of three locations:

- At the beginning of the function body.
- At the end of the function body.
- Before the `function` keyword. There can't be more than one blank line
  between the last line of the function help and the `function` keyword.

For example:

```powershell
function Get-Function {
    <#
        .<help keyword>
        <help content>
    #>

    # function logic
}
```

or

```powershell
function Get-Function {
    # function logic

    <#
        .<help keyword>
        <help content>
    #>
}
```

or

```powershell
<#
    .<help keyword>
    <help content>
#>
function Get-Function { }
```

## Syntax for comment-based help in scripts

Comment-based help for a script can appear in one of the following two
locations in the script.

- At the beginning of the script file. Script help can be preceded in the
  script only by comments and blank lines.

  If the first item in the script body (after the help) is a function
  declaration, there must be at least two blank lines between the end of the
  script help and the function declaration. Otherwise, the help is interpreted
  as being help for the function, not help for the script.

- At the end of the script file. However, if the script is signed, place
  Comment-based help at the beginning of the script file. The end of the script
  is occupied by the signature block.

For example:

```powershell
<#
.<help keyword>
<help content>
#>
function Get-Function { }
```

or

```powershell
function Get-Function { }
<#
.<help keyword>
<help content>
#>
```

## Comment-based help keywords

The following are valid comment-based help keywords. These keywords can appear
in any order in the comment-based help, and they aren't case-sensitive. The
keywords are listed in this article in the order that they typically appear
in a help topic.

### .SYNOPSIS

A brief description of the function or script. This keyword can be used
only once in each topic.

### .DESCRIPTION

A detailed description of the function or script. This keyword can be
used only once in each topic.

### .PARAMETER

The description of a parameter. Add a `.PARAMETER` keyword for each parameter
in the function or script syntax.

Type the parameter name on the same line as the `.PARAMETER` keyword. Type the
parameter description on the lines following the `.PARAMETER` keyword. Windows
PowerShell interprets all text between the `.PARAMETER` line and the next
keyword or the end of the comment block as part of the parameter description.
The description can include paragraph breaks.

```Syntax
.PARAMETER  <Parameter-Name>
```

The Parameter keywords can appear in any order in the comment block, but the
function or script syntax determines the order in which the parameters (and
their descriptions) appear in help topic. To change the order, change the
syntax.

You can also specify a parameter description by placing a comment in the
function or script syntax immediately before the parameter variable name. For
this to work, you must also have a comment block with at least one keyword.

If you use both a syntax comment and a `.PARAMETER` keyword, the description
associated with the `.PARAMETER` keyword is used, and the syntax comment is
ignored.

```powershell
<#
.SYNOPSIS
    Short description here
#>
function Verb-Noun {
    [CmdletBinding()]
    param (
        # This is the same as .PARAMETER
        [string]$ComputerName
    )
    # Verb the Noun on the computer
}
```

### `.EXAMPLE`

A sample command that uses the function or script, optionally followed by
sample output and a description. Repeat this keyword for each example.

### `.INPUTS`

The .NET types of objects that can be piped to the function or script. You can
also include a description of the input objects. Repeat this keyword for each
input type.

### `.OUTPUTS`

The .NET type of the objects that the cmdlet returns. You can also include a
description of the returned objects. Repeat this keyword for each output type.

### `.NOTES`

Additional information about the function or script.

### `.LINK`

The name of a related topic. Repeat this keyword for each related topic. This
content appears in the Related Links section of the Help topic.

The `.LINK` keyword content can also include a Uniform Resource Identifier
(URI) to an online version of the same help topic. The online version opens
when you use the **Online** parameter of `Get-Help`. The URI must begin with
`http` or `https`.

### `.COMPONENT`

The name of the technology or feature that the function or script uses, or to
which it's related. The **Component** parameter of `Get-Help` uses this value
to filter the search results returned by `Get-Help`.

### `.ROLE`

The name of the user role for the help topic. The **Role** parameter of
`Get-Help` uses this value to filter the search results returned by `Get-Help`.

### `.FUNCTIONALITY`

The keywords that describe the intended use of the function. The
**Functionality** parameter of `Get-Help` uses this value to filter the search
results returned by `Get-Help`.

### `.FORWARDHELPTARGETNAME <Command-Name>`

Redirects to the help topic for the specified command. You can redirect users
to any help topic, including help content for a function, script, cmdlet, or
provider.

```powershell
# .FORWARDHELPTARGETNAME <Command-Name>
```

### `.FORWARDHELPCATEGORY`

Specifies the help category of the item in `.FORWARDHELPTARGETNAME`. Valid
values are `Alias`, `Cmdlet`, `HelpFile`, `Function`, `Provider`, `General`,
`FAQ`, `Glossary`, `ScriptCommand`, `ExternalScript`, `Filter`, or `All`. Use
this keyword to avoid conflicts when there are commands with the same name.

```powershell
# .FORWARDHELPCATEGORY <Category>
```

### `.REMOTEHELPRUNSPACE <PSSession-variable>`

Specifies a session that contains the help topic. Enter a variable that
contains a **PSSession** object. This keyword is used by the
[Export-PSSession][09] cmdlet to find the help content for the exported
commands.

```powershell
# .REMOTEHELPRUNSPACE <PSSession-variable>
```

### `.EXTERNALHELP`

Specifies an XML-based help file for the script or function.

```powershell
# .EXTERNALHELP <XML Help File>
```

The `.EXTERNALHELP` keyword is required when a function or script is documented
in XML files. Without this keyword, `Get-Help` can't find the XML-based help
file for the function or script.

The `.EXTERNALHELP` keyword takes precedence over other comment-based help
keywords. If `.EXTERNALHELP` is present, `Get-Help` doesn't display
comment-based help, even if it can't find a help topic that matches the value
of the `.EXTERNALHELP` keyword.

If the function is exported by a module, set the value of the `.EXTERNALHELP`
keyword to a filename without a path. `Get-Help` looks for the specified file
name in a language-specific subdirectory of the module directory. There are no
requirements for the name of the XML-based help file for a function, but a best
practice is to use the following format:

```Syntax
<ScriptModule.psm1>-help.xml
```

If the function isn't included in a module, include a path to the XML-based
help file. If the value includes a path and the path contains
UI-culture-specific subdirectories, `Get-Help` searches the subdirectories
recursively for an XML file with the name of the script or function in
accordance with the language fallback standards established for Windows, just
as it does in a module directory.

For more information about the cmdlet help XML-based help file format, see
[How to Write Cmdlet Help][01].

## Autogenerated content

The name, syntax, parameter list, parameter attribute table, common parameters,
and remarks are automatically generated by the `Get-Help` cmdlet.

### Name

The **Name** section of a function help topic is taken from the function name
in the function syntax. The **Name** of a script help topic is taken from the
script filename. To change the name or its capitalization, change the function
syntax or the script filename.

### Syntax

The **Syntax** section of the help topic is generated from the function or
script syntax. To add detail to the help topic syntax, such as the .NET type of
a parameter, add the detail to the syntax. If you don't specify a parameter
type, the **Object** type is inserted as the default value.

### Parameter List

The parameter list in the help topic is generated from the function or script
syntax and from the descriptions that you add by using the `.PARAMETER`
keyword. The function parameters appear in the **Parameters** section of the
help topic in the same order that they appear in the function or script syntax.
The spelling and capitalization of parameter names is also taken from the
syntax. It isn't affected by the parameter name specified by the `.PARAMETER`
keyword.

### Common Parameters

The **Common parameters** are added to the syntax and parameter list of the
help topic, even if they have no effect. For more information about the common
parameters, see [about_CommonParameters][02].

### Parameter Attribute Table

`Get-Help` generates the table of parameter attributes that appears when you
use the **Full** or **Parameter** parameter of `Get-Help`. The value of the
**Required**, **Position**, and **Default** value attributes is taken from the
function or script syntax.

Default values and a value for **Accept Wildcard characters** don't appear in
the parameter attribute table even when they're defined in the function or
script. To help users, provide this information in the parameter description.

### Remarks

The **Remarks** section of the help topic is automatically generated from the
function or script name. You can't change or affect its content.

## Examples

### Comment-based Help for a Function

The following sample function includes comment-based help:

```powershell
function Add-Extension
{
param ([string]$Name,[string]$Extension = "txt")
$Name = $Name + "." + $Extension
$Name

<#
.SYNOPSIS

Adds a file name extension to a supplied name.

.DESCRIPTION

Adds a file name extension to a supplied name.
Takes any strings for the file name or extension.

.PARAMETER Name
Specifies the file name.

.PARAMETER Extension
Specifies the extension. "Txt" is the default.

.INPUTS

None. You can't pipe objects to Add-Extension.

.OUTPUTS

System.String. Add-Extension returns a string with the extension
or file name.

.EXAMPLE

PS> Add-Extension -Name "File"
File.txt

.EXAMPLE

PS> Add-Extension -Name "File" -Extension "doc"
File.doc

.EXAMPLE

PS> Add-Extension "File" "doc"
File.doc

.LINK

http://www.fabrikam.com/extension.html

.LINK

Set-Item
#>
}
```

The results are as follows:

```powershell
Get-Help -Name "Add-Extension" -Full
```

```Output
NAME

Add-Extension

SYNOPSIS

Adds a file name extension to a supplied name.

SYNTAX

Add-Extension [[-Name] <String>] [[-Extension] <String>]
[<CommonParameters>]

DESCRIPTION

Adds a file name extension to a supplied name. Takes any strings for the
file name or extension.

PARAMETERS

-Name
Specifies the file name.

Required?                    false
Position?                    0
Default value
Accept pipeline input?       false
Accept wildcard characters?

-Extension
Specifies the extension. "Txt" is the default.

Required?                    false
Position?                    1
Default value
Accept pipeline input?       false
Accept wildcard characters?

<CommonParameters>
This cmdlet supports the common parameters: -Verbose, -Debug,
-ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
-OutBuffer and -OutVariable. For more information, type
"Get-Help about_CommonParameters".

INPUTS
None. You can't pipe objects to Add-Extension.

OUTPUTS

System.String. Add-Extension returns a string with the extension or
file name.

Example 1

PS> Add-Extension -Name "File"
File.txt

Example 2

PS> Add-Extension -Name "File" -Extension "doc"
File.doc

Example 3

PS> Add-Extension "File" "doc"
File.doc

RELATED LINKS

http://www.fabrikam.com/extension.html
Set-Item
```

### Parameter Descriptions in Function Syntax

This example is the same as the previous one, except that the parameter
descriptions are inserted in the function syntax. This format is most useful
when the descriptions are brief.

```powershell
function Add-Extension
{
param
(

[string]
#Specifies the file name.
$Name,

[string]
#Specifies the file name extension. "Txt" is the default.
$Extension = "txt"
)

$Name = $Name + "." + $Extension
$Name

<#
.SYNOPSIS

Adds a file name extension to a supplied name.

.DESCRIPTION

Adds a file name extension to a supplied name. Takes any strings for the
file name or extension.

.INPUTS

None. You can't pipe objects to Add-Extension.

.OUTPUTS

System.String. Add-Extension returns a string with the extension or
file name.

.EXAMPLE

PS> Add-Extension -Name "File"
File.txt

.EXAMPLE

PS> Add-Extension -Name "File" -Extension "doc"
File.doc

.EXAMPLE

PS> Add-Extension "File" "doc"
File.doc

.LINK

http://www.fabrikam.com/extension.html

.LINK

Set-Item
#>
}
```

### Comment-based Help for a Script

The following sample script includes comment-based help. Notice the blank lines
between the closing `#>` and the `param` statement. In a script that doesn't
have a `param` statement, there must be at least two blank lines between the
final comment in the help topic and the first function declaration. Without
these blank lines, `Get-Help` associates the help topic with the function, not
the script.

```powershell
<#
.SYNOPSIS

Performs monthly data updates.

.DESCRIPTION

The Update-Month.ps1 script updates the registry with new data generated
during the past month and generates a report.

.PARAMETER InputPath
Specifies the path to the CSV-based input file.

.PARAMETER OutputPath
Specifies the name and path for the CSV-based output file. By default,
MonthlyUpdates.ps1 generates a name from the date and time it runs, and
saves the output in the local directory.

.INPUTS

None. You can't pipe objects to Update-Month.ps1.

.OUTPUTS

None. Update-Month.ps1 doesn't generate any output.

.EXAMPLE

PS> .\Update-Month.ps1

.EXAMPLE

PS> .\Update-Month.ps1 -InputPath C:\Data\January.csv

.EXAMPLE

PS> .\Update-Month.ps1 -InputPath C:\Data\January.csv -OutputPath `
C:\Reports\2009\January.csv
#>

param ([string]$InputPath, [string]$OutputPath)

function Get-Data { }
...
```

The following command gets the script help. Because the script isn't in a
directory that's listed in the `$Env:PATH` environment variable, the
`Get-Help` command that gets the script help must specify the script path.

```powershell
Get-Help -Name .\update-month.ps1 -Full
```

```Output
# NAME

C:\ps-test\Update-Month.ps1

# SYNOPSIS

Performs monthly data updates.

# SYNTAX

C:\ps-test\Update-Month.ps1 [-InputPath] <String> [[-OutputPath]
<String>] [<CommonParameters>]

# DESCRIPTION

The Update-Month.ps1 script updates the registry with new data
generated during the past month and generates a report.

# PARAMETERS

-InputPath
Specifies the path to the CSV-based input file.

Required?                    true
Position?                    0
Default value
Accept pipeline input?       false
Accept wildcard characters?

-OutputPath
Specifies the name and path for the CSV-based output file. By
default, MonthlyUpdates.ps1 generates a name from the date
and time it runs, and saves the output in the local directory.

Required?                    false
Position?                    1
Default value
Accept pipeline input?       false
Accept wildcard characters?

<CommonParameters>
This cmdlet supports the common parameters: -Verbose, -Debug,
-ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
-OutBuffer and -OutVariable. For more information, type,
"Get-Help about_CommonParameters".

# INPUTS

None. You can't pipe objects to Update-Month.ps1.

# OUTPUTS

None. Update-Month.ps1 doesn't generate any output.

Example 1

PS> .\Update-Month.ps1

Example 2

PS> .\Update-Month.ps1 -InputPath C:\Data\January.csv

Example 3

PS> .\Update-Month.ps1 -InputPath C:\Data\January.csv -OutputPath
C:\Reports\2009\January.csv

# RELATED LINKS
```

### Redirecting to an XML File

You can write XML-based help content for functions and scripts. Although
comment-based help is easier to implement, XML-based help is required for
Updatable Help and to provide help content in multiple languages.

The following example shows the first few lines of the Update-Month.ps1 script.
The script uses the `.EXTERNALHELP` keyword to specify the path to an XML-based
help topic for the script.

Note that the value of the `.EXTERNALHELP` keyword appears on the same line as
the keyword. Any other placement is ineffective.

```powershell
# .EXTERNALHELP C:\MyScripts\Update-Month-Help.xml

param ([string]$InputPath, [string]$OutputPath)
function Get-Data { }
...
```

The following examples show three valid placements of the `.EXTERNALHELP`
keyword in a function.

```powershell
function Add-Extension {
    # .EXTERNALHELP C:\ps-test\Add-Extension.xml

    param ([string] $Name, [string]$Extension = "txt")
    $Name = $Name + "." + $Extension
    $Name
}
```

```powershell
function Add-Extension {
    param ([string] $Name, [string]$Extension = "txt")
    $Name = $Name + "." + $Extension
    $Name

    # .EXTERNALHELP C:\ps-test\Add-Extension.xml
}
```

```powershell
# .EXTERNALHELP C:\ps-test\Add-Extension.xml
function Add-Extension {
    param ([string] $Name, [string]$Extension = "txt")
    $Name = $Name + "." + $Extension
    $Name
}
```

### Redirecting to a Different Help Topic

The following code is an excerpt from the beginning of the built-in help
function in PowerShell, which displays one screen of help text at a time.
Because the help topic for the `Get-Help` cmdlet describes the help function,
the help function uses the `.FORWARDHELPTARGETNAME` and `.FORWARDHELPCATEGORY`
keywords to redirect the user to the `Get-Help` cmdlet help topic.

```powershell
function help {
    <#
    .FORWARDHELPTARGETNAME Get-Help
    .FORWARDHELPCATEGORY Cmdlet
    #>

    [CmdletBinding(DefaultParameterSetName='AllUsersView')]
    param(
        [Parameter(Position=0, ValueFromPipelineByPropertyName=$true)]
        [System.String]
        ${Name},
    ...
```

The following command uses this feature:

```powershell
Get-Help -Name help
```

```Output
NAME

Get-Help

SYNOPSIS

Displays information about PowerShell cmdlets and concepts.
...
```

## See also

- [about_Functions][04]
- [about_Functions_Advanced_Parameters][03]
- [about_Scripts][05]
- [Writing Comment-Based help content][01]

<!-- link references -->
[01]: /powershell/scripting/developer/help/writing-comment-based-help-topics
[02]: about_CommonParameters.md
[03]: about_Functions_Advanced_Parameters.md
[04]: about_Functions.md
[05]: about_Scripts.md
[06]: xref:Microsoft.PowerShell.Core.Get-Help
[07]: xref:Microsoft.PowerShell.Core.Save-Help
[08]: xref:Microsoft.PowerShell.Core.Update-Help
[09]: xref:Microsoft.PowerShell.Utility.Export-PSSession
