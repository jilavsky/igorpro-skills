---
description: "SetScale d, num1, num2 [, unitsStr ], waveName [, waveName]... The SetScale operation sets the dimension scaling or the data full scale for the named waves."
slug: /commands/setscale
---

<div className="command-signature">

## <strong>SetScale</strong>  [/I/P] <em>dim</em>, <em>num1</em>, <em>num2</em>  [, <em>unitsStr</em> ] , <em>waveName</em> [, <em>waveName</em>]... {#setscale}

</div>

**SetScale** d, *num1*, *num2* [, *unitsStr* ] , *waveName [, waveName]*...

The SetScale operation sets the dimension scaling or the data full scale for the named waves.

### *Parameters* {#parameters}
The first parameter *dim* must be one of the following:


| Character | Signifies |
| --- | --- |
| d | Data full scale |
| t | Scaling of the chunks dimension (t scaling) |
| x | Scaling of the rows dimension (x scaling) |
| y | Scaling of the columns dimension (y scaling) |
| z | Scaling of the layers dimension (z scaling) |

If setting the scaling of any dimension (x, y, z or t), *num1* is the starting index value - the scaled index for the first point in the dimension. The meaning of *num2* changes depending on the /I and /P flags. If you use /P, then *num2* is the delta value - the difference in the scaled index from one point to the next. If you use /I, *num2* is the "ending value" - the index value for the last element in the dimension. If you use neither flag, *num2* is the "right value" - the index value that the element ***after the last element in the dimension*** would have.

These three methods are just three different ways to specify the two scaling values, the starting value and the delta value, that are stored for each dimension of each wave.

If setting the data full scale (d), then *num1* is the nominal minimum and *num2* is the nominal maximum data value for the waves. The data full scale values are not used by Igor. They serve only to document the minimum and maximum values the waves are expected to attain. No flags are used when setting the data full scale.

The *unitsStr* parameter is a string that identifies the natural units for the X or Y values of the named waves or defaults. Igor will use this to automatically label graph axes. This string must be one to 49 bytes such as "m" for meters, "g" for grams or "s" for seconds. If the waves have no natural units you, pass "" for this parameter.

Setting *unitsStr* to "dat" (case-sensitive) tells Igor that the wave is a date/time wave containing data in Igor date/time format (seconds since midnight on January 1, 1904). Date/time waves must be double-precision.

### *Flags* {#flags}
At most one flag is allowed, and then only if dimension scaling (not data full scale) is being set:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Inclusive scaling. *num2* is the ending index - the index value for the very last element in the dimension. |
| <span class="table-cell-nowrap">/P</span> | Per-point scaling. *num2* is the delta index value - the difference in scaled index value from one element to the next. |

### *Details* {#details}
SetScale will not allow the delta scaling value to be zero. If you execute a SetScale command with a delta value of zero, it will set the delta value to 1.0.

If you do not use the /P flag, SetScale converts *num1* and *num2* into a starting index value and a delta index value. If you call SetScale on a dimension with fewer than two elements, it does this conversion as if the dimension had two elements.

Prior to Igor Pro 3.0, Igor supported only 1D waves. "SetScale x" was used to set the scaling for the rows dimensions and "SetScale y" was used to set the data full scale. With the addition of multidimensional waves, "SetScale y" is now used to set the scaling of the columns dimension and "SetScale d" is used to set the data full scale. For backward compatibility, "SetScale y" on a 1D wave sets the data full scale.

When setting the dimension scaling of a numeric wave, you can omit the *unitsStr* parameter. Igor will set the wave's scaling but not change its units. However, when setting the dimension scaling of a text wave, you must supply a *unitsStr* parameter (use "" if the wave has no units). If you don't, Igor will think that the text wave is the start of a string expression and will attempt to treat it as the *unitsStr*.

### *See Also* {#see-also}
[DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), [DimSize](/igorpro/commands/dimsize.md), [WaveUnits](/igorpro/commands/waveunits.md)

For an explanation of waves and dimension scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).

For a discussion of how Igor represents dates, see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves).