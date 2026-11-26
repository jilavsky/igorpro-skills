---
description: "The WaveInfo function returns a string containing a semicolon-separated list of information about the given wave."
slug: /commands/waveinfo
---

<div className="command-signature">

## <strong>WaveInfo</strong> (<em>wave</em>, ) {#waveinfo}

</div>

The WaveInfo function returns a string containing a semicolon-separated list of information about the given wave.

The second parameter is reserved for future use and must be zero.

A null wave reference returns a zero-length string. This might be encountered, for instance, when extracting wave names from a list using the StringFromList function, when the last wave name has been extracted from the list.

### *Details* {#details}
The result string contains a list of keyword-value pairs. Each pair consists of a keyword, a colon, the value text, and a semicolon.

Here are the keywords:


| Keyword | Information Following Keyword |
| --- | --- |
| DUNITS | The wave's data units. |
| FULLSCALE | Three numbers indicating whether the wave has any data full scale information, and the min and max data full scale values. |
|  | The format of the FULLSCALE description is: |
|  | FULLSCALE:*validFS*, *minFS*, *maxFS* ; |
|  | *validFS* is 1 if *minFS* and *maxFS* have been set via a SetScale d command; otherwise it is 0. |
| LOCK | Reads back the value set by [SetWaveLock](/igorpro/commands/setwavelock.md). |
| MODIFIED | 1 if the wave has been modified since the experiment was last saved, else 0. |
| MODTIME | The date and time that the wave was last modified in seconds since January 1, 1904. |
| NUMTYPE | A number denoting the data type of the wave. |
|  | For text waves this is 0. |
|  | For wave reference waves it is 16384. |
|  | For data folder reference waves it is 256. |
|  | For numeric waves it is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Complex, added to one of the following:</td></tr><tr><td>2:</td><td>32-bit (single precision) floating point</td></tr><tr><td>4:</td><td>64-bit (double precision) floating point</td></tr><tr><td>8:</td><td>8-bit signed integer</td></tr><tr><td>16:</td><td>16-bit signed integer</td></tr><tr><td>32:</td><td>32-bit signed integer</td></tr><tr><td>64:</td><td>Unsigned, added to 8, 16, 32 or 128 if wave is unsigned</td></tr><tr><td>128:</td><td>64-bit signed integer</td></tr></tbody></table>
|  | For example, the number denoting a complex double precision wave is 5 (1+4). |
| PATH | The name of the symbolic path in which the wave file is stored (e.g., PATH:home;) or nothing if there is no path for the wave (PATH:;). |
| SIZEINBYTES | The total size of the wave in bytes. This includes the wave's header, data, note, dimension labels, and unit strings. This keyword was added in Igor Pro 7.00. |
| XUNITS | The wave's x units. |

Always pass 0 as the second input parameter. In future versions of Igor, this parameter may request other kinds of information to be returned.

A null wave reference returns a zero-length string. This might be encountered, for instance, when using [WaveRefIndexedDFR](/igorpro/commands/waverefindexeddfr.md) in a loop to act on all waves in a data folder, and the loop has incremented beyond the highest valid index.

### *Examples* {#examples}

```igor
Make/O wave1;SetScale x,0,1,"dyn",wave1;SetScale y,3,20,"v",wave1
String info = WaveInfo(wave1,0)
Print NumberByKey("NUMTYPE", info)  // Prints 2
Print StringByKey("DUNITS", info)   // Prints "v"
```

### *See Also* {#see-also}
The functions and operations listed under "About Waves" categories in the Command Help tab of the Igor Help Browser; among them are [CreationDate](/igorpro/commands/creationdate.md), [ModDate](/igorpro/commands/moddate.md), [WaveModCount](/igorpro/commands/wavemodcount.md), [WaveType](/igorpro/commands/wavetype.md), [note](/igorpro/commands/note_operation.md), and [numpnts](/igorpro/commands/numpnts.md).

WaveInfo lacks information about multidimensional waves. Individual functions are provided to return dimension-related information: [DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), [DimSize](/igorpro/commands/dimsize.md), [WaveUnits](/igorpro/commands/waveunits.md), [GetDimLabel](/igorpro/commands/getdimlabel.md).

For an explanation of waves and wave scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).