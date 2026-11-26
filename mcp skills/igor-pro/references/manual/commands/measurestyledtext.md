---
description: "The MeasureStyledText operation takes as input a string optionally containing style codes such as are used in graph annotations and the DrawText operation."
slug: /commands/measurestyledtext
---

<div className="command-signature">

## <strong>MeasureStyledText</strong>  [/W=<em>winName</em> /A=<em>axisName</em> /B=<em>baselineMode</em> /F=<em>fontName</em> /SIZE=<em>fontSize</em> /STYL=<em>fontStyle</em>] [<em>styledTextStr</em>] {#measurestyledtext}

</div>

The MeasureStyledText operation takes as input a string optionally containing style codes such as are used in graph annotations and the [DrawText](/igorpro/commands/drawtext.md) operation. It sets various variables with information about the dimensions of the string.

In Igor Pro 9.00, the *styledTextStr* parameter was made optional, the /B flag was added, and several output variables (all but V_width and V_height) were added.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Takes default text information from the window *winName*. |
|  | If you omit /W, MeasureStyledText works on the top graph window. |
| <span class="table-cell-nowrap">/A = *axisName*</span> | Takes default text information from the axis named *axisName* in the top graph or in the graph window specified by /W. |
| <span class="table-cell-nowrap">/B = *baselineMode*</span> | Selects which line's baseline offset is returned in V_baseline if the text contains multiple lines (separated by carriage-return). |
|  | If you omit /B or specify /B=0, V_baseline is set to the offset to the last line of the text. |
|  | If you specify /B=1, V_baseline is set to the offset to the first line of the text. |
|  | The /B flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/F = *fontNameStr*</span> | The name of the default font. |
|  | In Igor Pro 9.00 and later, /F="default" and /F="" are the same as omitting /F in which case the default font is defined by /W, /A, or by the overall default font specified by the [DefaultFont](/igorpro/commands/defaultfont.md) operation. |
| <span class="table-cell-nowrap">/SIZE = *size*</span> | Sets default font size. |
| <span class="table-cell-nowrap">/STYL = *fontStyle*</span> | Sets default font style: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | /STYLE=0 specifies plain text. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |

### *Parameters* {#parameters}
*styledTextStr* is the styled text to be measured.

In Igor Pro 9.00, *styledTextStr* is an optional parameter. Previously it was required.

If you include *styledTextStr*, the default font and styled text output variables are set.

If you omit *styledTextStr*, only the default font output variables are set.

See ***Default Font Output Variables*** and ***Styled Text Output Variables*** below.

*styledTextStr* can contain escape codes to set the font, size, style, color and other properties. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. The text may contain multiple lines separated with carriage returns ("\r").

### *Details* {#details}
In the absence of formatting codes within the text that set the font, font size and font style, some mechanism must be provided that sets them.

The /W flag tells MeasureStyledText to get the default font name and font size from the specified window. If /W is omitted, defaults come from the top graph window.

The /A flag specifies that the default font name and font size come from the specified axis in the graph window specified by /W or in the top graph if /W is omitted.

The /F, /SIZE and /STYL flags set defaults that override any defaults from a window or axis. If you don't use any flags, the defaults are Igor's overall defaults.

If you omit all flags, the font specified by the [DefaultFont](/igorpro/commands/defaultfont.md) operation is used, the default font size is 12 points, and the style is plain.

### *Default Font Output Variables* {#default-font-output-variables}
In the descriptions of these variables, "default font" refers to the font, size, and style defined by /W, /A, /SIZE, and /STYLE, and not any escape codes in *styledTextStr*.

MeasureStyledText returns information about the default font via the following output variables:


|  |  |
| --- | --- |
| S_font | The name of the default font (before escape codes in *styledTextStr* take effect). If a substitute font would be used, the name of the substitute font is returned. |
| V_ascent | Height above the baseline of the default font. This will include some blank space above even the tallest characters. |
| V_descent | Height below the baseline of the default font. |
| V_fontSize | The default font size in points. |
| V_fontStyle | The default font style. |
| V_subscriptExtraHeight | Extra height needed to accomodate any subscript when using the default font. |
| V_superscriptExtraHeight |  |
|  | Extra height needed to accomodate any superscript when using the default font. |

### *Styled Text Output Variables* {#styled-text-output-variables}
MeasureStyledText returns information about the styled text via the following output variables:


|  |  |
| --- | --- |
| V_height | The total height of the styled text in points. |
| V_width | The total width of the styled text in points. |
| V_baseline | The offset to the baseline of the styled text in points, as measured from the bottom of the text. |
|  | If you omit /B or specify /B=0, this is is the offset to the last line's baseline. |
|  | If you omit /B or specify /B=1, this is is the offset to the first line's baseline. |

### *MeasureStyledText Diagrams* {#measurestyledtext-diagrams}

|  |
| --- |
| These diagrams illustrate the meanings of the various output variables: |
| <img src="Images/MeasureStyledText/MeasureStyledText_0.png" width="50%"/> |
| <img src="Images/MeasureStyledText/MeasureStyledText_1.png" width="50%"/> |

### *Example* {#example}

```igor
Menu "Macros"
	"Demo MeasureStyledText", DemoMeasureStyledText()
End

Function/S GetExampleTextDialog()
	String textStr = ""
	String menuItemList = ""
	menuItemList += "Example Text;"
	menuItemList += "Example Text\\B2;"
	menuItemList += "Example Text\\S2;"
	menuItemList += "Example\\B2\\M Text\\S2;"
	menuItemList += "Example\\S[1]\\M<CR>Text\\B2;"
	Prompt textStr, "Example Text:", popup, menuItemList
	DoPrompt "Choose Example Text", textStr
	if (V_Flag)
		return ""			// User canceled
	endif
	return textStr
End

Function DemoMeasureStyledText()
	String textStr = GetExampleTextDialog()
	if (strlen(textStr) == 0)
		return -1			// User canceled
	endif
	textStr = ReplaceString("<CR>", textStr, "\r")
	
	DoWindow/K ExampleGraph
	Display/N=ExampleGraph/W=(50,50,50+250,50+150)
	ModifyGraph/W=ExampleGraph gbRGB=(65535,65534,49151) 		// Light yellow background
	ModifyGraph/W=ExampleGraph expand=3
	SetDrawEnv/W=ExampleGraph xcoord=abs, ycoord=abs, save 	// Points
	MeasureStyledText/W=ExampleGraph/F="Courier New"/SIZE=20/STYL=1 textStr
	Variable x0=50, y0=80 	// Text is bottom-aligned and left-aligned to this point
	DrawRect/W=ExampleGraph x0, y0, x0+V_width, y0-V_height 	// Opaque background
	SetDrawEnv/W=ExampleGraph fname="Courier New", fsize=20, fstyle=1 // Bold
	DrawText/W=ExampleGraph x0, y0, textStr 			// Text on top

	// Draw a baseline
	Variable baseline = y0-V_baseline
	SetDrawEnv/W=ExampleGraph linefgc=(16385,28398,65535, 40000) // Translucent blue
	DrawLine/W=ExampleGraph x0, baseline, x0+V_width, baseline
	
	// Print output variables
	Printf "S_font=\"%s\", V_fontSize=%g, V_fontStyle=%g\r", S_font, V_fontSize, V_fontStyle
	Printf "V_width=%g, V_height=%g\r", V_width, V_height
	Printf "V_baseline=%g, V_ascent=%g, V_descent=%g\r", V_baseline, V_ascent, V_descent
	Printf "V_subscriptExtraHeight=%g, V_superscriptExtraHeight=%g\r", V_subscriptExtraHeight, V_superscriptExtraHeight
	
	return 0
End
```

### *See Also* {#see-also}
[Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for a list of text formatting codes.

[DefaultFont](/igorpro/commands/defaultfont.md)