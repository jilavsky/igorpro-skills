---
description: "The GBLoadWave operation loads data from a binary file into waves. For more complex applications such as loading structured data into Igor structures see the…"
slug: /commands/gbloadwave
---

<div className="command-signature">

## <strong>GBLoadWave</strong>  [<em>flags</em>] <em>fileNameStr</em> {#gbloadwave}

</div>

The GBLoadWave operation loads data from a binary file into waves.

For more complex applications such as loading structured data into Igor structures see the [FBinRead](/igorpro/commands/fbinread.md) operation.

### *Parameters* {#parameters}
If *fileNameStr*  is omitted or is "", or if the /I flag is used, GBLoadWave presents an Open File dialog from which you can choose the file to load.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Automatically assigns arbitrary wave names using "wave" as the base name. Skips names already in use. |
| <span class="table-cell-nowrap">/A = *baseName*</span> | Same as /A but it automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/B = b</span> | Tells GBLoadWave the byte order used for multi-byte data (shorts, longs, floats and doubles). |
|  |<table class="nested-table"><tbody><tr><td>b=0:</td><td>Bytes in data in high-byte-first (Motorola) format. This is the default (used if /B is omitted).</td></tr><tr><td>b=1:</td><td>Bytes in data in low-byte-first (Intel) format.</td></tr></tbody></table>
|  | Just /B is equivalent to /B=1. Do not use /B for VAX floating point. |
| <span class="table-cell-nowrap">/D = d</span> | New programming should use the /T flag instead of the /D, /L and /F flags. |
|  |<table class="nested-table"><tbody><tr><td>d=0:</td><td>Creates single-precision waves.</td></tr><tr><td>d=1:</td><td>Creates double-precision waves.</td></tr></tbody></table>
|  | /D by itself is equivalent to /D=1. |
| <span class="table-cell-nowrap">/F = f</span> | New programming should use the /T flag instead of the /D, /L and /F flags. |
|  | *f* specifies the data format of the data in the file: |
|  |<table class="nested-table"><tbody><tr><td>f=1:</td><td>Signed integer (8, 16, 32 bits allowed)</td></tr><tr><td>f=2:</td><td>Unsigned integer (8, 16, 32 bits allowed)</td></tr><tr><td>f=3:</td><td>Floating point (default, 32, 64 bits allowed)</td></tr></tbody></table>
| <span class="table-cell-nowrap">/FILT = *fileFilterStr*</span> | Provides control over the file filter menu in the Open File dialog. This flag was added in Igor Pro 7.00. |
|  | The construction of *fileFilterStr*  is the same as for the /F=*fileFilterStr*  flag of the Open operation. See [Open File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#open-file-dialog-file-filters) for details. |
| <span class="table-cell-nowrap">/I[ = {*macFilterStr* , *winFilterStr* }]</span> |  |
|  | Specifies interactive mode which displays the Open File dialog. |
|  | In Igor 7 and later, the *macFilterStr*  and *winFilterStr*  are ignored. Use the /FILT flag instead. |
| <span class="table-cell-nowrap">/J = j</span> | Specifies how input floating point data is interpreted. |
|  |<table class="nested-table"><tbody><tr><td>j=1:</td><td>IEEE floating point (default)</td></tr><tr><td>j=2:</td><td>VAX floating point</td></tr></tbody></table>
| <span class="table-cell-nowrap">/L = *length*</span> | New programming should use the /T flag instead of the /D, /L and /F flags. |
|  | *length* specifies the data length of the data in the file in bits (default = 32). Allowable data lengths are 8, 16, 32, 64. |
| <span class="table-cell-nowrap">/N</span> | Same as /A except that, instead of choosing names that are not in use, it overwrites existing waves. |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Same as /N except that Igor automatically assigns wave names of the form *baseName0*, *baseName1*. |
| <span class="table-cell-nowrap">/O = *o*</span> | Controls overwriting of waves in case of a name conflict. |
|  |<table class="nested-table"><tbody><tr><td>o=0:</td><td>Use unique wave names.</td></tr><tr><td>o=1:</td><td>Overwrite existing waves.</td></tr></tbody></table>
|  | /O by itself is equivalent to /O=1. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to look in for *fileNameStr.* *pathName*  is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Q = *q*</span> | Controls messages written to the history area of the command window. |
|  |<table class="nested-table"><tbody><tr><td>q=0:</td><td>Write messages.</td></tr><tr><td>q=1:</td><td>Suppress messages.</td></tr></tbody></table>
|  | /Q by itself is equivalent to /Q=1. |
| <span class="table-cell-nowrap">/S = *s*</span> | *s* is the number of bytes at the start of the file to skip. It defaults to 0. |
| <span class="table-cell-nowrap">/T = {*fType* , *wType* }</span> | Specifies the data type of the file (*fType* ) and the data type of the wave or waves to be created (*wType* ). The allowed codes for both *fType*  and *wType*  are: |
|  |<table class="nested-table"><tbody><tr><td>2:</td><td>Single-precision floating point</td></tr><tr><td>4:</td><td>Double-precision floating point</td></tr><tr><td>8:</td><td>8-bit signed integer</td></tr><tr><td>16:</td><td>16-bit signed integer</td></tr><tr><td>32:</td><td>32-bit signed integer</td></tr><tr><td>128:</td><td>64 bit signed integer (Igor 7 or later)</td></tr><tr><td>72:</td><td>8-bit unsigned integer (8+64)</td></tr><tr><td>80:</td><td>16-bit unsigned integer (16+64)</td></tr><tr><td>96:</td><td>32-bit unsigned integer (32+64)</td></tr><tr><td>192:</td><td>64 bit unsigned integer (128+64) (Igor 7 or later)</td></tr></tbody></table>
| <span class="table-cell-nowrap">/U = u</span> | Specifies the number of points of data per array in the file. |
|  | The default is 0 which means "auto". In this case GBLoadWave calculates the number of data points per array based on the number of bytes in the file, the number of bytes to be skipped at the start (/S flag), and the number of arrays in the file (/W flag). |
| <span class="table-cell-nowrap">/V = v</span> | Specifies interleaving of data in the file. |
|  |<table class="nested-table"><tbody><tr><td>v=0:</td><td>Data in file is not interleaved (default)</td></tr><tr><td>v=1:</td><td>Data in file is interleaved</td></tr></tbody></table>
|  | /V by itself is equivalent to /V=1. |
| <span class="table-cell-nowrap">/W = w</span> | Specifies the number of arrays in the file. The default is 1. |
|  | If you omit /W but specify the number of points per data array in the file via /U then GBLoadWave calculates the number of waves to be loaded based on the number of bytes in the file, the number of bytes to be skipped at the start (/S flag), and the specified number of points per data array in the file (/U flag). Therefore, if you specify /U and want to load just one wave you must also specify /W=1. |
| <span class="table-cell-nowrap">/Y = {*offset* , *mult* }</span> | Data loaded into waves is scaled using *offset* and *mult* : |
|  | <code class="igor">output data = (input data + offset) \* multiplier</code> |
|  | This is useful to convert integer data into scaled, real numbers. |

### *Details* {#details}
The /N flag instructs Igor to automatically name new waves "wave" (or *baseName* if /N=*baseName* is used) plus a number. The number starts from zero and increments by one for each wave loaded from the file. If the resulting name conflicts with an existing wave, the existing wave is overwritten.

The /A flag is like /N except that Igor skips names already in use.

The /T flag allows you to specify a data type for both the input (data in the file) and the output (data in the waves). You should use the /T flag instead of the /D, /L and /F flags. These flags are obsolete but are still supported.

### *GBLoadWave Open File Dialog* {#gbloadwave-open-file-dialog}
If you include the /I flag, or if the /P=*pathName* flag and the *fileNameStr* parameter do not fully specify the file to be loaded, GBLoadWave displays the Open File dialog.

The /FILT=*fileFilterStr* provides control over the file filter menu in the Open File dialog. This flag was added in Igor Pro 7.00. The construction of *fileFilterStr* is the same as for the /F=*fileFilterStr* flag of the Open operation. See [Open File Dialog File Filters](/igorpro/programming/interacting-with-the-user.md#open-file-dialog-file-filters) for details.

In Igor 7 and later, the *macFilterStr* and *winFilterStr* parameters of the /I flag are ignored. Use the /FILT flag instead.

### *Output Variables* {#output-variables}
GBLoadWave sets the following variables:

|  |  |
| --- | --- |
| V_flag | Number of waves loaded. |
| S_fileName | Name of the file being loaded. |
| S_path | File system path to the folder containing the file. |
| S_waveNames | Semicolon-separated list of the names of loaded waves. |

S_path uses Macintosh path syntax (e.g., "hd:FolderA:FolderB:"), even on Windows. It includes a trailing colon.

When GBLoadWave presents an Open File dialog and the user cancels, V_flag is set to 0 and S_fileName is set to "".

### *Examples* {#examples}

```igor
// Load 128 point single precision version 2 Igor binary wave file
GBLoadWave/S=126/U=128 "fileName"

// Load 8 256 point arrays of 16 bit signed integers into single-precision waves
// after skipping 128 byte header
GBLoadWave/S=128/T={16,2}/W=8/U=256 "fileName"

// Load n 100 point arrays of double-precision floating point numbers
// into double-precision Igor waves with names like temp0, temp1, etc,
// overwriting existing waves. n is determined by the number of bytes
// in the file.
GBLoadWave/O/N=temp/T={4,4}/U=100 "fileName"

// Load a file containing a 1024 byte header followed by a 512 row
// by 384 column array of unsigned bytes into an unsigned byte matrix
// wave and display it as an image
GBLoadWave/S=1024/T={8+64,8+64}/N=temp "fileName"
Rename temp0, image
Redimension/N=(512,384) image
if (<file uses row-major order>)
	MatrixTranspose image
endif
Display; AppendImage image
```

"Row-major order" relates to how a 2D array is stored in memory. In row-major order, all data for a given row is stored contiguously in memory. In column-major order, all data for a given column is stored contiguously in memory. Igor uses column-major order but row-major is more common.

### *See Also* {#see-also}
[Loading General Binary Files](/igorpro/data/importing-and-exporting-data.md#loading-general-binary-files)

See the [FBinRead](/igorpro/commands/fbinread.md) operation for more complex applications such as loading structured data into Igor structures.