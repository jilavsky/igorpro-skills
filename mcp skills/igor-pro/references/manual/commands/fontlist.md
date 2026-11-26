---
description: "The FontList function returns a list of the installed fonts, separated by the characters in separatorStr."
slug: /commands/fontlist
---

<div className="command-signature">

## <strong>FontList</strong> (<em>separatorStr</em> [, <em>options</em> ]) {#fontlist}

</div>

The FontList function returns a list of the installed fonts, separated by the characters in *separatorStr*.

### *Parameters* {#parameters}
A maximum of 10 bytes from *separatorStr* are appended to each font name as the output string is generated. *separatorStr* is usually ";".

Use *options* to limit the returned font list according to font type. It is restricted to returning only scalable fonts (TrueType, PostScript, or OpenType), which you can do with *options* = 1.

To get a list of nonscalable fonts (bitmap or raster), use:


```igor
String bitmapFontList = RemoveFromList(FontList(";",1), FontList(";"))
```

(If all fonts are scalable, bitmapFontList might be empty.)

### *Examples* {#examples}

```igor
Function SetFont(fontName)
	String fontName
	Prompt fontName, "font name:", popup, FontList(";") + "default;"
	DoPrompt "Pick a Font", fontName

	Print fontName
	
	Variable type= WinType("")                      // target window type
	String windowName= WinName(0,127)
	if( (type == 1) || (type == 3) || (type == 7) ) // graph,panel,layout
		Print "Setting drawing font for " + windowName
		Execute "SetDrawEnv fname=\"" + fontName + "\""
	else
		if( type == 5 )	// notebook
			Print "Setting font for selection in " + windowName			
			Notebook $windowName font=fontName
		endif
	endif
End
```

### *See Also* {#see-also}
[FontSizeStringWidth](/igorpro/commands/fontsizestringwidth.md), [FontSizeHeight](/igorpro/commands/fontsizeheight.md), [WinType](/igorpro/commands/wintype.md)

[Execute](/igorpro/commands/execute.md), [SetDrawEnv](/igorpro/commands/setdrawenv.md), [Notebook](/igorpro/commands/notebook.md)