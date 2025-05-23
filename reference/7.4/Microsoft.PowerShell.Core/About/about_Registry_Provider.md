---
description: Registry
Locale: en-US
ms.date: 07/31/2024
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_registry_provider?view=powershell-7.4&WT.mc_id=ps-gethelp
schema: 2.0.0
title: about_Registry_Provider
---
# about_Registry_Provider

## Provider name

Registry

## Drives

`HKLM:`, `HKCU:`

## Capabilities

**ShouldProcess**, **UseTransactions**

## Short description

Provides access to the registry keys, entries, and values in PowerShell.

## Detailed description

> This information only applies to PowerShell running on Windows.

The PowerShell **Registry** provider lets you get, add, change, clear, and
delete registry keys, entries, and values in PowerShell.

The **Registry** drives are a hierarchical namespace containing the registry
keys and subkeys on your computer. Registry entries and values aren't
components of that hierarchy. Instead, they're properties of each of the keys.

The **Registry** provider supports the following cmdlets:

- [Get-Location][13]
- [Set-Location][23]
- [Get-Item][10]
- [Get-ChildItem][09]
- [Invoke-Item][14]
- [Move-Item][15]
- [New-Item][17]
- [Remove-Item][19]
- [Clear-ItemProperty][06]
- [Get-ItemProperty][11]
- [New-ItemProperty][18]
- [Remove-ItemProperty][20]
- [Set-ItemProperty][22]
- [Get-Acl][24]
- [Set-Acl][25]

## Types exposed by this provider

The **Registry** provider returns registry data in one of two types:

- [Microsoft.Win32.RegistryKey][01] for registry keys
- [PSCustomObject][02] for registry values

## Navigating the Registry drives

The **Registry** provider exposes its data store as two default drives.

- `HKLM:` maps to the `HKEY_LOCAL_MACHINE` registry hive
- `HKCU:` maps to the `HKEY_CURRENT_USER` registry hive

To work with the registry, you can change your location to the `HKLM:` drive
using the following command.

```powershell
Set-Location HKLM:
```

To return to a file system drive, type the drive name. For example, type:

```powershell
Set-Location C:
```

You can also work with the **Registry** provider from any other PowerShell
drive. To reference a registry key from another location, use the drive name
(`HKLM:`, `HKCU:`) in the path. Use a backslash (`\`) or a forward slash (`/`)
to indicate a level of the **Registry** drive.

```powershell
PS C:\> cd HKLM:\Software
```

> [!NOTE]
> PowerShell uses aliases to allow you a familiar way to work with provider
> paths. Commands such as `dir` and `ls` are aliases for [Get-ChildItem][09],
> `cd` is an alias for [Set-Location][23], and `pwd` is an alias for
> [Get-Location][13].

This last example shows another path syntax you can use to navigate the
**Registry** provider. This syntax uses the provider name, followed by two
colons `::`. This syntax allows you to use the full HIVE name, instead of the
mapped drive name `HKLM`.

```powershell
cd "Registry::HKEY_LOCAL_MACHINE\Software"
```

## Displaying the contents of registry keys

The registry is divided into keys, subkeys, and entries. For more information
about registry structure, see [Structure of the Registry][03].

In a **Registry** drive, each key is a container. A key can contain any number
of keys. A registry key that has a parent key is called a subkey. You can
use `Get-ChildItem` to view registry keys and `Set-Location` to navigate to
a key path.

Registry values are attributes of a registry key. In the **Registry** drive,
they're called **Item Properties**. A registry key can have both children keys
and item properties.

In this example, the difference between `Get-Item` and `Get-ChildItem` is
shown. When you use `Get-Item` on the "Spooler" registry key, you can view its
properties.

```powershell
Get-Item -Path HKLM:\SYSTEM\CurrentControlSet\Services\Spooler
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services


Name        Property
----        --------
Spooler     DependOnService    : {RPCSS, http}
            Description        : @%systemroot%\system32\spoolsv.exe,-2
            DisplayName        : @%systemroot%\system32\spoolsv.exe,-1
            ErrorControl       : 1
            FailureActions     : {16, 14, 0, 0...}
            Group              : SpoolerGroup
            ImagePath          : C:\WINDOWS\System32\spoolsv.exe
            ObjectName         : LocalSystem
            RequiredPrivileges : {SeTcbPrivilege, SeImpersonatePrivilege, ...
            ServiceSidType     : 1
            Start              : 2
            Type               : 27
```

Each registry key can also have subkeys. When you use `Get-Item` on a registry
key, the subkeys aren't displayed. The `Get-ChildItem` cmdlet shows you subkeys
of the "Spooler" key, including each subkey's properties. The parent keys
properties aren't shown when using `Get-ChildItem`.

```powershell
Get-ChildItem -Path HKLM:\SYSTEM\CurrentControlSet\Services\Spooler
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Spooler


Name             Property
----             --------
Performance      Close           : PerfClose
                 Collect         : PerfCollect
                 Collect Timeout : 2000
                 Library         : C:\Windows\System32\winspool.drv
                 Object List     : 1450
                 Open            : PerfOpen
                 Open Timeout    : 4000
Security         Security : {1, 0, 20, 128...}
```

The `Get-Item` cmdlet can also be used on the current location. The following
example navigates to the "Spooler" registry key and gets the item properties.
The dot `.` is used to indicate the current location.

```powershell
cd HKLM:\System\CurrentControlSet\Services\Spooler
Get-Item .
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services

Name             Property
----             --------
Spooler          DependOnService    : {RPCSS, http}
                 Description        : @%systemroot%\system32\spoolsv.exe,-2
...
```

For more information on the cmdlets covered in this section, see the following
articles.

-[Get-Item][10]
-[Get-ChildItem][09]

## Viewing registry key values

Registry key values are stored as properties of each registry key. The
`Get-ItemProperty` cmdlet views registry key properties using the name you
specify. The result is a **PSCustomObject** containing the properties you
specify.

The Following example uses the `Get-ItemProperty` cmdlet to view all
properties. Storing the resulting object in a variable allows you to access
the desired property value.

```powershell
$p = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Spooler
$p.DependOnService
```

```output
RPCSS
http
```

Specifying a value for the `-Name` parameter selects the properties you
specify and returns the **PSCustomObject**.  The following example shows
the difference in output when you use the `-Name` parameter.

```powershell
Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Wbem
```

```Output
BUILD                      : 17134.1
Installation Directory     : C:\WINDOWS\system32\WBEM
MOF Self-Install Directory : C:\WINDOWS\system32\WBEM\MOF
PSPath                     : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wbem
PSParentPath               : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft
PSChildName                : Wbem
PSDrive                    : HKLM
PSProvider                 : Microsoft.PowerShell.Core\Registry
```

```powershell
Get-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Wbem -Name BUILD
```

```Output
BUILD        : 17134.1
PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wbem
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft
PSChildName  : Wbem
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
```

Beginning in PowerShell 5.0, the `Get-ItemPropertyValue` cmdlet returns
only the value of the property you specify.

```powershell
Get-ItemPropertyValue -Path HKLM:\SOFTWARE\Microsoft\Wbem -Name BUILD
```

```output
17134.1
```

For more information on the cmdlets used in this section, see the following
articles.

- [Get-ItemProperty][11]
- [Get-ItemPropertyValue][12]

## Changing registry key values

The `Set-ItemProperty` cmdlet sets registry values associated with a registry
key. The following example uses `Set-ItemProperty` to change the spooler
service start type to manual. The example changes the **StartType** back to
`Automatic` using the `Set-Service` cmdlet.

```powershell
Get-Service spooler | Select-Object Name, StartMode
```

```Output
Name    StartType
----    ---------
spooler Automatic
```

```powershell
$path = "HKLM:\SYSTEM\CurrentControlSet\Services\Spooler\"
Set-ItemProperty -Path $path -Name Start -Value 3
Get-Service spooler | Select-Object Name, StartMode
```

```Output
Name    StartType
----    ---------
spooler    Manual
```

```powershell
Set-Service -Name Spooler -StartupType Automatic
```

Each registry key has a _default_ value. You can change the `default` value
for a registry key with either `Set-Item` or `Set-ItemProperty`.

```powershell
Set-ItemProperty -Path HKLM:\SOFTWARE\Contoso -Name "(default)" -Value "one"
Set-Item -Path HKLM:\SOFTWARE\Contoso -Value "two"
```

For more information on the cmdlets used in this section, see the following
articles.

- [Set-Item][21]
- [Set-ItemProperty][22]

## Creating registry keys and values

The `New-Item` cmdlet creates new registry keys with a name that you provide.
You can also use the `mkdir` function, which calls the `New-Item` cmdlet
internally.

```powershell
mkdir ContosoCompany
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SOFTWARE

Name                           Property
----                           --------
ContosoCompany
```

You can use the `New-ItemProperty` cmdlet to create values in a registry key
that you specify. The following example creates a new DWORD value on the
ContosoCompany registry key.

```powershell
$path = "HKLM:\SOFTWARE\ContosoCompany"
New-ItemProperty -Path $path -Name Test -Type DWord -Value 1
```

> [!NOTE]
> Review the dynamic parameters section in this article for other allowed type
> values.

For detailed cmdlet usage, see [New-ItemProperty][18].

## Copying registry keys and values

In the **Registry** provider, use the `Copy-Item` cmdlet copies registry keys
and values. Use the `Copy-ItemProperty` cmdlet to copy registry values only.
The following command copies the "Contoso" registry key, and its properties to
the specified location `HKLM:\Software\Fabrikam`.

`Copy-Item` creates the destination key if it doesn't exist. If the destination
key exists, `Copy-Item` creates a duplicate of the source key as a child item
(subkey) of the destination key.

```powershell
Copy-Item -Path  HKLM:\Software\Contoso -Destination HKLM:\Software\Fabrikam
```

The following command uses the `Copy-ItemProperty` cmdlet to copy the "Server"
value from the "Contoso" key to the "Fabrikam" key.

```powershell
$source = "HKLM:\SOFTWARE\Contoso"
$dest = "HKLM:\SOFTWARE\Fabrikam"
Copy-ItemProperty -Path $source -Destination $dest -Name Server
```

For more information on the cmdlets used in this section, see the following
articles.

- [Copy-Item][07]
- [Copy-ItemProperty][08]

## Moving registry keys and values

The `Move-Item` and `Move-ItemProperty` cmdlets behave like their "Copy"
counterparts. If the destination exists, `Move-Item` moves the source key
underneath the destination key. If the destination key doesn't exist, the
source key is moved to the destination path.

The following command moves the "Contoso" key to the path
`HKLM:\SOFTWARE\Fabrikam`.

```powershell
Move-Item -Path HKLM:\SOFTWARE\Contoso -Destination HKLM:\SOFTWARE\Fabrikam
```

This command moves all properties from `HKLM:\SOFTWARE\ContosoCompany` to
`HKLM:\SOFTWARE\Fabrikam`.

```powershell
$source = "HKLM:\SOFTWARE\Contoso"
$dest = "HKLM:\SOFTWARE\Fabrikam"
Move-ItemProperty -Path $source -Destination $dest -Name *
```

For more information on the cmdlets used in this section, see the following
articles.

- [Move-Item][15]
- [Move-ItemProperty][16]

## Renaming registry keys and values

You can rename registry keys and values just like you would files and folders.
`Rename-Item` renames registry keys, while `Rename-ItemProperty` renames
registry values.

```powershell
$path = "HKLM:\SOFTWARE\Contoso"
Rename-ItemProperty -Path $path -Name ContosoTest -NewName FabrikamTest
Rename-Item -Path $path -NewName Fabrikam
```

## Changing security descriptors

You can restrict access to registry keys using the `Get-Acl` and `Set-Acl`
cmdlets. The following example adds a new user with full control to the
`HKLM:\SOFTWARE\Contoso` registry key.

```powershell
$acl = Get-Acl -Path HKLM:\SOFTWARE\Contoso
$rule = New-Object System.Security.AccessControl.RegistryAccessRule `
("CONTOSO\jsmith", "FullControl", "Allow")
$acl.SetAccessRule($rule)
$acl | Set-Acl -Path HKLM:\SOFTWARE\Contoso
```

For more examples and cmdlet usage details see the following articles.

- [Get-Acl][24]
- [Set-Acl][25]

## Removing and clearing registry keys and values

You can remove contained items using `Remove-Item`. You are prompted to confirm
the removal if the item contains anything else. The following example attempts
to delete a key `HKLM:\SOFTWARE\Contoso`.

```powershell
dir HKLM:\SOFTWARE\Contoso\
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SOFTWARE\Contoso

Name                           Property
----                           --------
ChildKey
```

```powershell
Remove-Item -Path HKLM:\SOFTWARE\Contoso
```

```Output
Confirm
The item at HKLM:\SOFTWARE\Contoso has children and the -Recurse
parameter wasn't specified. If you continue, all children will be removed
with the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

To delete contained items without prompting, specify the `-Recurse` parameter.

```powershell
Remove-Item -Path HKLM:\SOFTWARE\Contoso -Recurse
```

If you wanted to remove all items within `HKLM:\SOFTWARE\Contoso` but not
`HKLM:\SOFTWARE\Contoso` itself, use a trailing backslash `\` followed by a
wildcard.

```powershell
Remove-Item -Path HKLM:\SOFTWARE\Contoso\* -Recurse
```

This command deletes the "ContosoTest" registry value from the
`HKLM:\SOFTWARE\Contoso` registry key.

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Contoso -Name ContosoTest
```

`Clear-Item` clears all registry values for a key. The following example
clears all values from the `HKLM:\SOFTWARE\Contoso` registry key. To clear
only a specific property, use `Clear-ItemProperty`.

```powershell
Get-Item .\Contoso\
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SOFTWARE

Name           Property
----           --------
Contoso        Server     : {a, b, c}
               HereString : {This is text which contains
               newlines. It also contains "quoted" strings}
               (default)  : 1
```

```powershell
Clear-Item .\Contoso\
Get-Item .\Contoso\
```

```Output
    Hive: HKEY_LOCAL_MACHINE\SOFTWARE

Name                           Property
----                           --------
Contoso
```

For more examples and cmdlet usage details see the following articles.

- [Clear-Item][05]
- [Clear-ItemProperty][06]
- [Remove-Item][19]
- [Remove-ItemProperty][20]

## Dynamic parameters

Dynamic parameters are cmdlet parameters that are added by a PowerShell
provider and are available only when the cmdlet is being used in the
provider-enabled drive.

### Type <Microsoft.Win32.RegistryValueKind>

Establishes or changes the data type of a registry value. The default is
`String` (REG_SZ).

This parameter works as designed on the [Set-ItemProperty][22] cmdlet. It's
also available on the [Set-Item][21] cmdlet in the registry drives, but it has
no effect.

- `String` - Used for REG_SZ values. Pass a `[System.String]` object to the
  **Value** parameter.
- `ExpandString` - Used for REG_EXPAND_SZ values. Pass a `[System.String]`
  object to the **Value** parameter. The string should contain unexpanded
  references to environment variables that are expanded when the value is
  retrieved.
- `Binary` - Used for REG_BINARY values. Pass a `[System.Byte[]]` object to the
  **Value** parameter.
- `DWord` - Used for REG_DWORD values. Pass a `[System.Int32]` object to the
  **Value** parameter.
- `MultiString` - Used for REG_MULTI_SZ values. Pass a `[System.String[]]`
  object to the **Value** parameter.
- `QWord` - Used for REG_QWORD values. Pass a `[System.Int64]` object to the
  **Value** parameter.
- `Unknown` - Indicates an unsupported registry data type, such as
  REG_RESOURCE_LIST values.

## Using the pipeline

Provider cmdlets accept pipeline input. You can use the pipeline to simplify
task by sending provider data from one cmdlet to another provider cmdlet. To
read more about how to use the pipeline with provider cmdlets, see the cmdlet
references provided throughout this article.

## Getting help

Beginning in Windows PowerShell 3.0, you can get customized help topics for
provider cmdlets that explain how those cmdlets behave in a file system drive.

To get the help topics that are customized for the file system drive, run a
`Get-Help` command in a file system drive or use the **Path** parameter to
specify a file system drive.

```powershell
Get-Help Get-ChildItem
```

```powershell
Get-Help Get-ChildItem -Path HKLM:
```

## See also

- [about_Providers][04]

<!-- link references -->
[01]: /dotnet/api/microsoft.win32.registrykey
[02]: /dotnet/api/system.management.automation.pscustomobject
[03]: /windows/desktop/sysinfo/structure-of-the-registry
[04]: about_Providers.md
[05]: xref:Microsoft.PowerShell.Management.Clear-Item
[06]: xref:Microsoft.PowerShell.Management.Clear-ItemProperty
[07]: xref:Microsoft.PowerShell.Management.Copy-Item
[08]: xref:Microsoft.PowerShell.Management.Copy-ItemProperty
[09]: xref:Microsoft.PowerShell.Management.Get-ChildItem
[10]: xref:Microsoft.PowerShell.Management.Get-Item
[11]: xref:Microsoft.PowerShell.Management.Get-ItemProperty
[12]: xref:Microsoft.PowerShell.Management.Get-ItemPropertyValue
[13]: xref:Microsoft.PowerShell.Management.Get-Location
[14]: xref:Microsoft.PowerShell.Management.Invoke-Item
[15]: xref:Microsoft.PowerShell.Management.Move-Item
[16]: xref:Microsoft.PowerShell.Management.Move-ItemProperty
[17]: xref:Microsoft.PowerShell.Management.New-Item
[18]: xref:Microsoft.PowerShell.Management.New-ItemProperty
[19]: xref:Microsoft.PowerShell.Management.Remove-Item
[20]: xref:Microsoft.PowerShell.Management.Remove-ItemProperty
[21]: xref:Microsoft.PowerShell.Management.Set-Item
[22]: xref:Microsoft.PowerShell.Management.Set-ItemProperty
[23]: xref:Microsoft.PowerShell.Management.Set-Location
[24]: xref:Microsoft.PowerShell.Security.Get-Acl
[25]: xref:Microsoft.PowerShell.Security.Set-Acl
