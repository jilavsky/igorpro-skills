---
description: "The TableInfo function returns a string containing a semicolon-separated list of keywords and values that describe a column in a table or overall properties…"
slug: /commands/tableinfo
---

<div className="command-signature">

## <strong>TableInfo</strong> (<em>winNameStr</em>, <em>itemIndex</em>) {#tableinfo}

</div>

The TableInfo function returns a string containing a semicolon-separated list of keywords and values that describe a column in a table or overall properties of the table. The main purpose of TableInfo is to allow an advanced Igor programmer to write a procedure which formats or arranges a table or which manipulates the table selection.

### *Parameters* {#parameters}
*winNameStr* is the name of an existing table window or "" to refer to the top table.

*itemIndex* is one of the following:


|  |  |
| --- | --- |
| -2 | Get information about the table as a whole |
| -1 | Get information about the Point column |
| <span class="table-cell-nowrap">> = 0</span> | Get information about a column other than the Point column. 0 refers to the first column after the Point column, 1 refers to the second column after the Point column, and so on. |

TableInfo returns "" in the following situations:

*winNameStr* is "" and there are no table windows.

*winNameStr* is a name but there are no table windows with that name.

*itemIndex* not -2 and is out of range for an existing column.

### *Details* {#details}
If *itemIndex* is -2, the returned string describes the table as a whole and contains the following keywords, with a semicolon after each keyword-value pair.


| Keyword | Information Following Keyword |
| --- | --- |
| TABLENAME | The name of the table. |
| HOST | The host specification of the table's host window if it is a subwindow or "" if it is a top-level table window. |
| ROWS | Number of used rows in the table. |
| COLUMNS | Number of used columns in the table including the Point column. |
| SELECTION | A description of the table selection as you would specify it when invoking the [ModifyTable](/igorpro/commands/modifytable.md) operation's selection keyword. |
| FIRSTCELL | An identification of the first visible data cell in the top/left corner of the table in row-column format. The first data cell is at location 0, 0. |
| LASTCELL | An identification of the last visible data cell in the bottom/right corner of the table in row-column format. |
| TARGETCELL | An identification of the target (highlighted) data cell in row-column format. |
| ENTERING | 1 if an entry has been started in the entry line, 0 if not. |
| ENTRYTEXT | The text displayed in the entry line. If the user is editing the text in the entry line, this is the text as edited so far. If the user is not editing, it is the value of the first selected cell, as text. |
|  | The ENTRYTEXT keyword is the last keyword-value pair in the returned string. It is not terminated with a trailing ";" character unless the entry line text itself ends with ";". |
|  | The ENTRYTEXT keyword was added in Igor Pro 9.00. |



If *itemIndex* is -1 up to but not including the number of used columns to the right of the Point column, the returned string describes the specified column and contains the following keywords, with a semicolon after each keyword-value pair.


| Keyword | Information Following Keyword |
| --- | --- |
| TABLENAME | The name of the table. |
| HOST | The host specification of the table's host window if it is a subwindow or "" if it is a top-level table window. |
| COLUMNNAME | Name of the column as you would specify it to the [Edit](/igorpro/commands/edit.md) operation if you were creating a table showing just the column of interest. |
| TYPE | Column's type which will be one of the following: Unused, Point, Index, Label, Data, RealData, ImagData. "Index" identifies a index column such as the X values of a wave. "Label" identifies a column of dimension labels. "Data" identifies a data column of a scalar wave. RealData and ImagData identify a real or imaginary column of a complex wave. |
| INDEX | Column's position. -1 refers to the Point column, 0 to the first data column and so on. |
| DATATYPE | Numeric data type of the wave or zero for text waves. See [WaveType](/igorpro/commands/wavetype.md) for a definition of data type codes. |
| WAVE | A full data folder path to the wave displayed in the column or "" for the Point column. |
| COLUMNS | The total number of columns in the table from the wave for the column for which you are getting information. This can be used to skip over all of the columns of a multidimensional wave. |
| HDIM | The wave dimension displayed horizontally as you move from one column to the next. 0 means rows, 1 means columns, 2 means layers, 3 means chunks. |
| VDIM | The wave dimension displayed vertically in the column. 0 means rows, 1 means columns, 2 means layers, 3 means chunks. |
| TITLE | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's title keyword. |
| WIDTH | Column's width in points. |
| FORMAT | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's format keyword. |
| DIGITS | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's digits keyword. |
| SIGDIGITS | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's sigDigits keyword. |
| TRAILINGZEROS | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's trailingZeros keyword. |
| SHOWFRACSECONDS |  |
|  | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's showFracSeconds keyword. |
| FONT | The name of the column's font. |
| SIZE | Column's font size. |
| STYLE | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's style keyword. |
| ALIGNMENT | 0=left, 1=center, 2=right. |
| RGB | The column's color in R,G,B format. |
| RGBA | The column's color in R,G,B,A format. Added in Igor Pro 9.00. |
| ELEMENTS | As specified for the [ModifyTable](/igorpro/commands/modifytable.md) operation's elements keyword. |

### *Examples* {#examples}
This example makes the table's target cell advance by one position within the range of selected cells each time it is called. To try it, create a table, select a range of cells and then run the function using the Macros menu.


```igor
Menu "Macros"
	"Test/1", /Q, AdvanceTargetCell("")
End

Function AdvanceTargetCell(tableName)
	String tableName	// Name of table or "" for top table.
	
	String info = TableInfo(tableName, -2)
	if (strlen(info) == 0)
		return -1		// No such table
	endif
	
	String selectionInfo
	selectionInfo = StringByKey("SELECTION", info)
	
	Variable fRow, fCol, lRow, lCol, tRow, tCol
	sscanf selectionInfo, "%d,%d,%d,%d,%d,%d", fRow, fCol, lRow, lCol, tRow, tCol

	tCol += 1
	if (tCol > lCol) 
		tCol = fCol
		tRow += 1
		if (tRow > lRow)
			tRow = fRow
		endif
	endif
	
	ModifyTable selection=(-1, -1, -1, -1, tRow, tCol)
End
```