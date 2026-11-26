---
description: "The CreateBrowser operation creates a data browser window. It has two uses."
slug: /commands/createbrowser
---

<div className="command-signature">

## <strong>CreateBrowser</strong>  [/M] [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#createbrowser}

</div>

The CreateBrowser operation creates a data browser window. It has two uses:


-	To display the regular data browser


-	To display a modal data browser when you want the user to choose one or more data objects to be used as input by a procedure

Usually you leave it up to the user when to display the regular data browser, so the main purpose of CreateBrowser is to create the modal data browser for use as a user-interface element during a procedure.

The modal data browser is separate from the regular data browser and normally exists only briefly, while you are using it to solicit input.

The CreateBrowser operation targets the modal data browser if you use the prompt keyword or if you use the /M flag. The purpose of the /M flag is to allow you to execute CreateBrowser followed by one or more ModifyBrowser commands before showing the modal data browser. This is illustrated by the SelectWavesUsingDataBrowser example below.

If you call CreateBrowser without the prompt keyword and without the /M flag, it creates the regular data browser, if it does not yet exist, and displays it. In this case, all CreateBrowser keywords are ignored.

The user can change the current data folder using the modal data browser. If you don't want to allow this, you can save and restore the current data folder as shown in the SelectDataObjects example below.

Using the executeMode keyword and related keywords, you can instruct the modal data browser to execute commands when the user clicks OK. This is illustrated by the SelectWavesAndDisplayInGraph example below.

The modal data browser creates output variables based on the user's selection as described below.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M</span> | Creates a modal browser if one has not already been created. prompt is the only keyword that is permitted when the /M flag is used. Although a modal browser is created, it is not shown until `ModifyBrowser/M showModalBrowser` is called. See the `SelectWavesUsingDataBrowser` example below. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">prompt = *string*</span> | *string* is any string that you would like to use as a prompt in a modal browser. If the /M flag is not used, the presence of the prompt keyword will cause the modal browser to be shown when the command is executed. |
| The following keywords are for use when creating an immediate modal data browser using the prompt keyword without the <span class="table-cell-nowrap">/M</span> flag. They are illegal when <span class="table-cell-nowrap">/M</span> is present. They are ignored when CreateBrowser is called to display the regular data browser (<span class="table-cell-nowrap">/M</span> and prompt are omitted). |  |
| <span class="table-cell-nowrap">command1 = *cmdStr*</span> | *cmdStr* contains the command that you want the modal data browser to execute when the user presses the OK button. It is the main command that is executed on selections. See the SelectWavesAndDisplayInGraph example below. |
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for further discussion. |
| <span class="table-cell-nowrap">command2 = *cmdStr*</span> | *cmdStr*  contains the secondary command that you want the modal data browser to execute when the user presses the OK button. It is executed only when the list of selected items exceeds the maximum command length and executeMode=2. command2 is ignored when command1 is empty. See the SelectWavesAndDisplayInGraph example below. |
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for further discussion. |
| executeMode=*mode* |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1</td><td>Execute the command specified by command1 on each selected item, one-at-a-time. This is the default setting.</td></tr><tr><td>*mode*&nbsp;=2</td><td>Execute the commands on the entire list of selected items at once, if possible. The command specified by command1 is executed first. If the list of all selected items exceeds the maximum command length, the command specified by command2 is executed on the remaining selections. See the SelectWavesAndDisplayInGraph example below.</td></tr></tbody></table>
|  | See [Data Browser Command String Limitations](/igorpro/igor-basics/data-folders.md#data-browser-command-string-limitations) for further discussion. |
| <span class="table-cell-nowrap">exitCommand = *cmdStr*</span> | *cmdStr*  contains the command that you want the modal data browser to execute before it is closed. This command does not act on the selection, and it is only executed if the command1 string is empty. |
| expandAll | Display all data folders fully expanded. |
| <span class="table-cell-nowrap">select = *findStr*</span> | Selects all item names that match *findStr*. |
|  | The match depends on the case-sensitivity and-whole word settings in effect for the Data Browser. See the  [ModifyBrowser](/igorpro/commands/modifybrowser.md) case and wholeWord keywords. |
| <span class="table-cell-nowrap">showWaves = *mode*</span> | *mode* =1 for the modal data browser to display waves in the list, 0 to hide waves. |
| <span class="table-cell-nowrap">showVars = *mode*</span> | *mode* =1 for the modal data browser to display numeric variables in the list, 0 to hide numeric variables. |
| <span class="table-cell-nowrap">showStrs = *mode*</span> | *mode* =1 for the modal data browser to display string variables in the list, 0 to hide string variables. |

### *Details* {#details}
When you use the modal data browser, the normal menus are not accessible. However, you can still use the following keyboard shortcuts:

| Action | Windows |
| --- | --- |
| Select All | Ctrl-A |
| Find | Ctrl-F |
| Use Selection For Find | None |
| Find Again | Ctrl-G |

### *Output Variables* {#output-variables}
CreateBrowser creates two output variables: V_Flag and S_BrowserList. The values of these outputs are meaningful only after the user dismisses the modal data browser by clicking the OK or Cancel button.

These output variables are local when CreateBrowser is executed from a procedure. There is no reason for you to create the modal data browser from the command line, but if you do, the output variables are global and are created in the current data folder at the time the CreateBrowser operation was invoked.


|  |  |
| --- | --- |
| V_flag | Set to 1 if the user clicks the OK button. |
|  | Set to 0 if the user clicks the Cancel button or the window's close button. |
| S_BrowserList | Contains a semicolon-separated list of the full path, quoted if necessary, of each selected item. The order of items in the list is undefined. |

### *Examples* {#examples}

```igor
// Display a modal data browser and return a string list
// of items selected by the user
Function/S SelectDataObjects()
	DFREF saveDF = GetDataFolderDFR		// Save current data folder before
	String promptStr = "Select Items"
	CreateBrowser prompt=promptStr, showWaves=1, showVars=0, showStrs=0
	SetDataFolder saveDF		// Restore current data folder

	if (V_Flag == 0)
		return ""			// User cancelled
	endif
	return S_BrowserList
End

// Display a modal data browser and display the waves selected
// by the user in a graph
Function SelectWavesAndDisplayInGraph()
	String cmd1 = "Display %s"
	String cmd2 = "AppendToGraph %s"
	String promptStr="Select Waves for Graph"
	CreateBrowser prompt=promptStr, executeMode=2, command1=cmd1, command2=cmd2
End

// This example illustrates use of the /M flag so that you can call
// ModifyBrowser on the modal data browser before displaying it.
Function/S SelectWavesUsingDataBrowser()
	// Create the modal data browser but do not display it
	CreateBrowser/M prompt="Select a wave:"

	// Show waves but not variables in the modal data browser
	ModifyBrowser/M showWaves=1, showVars=0, showStrs=0

	// Set the modal data browser to sort by name 
	ModifyBrowser/M sort=1, showWaves=1, showVars=0, showStrs=0

	// Hide the info and plot panes in the modal data browser 
	ModifyBrowser/M showInfo=0, showPlot=0

	// Display the modal data browser, allowing the user to make a selection
	ModifyBrowser/M showModalBrowser

	if (V_Flag == 0)
		return ""			// User cancelled
	endif
	return S_BrowserList	
End
```

### *See Also* {#see-also}

|  |
| --- |
| [The Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser), [ModifyBrowser](/igorpro/commands/modifybrowser.md), [GetBrowserSelection](/igorpro/commands/getbrowserselection.md), [GetBrowserLine](/igorpro/commands/getbrowserline.md) |