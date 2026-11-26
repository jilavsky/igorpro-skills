---
description: "The PrintSettings operation gets or sets parameters associated with printing, such as a list of available printers or page setup information for a particular…"
slug: /commands/printsettings
---

<div className="command-signature">

## <strong>PrintSettings</strong>  [ /I /M /W=<em>winName</em> ] [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#printsettings}

</div>

The PrintSettings operation gets or sets parameters associated with printing, such as a list of available printers or page setup information for a particular window.

An exception is the graphMode and graphSize keyword pair which affect printing of all graphs. This pair was added in Igor Pro 7.00.

Prior to Igor Pro 7.00, PrintSettings applied to a page layout affected the size and orientation of the layout page. In Igor Pro 7.00 and later, the size and orientation of the layout page are independent of print settings. See [Page Layout Page Sizes](/igorpro/graphing/making-figures/page-layouts.md#page-layout-page-sizes) for details.

When getting or setting page setup information, PrintSettings acts on a particular window called the destination window. The destination window is the top graph, table, page layout, or notebook window or the window specified by the /W flag.

PrintSettings cannot act on page setup records associated with the command window, procedure windows, help windows, control panel, XOP windows, or any type of window other than graphs, tables, page layouts, and notebooks.

The PrintSettings operation services the keywords in the order shown above, not in the order in which they appear in the command. Thus, for example, the getPageSettings and getPageDimensions keywords report the settings after all other keywords are executed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Measurements are in inches. If both /I and /M are omitted, measurements are in points. |
| <span class="table-cell-nowrap">/M</span> | Measurements are in centimeters. If both /I and /M are omitted, measurements are in points. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Acts on the page setup record of the graph, table, page layout, or notebook window identified by *winName*. If *winName* is omitted or if *winName* is "", then it used the page setup for the top window. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">colorMode = *m*</span> | Sets the color mode for the page setup to monochrome (*m* =0) or to color (*m* =1). |
| <span class="table-cell-nowrap">copySource = *source*</span> | Copies page setup settings from the specified source to the destination window. *source* can be the name of a graph, table, page layout, or notebook window or it can be one of the following special keywords: |
|  |<table class="nested-table"><tbody><tr><td>Default_Settings:</td><td>Sets the page setup record to the default for the associated printer as specified by the printer driver.</td></tr><tr><td>Factory_Settings:</td><td>Sets the page setup record to the WaveMetrics factory default. This is the page setup you get when creating a new window with user preferences turned off.</td></tr><tr><td>Preferred_Settings:</td><td>Sets the page setup record to the user preferred page setup. This is the page setup you get when creating a new window with user preferences turned on. Because there is only one page setup for all graphs and one page setup for all tables, this has no effect when the destination window is a graph or table. It does work for layouts and notebooks.</td></tr></tbody></table>
| getPageDimensions | Returns page dimensions via the string variable S_value, which contains keyword-value pairs that can be extracted using [NumberByKey](/igorpro/commands/numberbykey.md) and [StringByKey](/igorpro/commands/stringbykey.md). See Details below for keyword-value pair descriptions. |
| getPageSettings | Returns page setup settings via the string variable S_value, which contains keyword-value pairs that can be extracted using [NumberByKey](/igorpro/commands/numberbykey.md) and [StringByKey](/igorpro/commands/stringbykey.md). See Details below for keyword-value pair descriptions. |
| getPrinterList | Returns a semicolon-separated list of printer names in the string variable S_value. |
|  | This keyword returns the names of any local printers and names of network printers to which the user has made previous connections. |
| getPrinter | Returns the name of the selected printer for the destination window in the string variable S_value. |
| <span class="table-cell-nowrap">graphMode = *g*</span> | Sets the printing mode for graphs: |
|  |<table class="nested-table"><tbody><tr><td>*g*&nbsp;=&nbsp;1:</td><td>Fill page</td></tr><tr><td>*g*&nbsp;=&nbsp;2:</td><td>Same size</td></tr><tr><td>*g*&nbsp;=&nbsp;3:</td><td>Same aspect ratio</td></tr><tr><td>*g*&nbsp;=&nbsp;4:</td><td>Custom size as set by graphSize keyword</td></tr><tr><td>*g*&nbsp;=&nbsp;5:</td><td>Same size or shrink to fit page (default)</td></tr></tbody></table>
|  | This setting is not saved and is set to 5 when Igor starts. |
|  | The graphMode keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">graphSize = {*left*, *top*, *width*, *height* }</span> |  |
|  | Sets the custom graph size used when graphMode is 4. Parameters are in points unless /I or /M is used. |
|  | Invoking the graphSize keyword automatically sets the graphMode to 4. |
|  | *left* and *top* are clipped so that they are no smaller than the minimum allowed by the printer driver. *width* and *height* are not clipped. |
|  | This setting is not saved and is set to a default value when Igor starts. |
|  | The graphSize keyword was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">margins = {*left*, *top*, *right*, *bottom* }</span> |  |
|  | Sets the page margins. Measurements are in points unless /I or /M is used. |
|  | This setting is ignored for notebook windows. Use the Notebook operation pageMargins keyword instead. |
|  | The margins are clipped so that they are no smaller than the minimum allowed by the printer driver and no larger than one-half the size of the paper. |
|  | The terms "left", "top", "right" and "bottom" refer to the sides of the page after possible rotation for landscape orientation. |
|  | Passing zero for all four margins sets the margins to the minimum margin allowed by the printer. |
| <span class="table-cell-nowrap">orientation = *o*</span> | Sets the paper orientation to portrait (*o* =0) or to landscape (*o* =nonzero). |
| <span class="table-cell-nowrap">scale = *s*</span> | In Igor Pro 7 and later, the scale keyword returns an "unimplemented" error, unless *s* =100, because it is currently not supported. Let us know if this feature is important to you. Though *s* =100 does not generate an error, it does nothing. You can still set the scaling manually using the Page Setup dialog. |
| <span class="table-cell-nowrap">setPrinter = *printerNameStr*</span> |  |
|  | Sets the selected printer for the destination window. |
|  | SetPrinter attempts to preserve orientation, margins, scale and color mode but other settings may revert to the default state. |
|  | *printerNameStr* is a name as returned by the getPrinterList keyword and cannot be identical to the name displayed in various dialogs. |
|  | If *printerNameStr* is "", the printer for the destination window is set to the default state. This means different things depending on the operating system: |
|  | The destination window will use the system default printer. |
|  | If you receive an error when using setPrinter, use the getPrinterList keyword to verify that the printer name you are using is correct. Verify that the printer is connected and turned on. |
|  | Windows printer names are sometimes UNC names of the form "\\\\Server\\Printer". You must double-up backslashes when using a UNC name in a literal string. See [UNC Paths](/igorpro/user-interface/platform-related-issues.md#unc-paths) for details. |

### *Details* {#details}
All graphs in the current experiment share a single page setup record so if you change the page setup for one graph, you change it for all graphs.

All tables in the current experiment share a single page setup record.

Each page layout window has its own page setup record.

Each notebook window has its own page setup record.

The keyword-value pairs for the getPageSettings keyword are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| ORIENTATION: | 0 if the page is in portrait orientation, 1 if it is in landscape orientation. |
| MARGINS: | The left, top, right and bottom margins in points, separated by commas. |
|  | These margins are ignored for notebook windows. Use the Notebook operation pageMargins keyword instead. |
| SCALE: | The page scaling expressed in percent. 50 means that the graphics are drawn at 50% of their normal size. |
| COLORMODE: | 0 for black&white, 1 for color. |



The keyword-value pairs for the getPageDimensions keyword are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| PAPER: | The left, top, right and bottom coordinates of the paper in points, separated by commas. The top and left are negative numbers so that the page can start at (0,0). |
| PAGE: | The left, top, right and bottom coordinates of the page in points, separated by commas. The term page refers to the part of the paper inside the margins. The top/left corner of the page is always at (0, 0). |
| PRINTAREA: | The left, top, right and bottom coordinates of the page in points, separated by commas. The print area is the part of the paper on which printing can occur, as determined by the printer. This is equal to the paper inset by the minimum supported margins. The top and left are negative numbers so that the page can start at (0,0). |

### *Examples* {#examples}
For an example using the PrintSettings operation, see the PrintSettings Tests example experiment file in "Igor Pro Folder:Examples:Testing".

Here are some simple examples showing how you can use the PrintSettings operation.


```igor
Function GetOrientation(name)   // Returns 0 (portrait) or 1 (landscape)
    String name                 // Name of graph, table, layout or notebook

	PrintSettings/W=$name getPageSettings
	Variable orientation = NumberByKey("ORIENTATION", S_value)
	return orientation
End

Function SetOrientationToLandscape(name)
	String name                 // Name of graph, table, layout or notebook

	PrintSettings/W=$name orientation=1
End

Function/S GetPrinterList()
	PrintSettings getPrinterList
	return S_value
End

Function SetPrinter(destWinName, printerName)
	String destWinName, printerName
	
	PrintSettings/W=$destWinName setPrinter=printerName
	return 0
End
```

### *Demos* {#demos}
[Open PrintSettings Demo](#igor-pxp/Examples/Testing/PrintSettings__Test.pxp)

### *See Also* {#see-also}
[PrintGraphs](/igorpro/commands/printgraphs.md), [PrintTable](/igorpro/commands/printtable.md), [PrintLayout](/igorpro/commands/printlayout.md), [PrintNotebook](/igorpro/commands/printnotebook.md)