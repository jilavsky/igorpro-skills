---
description: "The HDF5SaveData operation saves a single wave in an HDF5 file as a dataset or as an attribute if /A is present."
slug: /commands/hdf5savedata
---

<div className="command-signature">

## <strong>HDF5SaveData</strong>  [ /A={<em>attributeNameStr</em> [, <em>options</em> ]} /APND=<em>append</em> /ENUM={<em>enumList</em> [, <em>keyValSepStr</em>, <em>keyValTermStr</em> ]} /IGOR=<em>attributesMask</em> /GZIP={<em>compressionLevel</em>, <em>shuffle</em>} /LAYO={<em>layout</em> [, <em>chunkSizeList</em> ]} /MAXD={<em>maxDimSizeList</em>} /O /OPTS=<em>options</em> /REF=<em>refMode</em> /SLAB=<em>slabWave</em> /STRF={<em>fixedLength</em>,<em>paddingMode</em>,<em>charset</em>} /TRAN=<em>transpose</em> /WRIT=<em>write</em> /Z ] <em>wave</em>, <em>locationID</em> [, <em>nameStr</em> ] {#hdf5savedata}

</div>

The HDF5SaveData operation saves a single wave in an HDF5 file as a dataset or as an attribute if /A is present.

HDF5SaveData cannot save Igor variables. To save variables in an HDF5 file, you must use  [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) or you must copy the variables into waves and then save the waves.

### *Parameters* {#parameters}
*wave* is the name of or path to the wave to be saved.

*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is an optional string containing the name of the dataset to be created or to which an attribute is to be attached. This can be a full HDF5 path or partial HDF5 path or simple name relative to *locationID*. All groups referenced by *nameStr* must already exist.

If *nameStr* is omitted, HDF5SaveData acts as if the name of the wave name were provided as *nameStr*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = {*attributeNameStr* [, *options* ]}</span> |  |
|  | If *attributeNameStr* is not "" then an attribute is written rather than a dataset. The wave is saved as an attribute of the dataset specified by *locationID* and *nameStr*. The dataset must already exist in the file. |
|  | When you write an attribute, you must provide the normally-optional *nameStr* parameter. See the DemoAttributes example below. |
|  | If you omit options, it defaults to 0, and you can omit the curly braces. |
|  | If *options* is omitted or is 0, a single-element attribute is written using a scalar dataspace. This is needed for compatibility with the NeXus NeXpy program. |
|  | If *options* is 1, a single-element attribute is written using a simple dataspace. This is needed for compatibility with [https://nwb.org/](https://nwb.org/). |
| <span class="table-cell-nowrap">/APND = *dim*</span> | /APND is used to append new data to an existing dataset, increasing its size. It works with datasets only and returns an error if saving an attribute. |
|  | /APND is not allowed together with /SLAB. |
|  | By default, an HDF5 dataset's is not extendible (its size cannot be increased) because its layout is "contiguous" and its maximum dimensions are equal to its initial dimensions. Consequently, if you use /APND on a typical dataset, it returns an error. For it to work, the dataset must be specifically created to be extendible. |
|  | In order for a dataset to be extendible, its layout must be set appropriately when the dataset is initially created. The dataset's layout must be set to "chunked" (using the /LAYO flag) and its maximum dimensions must be set sufficiently large (using the /MAXD flag). Then the /APND flag will work. |
|  | The DemoSaveAndExtend2DWave example below illustrates the use of /LAYO, /MAXD and /APND. |
|  | *dim* = -1: Normal save, no append (default). |
|  | If the specified dataset does not exist then /APND is ignored and the save is a normal save which creates a new dataset. |
|  | The rest of this section covers the case where *dim* is 0, 1, 2 or 3 and the dataset already exists. In this case, all of the data in the wave is appended to the dataset. |
|  | *dim* is a dimension number (in Igor terminology, 0=rows, 1=columns, 2=layers, 3=chunks). The wave data is appended to the dataset by adding elements to the specified dimension while keeping the sizes of all other dimensions unchanged. |
|  | The number of dimensions in the wave must be the same as the number of dimensions in the specified dataset. Also the size of all dimensions except the the dimension specified by *dim* must match. Also the wave and dataset must both be either numeric or text. |
|  | *dim* must be less than the rank of the dataset. For example, you cannot specify *dim* as 1 for a 1D dataset because this implies extending a dimension that does not exist. |
|  | For a 1D dataset, you can only add additional rows. |
|  | For a 2D dataset, you can add additional rows (/APND=0) or additional columns (/APND=1). |
|  | For a 3D dataset, you can add additional rows (/APND=0) additional columns (/APND=1) or additional layers (/APND=2). |
|  | For a 4D dataset, you can add additional rows (/APND=0) additional columns (/APND=1), additional layers (/APND=2) or additional chunks (/APND=3). |
|  | The DemoSaveAndExtend2DWave example below illustrates the use of /LAYO, /MAXD and /APND. |
| <span class="table-cell-nowrap">/ENUM = {*enumList* [, *keyValSepStr*, *keyValTermStr* ]</span> |  |
|  | Specifies that the dataset or attribute is to be saved using an enum datatype. /ENUM was added in Igor Pro 9.01. |
|  | *wave* must be an integer data type. |
|  | *enumList* is a list of enumerator names and values like "True=1;False=0;". If you specify "" for *enumList*, this acts like omitting /ENUM entirely. |
|  | Each enumeration datatype member is specified by one name and one integer number separated by an equal sign. A semicolon must follow each keyword=value pair. No extraneous characters, such as white space, are allowed. |
|  | *keyValSepStr* is the separator between each keyword and the associated integer value. If omitted, it defaults to "=" which will be sufficient for normal use. If specified, the separator is the first byte of *keyValSepStr*. |
|  | *keyValTermStr* is the terminator after each keyword/value pair. If omitted, it defaults to ";" which will be sufficient for normal use. If specified, the terminator is the first byte of *keyValTermStr*. |
|  | Normally you can omit the *keyValSepStr* and *keyValTermStr* parameters and use just /ENUM=*enumList*. You need to use *keyValSepStr* and *keyValTermStr* only in the very rare circumstance that the equal sign or semicolon are used as part of an enum member name. If you specify either, specify a single ASCII character. |
|  | See [Saving HDF5 Enum Data](/igorpro/data/igor-hdf5-guide.md#saving-hdf5-enum-data) for further details and an example. |
| <span class="table-cell-nowrap">/GZIP = {*compressionLevel*, *shuffle*}</span> |  |
|  | Tells the HDF5 library to use GZIP compression when writing the data. |
|  | *compressionLevel* : An integer from 0 to 9. 0 is no compression, 9 is maximum compression. |
|  |<table class="nested-table"><tbody><tr><td>*shuffle*&nbsp;=&nbsp;0:</td><td>Do not shuffle data prior to compressing.</td></tr><tr><td>*shuffle*&nbsp;=&nbsp;1:</td><td>Do shuffle data prior to compressing. Shuffle reorders the bytes of multi-byte data elements and can result in higher compression ratios.</td></tr></tbody></table>
|  | Using compression or shuffle requires the use of chunked layout which you can specify using the /LAYO flag. In Igor Pro 9.00 and later, the /GZIP flag sets the layout to chunked if *compressionLevel* or *shuffle* are non-zero. You can override this using the /LAYO flag but there is no reason to do so. |
|  | For background information on compression, see [HDF5 Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-compression). |
| <span class="table-cell-nowrap">/IGOR = *attributesMask*</span> | The /IGOR flag determines which attributes HDF5SaveData writes attributes to record wave properties such as units and scaling. |
|  | If *attributesMask* is 0, no attributes are written. |
|  | If *attributesMask* is -1, all attributes are written (except, as explained below, that attributes are not written if the corresponding wave property is the default value). This is recommended if you intend to load the data back into Igor. If the /IGOR flag is omitted it behaves like /IGOR=-1. |
|  | Otherwise *attributesMask* is a bitwise mask, described below. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | If you omit the /IGOR flag, it behaves like /IGOR=63 (bits 0 through 5 are set). This excludes date attributes (bit 6). Excluding this maintains compatibility with earlier versions of HDF5SaveData and prevents clutter. |
|  | The bits are defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Write wave type attribute named &quot;IGORWaveType&quot;. This is a number that identifies the wave&#39;s data type. See [WaveType](/igorpro/commands/wavetype.md) for the interpretation of this number.</td></tr><tr><td>Bit&nbsp;1:</td><td>Write wave scaling attribute named &quot;IGORWaveScaling&quot;.</td></tr><tr><td></td><td>The wave scaling attribute is an N+1 row by 2 column double-precision floating point array where N is the number of dimensions in the wave.</td></tr><tr><td></td><td>Row 0 contains the data full scale values for the wave. Column 0 of row 0 contains the max full scale value and column 1 contains the min full scale value.</td></tr><tr><td></td><td>Row i+1 contains the dimension scaling values for dimension i of the wave. Dimension scaling is defined as:</td></tr><tr><td></td><td>`Scaled index value = A * elementNumber + B`</td></tr><tr><td></td><td>Column 0 of row i+1 contains the A values and column 1 contains the B values for dimension i.</td></tr><tr><td></td><td>The `IGORWaveScaling` attribute is not written if the data full scale values are both zero and A=1 and B=0 for all dimensions.</td></tr><tr><td>Bit&nbsp;2:</td><td>Write wave units attribute named &quot;IGORWaveUnits&quot;. This attribute is written using a variable-length, null-terminated string datatype.</td></tr><tr><td></td><td>The wave units attribute is an N+1 row array of C strings where N is the number of dimensions in the wave. Row 0 contains the data units for the wave. Row i+1 contains the dimension units for dimension i of the wave.</td></tr><tr><td></td><td>The `IGORWaveUnits` attribute is not written if the all units are empty (&quot;&quot;).</td></tr><tr><td>Bit&nbsp;3:</td><td>Write wave dimension labels attribute named &quot;IGORWaveDimensionLabels&quot;. This attribute is written using a variable-length, null-terminated string datatype.</td></tr><tr><td></td><td>The wave dimension labels attribute is an N+1 row by M array of C strings.</td></tr><tr><td></td><td>M is the number of dimensions.</td></tr><tr><td></td><td>N is chosen so to be large enough to hold all dimension labels up to the last non-empty one. For example, if you have a 5x3 matrix wave with labels for rows 1 and 2 and for column 0, and with all other dimension labels empty, N would be 3 (one for the overall dimension label and two for the two row labels.</td></tr><tr><td></td><td>Row 0 contains the overall label for the dimension. Row i contains the dimension label for element i-1.</td></tr><tr><td></td><td>The `IGORWaveDimensionLabels` attribute is not written if the wave has no dimension labels.</td></tr><tr><td></td><td>When using the /APND or /SLAB flags, writing the `IGORWaveDimensionLabels` attribute would give the wrong result because the labels written would represent just a subset of the data. Thus this bit is ignored when those flags are used.</td></tr><tr><td>Bit&nbsp;4:</td><td>Write wave note attribute named &quot;IGORWaveNote&quot;. This attribute is written using a fixed-length, unterminated string datatype.</td></tr><tr><td></td><td>The wave note attribute is a fixed length scalar string containing the wave&#39;s note text.</td></tr><tr><td></td><td>The `IGORWaveNote` attribute is not written if the wave has no wave note.</td></tr><tr><td>Bit&nbsp;5:</td><td>Write wave lock attribute named &quot;IGORWaveLock&quot;.</td></tr><tr><td></td><td>A scalar containing the wave lock state.</td></tr><tr><td></td><td>The `IGORWaveLock` attribute is not written if the wave lock state is zero (unlocked).</td></tr><tr><td>Bit&nbsp;6:</td><td>Write a wave creation date attribute named &quot;IGORWaveCreationDateLocal&quot; and a wave modification date attribute named &quot;IGORWaveModificationDateLocal&quot;.</td></tr><tr><td></td><td>The dates are written as doubles in Igor date/time format (seconds since 1904-01-01) using integer local time coordinates.</td></tr><tr><td></td><td>Support for writing these date attributes was added in Igor Pro 9.00.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/LAYO = {*layout* [, *chunkSizeList* ]}</span> |  |
|  | This flag is used to create an extendible dataset (one whose size can be increased at a later time) and when saving a compressed dataset, both of which require that the layout be chunked. The layout and chunk sizes must be set when the dataset is initially created. /LAYO is ignored when HDF5SaveData is called to extend an existing dataset. |
|  |<table class="nested-table"><tbody><tr><td>*layout*&nbsp;=&nbsp;0:</td><td>Compact layout.</td></tr><tr><td>*layout*&nbsp;=&nbsp;1:</td><td>Contiguous layout. This is the default layout if /LAYO is not present.</td></tr><tr><td>*layout*&nbsp;=&nbsp;2:</td><td>Chunked layout. For a dataset to be extendible or compressed, the layout must be chunked.</td></tr></tbody></table>
|  | *chunkSizeList* is a list of zero to four dimension sizes for dimensions 0 through 3 respectively. If *layout* is 2 (chunked layout), you can specify a chunk size for each dimension in the dataset. |
|  | In Igor Pro 9.00 and later, the /GZIP flag sets the layout to chunked if *compressionLevel* or *shuffle* are non-zero. You can override this using the /LAYO flag but there is no reason to do so. |
|  | In Igor Pro 9.00 and later, if you specify fewer chunk sizes than there are dimensions in the wave being saved, or if you specify 0 for a dimension's chunk size, HDF5SaveData uses the size of the corresponding wave dimension as the chunk size. Therefore /LAYO={2}, by omitting chunk sizes, tells HDF5SaveData to use the wave dimension for the chunk size for each wave dimension which in turn means that the entire wave is saved as one chunk. Prior to Igor Pro 9.00, it was an error to specify fewer dimensions than exist in the wave or to specify 0 for an existing wave dimension chunk size. |
|  | In Igor Pro 9.00 and later, if you are satisfied with writing a compressed dataset as one chunk, you can use /GZIP and omit /LAYO. |
|  | For background information on compression, see [HDF5 Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-compression). |
|  | If the /LAYO flag is used with the /MAXD flag, the chunk size for a given dimension must be less than or equal to the maximum dimension size. |
|  | The DemoSaveAndExtend2DWave example below illustrates the use of /LAYO. |
| <span class="table-cell-nowrap">/MAXD = {*maxDimSizeList*}</span> |  |
|  | This flag is used mostly to create an extendible dataset (one whose size can be increased at a later time) which requires that the maximum size of each dimension be set at least as large as the ultimate size of the dataset. This maximum size must be set when the dataset is initially created. /MAXD is ignored when HDF5SaveData is called to extend an existing dataset. |
|  | If /MAXD is omitted then the maximum size of each dimension in the dataset is the same as its initial size which is set by the size of the wave being saved. In this case, the dataset cannot be extended at a later time. |
|  | *maxDimSizeList* is a list of zero to four maximum dimension sizes for dimensions 0 through 3 respectively. You must specify a chunk size for each dimension in the dataset. If the /LAYO flag is used with the /MAXD flag, the chunk size for a given dimension must be less than or equal to the maximum dimension size. |
|  | A value of -1 for a particular dimension means that the maximum size of that dimension is unlimited. A value of zero means that the maximum size of that dimension is equal to its initial size. Otherwise each maximum dimension size must be a positive integer at least as large as the corresponding dimension of the wave being saved. |
|  | The DemoSaveAndExtend2DWave example below illustrates the use of /MAXD. |
| <span class="table-cell-nowrap">/O</span> | Overwrite existing dataset in case of a name conflict. If /O is omitted and the dataset already exists, HDF5SaveData returns an error. |
| <span class="table-cell-nowrap">/OPTS = *options*</span> | Controls aspects of saving data. |
|  | /OPTS requires Igor Pro 9.00 or later. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>If set, HDF5SaveData saves 64-bit integer data as 64-bit integer. If cleared, it saves 64-bit integer data as double-precision floating point.</td></tr><tr><td></td><td>For backward compatibility, bit 0 defaults to 0. If you omit /OPTS, 64-bit integer data is saved as double-precision floating point.</td></tr><tr><td>Bit&nbsp;1:</td><td>If set, HDF5SaveData saves single-element datasets using a scalar dataspace. If cleared or if you omit /OPTS a simple dataspace is used. This bit applies to datasets only;  for attributes use the options parameter of the /A flag. Bit 1 requires Igor Pro 9.01 or later.</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
| <span class="table-cell-nowrap">/REF = *refMode*</span> | If *refMode* is non-zero, text waves are saved as HDF5 object references. |
|  |<table class="nested-table"><tbody><tr><td>*refMode*&nbsp;=&nbsp;0:</td><td>Do not save text waves as references.</td></tr><tr><td>*refMode*&nbsp;=&nbsp;1:</td><td>Save text waves as object references.</td></tr><tr><td>*refMode*&nbsp;=&nbsp;2:</td><td>Save text waves as dataset region references. This is currently not supported.</td></tr></tbody></table>
|  | See [Saving HDF5 Object Reference Data](/igorpro/data/igor-hdf5-guide.md#saving-hdf5-object-reference-data) for details. |
|  | /REF requires Igor Pro 8.03 or later. |
| <span class="table-cell-nowrap">/SLAB = *slabWave*</span> | Saves a wave in a subset of an existing dataset. |
|  | *slabWave* is a two-dimensional, numeric wave with exactly four columns and a number of rows greater than or equal to the number of dimensions in the dataset being loaded. *slabWave* defines a hyperslab used during the save. |
|  | See [HDF5 Dataset Subsets](/igorpro/data/igor-hdf5-guide.md#hdf5-dataset-subsets) for details on constructing a slab wave. |
|  | The size and shape of the wave must match the size and shape of the slab. Otherwise an error or unpredictable behavior results. |
|  | When saving an attribute, /SLAB is ignored. |
|  | /SLAB is not allowed together with /APND. |
|  | The HDF5SaveData operation does not support saving a subset of a variable-length dataset. If you use the /SLAB flag when saving a variable-length dataset, HDF5SaveData returns an error. |
|  | The DemoSaveSlab2D example below illustrates the use of /SLAB. |
| <span class="table-cell-nowrap">/STRF = {*fixedLength*,*paddingMode*,*charset*}</span> |  |
|  | Controls the format in which string datasets and attributes are written. /STRF requires Igor Pro 9.00 or later. |
|  | If *fixedLength* is 0, HDF5SaveData writes strings using a variable-length HDF5 string datatype. |
| The HDF5 library does not allow the creation of a zero-length fixed-length datatype. Consequently, starting with Igor Pro 9.02, Igor writes zero-length strings using a variable-length datatype regardless of the type specified by <span class="table-cell-nowrap">/STRF.</span> |  |
|  | If *fixedLength* is greater than 0, HDF5SaveData writes strings using a fixed-length HDF5 string datatype of the specified length with padding specified by *paddingMode*. |
|  | If *fixedLength* is -1, HDF5SaveData determines the length of the longest string to be written for a given dataset or attribute and writes strings using a fixed-length HDF5 string datatype of that length with padding specified by *paddingMode*. |
|  |<table class="nested-table"><tbody><tr><td>*paddingMode*&nbsp;=&nbsp;0:</td><td>Writes fixed-length strings as null terminated strings.</td></tr><tr><td>*paddingMode*&nbsp;=&nbsp;1:</td><td>Writes fixed-length strings as null-padded strings.</td></tr><tr><td>*paddingMode*&nbsp;=&nbsp;2:</td><td>Writes fixed-length strings as space-padded strings.</td></tr></tbody></table>
|  | When writing strings as variable length (*fixedLength*=0), *paddingMode* is ignored. |
|  |<table class="nested-table"><tbody><tr><td>*charset*&nbsp;=&nbsp;0:</td><td>Writes strings marked as ASCII.</td></tr><tr><td>*charset*&nbsp;=&nbsp;1:</td><td>Writes strings marked as UTF-8.</td></tr></tbody></table>
|  | See [HDF5 String Formats](/igorpro/data/igor-hdf5-guide.md#hdf5-string-formats) for details. |
| /TRAN=*transpose* |<table class="nested-table"><tbody><tr><td>*transpose*&nbsp;=&nbsp;0:</td><td>Normal save, no transpose (default).</td></tr><tr><td>*transpose*&nbsp;=&nbsp;1:</td><td>Multi-dimensional numeric waves are saved transposed. This works only when saving multi-dimensional, numeric (real or complex) waves and is ignored for 1D and text waves. See [HDF5 Images Versus Igor Images](/igorpro/data/igor-hdf5-guide.md#hdf5-images-versus-igor-images) for details.</td></tr></tbody></table>
| /WRIT=*write* |<table class="nested-table"><tbody><tr><td>*write*&nbsp;=&nbsp;0:</td><td>The dataset is created but no data is actually written. The data in the dataset is set to 0.</td></tr><tr><td>*write*&nbsp;=&nbsp;1:</td><td>The dataset is created and the data is written to it. This is the default.</td></tr></tbody></table>
|  | Use /WRIT=0 to quickly create a very large wave when you intend to write it piece-by-piece later using HDF5SaveData with the /SLAB flag. |
|  | Although the wave data is not written to disk when you use /WRIT=0, you must still create the entire wave because this determines the size and data type of the HDF5 dataset. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
HDF5SaveData writes multi-element datasets and attributes using a simple dataspace.

HDF5SaveData writes single-element datasets using a simple dataspace unless, in Igor Pro 9.01 or later, you set bit 1 of the options parameter of the /OPTS flag in which case it uses a scalar dataspace.

HDF5SaveData writes single-element attributes using a scalar dataspace unless you specify otherwise using the *options* parameter of the /A flag.

Igor Pro supports complex waves but HDF5 does not support complex datasets. Therefore, when saving a complex wave, HDF5SaveData writes the wave as if its number of rows were doubled. For details, see [Handling of Complex Waves](/igorpro/data/igor-hdf5-guide.md#handling-of-complex-waves).

The [HDF5SaveData](/igorpro/commands/hdf5savedata.md) operation returns an error if you try to save a wave reference or data folder reference wave.

### *Output Variables* {#output-variables}
HDF5SaveData sets the following output variable:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *Example* {#example}

```igor
// A simple save routine
Function DemoSaveWave(w)
	Wave w

	Variable result = 0	// 0 means no error
	
	Variable fileID
	HDF5CreateFile/P=HDF5Data /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif
	
	HDF5SaveData /O /Z w, fileID
	if (V_flag != 0)
		Print "HDF5SaveData failed"
		result = -1
	endif

	HDF5CloseFile fileID
	
	return result
End

// Save a dataset and then extend its size
Function DemoSaveAndExtend2DWave()
	Variable result = 0	// 0 means no error
	
	Variable fileID
	HDF5CreateFile/P=HDF5Data /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif
	
	Make/O/N=(3,2) wave2D = p + 10*q

	// In order for the dataset to be extendible, chunked layout must be used
	// and the maximum dimension sizes must be set. In this case, we set the
	// maximum dimension size to unlimited (-1).
	HDF5SaveData /LAYO={2,32,32} /MAXD={-1,-1} /O /Z wave2D, fileID
	if (V_flag != 0)
		Print "First HDF5SaveData failed"
		result = -1
	else
		// We have created the initial dataset, now we add two new rows
		Make/O/N=(2,2) wave2D = p+3 + 10*q

		// We now append to the rows dimension (dimension 0) of the dataset
		HDF5SaveData /APND=0 /Z wave2D, fileID
		if (V_flag != 0)
			Print "Second HDF5SaveData failed"
			result = -1
		endif			
	endif

	HDF5CloseFile fileID
	
	return result
End

// Overwrite a section of a 2D dataset
Function DemoSaveSlab2D()
	Variable result = 0		// 0 means no error

	Make/O/N=(5,4) wave2D = p + 10*q

	// Save original dataset
	Variable fileID
	HDF5CreateFile/P=HDF5Data /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif
	HDF5SaveData /O /Z wave2D, fileID
	if (V_flag != 0)
		Print "First HDF5SaveData failed"
		result = -1
	else
		// Overwrite with new data.	
		Make/O/N=(3,2) wave2D = -(p+2 + 10*(q+1))
		HDF5MakeHyperslabWave("tempSlab", 2)	// Make hyperslab wave for two dimensional slab
		Wave tempSlab
		tempSlab[0][%Start] = 2		// Start at row 2
		tempSlab[0][%Stride] = 1
		tempSlab[0][%Count] = 1		// Save 1 block
		tempSlab[0][%Block] = 3		// A block is 3 rows
		tempSlab[1][%Start] = 1		// Start at column 1
		tempSlab[1][%Stride] = 1
		tempSlab[1][%Count] = 1		// Save 1 block
		tempSlab[1][%Block] = 2		// A block is 2 columns
		HDF5SaveData /SLAB=tempSlab /Z wave2D, fileID
		if (V_flag != 0)
			Print "Second HDF5SaveData failed"
			result = -1
		endif
		KillWaves/Z tempSlab
	endif

	KillWaves/Z wave2D

	HDF5CloseFile fileID

	return result
End

// Writing attributes to a group and to a dataset
Function DemoAttributes(w)
	Wave w

	Variable result = 0	// 0 means no error
	
	// Create file
	Variable fileID
	HDF5CreateFile/P=HDF5Data /O /Z fileID as "Test.h5"
	if (V_flag != 0)
		Print "HDF5CreateFile failed"
		return -1
	endif

	// Write an attribute to the root group
	Make /FREE /T /N=1 groupAttribute = "This is a group attribute"
	HDF5SaveData /A="GroupAttribute" groupAttribute, fileID, "/"
	
	// Save wave as dataset
	HDF5SaveData /O /Z w, fileID	// Uses wave name as dataset name
	if (V_flag != 0)
		Print "HDF5SaveData failed"
		result = -1
	endif

	// Write an attribute to the dataset
	Make /FREE /T /N=1 datasetAttribute = "This is a dataset attribute"
	String datasetName = NameOfWave(w)
	HDF5SaveData /A="DatasetAttribute" datasetAttribute, fileID, datasetName

	HDF5CloseFile fileID
	
	return result
End		// The attribute waves are automatically killed since they are free waves
```

### *See Also* {#see-also}
[HDF5CreateFile](/igorpro/commands/hdf5createfile.md), [HDF5OpenFile](/igorpro/commands/hdf5openfile.md), [HDF5CloseFile](/igorpro/commands/hdf5closefile.md), [HDF5FlushFile](/igorpro/commands/hdf5flushfile.md), [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md), [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md), [HDF5CloseGroup](/igorpro/commands/hdf5closegroup.md)

See [Saving HDF5 Object Reference Data](/igorpro/data/igor-hdf5-guide.md#saving-hdf5-object-reference-data) for details on saving reference data.