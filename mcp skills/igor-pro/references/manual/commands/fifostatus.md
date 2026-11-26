---
description: "The FIFOStatus operation returns miscellaneous information about a FIFO and its channels. FIFOs are used for data acquisition."
slug: /commands/fifostatus
---

<div className="command-signature">

## <strong>FIFOStatus</strong>  [/Q] <em>FIFOName</em> {#fifostatus}

</div>

The FIFOStatus operation returns miscellaneous information about a FIFO and its channels. FIFOs are used for data acquisition.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Doesn't print the S_Info string in the history area. |

### *Details* {#details}
FIFOStatus sets the variable V_flag to nonzero if a FIFO of the given name exists. If the named FIFO does exist then FIFOStatus stores information about the FIFO in the following variables:


|  |  |
| --- | --- |
| V_FIFORunning | Nonzero if FIFO is running. |
| V_FIFOChunks | Number of chunks of data placed in FIFO so far. |
| V_FIFOnchans | Number of channels in the FIFO. |
| S_Info | Keyword-packed information string. |

The keyword-packed information string consists of a sequence of sections with the following form: *keyword*:*value*;

You can pick a value out of a keyword-packed string using the [NumberByKey](/igorpro/commands/numberbykey.md) and [StringByKey](/igorpro/commands/stringbykey.md) functions. Here are the keywords for S_Info:


| Keyword | Type | Meaning |
| --- | --- | --- |
| DATE | Number | Date/time when start was issued via CtrlFIFO. |
| DELTAT | Number | FIFO's deltaT value as set by CtrlFIFO. |
| DISKTOT | Number | Current number of chunks written to the FIFO's file. |
| FILENUM | Number | Output file refNum or review file refNum as set by CtrlFIFO. This will be zero if the FIFO is connected to no file. |
| NOTE | String | FIFO's note string as set by CtrlFIFO. |
| VALID | Number | Zero if FIFO is not valid. |
| DATATYPE | Number | Channel's data type as if set by [NewFIFOCHAN](/igorpro/commands/newfifochan.md)/Y=(*numType*), where *numType* is a value as returned by the [WaveType](/igorpro/commands/wavetype.md) function. |

In addition, FIFOStatus writes fields to S_Info for each channel in the FIFO. The keyword for the field is a combination of a name and a number that identify the field and the channel to which it refers. For example, if channel 4 is named "Pressure" then the following would appear in the S_Info string: NAME4:Pressure.

In the following table, the channel's number is represented by #.


| Keyword | Type | Meaning |
| --- | --- | --- |
| FSMINUS# | number | Channel's minus full scale value as set by NewFIFOChan. |
| FSPLUS# | number | Channel's plus full scale value as set by NewFIFOChan. |
| GAIN# | number | Channel's gain value as set by NewFIFOChan. |
| NAME# | string | Name of channel. |
| OFFSET# | number | Channel's offset value as set by [NewFIFOChan](/igorpro/commands/newfifochan.md). |
| UNITS# | string | Channel's units as set by NewFIFOChan. |



### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)

[NumberByKey](/igorpro/commands/numberbykey.md), [StringByKey](/igorpro/commands/stringbykey.md)