---
description: PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry
ms.date: 08/24/2021
title: PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry
---
# PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry

Specifies the .NET property that triggers the condition. When this property is present or when it
evaluates to `true`, the condition is met, and the definition is used.

- Configuration Element
- ViewDefinitions Element
- View Element
- WideControl Element
- WideEntries Element
- WideEntry Element
- EntrySelectedBy Element
- SelectionCondition Element
- PropertyName Element

## Syntax

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

```csharp

```

## Attributes and Elements

The following sections describe attributes, child elements, and the parent element of the
`PropertyName` element.

### Attributes

None.

### Child Elements

None.

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[SelectionCondition Element for EntrySelectedBy for WideEntry](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|Defines the condition that must exist for this definition to be used.|

## Text Value

Specify the .NET property name.

## Remarks

The selection condition must specify at least one property name or a script to evaluate, but cannot
specify both. For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).

For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).

## See Also

[Creating a Wide View](./creating-a-wide-view.md)

[Defining Conditions for When Data Is Displayed](./defining-conditions-for-displaying-data.md)

[ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[SelectionCondition Element for EntrySelectedBy for WideEntry](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
