---
title: Office Common API requirement sets
description: ''
ms.date: 06/20/2019
ms.prod: non-product-specific
localization_priority: Priority
---

# Office Common API requirement sets

Requirement sets are named groups of API members. Office Add-ins use requirement sets specified in the manifest or use a runtime check to determine whether an Office host supports APIs that an add-in needs. For more information, see [Office versions and requirement sets](/office/dev/add-ins/develop/office-versions-and-requirement-sets).

Need information about where add-ins are supported by Office host? See [Office Add-in host and platform availability](/office/dev/add-ins/overview/office-add-in-availability).

Looking for the *host-specific* API requirement sets? See the following API requirement sets:

- [Excel JavaScript API requirement sets](excel-api-requirement-sets.md) (ExcelApi)
- [Word JavaScript API requirement sets](word-api-requirement-sets.md) (WordApi)
- [OneNote JavaScript API requirement sets](onenote-api-requirement-sets.md) (OneNoteApi)
- [Understanding Outlook API requirement sets](outlook-api-requirement-sets.md) (Mailbox)

> [!IMPORTANT]
> We no longer recommend that you create and use Access web apps and databases in SharePoint. As an alternative, we recommend that you use [Microsoft PowerApps](https://powerapps.microsoft.com/) to build no-code business solutions for web and mobile devices.

## Common API requirement sets

The following sections list the Common API requirement sets, the methods in each set, and the Office host applications that support that requirement set. All of these API requirement sets are version 1.1.

### ActiveView

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac|Document.getActiveViewAsync|

---

### AddInCommands

See [Add-in command requirement sets](add-in-commands-requirement-sets.md).

---

### BindingEvents

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Access Web Apps<br>Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Binding.addHandlerAsync<br>Binding.removeHandlerAsync|

---

### CompressedFile

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on Mac<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports output to Office Open XML (OOXML) format as a byte array<br>(Office.FileType.Compressed) when using the Document.getFileAsync method.|

---

### CustomXmlParts

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|CustomXmlNode.getNodesAsync<br>CustomXmlNode.getNodeValueAsync<br>CustomXmlNode.getTextAsync<br>CustomXmlNode.getXmlAsync<br>CustomXmlNode.setNodeValueAsync<br>CustomXmlNode.setTextAsync<br>CustomXmlNode.setXmlAsync<br>CustomXmlPart.addHandlerAsync<br>CustomXmlPart.deleteAsync<br>CustomXmlPart.getNodesAsync<br>CustomXmlPart.getXmlAsync<br>CustomXmlPart.removeHandlerAsync<br>CustomXmlParts.addAsync<br>CustomXmlParts.getByIdAsync<br>CustomXmlParts.getByNamespaceAsync<br>CustomXmlPrefixMappings.addNamespaceAsync<br>CustomXmlPrefixMappings.getNamespaceAsync<br>CustomXmlPrefixMappings.getPrefixAsync|

---

### DialogApi

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| See [Dialog API requirement sets](dialog-api-requirement-sets.md). | UI.messageParent<br>UI.displayDialogAsync<br>UI.closeContainer<br>UI.Dialog |

---

### DocumentEvents

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>OneNote on the web<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Document.addHandlerAsync<br>Document.removeHandlerAsync|

---

### File

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Document.getFileAsync<br>File.closeAsync<br>File.getSliceAsync|

---

### HtmlCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| OneNote on the web<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports coercion to HTML (Office.CoercionType.Html) when reading and writing data using the Document.getSelectedDataAsync,<br>Document.setSelectedDataAsync, Binding.getDataAsync, or Binding.setDataAsync methods.|

---

### IdentityAPI

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| See [Identity API requirement sets](identity-api-requirement-sets.md). | Auth.getAccessTokenAsync |

---

### ImageCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on iPad<br>Excel on Mac<br>OneNote on the web<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports conversion to an image (Office.CoercionType.Image) when writing data using the Document.setSelectedDataAsync method.|

---

### Mailbox

|**Office hosts**|**Methods in set**|
|:-----|:-----|
|Outlook on Windows<br>Outlook on the web<br>Outlook on Android<br>Outlook on Mac<br>Outlook on iOS|See [Understanding Outlook API requirement sets](outlook-api-requirement-sets.md).|

---

### MatrixBindings

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word on Windows<br>Word on the web<br>Word on iPad<br>Word on Mac|Bindings.addFromNamedItemAsync<br>Bindings.addFromSelectionAsync<br>Bindings.getAllAsync<br>Bindings.getByIdAsync<br>Bindings.releaseByIdAsync<br>Binding.getDataAsync<br>Binding.setDataAsync|

---

### MatrixCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports coercion to the "matrix" (array of arrays) data structure (Office.CoercionType.Matrix) when reading and writing data using the Document.getSelectedDataAsync, Document.setSelectedDataAsync, Binding.getDataAsync, or Binding.setDataAsync methods.|

---

### OoxmlCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports coercion to Open Office XML (OOXML) format (Office.CoercionType.Ooxml) when reading and writing data using the Document.getSelectedDataAsync, Document.setSelectedDataAsync, Binding.getDataAsync, or Binding.setDataAsync methods.|

---

### PartialTableBindings

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Access Web Apps||

---

### PdfFile

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Mac<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports output to PDF format (Office.FileType.Pdf)<br>when using the Document.getFileAsync method.|

---

### Selection

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Project on Windows<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Document.getSelectedDataAsync<br>Document.setSelectedDataAsync|

---

### Settings

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Access Web Apps<br>Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>OneNote on the web<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Settings.get<br>Settings.remove<br>Settings.saveAsync<br>Settings.set|

---

### TableBindings

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Access Web Apps<br>Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Bindings.addFromNamedItemAsync<br>Bindings.addFromSelectionAsync<br>Bindings.getAllAsync<br>Bindings.getByIdAsync<br>Bindings.releaseByIdAsync<br>Binding.addColumnsAsync<br>Binding.addRowsAsync<br>Binding.deleteAllDataValuesAsync<br>Binding.getDataAsync<br>Binding.setDataAsync|

---

### TableCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Access Web Apps<br>Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports coercion to the "table" data structure (Office.CoercionType.Table) when reading and writing data using the Document.getSelectedDataAsync, Document.setSelectedDataAsync, Binding.getDataAsync, or Binding.setDataAsync methods.|

---

### TextBindings

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>Excel on Mac<br>Word 2013 and later and Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Bindings.addFromNamedItemAsync<br>Bindings.addFromSelectionAsync<br>Bindings.getAllAsync<br>Bindings.getByIdAsync<br>Bindings.releaseByIdAsync<br>Binding.getDataAsync<br>Binding.setDataAsync|

---

### TextCoercion

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Excel on Windows<br>Excel on the web<br>Excel on iPad<br>OneNote on the web<br>PowerPoint on Windows<br>PowerPoint on the web<br>PowerPoint on iPad<br>PowerPoint on Mac<br>Project on Windows<br>Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports coercion to text format (Office.CoercionType.Text) when reading and writing data using the Document.getSelectedDataAsync, Document.setSelectedDataAsync, Binding.getDataAsync, or Binding.setDataAsync methods.|

---

### TextFile

|**Office hosts**|**Methods in set**|
|:-----|:-----|
| Word 2013 and later on Windows<br>Word 2016 and later on Mac<br>Word on the web<br>Word on iPad|Supports output to text format (Office.FileType.Text) when using the Document.getFileAsync method.|

---

## Methods that aren't part of a requirement set

The following methods in the JavaScript API for Office aren't part of a requirement set. If your add-in requires any of these methods, use the **Methods** and **Method** elements in the add-in's manifest to declare that they are required, or perform the runtime check using an `if` statement. For more information, see [Specify Office hosts and API requirements](/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements).

|**Method name**|**Office host support**|
|:-----|:-----|
|Bindings.addFromPromptAsync|Access web apps, Excel on Windows, Excel on the web, Excel on iPad, and Excel on Mac|
|Document.getFilePropertiesAsync|Excel on Windows, Excel on the web, Excel on iPad, Excel on Mac, PowerPoint on Windows, PowerPoint on the web, PowerPoint on iPad, PowerPoint on Mac, Word on Windows, Word on the web, Word on iPad, and Word on Mac|
|Document.getProjectFieldAsync|Project Standard 2013 and Project Professional 2013|
|Document.getResourceFieldAsync|Project Standard 2013 and Project Professional 2013|
|Document.getSelectedResourceAsync|Project Standard 2013 and Project Professional 2013|
|Document.getSelectedTaskAsync|Project Standard 2013 and Project Professional 2013|
|Document.getSelectedViewAsync|Project Standard 2013 and Project Professional 2013|
|Document.getTaskAsync|Project Standard 2013 and Project Professional 2013|
|Document.getTaskFieldAsync|Project Standard 2013 and Project Professional 2013|
|Document.goToByIdAsync|Excel on Windows, Excel on the web, Excel on iPad, Excel on Mac, PowerPoint on Windows, PowerPoint on the web, PowerPoint on iPad, PowerPoint on Mac, Word on Windows, Word on the web, Word on iPad, and Word on Mac|
|Settings.addHandlerAsync|Access web apps and Excel on the web|
|Settings.refreshAsync|Access web apps, Excel on Windows, Excel on the web, PowerPoint on Windows, PowerPoint on the web, Word, and Word on the web|
|Settings.removeHandlerAsync|Access web apps and Excel on the web|
|TableBinding.clearFormatsAsync|Excel on Windows, Excel on the web, Excel on iPad, and Excel on Mac|
|TableBinding.setFormatsAsync|Excel on Windows, Excel on the web, Excel on iPad, and Excel on Mac|
|TableBinding.setTableOptionsAsync|Excel on Windows, Excel on the web, Excel on iPad, and Excel on Mac|

## See also

- [Office versions and requirement sets](/office/dev/add-ins/develop/office-versions-and-requirement-sets)
- [Specify Office hosts and API requirements](/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements)
- [Office Add-ins XML manifest](/office/dev/add-ins/develop/add-in-manifests)
