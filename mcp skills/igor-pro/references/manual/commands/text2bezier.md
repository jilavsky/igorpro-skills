---
description: "The Text2Bezier operation creates the data for a Bezier curve corresponding to the outline of some text using the supplied font information."
slug: /commands/text2bezier
---

<div className="command-signature">

## <strong>Text2Bezier</strong> [/O/FS=<em>fontSize</em>] <em>fontNameStr</em>, <em>fstyle</em>, <em>textStr</em>, <em>xWaveName</em>, <em>yWaveName</em> {#text2bezier}

</div>

The Text2Bezier operation creates the data for a Bezier curve corresponding to the outline of some text using the supplied font information. The output waves are formatted to be drawn using Igor's DrawBezier operation.

### *Parameters* {#parameters}
| *fontNameStr* | A string expression containing the name of a font to be used for generating outlines. |
| --- | --- |
| *fstyle* | *fstyle* is a bitwise parameter with each bit controlling one aspect of the font style as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Bold</td></tr><tr><td>Bit&nbsp;1:</td><td>Italic</td></tr><tr><td>Bit&nbsp;2:</td><td>Underline</td></tr><tr><td>Bit&nbsp;4:</td><td>Strikethrough</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| *textStr* | A string expression containing the text to be transformed into Bezier outlines. |
| *xWaveName* | Specifies X output wave to receive the Bezier curve data. |
| *yWaveName* | Specifies Y output wave to receive the Bezier curve data. |

### *Flags* {#flags}
|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FS = fs</span> | *fs* is the font size to apply while generating the outlines. Without this flag, glyphs are scaled to unit size. The scaling parameters for DrawBezier are limited to a maximum of 20, so you will probably need to use this flag if you want very large text. |
| <span class="table-cell-nowrap">/O</span> | Allow overwriting the output waves. |

### *Details* {#details}

To draw the text outline, pass the output waves from Text2Bezier to the DrawBezier operation. The coordinates are such that the DrawBezier origin will be the left baseline of the text. In most cases you will want to use the SetDrawEnv operation to set the coordinate system to absolute. If you wish to fill the text with color or gradient, you will need to use the SetDrawEnv subpaths keyword.

### *Output Variables* {#output-variables}
| V_Flag | 0 for success, 1 for general failure, 2 for extraction failure. |
| --- | --- |

### *Examples* {#examples}

```igor
// Extract text to Bezier data
Text2Bezier/O/FS=20 "Helvetica", 0, "Text2Bezier", textx, texty

// Draw outline in a graph window with no fill
Display /W=(100,100,700,450)
SetDrawLayer UserFront
SetDrawEnv fillpat=0,xcoord= abs,ycoord= abs	// fillpat=0 specifies no fill
DrawBezier 100,100,1,1,textx,texty

// Draw outline three times larger and filled with a gradient shading
// subpaths=1 draws the entire Bezier as a series of subpaths for correct filling
SetDrawEnv xcoord= abs,ycoord= abs,subpaths= 1,gradient= {0, 0, 0, 1, 0, (65535,65535,0), (65535,0,0)}
DrawBezier 100,150,3,3,textx,texty
```

### *See Also* {#see-also}
[DrawBezier](/igorpro/commands/drawbezier.md), [SetDrawEnv](/igorpro/commands/setdrawenv.md)