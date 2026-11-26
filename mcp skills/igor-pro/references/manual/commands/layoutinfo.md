---
description: "The LayoutInfo function returns a string containing a semicolon-separated list of keywords and values that describe an object in the active page of a page…"
slug: /commands/layoutinfo
---

<div className="command-signature">

## <strong>LayoutInfo</strong> (<em>winNameStr</em>, <em>itemNameStr</em>) {#layoutinfo}

</div>

The LayoutInfo function returns a string containing a semicolon-separated list of keywords and values that describe an object in the active page of a page layout or overall properties of the layout. The main purpose of LayoutInfo is to allow an advanced Igor programmer to write a procedure which formats or arranges objects.

*winNameStr* is the name of an existing page layout window or "" to refer to the top layout.

*itemNameStr* is a string expression containing one of the following:


1.	The name (e.g., "Graph0") of a layout object in the active page to get information about that object.


2.	An object instance (e.g., "Graph0#0" or "Graph0#1") to get information about a particular instance of an object in the active page. This is of use only in the unusual situation when the same object appears in the active page multiple times. "Graph0#0" is equivalent to "Graph0". "Graph0#1" is the second occurrence of Graph0 in the active page.


3.	An integer object index starting from zero to get information about an object referenced by its position in the active page of the layout. Zero refers to the first object going from back to front in the page.


4.	The word "Layout" to get overall information about the layout.

### *Details* {#details}
In cases 1, 2 and 3 above, where *itemNameStr* references an object, the returned string contains the following keywords, with a semicolon after each keyword-value pair.


| Keyword | Information Following Keyword |
| --- | --- |
| NAME | Name of the object. |
| TYPE | Object type which is one of: Graph, Table, Picture, or Textbox. |
| INDEX | Object position in back-to-front order in the active page of the layout, starting from zero. |
| SELECTED | Zero if the object is not selected or nonzero if it is selected. |
| LEFT | Object left position in points. |
| TOP | Object top position in points. |
| WIDTH | Object width in points. |
| HEIGHT | Object height in points. |
| FRAME | Object frame expressed as a code usable in a ModifyLayout frame command. |
| TRANS | Object transparency expressed as a code usable in a ModifyLayout trans command. |
| FIDELITY | Object fidelity expressed as a code usable in a ModifyLayout fidelity command. |



In case 4 above, where *itemNameStr* is "Layout", the returned string contains the following keywords, with a semicolon after each keyword-value pair.


| Keyword | Information Following Keyword |
| --- | --- |
| UNITS | Units used to display object locations and sizes. This will be one of the following: 0 for points, 1 for inches, 2 for centimeters. |
| MAG | Layout magnification: .25, .5, 1.0, or 2.0. |
| BGRGB | Layout background color expressed as \<red\>,\<green\>,\<blue\> where each color is a value from 0 to 65535. |
| PAPER | Rectangle defining the bounds of the paper, expressed in points. The format is \<left\>,\<top\>,\<right\>,\<bottom\>. |
| PAGE | Rectangle defining the part of the paper that is inside the margins, expressed in points. The format is \<left\>,\<top\>,\<right\>,\<bottom\>. |
| CURRENTPAGENUM |  |
|  | One-based page number of the currently active page. |
| NUMPAGES | Total number of pages in the layout. |
| NUMOBJECTS | Total number of objects in the active page of the layout. |
| NUMSELECTED | Number of selected objects in the active page of the layout. |
| SELECTED | Comma-separated list of the names of selected objects in the active page of the layout. |



LayoutInfo returns "" in the following situations:

*winNameStr* is "" and there are no layout windows.

*winNameStr* is a name but there are no layout windows with that name.

*itemNameStr* is not "Layout" and is not the name or index of an existing object.

### *Examples* {#examples}
This example sets the background color of all selected graphs in the active page of a particular page layout to the color specified by red, green, and blue, which are numbers from 0 to 65535.


```igor
Function SetLayoutGraphsBackgroundColor(layoutName,red,green,blue)
	String layoutName	// Name of layout or "" for top layout.
	Variable red, green, blue
	
	Variable index
	String info
	Variable selected
	String indexStr
	String objectTypeStr
	String graphNameStr
	
	index = 0
	do
		sprintf indexStr, "%d", index
		info = LayoutInfo(layoutName, indexStr)
		if (strlen(info) == 0)
			break				// No more objects
		endif

		selected = NumberByKey("SELECTED", info)
		if (selected)
			objectTypeStr = StringByKey("TYPE", info)
			if (CmpStr(objectTypeStr,"Graph") == 0)	// This is a graph?
				graphNameStr = StringByKey("NAME", info)
				ModifyGraph/W=$graphNameStr wbRGB=(red,green,blue)
				ModifyGraph/W=$graphNameStr gbRGB=(red,green,blue)
			endif
		endif

		index += 1
	while(1)
End
```