---
description: "The FontSizeStringWidth function returns the width of theStr in pixels, when rendered with the named font and the given font style and size."
slug: /commands/fontsizestringwidth
---

<div className="command-signature">

## <strong>FontSizeStringWidth</strong> (<em>fontNameStr</em>, <em>fontSize</em>, <em>fontstyle</em>, <em>theStr</em> [,<em>appearanceStr</em>]) {#fontsizestringwidth}

</div>

The FontSizeStringWidth function returns the width of *theStr* in pixels, when rendered with the named font and the given font style and size.

### *Parameters* {#parameters}
*fontNameStr* is the name of the font, such as "Helvetica".

*fontSize* is the size (height) of the font in pixels.

*fontStyle* is text style (bold, italic, etc.). Use 0 for plain text.

*theStr* is the string whose width is being measured.

The optional *appearanceStr* parameter is no longer used and has no effect.

Usually you will want to set *appearanceStr* to the S_Value output of [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md)/W=*winName* when determining the width of a string drawn by a control.

### *Details* {#details}
If the named font is not installed, FontSizeStringWidth returns NaN.

FontSizeStringWidth understands "default" to mean the current experiment's default font.

*FontSize* is in pixels. To obtain the width of a font specified in points, use the [ScreenResolution](/igorpro/commands/screenresolution.md) function and the conversion factor of 72 points per inch (see Examples).

*fontStyle* is a binary coded integer with each bit controlling one aspect of the text style as follows:

|  |  |
| --- | --- |
| Bit 0: | Bold |
| Bit 1: | Italic |
| Bit 2: | Underline |
| Bit 4: | Strikethrough |

To set bit 0 and bit 2 (bold, underline), use 2<sup>0</sup>+2<sup>2</sup> = 1+4 = 5 for *fontStyle*. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.


```igor
Example 1
Variable fsPix= 10 * ScreenResolution/72    // 10 point text in pixels
String text= "How long is this text?"
Variable WidthPix= FontSizeStringWidth("Helvetica",fsPix,0,text)
Print "width in inches= ", WidthPix / ScreenResolution
```

### *Example 2* {#example-2}

```igor
Variable fsPix= 13 * ScreenResolution/72    // 13 point text in pixels
String text= "text for a control"
DefaultGUIControls/W=Panel0                 // Sets S_Value
Variable WidthPix= FontSizeStringWidth("Helvetica",fsPix,0,text,S_Value)
Print "width in points= ", WidthPix / ScreenResolution * 72
```

### *See Also* {#see-also}
[FontList](/igorpro/commands/fontlist.md), [FontSizeHeight](/igorpro/commands/fontsizeheight.md), [ScreenResolution](/igorpro/commands/screenresolution.md), [DefaultGUIControls](/igorpro/commands/defaultguicontrols.md)