---
description: CustomControl Element for View
ms.date: 08/20/2021
title: CustomControl Element for View
---
# CustomControl Element for View

Defines a custom control format for the view.

## Schema

- Configuration Element
- ViewDefinitions Element
- View Element
- CustomControl Element

## Syntax

```xml
<CustomControl>
  <CustomEntries>...</CustomEntries>
</CustomControl>
```

## Attributes and Elements

The following sections describe attributes, child elements, and the parent element of the
`CustomControl` element. You must specify one child element.

### Attributes

None.

### Child Elements

|Element|Description|
|-------------|-----------------|
|[CustomEntries Element for CustomControl for View](./customentries-element-for-customcontrol-for-view-format.md)|Required element.<br /><br /> Provides the definitions of the custom control view.|

### Parent Elements

|Element|Description|
|-------------|-----------------|
|[View Element](./view-element-format.md)|Defines a view that is used to display one or more .NET objects.|

## Remarks

In most cases, only one definition is required for each control view, but it is possible to provide
multiple definitions if you want to use the same view to display different .NET objects. In those
cases, you can provide a separate definition for each object or set of objects.

## See Also

[CustomEntries Element for CustomControl for View](./customentries-element-for-customcontrol-for-view-format.md)

[View Element](./view-element-format.md)

[Writing a PowerShell Formatting File](./writing-a-powershell-formatting-file.md)
