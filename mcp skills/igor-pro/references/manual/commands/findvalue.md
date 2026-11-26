---
description: "The FindValue operation finds the location of the specified value starting the search from the specified start point."
slug: /commands/findvalue
---

<div className="command-signature overload">

## <strong>FindValue</strong>  [/I=<em>iValue</em> /S=<em>start</em> /T=<em>tolerance</em> /U=<em>uValue</em> /V=<em>rValue</em> /Z] <em>srcWave</em> {#findvalue}

</div>
<div className="command-signature">

## <strong>FindValue</strong>  [/S=<em>start</em> /TEXT=<em>templateString</em>/TXOP=<em>txOptions</em> /Z] <em>txtWave</em> {#findvalue}

</div>

The FindValue operation finds the location of the specified value starting the search from the specified start point. It stores the results of the search in the variables V_value,V_row, V_col, V_layer, and V_chunk.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = *cvalue*</span> | Specifies searching for a complex value *cvalue* provided by a local or global complex variable. For example: |
|  | <code class="igor">Variable /C c0=cmplx(1,2)&#10;FindValue/C=c0 srcWave</code> |
| <span class="table-cell-nowrap">/FNAN</span> | Specifies searching for a NaN value when *srcWave*  is floating point. |
|  | The /FNAN flag was added in Igor Pro 7.00. |
| <span class="table-cell-nowrap">/I = *ivalue*</span> | Specifies an integer value for integer search. |
| <span class="table-cell-nowrap">/R</span> | Reverses the order of the search. |
|  | In the absence of /S and /RMD, the search starts from the end of the wave. |
|  | /R is not compatible with /UOFV. |
|  | The /R flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/RMD = [*firstRow*, *lastRow*][*firstColumn* , *lastColumn*][*firstLayer*, *lastLayer*][*firstChunk*, *lastChunk*]</span> |  |
|  | Designates a contiguous range of data in the source wave to which the operation is to be applied. This flag was added in Igor Pro 8.00. |
|  | You can include all higher dimensions by leaving off the corresponding brackets. For example: |
|  | <code class="igor">/RMD=[firstRow,lastRow]</code> |
|  | includes all available columns, layers and chunks. |
|  | You can use empty brackets to include all of a given dimension. For example: |
|  | <code class="igor">/RMD=[][firstColumn,lastColumn]</code> |
|  | means "all rows from firstColumn to lastColumn". |
|  | You can use a * to specify the end of any dimension. For example: |
|  | <code class="igor">/RMD=[firstRow,\*]</code> |
|  | means "from firstRow through the last row". |
| <span class="table-cell-nowrap">/S = *start*</span> | Where to start the search in the wave. If /S is not specified, start is set to 0. |
| <span class="table-cell-nowrap">/T = *tolerance*</span> | Use this flag when comparing floating point numbers to define a non-negative tolerance such that the specified value +/- tolerance will be accepted. |
| <span class="table-cell-nowrap">/TEXT = *templateString*</span> |  |
|  | Use this flag to specify a template string that will be searched for in *txtWave*. |
| <span class="table-cell-nowrap">/TXOP = *txOptions*</span> |  |
|  | Specifies the search options using a combination of binary values |
|  |<table class="nested-table"><tbody><tr><td>**txOptions**</td><td>**search type**</td></tr><tr><td>1</td><td>case sensitive</td></tr><tr><td>2</td><td>whole word</td></tr><tr><td>4</td><td>whole wave element</td></tr></tbody></table>
| <span class="table-cell-nowrap">/U = *uValue*</span> | Specifies the match value in case of unsigned long range. |
| <span class="table-cell-nowrap">/UOFV</span> | The /UOFV (unordered find value) flag, which was added in Igor Pro 8.00, runs the search using multiple threads with each thread searching a different section of the wave. The search terminates when any thread finds a matching value. |
|  | Use /UOFV when you need the fastest result and you do not care if it finds the first matching value in the wave or a subsequent matching value. |
|  | By default /UOFV is ignored if *srcWave* contains fewer than 2,000 points. You can modify this value using [MultiThreadingControl](/igorpro/commands/multithreadingcontrol.md). /UOFV is also ignored if you use the /RMD flag. |
| <span class="table-cell-nowrap">/V = *rValue*</span> | Specifies the match value in the case of single/double precision numbers. For most purposes you should also use /T to specify the tolerance. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
If the match value is specified via the /V flag, it is considered to be a floating point value in which case it is compared to data in the wave using a tolerance value. If the tolerance is not specified by the /T flag, the value 1.0E-7 is used.

If the match value is specified via the /I flag, the value is assumed to be an integer. In this case srcWave must be of integer type and the operation searches for the value based on exact equality between the match value and entries in the wave as signed long integers.

If the match value is unsigned long use the /U flag to specify the value for an integer comparison.

The result of the search is stored in the output variables V_value, V_row, V_col, V_layer, and V_chunk. V_value is set to to the index in *srcWave*, treating it as 1D regardless of its dimensionality, where the searched value was found or to -1 if it was not found. V_row, V_col, V_layer, and V_chunk are set to the row, column, layer, and chunk number where the searched value was found or to -1 if it was not but the latter three are set to NaN if the corresponding dimension does not exist in *srcWave*.

When searching for text in a text wave the operation creates the variable V_value as above but it also creates the variable V_startPos to specify the position of *templateString* from the start of the particular wave element.

### *Example* {#example}

```igor
Make jack = sin(x/8)	// Single-precision floating point
Display jack

// This prints -1 because 0.5 +/- 1.0E-7 does not occur in wave jack
FindValue /V=.5 jack; Print V_value

// This prints 21 because 0.5 +/- 0.01 does occur in wave jack
FindValue /V=.5 /T=.01 jack; Print V_value

// The value of jack(21), to 6 decimal digits of precision, is 0.493920
Print jack(21)

// This finds the row of the keyword "BUILD" in column 0, and prints the value from column 1.
WAVE/T keysAndValues = ListToTextWave(IgorInfo(0), ":", ";") // keys in column 0. Requires Igor 10.
FindValue/Z/TEXT="BUILD" /RMD=[][0,0] keysAndValues
Print "Igor Build Number is " + keysAndValues[V_row][1]
```

### *See Also* {#see-also}
[FindSequence](/igorpro/commands/findsequence.md), [FindLevel](/igorpro/commands/findlevel.md), [FindLevels](/igorpro/commands/findlevels.md), [FindDuplicates](/igorpro/commands/findduplicates.md)