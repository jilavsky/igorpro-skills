---
description: "The FontSizeHeight function returns the line height in pixels of any string when rendered with the named font and the given font style and size."
slug: /commands/fontsizeheight
---

<div className="command-signature">

## <strong>FontSizeHeight</strong> (<em>fontNameStr</em>, <em>fontSize</em>, <em>fontstyle</em> [,<em>appearanceStr</em> ] ) {#fontsizeheight}

</div>

The FontSizeHeight function returns the line height in pixels of any string when rendered with the named font and the given font style and size.

### *Parameters* {#parameters}
*fontNameStr* is the name of the font, such as "Helvetica".

*fontSize* is the size (height) of the font in pixels.

*fontStyle* is text style (bold, italic, etc.). Use 0 for plain text.

### *Details* {#details}
The returned height is the sum of the font's ascent and descent heights. Variations in *fontStyle* and typeface design cause the actual font height to be different than *fontSize* would indicate. (Typically a font "height" refers to only the ascent height, so the total height will be slightly larger to accommodate letters that descend below the baseline, such as g, p, q, and y).

*FontSize* is in pixels. To obtain the height of a font specified in points, use the [ScreenResolution](/igorpro/commands/screenresolution.md) function and the conversion factor of 72 points per inch (see Examples).

If the named font is not installed, FontSizeHeight returns NaN.

FontSizeHeight understands "default" to mean the current experiment's default font.

*fontStyle* is a binary coded integer with each bit controlling one aspect of the text style as follows:

|  |  |
| --- | --- |
| Bit 0: | Bold |
| Bit 1: | Italic |
| Bit 2: | Underline |
| Bit 4: | Strikethrough |

To set bit 0 and bit 2 (bold, underline), use 2<sup>0</sup>+2<sup>2</sup> = 1+4 = 5 for *fontStyle*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

The optional *appearanceStr* parameter is no longer used and has no effect.

### *Examples* {#examples}

```igor
Variable pixels= 12 * ScreenResolution/72	// convert 12 points to pixels
Variable pixelHeight= FontSizeHeight("Helvetica",pixels,0)
Print "Height in points= ", pixelHeight * 72/ScreenResolution

Function FontIsInstalled(fontName)
	String fontName
	if( numtype(FontSizeHeight(fontName,10,0)) == 2 )
		return 0	// NaN returned, font not installed
	else
		return 1
	endif
End
```



### *See Also* {#see-also}
[FontList](/igorpro/commands/fontlist.md), [FontSizeStringWidth](/igorpro/commands/fontsizestringwidth.md), [numtype](/igorpro/commands/numtype.md), [ScreenResolution](/igorpro/commands/screenresolution.md), [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md)