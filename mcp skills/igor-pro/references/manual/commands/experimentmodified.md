---
description: "The ExperimentModified operation gets and optionally sets the modified (save) state of the current experiment."
slug: /commands/experimentmodified
---

<div className="command-signature">

## <strong>ExperimentModified</strong>  [<em>newModifiedState</em> ] {#experimentmodified}

</div>

The ExperimentModified operation gets and optionally sets the modified (save) state of the current experiment.

Use this command to prevent Igor from asking you to save the current experiment after you have made changes you do not need to save or, conversely, to force Igor to ask about saving the experiment even though Igor would not normally do so.

The variable V_flag is always set to the experiment-modified state that was in effect before the ExperimentModified command executed: 1 for modified, 0 for not modified.

The string S_Info is always set to a semicolon-separated list of modifications to the current experiment since it was last saved or since ExperimentModified 0 was executed. This is the same list that appears in the "Do you want to save changes to experiment" dialog.

### *Parameters* {#parameters}
If *newModifiedState*  is present, it sets the experiment-modified state as follows:

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">*newModifiedState* = 0:</span> | Igor **will not** ask to save the experiment before quitting or opening another experiment, and the Save Experiment menu item will be disabled. |
| <span class="table-cell-nowrap">*newModifiedState* = 1:</span> | Igor **will** ask to save the experiment before quitting or opening another experiment, and the Save Experiment menu item will be enabled. |

If *newModifiedState*  is omitted, the state of experiment-modified state is not changed.

### *Details* {#details}
Executing ExperimentModified 0 on the command line will not work because the command will be echoed to the history area, marking the experiment as modifed. Use the command in a function or macro that does not echo text to the history area.

### *Examples* {#examples}
The /Q flag is vital: it suppresses printing into the history area which would mark the experiment as modified again.


```igor
Menu "Modified", dynamic
	"Mark Experiment Modified",/Q,ExperimentModified 1 // Enables "Save Experiment", sets V_Flag, S_Info
	"Mark Experiment Saved",/Q,ExperimentModified 0	  // Disables "Save Experiment"
	"-"
	ShowModifiedItems(),/Q, ; // do nothing
End

Function/S ShowModifiedItems()
	String dnm= "\\M0:1(:" // disabled no meta-chars
	ExperimentModified
	if( V_Flag )
		return dnm+ReplaceString(";", S_info, ";"+dnm)
	endif
	return dnm+"Not Modified"
End
```

### *See Also* {#see-also}
[SaveExperiment](/igorpro/commands/saveexperiment.md), [ExperimentInfo](/igorpro/commands/experimentinfo.md), [Menu Definition Syntax](/igorpro/user-interface/user-defined-menus.md#menu-definition-syntax)