---
description: "The ModifyBrowser operation modifies the state of the Data Browser according to the specified keywords."
slug: /commands/modifybrowser
---

<div className="command-signature">

## <strong>ModifyBrowser</strong>  [/M] [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#modifybrowser}

</div>

The ModifyBrowser operation modifies the state of the Data Browser according to the specified keywords.

If the /M flag is present, the ModifyBrowser command applies to the modal data browser. Otherwise it applies to the regular data browser. See [CreateBrowser](/igorpro/commands/createbrowser.md) for a discussion of modal versus regular.

The order in which keywords in a single command are executed is undefined. If the behavior of one keyword depends on another keyword being executed first, use multiple ModifyBrowser commands instead of using both keywords in one command.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M</span> | Modifies the modal data browser, if one has been created using CreateBrowser/M. An error will result if no modal data browser has been created. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">animation = *mode*</span> | Controls the display of 3D and 4D waves in the plot pane of the Data Browser. |
|  | Use *mode*=0 to stop the animation and *mode*=1 to start animation. "Animation" refers the the sequencing through the various layers of the 3D or 4D wave. |
| <span class="table-cell-nowrap">appendUserButton = {*buttonName,buttonCmdStr* [,*options*]}</span> |  |
|  | Appends a user-defined button below the Execute Cmd button in the Data Browser window. |
|  | *buttonName* must be valid as an Igor liberal name. It is used as the button's title as well as its name. |
|  | *buttonCmdStr* is a standard Data Browser command string as described for the command1 keyword. The command can apply to the current selection in the Data Browser's main list, using %s to represent the selected item or items, or it can be completely independent. |
|  | *options* is defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Delete button on new experiment (default)</td></tr><tr><td>1:</td><td>Retain button on new experiment</td></tr></tbody></table>
|  | All other values are reserved for future use. |
|  | New buttons are appended below the currently existing buttons and the Data Browser's window is sized to accomodate them. Don't add too many buttons or the window height will exceed the screen height. |
|  | If you use appendUserButton with a button name that already exists, the new *buttonCmdStr* and *options* are applied to the already existing button. |
|  | For more information see the documentation for the keyword deleteUserButton and [Managing Data Browser User-Defined Buttons](/igorpro/igor-basics/data-folders.md#managing-data-browser-user-defined-buttons). |
|  | appendUserButton is not allowed when the /M flag is used. |
| <span class="table-cell-nowrap">aspectRatio = *mode*</span> | Controls the aspect ratio of image plots in the plot pane. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Scales the image to fill the pane.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Retaining the original image aspect ratio.</td></tr></tbody></table>
| <span class="table-cell-nowrap">case = *state*</span> | Controls the case sensitivity of the find and select operations. |
|  |<table class="nested-table"><tbody><tr><td>*state*&nbsp;=0:</td><td>Case-insensitive</td></tr><tr><td>*state*&nbsp;=1:</td><td>Case-sensitive</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| clearSelection | Deselects any selected items. |
| close | Closes the Data Browser. If an exit command is specified, the Data Browser executes the command before it is closed. |
| <span class="table-cell-nowrap">collapse = *lineNum*</span> | *lineNum* is the zero-based line number of the data folder icon to collapse. The line number to use for a given data folder depends on the current sorting, filtering, and data folder expansion state of the browser. |
| collapseAll | Collapses all visible data folders. |
| <span class="table-cell-nowrap">command1 = *cmdStr*</span> | *cmdStr* contains the command that you want the Data Browser to execute when the executeCmd keyword is executed. It is the main command that is executed on selections. |
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for further discussion. |
| <span class="table-cell-nowrap">command2 = *cmdStr*</span> | *cmdStr* contains the secondary command that the Data Browser executes when the list of selected items exceeds the maximum command length and bit 1 of executeMode is set. command2 is ignored when command1 is empty. |
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for further discussion. |
| <span class="table-cell-nowrap">command3 = *cmdstr*</span> | *cmdStr* contains the command that the Data Browser executes each time the current data folder is changed from within the Data Browser. |
| <span class="table-cell-nowrap">dataFolderHistory = *h*</span> | *h* is a bitwise setting that controls the printing of messages in the history area of the command window. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Print a command in the history each time you change the current data folder from within the Data Browser.</td></tr><tr><td>Bit&nbsp;1:</td><td>Print the name of the experiment from which data is loaded using the Browse Expt button.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">deleteUserButton = *buttonName*</span> |  |
|  | Use this keyword to delete a named user button. This keyword is not allowed when the /M flag is used. |
| deleteAllUserButtons | Deletes all user buttons. |
| <span class="table-cell-nowrap">echoCommands = *mode*</span> | Set *mode* to zero to prevent printing of Data Browser-generated commands in the history area of the command window. This setting is saved in preferences and remembered between sessions. |
| executeCmd | Executes the Data Browser commands set using the command1 and command2 keywords on the current selection. |
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for details. |
| executeExitCmd | Execute the exit command if one exists. This does not close the Data Browser. |
| <span class="table-cell-nowrap">executeMode = *mode*</span> | *mode* is a bitwise setting that controls the execution of commands specified by the command1 and command2 keywords. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Executes command1 on each selected item, one-at-a-time. This is the default setting.</td></tr><tr><td>Bit&nbsp;1:</td><td>Execute the commands on the entire list of selected items at once, if possible. The command specified by command1 is executed first. If the list of all selected items exceeds the maximum command length, the command specified by command2 is executed on the remaining selections.</td></tr><tr><td>Bit&nbsp;2:</td><td>If set, when the user clicks the Execute Cmds button, the commands are executed without displaying the Execute on Browser selection dialog.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">exitCommand = *cmdStr*</span> | *cmdStr* contains the command that you want the Data Browser to execute before it is closed via the command line using close or executeExitCmd keywords. |
|  | This command is not executed if the user closes the Data Browser using the close boc. |
|  | If the browser is modal, the exit command is executed only if command1 is empty or if the ModifyBrowser/M executeExitCmd keyword is used. |
| <span class="table-cell-nowrap">expand = *lineNum*</span> | *lineNum* is the zero-based line number of the data folder icon to expand. The line number to use for a given data folder depends on the current sorting, filtering, and data folder expansion state of the browser. |
| expandAll | Expands all visible data folders as well as the top data folder. |
| <span class="table-cell-nowrap">find = *findStr*</span> | Finds an item in the Data Browser list. If a matching object is found, the item is scrolled into view, if necessary. |
|  | The match depends on the case-sensitivity and-whole word settings. See the case and wholeWord keywords. |
|  | Repeated applications of the command are equivalent to using the Find Same command in the menu. The find command uses the same settings that are set in the Find in Data Browser dialog which you access by choosing Edit→Find. |
| <span class="table-cell-nowrap">infoFont = *fontNameStr*</span> | Sets the font for the information pane. This setting is saved in preferences and remembered between sessions. Pass "" for *fontNameStr* to use the default font. |
| <span class="table-cell-nowrap">infoFontSize = *size*</span> | Sets the size in points of the text in the information pane. This setting is saved in preferences and remembered between sessions. Pass -1 for *size* to use the default font size. |
| <span class="table-cell-nowrap">palette = *palName*</span> | Sets the color table used for displaying plots of 2D, 3D, and 4D data in the plot pane. *palName* is a name of one of the built-in color tables listed in [Color Table Details](/igorpro/graphing/image-plots.md#color-table-details). |
| saveExpandedFolders | Creates a text wave named DB_FolderReference that contains the full unquoted paths to all expanded data folders. The first entry in the text wave is empty and represents the current top data folder displayed in the browser. You can use the paths stored in this wave with the function [GetBrowserLine](/igorpro/commands/getbrowserline.md) to obtain the line in which the expanded data folder is displayed. |
| <span class="table-cell-nowrap">saveOnlyDisplayedTypes = *mode*</span> |  |
|  | Controls what happens when you click the Save Copy button. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>All types will be saved even if they are not displayed.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Only displayed types are saved.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">select = *findStr*</span> | Selects all item names that match *findStr*. |
|  | The match depends on the case-sensitivity and-whole word settings. See the case and wholeWord keywords. |
| <span class="table-cell-nowrap">selectList = *strList*</span> | Toggles the selection state of all items specified in *strList* , a semicolon-separated list containing the full path for each data object. *strList* must be terminated with a semicolon. Liberal names may be quoted but quoting is not required. |
| <span class="table-cell-nowrap">setDataFolder = *path*</span> | Sets the top data folder. This is equivalent to double-clicking the data folder icon. *path* is a full path to the data folder. This does not change Igor's current data folder. Liberal names may be quoted but quoting is not required. |
| setDefaults | Overwrites user Data Browser preferences with factory defaults. All user-defined buttons are also deleted. |
| <span class="table-cell-nowrap">showInfo = *mode*</span> | Controls the visibility of the info pane. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides the info pane.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows the info pane.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| showModalBrowser | When used with the /M flag, shows the modal data browser, previously created by CreateBrowser/M, and waits for the user to click the OK or Cancel button. This keyword is only allowed when the /M flag is used. See [CreateBrowser](/igorpro/commands/createbrowser.md) for details. |
| <span class="table-cell-nowrap">showPlot = *mode*</span> | Controls the visibility of the plot pane. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides the plot pane.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows the plot pane.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">showStrs = *mode*</span> | Controls the visibility of string variables. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides string variables.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows string variables.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">showVars = *mode*</span> | Controls the visibility of numeric variables. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides numeric variables.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows numeric variables.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">showWaves = *mode*</span> | Controls the visibility of waves. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides waves.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows waves.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">showWaveStats = *mode*</span> | Controls what is displayed in the info pane. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Shows general information for the wave.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows statistics for the wave.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |
| <span class="table-cell-nowrap">slashK = *k*</span> | Controls the kill mode used when the Data Browser creates a window such as a table, graph or Gizmo plot. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr></tbody></table>
| <span class="table-cell-nowrap">sort = *sortKey*</span> | Controls the sorting of items. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Sort by creation time.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Sort by name.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Sort by name and data type.</td></tr></tbody></table>
| <span class="table-cell-nowrap">startLine = *lineNum*</span> | *lineNum* is the zero-based line number from which the next find operation is started if there is no selection. If there *is* a selection, the first selected line is used as the starting line and *lineNum* is ignored. |
|  | The *lineNum* to use for any given data folder may change depending on the current sorting and filtering of the browser and which data folders are expanded. |
| <span class="table-cell-nowrap">topLine = *lineNum*</span> | Moves *lineNum* so that it is visible in the browser. If there are enough items below *lineNum*, it is positioned so that it is the top line in the browser. This keyword does not affect the expanded state of data folders. |
|  | If necessary, *lineNum* is clipped to the largest line number in the browser. |
|  | The *lineNum* to use for any given data folder may change depending on the current sorting and filtering of the browser. |
| <span class="table-cell-nowrap">wholeWord = *state*</span> | Controls the whole-word behavior of the find and select operations. |
|  |<table class="nested-table"><tbody><tr><td>*state*&nbsp;=0:</td><td>The find and select keywords match items whose names contain the specified search string</td></tr><tr><td>*state*&nbsp;=1:</td><td>The find and select keywords match items whose names equal the specified search string.</td></tr></tbody></table>
|  | This setting is saved in preferences and remembered between sessions. |

### *Output Variables* {#output-variables}
ModifyBrowser creates two outputs, V_Flag and S_BrowserList, each time it is executed. The values of these outputs are meaningful only when you use the showModalBrowser keyword with the /M flag after creating a modal data browser using [CreateBrowser](/igorpro/commands/createbrowser.md)/M.

These output variables are local when CreateBrowser is executed from a procedure. There is no reason for you to show the modal data browser from the command line, but if you do, the output variables are global and are created in the current data folder at the time the ModifyBrowser operation was invoked with the  showModalBrowser keyword.


|  |  |
| --- | --- |
| V_flag | Set to 1 if the user clicks the OK button. |
|  | Set to 0 if the user clicks the Cancel button or the window's close button. |
| S_BrowserList | Contains a semicolon-separated list of the full path, quoted if necessary, of each selected item. The order of items in the list is undefined. |

### *See Also* {#see-also}

|  |
| --- |
| [The Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser), [CreateBrowser](/igorpro/commands/createbrowser.md), [GetBrowserSelection](/igorpro/commands/getbrowserselection.md) |