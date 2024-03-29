## ArcGIS Pro 3.2 SDK for .NET
```
ArcGIS Pro Version: 3.2.0.xxxxx
```
Extend ArcGIS Pro with the ArcGIS Pro SDK for Microsoft .NET.  The ArcGIS Pro SDK provides four main extensibility patterns:  add-ins, managed configurations, plugin datasources and CoreHost applications.  You can leverage modern .NET features and patterns such as Task Asynchronous Programming (TAP), LINQ, WPF Binding, and MVVM to build integrated 2D and 3D add-ins with the ArcGIS Pro APIs.

********

**In this topic**    
* [Overview of the ArcGIS Pro SDK](#overview-of-the-arcgis-pro-sdk)
   * [Requirements](#requirements)
   * [ArcGIS Pro API](#arcgis-pro-api)
       * [Core](#core)
       * [Extensions](#extensions)
       * [Extensions with no public API](#extensions-with-no-public-api)
       * [ArcGIS Pro Extensions Nuget](#arcgis-pro-extensions-nuget)
* [What's New for Developers at 3.2](#whats-new-for-developers-at-32) 
* [Installing ArcGIS Pro SDK for .NET](#installing-arcgis-pro-sdk-for-net) 
* [Release notes](#release-notes) 
   * [ArcGIS Pro SDK for .NET components](#arcgis-pro-sdk-for-net-components)
       * [ArcGIS Pro SDK for .NET templates](#arcgis-pro-sdk-for-net-templates)
       * [ArcGIS Pro SDK for .NET utilities](#arcgis-pro-sdk-for-net-utilities)
       * [ArcGIS Pro SDK for .NET Migration](#arcgis-pro-sdk-for-net-migration)
   * [Previous versions](#previous-versions)
* [Resources](#resources) 

## Overview of the ArcGIS Pro SDK

### Requirements

#### ArcGIS Pro

* ArcGIS Pro 3.2

#### Supported platforms

* Windows 11 (Home, Pro, Enterprise)
* Windows 10 (Home, Pro, Enterprise) (64 bit)

#### Supported .NET

* Microsoft .NET Runtime 6.0.5 or [better](https://github.com/dotnet/core/blob/main/release-notes/6.0/README.md). [Download .NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)

#### Supported IDEs

* Visual Studio 2022 (v17.2 or higher)  
   * Community Edition  
   * Professional Edition  
   * Enterprise Edition  

We recommend installing a minimum version of 17.2 of Visual Studio. This version includes .NET 6.0.5 as part of the Visual Studio 2022 install (.NET SDK 6.0.3). Installing a lesser version of Visual Studio 2022 may require a separate install of the .NET Desktop Runtime 6.0.5 and/or .NET SDK 6.0.3. Consult Microsoft’s [Download .NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) site for more information.

#### Third party assemblies
_**Newtonsoft Json**_  
* At 3.2, ArcGIS Pro is using version 13.0.1.25517 of the Newtonsoft Json NuGet. If you require Newtonsoft NuGet in your add-ins it is recommended to use the same version.  

_**WebView2**_  
* Add-in developers can use the new WebViewBrowser control based on Microsoft Edge WebView2. Consult the WebView2 manifest in the Pro bin\WebView folder for the current WebView2 fixed version runtime in use by ArcGIS Pro.

[ArcGIS Pro system requirements](https://pro.arcgis.com/en/pro-app/get-started/arcgis-pro-system-requirements.htm) 

### ArcGIS Pro API

The ArcGIS Pro APIs are _managed .NET assemblies_ which are installed with each ArcGIS Pro installation. Intermediary assemblies containing .NET metadata or PIAs (Primary Interop Assemblies) are not required.

Add any of the ArcGIS Pro managed assemblies that comprise its API as references directly in your Visual Studio add-in projects

A complete list of the ArcGIS Pro assemblies in the public API is provided below. Consult the online [API Reference](https://pro.arcgis.com/en/pro-app/latest/sdk/api-reference) for specific details of each assembly:

#### Core

Core assemblies are located in the {ArcGIS Pro Installation folder}\bin.

Assembly           | Description
------------------------| -------------
ArcGIS.Core.dll        | Provides CIM, Geodatabase, Geometry and Utility Network APIs.
ArcGIS.CoreHost.dll | Provides Host.Initialize to initialize ArcGIS.Core.dll for stand-alone use.
ArcGIS.Desktop.Framework.dll        | Provides the application framework to include add-in contracts, DAML support, and base classes. This assembly **must be referenced** by every add-in.
ESRI.ArcGIS.ItemIndex.dll       | Provides functionality to create and work with Custom items.


#### Extensions

Major subsystems within ArcGIS Pro are organized into units called extensions. Extension assemblies are located in the {ArcGIS Pro Installation folder}\bin\Extensions folder in their own individual subfolder. 
Extension subfolder names are logically named for the unit of functionality they represent, for example, Mapping, Editing, Layout, and so on.

Assembly           | Description
------------------------| -------------
ArcGIS.Desktop.Catalog.dll   | Provides access to project content items (map items, layout items, style items, folder items, and so on).
ArcGIS.Desktop.Core.dll    | Provides functionality to create and manage projects, access to events associated with the current project, and the ability to execute geoprocessing tools.
ArcGIS.Desktop.DataReviewer.dll | Provides functionality to establish and manage Reviewer results, sessions, and batch jobs in a project.
ArcGIS.Desktop.Editing.dll        | Provides access to the editing environment and core editing functionality required for custom edit tool implementations.
ArcGIS.Desktop.Extensions.dll        | Provides extension methods for other ArcGIS Pro classes. Provides a base class for custom map tools.
ArcGIS.Desktop.Geoprocessing.dll        | Provides access to geoprocessing history items stored in the project. (Note: Adds a reference to ArcGIS.Desktop.Core.dll to execute geoprocessing tools.)
ArcGIS.Desktop.Layouts.dll        | Provides functionality for manipulating elements on a layout and exporting to a variety of image formats.
ArcGIS.Desktop.Mapping.dll        | Provides types to create maps and layers, label features, perform query operations, and visualize them in 2D or 3D. Provides a raster API to create raster layers and customize raster rendering, and an API to manage styles, style items, and symbols.
ArcGIS.Desktop.TaskAssistant.dll        | Provides the Tasks framework, allowing developers to access, open, close, or export task items.
ArcGIS.Desktop.Workflow.dll       | Provides functionality to create, configure, and execute Workflow Manager Classic jobs and queries. Provides functionality to retrieve configuration information from the Workflow Manager Classic database.
ArcGIS.Desktop.Workflow.Client.dll       | Provides functionality to retrieve job id and connection information for Workflow Manager.


#### Extensions with no public API

There are extension assemblies in {ArcGIS Pro Installation folder}\bin\Extensions subfolders) that do not have a public API. They are currently for Esri internal use only.

* ArcGIS.Desktop.Analyst3D.dll
* ArcGIS.Desktop.Aviation.dll
* ArcGIS.Desktop.BusinessAnalyst.dll
* ArcGIS.Desktop.CAD.dll
* ArcGIS.Desktop.Charts.dll
* ArcGIS.Desktop.DataEngineering.dll
* ArcGIS.Desktop.DataSourcesRaster.dll
* ArcGIS.Desktop.Defense.dll
* ArcGIS.Desktop.DefenseMapping.dll
* ArcGIS.Desktop.Editing.PushPull.dll
* ArcGIS.Desktop.FullMotionVideo.dll
* ArcGIS.Desktop.GAWizard.dll
* ArcGIS.Desktop.GeoProcessing.BDC.dll
* ArcGIS.Desktop.GeoProcessing.SAModels.dll
* ArcGIS.Desktop.Geostatistics.dll
* ArcGIS.Desktop.Indoors.dll
* ArcGIS.Desktop.Intelligence.dll
* ArcGIS.Desktop.Intelligence.Common.dll
* ArcGIS.Desktop.KnowledgeGraph.dll
* ArcGIS.Desktop.LocationReferencing.dll
* ArcGIS.Desktop.Maritime.dll
* ArcGIS.Desktop.Metadata.dll
* ArcGIS.Desktop.MotionImagery.dll
* ArcGIS.Desktop.NetworkAnalysis.Facility.dll
* ArcGIS.Desktop.NetworkAnalysis.NetworkDiagrams.dll
* ArcGIS.Desktop.NetworkAnalysis.Transportation.dll
* ArcGIS.Desktop.Search.dll
* ArcGIS.Desktop.Sharing.dll
* ArcGIS.Desktop.TerritoryDesign.dll

Note: Static string resource properties and image resources included within the public API assemblies are for Esri internal use only. They are not intended for use in third-party add-ins. 

#### ArcGIS Pro Extensions NuGet

The ArcGIS Pro Extensions NuGet contains all the Pro API assemblies needed to compile your Add-ins and Configurations and offers an alternate way to reference the ArcGIS Pro assemblies in your add-in and configuration over traditional file based references. 

To use the ArcGIS Pro Extensions NuGet, set the NuGet Package Management format setting in Visual Studio to be PackageReference.

[ProGuide: ArcGIS Pro Extensions NuGet](https://github.com/Esri/arcgis-pro-sdk/wiki/ProGuide-ArcGIS-Pro-Extensions-NuGet)

## What's New for Developers at 3.2

#### 1. API enhancements
At 3.2 you can take advantage of API enhancements for: <br/>

**Geodatabase:**  
* DDL enhancements for Relates, Domains, and Subtypes. 

**Editing:**  
* New Extensibility API for Customizing Editor Attributes window.  

**Framework:**  
* New Start Page Controls for use within Configurations.

**Map Authoring:**  
* Improvements to Layout tool and Tray button patterns.
* Time support on layers and new Time Picker control.
* Catalog layer creation for storing references to multiple different data types.

**Layout:**  
* Map frame activation API in Layout

A complete list of the API enhancements is provided in the [API Changes section of the API Reference](https://pro.arcgis.com/en/pro-app/latest/sdk/api-reference/topic15120.html).

#### 2. SDK Resources
There are many ProConcepts, ProGuide, ProSnippets, and samples to help you get up and running with the new SDK features. Updates to the SDK Resources include, but are not limited to:    
* [ProConcepts: Framework](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-Framework)
* [ProConcepts: Editing](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-Editing)
* [ProConcepts: Map Authoring](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-Map-Authoring)
* [ProConcepts: Layouts](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-Layouts)
* [ProGuide: Tray buttons](https://github.com/Esri/arcgis-pro-sdk/wiki/ProGuide-Tray-buttons)
* [ProConcepts: Geometry](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-Geometry)
* [ProSnippets: Charts](https://github.com/Esri/arcgis-pro-sdk/wiki/ProSnippets-Charts)
* The [Pro Community Samples](https://github.com/Esri/arcgis-pro-sdk-community-samples) and [Snippets](https://github.com/Esri/arcgis-pro-sdk/wiki/ProSnippets)

## Installing ArcGIS Pro SDK for .NET

ArcGIS Pro SDK for .NET can be downloaded and installed from within Visual Studio. There will be 2 separate extensions you can install: 
* ArcGIS Pro SDK for .NET, 
* ArcGIS Pro SDK for .NET (Utilities) 

**Notes:**
Moving to ArcGIS Pro 3.2 SDK (or 3.0 SDK) from 2.x is not an upgrade. To install ,
1. Consult [Migrating from 2.x](https://github.com/arcgis/arcgis-pro-sdk/wiki/ProGuide-Installation-and-Upgrade#migrating-from-2x) if you want to install ArcGIS Pro 3.2 SDK and you are on 2.x, **_not_** 3.0.
2. If you are migrating a 2.x add-in to 3.2 you can install the migration tool to help automate the conversion process. Refer to the migration guide [ProConcepts: 3.0 Migration Guide](https://github.com/Esri/arcgis-pro-sdk/wiki/ProConcepts-3.0-Migration-Guide) for more details. ArcGIS Pro SDK for .NET (Migration).

Read the [ProGuide: Installation](http://github.com/Esri/arcgis-pro-sdk/wiki/ProGuide-Installation-and-Upgrade) for detailed installation instructions.

## Release notes

### ArcGIS Pro SDK for .NET components

The following table summarizes the functionality of each .vsix file included in the SDK download:

| Name|File|Functionality|
| ------------- | ------------- |------------- |
| ArcGIS Pro SDK for .NET | proapp-sdk-templates.vsix | A collection of project and item templates to create ArcGIS Pro add-ins|
| ArcGIS Pro SDK for .NET (Utilities)  | proapp-sdk-utilities.vsix  | A collection of utilities to help create ArcGIS Pro add-ins|
| ArcGIS Pro SDK for .NET (Migration)  | proapp-sdk-migration.vsix  | Migrates ArcGIS Pro SDK 2.x extensions to ArcGIS Pro SDK 3.x for .NET|


#### ArcGIS Pro SDK for .NET templates 
Package: proapp-sdk-templates.vsix  

ArcGIS Pro SDK for .NET provides the following project and item templates:
<table>
<tr><th>C# </th> <th> VB</th><th> Name</th> </tr>
<tr><td><span title="ArcGIS Pro Add-in C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProModuleC32.png"></span> </td><td> <span title="ArcGIS Pro Add-in VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProModuleVB32.png"></span> </td><td> ArcGIS Pro Module Add-in Project template </td></tr>
<tr><td><span title="ArcGIS Pro Configurations C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProConfigurationsC32.png"></span> </td><td> <span title="ArcGIS Pro Configurations VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProConfigurationsVB32.png"></span> </td><td> ArcGIS Pro Managed Configurations Project template </td></tr>
<tr><td><span title="ArcGIS Pro Plugin C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProPluginC32.png"></span> </td><td> N/A</td><td> ArcGIS Pro Plugin Project template </td></tr>
<tr><td><span title="ArcGIS Pro CoreHost Application"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProCoreHostC32.png"></span> </td><td> N/A</td><td> ArcGIS Pro CoreHost Application Project template </td></tr>
<tr><td><span title="ArcGIS Pro Backstage Tab C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProBackstageTabC32.png"></span></td><td> <span title="ArcGIS Pro Backstage Tab VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProBackstageTabVB32.png"></span> </td><td> ArcGIS Pro Backstage Tab </td></tr>
<tr><td><span title="ArcGIS Pro Button C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProButtonC32.png"></span> </td><td> <span title="ArcGIS Pro Button VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProButtonVB32.png"></span> </td><td> ArcGIS Pro Button </td></tr>
<tr><td><span title="ArcGIS Pro Button Palette C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProButtonPaletteC32.png"></span> </td><td> <span title="ArcGIS Pro Button Palette VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProButtonPaletteVB32.png"></span> </td><td> ArcGIS Pro Button Palette</td></tr>
<tr><td><span title="ArcGIS Pro Combo Box C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProComboBoxC32.png"></span> </td><td> <span title="ArcGIS Pro Combo Box VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProComboBoxVB32.png"></span> </td><td> ArcGIS Pro Combo Box</td></tr>
<tr><td><span title="ArcGIS Pro Construction Tool C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProConstructionToolC32.png"></span> </td><td> <span title="ArcGIS Pro Construction Tool VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProConstructionToolVB32.png"></span> </td><td> ArcGIS Pro Construction Tool</td></tr>
<tr><td><span title="ArcGIS Pro Custom Control C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProCustomControlC32.png"></span> 
</td>
<td> <span title="ArcGIS Pro Custom Control VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProCustomControlVB32.png"> </span></td>
<td> ArcGIS Pro Custom Control </td></tr>
<tr><td><span title="ArcGIS Pro Custom Item C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProCustomItemC32.png"></span> 
</td>
<td> N/A</td>
<td> ArcGIS Pro Custom Item</td></tr>
<tr><td><span title="ArcGIS Pro Custom Project Item C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProCustomProjectItemC32.png"></span> 
</td>
<td> N/A</td>
<td> ArcGIS Pro Custom Project Item</td></tr>
<tr><td><span title="ArcGIS Pro Dockpane C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDockPaneC32.png"></span> </td><td> <span title="ArcGIS Pro Dockpane VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDockPaneVB32.png"></span> </td><td> ArcGIS Pro Dockpane</td></tr>
<tr><td><span title="ArcGIS Pro Dockpane with Burger Button C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDockPaneC32.png"></span> </td><td> <span title="ArcGIS Pro Dockpane with Burger Button VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDockPaneVB32.png"></span> </td><td> ArcGIS Pro Dockpane with Burger Button</td></tr>
<tr><td><span title="ArcGIS Pro Drop Handler C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDropHandlerC32.png"></span> </td><td> <span title="ArcGIS Pro Drop Handler VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProDropHandlerVB32.png"></span> </td><td> ArcGIS Pro Drop Handler</td></tr>
<tr><td><span title="ArcGIS Pro Embeddable Control C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProEmbeddableControlC32.png"></span> </td><td> <span title="ArcGIS Pro Embeddable Control VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProEmbeddableControlVB32.png"></span> </td><td> ArcGIS Pro Embeddable Control</td></tr>
<tr><td><span title="ArcGIS Pro Gallery C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProGalleryC32.png"></span> </td><td> <span title="ArcGIS Pro Gallery VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProGalleryVB32.png"></span> </td><td> ArcGIS Pro Gallery</td></tr>
<tr><td><span title="ArcGIS Pro Inline-Gallery C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProInLineGalleryC32.png"></span> </td><td> <span title="ArcGIS Pro Inline-Gallery VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProInLineGalleryVB32.png"></span> </td><td> ArcGIS Pro Inline-Gallery</td></tr>
<tr><td><span title="ArcGIS Pro Layout Tool C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProLayoutToolC32.png"></span> </td><td> <span title="ArcGIS Pro Layout Tool">N/A</td><td> ArcGIS Pro Layout Tool</td></tr>
<tr><td><span title="ArcGIS Pro Layout Tray Button C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProLayoutTrayC32.png"></span> </td><td> <span title="ArcGIS Pro Layout Tray Button">N/A</td><td> ArcGIS Pro Layout Tray Button</td></tr>
<tr><td><span title="ArcGIS Pro Map Pane Impersonation C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMapPaneC32.png"></span> </td><td> <span title="ArcGIS Pro Map Pane Impersonation VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMapPaneVB32.png"></span> </td><td> ArcGIS Pro Map Pane Impersonation</td></tr>
<tr><td><span title="ArcGIS Pro Map Tool C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMapToolC32.png"></span> </td><td> <span title="ArcGIS Pro Map Tool VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMapToolVB32.png"></span> </td><td> ArcGIS Pro Map Tool</td></tr>
<tr><td><span title="ArcGIS Pro Map Tray Button C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMapTrayC32.png"></span> </td><td> <span title="ArcGIS Pro Table Construction Tool">N/A</td><td> ArcGIS Pro Map Tray Button</td></tr>
<tr><td><span title="ArcGIS Pro Menu C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMenuC32.png"></span> </td><td> <span title="ArcGIS Pro Menu VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProMenuVB32.png"></span> </td><td> ArcGIS Pro Menu</td></tr>
<tr><td><span title="ArcGIS Pro Pane C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProPaneC32.png"></span> </td><td> <span title="ArcGIS Pro Pane VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProPaneVB32.png"></span> </td><td> ArcGIS Pro Pane</td></tr>
<tr><td><span title="ArcGIS Pro Property Sheet C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProPropertySheetC32.png"></span> </td><td> <span title="ArcGIS Pro Property Sheet VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProPropertySheetVB32.png"></span> </td><td> ArcGIS Pro Property Sheet </td></tr>
<tr><td><span title="ArcGIS Pro ProWindow C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProWindowC32.png"></span> </td><td> <span title="ArcGIS Pro ProWindow VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProWindowVB32.png"></span> </td><td> ArcGIS Pro ProWindow</td></tr>
<tr><td><span title="ArcGIS Pro Split Button C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProSplitButtonC32.png"></span> </td><td> <span title="ArcGIS Pro Split Button VB"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProSplitButtonVB32.png"></span> </td><td> ArcGIS Pro Split Button</td></tr>
<tr><td><span title="ArcGIS Pro Table Construction Tool C#"><img src="https://ArcGIS.github.io/arcgis-pro-sdk/images/VisualStudioTemplates/ArcGISProTableConstToolC32.png"></span> </td><td> <span title="ArcGIS Pro Table Construction Tool">N/A</td><td> ArcGIS Pro Table Construction Tool</td></tr>
</table>

In general, there is a one-to-one correspondence between a framework UI element extensibility point (e.g. button, tool, menu, dockpane, etc) and an item template. Use the relevant item template to add the corresponding extensibility point to your Add-in. 

#### ArcGIS Pro SDK for .NET utilities 
Package: proapp-sdk-utilities.vsix  

ArcGIS Pro SDK for .NET (Utilities) provides the following utilities that extend the Visual Studio environment:

![pro-fix-references](https://ArcGIS.github.io/arcgis-pro-sdk/images/Home/proapp-sdk-utilities.png "ArcGIS Pro SDK(Utilities)") 

Name               | Description
----------------------------  | --------------------------------------
Pro Fix References utility | Fixes broken references in an ArcGIS Pro add-in, core host, configuration, or plug-in projects. Broken references can be caused when you share add-ins with other colleagues or download add-ins where the ArcGIS Pro assembly references point to a different location from where you installed them. Pro Fix References can be run on individual projects or all projects within a solution.
Pro Generate DAML Ids utility| Converts all of the ArcGIS Pro Desktop Application Markup Language (DAML) string IDs into static string properties organized by DAML element types (for example, Button, Dockpane, Tool, Condition, and so on). This allows you to use the IntelliSense feature of Visual Studio within your source code file to add IDs, rather than having to manually type DAML string IDs).

#### ArcGIS Pro SDK for .NET Migration 
Package: proapp-sdk-migration.vsix 

![pro-migration](https://ArcGIS.github.io/arcgis-pro-sdk/images/Home/proapp-sdk-migration.png "ArcGIS Pro SDK(Migration)") 

ArcGIS Pro SDK for .NET (Migration) provides support to migrate ArcGIS Pro SDK 2.x extensions to ArcGIS Pro SDK 3.x for .NET. **Note:** When you migrate your add-in, the dekstopVersion attribute in your config.daml will be set to the current version of ArcGIS Pro installed.

### Previous versions
* [ArcGIS Pro 3.1 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/3.1.0.41833)
* [ArcGIS Pro 3.0 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/3.0.0.36056)
* [ArcGIS Pro 2.9 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.9.0.32739)
* [ArcGIS Pro 2.8 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.8.0.29751)
* [ArcGIS Pro 2.7 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.7.0.26828)
* [ArcGIS Pro 2.6 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.6.0.24783)
* [ArcGIS Pro 2.5 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.5.0.22081)
* [ArcGIS Pro 2.4 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.4.0.19948)
* [ArcGIS Pro 2.3 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.3.0.15769)
* [ArcGIS Pro 2.2 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.2.0.12813)
* [ArcGIS Pro 2.1 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.1.0.10257)
* [ArcGIS Pro 2.0 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/2.0.0.8933)
* [ArcGIS Pro 1.4 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/1.4.0.7198)
* [ArcGIS Pro 1.3 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/1.3.0.5861)
* [ArcGIS Pro 1.2 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/1.2.0.5023)
* [ArcGIS Pro 1.1 SDK for .NET](https://github.com/Esri/arcgis-pro-sdk/releases/tag/1.1.0.3318)


## Resources

* [API Reference online](https://pro.arcgis.com/en/pro-app/latest/sdk/api-reference)
* [ProSnippets: ready-made snippets of code for your ArcGIS Pro add-ins.](https://github.com/Esri/arcgis-pro-sdk/wiki/ProSnippets).
* <a href="https://pro.arcgis.com/en/pro-app/sdk/" target="_blank">ArcGIS Pro SDK for .NET (pro.arcgis.com)</a>
* [arcgis-pro-sdk-community-samples](http://github.com/Esri/arcgis-pro-sdk-community-samples)
* [ArcGIS Pro DAML ID Reference](http://github.com/Esri/arcgis-pro-sdk/wiki/ArcGIS-Pro-DAML-ID-Reference)
* [FAQ](http://github.com/Esri/arcgis-pro-sdk/wiki/FAQ)
* [ArcGIS Pro SDK icons](https://github.com/Esri/arcgis-pro-sdk/releases/tag/3.2.0.xxx)

<p align = center><a href="https://Esri.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-first.png" target="_blank">
  <img align="center" src="https://Esri.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-first.png"/>
</a></p>
<p align = center><a href="https://Esri.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-second.png" target="_blank">
  <img align="center" src="https://Esri.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-second.png"/>
</a></p>
<p align = center><a href="https://ArcGIS.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-third.png" target="_blank">
  <img align="center" src="https://ArcGIS.github.io/arcgis-pro-sdk/images/Home/Image-of-icons-third.png"/>
</a></p>

All the above Pro SDK icons are available as XAML resources in ArcGIS.Desktop.Resources.dll. In your addin Config.daml, you can reference the Pro SDK Icons directly from ArcGIS.Desktop.Resources.dll to use as the image for your controls on the Pro Ribbon. The code snippet below provides the syntax to be used in your add-in's config.daml. Note: "BexDog32" can be replaced by any of the image names listed in the Pro SDK icon images above.

```xml
<button...smallImage="BexDog16" largeImage="BexDog32"/>
```

You can also access these resources as an [ImageSource](https://learn.microsoft.com/en-us/dotnet/api/system.windows.media.imagesource?view=windowsdesktop-7.0) in your WPF code-behind. In the following code snippet, the BexDog32 Pro SDK icon is being accessed as the ImageSource for the return value of an ImageSource property in a view model. Note: "BexDog32" can be replaced by any of the image names listed in the icon image above.

```cs
  public ImageSource SomeCustomProperty {
    get {
       return Application.Current.Resources["BexDog32"] as ImageSource;
    ...
```
