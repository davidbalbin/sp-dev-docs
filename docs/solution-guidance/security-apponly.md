---
title: Accessing SharePoint using an application context, also known as app-only
description: Accessing SharePoint using an application context, also known as app-only
ms.date: 03/03/2022
ms.prod: sharepoint
author: vesajuvonen
ms.author: vesaj
ms.topic: sharepoint
ms.localizationpriority: medium
---

# Accessing SharePoint using an application context, also known as app-only

There are two approaches for doing app-only for SharePoint: 

 - Using an **Azure AD application**: this is the preferred method when using SharePoint Online because you can also grant permissions to other Office 365 services (if needed) + you’ve a user interface (Azure portal) to maintain your app principals.
 - Using a **SharePoint App-Only principal**: this method is older and only works for SharePoint access, but is still relevant. This method is also the recommended model when you’re still working in SharePoint on-premises since this model works in both SharePoint on-premises as SharePoint Online.

Both methods are detailed in following articles: 

 - [Granting access via Azure AD App-Only](security-apponly-azuread.md)
 - [Granting access using SharePoint App-Only](security-apponly-azureacs.md)

## What are the limitations when using app-only

App-Only does not work in following cases:

 - Updating taxonomy service entries (write) - read works
 - Creating modern team sites does not support app-only when you [use the SharePoint API](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Sites/SiteCollection.cs) for it. When modern team sites are created [using Microsoft Graph](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs) to create the group then app-only is a supported scenario
 - Creating communication sites is supported in app-only context, but owner property is required. [using the SharePoint API](/sharepoint/dev/apis/site-creation-rest)
 - Search when using SharePoint On-Premises. SharePoint Online support for it has been added ([blog post](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))
 - User Profile CSOM write operations do not work with **Azure AD application** - read operations work. Both read and write operations work through **SharePoint App-Only principal**
 - User Profile Bulk Update API can be used with app-only permissions
 - Manipulating files via WebDav protocol and CSOM (using `File.SaveBinaryDirect` or `File.OpenBinaryDirect`) does not work with app-only. Use `File.SaveBinary` and `File.OpenBinaryStream` instead.
 - The use of the `Microsoft.SharePoint.Client.Web.ShareObject()` API was not tested with app-only permissions, and may not work consistently. 
The recommendation is to use it only with an app+user context.

> [!IMPORTANT]
> If the above scenarios are critical for you it's recommended to define a service account, grant that one permissions and then use it in your application. See the [Governance.EnsurePolicy](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.EnsurePolicy) sample to learn more on how you can grant tenant wide permissions for a service account. Also the article explaining an [alternative model for web app policies in SharePoint Online](security-webapppolicies.md) does contain a lot of information on this topic.

> [!IMPORTANT]
> Azure Access Control (ACS), a service of Azure Active Directory (Azure AD), was retired on November 7, 2018. This retirement does not impact the SharePoint Add-in model, which uses the `https://accounts.accesscontrol.windows.net` hostname (which is not impacted by this retirement). For more information, see [Impact of Azure Access Control retirement for SharePoint Add-ins](https://developer.microsoft.com/office/blogs/impact-of-azure-access-control-deprecation-for-sharepoint-add-ins).
