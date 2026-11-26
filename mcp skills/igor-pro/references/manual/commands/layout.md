---
description: "The Layout operation creates a page layout. The Layout operation is antiquated and cannot be used in user-defined functions."
slug: /commands/layout
---

<div className="command-signature">

## <strong>Layout</strong>  [/A=(<em>rows</em>,<em>cols</em>)/B=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>]) /C=<em>color</em> /G=<em>g</em>  /HIDE=<em>h</em> /I /K=<em>k</em> /M /P=<em>orientation</em>  /R/S/T /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>)] [<em>objectSpec</em> [, <em>objectSpec</em> ]...] [<em>as</em> <em>titleStr</em> ] {#layout}

</div>

The Layout operation creates a page layout.
:::note
The Layout operation is antiquated and cannot be used in user-defined functions. For new programming, use the NewLayout operation instead.
:::

### *Parameters* {#parameters}

All of the parameters are optional.
Each *objectSpec* parameter identifies a graph, table, textbox or picture to be added to the layout. An object specification can also specify the location and size of the object, whether the object should have a frame or not, whether it should be transparent or opaque, and whether it should be displayed in high fidelity or not. See details below.

*titleStr* is a string expression containing the layout's title. If not specified, Igor will provide one which identifies the objects displayed in the graph.

### *Flags* {#flags}
|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = (rows,cols)</span> | Specifies rows and columns for tiling or stacking. |
| <span class="table-cell-nowrap">/B = (r,g,b[,a])</span> | Specifies the background color for the layout. *r*, *g*, *b*, and *a* specify the the color and optional opacity as RGBA Values. The default is opaque white. |
| <span class="table-cell-nowrap">/C = color</span> | Obsolete. In ancient times, this flag switched the screen display of the layout between black and white and color. It is still accepted but has no effect. |
| <span class="table-cell-nowrap">/G = g</span> | Specifies grout, the spacing between tiled objects. Units are points unless /I, /M, or /R are specified. |
| <span class="table-cell-nowrap">/HIDE = h</span> | Hides (h = 1) or shows (h = 0, default) the window. |
| /I | Specifies that coordinates are in inches. This affects subsequent /G, /W, and objectSpec  coordinates. Coordinates are relative to the top/left corner of the paper.
| <span class="table-cell-nowrap">/K = k</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>k&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>k&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>k&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>k&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>k&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the KillWindow operation. |
| /M | Specifies that coordinates are in centimeters. This affects subsequent /G, /W, and *objectSpec* coordinates. Coordinates are relative to the top/left corner of the paper.
| <span class="table-cell-nowrap">/P = orientation</span> | *orientation* is either Portrait or Landscape (e.g., `Layout/P= Landscape`). This controls the orientation of the page in the layout. See details below. |
|  | If you use the /P flag, you should make it the first flag in the Layout operation. This is necessary because the orientation of the page affects the behavior of other flags, such as /T and /G. |
| <span class="table-cell-nowrap">/R</span> | Specifies that coordinates are in percent. This affects subsequent /G, /W, and *objectSpec* coordinates. For /W, coordinates are in terms of percent of the main screen. For /G and objectSpec, coordinates are relative to the top/left corner of the printing part of the page. |
| <span class="table-cell-nowrap">/S</span> | Stacks objects. |
| <span class="table-cell-nowrap">/T</span> | Tiles objects. |
| <span class="table-cell-nowrap">/W = (left,top,right,bottom)</span> |  |
|  | Gives the layout window a specific location and size on the screen. Coordinates for /W are in screen units (pixels) unless /I or /M are specified. |

### *Details* {#details}

When you create a new layout window, if preferences are enabled, the page size is determined by the preferred page size as set via the Capture Layout Prefs dialog. If preferences are disabled, as is usually the case when executing a procedure, the page is set to the factory default size.

If you use the /P flag, you should make it the first flag in the Layout operation. This is necessary because the orientation of the page affects the behavior of other flags, such as /T and /G.

The form of an *objectSpec* is:

```igor
objectName[(objLeft, objTop, objRight, objBottom)] [/O=objType] [/F=frame] [/T=trans] [/D=fidelity]
```

*objectName* can be the name of an existing graph, table or picture. It can also be the name of an object that does not yet exist. In this case it is called a "dummy object".

*objectSpec* can be specified using a string by using the $ operator, but the entire objectSpec  must be in the string.

Here are some examples of valid usage:

```igor
Layout Graph0
Layout/I Graph0(1, 1, 6, 5)/F=1
String s = "Graph0"
Layout/I $s
String s = "Graph0(1, 1, 6, 5)/F=1"
Layout/I $s	// Entire object spec is in string.
```

The object's coordinates are determined as follows:

- If *objectName* is followed by a coordinates specification in (*objLeft*, *objTop*, *objRight*, *objBottom*) form then this sets the object's coordinates. The units for the coordinates are points unless the /I or /M flag was present in which case the units are inches or centimeters respectively.
- If the object coordinates are not specified explicitly but the Layout/S flag was present then the object is stacked. If the Layout/T flag was present then the object is tiled, and if the Layout/A=(*rows*,*cols*) flag is present, tiling is performed using that number of rows and columns.
- If the object's coordinates are not determined by these rules then the object is set to a default size and is stacked.

Each object has a type (graph, table, textbox or picture) determined as follows:
If the *objectName*/O=*objType* flag is present, then it determines the object's type:

|  |  |
| --- | --- |
| /O=*objType* |<table class="nested-table"><tbody><tr><td>*objType*&nbsp;=1:</td><td>Graph</td></tr><tr><td>*objType*&nbsp;=2:</td><td>Table</td></tr><tr><td>*objType*&nbsp;=8:</td><td>Picture</td></tr><tr><td>*objType*&nbsp;=32:</td><td>Textbox</td></tr></tbody></table>

If there is no /O flag and *objectName* is the name of an existing graph, table or picture, then the object type is graph, table or picture.

If the object's type is not determined by the above rules and *objectName* contains "Table", "PICT", or "TextBox", then the object type is table, picture or textbox.

If the object's type is not specified by any of the above rules, it is taken to be a graph type object.

The remaining flags have the following meanings:

|  |  |
| --- | --- |
| /D=*fidelity* |<table class="nested-table"><tbody><tr><td>*fidelity*&nbsp;=0:</td><td>Low fidelity display</td></tr><tr><td>*fidelity*&nbsp;=1:</td><td>High fidelity display (default)</td></tr></tbody></table>
| /F=*frame* |<table class="nested-table"><tbody><tr><td>*frame*&nbsp;=0:</td><td>No frame</td></tr><tr><td>*frame*&nbsp;=1:</td><td>Single frame (default)</td></tr><tr><td>*frame*&nbsp;=2:</td><td>Double frame</td></tr><tr><td>*frame*&nbsp;=3:</td><td>Triple frame</td></tr><tr><td>*frame*&nbsp;=4:</td><td>Shadow frame</td></tr></tbody></table>
| /T=trans |<table class="nested-table"><tbody><tr><td>*trans*&nbsp;=0:</td><td>Opaque (default)</td></tr><tr><td>*trans*&nbsp;=1:</td><td>Transparent For this to be effective, the object itself must also be transparent. Annotations have their own transparent/opaque settings. Graphs are transparent only if their backgrounds are white. Pictures may have been created transparent or opaque, and Igor cannot make an inherently opaque picture transparent.</td></tr></tbody></table>

### *See Also* {#see-also}

[NewLayout](/igorpro/commands/newlayout.md)