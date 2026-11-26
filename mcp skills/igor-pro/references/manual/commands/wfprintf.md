---
description: "The wfprintf operation is like the printf operation, except that it prints the contents of the named waves to a file whose file reference number is in refNum."
slug: /commands/wfprintf
---

<div className="command-signature">

## <strong>wfprintf</strong>  <em>refNumOrStr</em>, <em>formatStr</em> [/R=(<em>startX</em>, <em>endX</em> )] <em>waveName</em>  [, <em>waveName</em> ]... {#wfprintf}

</div>

The wfprintf operation is like the [printf](/igorpro/commands/printf.md) operation, except that it prints the contents of the named waves to a file whose file reference number is in *refNum*.

The [Save](/igorpro/commands/save.md) operation also outputs wave data to a text file. Use Save unless you need the added flexibility provided by wfprintf.

### *Parameters* {#parameters}
*refNumOrStr* is a numeric expression, a string variable name or an SVAR pointing to a global string variable.

If a numeric expression, then it is a file reference number returned by the [Open](/igorpro/commands/open.md) operation or an expression that evaluates to 1.

If *refNumOrStr* is 1, Igor prints to the history area instead of to a file.

If *refNumOrStr* is the name of a string variable, the wave contents are "printed" to the named string variable. *refNumOrStr* can also be the name of an SVAR to print to a global string:


```igor
SVAR sv = root:globalString
wfprintf sv, "", wave0
```

*refNumOrStr* cannot be an element of a text wave.

The value of each named wave is printed to the file according to the conversion specified in *formatStr*.

*formatStr* contains one numeric conversion specification per column. See printf. If *formatStr* is "", wfprintf uses a default format which gives tab-delimited columns.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/R = (*startX*, *endX*)</span> | Specifies an X range in the wave(s) to print. |
| <span class="table-cell-nowrap">/R = [*startP*, *endP*]</span> | Specifies a point range in the wave(s) to print. |

:::note
/R must follow the formatStr parameter directly without an intervening comma.
:::


### *Details* {#details}
As of Igor 7, wfprintf supports 1D and 2D waves. Previously it supported 1D waves only.

The number of conversion characters in *formatStr* must exactly match the number of wave columns in all input waves. With real waves, the total number of columns is limited to 100. With complex waves, the real column and imaginary column each count as a column and the total number of columns is limited to 200.

The only conversion characters allowed are fFeEgdouxXcs (the floating point, integer and string conversion characters). The use of the asterisk to specify field width or precision is not allowed. If any of these restrictions is intolerable, you can write your wave output using fprintf in a loop.

With integer conversion specifications d, o, u, x, and X, applied to floating point waves, wfprintf rounds the fractional part.

In Igor Pro 9.00 and or later, there is no limit to the length of an element of a text wave parameter passed to the wfprintf operation. Previously text wave element contents were clipped to about 500 bytes. There is also no limit to the length of *formatStr*. Previously it was limited to 800 bytes.

### *Examples* {#examples}

```igor
Function Example1()
	Make/O/N=10 wave0=sin(p*pi/10)                          // test numeric wave
	Make/O/N=10/T textWave= "row "+num2istr(p)              // test text wave
	Variable refNum
	Open/P=home refNum as "output.txt"                      // open file for write
	wfprintf refNum, "%s = %g\r"/R=[0,5], textWave, wave0   // print 6 values each
	Close refNum
End
```

The resulting output.txt file contains:


```igor
row 0 = 0
row 1 = 0.309017
row 2 = 0.587785
row 3 = 0.809017
row 4 = 0.951057
row 5 = 1

Function/S NumericWaveToStringList(w)
	Wave w	// numeric wave (if text, use /T here and %s below)
	String list
	wfprintf list, "%g;", w	// semicolon-separated list
	return list
End
Print NumericWaveToStringList(wave0)
  0;0.309017;0.587785;0.809017;0.951057;1;0.951057;0.809017;0.587785;0.309017;
```

### *See Also* {#see-also}
The [printf](/igorpro/commands/printf.md) operation for complete format and parameter descriptions and [Creating Formatted Text](/igorpro/advanced-topics.md#creating-formatted-text) in the Advanced Topics help file.

[Open](/igorpro/commands/open.md) about *refNum*, [fprintf](/igorpro/commands/fprintf.md), and [Save](/igorpro/commands/save.md) operations. See [Open](/igorpro/commands/open.md) for another way of writing wave files.