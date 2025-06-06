---
external help file: Microsoft.PowerShell.Security.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Security
ms.date: 05/15/2024
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.security/get-credential?view=powershell-7.5&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-Credential
---

# Get-Credential

## SYNOPSIS
Gets a credential object based on a user name and password.

## SYNTAX

### CredentialSet (Default)

```
Get-Credential [[-Credential] <PSCredential>] [<CommonParameters>]
```

### MessageSet

```
Get-Credential [-Message <String>] [[-UserName] <String>] [-Title <String>] [<CommonParameters>]
```

## DESCRIPTION

The `Get-Credential` cmdlet creates a credential object for a specified user name and password. You
can use the credential object in security operations.

The `Get-Credential` cmdlet prompts the user for a password or a user name and password. You can use
the **Message** parameter to specify a customized message for the prompt.

In Windows PowerShell 5.1 and earlier, Windows presents a dialog box to prompt for a user name and
password. In PowerShell 6.0 and later, the prompt is presented in the console for all platforms.

## EXAMPLES

### Example 1

```powershell
$c = Get-Credential
```

This command gets a credential object and saves it in the `$c` variable.

When you enter the command, you are prompted for a user name and password. When you enter
the requested information, the cmdlet creates a **PSCredential** object representing the credentials
of the user and saves it in the `$c` variable.

You can use the object as input to cmdlets that request user authentication, such as those with a
**Credential** parameter. However, some providers that are installed with PowerShell do not support
the **Credential** parameter.

### Example 2

```powershell
$c = Get-Credential -Credential User01
$c.Username
User01
```

This example creates a credential that includes a user name without a domain name.

The first command gets a credential with the user name User01 and stores it in the `$c` variable.
The second command displays the value of the **Username** property of the resulting credential
object.

### Example 3

```powershell
$Credential = $Host.UI.PromptForCredential(
    "Need credentials", "Please enter your user name and password.", "", "NetBiosUserName")
```

This command uses the **PromptForCredential** method to prompt the user for their user name and
password. The command saves the resulting credentials in the `$Credential` variable.

The **PromptForCredential** method is an alternative to using the `Get-Credential` cmdlet. When you
use **PromptForCredential**, you can specify the caption, messages, and user name that appear in the
prompt.

For more information, see the
[PromptForCredential](xref:System.Management.Automation.Host.PSHostUserInterface.PromptForCredential%2A)
documentation in the SDK.

### Example 4

This example demonstrates how to create a credential object identical to the one returned by
`Get-Credential`.

```powershell
$User = "Domain01\User01"
$PWord = Read-Host -Prompt 'Enter a Password' -AsSecureString
$credentialParams = @{
    TypeName = 'System.Management.Automation.PSCredential'
    ArgumentList = $User, $PWord
}
$Credential = New-Object @credentialParams
```

The first command assigns the username to the `$User` variable. Ensure the value follows
the "Domain\User" or "ComputerName\User" format.

The second command uses the `Read-Host` cmdlet to create a secure string from user input. The
**Prompt** parameter requests user input, and the **AsSecureString** parameter masks the input and
converts it to a secure string.

The third command uses the `New-Object` cmdlet to create a **PSCredential** object from the values
stored in the `$User` and `$PWord` variables.

### Example 5

```powershell
$credentialParams = @{
    Message = "Credential are required for access to the \\Server1\Scripts file share."
    UserName = "Server01\PowerUser"
}
Get-Credential @credentialParams
```

```Output
PowerShell Credential Request
Credential are required for access to the \\Server1\Scripts file share.
Password for user Server01\PowerUser:
```

This command uses the **Message** and **UserName** parameters of the `Get-Credential` cmdlet. This
command format is designed for shared scripts and functions. In this case, the message tells the
user why credentials are needed and gives them confidence that the request is legitimate.

### Example 6

```powershell
Invoke-Command -ComputerName Server01 -ScriptBlock {Get-Credential Domain01\User02}
```

```Output
PowerShell Credential Request : PowerShell Credential Request
Warning: This credential is being requested by a script or application on the SERVER01 remote
computer. Enter your credentials only if you trust the remote computer and the application or script
requesting it.

Enter your credentials.
Password for user Domain01\User02: ***************

PSComputerName     : Server01
RunspaceId         : 422bdf52-9886-4ada-ab2f-130497c6777f
PSShowComputerName : True
UserName           : Domain01\User01
Password           : System.Security.SecureString
```

This command gets a credential from the Server01 remote computer. The command uses the
`Invoke-Command` cmdlet to run a `Get-Credential` command on the remote computer. The output shows
the remote security message that `Get-Credential` includes in the authentication prompt.

## PARAMETERS

### -Credential

Specifies a user name for the credential, such as **User01** or **Domain01\User01**. The parameter
name, `-Credential`, is optional.

When you submit the command and specify a user name, you're prompted for a password. If you omit
this parameter, you're prompted for a user name and a password.

Starting in PowerShell 3.0, if you enter a user name without a domain, `Get-Credential` no longer
inserts a backslash before the name.

Credentials are stored in a [PSCredential](xref:System.Management.Automation.PSCredential) object
and the password is stored as a [SecureString](xref:System.Security.SecureString).

> [!NOTE]
> For more information about **SecureString** data protection, see
> [How secure is SecureString?](xref:System.Security.SecureString#how-secure-is-securestring).

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: CredentialSet
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Message

Specifies a message that appears in the authentication prompt. This parameter is designed for use in
a function or script. You can use the message to explain to the user why you are requesting
credentials and how they will be used.

This parameter was introduced in PowerShell 3.0.

```yaml
Type: System.String
Parameter Sets: MessageSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Title

Sets the text of the title line for the authentication prompt in the console.

This parameter was introduced in PowerShell 6.0.

```yaml
Type: System.String
Parameter Sets: MessageSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UserName

Specifies a user name. The authentication prompt requests a password for the user name. By default,
the user name is blank and the authentication prompt requests both a user name and password.

This parameter was introduced in PowerShell 3.0.

```yaml
Type: System.String
Parameter Sets: MessageSet
Aliases:

Required: False
Position: 1
Default value: None (blank)
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

You can't pipe objects to this cmdlet.

## OUTPUTS

### System.Management.Automation.PSCredential

This cmdlet returns a credential object.

## NOTES

You can use the **PSCredential** object that `Get-Credential` creates in cmdlets that request user
authentication, such as those with a **Credential** parameter.

The **Credential** parameter is not supported by all providers that are installed with PowerShell.
Beginning in PowerShell 3.0, it is supported on select cmdlets, such as the `Get-Content`
and `New-PSDrive` cmdlets.

## RELATED LINKS

[PromptForCredential](xref:System.Management.Automation.Host.PSHostUserInterface.PromptForCredential%2A)
