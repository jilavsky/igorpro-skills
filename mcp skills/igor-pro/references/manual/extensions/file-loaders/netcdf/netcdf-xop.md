---
description: "The NetCDF XOP extends Igor Pro with operations for reading data from NetCDF Classic and NetCDF 64-bit offset files."
slug: /extensions/file-loaders/netcdf/netcdf-xop
---

The NetCDF XOP extends Igor Pro with operations for reading data from NetCDF Classic and NetCDF 64-bit offset files. It also provides ways to browse NetCDF data files.

The NetCDF file format was developed and is maintained at Unidata. ([https://docs.unidata.ucar.edu/netcdf-c/current/](https://docs.unidata.ucar.edu/netcdf-c/current/))

:::note
NetCDF XOP does not support NetCDF-4 files. Please use [HDF5 Operations and Functions](/igorpro/data/igor-hdf5-guide.md#hdf5-operations-and-functions) for NetCDF-4 files.
:::

NetCDF XOP runs on Windows 64-bit. This version is intended for use with Igor Pro 8.00 or later.

## Installing NetCDF XOP {#installing-netcdf-xop}

To install the XOP create a shortcut in the "Igor Extensions" folder. A quick way to open Igor's Extension folder is choosing "Show Igor Pro User Files" from the Help menu. It opens a file browser window where "Igor Extensions" is a subfolder ("Igor Extensions (64-bit)" for IGOR64).

The 64-bit NetCDF XOP is located at:

```
Igor Pro Folder\More Extensions (64-bit)\File Loaders\NetCDF64.xop
```

Choose "Show Igor Pro Folder" from the Help menu and navigate to the XOP file. Create a shortcut for the XOP file and move it to the Igor Extensions (64-bit) folder.

If the NetCDF XOP was installed correctly in the menu Data/Load Waves a new item *Load NetCDF File...* is available that allows to load complete data files conveniently.

## Data Type Mapping {#data-type-mapping}
| NetCDF | Igor Pro Type | Comment |
| --- | --- | --- |
| NC_CHAR | NT_I8 | 8 bit INT |
|  | TEXT_WAVE | with /T=0 one character per wave element
|  | TEXT_WAVE | with /T=1 String in element 0, 1D source data only
| NC_BYTE | NT_I8 | 8 bit INT |
| NC_SHORT | NT_I16 | 16 bit INT |
| NC_INT | NT_I32 | 32 bit INT |
| NC_LONG | NT_I32 | 32 bit INT |
| NC_FLOAT | NT_FP32 | 2 bit floating point |
| NC_DOUBLE | NT_FP64 | 4 bit floating point |

## Data Ordering {#data-ordering}

For multidimensional data NetCDF defines that the last dimension varies the fastest. The XOP reorders the data in memory accordingly. For example reading a 2x2 matrix from a NetCDF file with input data:

```
{1, 2, 3, 4}
```

is represented in Igor Pro in the mapping:

```igor
data[0][0] = 1; data[0][1] = 2; data[1][0] = 3; data[1][1] = 4;
```

When forcing a one dimensional load of a multidimensional NetCDF variable using the /L flag the XOP does not reorder the data. With the /L flag the upper example results in a one dimensional wave with:

```igor
data[0] = 1; data[1] = 2; data[2] = 3; data[3] = 4;
```
<br>

## The NetCDF Copyright {#the-netcdf-copyright}

The NetCDF XOP contains software written by third parties. The copyright notices below are included as a condition of our use of such software.

Copyright 1993, 1994, 1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, University Corporation for Atmospheric Research/Unidata.

Portions of this software were developed by the Unidata Program at the University Corporation for Atmospheric Research.

Access and use of this software shall impose the following obligations and understandings on the user. The user is granted the right, without any fee or cost, to use, copy, modify, alter, enhance and distribute this software, and any derivative works thereof, and its supporting documentation for any purpose whatsoever, provided that this entire notice appears in all copies of the software, derivative works and supporting documentation.  Further, UCAR requests that the user credit UCAR/Unidata in any publications that result from the use of this software or in any product that includes this software, although this is not an obligation. The names UCAR and/or Unidata, however, may not be used in any advertising or publicity to endorse or promote any products or commercial entity unless specific written permission is obtained from UCAR/Unidata. The user also understands that UCAR/Unidata is not obligated to provide the user with any support, consulting, training or assistance of any kind with regard to the use, operation and performance of this software nor to provide the user with any updates, revisions, new versions or "bug fixes."

THIS SOFTWARE IS PROVIDED BY UCAR/UNIDATA "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL UCAR/UNIDATA BE LIABLE FOR ANY SPECIAL, INDIRECT OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE ACCESS, USE OR PERFORMANCE OF THIS SOFTWARE.