---
description: "The ListBox operation creates or modifies the named control that displays, in the target window, a list from which the user can select any number of items."
slug: /commands/listbox
---

<div className="command-signature">

## <strong>ListBox</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#listbox}

</div>

The ListBox operation creates or modifies the named control that displays, in the target window, a list from which the user can select any number of items.

For information about the state or status of the control, use the [ControlInfo](/igorpro/commands/controlinfo.md) operation.

### *Parameters* {#parameters}
*ctrlName* is the name of the ListBox control to be created or changed.

The following keyword=value parameters are supported:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">align = *alignment*</span> | Sets the alignment mode of the control. The alignment mode controls the interpretation of the *leftOrRight* parameter to the pos keyword. The align keyword was added in Igor Pro 8.00. |
|  | If *alignment*=0 (default), *leftOrRight* specifies the position of the left end of the control and the left end position remains fixed if the control size is changed. |
|  | If *alignment*=1, *leftOrRight* specifies the position of the right end of the control and the right end position remains fixed if the control size is changed. |
| <span class="table-cell-nowrap">appearance = {*kind* [, *platform* ]}</span> |  |
|  | Sets the appearance of the control. *platform* is optional. Both parameters are names, not strings. |
|  | *kind* can be one of default, native, or os9. |
|  | *platform* can be one of Mac, Win, or All. |
|  | See [Button](/igorpro/commands/button.md) and [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md) for more appearance details. |
| <span class="table-cell-nowrap">clickEventModifiers = *modifierSelector*</span> |  |
|  | Selects modifier keys to ignore when processing clicks to start editing a cell or when toggling a checkbox. That is, use this keyword if you want to prevent a shift-click (for instance) from togging checkbox cells. Allows the action procedure to receive mousedown events with those modifiers without interfering with actions on the part of the listbox control. |
|  | *modifierSelector* is a bit pattern with a bit for each modifier key; sum these values to get the desired combination of modifiers: |
|  |<table class="nested-table"><tbody><tr><td>*modifierSelector*=1:</td><td>This modifier key has no effect.</td></tr><tr><td>*modifierSelector*=2:</td><td>Alt</td></tr><tr><td>*modifierSelector*=4:</td><td>Context click (right click)</td></tr><tr><td>*modifierSelector*=8:</td><td>Shift key</td></tr><tr><td>*modifierSelector*=16:</td><td>Ctrl key</td></tr><tr><td>*modifierSelector*=32:</td><td>Caps lock key</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">col = *c*</span> | Sets the left-most visible column (user scrolling will change this). The list is scrolled horizontally as far as possible. Sometimes this won't be far enough to actually make column c the first column, but it will at least be visible. Use *c* =1 to put the left edge of column 1 (the **second** column) at the left edge of the list |
| <span class="table-cell-nowrap">colorWave = *cw*</span> | Specifies a 3-column (RGB) or 4-column (RGBA) numeric wave. Used in conjunction with planes in selWave to define foreground and background colors for individual cells. Values range from 65535 (full on) to 0. |
| <span class="table-cell-nowrap">disable = *d*</span> | Sets user editability of the control. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=0:</td><td>Normal.</td></tr><tr><td>*d*&nbsp;=1:</td><td>Hide.</td></tr><tr><td>*d*&nbsp;=2:</td><td>Draw in gray state; disable control action.</td></tr></tbody></table>
| <span class="table-cell-nowrap">editStyle = *e*</span> | Sets style for cells designated as editable (see selWave, bit 1). |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Uses a light blue background (default).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Draws a frame around the cell with a white background.</td></tr><tr><td>*e*&nbsp;=&nbsp;2:</td><td>Combines the frame with the blue background. The background in all cases can be overridden using the colorWave parameter.</td></tr></tbody></table>
| <span class="table-cell-nowrap">focusRing = *fr*</span> | Enables or disables the drawing of a rectangle indicating keyboard focus: |
|  |<table class="nested-table"><tbody><tr><td>*fr*=0:</td><td>Focus rectangle will not be drawn.</td></tr><tr><td>*fr*=1:</td><td>Focus rectangle will be drawn (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">font = "*fontName*"</span> | Sets the font for the list box items. |
| <span class="table-cell-nowrap">frame = *f*</span> | Specifies the list box frame style. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*f*&nbsp;=1:</td><td>simple rectangle.</td></tr><tr><td>*f*&nbsp;=2:</td><td>3D well.</td></tr><tr><td>*f*&nbsp;=3:</td><td>3D raised.</td></tr><tr><td>*f*=&nbsp;4:</td><td>text well style.</td></tr></tbody></table>
| <span class="table-cell-nowrap">fsize = *s*</span> | Sets list box font size. |
| <span class="table-cell-nowrap">fstyle = *fs*</span> | *fs* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">guides = {*left, hcenter, right, top, vcenter, bottom*}</span> |  |
|  | Controls attachments of anchor points to layout guides. See [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode) for detailed information and examples. |
|  | Each of *left, hcenter, right, top, vcenter, bottom* is replaced with the name of a layout guide of appropriate orientation. That is, *left, hcenter, right* indicate attachments to vertical guides, and *top, vcenter, bottom* indicate attachments to horizontal guides. Use the special name *kwNone* to represent an unattached anchor point. |
|  | An error results if you overconstrain a control's layout. Of the three horizontal or vertical anchor points, at most two may be attached to layout guides. Attaching one of the three causes a control to move as the layout guide moves. Attaching two causes a control to both move and resize.  Thus, the name *kwNone* will appear at least twice. |
|  | Using *kwNone* for all anchor points results in completely detaching a control from the layout guides. |
| <span class="table-cell-nowrap">help = {*helpStr* }</span> | Sets the help for the control. |
|  | *helpStr* is limited to 1970 bytes (255 in Igor Pro 8 and before). |
|  | You can insert a line break by putting "\r" in a quoted string. |
| <span class="table-cell-nowrap">hScroll = *h*</span> | Scrolls the list to the right by *h* pixels (user scrolling will change this). *h* is the total amount of horizontal scrolling, not an increment from the current scroll position: h will be the value returned in the V_horizScroll variable by [ControlInfo](/igorpro/commands/controlinfo.md). |
| <span class="table-cell-nowrap">helpWave = *w*</span> | Text wave containing text for tooltips for individual listbox cells. See ***ListBox Help*** below. Added in Igor Pro 8.00 |
| <span class="table-cell-nowrap">keySelectCol = *col*</span> | Sets scan column number *col* when doing keyboard selection. Default is to scan column zero. |
| <span class="table-cell-nowrap">labelBack = (*r*,*g*,*b[,a]* ) or 0</span> |  |
|  | Sets the background color for the header area of the ListBox, which is only visible if the *listWave* has column dimension labels, or a *titleWave* defined. |
|  | The labelBack keyword was added in Igor Pro 9.00. |
|  | *r*, *g,* *b,* and *a* specify the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
|  | If you omit labelBack or specify labelBack=0, then the header background color is the background color of the window in which the ListBox is drawn. |
| <span class="table-cell-nowrap">listWave = *w*</span> | 1D or 2D text wave containing the list contents. |
| <span class="table-cell-nowrap">mode = *m*</span> | List selection mode specifying the behavior for selecting list items. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>No selection allowed.</td></tr><tr><td>*m*&nbsp;=1:</td><td>One or zero selection allowed.</td></tr><tr><td>*m*&nbsp;=2:</td><td>One and only one selection allowed.</td></tr><tr><td>*m*&nbsp;=3:</td><td>Multiple, but not disjoint, selections allowed. Shift selects a contiguous blocks of cells.</td></tr><tr><td>*m*&nbsp;=4:</td><td>Multiple and disjoint selections allowed. Shift selects additional cells, but does not select blocks of cells.</td></tr></tbody></table>
|  | Modes 5 - 8 are analogous to modes 1 - 4, but apply to individual *cells*, as opposed to entire *rows*. This is most useful when the *listWave* has multiple columns. When modes 1 - 4 are used with a multi-column *listWave*, the entire row is selected. When modes 3 or 4 are used with multiple columns, then only the first column of the *selWave* is used to indicate selections. Checkboxes and editing mode, however, use all cells even in modes 0 - 4. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=5:</td><td>One or zero *cell* selections allowed.</td></tr><tr><td>*m*&nbsp;=6:</td><td>One and only one *cell* selections allowed.</td></tr><tr><td>*m*&nbsp;=7:</td><td>Multiple, but not disjoint, *cell* selections allowed. Shift selects a contiguous block of cells.</td></tr><tr><td>*m*&nbsp;=8:</td><td>Multiple and disjoint *cell* selections allowed. Shift selects additional cells, but does not select blocks of cells.</td></tr></tbody></table>
|  | Modes 9 and 10 are the same as modes 4 and 8, but they both allow blocks of rows (*m* = 9) or cells (*m* = 10) to be selected while holding Shift, and individual rows (*m* = 9) or cells (*m* = 10) to be toggled while holding Ctrl. To determine if a cell is selected, perform a bitwise AND with 0x09 (e.g. `selWave[index] & 0x09`). |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=9:</td><td>Multiple and disjoint *row* selections allowed. Block selection (Shift) and individual cell toggling (Ctrl) allowed.</td></tr><tr><td>*m*&nbsp;=10:</td><td>Multiple and disjoint *cell* selections allowed. Block selection (Shift) and individual cell toggling (Ctrl) allowed.</td></tr></tbody></table>
| <span class="table-cell-nowrap">pos = {*leftOrRight*,*top*}</span> | Sets the position in [control panel units](/igorpro/user-interface/controls.md#control-panel-units) of the top/left corner of the control if its alignment mode is 0 or the top/right corner of the control if its alignment mode is 1. See the align keyword above for details. |
| <span class="table-cell-nowrap">pos+ = {*dx,dy*}</span> | Offsets the position of the list box in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">proc = *p*</span> | Set name of user function proc to be called upon certain events. See discussion below. |
| <span class="table-cell-nowrap">rename = *newName*</span> | Gives the control a new name. |
| <span class="table-cell-nowrap">row = *r*</span> | *r* is desired top row (user scrolling will change this). Use a value of -1 to scroll to the first selected cell (if any). Combine with selRow to select a row and to ensure it is visible (modes 1 and 2). |
| <span class="table-cell-nowrap">selCol = *c*</span> | Defines the selected column when mode is 5 or 6 and no selWave is used. To read this value, use ControlInfo and the V_selCol variable. |
| <span class="table-cell-nowrap">selRow = *s*</span> | Defines the selected row when mode is 1 or 2; when no selWave is used, it is defined by modes 5 or 6. Use -1 for no selection. |
|  | To read this value, use [ControlInfo](/igorpro/commands/controlinfo.md) and the V_Value variable. |
| <span class="table-cell-nowrap">selWave = *sw*</span> | *sw* is a numeric wave with the same dimensions as listWave. It is optional for modes 0-2, 5 and 6 and required in all other modes. |
|  | In modes greater than 2, *sw* indicates which cells are selected. In modes 1 and 2 use [ControlInfo](/igorpro/commands/controlinfo.md) to find out which row is selected. |
|  | In all modes *sw* defines which cells are editable or function as checkboxes or disclosure controls. |
|  | Numeric values are treated as integers with individual bits defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0&nbsp;(0x01):</td><td>Cell is selected.</td></tr><tr><td>Bit&nbsp;1&nbsp;(0x02):</td><td>Cell is editable.</td></tr><tr><td>Bit&nbsp;2&nbsp;(0x04):</td><td>Cell editing requires a double click.</td></tr><tr><td>Bit&nbsp;3&nbsp;(0x08):</td><td>Current shift selection.</td></tr><tr><td>Bit&nbsp;4&nbsp;(0x10):</td><td>Current state of a checkbox cell.</td></tr><tr><td>Bit&nbsp;5&nbsp;(0x20):</td><td>Cell is a checkbox.</td></tr><tr><td>Bit&nbsp;6&nbsp;(0x40):</td><td>Cell is a disclosure cell. Drawn as a treeview expansion node.</td></tr><tr><td>Bit&nbsp;7&nbsp;(0x80):</td><td>Cell is disabled. Clicks on the cell are ignored and it is drawn with a grayed appearance. Added in Igor Pro 8.00.</td></tr><tr><td></td><td>Because of technical issues, this bit currently does not prevent the selection of the cell using the arrow keys.</td></tr></tbody></table>
|  | In modes 3 and 4 bit 0 is set only in column zero of a multicolumn listbox. |
|  | Other bits are reserved. Additional dimensions are used for color info. See the discussion for colorWave. selWave is not required for modes 5 and 6. |
| <span class="table-cell-nowrap">setEditCell = {*row*, *col* , *selStart*, *selEnd*}</span> |  |
|  | Initiates edit mode for the cell at *row*, *col*. An error is reported if *row* or *col* is less than zero. Nothing happens and no error is reported if *row*, *col* is beyond the limits of the listbox, or if the cell has not been made editable by setting bit 1 of *selWave*. |
|  | *selStart* and *selEnd* set the range of bytes that are selected when editing is initiated; 0 is the start of the text. If there are N bytes in the listbox cell, setting *selStart* or *selEnd* to N or greater moves the start or end of the selection to the point after the last character. Setting *selStart* and *selEnd* to the same value selects no characters and the insertion point is set to *selStart*. Setting *selStart* to -1 always causes all characters to be selected. |
| <span class="table-cell-nowrap">size = {*width*,*height* }</span> | Sets list box size in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
| <span class="table-cell-nowrap">special = {*kind*,*height*,*style* }</span> |  |
|  | Specifies special cell formatting or contents. |
|  |<table class="nested-table"><tbody><tr><td>*kind*&nbsp;=0:</td><td>Normal text but with specified height (if nonzero). Use a style of 1 to autocalculate widths based on the entire list contents. In this case, user widths are taken to be minimums and the last is not repeated.</td></tr><tr><td>*kind*&nbsp;=1:</td><td>Text taken to be the names of graphs or tables. Images of the graphs or tables are displayed in the cells. Use a style of 0 to display just the presentation portion of the graph or 1 to display it entirely. For tables, only the presentation portion is displayed.</td></tr><tr><td>*kind*&nbsp;=2:</td><td>Text taken to be the names of pictures. Images are displayed in the cells.</td></tr><tr><td>*kind*&nbsp;=3:</td><td>Displays a PNG, TIFF, or JPEG image. You can obtain binary picture data using SavePICT.</td></tr><tr><td>*kind*&nbsp;=4:</td><td>Displays raw text without any escape code processing. Added in Igor Pro 8.00 to allow display of LaTeX expressions which make heavy use of backslash.</td></tr></tbody></table>
|  | For *kind* =1 or 2, height may be zero to auto-set cell height to same as width or a specific value. |
| <span class="table-cell-nowrap">titleWave = *w*</span> | Specifies a text wave containing titles for the listbox columns, instead of using the list wave dimension labels. Each row is the title for one column; if you have *N* columns you must have a wave with *N* rows. |
| <span class="table-cell-nowrap">userColumnResize = *u*</span> | Enables resizing the list columns using the mouse. |
|  |<table class="nested-table"><tbody><tr><td>*u*&nbsp;=0:</td><td>Columns are not resizable. The widths={} parameter still works, though (default).</td></tr><tr><td>*u*&nbsp;=1:</td><td>User can resize columns by dragging the column dividers.</td></tr><tr><td></td><td>When resizing a column without Option, Alt, or Shift modifiers (a &quot;normal&quot; resizing), any width added to the column is subtracted from the following column (if any).</td></tr><tr><td></td><td>When resizing while pressing Alt, only columns following the dragged divider will move (the same way table columns are resized).</td></tr><tr><td></td><td>When pressing Shift, all columns are set to the same width as the column being resized. If the total widths of all columns is less than the width of the listbox, then each column expands to fill the available width.</td></tr></tbody></table>
| <span class="table-cell-nowrap">userdata = *UDStr*</span> | Sets the unnamed user data to *UDStr*. |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the named user data to *UDStr*. |
| <span class="table-cell-nowrap">userdata+ = *UDStr*</span> | Appends *UDStr* to the current unnamed user data. |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends *UDStr* to the named user data. |
| <span class="table-cell-nowrap">widths = {*w1*,*w2*,...}</span> | Optional list of minimum column widths in screen pixels. If more columns than widths, the last is repeated. If total of widths is greater than list box width then a horizontal scroll bar is provided. If total is less than available width then each is expanded proportionally. |
| <span class="table-cell-nowrap">widths+ = {*w1*,*w2*,...}</span> | Additional column widths. Because only 2500 bytes fit on a command line, lists with many columns may require multiple widths+= parameters to define all the column widths. However if all the widths are the same, widths+= is not needed; just use: |
|  | `ListBox ctrlName widths={sameWidth}` |
| <span class="table-cell-nowrap">win = *winName*</span> | Specifies which window or subwindow contains the named control. If not given, then the top-most graph or panel window or subwindow is assumed. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
If the list wave has column dimension labels (see [SetDimLabel](/igorpro/commands/setdimlabel.md)), then those will be used as column titles. Note that a 1D wave is subtly different from a 1 column 2D wave. The former does not have any columns and therefore no column dimension labels.

Alternately, use a text wave with the titleWave keyword to specify column titles.

Using escape codes you can change the font, size, style and color of the title. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

For instance, to make a title bold use the \f01 escape sequence:


```igor
SetDimLabel 1, columnNum, $"\\f01My Label", textWave
```

If you can't fit title text within the 255 byte limit (styled text can be especially long), use the *titleWave* keyword with a text wave. The wave must have as many rows as the list wave has columns. When using a title wave, there are no restrictions on the number of bytes or on what characters you can use.

This example uses a title wave to add a red up-arrow graph marker to the end of a centered title:


```igor
Make/O/T/N=(numColumns) columnTitles
columnTitles[colNum]="\\JCThis is the title\\K(65535,0,0)\\k(65535,0,0)\\W523"
ListBox list0 titleWave=columnTitles
```

That's a 51-byte title that results in 19 characters or symbols that you actually see. \JC requests centered text, \K sets the text color (which colors the inside of the graph marker),\k sets the marker stroke color, and \W523 inserts a down-pointing triangular graph marker.

When using modes that allow multiple selections, the Shift key is used to extend or add to the selection.

You can specify individual cells as being editable by setting bit 1 (counting from zero on the right) in selWave. The user can start editing a cell by either clicking in it or, if the cell is selected, by pressing Enter (or Return). When finished, the user can press Enter to accept the changes or can press Escape to reject changes. The user may also press Up or Down Arrow to accept changes and begin editing the next editable cell in a column. Likewise, Tab and Shift-Tab moves to the next or previous column in a row. If bit 2 of selWave is set then a double click will be required rather than a single click. **Note:** in edit mode, Tab and Shift-Tab are used to move left and right because the Left and Right Arrow keys are used to move the text entry cursor left and right.

When the listbox has keyboard focus (either by tabbing to the list box or by clicking on the box), the arrow keys move a cell selection (or row depending on mode). When not in cell edit mode, Tab and Shift-Tab move the keyboard focus to other objects in the window. The Home, End, Page Up, and Page Down keys affect the vertical scroll bar.

When the listbox has focus, the user may type the first few chars of an entry in the list to select that entry. Only the first column is used. If a match is not found then nothing is done. The search is case insensitive.

### *ListBox Help* {#listbox-help}
You can provide a text wave with help strings to show a tooltip for individual cells or rows of a listbox in place of the generic help string provided by the *help* keyword. In general, the string in helpWave[*listbox row*][*listbox column*] is used. If your help wave is a 1D wave, then the listbox column is ignored, and helpWave[*listbox row*] is used in all columns.

Note that a 1D wave (Make/N=*rows*) is not the same as a 2D wave with one column (Make/N=(*rows*,1)). A 2D wave with one column provides help for column 0 only and the generic help string is shown for column 1 and beyond. A 1D wave provides help for all columns.

If the help wave has an empty string for a given row and column then the generic help string is shown for the corresponding listbox cell. If the help wave has too few rows or columns, then the generic help string is shown for the cells outside the range of the help wave.

### *Listbox Action Procedure* {#listbox-action-procedure}
The action procedure for a ListBox control takes a predefined structure WMListboxAction as a parameter to the function:


```igor
Function ActionProcName(LB_Struct) : ListboxControl
	STRUCT WMListboxAction &LB_Struct
	...
	return 0
End
```

The ": ListboxControl" designation tells Igor to include this procedure in the Procedure pop-up menu in the List Box Control dialog.

See [WMListboxAction](/igorpro/programming/structures/wmlistboxaction.md) for details on the WMListboxAction structure.

Although the return value is not currently used, action procedures should always return zero.

You may see an old format listbox action procedure in old code:


```igor
Function MyListboxProc(ctrlName,row,col,event) : ListboxControl
	String ctrlName     // name of this control
	Variable row        // row if click in interior, -1 if click in title
	Variable col        // column number
	Variable event      // event code
	...
	return 0            // other return values reserved
End
```

This old format should not be used in new code.

*Specifying Cell Color*

The background and foreground (text) color of individual cells may be defined by providing colorWave in conjunction with specific planes in selWave. The planes in selWave are taken to be integer indexes into colorWave. The planes are defined by specific dimension labels and not by specific plane numbers. To provide foreground colors, define a plane labeled "foreColors" that contains the desired index values. Likewise define and fill a plane labeled "backColors" for background colors. The value 0 is special and indicates that Igor's default colors should be used. Note that if you have a one column list for which you want to supply colors, the selWave needs to be three dimensional but with just one column. Here is an example:


```igor
Make/T/N=(5,1) tw= "row "+num2str(p)	// 5 row, 1 col text wave (2D)
Make/B/U/N=(5,1,2) sw           // 5 row, 1 col, 2 plane byte wave
Make/O/W/U myColors= {{0,0,0},{65535,0,0},{0,65535,0},{0,0,65535},{0,65535,65535}}
MatrixTranspose myColors        // above was easier to enter as 3 rows, 5 cols

NewPanel
ListBox lb,mode=3,listWave= tw,selWave= sw,size={200,100},colorWave=myColors
sw[][][1]= p                    // arbitrary index values into plane 1

// now, execute the following one at a time and observe the results

SetDimLabel 2,1,backColors,sw   // define plane 1 as background colors

SetDimLabel 2,1,foreColors,sw   // redefine plane 1 as foreground colors

sw[][][%foreColors]= 4-p        // change the color index values
```

In the above example, the selWave was defined as unsigned byte. If you need more than 254 colors, you will have to use a larger number size.

The color wave may have four columns instead of three, with the fourth specifying transparency (65535=fully opaque, fully 0=transparent). Transparency of the background color is of limited utility as it just shows the white background color through the cell color, resulting in pastel shades. Transparency of the foreground color permits the cell background color to show through the text color.

*Checkboxes in Cells*

You can cause a cell to contain a checkbox by setting bit 5 in selWave. The title (if any) is taken from listWave and the results (selected/deselected) is bit 4 of selWave. If a checkbox cell is selected then the space bar will toggle the checkbox. (Clicking on a checkbox cell does not select it -- use the arrow keys.)

*Errors*

Your listbox may be drawn with a red X and an error code. The codes are:


| Error | Meaning |
| --- | --- |
| E1 | The listbox is too small |
| E2 | The listWave is invalid (missing, not text or no rows) |
| E3 | The listWave and selWave do not match in dimensions |
| E4 | Mode is greater than 2 but no selWave was specified |
| E5 | The number of rows in titleWave does not match the number of columns in listWave |
| E6 | The titleWave is not a text wave |

*Event Queue*

It is possible for a single user action to produce more than one event. For instance, pressing the up arrow key while editing to select a cell that is not visible generates event codes 4, 8, and 6. Igor calls your action procedure separately for each code.

*Scroll Event Warnings*

Events 8, 9, and 10 report to you that the listbox has been scrolled vertically or horizontally. These events are envisioned as allowing you to keep two listboxes synchronized (you may find other uses for these events). You might use an action procedure like this one to keep two listboxes (named list0 and list1) in sync:


```igor
Function ListBoxProc2(LB_Struct) : ListBoxControl
	STRUCT WMListboxAction &LB_Struct
	
	if (LB_Struct.eventCode == 8)
		String listname
		if (CmpStr(LB_Struct.ctrlName, "list1") == 0)
			listname = "list0"
		else
			listname = "list1"
		endif
		ControlInfo $listname
		if (V_startRow != LB_Struct.row)
			listbox $listname,row=LB_Struct.row
			ControlUpdate $listname
		endif
	endif
	
	return 0
End
```

It is very easy to create an infinite cascade of events feeding back between the two listboxes, especially if you use event 10. When this happens, you will see your listboxes jigging up and down endlessly. The test using ControlInfo is intended to make this unlikely.

The slow response of the old-style, nonstructure action procedure can defeat the ControlInfo test by delaying the action procedure execution. If you use events 8, 9, or 10, it is recommended that you use the new-style action procedure.

*Note on Keystroke Event*

In a keystroke event passed to a listbox action procedure the eventCode is 12. A character code is stored in the row field of the WMListboxAction structure. This works only for ASCII characters and for a few special characters such as delete (8), forward delete (127) and escape (27). It does not work for non-ASCII characters such as accented characters which are represented as UTF-8 and require multiple bytes.

As explained below, many keystroke events are not sent to the listbox action procedure because they are consumed by the internal listbox code in Igor. For this reason the keystroke event for a listbox is of limited use.

The architecture of Igor controls is such that events are passed to an action procedure only after the control has used them. In the case of a keystroke event, that means that other uses of the keystroke may consume the event before the action procedure gets a chance at it. In particular, a listbox editable cell that is actively being edited consumes keystroke events, and the action procedure is not called. The only editing-related events your action procedure will get are event codes 6 and 7.

If an arrow key is pressed, and this results in the selected row or cell changing, your action procedure will not get a keystroke event. Instead, your action procedure will receive event code 4 or 5. If the arrow key causes scrolling to occur, the action procedure will also get event code 8 or 9.

### *Examples* {#examples}
Here is a simple Listbox example:


```igor
Make/O/T/N=30 tjack="this is row "+num2str(p)
Make/O/B/N=30 sjack=0
NewPanel /W=(19,61,319,261)
ListBox lb1,pos={42,9},size={137,94},listWave=tjack,selWave=sjack,mode= 3
Edit/W=(367,61,724,306) tjack,sjack
ModifyTable width(tjack)=148
```

Make selections in the list and note changes in the table and vice versa. Edit one of the list text values in the table and note update of the list.

Here is an example using a titleWave and styled text in the title cells. Note that the last title isn’t very long when rendered, but requires a 63 byte specification.


```igor
Make/O/T/N=(4,3) ListWave="row "+num2str(p)+" col "+num2str(q)
Make/O/T/N=3 titles	// three rows to match 3-column ListWave
titles[0] = "\f01Bold Title"
titles[1] = "title with semicolon;"
titles[2] = "Marker in Gray: \K(40000,40000,40000)\k(40000,40000,40000)\W517"
NewPanel /W=(515,542,1011,794)
ListBox list0,pos={1,2},size={391,120},listWave=ListWave
ListBox list0,titleWave=titles
```

It is often useful to be able to display a contextual menu in response to a click in a listbox cell. Here is a simple example:


```igor
Function ListBoxContextProc(lba) : ListBoxControl
	STRUCT WMListboxAction &lba

	Variable row = lba.row
	Variable col = lba.col
	WAVE/Z selWave = lba.selWave

	switch( lba.eventCode )
			// Always display the contextual menu on the mouse-down event
			// On Windows, the mouse-down is delivered only after the mouse is released
		case 1: // mouse down
			if (row >= 0 && row < DimSize(selWave, 0))		// click must be in a cell
				if (col == 0)				// click must be in the left column
					if (lba.eventMod & 16)			// it's a contextual click
						String menucontents = "Nothing;Checkbox;Disclosure;Disabled;Enabled;"
						PopupContextualMenu menucontents
						if (V_flag > 0)			// if nothing was selected, V_flag = 0
							StrSwitch(S_selection)			// S_selection is the text of the menu item
								case "Nothing":
									SelWave[row][1] = 0
									break
								case "Checkbox":
									SelWave[row][1] = 0x20
									break
								case "Disclosure":
									SelWave[row][1] = 0x40
									break
								case "Disabled":
									SelWave[row][1] = SelWave[row][1] | 0x80
									break
								case "Enabled":
									SelWave[row][1] = SelWave[row][1] & ~0x80
									break
							endswitch
						endif
					endif
				endif
			endif
			break
		case 13: 					// checkbox clicked
			String msg
			// test the value of SelWave for the clicked cell to see what it is, and its state
			Variable isOn = (SelWave[row][1] & 0x10) ? 1 : 0
			if (SelWave[row][1] & 0x20)
				msg = "Checbox was turned "
				if (isOn)
					msg += "on"
				else
					msg += "off"
				endif
			else
				msg = "Disclosure was "
				if (isOn)
					msg += "opened"
				else
					msg += "closed"
				endif
			endif
			DoAlert 0, msg
			break
	endswitch
	return 0
End

Function ListBoxContextMenu()
	Make/N=(5,2)/T/O ListWaveContext
	ListWaveContext[][0] = "Column 1 should be:"
	ListWaveContext[][1] = "Row "+num2str(p)
	Make/N=(5,2)/O SelWaveContext
	SelWaveContext=0
	NewPanel /W=(150,53,450,253)
	ListBox list_w_context,pos={50,30},size={200,150},proc=ListBoxContextProc,widths={3,1}
	ListBox list_w_context,listWave=root:ListWaveContext,selWave=root:SelWaveContext
EndMacro
```

Copy the code above to the Procedure window and compile. On the command line, invoke the function to build the panel:


```igor
ListBoxContextMenu()
```

In the listbox, right-clicking in the left column of the listbox will present a contextual menu with choices for what to do with the right column. If you choose Checkbox or Disclosure, and the cell is enabled, when you click on the cell in the right column, an alert is displayed telling you about what happened.

An example experiment that lets you easily experiment with ListBox settings is available in "Examples:Feature Demos 2: ListBox Demo.pxp".

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.

See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

### *Demos* {#demos}
[Open ListBox Demo](#igor-pxp/Examples/Feature__Demos__2/ListBox__Demo.pxp)

[Open Wave Selector List Demo](#igor-pxp/Examples/Programming/WaveSelectorWidgetExample.pxp)