---
title: "ExcludeOtherLists element (SPMetal)"
manager: soliver
ms.date: 3/9/2015
ms.audience: Developer
ms.topic: reference
ms.prod: sharepoint
ms.localizationpriority: medium
api_name:
- SPMetal Parameters XML
api_type:
- schema
ms.assetid: 681e25ee-a1b7-4adf-9aa6-393917292bb9
description: Specifies that SPMetal generates code only for lists that are explicitly represented by List elements. 
---

# ExcludeOtherLists element (SPMetal)

**Applies to:** SharePoint 2016 | SharePoint Foundation 2013 | SharePoint Online | SharePoint Server 2013
  
Specifies that SPMetal generates code only for lists that are explicitly represented by **List** elements. 
  
```XML
<ExcludeOtherLists />
```

## Elements and attributes

The following sections describe attributes, child elements, and parent elements.

### Attributes

None.
  
### Child elements

None.
  
### Parent elements

|**Element**|**Description**|
|:-----|:-----|
|[Web](web-spmetal.md) <br/> |Specifies the name and access level (public or internal) of the class (derived from **DataContext**) that SPMetal generates.  <br/> |
   
### Remarks

A **Web** element cannot have both an **ExcludeOtherLists** element and an **IncludeHiddenLists** element. 
  
## Example

The following is an example of an **ExcludeOtherLists** element in use. In this case, it ensures that the "Team Members" list is the only one for which SPMetal generates a property declaration.
  
```XML
<?xml version="1.0" encoding="utf-8"?>
<Web AccessModifier="Internal" xmlns="http://schemas.microsoft.com/SharePoint/2009/spmetal">
  <List Name="Team Members">
    <ContentType Name="Item" Class="TeamMember" />
  </List>
 <ExcludeOtherLists />
</Web>

```

## See also

- [SPMetal Default Code Generation Rules](https://msdn.microsoft.com/library/873ac65e-425e-40f3-9ef6-753d3cda1436%28Office.15%29.aspx) 
- [Overriding SPMetal Defaults by Using a Parameters XML File](https://msdn.microsoft.com/library/209359b2-bd46-47b6-837d-3c0c2005cb19%28Office.15%29.aspx)

