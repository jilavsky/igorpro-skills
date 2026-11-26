---
description: "The ListToTextWave function returns a free text wave containing the individual list items in listStr."
slug: /commands/listtotextwave
---

<div className="command-signature">

## <strong>ListToTextWave</strong> (<em>listStr</em>, <em>separatorStr</em> [, <em>keySepStr</em>])) {#listtotextwave}

</div>

The ListToTextWave function returns a free text wave containing the individual list items in *listStr* .

See [Free Waves](/igorpro/programming/programming.md#free-waves) for details on free waves.

The ListToTextWave function was added in Igor Pro 7.00.

The optional *keySepStr* parameter was added in Igor Pro 10.00.

### *Parameters* {#parameters}
*listStr* is a string that contains any number of substrings separated by a common string separator.

*keySepStr* is an optional key separator string that separates the key text from the value text in each list item of a keyword-value packed string. It is usually a single colon character, but can be any string. "=" and even "(x)=" are useful for parsing the results of some Igor commands like [IgorInfo](/igorpro/commands/igorinfo.md) and [GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md).

*separatorStr* is the separator string that separates one item in the list from the next. It is usually a single semicolon character but can be any string.

### *Details* {#details}
While *keySepStr* is optional, *separatorStr* is always required.

If *keySepStr* is specified (and isn't ""), the returned free wave is a two-column text wave; the keys are in column 0 and the values are in column 1. Column dimension labels of "key" and "value" are created in this case.

The ListToTextWave function returns a free wave so it can't be used on the command line or in a macro normally. If you need to convert the free wave to a global wave use [MoveWave](/igorpro/commands/movewave.md) or [Duplicate](/igorpro/commands/duplicate.md).

For lists with a large number of items, using ListToTextWave and then retrieving the substrings sequentially from the returned text wave is much faster than retrieving the substrings using StringFromList.

The reverse operation, converting the contents of a one-column text wave into a string list, can be accomplished using [wfprintf](/igorpro/commands/wfprintf.md) like this:


```igor
WAVE/T tw
String list
wfprintf list, "%s\r", tw   // Carriage-return separated list
```

### *Examples* {#examples}

```igor
Function Test(num, separator)
	Variable num
	String separator        // Usually ";"

	// Build a string list using separator
	String list = ""
	Variable i
	for(i=0; i<num; i+=1)
		list += "item_" + num2str(i) + separator
	endfor
	
	// Convert to a text wave and print its elements
	Wave/T w = ListToTextWave(list, separator)
	Print numpnts(w)
	for(i=0; i<num; i+=1)
		Print i, w[i]
	endfor
End

Macro IgorInfoExample()
	Duplicate/O ListToTextWave(IgorInfo(0), ":", ";"), W_IgorInfo
	Edit W_IgorInfo.ld
End
```

### *See Also* {#see-also}
[Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels), [FindValue](/igorpro/commands/findvalue.md), [Free Waves](/igorpro/programming/programming.md#free-waves), [ListToWaveRefWave](/igorpro/commands/listtowaverefwave.md), [MoveWave](/igorpro/commands/movewave.md), [StringFromList](/igorpro/commands/stringfromlist.md),

[Using Keyword-Value Packed Strings](/igorpro/programming/programming-techniques.md#using-keyword-value-packed-strings), [Using Strings as Lists](/igorpro/programming/programming-techniques.md#using-strings-as-lists), [WaveRefWaveToList](/igorpro/commands/waverefwavetolist.md), [wfprintf](/igorpro/commands/wfprintf.md).