---
description: "The WaveDataToString function returns a string containing an exact copy of the data from the numeric wave wave. The returned string may contain null bytes."
slug: /commands/wavedatatostring
---

<div className="command-signature">

## <strong>WaveDataToString</strong> (<em>wave</em>) {#wavedatatostring}

</div>

The WaveDataToString function returns a string containing an exact copy of the data from the numeric wave *wave*. The returned string may contain null bytes.

The WaveDataToString function was added in Igor Pro 9.00.

If *wave* has 0 points, WaveDataToString returns an empty string. If *wave* is an invalid wave reference or a non-numeric wave, the WaveDataToString returns a null string.

If the size of the data in the wave is larger than about 2<sup>31</sup> bytes, the function returns a null string because Igor strings are limited to about 2GB in size. You can determine the size of the wave's data by multiplying the number of points by the size per point (double=8 bytes/point, float=4 bytes/point, etc.). The per-point size is doubled for complex waves.

### *Parameters* {#parameters}
*wave* is a wave reference to a numeric wave.

### *Details* {#details}
Only the wave's data is present in the returned string. Other information, such as scaling, dimension labels, etc., is not included. You may need to use the Redimension operation to change the type of the wave or to perform an endian swap before you use WaveDataToString.

While Igor strings can contain embeded nulls, some parts of Igor are not prepared to handle them. For example printing a string with a null will only print the part of the string before the null. For more information, see [Embedded Nulls in Literal Strings](/igorpro/programming/commands.md#embedded-nulls-in-literal-strings).

### *Example* {#example}

```igor
Function WaveDataToStringDemo1()
	Make/FREE/B/U w1 = {49, 50, 51}
	
	// This requires Igor 9.00
	String s1 = WaveDataToString(w1)
	Print s1		// Prints 123
	
	// This approach works in older versions of Igor
	Variable np = numpnts(w1)
	String s2 = ""
	s2 = PadString(s2, np, 0)
	Variable n
	For (n=0; n < np; n++)
		s2[n,n] = num2char(w1[n])
	EndFor
	Print s2		// Prints 123
End

// Round trip using WaveDataToString and StringToUnsignedByteWave
Function WaveDataToStringDemo2()
	Make/FREE/D w2 = {1}
	String w2Str = WaveDataToString(w2)
	Print w2Str		// Prints nothing because w2Str contains leading null bytes
	Print strlen(w2Str)
	WAVE/B/U w2ByteWave = StringToUnsignedByteWave(w2Str)
	Print w2ByteWave	// Prints {0,0,0,0,0,0,240,63}
	
	// Redimension the byte wave to a double precision floating point wave
	Redimension/E=1/D/N=1 w2ByteWave
	Print w2ByteWave	// Prints {1}
End

// Generate mixed-case random letters
Function WaveDataToStringDemo3()
	Make/O/FREE/N=(1e3) letters
	MultiThread letters = trunc(abs(enoise(52)))
	
	// 0-25 uppercase, 26-51 become lowercase
	MultiThread letters = letters[p] < 26 ? letters[p] + 65 : letters[p] + 71
	Redimension/B/U letters
	
	// Create a string with all the letters.
	String lettersStr = WaveDataToString(letters)
	Print lettersStr[0,100]
End
```

### *See Also* {#see-also}
[StringToUnsignedByteWave](/igorpro/commands/stringtounsignedbytewave.md), [wfprintf](/igorpro/commands/wfprintf.md), [Working With Binary String Data](/igorpro/programming/programming-techniques.md#working-with-binary-string-data)