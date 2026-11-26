---
description: "The StringToUnsignedByteWave function returns a free unsigned byte wave containing the contents of str."
slug: /commands/stringtounsignedbytewave
---

<div className="command-signature">

## <strong>StringToUnsignedByteWave</strong> (<em>str</em>) {#stringtounsignedbytewave}

</div>

The StringToUnsignedByteWave function returns a free unsigned byte wave containing the contents of *str*.

If *str* is an empty string, a zero point wave is returned. If *str* is null, a null wave reference is returned.

The StringToUnsignedByteWave function was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*str* is a string.

### *Details* {#details}
The StringToUnsignedByteWave function returns a free wave so it can't be used on the command line or in a macro. If you need to convert the free wave to a global wave use [MoveWave](/igorpro/commands/movewave.md).

Using StringToUnsignedByteWave makes it possible to use commands that work on waves to manipulate the data originally stored in a string. This can be faster and more convenient than manipulating the data directly in the string. If necessary, you can create a string containing the manipulated data using [WaveDataToString](/igorpro/commands/wavedatatostring.md).

StringToUnsignedByteWave stores each byte of *str* in an element of the output wave. It does not do ASCII-to-binary conversion. For example, if str contains "123", it returns an unsigned binary wave containing three elements with values 49, 50, and 51 (0x31, 0x32, and 0x33). It does not return the numeric value 123.

### *Example* {#example}

```igor
Function DemoStringToUnsignedByteWave()
	String theStr = "123"
	
	// This requires Igor 9.00
	WAVE/B/U w1 = StringToUnsignedByteWave(theStr)
	Print w1
	
	// This works in older versions of Igor
	Variable len = strlen(theStr)
	Make/B/U/FREE/N=(len) w1
	w1 = char2num(theStr[p])
	Print w1
End
```

### *See Also* {#see-also}
[WaveDataToString](/igorpro/commands/wavedatatostring.md), [MoveWave](/igorpro/commands/movewave.md), [Free Waves](/igorpro/programming/programming.md#free-waves), [Working With Binary String Data](/igorpro/programming/programming-techniques.md#working-with-binary-string-data)