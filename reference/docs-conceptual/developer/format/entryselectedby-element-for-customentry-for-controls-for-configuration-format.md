---
description: EntrySelectedBy Element for CustomEntry for Controls
ms.date: 08/23/2021
title: EntrySelectedBy Element for CustomEntry for Controls
---
# EntrySelectedBy Element for CustomEntry for Controls

Defines the .NET types that use the definition of the common control or the condition that must
exist for this control to be used. This element is used when defining a common control that can be
used by all the views in the formatting file.

## Schema

- Configuration Element
- Controls Element
- Control Element
- CustomControl Element
- CustomEntries Element
- CustomEntry Element
- EntrySelectedBy Element

## Syntax

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>SelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## Attributes and Elements

The following sections describe attributes, child elements, and the parent element of the
`EntrySelectedBy` element.

### Attributes

None.

### Child Elements

|Element|Description|
|-------------|-----------------|
|[SelectionCondition Element for EntrySelectedBy for Controls for Configuration](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|Optional element.<br /><br /> Defines the condition that must exist for the common control definition to be used.|
|[SelectionSetName Element for EntrySelectedBy for Controls for Configuration](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)|Optional element.<br /><br /> Specifies a set of .NET types that use this definition of the common control.|
|[TypeName Element for EntrySelectedBy for Controls for Configuration](./typename-element-for-entryselectedby-for-controls-for-configuration-format.md)|Optional element.<br /><br /> Specifies a .NET type that uses this definition of the common control.|

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[CustomEntry Element for CustomControl for Controls for Configuration](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|Provides a definition of the common control.|

## Remarks

At a minimum, each definition must have at least one .NET type, selection set, or selection
condition specified. There is no maximum limit to the number of types, selection sets, or selection
conditions that you can specify.

## See Also

[SelectionCondition Element for EntrySelectedBy for Controls for Configuration](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[SelectionSetName Element for EntrySelectedBy for Controls for Configuration](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[CustomEntry Element for CustomControl for Controls for Configuration](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[TypeName Element for EntrySelectedBy for Controls for Configuration](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
