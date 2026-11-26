---
description: "The ModifyTable operation modifies the appearance of the top or named table window or subwindow."
slug: /commands/modifytable
---

<div className="command-signature">

## <strong>ModifyTable</strong>  [/W=<em>winName</em> /Z] [<em>keyword</em>=<em>value</em>, <em>keyword</em>=<em>value</em>, ...] {#modifytable}

</div>

The ModifyTable operation modifies the appearance of the top or named table window or subwindow.

### *Parameters* {#parameters}
Many of the parameter keywords take an optional *columnSpec* (abbreviated as *col* in the synopsis above) enclosed in parentheses. Usually *columnSpec* is simply the name of a wave displayed in the table. If "(*columnSpec*)" is omitted, all columns in the table are affected.

More precisely, column specifications are wave names for waves in the current data folder or data folder paths leading to waves in any data folder optionally followed by the suffixes .i, .l, .d, .id or .ld to specify dimension indices, dimension labels, data values, dimension indices and data values, or dimension labels and data values of the wave. For example, ModifyTable font(myWave.i)="Helvetica". If the wave is complex, the column specification may be followed by .real or .imag suffixes.

One additional *columnSpec* is Point, which refers to the first column containing the dimension index numbers. If multidimensional waves are displayed in the table, this column may have the title "Row", "Column", "Layer", "Chunk" or "Element", but the *columnSpec* for this column is always Point. See [Column Names](/igorpro/igor-basics/tables.md#column-names) in the Tables help file for details.

Though not shown in the syntax, the optional "(*columnSpec* )" may be replaced with "[*columnIndex* ]", where *columnIndex* is zero or a positive integer denoting the column to be modified. "[0]" denotes the Point column, "[1]" denotes the first column appended to the table, "[2]" denotes the second appended column, etc. This syntax is used for style macros, in conjunction with the /Z flag.

You can use a range of column numbers instead of just a single column number, for example "[0,3]".

The parameter descriptions below omit the optional "(*columnSpec* )".


|  |  |
| --- | --- |
| alignment=*a* |<table class="nested-table"><tbody><tr><td>*a*&nbsp;=0:</td><td>Left alignment.</td></tr><tr><td>*a*&nbsp;=1:</td><td>Center alignment.</td></tr><tr><td>*a*&nbsp;=2:</td><td>Right alignment.</td></tr></tbody></table>
| <span class="table-cell-nowrap">autosize = {*mode*, *options*, *padding*, *perColumnMaxSeconds*, *totalMaxSeconds* }</span> |  |
|  | Autosizes the specified column or columns. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>Sets width of each data column from a given multidimensional wave individually.</td></tr><tr><td>*mode*=1:</td><td>Sets width of all data columns from a given multidimensional wave the same.</td></tr></tbody></table>
|  | *options* is a bitwise parameter. Usually 0 is the best choice. |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Ignores column names.</td></tr><tr><td>bit&nbsp;1:</td><td>Ignores horizontal indices.</td></tr><tr><td>bit&nbsp;2:</td><td>Ignores data cells.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | *padding* specifies extra padding for each column in points. Use -1 to get the default amount of padding (16 points). |
|  | *perColumnMaxSeconds* specifies the maximum amount of time to spend autosizing a single column. Use 0 to get the default amount of time (one second). |
|  | *totalmaxSeconds* specifies the maximum amount of time to spend autosizing the entire table. Use 0 to get the default amount of time (ten seconds). |
| <span class="table-cell-nowrap">digits = *d*</span> | *d* is number of digits after decimal point or, for hex and octal columns, the number of total digits. |
| <span class="table-cell-nowrap">elements = (*row*, *col*, *layer*, *chunk* )</span> |  |
|  | Selects the view of a multidimensional wave in the table. The values given to *row*, *col*, *layer*, *chunk* are codes telling Igor how to change the view. |
|  |<table class="nested-table"><tbody><tr><td>-1:</td><td>No change from current view.</td></tr><tr><td>-2:</td><td>Display this dimension vertically.</td></tr><tr><td>-3:</td><td>Display this dimension horizontally.</td></tr><tr><td>&gt;=0:</td><td>For waves with 3 or 4 dimensions, display this element of the other dimensions.</td></tr></tbody></table>
|  | See [ModifyTable Elements Command](/igorpro/igor-basics/tables.md#modifytable-elements-command) for a detailed discussion of this keyword. |
| <span class="table-cell-nowrap">entryMode = *m*</span> | Queries or sets the table's entry line mode. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Just queries.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Accepts any entry that was started if possible.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Cancels any entry that was started if possible.</td></tr></tbody></table>
|  | If *m* is 0 then the entry line state is not changed but is returned via the V_flag variable as follows: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No entry is in progress.</td></tr><tr><td>-1:</td><td>An entry is in progress and is valid.</td></tr><tr><td>Other:</td><td>An entry is in progress and is invalid.</td></tr></tbody></table>
|  | In Igor Pro 8.03 and later, S_value is set to contain the text showing in the entry line. |
|  | If *m* is 1 then the entry is accepted if it is valid and its state is returned via the V_flag variable as follows: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No entry is in progress.</td></tr><tr><td>-1:</td><td>The entry was accepted.</td></tr><tr><td>Other:</td><td>The entry is invalid and was not accepted.</td></tr></tbody></table>
|  | In Igor Pro 8.03 and later, S_value is set to contain the text showing in the entry line whether or not an entry was in progress and whether or not it was accepted. |
|  | If *m* is 2 then the entry is cancelled if possible and its state is returned via the V_flag variable as follows: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No entry is in progress.</td></tr><tr><td>-1:</td><td>The entry was cancelled.</td></tr></tbody></table>
|  | In Igor Pro 8.03 and later, S_value is set to contain the text showing in the entry line after the entry was cancelled. |
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Font name (e.g., font="Helvetica"). |
| <span class="table-cell-nowrap">format = *f*</span> | Sets the data format for the table. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>General.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Integer.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Integer with thousands (e.g., &quot;1,234&quot;).</td></tr><tr><td>*f*&nbsp;=3:</td><td>Decimal (e.g., &quot;1234.56&quot;).</td></tr><tr><td>*f*&nbsp;=4:</td><td>Decimal with comma (e.g., &quot;1,234.56&quot;).</td></tr><tr><td>*f*&nbsp;=5:</td><td>Scientific (e.g., 1.23456e3).</td></tr><tr><td>*f*&nbsp;=6:</td><td>Date format.</td></tr><tr><td>*f*&nbsp;=7:</td><td>Time format (always 24 hour time).</td></tr><tr><td>*f*&nbsp;=8:</td><td>Date&amp;time format (date followed by time).</td></tr><tr><td>*f*&nbsp;=9:</td><td>Octal.</td></tr><tr><td>*f*&nbsp;=10:</td><td>Hexadecimal.</td></tr></tbody></table>
|  | You cannot apply date or date&time formats to a wave that is not double-precision (see [Date, Time, and Date&Time Units](/igorpro/igor-basics/waves.md#date-time-and-date-time-units)). To avoid this error, use [Redimension](/igorpro/commands/redimension.md) to change the wave to double-precision. |
| <span class="table-cell-nowrap">frameInset = *i*</span> | Specifies the number of pixels by which to inset the frame of the table subwindow. |
| <span class="table-cell-nowrap">frameStyle = *f*</span> | Specifies the frame style for a table subwindow. Values for frameStyle are: |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>None</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow</td></tr><tr><td>*f*&nbsp;=5:</td><td>Indented</td></tr><tr><td>*f*&nbsp;=6:</td><td>Raised</td></tr><tr><td>*f*&nbsp;=7:</td><td>Text well</td></tr></tbody></table>
|  | The last three styles are fake 3D and will look good only if the background color of the enclosing space and the table itself is a light shade of gray. |
| <span class="table-cell-nowrap">horizontalIndex = *h*</span> | Controls what is displayed in the horizontal index row when multidimensional waves are displayed. |
|  |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=0:</td><td>Displays dimension labels if the multidimensional wave&#39;s label column is displayed, otherwise displays numeric indices (default).</td></tr><tr><td>*h*&nbsp;=1:</td><td>Always displays numeric indices for multidimensional waves.</td></tr><tr><td>*h*&nbsp;=2:</td><td>Always displays dimension labels for multidimensional waves.</td></tr></tbody></table>
|  | The horizontal index row appears below the row of column names if the table contains a multidimensional wave. Use horizontalIndex to override the default behavior in order to display labels for the horizontal dimension while displaying numeric indices for the vertical dimension or vice versa. |
|  | The horizontalIndex keyword controls the horizontal index row only. To control what is displayed vertically, append a numeric index or dimension label column using [AppendToTable](/igorpro/commands/appendtotable.md). |
| <span class="table-cell-nowrap">rgb = (*r*,*g*,*b*[,*a*])</span> | Sets color of text. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black. |
| <span class="table-cell-nowrap">selection = (*firstRow* , *firstCol* , *lastRow* , *lastCol* , *targetRow* , *targetCol* )</span> |  |
|  | Sets the selected cells in the table. |
|  | If any of the parameters have the value -1 then the corresponding part of the selection is not changed. |e 
|  | Otherwise they set the first and last selected cell and the target cell. Row and column values are 0 oreater. The Point column cannot be selected. |
|  | The proposed parameters are clipped to avoid invalid combinations, such as the last selected row being before the first selected row. |
|  | With one exception, Igor does not support selecting unused cells. Therefore the proposed selection is clipped to prevent this. The exception is that, if the parameters call for selecting the first cell in the first unused column, then this is permitted. |
| showFracSeconds=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Don&#39;t show fractional seconds in time data. (Default)</td></tr><tr><td>*s*&nbsp;=1:</td><td>&quot;&quot;Show fractional seconds in time data.</td></tr></tbody></table>
| <span class="table-cell-nowrap">showParts = *parts*</span> | Specifies what elements of the table should be visible. Other elements are hidden. |
|  | *parts* is a bitwise parameter specifying what to show. |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Entry line and other top line controls.</td></tr><tr><td>bit&nbsp;1:</td><td>Name row.</td></tr><tr><td>bit&nbsp;2:</td><td>Horizontal index row.</td></tr><tr><td>bit&nbsp;3:</td><td>Point column.</td></tr><tr><td>bit&nbsp;4:</td><td>Horizontal scroll bar.</td></tr><tr><td>bit&nbsp;5:</td><td>Vertical scroll bar.</td></tr><tr><td>bit&nbsp;6:</td><td>Selection highlighting.</td></tr><tr><td>bit&nbsp;7:</td><td>Insertion cells.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero except that you can pass -1 to indicate that you want to show all parts of the table. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | Presentation tables in subwindows in graphs and page layouts do not have an entry line or scroll bars and therefore never show these items. |
|  | See [Parts of a Table](/igorpro/igor-basics/tables.md#parts-of-a-table) and [Showing and Hiding Parts of a Table](/igorpro/igor-basics/tables.md#showing-and-hiding-parts-of-a-table) for further information. |
| <span class="table-cell-nowrap">sigDigits = *d*</span> | *d* is number of significant digits when the numeric format is general. |
| <span class="table-cell-nowrap">size = *s*</span> | Font size, e.g., size=14. |
| <span class="table-cell-nowrap">style = *n*</span> | *n* is a bitwise parameter with each bit controlling one aspect of the column's font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | For example, bold underlined is 2<sup>0</sup> + 2<sup>2</sup> = 1 + 4 = 5. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">title = "*title"*</span> | Sets the title of a column to *title*. |
| <span class="table-cell-nowrap">topLeftCell = (*row* , *column* )</span> |  |
|  | Scrolls the table contents so that the cell identified by (*row* , *column* ) is the top/left visible data cell, or as close as possible. |
|  | If *row* is -1 then the table's vertical scrolling is not changed. If *column* is -1 then the table's horizontal scrolling is not changed. |
|  | If they are positive, *row* and *column* are zero-based numbers which are clipped to valid values before being used. *row* =0 refers to the first row of data in the table, *column* =0 refers to the first column of data. |
|  | The Point column cannot be scrolled horizontally. |
| <span class="table-cell-nowrap">trailingZeros = *t*</span> | *t* =1 shows trailing zeros. This affects the general numeric format only. |
| viewSelection | Scrolls the table contents so that the target cell and selection are maximally in view. The target cell will always be visible. The selection may overflow the visible area. |
|  | See also the topLeftCell and selection keywords. |
| viewSelection was added in Igor Pro 9.00. |  |
| <span class="table-cell-nowrap">width = *w*</span> | Sets column width to *w* points. |
|  | You will not always get the exact number of points that you request. This is because Igor requires that a column be an even number of screen pixels, so that grid lines look good. Igor will modify your requested number of points to meet this requirement. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the named table window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | No errors generated if the indexed or specified column does not exist in a style macro. |