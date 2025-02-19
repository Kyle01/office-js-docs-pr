---
title: Dialog API requirement sets
description: ''
ms.date: 06/20/2019
ms.prod: non-product-specific
localization_priority: Normal
---

# Dialog API requirement sets

Requirement sets are named groups of API members. Office Add-ins use requirement sets specified in the manifest or use a runtime check to determine whether an Office host supports APIs that an add-in needs. For more information, see [Office versions and requirement sets](/office/dev/add-ins/develop/office-versions-and-requirement-sets).

Office Add-ins run across multiple versions of Office. The following table lists the Dialog API requirement sets, the Office host applications that support that requirement set, and the build or version numbers for the Office application.

|  Requirement set  | Office 2013 on Windows<br>(one-time purchase) | Office 2016 or later on Windows<br>(one-time purchase)   | Office on Windows<br>(connected to Office 365 subscription) |  Office on iPad<br>(connected to Office 365 subscription)  |  Office on Mac<br>(connected to Office 365 subscription)  | Office on the web  |  Office Online Server  |
|:-----|-----|:-----|:-----|:-----|:-----|:-----|:-----|
| DialogApi 1.1  | Build 15.0.4855.1000 or later | Build 16.0.4390.1000 or later | Version 1602 (Build 6741.0000) or later | 1.22 or later | 15.20 or later| January 2017 | Version 1608 (Build 7601.6800) or later|

To find out more about versions, build numbers, and Office Online Server, see:

- [Version and build numbers of update channel releases for Office 365 clients](https://support.office.com/article/version-and-build-numbers-of-update-channel-releases-ae942449-1fca-4484-898b-a933ea23def7)
- [What version of Office am I using?](https://support.office.com/article/What-version-of-Office-am-I-using-932788b8-a3ce-44bf-bb09-e334518b8b19)
- [Where you can find the version and build number for an Office 365 client application](https://support.office.com/article/version-and-build-numbers-of-update-channel-releases-ae942449-1fca-4484-898b-a933ea23def7)
- [Office Online Server overview](/officeonlineserver/office-online-server-overview)

## Office Common API requirement sets

For information about Common API requirement sets, see [Office Common API requirement sets](office-add-in-requirement-sets.md).

## Dialog API 1.1

The Dialog API 1.1 is the first version of the API. For details about the API, see the [Dialog API
](/javascript/api/office/office.ui) reference topic.

## See also

- [Office versions and requirement sets](/office/dev/add-ins/develop/office-versions-and-requirement-sets)
- [Specify Office hosts and API requirements](/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements)
- [Office Add-ins XML manifest](/office/dev/add-ins/develop/add-in-manifests)
