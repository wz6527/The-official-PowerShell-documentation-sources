---
description: SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableControl
ms.date: 08/25/2021
title: SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableControl
---
# SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableControl

Specifies the set of .NET types that trigger the condition. When any of the types in this set are
present, the condition is met, and the object is displayed by using this definition of the table
view.

## Schema

- Configuration Element
- ViewDefinitions Element
- View Element
- TableControl Element
- TableRowEntries Element
- TableRowEntry Element
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
|[SelectionCondition Element for EntrySelectedBy for TableRowEntry](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|Defines the condition that must exist to use for this definition of the table view.|

## Text Value

Specify the name of the selection set.

## Remarks

The selection condition can specify a selection set or .NET type, but cannot specify both. For more
information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).

Selection sets are common groups of .NET objects that can be used by any view that the formatting
file defines. For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).

For more information about other components of a wide view, see [Creating a Table View](./creating-a-table-view.md).

## See Also

[Creating a Table View](./creating-a-table-view.md)

[Defining Conditions for When Data Is Displayed](./defining-conditions-for-displaying-data.md)

[TypeName Element for SelectionCondition for EntrySelectedBy for TableRowEntry](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[SelectionCondition Element for EntrySelectedBy for TableRowEntry](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
