---
description: "Tables are useful for entering, modifying, and inspecting waves. You can also use a table for presentation purposes by exporting it to another program as a…"
slug: /igor-basics/tables
---

# Tables {#tables}

Tables are useful for entering, modifying, and inspecting waves. You can also use a table for presentation purposes by exporting it to another program as a picture or by including it in a page layout. However, it is not optimized for this purpose.

If your data has a small number of points you will probably find it most convenient to manually enter it in a table. In this case, creating a new empty table will be your first step.

If your data has a large number of points you will most likely load it into Igor from a file. In this case it is not necessary to make a table. However, you may want to display the waves in a table to inspect them. Igor Pro tables can handle virtually any number of rows and columns provided you have sufficient memory.

A table in Igor is similar to but not identical to a spreadsheet in other graphing programs. The main difference is that in Igor data exists independent of the table. You can create new waves in Igor's memory by entering data in a table. Once you have entered your data, you may, if you wish, kill the table. The waves exist independently in memory so killing the table does not kill the waves. You can still display them in a graph or in a new table.

In a spreadsheet, you can create a formula that makes one cell dependent on another. You cannot create cell-based dependencies in Igor. You can create dependencies that control entire waves using Analysis→Compose Expression, Misc→Object Status, or the [SetFormula](/igorpro/commands/setformula.md) operation, but this is not recommended for routine work.

To make a table, choose Windows→New Table.

When the active window is a table, the Table menu appears in Igor's menu bar. Items in this menu allow you to append and remove columns, change the formatting of columns, and sets table preferences.

Waves in tables are updated dynamically. Whenever the values in a wave change, Igor automatically updates any tables containing that wave. Because of this, tables are often useful for troubleshooting number-crunching procedures.



## Creating Tables {#creating-tables}

### Table Creation with New Experiment {#table-creation-with-new-experiment}

By default, when you create a new experiment, Igor automatically creates a new, empty table. This is convenient if you generally start working by entering data manually. However, in Igor data can exist in memory without being displayed in a table. If you wish, you can turn automatic table creation off using the Experiment Settings category of the Miscellaneous Settings dialog (Misc menu).

### Creating an Empty Table for Entering New Waves {#creating-an-empty-table-for-entering-new-waves}

Choose Windows→New Table and click the `Do It` button.

If you enter a numeric value, Igor creates a numeric wave. If you enter a non-numeric value, Igor creates a text wave.

To create multidimensional waves you must use the Make Waves dialog (Data menu).

After creating the wave, you may want to rename it. Choose Rename from the Table pop-up menu or from the Data menu in the main menu bar.

### Creating a Table to Edit Existing Waves {#creating-a-table-to-edit-existing-waves}

Choose New Table from the Windows menu. This displays the New Table dialog.

Select the waves to appear in the table from the Columns to Edit list. Press Shift while clicking to select a range of waves. Press Ctrl while clicking to select an individual list item.

Click the `Do It` button to create the table.

### Showing Index Values {#showing-index-values}

As described in [Waves](/igorpro/igor-basics/waves.md), waves have built-in scaled index values. The New Table and Append to Table dialogs allow you to display just the data in the wave or the index values and the data. If you click the Edit Index And Data Columns radio button in either of these dialogs, Igor displays both index and data columns in the table.

A 1D wave's X index values are determined by its X scaling which is a property that you set using the Change Wave Scaling dialog or SetScale operation. A 2D wave has X and Y scaling, controlling X and Y scaled index values. Higher dimension waves have additional scaling properties and scaled index values. Displaying index values in a table is of use mostly if you are not sure what a wave's scaling is or if you want to see the effect of a SetScale operation.

### Showing Dimension Labels {#showing-dimension-labels}

As described in [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels), waves have dimension labels. The New Table and Append Columns to Table dialogs allow you to display just the data in the wave or the dimension labels and the data. If you click the Edit Dimension Label And Data Columns radio button in either of these dialogs, Igor displays both label and data columns in the table.

Dimension labels are of use only when individual rows or columns of data have distinct meanings. In an image, for example, this is not the case because the significance of one row or column is the same as any other row or column. It is the case when a multidimensional wave is really a collection of related but disparate data.

A 2D wave has row dimension labels and column dimension labels. A 1D wave has row dimension labels only.

You can display dimension labels or dimension indices in a table, but you cannot display both at the same time for the same wave.

### The Horizontal Index Row {#the-horizontal-index-row}

When a multidimensional wave is displayed in a table, Igor adds the horizontal index row which appears below the column names and above the data cells. This row can display numeric dimension indices or textual dimension labels.

By default, the horizontal index row displays dimension labels if the wave's dimension label column is displayed in the table. Otherwise it displays numeric dimension indices. You can override this default using the Table→Horizontal Index submenu.

### Creating a Table While Loading Waves From a File {#creating-a-table-while-loading-waves-from-a-file}

The Load Waves dialog (Data menu) has an option to create a table to show the newly loaded waves.



## Parts of a Table {#parts-of-a-table}

This diagram shows the parts of a table displaying 1D waves. If you display multidimensional waves, Igor adds some additional items to the table, described under [Editing Multidimensional Waves](#editing-multidimensional-waves).

<img src="MD_images/Tables/image_1.png" width="100%"/>

The bulk of a table is the **cell area**. The cell area contains columns of numeric or text data values as well as the column of point numbers on the left. If you wish, it can also display index columns or dimension label columns. To the right are unused columns into which you can type or paste new data.

If the table displays multidimensional waves then it will include a row of column indices or dimension labels below the row of names. Use the Append Columns to Table dialog to switch between the indices and labels.

In the top left corner is the **target cell** ID area. This identifies wave element corresponding to the target cell. For example, if a table displays a 2D wave, the ID area might show "R13 C22", meaning that the target cell is on row 13, column 22 of the 2D wave. For 3D waves the target cell ID includes the layer ("L") and for a 4D wave it includes the chunk ("Ch").

If you scroll the target cell out of view you can quickly bring it back into view by clicking in the target cell ID.

There is a special cell, called the **insertion cell**, at the bottom of each column of data values. You can add points to a wave by entering a value or pasting in the insertion cell.

<img src="MD_images/Tables/image_2.png" width="100%"/>

The **Table pop-up menu** provides a quick way to inspect or change a wave, remove or kill a wave, and change the formatting of one or more columns. You can invoke the Table pop-up menu by clicking the gear icon or right-clicking.

For waves displayed in multiple columns (complex waves and multidimensional waves), if you change the display format of any data column from the wave, Igor changes the format for all data columns from that wave.

One of the items in the pop-up menu is Delay Update. Normally, when you change the value of a cell in the table, Igor immediately updates any other tables or graphs to reflect the new value. Enabling Delay Update forces this updating of other tables and graphs to be postponed until you click in another window or disable Delay Update. When Delay Update has been enabled, there is a checkmark next to the menu item. You can do this if you have a list of values to enter into a table and you don't want other tables or graphs to be updated until you are finished.

Delay Update does not delay updates when you remove or add cells to a wave. It only delays updates when you change the value of a cell.



## Showing and Hiding Parts of a Table {#showing-and-hiding-parts-of-a-table}

The Table menu has a Show submenu that shows or hides various parts of a table. This is of use only in specialized situations such as when you are using a table subwindow in a control panel to display data but don't want the user to enter data. For normal use you should leave all of the items in the Show submenu checked so that all parts of the table will be visible.

When the entry line is hidden, the user cannot change values in the table.



## Arrow Keys In Tables {#arrow-keys-in-tables}

By default, if you are in the process of entering data, the arrow keys accept the entry as if you pressed Enter and then move the selected cell.

Some users prefer to use the arrow keys to move the selection in the entry line when an entry is in progress. You can tell Igor that this is your preference via the Table Settings category in the Miscellaneous Settings dialog (Misc menu).



## Table Keyboard Navigation {#table-keyboard-navigation}

The term "keyboard navigation" refers to selection and scrolling actions in response to the arrow keys and to the Home, End, Page Up, and Page Down keys.


|  | No Modifier | Alt | Ctrl |
| --- | --- | --- | --- |
| Left | Move selection left one cell | Not used | Move selection to first column |
| Right | Move selection right one cell | Not used | Move selection to last column |
| Up | Move selection up one cell | Shows previous layer | Scroll and move selection to first row |
| Down | Move selection down one cell | Shows next layer | Scroll and move selection to last row |
| Home | Move selection to first visible cell | Not used | Scroll and move selection to first cell |
| End | Move selection to last visible cell | Not used | Scroll and move selection to last cell |
| Page Up | Scroll up one screen | Scroll left one screen | Scroll up one screen |
| Page Down | Scroll down one screen | Scroll right one screen | Scroll down one screen |


When viewing a 3D or 4D wave, `Alt+Up Arrow` and `Alt+Down Arrow` change the currently viewed layer.

When viewing a 4D wave, `Ctrl+Alt+Up Arrow` and `Ctrl+Alt+Down Arrow` change the currently viewed chunk.

Pressing `Shift+Arrow-key` extends the selection in the direction of the arrow key. Pressing `Ctrl+Shift+Arrow-key` extends selection as far as possible in the direction of the arrow key.

## Decimal Symbol and Thousands Separator in Tables {#decimal-symbol-and-thousands-separator-in-tables}

By default, the decimal symbol for entering a number in a table is period. You can change this to comma or Per System Setting using the Table→Table Misc Settings menu. The selected decimal symbol is used for entering, copying, and pasting data in tables.

The Decimal Symbol setting controls the character that is produced when you press the decimal key on the numeric keypad while entering a value in the entry area of a table.

If comma is selected as the decimal symbol then it is not supported as a column separator when creating new waves by pasting text into a table.

When you choose Per System Setting, the decimal symbol is determined by your system settings as of when Igor was launched. Only period and comma are supported as the decimal symbol. If you choose any decimal symbol other than comma, period will be used as the decimal symbol for tables.

When creating a new wave by entering data into an unused table cell, there are some rare situations when what you are trying to enter cannot be properly interpreted unless you first choose the appropriate column numeric format from the Table menu. For example, if the decimal symbol is comma and you want to enter a time or date/time value with fractional seconds, you must choose Time or Date/Time from the Table→Formats menu before entering the data.

If the decimal symbol is period then the thousands separator is comma. If the decimal symbol is comma then the thousands separator is period. The thousands separator is permitted when entering data in a table. You can also choose a column numeric format that displays thousands separators. However thousands separators are not permitted when creating new waves by pasting text into a table.

## Using a Table to Create New Waves {#using-a-table-to-create-new-waves}

If you click in any unused column, Igor selects the first cell in the first unused column. You can then create new waves by entering a value or pasting data that you have copied to the clipboard.

### Creating a New Wave by Entering a Value {#creating-a-new-wave-by-entering-a-value}

When you enter a data value in the first unused cell, Igor creates a single new 1D wave and displays it in the table. This is handy for entering a small list of numbers or text items. If you enter a numeric value, including date/time values, Igor creates a numeric wave. If you enter a non-numeric value, Igor creates a text wave.

Igor gives the wave a default name, such as wave0 or wave1. You can rename the wave using the Rename item in the Data menu or the Rename item in the Table pop-up menu. You can also rename the wave from the command line by simply executing:


```igor
Rename oldName, newName
```

When you create a new wave, the wave has one data point — point 0. The cell in point number 1 appears gray. This is the **insertion cell**. It indicates that the preceding cell is the last point of the wave. You can click in the insertion cell and enter a value or do a paste. This adds one or more points to the wave.

If the new wave is numeric, it will be single or double precision, depending on the Default Data Precision setting in the Miscellaneous Settings dialog. The number of digits displayed, however, depends on the numeric format. See [Numeric Formats](#numeric-formats).

When entering a date, you must use the format selected in the Table Date Format dialog, accessible via the Table menu. The setting in this dialog affects all tables.

If you enter a date (e.g., 1993-01-26), time (e.g., 10:23:30) or date/time (e.g., 1993-01-26 10:23:30) value, Igor notices this. It sets the column's numeric format to display the value properly. It also forces the new wave to be double precision, regardless the Default Data Precision setting in the Miscellaneous Settings dialog. This is necessary because single precision does not have enough range to store date and time values.

### Creating New Waves by Pasting Data from Another Program {#creating-new-waves-by-pasting-data-from-another-program}

If you have data in a spreadsheet program or other graphing program, you may be able to import that data into Igor using copy and paste.

This will work if the other program can copy its data to the clipboard as tab-delimited text or comma-delimited text. Most programs that handle data in columns can do this. Tab-delimited data consists of a number of lines of text with following format:


```igor
value		<tab>		value		<tab>		value		<terminator>
```

It may start with a line containing column names. The end of a line is marked by a \<terminator\> which may be a carriage return, a linefeed, or a carriage return/linefeed combination. If pasted into a word processor, tab delimited text would look something like this:

```
column1 column2   column3 (this line is optional)
27.95   -13.738   12.74e3
31.37   -12.89    13.97e3 
. . .
. . .	
. . .
```

In the other program, select the cells containing the data of interest and copy them to the clipboard. In Igor, select the first cell in the first unused column in a table and then select Paste from Igor's Edit menu.

Igor scans the contents of the clipboard to determine the number of rows and columns of numeric text data. It also checks the first line of text in the clipboard to see if it contains column names. It creates waves and displays them in the table using the names found in the clipboard or default names. If the text contains names which conflict with existing names, Igor presents a dialog in which you can correct the problem.

If you paste text-only data, which does not contain numbers, dates, times or date/time values, Igor treats all of the pasted text as data instead of treating the first line as column names. This will usually produce the desired results. If you want to treat the first line as column names, use the Load Delimited Text routine to load the text from the clipboard and specify that you want to load wave names. See [Loading Delimited Text Files](/igorpro/data/importing-and-exporting-data.md#loading-delimited-text-files) for details.

### Troubleshooting Table Copy and Paste {#troubleshooting-table-copy-and-paste}

If the waves that are created when you paste don't contain the values you expect, chances are that the clipboard does not contain tab-delimited text. In this case you will need to undo the paste. To examine the contents of the clipboard, paste it into an Igor plain text notebook or into the word processor of your choice. After editing the text, copy it to the clipboard again and repaste it into the table.

### Creating New Waves by Pasting Data from Igor {#creating-new-waves-by-pasting-data-from-igor}

You can also create new waves by copying data from existing waves. When you copy wave data in a table, Igor stores not only the raw data but also the following properties of the wave or waves:


-	Data units and dimension units


-	Data full scale and dimension scaling


-	Dimension labels


-	The wave note

Thus you can duplicate a wave by copying it in a table and pasting into the unused area of the same table or a different table. You can also copy from a table in one experiment and paste in a table in another experiment.

Igor copies and pastes the wave note only if you copy the entire wave. If you copy part of the wave, it does not copy the wave note.



## Table Names and Titles {#table-names-and-titles}

Every table that you create has a name. The name is a short Igor object name that you or Igor can use to reference the table from a command or procedure. When you create a new table, Igor assigns it a name of the form Table0, Table1 and so on. You will most often use a table's name when you kill and recreate the table, as described in the next section.

A table also has a title. The title is the text that appears at the top of the table window. Its purpose is to identify the table visually. It is not used to identify the table from a command or procedure. The title can consist of any text, up to 255 bytes.

You can change the name and title of a table using the Window Control dialog. Choose Windows→Control→Window Control to display the dialog.



## Hiding and Showing a Table {#hiding-and-showing-a-table}

You can hide a table by Shift-clicking the close button.

You can show a table by choosing the table's name from the Windows→Tables submenu.



## Killing and Recreating a Table {#killing-and-recreating-a-table}

Igor provides a way for you to kill a table and then later to recreate it. Use this to temporarily get rid of a table that you expect to be of use later.

You kill a table by clicking the table window's close button or by using the Close item in the Windows menu. When you kill a table, Igor offers to create a **window recreation macro**. Igor stores the window recreation macro in the procedure window of the current experiment. The name of the window recreation macro is the same as the name of the table. You can invoke the window recreation macro later to recreate the table by choosing its name from Windows→Table Macros.

A table does not contain waves but is just a way of viewing them. Killing a table does not kill the waves displayed in a table. If you want to kill the waves in a table, select all of them (Select All in Edit menu) and then choose Kill All Selected Waves from the Table pop-up menu.

For further details, see [Closing a Window](/igorpro/igor-basics/using-igor.md#closing-a-window) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro).



## Index Columns {#index-columns}

There are two kinds of numeric values associated with a numeric wave: the stored data values and the computed index values. For example, each point in a real 1D wave has two values: a data value and an X index value. The data value is stored in memory. The X value is computed based on the point number and the wave's X scaling property. The correspondence between point numbers and X values is discussed in detail under [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).

Because the index values for a wave are computed, a value in an index column in a table cannot be altered by editing the wave. Only values in data columns of a table can be edited. To alter the index values of a wave, use the Change Wave Scaling dialog.



## Column Names {#column-names}

Column names are related to but not identical to wave names. You need to use column names to append, remove or modify table columns from the command line or from an Igor procedure.

A column name consists of a wave name and a suffix that identifies which part of the wave the column displays. For each real 1D wave there can be two columns: one for the X index values or dimension labels of the wave and one for the data values of the wave. For complex waves there can be three columns: one for the X index values or dimension labels of the wave, one for the real data values of the wave and one for the imaginary data values of the wave.

If we have a real 1D wave named "test" then there are three column names associated with that wave: test.i ("i" for "index"), test.l ("l" for "label") and test.d ("d" for "data"). If we have a complex 1D wave named "ctest" then there are four column names associated with that wave:ctest.i, ctest.l, ctest.d.real and ctest.d.imag.

| Wave Name | Column Name | What Column Shows |
| --- | --- | --- |
| test | test.i | Index values of test |
| test | test.l | Dimension labels of test |
| test | test.d | Data values of test |
| test | test.id | Index and data values of test |
| ctest | ctest.i | Index values of ctest |
| ctest | ctest.id | Index and data values of ctest |
| ctest | ctest.d.real | Real part of data values of ctest |
| ctest | ctest.d.imag | Imaginary part of data values of ctest |


For multidimensional waves, the ".i" and ".l" suffixes still specify a single column of index values or dimension labels while the ".d" suffix specifies all of the data columns.

In the table-related commands, you can abbreviate column names as follows:


| Full Column Specification | Abbreviated Column Specification |
| --- | --- |
| test.d | test |
| test.i, test.d | test.id |
| test.l, test.d | test.ld |
| ctest.d.real, ctest.d.imag | ctest.d or ctest |
| ctest.i, ctest.d.real | ctest.id.real |
| ctest.l, ctest.d.real | ctest.ld.real |
| ctest.i, ctest.d.imag | ctest.id.imag |
| ctest.l, ctest.d.imag | ctest.ld.imag |
| ctest.i,ctest.d.real,ctest.d.imag | ctest.id |
| ctest.l,ctest.d.real,ctest.d.imag | ctest.ld |

A 2D wave has X and Y index values. A 3D wave has X, Y and Z index values. A 4D wave has X, Y, Z and T index values. Regardless of the dimensionality of the wave, however, it has only one index column in a table. The index column for a 2D wave, for example, may show the X values or the Y values, depending on how you are viewing the data. The index column will be labeled "wave.x" or "wave.y", depending on the view. When referring to the column from an Igor command, you can always use the generic column name "wave.i" as well as the specific column name "wave.x" or "wave.y". A dimension label column is always called "wave.l", regardless of which dimension is showing in the table.

See [Edit](/igorpro/commands/edit.md) for some examples of commands using column names.



## Appending Columns {#appending-columns}

To append columns to a table, choose Table→Append Columns to Table. This displays the Append Columns dialog.

Igor appends columns to the right end of the table. You can drag a column to a new position by pressing Alt and dragging the column name.



## Removing Columns {#removing-columns}

To remove columns from a table, choose Table→Remove Columns from. This displays the Remove Columns dialog.

You can also select the columns in the table, and use the Table pop-up menu to remove the selected columns.

Removing a column from a table does not kill the underlying wave. The column is not the wave but just a view of the wave. Use the Kill Waves item in the Table pop-up menu to remove waves from the table and kill them. Use the Kill Waves item in the Data menu to kill waves you have already removed from a table.



## Selecting Cells {#selecting-cells}

If you click in a cell, it becomes the target cell. The old target cell is deselected and the cell you clicked on is highlighted. The target cell ID changes to reflect the row and column of the new target cell and the value of the target cell is shown in the entry line. You click in a cell and make it the target when you want to enter a new value for that cell or because you want to select a range of cells starting with that cell.

Here are the selections that you can make:


| Click | Action |
| --- | --- |
| Click | Selects a single cell and makes it the target cell |
| Shift-click | Extends or reduces the selection range |
| Click in the point column | Selects the entire row |
| Click in a column name | Selects the entire column |
| Click in an unused column | Selects the first unused cell |
| Choose Select All (Edit menu) | Selects all cells (if possible) |



The selection in a table must be rectangular. Igor will not let you select a range that is not rectangular. If you choose Select All, Igor will attempt to select all of the cells in the table. However, if you have columns of different length, Igor will be limited to selecting a rectangular array of cells.

If, after clicking in a cell to make it the target cell, you drag the mouse, the cells over which you drag are selected and highlighted to indicate that they are selected. You select a range of cells in preparation for copying, cutting, pasting or clearing those cells. While you drag, the cell ID area shows the number of rows and columns that you have currently selected. If you drag beyond the edges of the table, the cell area scrolls so that you can select as many cells as you want.

Moving the target cell accepts any data entry in progress.

You can change which cell is the target cell using Return, Enter, Tab, or arrow keys. If you are entering a value, these keys also accept the entry.


| Key | Action (When a Single Cell is Selected) |
| --- | --- |
| Return, Enter, Down Arrow | Moves target cell down |
| Shift-Return, Shift-Enter, Up Arrow | Moves target cell up |
| Tab, Right Arrow | Moves target cell right |
| Shift-Tab, Left Arrow | Move target cell left |


If you have a range of cells selected, these keys keep the target cell within that selected range. If it is at one extreme of the selected range it will wrap around to the other extreme.

By default, the arrow keys move the target cell. You can change it so they move the insertion point in the entry line using Table→Table Misc Settings.

The used columns in a table are always contiguous. If you click in any unused column, Igor selects the first unused cell. There are just two things you can do when the first unused cell is selected: create a new wave by entering a value or create new waves by pasting data from the clipboard. Igor will not allow you to select any unused cell other than the first cell in the first unused column.



## The Insertion Cell {#the-insertion-cell}

At the bottom of every column of data values is a special cell called the insertion cell. It appears as a gray box below the very last point in a wave.

Sometimes you know the number of points that you want a wave to contain and don't need to insert additional points into the wave. However, if you want to enter a short list of values into a table or to add new data to an existing wave, you can do this by entering data in the insertion cell.

When you enter a value in an insertion cell, Igor extends the wave by one point. Then the insertion cell moves down one position and you can insert another point.

The insertion cell can also be used to a extend a wave or waves by more than one point at a time. This is described under [Pasting Values](#pasting-values).

You can also insert points in waves using the Insert Points item which appears in both the Table pop-up menu and the Data menu or using the InsertPoints operation from the command line.



## Entering Values {#entering-values}

You can alter the data value of a point in a wave by making the cell corresponding to that value the target cell, typing the new value in the entry line, and then confirming the entry.

You can also accept the entry by clicking in any cell or by pressing any of the keys that move the target cell: Return, Enter, Tab, or arrow keys. You can discard the entry by pressing Escape or by clicking the X icon.

If a range of cells is selected when you confirm an entry, the target cell will move within the range of selected cells unless you click in a cell outside this range.

While you are in the process of entering a value, the clear, copy, cut and paste items in the Edit menu as well as their corresponding command key equivalents affect the entry line. If you are not in the process of entering, these operations affect the cells.

Entering a value in an insertion cell is identical to entering a value in any other cell except that when the entry is confirmed the wave is extended by one point.

Igor will not let you enter a value in an index column since index values are computed by Igor based on a waves dimension scaling.

Dimension labels are limited to 255 bytes. If you paste into a dimension label cell, Igor clips the pasted data to 255 bytes.

Prior to Igor Pro 8.00, dimension labels were limited to 31 bytes. If you use long dimension labels, your wave files and experiments will require Igor Pro 8.00 or later.

When entering a value in a numeric column, if what you have entered in the entry line is not a valid numeric entry, Igor will not let you confirm it. The check icon will be dimmed to indicate that the value cannot be entered. To enter a value in a date column, you must use the date format specified in the Table Date Format dialog.

If you edit a text wave or dimension label which contains bytes that are not valid in the wave's text encoding, Igor displays a warning and substitutes escape codes for the invalid bytes. See [Editing Invalid Text](#editing-invalid-text) for details.

If you attempt to enter a character that cannot be represented in the text encoding controlling a text wave or dimension label, Igor displays an error message. See [Entering Special Characters](#entering-special-characters) for details.



## Table Display Precision {#table-display-precision}

The display of data in a column of a table depends on the data type of the displayed wave, the values stored in the wave, and the numeric format settings applied to the column. In some cases, the cell area displays less than full precision but the entry line always displays full precision.

For example, this table displays five double-precision floating point waves using different display formats. Each of the waves contains the values 10, 3.141592653589793, and 3 billion.

<img src="MD_images/Tables/image_3.png" width="100%"/>

The first column is set to general format with six digits of precision which is the factory default format for new table columns. The general format chooses either integer, floating point or scientific notation depending on the displayed value.

The value of General[1] is displayed in the body of the table as 3.14159 since the format specifies six digits of precision. Since this cell is selected as the target cell, its value appears in the entry line. However, the entry line displays the value using full 16-digit precision rather than using the column's format. This guarantees that, if you click in the entry line and accept the text that is already there, no precision is lost.

If the General wave were single-precision floating point instead of double-precision, the entry line would show 8 digits for non-integer values since 8 digits are sufficient for single-precision. Integer values from single-precision waves are displayed using up to 16 digits.

Because the Integer column is formatted to display as integer, 3.141592653589793 is displayed as 3. If you clicked on Integer[1], the entry line would show the full precision.

The story is the same for Decimal[1]. The cell area of the table follows the column's formatting but if you clicked Decimal[1], the full precision would appear in the entry line.

The Hex and Octal columns are set to hexadecimal and octal display respectively. The hex and octal formats do not support the display of fractional data so Hex[1] and Decimal[1] display error messages instead of values. This is further discussed under [Hexadecimal Numeric Format](#hexadecimal-numeric-format) and [Octal Numeric Format](#octal-numeric-format).



## Date Values {#date-values}

Dates and times are represented in Igor date format — as a number of seconds since midnight, January 1, 1904. Dates before that are represented by negative values.

A date cannot be accurately stored in the data values of a single precision wave. Make sure to use double precision to store dates and times.

For further discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).

The way you enter dates and the way that Igor displays them in tables is controlled by the Table Date Format dialog which you invoke through the Table menu. This dialog sets a global preference that determines the date format for all tables.

If in the Table Date Format dialog you choose to use the system date format, which is the factory default setting, Igor displays dates in a table using the short date format as set by the Region control panel.

Alternatively, you can choose to use a common date format or a custom date format. Here is what the dialog looks like if the Use Common Format radio button is selected:

<img src="MD_images/Tables/image_4.png" width="50%"/>

You can access even more flexibility in those rare cases where it's needed by clicking the Use Custom Format radio button:

<img src="MD_images/Tables/image_5.png" width="50%"/>

When using a common or custom date format that includes separators (e.g., 10/05/99 or 10.05.99), Igor is lenient about the number of digits in the year and whether or not leading zeros are used. Igor will accept two or four digit years and leading zeros or no leading zeros for the year, month, and day of month. However, when using a format with no separators (e.g., 991005 or 19991005), Igor requires that you enter the date exactly as the format specifies.

When you enter a value in the first unused column in a table, Igor must deduce what kind of value you are entering (number, date, time, date/time, or text). It then sets the column format appropriately and interprets what you have entered accordingly. An ambiguity occurs if you use date formats with no separators. For example, if you enter 991005, are you trying to enter a date or a number? Igor has no way to know. Therefore, if you want to create a new column consisting of dates with no separators, you must choose Date from the Table Format submenu before you enter the value. This is not necessary for dates that include separators because Igor can distinguish them from numbers.

If you choose a date format that includes alphabetic characters, such as "October 11, 1999", you must enter dates exactly as the format indicates, including spaces.

For further discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).



## Special Values {#special-values}

There are two special values that can be entered in any numeric data column. They are NaN and INF.

### Missing Values (NaNs) {#missing-values-nans}

NaN stand for "Not a Number" and is the value Igor uses for missing or blank data. Igor displays NaNs in a table as a blank cell. NaN is a legal number in a text data file, in text pasted from the clipboard, and in a numeric expression in Igor's command line or in a procedure.

A point will have the value NaN when a computation has produced a meaningless result, for example if you take the log of a negative number. You can enter a missing value in a cell of a table by entering NaN or by deleting all of the text in the entry line and confirming the entry.

You can also get NaNs in a wave if you load a delimited text data file or paste delimited text which contains two delimiters with no number in between.

### Infinities (INFs) {#infinities-infs}

INF stands for "infinity". Igor displays infinities in a table as "INF". INF is a legal number in a text data file, in text pasted from the clipboard and in a numeric expression in Igor's command line or in a procedure.

A point will have the value INF or -INF when a computation has produced an infinity, for example if you divide by zero. You can enter an infinity in a cell of a table by entering INF or -INF.



## Clearing Values {#clearing-values}

You invoke the clear operation by choosing Edit→Clear. Clear sets all selected cells in numeric columns to zero. It sets all selected cells in text and dimension label columns to "" (empty string). It has no effect on selected cells in index columns.

To set a block of numeric values to NaN (or any other numeric value), select the block and then choose Compose Expression (Analysis menu). In the resulting dialog, choose "\_table selection\_" from the Wave Destination pop-up menu. Enter "NaN" as the expression and click `Do It`.



## Copying Values {#copying-values}

You invoke the copy operation by choosing Edit→Copy. This copies all selected cells to the clipboard as text and as Igor binary. It is useful for copying ranges of points from one wave to another, from one part of a wave to another part of that wave, and for exporting data to another application or to another Igor experiment (see [Exporting Data from Tables](#exporting-data-from-tables)).

Copying and pasting in Igor tables uses the binary version of the data which represents the data with full precision and also includes wave properties such as scaling and units. If you paste anywhere other than an Igor table, for example to an Igor notebook or to another program, the text version of the data is used.

For technical reasons relating to 64-bit support, the binary clipboard format is different from the Igor Pro 6 format. Consequently you cannot copy binary table data between these version.

The text version of the copied data uses as many digits as needed to represent the data with full precision. If you want to export text exactly as shown in the table you must use the Save operation with the /F flag, or File→Save Table Copy, or the [SaveTableCopy](/igorpro/commands/savetablecopy.md) operation.

You can also create new waves by copying data from existing waves. This is described earlier in this help file under [Creating New Waves by Pasting Data from Igor](#creating-new-waves-by-pasting-data-from-igor).

See also [Multidimensional Copy/Cut/Paste/Clear](#multidimensional-copy-cut-paste-clear).



## Cutting Values {#cutting-values}

You invoke the cut operation by choosing Edit→Cut. Cut starts by copying all selected cells to the clipboard as text and as Igor binary. Then it deletes the selected points from their respective waves, thereby shortening the waves.

You cannot cut sections of an index column since index values are computed based on point numbers, not stored. However, if you cut a section of a data or dimension label column, the index column corresponding to the data column will also be shortened.



## Pasting Values {#pasting-values}

You invoke the paste operation by choosing Edit→Paste. There are three kinds of paste operations: a replace-paste, an insert-paste and a create-paste.


| Paste Type | What You Do | What Igor Does |
| --- | --- | --- |
| Replace-paste | Choose Paste. | Replaces the selected cells with |
|  |  | data from the clipboard. |
| Insert-paste | Press Shift and choose Paste. | Inserts data from clipboard as new cells. |
| Create-paste | Select the first cell in | Creates new waves with clipboard data. |
|  | the first unused column |  |
|  | and then choose Paste. |  |

When dealing with multidimensional waves, there are other options. See [Multidimensional Copy/Cut/Paste/Clear](#multidimensional-copy-cut-paste-clear) for details.

When you do a paste, Igor starts by figuring out how many rows and columns of values are in the clipboard. The clipboard may contain binary data that you just copied from an Igor table or it may contain plain text data from another application such as a spreadsheet or a text editor.

If the data in the clipboard is plain text, Igor expects that rows of values be separated by carriage return characters, linefeed characters, or carriage return/linefeed pairs and that individual values in a row be separated by tabs or commas. This is normally no problem since most applications export data as tab-delimited text. If you have trouble with a paste and are not sure about the format of the data in the clipboard, you can paste it into an Igor notebook to inspect or edit it.

Once Igor has figured out how many rows and columns are in the clipboard, it proceeds to paste those values into the table and therefore into the waves that the table displays.

If you select the first cell in the first unused column, the paste will be a create-paste. In this case, Igor makes new waves, appends them to the table and then stores the data in the clipboard in the new waves. It makes one new wave for each column of text in the clipboard. If the text starts with a row of column names, Igor uses this row as the basis for the names of the new waves. Otherwise Igor uses default wave names.

### Mismatched Number of Columns {#mismatched-number-of-columns}

If the number of columns in the clipboard is not the same as the number of columns selected in the table then Igor asks you how many columns to paste. This applies to the replace-paste but not to the insert-paste or create-paste.

For example, if you have M columns of text in the clipboard but you select N columns and then do a paste, Igor presents presents the Columns to Paste dialog which gives you two options:


-	Paste M columns using the current selection


-	Change the selection and paste N columns

### Mismatched Number of Rows {#mismatched-number-of-rows}

If the number of rows in the clipboard is not the same as the number of rows selected in the table then Igor asks you how many rows to paste. This applies to the replace-paste but not to the insert-paste or create-paste.

For example, if you have M rows of text in the clipboard but you select N rows and then do a paste, Igor presents the Rows to Paste dialog which gives you three options:


-	Paste M rows using the current selection


-	Change the selection and paste N rows


-	Replace the selected N rows with M rows from the clipboard

### Pasting and Index Columns {#pasting-and-index-columns}

Since the values of an index column are computed based on point numbers, they cannot be altered by pasting. However, if index columns and data columns are adjacent in a range of selected cells, a paste can still be done. The data values will be altered by the paste but the index values will not be altered.

### Pasting and Column Formats {#pasting-and-column-formats}

When you paste plain text data into existing numeric columns, Igor tries to interpret the text in the clipboard based on the numeric format of the columns. For example, if a column is formatted as dates then Igor tries to interpret the text according to the table date format. If the column is formatted as time then Igor tries to interpret the text as a time values (e.g., 10:00:00). If the column has a regular number format, Igor tries to interpret the text as regular numbers.

When you paste plain text data into unused columns, Igor does a create-paste. In this case, Igor inspects the text in the clipboard to determine if the data is in date format, time format, date and time format or regular number format. When it appends new columns to the table, it applies the appropriate numeric format.

When pasting octal or hexadecimal text in a table, you must first set the column format to octal or hexadecimal so that Igor will correctly interpret the text.

If the column does not appear to be in any of these formats, Igor creates a text wave rather than a numeric wave.

See [Date Values](#date-values) for details on entering dates.



## Copy-Paste Waves {#copy-paste-waves}

You can copy and paste entire waves within Igor. This is described under [Creating New Waves by Pasting Data from Igor](#creating-new-waves-by-pasting-data-from-igor).



## Inserting and Deleting Points {#inserting-and-deleting-points}

In addition to pasting and cutting, you can also insert and delete points from waves using the Insert Points and Delete Points dialogs via the Data menu or via the Table pop-up menu. You can use these dialogs to modify waves without using a table but they do work intelligently when a table is the top window.



## Finding Table Values {#finding-table-values}

You can search tables for specific contents by choosing Edit→Find. This displays the Find In Table dialog.



Find In Table can search the current selection in the active table, the entire active table or all table windows. You control this using the right-hand pop-up menu at the top of the dialog.

The All Table Windows mode searches standalone table windows only. It does not search table subwindows. It is possible to search a table subwindow in a control panel using the Top Table mode. Searching in tables embedded in graphs and page layouts is not supported.

Find In Table can search for the following types of values which you control using the left-hand pop-up menu.


| Find Type | Description |
| --- | --- |
| Row | Displays the specified row but does not select it. |
| Text String | Finds the specified text string in any type of column: text, numeric, date, time, date/time, and dimension labels. |
|  | For example, searching for "-1" would find numeric cells containing -1.234 and -1e6. A given cell is found only once, even if the search string occurs more than once in that cell. |
|  | The target string is limited to 254 bytes. |
| Blank Cell | Finds blank cells in any type of column: text, numeric, date, time, date/time, and dimension labels. Finds blank cells in numeric columns (NaNs) and text columns (text elements containing zero characters). |
| Numeric Value | Finds numeric values within the specified range in numeric columns only. Does not search the following types of columns: text, date, time, date/time, and dimension labels. |
| Date | Finds date values within the specified range in date and date/time columns only. Does not search the following types of columns: text, numeric, time and dimension labels. |
|  | Accepts input of dates in the format specified by Table Date Format dialog (Table menu). |
| Time of Day | Finds a time of day within the specified range in time and date/time columns only. Does not search the following types of columns: text, numeric, date and dimension labels. |
|  | A time of day is a time between 00:00:00 and 24:00:00. Times are entered as hh\:mm\:ss.ff with the seconds part and fractional part optional. |
| Elapsed Time | Finds an elapsed time within the specified range in time columns only. Does not search the following types of columns: text, numeric, date, date/time and dimension labels. |
|  | Unlike a time of day, an elapsed time can be negative and can be greater than 24:00:00. Times are entered as hh\:mm\:ss.ff with the seconds part and fractional part optional. |
| Date<span class="table-cell-nowrap">/Time</span> | Finds a date/time within the specified range in date/time columns only. Does not search the following types of columns: text, numeric, date, time and dimension labels. |
|  | Date/time values consist of a date, a space and a time. |



`Find In Table` does not search the point column.

The search starts from the "anchor" cell. If you are searching the top table or the current selection, the anchor cell is the target cell. If you are searching all tables, the anchor cell is the first cell in the first-opened table, or the last cell in the last-opened table if you are doing a backward search.

When you do an initial search via the Find dialog, the search includes the anchor cell. When you do a subsequent search using Find Again, the search starts from the cell after the anchor cell, or before it if you are doing a backward search.

A find in the top table starts from the target cell and proceeds forward or backward, depending on the state of the Search Backwards checkbox. The search stops when it hits the end or beginning of the table, unless Wrap Around Search is enabled, in which case the whole table is searched.

A find in the current selection also starts from the target cell and proceeds forward or backward, depending on the state of the Search Backwards checkbox. The search stops when it hits the end or beginning of the selection, unless Wrap Around Search is enabled, in which case the whole selection is searched.

If Search Rows First is selected, all rows of a given column are searched, then all rows of the next column. If Search Columns First is selected, all columns of a given row are searched, then all columns of the next row.

To do a search of a 3D or 4D wave, you must create a table containing just that wave. Then the Table Find will search the entirety of the wave. If the table contains more than one wave, the Table Find will not search the parts (e.g. other layers of a 3D wave) of a 3D or 4D wave that are not shown in the table.

Choosing Find Selection from the Edit menu sets the Find mode to Find Text String, Find Blank Cells, Find Numeric Value, Find Date, Find Time Of Day, Find Elapsed Time or Find Date/Time based on the format of the target cell except that, if the target cell is blank, the mode is set to Find Blank Cells regardless of the cell's format.

You may find it convenient to use Find Again (Ctrl+G) after doing an initial find to find subsequent cells with the specified contents. Pressing Ctrl+Shift+G does a Find Again in the opposite direction.



## Replacing Table Values {#replacing-table-values}

You can perform a mass replace in a table by choosing Edit→Replace. This displays the Replace In Table dialog.



Unlike Find In Table, which can search all tables, Replace In Table is limited to the top table or the current selection, as set by the right-hand pop-up menu.

When you click Replace All, Replace In Table first finds the specified cell contents using the same rules as Find In Table. It then replaces the contents with the specified replace value. It then continues searching and replacing until it hits the end of the table or selection, unless Wrap Around Search is enabled, in which case the whole table or selection is searched.

You can undo all of the replacements by choosing Edit→Undo Replace.

Replace In Table does not affect X columns. You must use the Change Wave Scaling dialog (Data menu) for that.

Replace In Table goes through each candidate cell looking for the specified search value. If it finds the value, it extracts the text from the cell and does the replacement on the extracted text. If the resulting text is legal given the format of the cell, the replacement is done. If it is not legal, Replace In Table stops and displays an error dialog showing where the error occurred.

Here are some additional considerations regarding Replace In Table.


| Find Type | Description |
| --- | --- |
| Text String | In each cell, all occurrences of the find string are replaced with the replace string. For example, if you replacing "22" with "33" and a cell contains the value 122.223, the resulting value will be 133.333. The replace string is limited to 254 bytes. |
|  | Using text string replace, it is possible to come up with a value that is not legal given a cell's formatting. For example, if you replace "22" with "9.9" in the example above, you get "19.9.9.93". This is not a legal numeric value so Replace In Table displays an error dialog. |
| Date | You can replace a date in a date column or a date/time column. When replacing a date in a date/time column, the time component is not changed. Dates must be use the format specified by Table Date Format dialog (Table menu). |
| Time of Day | You can replace a time of day in a time column or a date/time column. When replacing a time of day in a date/time column, the date component is not changed. |



### Selectively Replacing Table Values {#selectively-replacing-table-values}

The Replace In Table dialog is designed to do a mass replace. You can do a selective replace using the Find In Table dialog followed by a series of Find Again and Paste operations. Here is the process:


1.	Choose Edit→Find and find the first cell containing the value you want to replace.


2.	Edit that cell so it contains the desired value.


3.	Copy that cell's contents to the clipboard.


4.	Do Find Again Ctrl+G to find the next cell you might want to replace.


5.	If you want to replace the found cell, do Paste Ctrl-V.


6.	If not done, go back to step 4.



## Exporting Data from Tables {#exporting-data-from-tables}

You can use the clipboard to export data from an Igor table to another application. If you do this you must be careful to preserve the precision of the exported data.

When you copy data from an Igor table, Igor puts the data into the clipboard in two formats: tab-delimited text and Igor binary.

If you later paste that data into an Igor table, Igor uses the Igor binary data so that you retain all precision through the copy-paste operation.

If you paste the data into another application, the other application uses the text data that Igor stored in the clipboard. To prevent losing precision, Igor uses enough digits to represent the data with full precision.

You can also export data via files by choosing Data→Save Waves→Save Delimited Text or File→Save Table Copy.



## Changing Column Positions {#changing-column-positions}

You can rearrange the order of columns in the table. To do this, position the cursor over the name of the column that you want to move. While pressing Alt, the cursor changes to a hand. If you now click the mouse, you can drag an outline of the column to its new position.

When you release the mouse the column will be redrawn in its new position. Igor always keeps all of the columns for a particular wave together so if you drag a column, you will move all of the columns for that wave.

The point column cannot be moved and is always at the extreme left of the cell area.



## Changing Column Widths {#changing-column-widths}

You can change the width of a column by dragging the vertical boundary to the right of the column name.

You can influence the manner in which column widths are changed by pressing certain modifier keys.

If Shift is pressed, all table columns except the Point column are changed to the same width.

The Ctrl key determines what happens when you drag the boundary of a data column of a multi-dimensional wave. If that key is not pressed, all data columns of the wave are set to the same width. If that key is pressed then just the dragged column is changed.

### Autosizing Columns By Double-Clicking {#autosizing-columns-by-double-clicking}

You can autosize a column by double-clicking the vertical boundary to the right of the column name.

You can influence the manner in which column widths are changed by pressing certain modifier keys.

If the no modifier keys are pressed and you double-click the boundary of a data column of a multidimensional wave then the width of each data column is set individually.

When pressing Alt and you double-click the boundary of a data column of a multidimensional wave then the width of all data columns are set the same.

If Shift is pressed, all table columns except the Point column are autosized. Shift pressed with Alt will autosize all data columns of a given wave to the same width.

When pressing Ctrl, only the double-clicked column is autosized, not all data columns of a multidimensional wave.

### Autosizing Columns Using Menus {#autosizing-columns-using-menus}

You can autosize columns by selecting them and choosing Autosize Columns from the Table menu or from the table popup menu in the top-right corner of the table. You can also choose Autosize Columns from the contextual menu that you get when you right-click on a column.

You can influence the manner in which column widths are changed by pressing certain modifier keys.

If the no modifier keys are pressed and a data column of a multidimensional wave is selected, all data columns of that wave are set individually.

If Alt is pressed and a data column of a multidimensional wave is selected, all data columns of that wave are set the same.

If Shift is pressed, all table columns except the Point column are autosized. Shift pressed with Alt will autosize all data columns of a given wave to the same width.

When pressing Ctrl, only the selected columns are autosized, not all data columns of a multidimensional wave.

### Autosizing Limitations {#autosizing-limitations}

When you autosize a column, the width of every cell in that column must determined. For very long columns (100,000 points or more), this may take a very long time. When this happens, cell checking stops and the autosize is based only on the checked cells.

Similarly, if you autosize the data columns of a multidimensional wave with a very large number of columns (10,000 or more columns), this could take a very long time. When this happens, columns checking stops and the autosize is based only on the checked columns.

If the default time limits are not suitable, use the [ModifyTable](/igorpro/commands/modifytable.md) autosize keyword to set the time limits.



## Changing Column Styles {#changing-column-styles}

You can change the presentation style of columns in a table using the Modify Columns dialog, the Table menu in the main menu bar, the Table pop-up menu, or the contextual menu that you get by right-clicking.

You can invoke the Modify Columns dialog from the Table menu, from the Table pop-up menu (gear icon), from the contextual menu, or by double-clicking a column name.

You can select one or more columns in the Columns to Modify list. If you select more than one column, the items in the dialog reflect the settings of the first selected column.

Once you have made your selection, you can change settings for the selected columns. After doing this, you can then select a different column or set of columns and make more changes. Igor remembers all of the changes you make, allowing you to do everything in one trip to the dialog.

There is a shortcut for changing a setting for all columns at once without using the dialog: Press Shift while choosing an item from the Table menu, from the Table pop-up menu, or from the contextual menu.

Tables are primarily intended for on-screen data editing. You can use a table for presentation purposes by exporting it to another program as a picture or by including it in a page layout. However, it is not ideal for this purpose. For example, there no way to change the background color or the appearance of gridlines.

You can capture your favorite styles as preferences. See [Table Preferences](#table-preferences).



## Modifying Column Properties {#modifying-column-properties}

You can independently set properties, such as color, column width, font, etc., for the index or dimension label column and the data column of 1D waves. Except in rare cases all of the data columns of a multidimensional wave should have the same properties. When you set the properties of one data column of a multidimensional wave using Igor's menus or using the Modify Columns dialog, Igor sets the properties of all data columns the same.

For example, if you are editing a 3 x 3 2D wave and you set the first data column to red, Igor will make the second and third data columns will red too.

Despite Igor's inclination to set all of the data columns of a multidimensional wave the same, it is possible to set them differently. Select the columns to be modified. Press Ctrl before clicking the Table menu or Table pop-up menu and make a selection. Your selection will be applied to the selected columns only instead of to all data columns from the selected waves.

The ModifyTable operation supports a column number syntax that designates a column by its position in the table. Using this operation, you can set any column to any setting. For example:


```igor
Make/O/N=(3,3) mat
Edit mat
ModifyTable rgb[1]=(50000,0,0), rgb[2]=(0,50000,0)
```

This sets mat's first data column to red and its second to blue.

You can specify a range of columns using column number syntax:


```igor
ModifyTable rgb[1,3]=(50000,0,0)
```

The Modify Columns dialog sets the properties for both the real and imaginary columns of complex waves at the same time. If you really want to set the properties of the real and imaginary columns differently, you must use the column number syntax shown above.

### Column Titles {#column-titles}

The column title appears at the top of each column. By default, Igor automatically derives the column title from the name of the wave displayed in the column. For example, if we display the X index and data values of wave1 and data values of wave2, the table will have columns titled wave0.x, wave0.d, and wave1.

Igor uses the suffixes ".x" and ".d" only if this is necessary to distinguish columns. If there is no index column displayed, Igor omits the suffix.

Using the title setting in the Modify Columns dialog, you can replace the automatically derived title with a title of your own. Remove all text from the title setting to turn the automatic title back on.

The title setting changes only the title of the column in this table. It does not change wave name. We provide the column title setting primarily to make tables look better in presentations (in layouts and exported pictures). If you are not using a table for a presentation, it is better to let Igor automatically generate column titles since this has less potential for confusion. If you want to rename a wave, use the Rename items in the Data and Table pop-up menus.

If you really need to use column titles for multidimensional waves, use the techniques described in [Modifying Column Properties](#modifying-column-properties) to set the title for individual columns.

### Numeric Formats {#numeric-formats}

Columns in tables display either text or numeric waves. For numeric waves, the column format determines how the data values in the wave are entered and displayed. The column format has no effect on data columns of text waves.

In addition to regular number formats, tables support date, time and date&time formats. The format is merely a way of displaying a number. Even dates and times are stored internally in Igor as numbers. You can enter a value in a numeric column of a table as a number, date, time or date&time if you set the format for the column appropriately.

The following table lists all of the numeric formats.

| Numeric Format | Description |
| --- | --- |
| General | Displays numbers in a format appropriate to the number itself. Very large or small numbers are displayed in scientific notation. Other numbers are displayed in decimal form (e.g. 1234.567). The Digits setting controls the number of significant digits. Integers are displayed with no fractional digits. |
| Integer | Numbers are displayed as the nearest integer number. For example, 1234.567 is displayed as 1235. |
| Integer with comma | Numbers are displayed as the nearest integer number. In addition, commas are used to separate groups of three digits. For example, 1234.567 is displayed as 1,235. |
| Decimal | As many digits to the left of the decimal point as are required are used to display the number. The Digits setting controls the number of digits to the right of the decimal point. For example, if the number of digits is specified as two, 1234.567 is displayed as 1234.57. |
| Decimal with comma | Identical to the decimal format except that commas are used to separate groups of three digits to the left of the decimal point. |
| Scientific | Numbers are displayed in scientific notation. The Digits setting controls the number of digits to the right of the decimal point. |
| Date | Dates are displayed using the format set in the Table Date Format dialog. See [Date/Time Formats](#date-time-formats). |
| Time | [+][-]hhhh\:mm\:ss[.ff] [AM/PM]. See [Date/Time Formats](#date-time-formats). |
| Date & Time | Date format plus space plus time format. See [Date/Time Formats](#date-time-formats). |
| Octal | Numbers are displayed in octal (base 8) notation. Only integers are supported. The number of digits displayed depends on the wave data type and the Digits setting is ignored. See [Octal Numeric Format](#octal-numeric-format) for details. |
| Hexadecimal | Numbers are displayed in hexadecimal (base 16) notation. Only integers are supported. The number of digits displayed depends on the wave data type and the Digits setting is ignored. See [Hexadecimal Numeric Format](#hexadecimal-numeric-format) for details. |

When you enter a number in a table, Igor expects either dot or comma as the decimal symbol, as determined by the Decimal Symbol setting in the Table Misc Settings dialog. The factory default setting is dot. This setting applies only to entering numbers in tables. To change it, choose Table→Table Misc Settings. If it is set to Per System Settings and you change the system decimal symbol, you must restart Igor for the change to take effect.

For most numeric formats you can control the number of displayed digits. You can set this using the Modify Columns dialog or using the Digits submenu of the Table menu, table pop-up menu (gear icon), or table contextual menu. The meaning of the number that you choose from the Digits submenu depends on the numeric format.


| Numeric Format | You Specify |
| --- | --- |
| General | Number of displayed digits |
| Decimal (0.0...0) | Number of digits after the decimal point |
| Decimal with comma (0.0...0) | Number of digits after the decimal point |
| Time and Date&Time | Number of digits after the decimal point when displaying fractional seconds |
| Scientific (0.0...0E+00) | Number of digits after the decimal point |

The Digits setting has no effect on columns displayed using the integer, octal, and hexadecimal formats and also has no effect on columns displaying text waves. It affects time and date/time formats only if the display of fractional seconds is enabled.

With the General format, you can choose to display trailing zeros or not.

With the time format, Igor accepts and displays times from -9999:59:59 to +9999:59:59. This is the supported range of elapsed times. If you are entering a time-of-day rather than an elapsed time, you should restrict yourself to the range 00:00:00 to 23:59:59.

With the Time and Date&Time formats, you can choose to display fractional seconds. Most people dealing with time data use whole numbers of seconds. Therefore, by default, a table does not show fractional seconds. If you want to see fractional seconds in a table, you must tell Igor by choosing Show Fractional Seconds from the Table→Format menu. Once you do this, the Table→Digits menu controls the number of digits that appear in the fractional part of the time.

If you always want to see fractional seconds, use the Capture Table Prefs dialog to capture columns whose Show Fractional Seconds setting is on. This applies to tables created after you capture the preference.

When displaying fractional seconds, Igor always displays trailing zeros and the Show Trailing Zeros menu item in the Table→Format menu has no effect.

When choosing a format, remember that single precision floating point data stores about 7 decimal digits and double-precision floating point data stores about 16 decimal digits. If you want to inspect your data down to the last decimal place, you need to select a format with enough digits.

The format does not affect the precision of data that you export via the clipboard from a table to another application. See [Exporting Data from Tables](#exporting-data-from-tables).

### Date/Time Formats {#date-time-formats}

As described under [Date Values](#date-values), the way you enter dates in tables and the way that Igor displays them is controlled by the Table Date Format dialog which you invoke through the Table menu. This dialog sets a global preference that determines the date format for all tables. By factory default, the table date format is controlled by the system Regional Settings control panel.

If you set the column format to time, then Igor displays time in elapsed time format. You can enter elapsed times from -9999:59:59 to +9999:59:59. You can precede an elapsed time with a minus sign to enter a negative elapsed time. You can also enter a fractional seconds value, for example 31:35:20.19. To view fractional seconds, choose Show Fractional Seconds from the Format submenu of the Table menu.

You can also enter times in time-of-day format, for example 1:45 PM or 1:45:00 PM or 13:45 or 13:45:00. A space before the AM or PM is allowed but not required. AM and am have no effect on the resulting time. PM adds 12 hours to the time. PM has no effect if the hour is already 12 or greater.

Igor stores times the same way whether they are time-of-day times or elapsed times. The difference is in how you think of the value and how you choose to display it in a graph.

Here are some valid time-of-day times:

|  |  |
| --- | --- |
| 00:00:00 (midnight) | 12:00:00 (noon) |
| 06:30:00 (breakfast time) | 18:30:00 (dinner time) |
| 06:30 (breakfast time) | 18:30 (dinner time) |
| 06:30 PM (dinner time) | 18:30 PM (dinner time) |

Here are some valid elapsed times:

|  |  |
| --- | --- |
| -00:00:10 | (T minus 10 and counting) |
| 72:00:00 | (an elapsed time covering three days) |
| 4:17:33.25 | (an elapsed time with fractional seconds) |

The format for a date/time wave in a table defaults to Date, Time, or Date/Time depending on the content of the wave.


For displaying date/time data in a graph, see [Date/Time Axes](/igorpro/graphing/graphs.md#date-time-axes).

### Octal Numeric Format {#octal-numeric-format}

You can format any numeric column in a table as octal. Igor ignores the digits setting for columns displayed as octal and always displays all digits required for the supported range of values.

For floating point waves (single-precision and double-precision), negative values are displayed using a minus sign as this is necessary to accurately present the wave value. For example, -1 is displayed as -00000001.

It is possible to store in floating point waves a value that can't be displayed in octal because the value is fractional or exceeds the supported range of values. In these cases, the table will display an error message such as "# Can't format fractional value as octal" or "# Value too large to display as octal".

If you are using a floating point wave for data you think of as integer data of a given size, consider redimensioning the wave to the appropriate integer type using the [Redimension](/igorpro/commands/redimension.md) operation. For example, if you are storing 16-bit signed integer data in a floating point wave, consider redimensioning the wave as 16-bit signed integer to get a more appropriate octal display in a table.

### Hexadecimal Numeric Format {#hexadecimal-numeric-format}

You can format any numeric column in a table as hexadecimal. Igor ignores the digits setting for columns displayed as hexadecimal and always displays all digits required for the supported range of values.

For floating point waves (single-precision and double-precision), negative values are displayed using a minus sign as this is necessary to accurately present the wave value. For example, -1 is displayed as -00000001.

It is possible to store in floating point waves a value that can't be displayed in hexadecimal because the value is fractional or exceeds the supported range of values. In these cases, the table will display an error message such as "# Can't display fractional value as hex" or "# Value too large to display as hex".

If you are using a floating point wave for data you think of as integer data of a given size, consider redimensioning the wave to the appropriate integer type using the [Redimension](/igorpro/commands/redimension.md) operation. For example, if you are storing 16-bit signed integer data in a floating point wave, consider redimensioning the wave as 16-bit signed integer to get a more appropriate hexadecimal display in a table.

### Object Reference Wave Formatting {#object-reference-wave-formatting}

This section is for advanced users only.

In addition to text and numeric waves, tables can also display object reference waves. An object reference wave is a WAVE wave or a DFREF wave.

The elements of object reference waves are displayed with full precision either as decimal integer, hexadecimal, or octal. If the column format is integer or octal, the column is displayed as integer or octal. If the column format is any other format, including general, decimal, scientific, date, time, and date&time, the column is displayed as hexadecimal.



## Editing Text Waves {#editing-text-waves}

You can create a text wave in a table by clicking in the first unused cell and entering non-numeric text. For the most part, editing a text wave is self-evident. However, there are some issues, mostly relating to special characters or large amounts of text, that you may run into.

### Large Amounts of Text in a Single Cell {#large-amounts-of-text-in-a-single-cell}

A text wave is handy for storing short descriptions of corresponding data in numeric waves. In some cases, you may find it useful to store larger amounts of text. Igor imposes no limit on the number of characters in a point of a text wave. However, the entry area of a table can handle no more than 100,000 bytes. If you click in a cell containing more than 100,000 bytes, Igor will tell you that the cell can't be edited in a table.

### The Edit Text Cell Dialog {#the-edit-text-cell-dialog}

You edit numeric wave data using the table entry line. To edit text wave data, you can use the the table entry line or the Edit Text Cell dialog. The dialog is convenient for editing multi-line data. It is also convenient for editing text to be used for annotations.

When a text wave cell is selected, an icon appears at the right end of the table entry line. Click the icon to invoke the dialog.

The next section discusses using the Edit Text Cell dialog to edit tabs and terminators.

### Tabs, Terminators, and Other Control Characters {#tabs-terminators-and-other-control-characters}

In rare cases, you may want to store text containing control characters such as tabs and terminators (carriage-returns and linefeeds) in text waves. You can't enter such characters in the table entry line, but you can enter them using the Edit Text Cell dialog. To display the dialog, click the icon at the right end of the table entry line. This icon appears only when you are editing an existing text wave.

You can display whitespace characters (tabs, spaces, and terminators) in the Edit Text Cell dialog by right-clicking in the text entry area and choosing Settings→Show Whitespace. This is recommended for editing multi-line text. Tabs and terminators are identified with these symbols:


|  |  |
| --- | --- |
| → | Tab |
| ↵ | Carriage-return (CR) |
|  | For historical reasons, CR is the Igor-standard line terminator. Text for use within Igor should have CR terminators. |
| ¬ | Linefeed (LF) |
|  | LF is the Unix-standard line terminator. Text for use with Unix programs should have LF terminators. |
| ¶ | Carriage-return/linefeed (CRLF) |
|  | CRLF is the Windows-standard line terminator. Text for use with Windows programs should have CRLF terminators. |

When the dialog's text entry area includes one or more terminators, buttons appear that allow you to change terminators:

<img src="MD_images/Tables/Tabs,_Terminators,_and_Ot_0.png" width="50%"/>

You can also enter control characters by executing a command. For example:


```igor
textWave0[0] = "Hello\tGoodbye"		// Text with tab character
```

Use \\t for tab, \\r for carriage-return, and \\n for linefeed.

You can examine what is a text wave by printing it from the command line:


```igor
Print textWave0
```

This displays tabs, carriage-returns and linefeeds using escape sequences.

For expert debugging purposes, you can get a hex dump of text wave and dimension label cell contents by pressing Ctrl and double-clicking a cell. The hex dump is printed in the history area of the command window.



## Editing Invalid Text {#editing-invalid-text}

Some patterns of bytes are invalid in some text encodings. For example, this command creates a UTF-8 text wave with invalid text:


```igor
Make/O/T test = {"A", "\xFE", "C"}	// "\xFE" represents a single byte with value 0xFE
```

Point 1 of the wave is invalid because, in UTF-8, any byte outside the range 0x00..0x7F must be part of a multi-byte character. Invalid bytes are displayed in table cells using the Unicode replacement character.

The most likely way for this situation to arise is if you have a text wave containing MacRoman, Windows-1252 or Shift JIS text but the wave's text encoding is mistakenly set to UTF-8. In this case, you can either edit the wave to remove the invalid text or correct Igor's notion of the wave's text encoding using Misc→Text Encodings→Set Wave Text Encoding. In this section we assume that you want to edit the wave.

If you click a cell containing invalid text, Igor displays a yellow warning icon. If you attempt to edit the cell contents, Igor displays a warning dialog.

When the yellow warning icon is visible, the entry line works in a special mode. Each invalid byte in the cell is represented by a \\x escape code. In the example above, if you click the cell representing point 1 of the wave, Igor displays \\xFE in the entry area.

While editing the text, in most cases you will want to remove the escape sequences.

If you accept the text in the entry area, Igor converts any remaining \\x escape sequences back to the bytes which they represent. In the example above, assuming that you started the editing process, made no changes in the entry line, and accepted the text, the contents of the cell would be the same after editing as they were before.

This use of escape sequences in tables applies only when the yellow warning icon is visible, indicating that the cell contained invalid text when you selected it. It applies only to \x escape sequences, not to other escape sequences such as \\t (tab), \\r (carriage-return) or \\n (linefeed). If the yellow warning icon is not visible, there is no special treatment of escape sequences.

For expert debugging purposes, you can get a hex dump of text wave and dimension label cell contents by double-clicking the yellow warning icon. You can also get a hex dump whether the warning icon is visible or not by pressing Ctrl and double-clicking a cell. The hex dump is printed in the history area of the command window.

See Also:	[Text Encodings](/igorpro/igor-basics/text-encodings.md), [Wave Text Encodings](/igorpro/igor-basics/text-encodings.md#wave-text-encodings)



## Editing Control Characters {#editing-control-characters}

Control characters are special non-printing characters created in olden times for controlling teletype machines and similar equipment. The ASCII codes for control characters, expressed as hexadecimal, fall in the range 0x00 to 0x1F, except for 0x7F which is the delete control character.

Other than tab (0x09), carriage-return (CR, 0x0D) and linefeed (LF, 0x0A), control characters have little use and rarely appear in modern computer text. When they do appear, it is often the result of an error or bug. Null (0x00) is used internally in many programs to mean "end-of-string" but should not appear in text documents.

In nearly all computer fonts, control characters are displayed as blanks. This makes it difficult to recognize and edit them, if they happen to appear in text whether on purpose or by error.

When Igor displays a control character in a table cell, it displays a "stand-in" symbol so that you can see what is there instead of seeing a blank. Here are some examples:

| Character | ASCII Code | **Stand-in Symbol** (Unicode) |
| --- | --- | --- |
| Tab | 0x09 | → (U+2192) |
| CR | 0x0D | ↵ (U+21B5) |
| LF | 0x0A | ¬ (U+00AC) |
| CRLF | 0x0D, 0x0A | ¶ (U+00B6) |
| Null | 0x00 | ␀ (U+2400) |
| Escape | 0x1B | ␛ (U+241B) |

If you click a cell containing a control character, Igor displays a yellow warning icon. If you attempt to edit the cell contents, Igor displays a warning dialog.

When the yellow warning icon is visible, the entry line works in a special mode. If you edit and accept the text in the entry line, Igor converts any remaining stand-in symbols back to the control characters which they represent.

This use of stand-in symbols in tables applies only when the yellow warning icon is visible. If the yellow warning icon is not visible, there is no special treatment of these symbols.

You can disable use of stand-in symbols by unchecking the Use Special Symbols for Control Characters checkbox in the Tables section of the Miscellaneous Settings dialog. Except in rare cases, you should leave that setting checked.



## Entering Special Characters {#entering-special-characters}

While editing a cell, you can enter special characters, such as Greek letters and math symbols, by choosing Edit→Characters for commonly-used characters such as Greek letters and math symbols or Edit→Special Characters for other characters.

If the wave whose element you are editing uses the UTF-8 text encoding, which is the default for waves created in Igor 7 or later, then you can enter any character.

If the wave uses another text encoding then it is not possible to represent all characters. For example, the triple integral character, U+222D, cannot be represented in MacRoman, Windows-1252, Shift JIS, or any other non-Unicode text encoding.

If you attempt to enter a character that cannot be represented in the wave's text encoding, Igor displays an alert informing you of the problem. Your options are to omit that character or to convert the wave to UTF-8, using Misc→Text Encoding→Set Wave Text Encoding.

#### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [Wave Text Encodings](/igorpro/igor-basics/text-encodings.md#wave-text-encodings)



## Editing Multidimensional Waves {#editing-multidimensional-waves}

If you view a multidimensional wave in a table, Igor adds some items to the table that are not present for 1D waves. To see this, execute the following commands which create and display a 2D wave:


```igor
Make/O/N=(3,4) w2D = p + 10*q; Edit w2D.id
```

The first column in the table is labelled Row, indicating that it shows row numbers. The second column contains the scaled row indices, which in this case are the same as the row numbers. The remaining columns show the wave data. Notice the name at the top of the first column of wave data: "w2D[][0].d". The "w2D" identifies the wave. The ".d" specifies that the column shows wave data rather than wave indices. The "[][0]" identifies the part of the wave shown by this column. The "[]" means "all rows" and the "[0]" means column 0. This is derived from the syntax that you would use from Igor's command line to store values into all rows of column 0 of the wave:


```igor
w2D[][0] = 123	// Set all rows of column 0 to 123
```

When displaying a multidimensional wave in a table, Igor adds a row to the table below the row of names. This row is called the horizontal index row. It can display either the scaled indices or the dimension labels for the wave elements shown in the columns below.

By default, if you view a 2D wave in a table and append the wave's index column, Igor displays the wave's row indices in a column to the left of the wave data and displays the wave's column indices in the horizontal index row, above the wave data.

If you append the wave's dimension label column, Igor displays the wave's row labels in a column to the left of the wave data and displays the wave's column labels in the horizontal index row, above the wave data.

If you display neither index columns nor dimension labels, Igor still displays the wave's column indices in the horizontal index row.

If you want to show numeric indices horizontally and dimension labels vertically or vice versa, you can use the Table→Horizontal Index submenu to override the default behavior. For example, if you want dimension labels vertically and numeric indices horizontally, append the wave's dimension label column to the table and then choose Table→Horizontal Index→Numeric Indices.

In the example above, the row and column indices are equal to the row and column element numbers. You can set the row and column scaling of your 2D data to reflect the nature of your data. For example, if the data is an image with 5 mm resolution in both dimensions, you should tell Igor about this using the following commands:


```igor
SetScale/P x 0, .005, w2D; SetScale/P y 0, .005, w2D
```

When you do this, you will notice that the row and column indices in the table reflect the scaling that you have specified.

1D waves have no column indices. Therefore, if you have no multidimensional waves in the table, Igor does not display the horizontal index row. If you have a mix of 1D and multidimensional waves in the table, Igor does display the horizontal index row but displays nothing in that row for the 1D waves.

When showing 1D data, Igor displays a column of point numbers at the left side of the table. This is called the Point column. When showing a 2D wave, Igor titles the column Row or Column depending on how you are viewing the 2D wave. If you have 3D or 4D waves in the table, Igor titles the column Row, Column, Layer or Chunk, depending on how you are viewing the waves.

It is possible to display a mix of 1D waves and multidimensional waves such that none of these titles is appropriate. For example, you could display two 2D waves, one with the wave rows shown vertically (the normal case) and one with the wave rows shown horizontally. In this case, Igor will title the Point column "Element".

You can edit dimension labels in the main body of the table by merely clicking on the cell and typing. However, you can't edit dimension labels in the horizontal index row this way. Instead you must double-click a label in this row. Igor then displays a dialog into which you can enter a dimension label. You can also set dimension labels using the SetDimLabel operation from the command line.

### Changing the View of the Data {#changing-the-view-of-the-data}

A table can display waves of dimension 1 through 4. A one dimensional wave appears as a simple column of numbers, or, if the wave is complex, as two columns, one real and one imaginary. A two dimensional wave appears as a matrix. In the one and two dimensional cases, you can see all of the wave data at once.

If you display a three dimensional wave in a table, you can view and edit only one slice at a time. To see this, execute the following commands:


```igor
Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D.id
```

Initially you see the slice of the wave whose layer index is 0 — layer zero of the wave. You can change which layer you are viewing using the next layer (<img src="MD_images/Tables/Changing_the_View_of_the__2.png" width="33%"/>) and previous layer (<img src="MD_images/Tables/Changing_the_View_of_the__3.png" width="33%"/>) icons that appear in the top/right corner of the table or using keyboard shortcuts.

By analogy with the up-arrow and down-arrow keys as applied to the row dimension of a 1D wave, "up" means "previous layer" (lower index) and "down" means "next layer" (higher index).

To change the layer from the keyboard, press `Alt+Up Arrow` to view the previous layer and `Alt+Down Arrow` to view the next layer.

Pressing the Shift key reverses the direction for both the icons and the arrow keys.

If you know the index of the layer you want to view you can enter it directly in a dialog by pressing `Ctrl` while clicking the next or previous layer icon.

If you display a four dimensional wave in a table, you can still view and edit only one layer at a time. You can change which layer you are viewing by using the icons or keyboard shortcuts described above. To view the previous chunk in the 4D wave, press `Alt` while clicking the up icon or press `Ctrl+Alt+Up Arrow`. To view the next chunk, press the Alt key while clicking the down icon or press `Ctrl+Alt+Down Arrow`.

In addition to using the keyboard shortcuts, you can specify the layer and chunk that you want to use using the ModifyTable elements operation.

### Changing the Viewed Dimensions {#changing-the-viewed-dimensions}

When you initially view a 3D wave in a table, Igor shows a slice of the wave in the rows-columns plane. The wave's rows dimension is mapped to the table's vertical dimension and the wave's columns dimension is mapped to the table's horizontal dimension.

Using the Choose Dimensions icon, which appears to the right of the layer icons, you can instruct Igor to map any wave dimension to the vertical table dimension and any other wave dimension to the horizontal table dimension. This is primarily of interest if you work with waves of dimension three or higher because you can view and edit any orthogonal plane in the wave. You can, for example, create a new wave that contains a slice of data from the 3D wave.

When you click the Choose Dimensions icon, Igor displays the Choose Dimensions dialog. This dialog allows you to specify how the dimensions in the wave are to be displayed in the table.

### ModifyTable Elements Command {#modifytable-elements-command}

This section discusses choosing viewed dimensions using the ModifyTable "elements" keyword. You do not need to know about this unless you want a thorough understand of editing 3D and 4D waves and viewing them from different perspectives.

The best way to understand this section is to execute all of the commands shown.

Igor needs to know which wave dimension to map to the vertical table dimension and which wave dimension to map to the horizontal table dimension. In addition, for waves of dimension three or higher, Igor needs to know which element of the remaining dimensions to display.

The form of the command is:


```igor
ModifyTable elements(<wave name>) = (<row>,<column>,<layer>,<chunk>)
```

The parameters specify which element of the wave's rows, columns, layers and chunks dimensions you want to view. The value of each parameter may be an element number (0 or greater) or it may be a special value. There are three special values that you can use for any of the parameters:

|  |  |
| --- | --- |
| -1 | means no change from the current value |
| -2 | means map this dimension to the table's vertical dimension |
| -3 | means map this dimension to the table's horizontal dimension |

In reading the following discussion, remember that the first parameter specifies how you want to view the wave's rows, the second parameter specifies how you want to view the wave's columns, the third parameter specifies how you want to view the wave's layers and the fourth parameter specifies how you want to view the wave's chunks.

If you omit a parameter, it takes the default value of -1 (no change). Thus, if you are dealing with a 2D wave, you can supply only the first two parameters and omit the last two.

To get a feel for this command, let's start with the example of a simple matrix, which is a 2D wave.


```igor
Make/O/N=(3,3) wave0 = p + 10*q
Edit wave0.id
```

As you look down in the table, you see the rows of the matrix and as you look across the table, you see its columns. Thus, initially, the rows dimension is mapped to the vertical table dimension in the and the columns dimension is mapped to the horizontal table dimension. This is the default mapping. You can change this with the following command:


```igor
ModifyTable elements(wave0) = (-3, -2)
```

The first parameter tells Igor how you want to view the wave's rows and the second parameter tells Igor how you want to view the wave's columns. Since the wave has only two dimensions, the third and fourth parameters can be omitted.

The -3 in this example tells Igor that you want to map the wave's rows to the table's horizontal dimension. The -2 tells Igor that you want to map the wave's columns to the table's vertical dimension.

You can return the wave to its default view using:


```igor
ModifyTable elements(wave0) = (-2, -3)
```

When you consider a 3D wave, things get a bit more complex. In addition to the rows and columns dimensions, there is a third dimension -- the layers dimension. When you initially create a table containing a 3D wave, it shows all of the rows and columns of layer 0 of the wave. Thus, as with the 2D wave, the rows dimension is mapped to the vertical table dimension and the columns dimension is mapped to the horizontal table dimension. You can control which layer of the 3D wave is displayed in the table using the icons and keyboard shortcuts described above, or using the ModifyTable elements keyword.

For example:


```igor
Make/O/N=(5,4,3) wave0 = p + 10*q + 100*r
ModifyTable elements(wave0)=(-2, -3, 1)	// Shows layer 1 of the 3D wave
ModifyTable elements(wave0)=(-2, -3, 2)	// Shows layer 2 of the 3D wave
```

In these examples, the wave's layers dimension is fixed to a specific value whereas the wave's rows and columns dimensions change as you look down or across the table. The term "free dimension" refers to a wave dimension that is mapped to either of the table's dimensions. The term "fixed dimension" refers to a wave dimension for which you have chosen a fixed value.

In the preceding example, we viewed a slice of the 3D wave in the rows-columns plane. We can view any orthogonal plane. For example, this command tells Igor to show us the data in the layers-rows plane:


```igor
ModifyTable elements=(-3, 0, -2)		// Shows column 0 of the 3D wave
```

The first parameter says that we want to map the wave's rows dimension to the table's horizontal dimension. The second parameter says that we want to see column 0 of the wave. The third parameter says that we want to map the wave's layers dimension to the table's vertical dimension.

Dealing with a 4D wave is similar to the 3D case, except that, in addition to the two free dimensions, you have two fixed dimension.


```igor
Make/O/N=(5,4,3,2) wave0 = p + 10*q + 100*r + 1000*s
ModifyTable elements(wave0)=(-2, -3, 1, 0)	// Shows layer 1/chunk 0
ModifyTable elements(wave0)=(-2, -3, 2, 1)	// Shows layer 2/chunk 1
```

If you change a wave (using Make/O or Redimension) such that one or both of the free dimensions has zero points, Igor automatically resets the view to the default -- the wave's rows dimension mapped to the table's vertical dimension and the wave's column dimension mapped to the table's horizontal dimension. Here is an example:


```igor
Make/O/N=(5,4,3) wave0 = p + 10*q + 100*r
Edit wave0.id
Modify elements(wave0) = (0, -2, -3)	// Map layers to horizontal dimension
Redimension/N=(5,4) wave0				// Eliminate layers dimension!
```

This last command has eliminated the wave dimension that is mapped to the table horizontal dimension. Thus, Igor will automatically reset the table view.

If you ask Igor to use a dimension with zero points as a free dimension, Igor will also reset the view to the default:


```igor
Make/O/N=(3,3) wave0 = p + 10*q
Edit wave0.id
Modify elements(wave0) = (0, -2, -3)		// Map layers to horizontal dimension
```

This last command maps the wave's layers dimension to the table's horizontal dimension. However, the wave has no layers dimension, so Igor will reset the view to the default.

The initial discussion of changing the view using keyboard shortcuts was incomplete for the sake of simplicity. It said that Alt+Down Arrow displayed the next layer and that Command-Option-Down Arrow or Ctrl+Alt+Down Arrow displayed the next chunk. This is true if rows and columns are the free dimensions. A more general statement is that Option-Down Arrow or Alt+Down Arrow changes the viewed element of the first fixed dimension and Command-Option-Down Arrow or Ctrl+Alt+Down Arrow changes the viewed element of the second fixed dimension. Here is an example using a 4D wave:


```igor
Make/O/N=(5,4,3,2) wave0 = p + 10*q + 100*r + 1000*s
Edit wave0.id
ModifyTable elements(wave0)=(0, -2, 0, -3)
```

The ModifyTable command specifies that the columns and chunks dimensions are the free dimensions. The rows and layers dimensions are fixed at 0. If you now press `Option-Down Arrow` or `Alt+Down Arrow`, you change the element of the first fixed dimension — the rows dimension in this case. If you press `Command-Option-Down Arrow` or `Ctrl+Alt+Down Arrow`, you change the element of the second fixed dimension — the layers dimension in this case.

## Multidimensional Copy/Cut/Paste/Clear {#multidimensional-copy-cut-paste-clear}

The material in this section is primarily of interest if you intend to edit 3D and 4D data in a table. There are also a few items that deal with 2D data.

When you copy table cells, Igor copies the data in two formats:

- Igor binary, for pasting into another Igor wave
- Plain text, for pasting into another program

For 1D and 2D waves, the subset that you copy and paste is obvious from the table selection. In the case of 3D and 4D waves, you can only see two dimensions in the table at one time and you can select a subset of those two dimensions.

When copying as plain text, Igor always copies just the visible cells to the clipboard.

When copying as Igor binary, if you press Alt while doing the copy, Igor copies cells from all dimensions.

Consider the following example. We make a wave with 5 rows, 4 columns and 3 layers and display it in a table:


```igor
Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D.id
```

The table now displays all rows and all columns of layer 0 of the wave. If you select all of the visible data cells and do a copy, Igor copies all of layer 0 to the clipboard. However, if you do an Option-copy or Alt-copy, Igor copies all three layers to the clipboard — layer 0 plus the two layers that are currently not visible — in Igor binary format.

This table shows the effect of the Alt key.

|  |  |  |  |
| --- | --- | --- | --- |
|  | **Copy** | **Paste** | **Clear** |
| No modifiers | Copies visible | Replace-pastes visible | Clears visible |
| Alt | Copies all | Replace-pastes all | Clears all |

The middle column of the preceding table mentions "replace-pasting". When you do a paste, Igor normally replaces the selection in the table with the data in the clipboard. However, if you press Shift while pasting, Igor inserts the data as new cells in the table. This is called an "insert-paste". This table shows the effect of the Alt keys on a paste.

|  |  |
| --- | --- |
|  | **Paste** |
| No modifiers | Replace-pastes visible |
| Alt | Replace-pastes all |
| Shift | Insert-pastes visible |
| Shift and Alt | Insert-pastes all |

### Replace-paste of Multidimensional Data {#replace-paste-of-multidimensional-data}

If you copy data in a table, and then select cells in the table or in another table, and do a paste, you are doing a replace-paste. The copied data replaces the selection when you do the paste.

For 1D and 2D waves, the subset that you copy and paste is obvious from the table selection. In the case of 3D and 4D waves, you can only see two dimensions in the table at one time and you can select a subset of those two dimensions.

When you do a normal replace-paste involving waves of dimension 3 or higher, the data in the clipboard replaces the data in the currently visible slice of the selected wave.

### Copying a Layer of a 3D Wave to Another Layer {#copying-a-layer-of-a-3d-wave-to-another-layer}

Here is an example that illustrates replace-paste.


1.	Make a wave with 5 rows, 4 columns and 3 layers and display it in a table:


	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

	The table now displays all rows and all columns of layer 0 of the wave. Let's look at layer 1 of the wave.


2.	Press Alt+Down Arrow while the table is active.

	This changes the view to show layer 1 instead of layer 0.


3.	Select all of the visible cells and choose Edit→Copy.

	This copies all of layer 1 to the clipboard.


4.	Press Option-Down Arrow or Alt+Down Arrow again to view layer 2 of the wave.


5.	With all of the cells still selected, choose Edit→Paste.

	The data copied from layer 1 replaces the data in layer 2 of the wave.


6.	Choose Edit→Undo.

	Layer 2 is restored to its original state.


7.	Press Option-Up Arrow or Alt+Up Arrow two times.

	We are now looking at layer 0.


8.	Choose Edit→Paste.

	The data that we copied from layer 1 replaces the data in layer 0.


9.	Choose Edit→Undo to return layer 0 to the original state.

### Copying and Pasting All Data of a 3D Wave {#copying-and-pasting-all-data-of-a-3d-wave}

Now let's consider an example in which we copy and paste all of the wave data, not just one layer.


1.	Make a wave with 5 rows, 4 columns and 3 layers and display it in a table:

	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

2.	Select all of the visible cells.


3.	Press Alt and choose Edit→Copy All Layers.

	This copies the entire wave, all three layers, to the clipboard.


4.	Press Option or Alt and choose Edit→Clear All Layers.

	This clears all three layers.


5.	Use Option-Down Arrow or Alt+Down Arrow and Option-Up Arrow or Alt+Up Arrow to verify that all three layers were cleared.


6.	Press Option or Alt and choose Edit→Paste All Layers.

	This pastes all three layers from the clipboard into the selected wave.


7.	Use Option-Down Arrow and Option-Up Arrow or Alt+Down Arrow and Alt+Down Arrow to verify that all three layers were pasted.

### Making a 2D Wave from Two 1D Waves {#making-a-2d-wave-from-two-1d-waves}

In this example, we make a 2D wave from two 1D waves. Execute:


```igor
Make/O/N=5 w1DA=p, w1DB=100+p; Edit w1DA, w1DB
```

1.	Select all of the first 1D wave and choose Edit→Copy.
2.	Click in the first unused cell in the table and choose Edit→Paste.

	Because you pasted into the unused cell, Igor created a new wave. This is a "create-paste".

3.	Choose Redimension w1DA1 from the Table pop-up menu (gear icon).
4.	In the Redimension Waves dialog, enter 2 for the number of columns and click `Do It`.
5.	Right-click the column name of the redimensioned wave and choose Rename.
6.	Rename w1DA1 as w2D.
7.	Select all of the second 1D wave, w1DB, and choose Edit→Copy.
8.	Select all of the second column of the 2D wave, w2D, and choose Edit→Paste.

We now have a 2D wave generated from two 1D waves.

### Insert-paste of Multidimensional Data {#insert-paste-of-multidimensional-data}

If you copy data in a table, and then select cells in the table or in another table, and do a paste while pressing Shift, you are doing an insert-paste. The copied data is inserted into the selected wave or waves before the selected cells. As in the case of the replace-paste, the insert-paste works on just the visible layer of data if Alt is not pressed or on all layers if Alt is pressed. Next is an example that illustrates this.

### Inserting New Rows in a 3D Wave {#inserting-new-rows-in-a-3d-wave}


1.	Make a 3D wave and display it in a table:

	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

2.	Select all of the cells in rows 1 and 2 of the table.

	An easy way to do this is to click the "1" in the Row column and drag down to the "2".


3.	Choose Edit→Copy to copy the selected cells.

	Since you did not press Option or Alt, this copies just the visible layer.


4.	Press Shift and choose Edit→Insert Paste to insert-paste the copied data.

	Notice that two new rows were inserted, pushing the pre-existing rows down.


5.	Press Option-Down Arrow or Alt+Down Arrow to see what was inserted in layers 1 and 2 of the 3D wave.

	Notice that zeros were inserted. This is because the paste stored data only in the visible layer.


6.	Press Option-Up Arrow or Alt+Up Arrow to view layer 0 again.


7.	Choose Edit→Undo to undo the paste.


8.	Use Option-Down Arrow or Alt+Down Arrow to check the other layers of the wave and then use Option-Up Arrow or Alt+Up Arrow to come back to layer zero.

	The wave is back in its original state.

	Now we will do an insert-paste in all layers.


9.	Select rows 1 and 2 of the wave.


10.	Press Option or Alt and choose Edit→Copy All Layers.

	This copies data from all three layers to the clipboard.


11.	Press Shift-Option or Shift+Alt and choose Edit→ Insert Paste All Layers.

	This pastes data from the clipboard into all three layers of the wave. By pressing Shift, we told Igor that we wanted to do an insert-paste rather than a replace-paste. By pressing Option or Alt, we told Igor that we wanted to paste into all layers, not just the visible layer.


12.	Use Option-Down Arrow or Alt+Down Arrow to verify that we have pasted data into all layers.

### Cutting and Pasting Rows Versus Columns {#cutting-and-pasting-rows-versus-columns}

Normally, you cut and paste rows of data. However, there may be cases where you want to cut and paste columns. For example, if you have a 2D wave with 5 rows and 3 columns, you may want to cut the middle column from the wave. Here is how Igor determines if you want to cut rows or columns.

If the selected wave is 2D or higher, and if one or more entire columns is selected, Igor cuts the selected column or columns. In all other cases Igor cuts rows.

After copying or cutting wave data, you have data in the clipboard. Normally, a paste overwrites the selected rows or inserts new rows (if you press Shift).

To insert columns, you need to do the following:


1. Copy the column that you want to insert.
2. Select exactly one entire column. You can do this quickly by clicking in the column name.
3. Press Shift and choose Edit→Insert Paste or press Ctrl+Shift+V.

If the wave data is real (not complex), Igor normally pastes the new column or columns before the selected column. This behavior would provide you with no way to paste columns after the last column of a wave. Therefore, if the selected column is the last column, Igor presents a dialog to ask you if you want to paste the new columns before or after the last column.

If the wave data is complex, Igor pastes the new columns before the selected column if the selected column is real or after the selected column if it is imaginary.

If you select more than one column or if you do not select all of the column, Igor will insert rows instead of columns.

### Create-paste of Multidimensional Data {#create-paste-of-multidimensional-data}

When you copy data in a table and then select the first unused cell in the table and then do a paste, Igor creates one or more new waves.

The number of waves created and the number of dimensions in each wave are the same as for the copied data. Igor also copies and pastes the following wave properties:


- Data units and dimension units
- Data full scale and dimension scaling
- Dimension labels
- The wave note

Igor copies and pastes the wave note only if you copy the entire wave. If you copy part of the wave, it does not copy the wave note.

You can use a create-paste to create a copy of a subset of the data displayed in the table. For 1D and 2D waves, the subset that you copy and paste is obvious from the table selection. In the case of 3 and higher dimension waves, you can only see two dimensions in the table at one time and you can choose a subset of those two dimensions. If you do a copy and then a create-paste, Igor creates a new 2D wave containing just the data that was visible when you did the copy. If you do an Alt-copy to copy all and then a create-paste, Igor creates a new wave with the same number of dimensions and same data as what you copied.

### Making a 2D Wave from a Slice of a 3D Wave {#making-a-2d-wave-from-a-slice-of-a-3d-wave}


1.	Make a 3D wave and display it in a table:

	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

2.	Select all of the cells of the 3D wave and choose Edit→Copy.


3.	Click in the first unused cell and choose Edit→Paste.

You now have a 2D wave consisting of the data from layer 0 of the 3D wave.

### Making a 3D Wave from a 3D Wave {#making-a-3d-wave-from-a-3d-wave}


1.	Make a 3D wave and display it in a table:

	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

2.	Select all of the cells of the 3D wave.


3.	Press Option or Alt, and choose Edit→Copy All Layers.


4.	Click in the first unused cell and choose Edit→Paste.

You now have a 3D wave consisting of the data from all layers of the original 3D wave.

To confirm this, we will inspect all layers of the new wave.


5.	View the other layers of the new wave by pressing Option-Down Arrow or Alt+Down Arrow (to go to the next layer) and Option-Up Arrow or Alt+Up Arrow (to go to the previous layer).

### Making a 1D Wave from a Column of a 3D Wave {#making-a-1d-wave-from-a-column-of-a-3d-wave}


1.	Make a 3D wave and display it in a table:

	```igor
	Make/O/N=(5,4,3) w3D = p + 10*q + 100*r; Edit w3D
	```

2.	Select a single column of the 3D wave and choose Edit→Copy.


3.	Click the first unused cell in the table and choose Edit→Paste.

	You have created a single-column wave but it is a 2D wave, not a 1D wave.


4.	Choose Redimension w3D1 from the Table pop-up menu (gear icon) to display the Redimension Waves dialog.


5.	In the Redimension Waves dialog, enter 0 for the number of columns and click `Do It`.

	You now have a 1D wave created from a column of a 3D wave.



## Save Table Copy {#save-table-copy}

You can save the active table as an Igor packed experiment file or as a tab or comma-delimited text file by choosing File→Save Table Copy.

The main uses for saving as a packed experiment are to save an archival copy of data or to prepare to merge data from multiple experiments (see [Merging Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#merging-experiments)). The resulting experiment file preserves the data folder hierarchy of the waves displayed in the table starting from the "top" data folder, which is the data folder that encloses all waves displayed in the table. The top data folder becomes the root data folder of the resulting experiment file. Only the table and its waves are saved in the packed experiment file, not variables or strings or any other objects in the experiment.

Save Table Copy does not know about dependencies. If a table contains a wave, wave0, that is dependent on another wave, wave1 which is not in the table, Save Table Copy will save wave0 but not wave1. When the saved experiment is open, there will be a broken dependency.

The main use for saving as a tab or comma-delimited text file is for exporting data to another program.

The point column is never saved.

When saving as text, the data format matches the format shown in the table. This causes truncation if the underlying data has more precision than shown in the table.

To save data as text with full precision, choose Data→Save Waves→Save Delimited Text or use the [SaveTableCopy](/igorpro/commands/savetablecopy.md) operation with /F=1.

When saving 3D and 4D waves as text, only the visible layer is saved. To save the entirety of a 3D or 4D wave, choose Data→Save Waves→Save Delimited Text.

The [SaveTableCopy](/igorpro/commands/savetablecopy.md) operation provides options that are not available using the Save Table Copy menu command.



## Object Reference Waves in Tables {#object-reference-waves-in-tables}

This topic is for advanced users.

Object reference waves are waves containing wave references (WAVE waves) or data folder references (DFREF waves).

Object reference wave elements are formatted as hexadecimal by default. See [Object Reference Wave Formatting](#object-reference-wave-formatting) for details.

Because entering an invalid reference may cause a crash, you cannot modify the elements of an object reference wave by editing in the table.

If you display an object reference wave in a table, turn column info tags on via the Table menu, and hover the mouse over an element of the object reference wave, Igor displays in the column info tag information about the wave or data folder referenced by the element. This feature works in the debugger if you have column info tags turned on.

### Editing Waves Referenced by WAVE Waves {#editing-waves-referenced-by-wave-waves}

This is a feature for advanced users.

If you have a WAVE wave displayed in table, you can select one or more cells of that wave, right-click, and choose Edit Waves. Igor creates a new table showing the waves referenced by the selected wave references in the table.

You can do the same using the table popup menu (gear icon in top/right corner of the table). The Edit Waves item does not appear in the Table menu in the main menu bar.

The Edit Waves item appears in the contextual menu or table popup menu only if one or more editable wave references are selected. NULL waves (wave reference=0) and free waves cannot be edited in a table.

​This feature is not available in the table subwindow in the debugger.



## Printing Tables {#printing-tables}

Before printing a table you should bring the table to the top of the desktop and set the page size and orientation using the Page Setup dialog. Choose the Page Setup for All Tables item from the Files menu.

In each experiment, Igor stores one page setup for all tables. Thus, changing the page setup while a table is active changes the page setup for all tables in the current experiment.

When you invoke the Page Setup dialog you must make sure that the table that you want to print is the top window. Changing the page setup for graphs, page layouts, or other windows does not affect the page setup for tables.

You can print all or part of a table. To print the whole table, select just one cell and choose File→Print Table. To print the selection, select multiple cells and choose File→Print Table Selection.



## Exporting Tables as Graphics {#exporting-tables-as-graphics}

Although Igor tables are intended primarily for editing data, you can also use them for presentation purposes. You can put a table into an Igor page layout, as discussed in [Page Layouts](/igorpro/graphing/making-figures/page-layouts.md). This section deals with exporting a table to other applications as a picture.

Typically you would do this if you are preparing a report in a word processor or page layout program or making an illustration in a drawing program. If you are exporting to a program that has strong text formatting features, it may be better to copy the data from the table as text, using the Copy item in the Edit menu. You can paste the text into the other program and then format it as you wish.

### Exporting a Table as a Picture {#exporting-a-table-as-a-picture}

To export a table as a Macintosh picture via the clipboard, choose Export Graphics from the Edit menu. This copies the table to the clipboard as a picture.

The picture that Igor puts into the clipboard contains just the visible cells in the table window. You can scroll, expand or shrink the window to control which cells will appear in the picture.

Igor can write a picture out to a file instead of copying it to the clipboard. To do this, use the Save Graphics submenu of the File menu.

Most word processing, drawing and page layout programs permit you to import a picture via the clipboard or via a file.

Although we have not optimized tables for presentation purposes, we did put two features into tables specifically for presentation. First, you can hide the point column by setting its width to zero. Second, you can replace the automatic column titles with column titles of your own. Use the Modify Columns dialog for both of these.

There are some features lacking that would be nice for presentation. You can't change the background color of a table. You can't change or remove the grid lines. If you want to do these things, export the table to a drawing program for sprucing up.



## Table Preferences {#table-preferences}

Table preferences allow you to control what happens when you create a new table or add new columns to an existing table. To set preferences, create a table and set it up to your taste. We call this your prototype table. Then choose Capture Table Prefs from the Table menu.

Preferences are normally in effect only for manual operations, not for automatic operations from Igor procedures. This is discussed in more detail in [How to Use Preferences](/igorpro/igor-basics/using-igor.md#how-to-use-preferences).

When you initially install Igor, all preferences are set to the factory defaults. The dialog indicates which preferences you have changed, and which are factory defaults.

The Window Position and Size preference affects the creation of new tables only.

The Column Styles preference affects the formatting of newly created tables and of columns added to an existing table. This preference stores column settings for the point column and for one additional column - the first column after the point column in the prototype table. When you create a new table or add columns to a table, these settings determine the formatting of the columns.

The page setup preference affects what happens when you create a new experiment, not when you create a new table. Here is why.

Each experiment stores one page setup for all tables in that experiment. The preferences also store one page setup for tables. When you set the preferred page setup for tables, Igor stores a copy of the current experiment's page setup for tables in the preferences file. When you create a new experiment, Igor stores a copy of the preferred page setup for tables in the experiment.



## Table Style Macros {#table-style-macros}

The purpose of a table style macro is to allow you to create a number of tables with the same stylistic properties. Using the Window Control dialog, you can instruct Igor to automatically generate a style macro from a prototype table. You can then apply the macro to other tables.

Igor can generate style macros for graphs, tables and page layouts. However, their usefulness is mainly for graphs. See [Graph Style Macros](/igorpro/graphing/graphs.md#graph-style-macros). The principles explained there apply to table style macros also.



## Shortcuts for Tables {#shortcuts-for-tables}

See [Table Shortcuts](/igorpro/user-interface/igor-shortcuts.md#table-shortcuts) and [Table Keyboard Navigation](#table-keyboard-navigation).