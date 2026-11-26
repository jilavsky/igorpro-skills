---
description: "The HDF5Dump operation dumps information about the specified HDF5 file."
slug: /commands/hdf5dump
---

<div className="command-signature">

## <strong>HDF5Dump</strong>  [ [ /A[=<em>attributeNameStr</em> ] /ATTR=<em>dumpAttributes</em> /D=<em>datasetNameStr</em> /G=<em>groupNameStr</em> /H=<em>dumpHeaderOnly</em> /I=<em>dumpObjectIDs</em> /L=<em>linkNameStr</em> /Q /P=<em>pathName</em> /PROP=<em>dumpProperties</em> /R=<em>dumpAsASCII</em> /T=<em>datatypeNameStr</em> /TIME=<em>timeInSeconds</em> /W=<em>widthInColumns</em> /Z ] <em>fileNameStr</em> {#hdf5dump}

</div>

The HDF5Dump operation dumps information about the specified HDF5 file. The information is dumped into the string variable S_HDF5Dump or into the history area, depending on the /OUT flag.

This operation exists mainly for the use of the HDF5 Browser and is of little use otherwise except possibly for an advanced user.

HDF5Dump is based on the H5Dump command line tool from The HDF Group. The H5Dump tool is documented at: [https://support.hdfgroup.org/documentation/hdf5/latest/_h5_t_o_o_l__d_p__u_g.html](https://support.hdfgroup.org/documentation/hdf5/latest/_h5_t_o_o_l__d_p__u_g.html)

HDF5Dump dumps roughly the same information as H5Dump using the DDL (data description language) format (see [https://support.hdfgroup.org/documentation/hdf5/latest/_d_d_l_b_n_f114.html](https://support.hdfgroup.org/documentation/hdf5/latest/_d_d_l_b_n_f114.html)).

You can use HDF5Dump to get a more detailed view of the HDF5 file than is provided by the HDF5 Browser control panel. However, HDF5Dump supports only a subset of the H5Dump command line tool so you may need to obtain and use the H5Dump tool itself.

When working with a large HDF5 file, HDF5Dump can take a long time and generate a ton of text. See the notes in the Details section below about aborting the dump and diverting the output from the history area to a notebook.

### *Parameters* {#parameters}
*fileNameStr* is a full path to the HDF5 file, or a file name or partial path relative to the Igor symbolic path specified via /P.

If *fileNameStr* is omitted or is "", HDF5Dump displays an Open File dialog. HDF5Dump also displays an Open File dialog if the *fileNameStr* and *pathName* do not fully specify the file of interest.

If you use a full or partial path for *fileNameStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

The parameter for the /A, /D, /G, /L and /T flags are strings which can contain a simple name or a full HDF5 path.

At most one of the /A, /D, /G, /L and /T flags can be used in any single call to HDF5Dump.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *attributeNameStr* ]</span> | If /A alone is used, only the header and attributes are dumped, not specific datasets. If /A=*attributeNameStr* is used, only the specified attribute is dumped. |
| <span class="table-cell-nowrap">/ATTR = *dumpAttributes*</span> | If *dumpAttributes* is zero, dumping of attributes is suppressed. Use this when attributes clutter the dump. |
|  | If *dumpAttributes* is 1 or if the /ATTR flag is omitted, attributes are included in the dump. |
| <span class="table-cell-nowrap">/D = *datasetNameStr*</span> | Only the specified dataset is dumped. |
|  | *datasetNameStr* may contain a simple name ("Dataset1") in the root level of the file or a full HDF5 path ("/GroupA/Dataset1"). You may also specify hyperslab start, stride, count and block parameters ("/GroupA/Dataset1[1,1;2,3;3,19;1,1]"). |
| <span class="table-cell-nowrap">/G = *groupNameStr*</span> | Only the specified group is dumped. |
| /H=*dumpHeaderOnly* |<table class="nested-table"><tbody><tr><td>*dumpHeaderOnly*=0:</td><td>The header and data are dumped. This can take a long time when called for large datasets (default).</td></tr><tr><td>*dumpHeaderOnly*=1:</td><td>Only the header is dumped.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I = *dumpObjectIDs*</span> | If *dumpObjectIDs* = 1, object IDs are included in the dump. If *dumpObjectIDs* = 0 or /I is omitted, object IDs are excluded from the dump. |
| <span class="table-cell-nowrap">/L = *linkNameStr*</span> | Only the specified link is dumped. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | *pathName* is the name of an Igor symbolic path that specifies the directory to look in for *fileNameStr.* |
| <span class="table-cell-nowrap">/PROP = *dumpProperties*</span> | If *dumpProperties*  = 1, object properties are included in the dump. If *dumpProperties*  = 0 or /I is omitted, object properties are excluded from the dump. |
|  | Object properties include storage layout, chunking and compression information. They are of interest mainly to advanced HDF5 users. |
|  | /PROP=1 acts like the -p flag in the h5dump tool from the HDF Group. |
|  | The /PROP flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/Q</span> | If /Q is omitted, then the output is dumped to Igor's history area and to the S_HDF5Dump variable. If /Q is present, then output is dumped only to the S_HDF5Dump variable. |
| <span class="table-cell-nowrap">/R = *dumpAsASCII*</span> | If *dumpAsASCII* = 1, output for one-byte data is dumped as ASCII code. If If *dumpAsASCII* = 0 or /R is omitted, output for one-byte data is dumped as numbers. |
| <span class="table-cell-nowrap">/T = *datatypeNameStr*</span> | Only the specified named datatype is dumped. |
| <span class="table-cell-nowrap">/TIME = *timeInSeconds*</span> | Specifies a maximum time in seconds for the dump to complete. |
|  | A timeout is rarely needed. If you dump a very large HDF5 dataset and include the data in the dump (you omit /H), it can take an arbitrarily long time. You can specify a timeout to limit how long HDF5Dump will wait for the dump to finish. If a timeout occurs, HDF5Dump returns a timeout error. You can catch this error in a user-defined function using GetRTError. |
|  | /TIME was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/W = *widthInColumns*</span> | *widthInColumns* is the maximum number of characters in each dumped output line. The default value is 80 which should work for most cases. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
If you omit /H or specify /H=*0* the output from HDF5Dump can be voluminous and can take a long time for large datasets.

### *Output Variables* {#output-variables}
HDF5Dump sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
| S_path | Set to the path leading to the folder containing the dumped file. This is a system file path (e.g., "hd:FolderA:FolderB:"), not an Igor symbolic path. The path uses Macintosh HFS path syntax, even on Windows, and has a trailing colon. |
| S_fileName | Set to the name of the dumped file. |
| S_HDF5Dump | Set to the dump text. |

### *Examples* {#examples}

```igor
NewPath/O HDF5Data	// Create symbolic path to folder containing file

// Dump entire file but header only
HDF5Dump/P=HDF5Data/H=1 "test.h5"

// Dump just one dataset
HDF5Dump/P=HDF5Data /D="/GroupA/Dataset1" "test.h5"

// Dump just one attribute (TITLE) of one dataset
HDF5Dump/P=HDF5Data /A="/GroupA/Dataset1/TITLE" "test.h5"
```