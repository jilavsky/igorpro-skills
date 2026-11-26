---
description: "The FindSequence operation finds the location of the specified sequence starting the search from the specified start point."
slug: /commands/findsequence
---

<div className="command-signature">

## <strong>FindSequence</strong>  [/I=<em>iValueWave</em> /M=<em>match</em>  /R=<em>reverse</em>  /S=<em>start</em> /T=<em>tolerance</em> /U=<em>uValueWave</em> /V=<em>rValueWave</em> /Z] <em>srcWave</em> {#findsequence}

</div>

The FindSequence operation finds the location of the specified sequence starting the search from the specified start point. The result of the search stored in V_value is the index of the entry in the wave where the first value is found or -1 if the sequence was not found.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I = *wave*</span> | Specifies an integer sequence wave for integer search. |
| <span class="table-cell-nowrap">/M = *val*</span> | If there are repeating entries in the match sequence, *val* is a tolerance value that specifies the maximum difference between the number of repeats. So, for example, if the match sequence is aaabbccc and the *srcWave*  contains a sequence aabbcc then the sequence will not be considered a match if *val*=0 but will be considered a match if *val*=1. |
| <span class="table-cell-nowrap">/R</span> | Searches in reverse from the point in *srcWave* specified by /S or, if you omit /S, from the end of *srcWave*. /R was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/S = *start*</span> | Specifies starting point of the search. |
|  | If you omit /S, the search starts from the start of *srcWave* or, if you include /R, from the end of *srcWave*. |
| <span class="table-cell-nowrap">/T = *tolerance*</span> | Defines the tolerance (value +- *tolerance*  will be accepted) when comparing floating point numbers. |
| <span class="table-cell-nowrap">/U = *uValueWave*</span> | Specifies the match sequence wave in case of unsigned long range. |
| <span class="table-cell-nowrap">/V = *rValueWave*</span> | Specifies the match sequence wave in the case of single/double precision numbers. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
If the match sequence is specified via the /V flag, it is considered to be a floating point wave (i.e., single or double precision) in which case it is compared to data in  the wave using a tolerance value. If the tolerance is not specified by the /T flag, the default value 1.0E-7.

If the match sequence is specified via the /I flag, the sequence is assumed to be an integer wave (this includes both signed and unsigned char, signed and unsigned short as well as long). In this case srcWave must also be of integer type and the operation searches for the sequence based on exact equality between the match sequence and entries in the wave as signed long integers.

If the match sequence is unsigned long wave use the /U flag to specify the value for an integer comparison.

You can also use this operation on waves of two or more dimensions. In this case you can calculate the rows, columns, etc. For example, in the case of a 2D wave:


```igor
col=floor(V_value/rowsInWave)
row=V_value-col*rowsInWave
```

### *See Also* {#see-also}
[FindValue](/igorpro/commands/findvalue.md), [StringToUnsignedByteWave](/igorpro/commands/stringtounsignedbytewave.md)

### *Demos* {#demos}
[Open FindSequence Demo](#igor-pxp/Examples/Feature__Demos__2/SequenceSearchDemo.pxp)