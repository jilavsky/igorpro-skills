---
description: "The NotebookAction operation creates or modifies an \"action\" in a notebook. A notebook action is an object that executes commands when clicked."
slug: /commands/notebookaction
---

<div className="command-signature">

## <strong>NotebookAction</strong>  [/W=<em>winName</em> ] <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] {#notebookaction}

</div>

The NotebookAction operation creates or modifies an "action" in a notebook. A notebook action is an object that executes commands when clicked.

See [Notebooks](/igorpro/igor-basics/notebooks.md) for general information about notebooks.

NotebookAction returns an error if the notebook is open for read-only. See [Notebook Read/Write Properties](/igorpro/igor-basics/notebooks.md#notebook-read-write-properties) for further information.

### *Parameters* {#parameters}
The parameters are in keyword =value format. Parameters are automatically limited to legal values before being applied to the notebook.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">bgRGB = (*r*, *g*, *b*)</span> | Specifies the action background color. *r* , *g* and *b* specify the amount of red, green, and blue as integers from 0 to 65535. |
| <span class="table-cell-nowrap">commands = *str*</span> | Specifies the command string to be executed when clicking the action. For multiline commands, add a carriage return (\r) between lines. |
| <span class="table-cell-nowrap">enableBGRGB = *enable*</span> | Uses the background color specified by the bgRGB parameter (*enable*=1). Background color is ignored for *enable*=0. |
| <span class="table-cell-nowrap">frame = *f*</span> | Specifies the frame enclosing the action. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single frame.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double frame.</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple border.</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">helpText = *helpTextStr*</span> | Specifies the help string for the action. The text is limited to 255 bytes. Help appears in the status line when the cursor is over the action. |
| <span class="table-cell-nowrap">ignoreErrors = *ignore*</span> | Controls whether an error dialog will appear (*ignore*=0) or not (*ignore* is nonzero) if an error occurs while executing the action commands. |
| <span class="table-cell-nowrap">linkStyle = *linkStyle*</span> | Controls the text style of the action title. If *linkStyle*=1, the style is the same as a help link (blue underlined). If *linkStyle*=0, the style properties are the same as the preceding text. |
| <span class="table-cell-nowrap">name = *name*</span> | Specifies the name of the new or modified notebook action. This is a standard Igor name. See [Standard Object Names](/igorpro/igor-basics/using-igor.md#standard-object-names) for details. |
| <span class="table-cell-nowrap">padding = {*leftPadding*, *rightPadding*, *topPadding*, *bottomPadding*, *internalPadding* }</span> |  |
|  | Sets the padding in points. *internalPadding* sets the padding between the title and the picture when both elements are present. |
| <span class="table-cell-nowrap">picture = *name*</span> | Specifies a picture for the action icon. *name* is the name of a picture in the picture gallery (see [Pictures](/igorpro/graphing/making-figures/graphics.md#pictures)). |
|  | If name is null ($""), it clears the picture parameter. |
| <span class="table-cell-nowrap">procPICTName = *name*</span> | Specifies a Proc Picture for the action icon (see [Proc Pictures](/igorpro/programming/programming.md#proc-pictures)). *name* is the name of a Proc Picture or null ($"") to clear it. This will be a name like ProcGlobal#myPictName or MyModuleName#myPictName. If you use a module name, the Proc Picture must be declared static. |
|  | If you specify both picture and procPICTName, picture will be used. |
| <span class="table-cell-nowrap">quiet = *quiet*</span> | Displays action commands in the history area (*quiet* =0), otherwise (*quiet* =1) no commands will be recorded. |
| <span class="table-cell-nowrap">scaling = {*h*, *v*}</span> | Scales the picture in percent horizontally, *h*, and vertically, *v*. |
| <span class="table-cell-nowrap">showMode = *mode*</span> | Determines if the title or picture are displayed. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>Title only.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Picture only.</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Picture below title.</td></tr><tr><td>*mode*&nbsp;=4:</td><td>Picture above title.</td></tr><tr><td>*mode*&nbsp;=5:</td><td>Picture to left of title.</td></tr><tr><td>*mode*&nbsp;=6:</td><td>Picture to right of title.</td></tr></tbody></table>
|  | Without a picture specification, the action will use title mode regardless of what you specify. |
| <span class="table-cell-nowrap">title = *titleStr*</span> | Sets the action title to *titleStr*, which is limited to 255 bytes. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the notebook window of interest. |
|  | *winName* is either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications. |
|  | If /W is omitted, NotebookAction acts on the top notebook window. |

### *Examples* {#examples}

```igor
String nb = WinName(0, 16, 1)	// Top visible notebook
NotebookAction name=Action0, title="Beep", commands="Beep"  // Create action
NotebookAction name=Action0, enableBGRGB=1, padding={4,4,4,4,4}
Notebook $nb, findSpecialCharacter={"Action0",1}            // Select action
Notebook $nb, frame=1                                       // Set frame
```

### *See Also* {#see-also}
[Notebooks](/igorpro/igor-basics/notebooks.md)

[Notebook](/igorpro/commands/notebook.md), [NewNotebook](/igorpro/commands/newnotebook.md), [OpenNotebook](/igorpro/commands/opennotebook.md)

[SpecialCharacterList](/igorpro/commands/specialcharacterlist.md), [SpecialCharacterInfo](/igorpro/commands/specialcharacterinfo.md)

### *Demos* {#demos}
[Open Notebook Actions Demo](#igor-pxp/Examples/Feature__Demos/Notebook__Actions__Demo.pxp)