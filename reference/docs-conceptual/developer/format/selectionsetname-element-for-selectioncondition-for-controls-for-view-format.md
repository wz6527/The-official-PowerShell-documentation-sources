---
description: SelectionSetName Element for SelectionCondition for Controls for View
ms.date: 08/25/2021
title: SelectionSetName Element for SelectionCondition for Controls for View
---
# SelectionSetName Element for SelectionCondition for Controls for View

Specifies the set of .NET types that trigger the condition. When any of the types in this set are
present, the condition is met and the object is displayed using this control. This element is used
when defining controls that can be used by a view.

## Schema

- Configuration Element
- ViewDefinitions Element
- View Element
- Controls Element
- Control Element
- CustomControl Element
- CustomEntries Element
- CustomEntry Element
- EntrySelectedBy Element
- SelectionCondition Element
- SelectionSetName Element

## Syntax

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## Attributes and Elements

The following sections describe attributes, child elements, and the parent element of the
`SelectionSetName` element.

### Attributes

None.

### Child Elements

None.

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[SelectionCondition Element for EntrySelectedBy for Controls for View](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|Defines a condition that must exist for the control definition to be used.|

## Text Value

Specify the name of the selection set.

## Remarks

Selection sets are common groups of .NET objects that can be used by any view that the formatting
file defines. For more information about creating and referencing selection sets, see [Defining Selection Sets](./defining-selection-sets.md).

The selection condition can specify a selection set or .NET type, but cannot specify both. For more
information about how to use selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).

## See Also

[SelectionCondition Element for EntrySelectedBy for Controls for View](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[Defining Conditions for When Data Is Displayed](./defining-conditions-for-displaying-data.md)

[Defining Selection Sets](./defining-selection-sets.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
