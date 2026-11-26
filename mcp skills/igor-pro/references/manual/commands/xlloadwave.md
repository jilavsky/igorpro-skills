---
description: "The XLLoadWave operation loads data from the named Excel.xls,.xlsx or.xlsm file into waves."
slug: /commands/xlloadwave
---

<div className="command-signature">

## <strong>XLLoadWave</strong>  [<em>flags</em> ] <em>fileNameStr</em> {#xlloadwave}

</div>

The XLLoadWave operation loads data from the named Excel .xls, .xlsx or .xlsm file into waves.

XLLoadWave does not support .xlsb files and cannot load password-protected Excel files.

### *Parameters* {#parameters}
The file to be loaded is specified by *fileNameStr* and /P=*pathName* where *pathName* is the name of an Igor symbolic path. *fileNameStr* can be a full path to the file, in which case /P is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If XLLoadWave cannot determine the location of the file from *fileNameStr* and *pathName*, it displays a dialog allowing you to specify the file.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If *fileNameStr* is omitted or is "", or if the /I flag is used, XLLoadWave presents an Open File dialog from which you can choose the file to load.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Automatically assigns arbitrary wave names using "wave" as the base name. Skips names already in use. |
| <span class="table-cell-nowrap">/A = *baseName*</span> | Same as /A but it automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/C = *columnType*</span> | XLLoadWave will use the [Deduce from Row](/igorpro/data/importing-and-exporting-data.md#deduce-from-row) method of determining the type of the Excel file columns, using the row specified by *columnType* to deduce column types. |
| <span class="table-cell-nowrap">/COLT = *columnTypeStr*</span> | *columnTypeStr* specifies how XLLoadWave should treat each column. For example, "1T3N" means 1 text column followed by 3 numeric columns. See ***Determining Wave Types*** below. |
| <span class="table-cell-nowrap">/D</span> | Creates double-precision floating point waves. If omitted, XLLoadWave creates single-precision floating point waves. |
| <span class="table-cell-nowrap">/I</span> | Causes XLLoadWave to display the Open File dialog and another dialog that allows you to set the range of cells to load as well as other parameters. |
| <span class="table-cell-nowrap">/J = *infoMode*</span> | If *infoMode* is 1, 2 or 3, XLLoadWave does not load the file but instead returns information about the worksheets within the workbook via the string variable S_value. See ***Getting Information About the Excel File*** below. |
| <span class="table-cell-nowrap">/K = *k*</span> | Discards waves with fewer than *k* points. For historical reasons, *k* defaults to 2. |
| <span class="table-cell-nowrap">/N</span> | Same as /A except that, instead of choosing names that are not in use, it overwrites existing waves. |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Same as /N except that Igor automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/NAME = *nameList*</span> | *nameList* is a semicolon-separated list of wave names to be used for the loaded waves. See ***Wave Names*** below for details. |
| <span class="table-cell-nowrap">/O</span> | Overwrites existing waves in case of a name conflict. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* *pathName* is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses the normal messages in the history area. |
| <span class="table-cell-nowrap">/R = (*cell1*,*cell2*)</span> | Restricts loading to specified cells, e.g. /R=(A3,D21). Row and column numbers start from 1. |
|  | The /R flag supports an optional extra parameter that should be used only in very rare cases. XLLoadWave reads the range of defined cells from the file itself and clips *cell1* and *cell2* to that range. |
|  | In very rare cases the file does not accurately identify the range of defined cells so the clipping prevents loading cells that exist in the file. In this rare case, use /R=(*cell1*, *cell2*, 1). The last parameter tells XLLoadWave to skip the clipping. If you specify incorrect values for cell1 or cell2 you may get errors or garbage results. |
| <span class="table-cell-nowrap">/S = *sheetNameStr*</span> | Specifies which worksheet to load from a workbook file. If you omit /S=*sheetNameStr*, or if *sheetNameStr* is "", XLLoadWave loads the first worksheet in the workbook. |
| <span class="table-cell-nowrap">/T</span> | Automatically creates a table of loaded waves. |
| <span class="table-cell-nowrap">/V = *v*</span> | Controls the handling of blanks at the end of a column. |
|  |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=0:</td><td>XLLoadWave leaves blanks at the end of a column in the Igor wave.</td></tr><tr><td>*v*&nbsp;=1:</td><td>XLLoadWave removes blanks at the end of a column from the Igor wave. If the column has fewer than two remaining points, it is not loaded into a wave. This is the default mode that is used if you omit /V.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = *w*</span> | *w* specifies the row in which XLLoadWave will look for wave names. The first row is row number 1. |

### *Wave Names* {#wave-names}
The names of the loaded waves are determined by the /A, /N, /W and /NAME flags. If all of the flags are omitted, default names, like ColumnA and ColumnB, are used.

If /W=*w* is present, names are loaded from row *w* of the worksheet and then converted to standard Igor names by replacing spaces and punctuation characters with underscores.

If /NAME=*nameList* is present, the wave names come from *nameList*, a semicolon-separated list of names. For example:


```igor
/NAME="StartTime;UnitA;UnitB;"
```

The names in *nameList* can be standard or liberal names. For example, this specifies names two standard names and one liberal name which contains a space:


```igor
/NAME="Signal;Ambient Temp;Response;"
```

If a name in the list is \_skip\_, the corresponding Excel column is skipped. For example, this would load the first and third columns and skip the second:


```igor
/NAME="Signal;_skip_;Response;"
```

If a name in the list is empty, the name used for the corresponding wave is as it would be if /NAME were omitted. This can be used to skip columns while taking wave names from the spreadsheet for loaded columns. In this example, the names of the first and third waves would be determined by row 1 of the spreadsheet while the second column would be skipped:


```igor
/W=1 /NAME=";_skip_;;"
```

The /N flag instructs Igor to automatically name new waves "wave", or *baseName* if /N=*baseName* is used, plus a number. The number starts from zero and increments by one for each wave loaded from the file. If the resulting name conflicts with an existing wave, the existing wave is overwritten.

The /A flag is like /N except that it skips names already in use.

/NAME overrides /W. /A or /N overrides both /NAME and /W.

No matter how the wave names are generated, if there is a name conflict and overwrite is off (/O is omitted), a unique name is generated. See [XLLoadWave and Wave Names](/igorpro/data/importing-and-exporting-data.md#xlloadwave-and-wave-names) for further details.

### *Determining Wave Types* {#determining-wave-types}
The /C or /COLT flag tells XLLoadWave how to decide what kind of wave, numeric, text, or date/time, to make for each Excel column.

Using /C=*columnType* causes XLLoadWave to use the [Deduce from Row](/igorpro/data/importing-and-exporting-data.md#deduce-from-row) method of determining the type of the Excel file columns. *columnType* is the Excel row number that XLLoadWave should use to make the deduction.

Using /COLT=*columnTypeStr* causes XLLoadWave treat the columns based on the *columnTypeStr* parameter. If *columnTypeStr* is "N", XLLoadWave uses the [Treat all Columns as Numeric](/igorpro/data/importing-and-exporting-data.md#treat-all-columns-as-numeric) method. If *columnTypeStr* is "T", XLLoadWave uses the [Treat all Columns as Text](/igorpro/data/importing-and-exporting-data.md#treat-all-columns-as-text) method. If *columnTypeStr* is "D", XLLoadWave uses the [Treat all Columns as Date](/igorpro/data/importing-and-exporting-data.md#treat-all-columns-as-date) method.

For any other value of *columnTypeStr*, XLLoadWave uses the [Use Column Type String](/igorpro/data/importing-and-exporting-data.md#use-column-type-string) method. For example, "1T5N" tells XLLoadWave to create a text wave for the first column and numeric waves for the next 5 or more columns.

If you omit /C and /COLT, XLLoadWave uses the [Treat all columns as numeric](/igorpro/data/importing-and-exporting-data.md#treat-all-columns-as-numeric) method.

See [What XLLoadWave Loads](/igorpro/data/importing-and-exporting-data.md#what-xlloadwave-loads) for further details.

### *Output Variables* {#output-variables}
XLLoadWave sets the following output variables:


|  |  |
| --- | --- |
| V_flag | Number of waves loaded. |
| S_fileName | Name of the file being loaded. |
| S_path | File system path to the folder containing the file. |
| S_waveNames | Semicolon-separated list of the names of loaded waves. |
| S_worksheetName | Name of the loaded worksheet within the workbook file. |
| S_value | Set only if you use the /J flag. See ***Getting Information About the Excel File*** below. |

S_path uses Macintosh path syntax (e.g., "hd:FolderA:FolderB:"), even on Windows. It includes a trailing colon.

When XLLoadWave presents an Open File dialog and the user cancels, V_flag is set to 0 and S_fileName is set to "".

### *Getting Information About the Excel File* {#getting-information-about-the-excel-file}
The /J flag allows you to get information about an Excel file without actually loading it.

If *infoMode* is 1, XLLoadWave does not load the file but instead returns a semicolon-separated list of the names of the worksheets within the workbook via the string variable S_value.

If *infoMode* is 2, XLLoadWave does not load the file but instead returns information about the first worksheet or the worksheet specified by /S via the string variable S_value. The format of the returned information is:


```
NAME:<worksheet name>;FIRSTROW:<first row>;FIRSTCOL:<first col>;LASTROW:<last row>;LASTCOL:<last col>;
```

\<first row\> and \<last row\> are 1-based row numbers. \<first col\> and \<last col\> are 1-based column numbers; 1 refers to Column A. These refer to the defined rows and columns in the worksheet even if some or all cells are blank. If \<last col\> is zero, this means that there are no defined cells in the worksheet.

If *infoMode* is 3, XLLoadWave does not load the file but instead returns information about the first worksheet or the worksheet specified by /S via the string variable S_value. The format of the returned information is:


```
NAME:<worksheet name>;FIRST:<first cell>;LAST:<last cell>;
```

\<first cell\> and \<last cell\> are expressed in standard Excel notation (A1, B24, etc.). These refer to the defined rows and columns in the worksheet even if some or all cells are blank. If \<last cell\> is "@0", this means that there are no defined cells in the worksheet.

Use the [StringByKey](/igorpro/commands/stringbykey.md), [NumberByKey](/igorpro/commands/numberbykey.md) functions to extract the information from S_value. If you use these functions, your code won't break if we later add a keyword/value pair to the returned information.

### *Examples* {#examples}
Old versions of Excel came with a number of sample files. One of them was called "Instrument Data". The following procedure loads an area of this file, makes a table and then makes a graph of the loaded waves.

This example assumes that you have the "Instrument Data.xls" file and a symbolic path named Science that points to the folder containing the file.


```igor
Function InstrumentData()
	// Load Instrument Data file from the Scientific Analysis folder
	XLLoadWave/O/T/R=(C9,M27)/W=8/C=9/P=Science "Instrument Data.xls"

	// Make graph.
	Display M1, M2, M3 vs X_Time
	Label bottom, "Time"; Label left, "Mass"
	ModifyGraph dateInfo(bottom)={1,0,0}
End
```

See also [Loading Excel Data Into a 2D Wave](/igorpro/data/importing-and-exporting-data.md#loading-excel-data-into-a-2d-wave).