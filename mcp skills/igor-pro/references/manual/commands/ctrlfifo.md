---
description: "The CtrlFIFO operation controls various aspects of the named FIFO. Once start has been issued, the FIFO can accept no further commands except stop."
slug: /commands/ctrlfifo
---

<div className="command-signature">

## <strong>CtrlFIFO</strong>  <em>FIFOName</em>, [<em>deltaT</em>=<em>dt</em>, <em>note</em>=<em>noteStr</em>, <em>file</em>=<em>oRefNum</em>, <em>rfile</em>=<em>rRefNum</em>, <em>rdfile</em>=<em>rRefNum</em>, <em>doffset</em>=<em>dataOffset</em>, <em>dsize</em>=<em>dataSize</em>, <em>swap</em>, <em>size</em>=<em>s</em>, <em>start</em>, <em>stop</em>, <em>close</em>, <em>flush</em>] {#ctrlfifo}

</div>

The CtrlFIFO operation controls various aspects of the named FIFO.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| close | Closes the FIFO's output or review file (if any). |
| <span class="table-cell-nowrap">deltaT = *dt*</span> | Documents the data acquisition rate. |
| <span class="table-cell-nowrap">doffset = *dataOffset*</span> | Used only with rdfile. Offset to data. If not provided offset is zero. |
| <span class="table-cell-nowrap">dsize = *dataSize*</span> | Used only with rdfile. Size of data in bytes. If not provided, then data size is assumed to be the remainder of file. If this assumption is not valid then unexpected results may be observed. |
| flush | New data in FIFO is flushed to disk immediately. |
| <span class="table-cell-nowrap">file = *oRefNum*</span> | The file reference number for the FIFO's output file. You obtain this reference number from the Open operation used to create the file. |
| <span class="table-cell-nowrap">note = *noteStr*</span> | Stores the note string in the file header. It is limited to 255 bytes. |
| <span class="table-cell-nowrap">rfile = *rRefNum*</span> | The file reference number for the FIFO's review file. You use a review file when you are using a FIFO to review existing data. You obtain the reference number from the Open/R operation used to open the file. File may be either unified header/data or a split format where the header contains the name of a file containing the raw data. |
| <span class="table-cell-nowrap">rdfile = *rRefNum*</span> | Like rfile but for review of raw data (use Open/R command). Channel data must match raw data in file. Offset from start of file to start of data can be provided using doffset given in same command. If data does not extend all the way to the end of the file, then the number of bytes of data can be provided using dsize in the same command. |
| <span class="table-cell-nowrap">size = *s*</span> | Sets number of chunks in the FIFO. The default is 10000. A chunk of data consists of a single data point from each of the FIFO's channels. |
| start | Starts the FIFO running by setting the time/date info fields in the FIFO header, writing the header to the output file and marking the FIFO as active. |
| stop | Stops the FIFO by flushing data to disk and marking the FIFO as inactive. |
| swap | Used only with rdfile. Indicates that the raw data file requires byte-swapping when it is read. This would be the case if you are running on a Mac, reading a binary file from a PC, or vice-versa. |

### *Details* {#details}
Once start has been issued, the FIFO can accept no further commands except stop.

The FIFO must be in the valid state for you to access its data (using a chart control or using the FIFO2Wave operation). When you create a FIFO, using NewFIFO, it is initially invalid. It becomes valid when you issue the start command via the CtrlFIFO operation. It remains valid until you change a FIFO parameter using CtrlFIFO.

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts), [Open](/igorpro/commands/open.md)