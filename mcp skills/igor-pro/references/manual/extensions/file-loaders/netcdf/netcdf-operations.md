---
description: "Opens the named NetCDF Classic or NetCDF 64-bit offset format file. If fileNameStr is omitted or is \"\", or if the /I flag is used, NC_OpenFile presents an…"
slug: /extensions/file-loaders/netcdf/netcdf-operations
---

<div className="command-signature">

## <strong>NC_OpenFile</strong>  [/Z /I /PATH=<em>pathName</em> ] <em>refNum</em> [<em>as</em> <em>fileNameStr</em> ] {#nc_openfile}

</div>

Opens the named NetCDF Classic or NetCDF 64-bit offset format file.

### *Parameters* {#parameters}
If *fileNameStr* is omitted or is *""*, or if the /I flag is used, NC_OpenFile presents an Open File dialog from which you can choose the file to load.

If you use a full or partial path for fileNameStr, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

|  |  |
| --- | --- |
| *refNum* | is the name of a numeric variable to receive the file reference number. |
|  | *refNum* is set by NC_OpenFile if it actually opens a file for reading. |
| *fileNameStr* | The targeted file is specified by a combination of the *pathName* parameter and the *fileNameStr* parameter. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/I</span> | A Open File dialog is displayed to choose the file. |
| <span class="table-cell-nowrap">/PATH = *pathName*</span> | Specifies the folder to look in for the file. *pathName* is the name of an existing symbolic path. |

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| S_fileName | S_fileName is set to the opened file name if V_flag returns 0. |
| S_path | S_path is set to the path of the opened file name if V_flag returns 0. |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |

### *Thread Safety* {#thread-safety}
NC_OpenFile is thread-safe if fileNameStr is a full native path to an existing file. In this case an optional given pathName is ignored and not resolved.

NC_OpenFile is not thread-safe if a given pathName has to be resolved and/or the file dialog is used. pathName is evaluated if fileNameStr is not a full path to a file.

### *Example* {#example}

```igor
Variable fileID
NC_OpenFile fileID as "C:Data:test.nc"      // Windows using Macintosh path
NC_OpenFile fileID as "C:\\Data\\test.nc"   // Windows using Windows path
NC_CloseFile fileID
```

### *See Also* {#see-also}
[NC_CloseFile](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_closefile)


<div className="command-signature">

## <strong>NC_CloseFile</strong>  [/A /Z ] [<em>refNum</em> ] {#nc_closefile}

</div>

Closes a previously opened NetCDF file.

### *Parameters* {#nc_closefile-parameters}

|  |  |
| --- | --- |
| *refNum* | is a number or a numeric variable with the file reference number that was set by NC_OpenFile |

### *Flags* {#nc_closefile-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/A</span> | Closes all open NetCDF files. If /A is used *refNum* should be omitted. |

### *Output Variables* {#nc_closefile-output-variables}

|  |  |
| --- | --- |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |

### *Example* {#nc_closefile-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
NC_CloseFile fileID
```

### *See Also* {#nc_closefile-see-also}
[NC_OpenFile](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_openfile)

<div className="command-signature">

## <strong>NC_ListObjects</strong>  [/Z /Q [/T=<em>typeNameList</em> ] ] <em>refNum</em> {#nc_listobjects}

</div>

Returns object names from a NetCDF file in a semicolon separated list.

NC_ListObjects returns an error if no object of a given type exists.

### *Parameters* {#nc_listobjects-parameters}

|  |  |
| --- | --- |
| *refNum* | is a number or a numeric variable with the file reference number that was set by NC_OpenFile. |

### *Flags* {#nc_listobjects-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/Q</span> | Suppress output to history area. |
| <span class="table-cell-nowrap">/T = *typeNameList*</span> | A semicolon separated list of NetCDF object types. Valid types are |
|  |<table class="nested-table"><tbody><tr><td>*dim*</td><td>dimension names</td></tr><tr><td>*att*</td><td>global attribute names</td></tr><tr><td>*var*</td><td>variable names</td></tr><tr><td>*udim*</td><td>name of unlimited dimension</td></tr></tbody></table>
|  | If /T=*typeNameList* is omitted NC_ListObjects returns all names as if `"dim;att;var;udim;"` was given. |

### *Output Variables* {#nc_listobjects-output-variables}

|  |  |
| --- | --- |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |
| S_names | Returned list of object names |

### *Example* {#nc_listobjects-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
NC_ListObjects fileID
NC_ListObjects/T="var" fileID
NC_CloseFile fileID
```

### *See Also* {#nc_listobjects-see-also}
[NC_Inquire](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_inquire)





<div className="command-signature">

## <strong>NC_ListAttributes</strong>  [/Z /Q ] <em>refNum</em>, [<em>varNameStr</em> ] {#nc_listattributes}

</div>

Returns attribute names from a NetCDF file in a semicolon separated list.

### *Parameters* {#nc_listattributes-parameters}

|  |  |
| --- | --- |
| *refNum* | is a number or a numeric variable with the file reference number that was set by NC_OpenFile. |
| *varNameStr* | name of the NetCDF variable for which all attribute names are returned. When omitted the files global attribute names are returned. |

### *Flags* {#nc_listattributes-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/Q</span> | Suppress output to history area. |

### *Output Variables* {#nc_listattributes-output-variables}

|  |  |
| --- | --- |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |
| S_names | Returned list of attribute names |

### *Example* {#nc_listattributes-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
NC_ListAttributes fileID                    // Gets global attribute names
NC_ListAttributes fileID, "var"             // Gets attribute names of variable var
NC_CloseFile fileID
```

### *See Also* {#nc_listattributes-see-also}
[NC_Inquire](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_inquire)

<div className="command-signature">

## <strong>NC_Inquire</strong>  [/Z /Q /A=<em>attNameStr</em> ] <em>refNum</em>, [<em>varNameStr</em> ] {#nc_inquire}

</div>

Returns number of dimensions, dimension names and dimension sizes of a NetCDF attribute or variable.

### *Parameters* {#nc_inquire-parameters}

|  |  |
| --- | --- |
| *refNum* | is a number or a numeric variable with the file reference number that was set by NC_OpenFile. |
| *varNameStr* | name of a NetCDF variable. |
|  | When combined with /A=*attNameStr* the attribute of the variable is referenced. |
|  | When *varNameStr* is omitted /A=*attNameStr* should be set to refer to a global attribute. |

### *Flags* {#nc_inquire-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/Q</span> | Suppress output to history area. |
| <span class="table-cell-nowrap">/A = *attNameStr*</span> | optional attribute name. Can be combined with varNameStr to refer to an attribute of a variable. If varNameStr is omitted /A refers to a global attribute. |

### *Output Variables* {#nc_inquire-output-variables}

|  |  |
| --- | --- |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |
| V_type | Data type of the variable or attribute. See also [WaveType](/igorpro/commands/wavetype.md) for a type code table. |
| S_names | Semicolon separated list of dimension names of the variable. |
|  | If the variable is scalar (not an array) it has no dimension and S_names is empty. |
|  | In NetCDF attributes have no dimension names. If an attribute is referenced S_names is empty. |
| S_dims | Semicolon separated list of dimension sizes of the variable or attribute. |
|  | The order of S_names is equal to the order of S_dims. The number of elements in the lists equals the number of dimensions of the variable or attribute. Attributes are always one dimensional. |
|  | Scalar variables (not an array) have no NetCDF dimensions. For such variables S_dims and S_names is an empty String. |
|  | The NetCDF format allows to define a 'unlimited' dimension that grows dynamically. If no data was written to a variable defined with such dimension S_dims return a size of zero. |

### *Example* {#nc_inquire-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
NC_Inquire fileID, "var"                    // Gets information about variable var
NC_Inquire/A="att" fileID, "var"            // Gets information about attribute att of variable var
NC_Inquire/A="gatt" fileID                  // Gets information about global attribute gatt
NC_CloseFile fileID
```

### *See Also* {#nc_inquire-see-also}
[NC_LoadData](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_loaddata)





<div className="command-signature">

## <strong>NC_LoadData</strong>  [/Z /Q /O /L /U=<em>unpackMode</em> /T=<em>loadType</em> /FREE /DEST=<em>destWave</em> /A[=<em>attNameStr</em> ] /ALL[=<em>loadAll</em> ] ] <em>refNum</em>, [<em>varNameStr</em> ] {#nc_loaddata}

</div>

Loads an attribute or variable from a NetCDF data set into a wave. If no destination wave reference is given the name of the wave that is created is the same as *varNameStr* or if omitted as *attNameStr*. If a wave with this name exists and /O is not set the wave name is changed to a different unique name. Evaluate S_names in such case.

### *Parameters* {#nc_loaddata-parameters}

|  |  |
| --- | --- |
| *refNum* | is a number or a numeric variable with the file reference number that was set by NC_OpenFile. |
| *varNameStr* | name of a NetCDF variable. |
|  | When combined with /A=*attNameStr* the attribute of the variable is loaded. |
|  | When *varNameStr* is omitted /A=*attNameStr* refers to a global attribute. |

### *Flags* {#nc_loaddata-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents aborting of procedure execution if an error occurs. |
| <span class="table-cell-nowrap">/Q</span> | Suppress output to history area. |
| <span class="table-cell-nowrap">/O</span> | If a wave with the same name exists it is overwritten. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | The data is loaded to the wave referenced by destWave. If /FREE or /O is not specified and destWave exists an error is raised. |
| <span class="table-cell-nowrap">/FREE</span> | The data is loaded to a free wave. The wave reference must be given by /DEST=*destWave*. |
| <span class="table-cell-nowrap">/A[ = *attNameStr ]*</span> | Can be combined with varNameStr to refer to an attribute of a variable. If varNameStr is omitted /A refers to a global attribute. |
|  | /A without specifying attNameStr is only allowed in combination with /ALL. |
| <span class="table-cell-nowrap">/U = *unpackMode*</span> | The NetCDF format defines attribute conventions for basic data post processing of variables. Attributes of a variable can be set to enable *range checking* and *data scaling*. If these specific attributes are set for the variable NC_LoadData applies *range checking* and *data scaling.* The unpackMode flag allows to selectively disable this data post processing. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Range check and data scaling is enabled, same as /U is omitted.</td></tr><tr><td>1:</td><td>Range check is enabled, data scaling is disabled.</td></tr><tr><td>2:</td><td>Range check is disabled, data scaling is enabled.</td></tr><tr><td>3:</td><td>Range check and data scaling is disabled</td></tr></tbody></table>
|  | When data scaling is applied the resulting data type is converted to Float or Double accordingly. |
| <span class="table-cell-nowrap">/T = *loadType*</span> | This flag applies only if the data type of the source variable or attribute is NC_CHAR, it has no effect with other source types. As char data in NetCDF can contain zeroes it is loaded by default to a wave with data type Byte. The /T flag allows to load to a text wave instead. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Loads to a text wave where each element contains a string with a single char. Note that zeroes in the source data will appear as strings with zero length.</td></tr><tr><td>1:</td><td>Loads to a text wave with a single element that contains a string. This load type works on one dimensional data only. The string in wave[0] might contain zero bytes. Load type 1 is useful when loading variable meta data from attributes such as text descriptions.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/L</span> | When /L is set dimensions are ignored and the variable or attribute is loaded to an one dimensional wave. It is the only way to load high dimensional data that exceeds the maximum number of wave dimensions supported by Igor Pro. The source dimensions can be evaluated from S_dims. The NetCDF XOP does not reorder the data in memory when /L is used. |
| <span class="table-cell-nowrap">/ALL[ = *loadAll* ]</span> | Loads all NetCDF variables and attributes of a file. loadAll can either be 0 or 1, disabling or enabling this feature. /ALL without loadAll flag is identical to loadAll set to 1. |
|  | If /A and "*varNameStr*" is omitted all NetCDF variables, global attributes and variable attributes are loaded. |
|  | If /ALL is combined with /A and "*varNameStr*" is omitted all global NetCDF attributes are loaded. |
|  | If /ALL is combined with /A and "*varNameStr*" is given all NetCDF attributes of the specified NetCDF variable are loaded. |
|  | The /ALL option can be combined with /U, /T and /L. |
|  | Combining /ALL with one of /DEST, /FREE or /A="*attNameStr*" raises an error. |
|  | When executed from the command line on successful load a summary of loaded waves is printed to the history area. Note that the NetCDF properties are shown. The actual wave could have a different data type if scaling by unpacking (see /U) was applied or different dimension if /L was set. |
|  | In case there is an error loading data NC_LoadData stops loading further data and S_names returns empty. |

### *Output Variables* {#nc_loaddata-output-variables}

|  |  |
| --- | --- |
| V_flag | V_flag is set to 0 if no error occurred, otherwise it returns an error code. |
| S_names | Name of the created wave. |
|  | When /ALL was set, semicolon separated list of loaded waves. |
| S_dims | Semicolon separated list of dimension sizes of the variable or attribute. |
|  | When /ALL was set, S_dims returns an empty string. |

### *Variable Names* {#variable-names}
If /DEST=waveRef is omitted the name of the resulting wave equals the variable name / global attribute parameter of the operation. The NetCDF library uses normalized UTF-8 encoding for object names. The variable name from Igor is first normalized before accessing a NetCDF object. Thus, denormalized and normalized UTF-8 variable names from Igor target the same object in a NetCDF data set.

### *Text Data* {#text-data}
Source data of the type NC_CHAR can be loaded into an Igor text wave with the /T flag. The NC_CHAR data is assumed to use UTF-8 text encoding. If you know that the source data uses a different text encoding, after loading the data call [SetWaveTextEncoding](/igorpro/commands/setwavetextencoding.md) without the /CONV flag to specify the correct text encoding for the text wave's text data.

NetCDF char data can contain null bytes that are transferred to the strings of a text wave. As handling of such strings might be tedious loading without /T as Wave of type byte is recommended for such data.

See also: [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes)


### *Scalar Variables* {#scalar-variables}
A scalar variable (not an array) has by NetCDF specification no dimensions. S_dims returns an empty String for scalar variables.

### *Variables with dimension size zero* {#variables-with-dimension-size-zero}
NetCDF datasets can have one dimension that grows dynamically when data is written. This dimension is called "unlimited dimension". If no data was written the size of this dimension is zero. When loading a variable where at least one dimension size is zero an empty wave is created. This wave has zero dimensions. The actual number of source dimensions and dimension sizes can be read from S_dims.

### *Attributes with size zero* {#attributes-with-size-zero}
When loading an empty attribute that has zero size an empty wave is created.

### *Respected Attribute Conventions* {#respected-attribute-conventions}
NetCDF defines various attributes for variables with additional information. Respected are the following attributes when set:

|  |  |
| --- | --- |
| *units* | sets waves data units |
| *long_name* | sets wave note |
| *dimension names* | sets dimension labels (these are actually in NetCDF no attributes) |

### *Attributes for range check* {#attributes-for-range-check}

|  |  |
| --- | --- |
| *valid_min* | defines the minimum |
| *valid_max* | defines the maximum |
| *valid_range* | defines the range |
| *_FillValue* | defines the maximum if no other limit is set |
| *missing_value* | data points exceeding the valid range are treated as *missing_value* |

NC_LoadData respects the NetCDF attribute convention with the following rules:

- Data points exceeding the valid range get replaced by *missing_value*
- *missing_value* must be of the same data type as the source data set 
- It is treated as error to have valid_range and valid_min  or  valid_range and valid_max defined.
- If *_FillValue* is defined and neither *valid_range* nor *valid_min* nor *valid_max* is defined then *_FillValue* sets the maximum of the range.

See also: [https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html](https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html)

If range attributes for a variable in the NetCDF file are defined then NC_LoadData sets the data full scale property of the wave accordingly. See also [WaveInfo](/igorpro/commands/waveinfo.md).

Range check can be disabled with /U=2.

### *Attributes for data scaling* {#attributes-for-data-scaling}

|  |  |
| --- | --- |
| *scale_factor* | the raw data gets multiplied by scale_factor |
| *add_offset* | add_offset is added to the raw data |

These attributes are typically used to save data in a smaller data type. Depending on the source data type and the data type of scale_factor and add_offset the resulting wave is of type Float or Double. Thus the scaling may increase the memory footprint. Scaling can be disabled with /U=1.

See also [https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html](https://docs.unidata.ucar.edu/netcdf-c/current/attribute_conventions.html)

### *Example* {#nc_loaddata-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
NC_LoadData fileID, "var"                           // Loads variable var
NC_LoadData/A="att" fileID, "var"                   // Loads attribute att of variable var
NC_LoadData/A="gatt" fileID                         // Loads global attribute gatt
NC_LoadData/DEST=ram/FREE/U=3/T=1 fileID, "var"     // Loads variable var which must be of type NC_CHAR
                                                    // into the free text wave ram as a single String in
// element 0, disables unpacking of the data
NC_LoadData/ALL fileID                              // Loads all variables
NC_LoadData/ALL/A fileID, "var"                     // Loads all attributes of variable var
NC_CloseFile fileID
```

### *See Also* {#nc_loaddata-see-also}
[NC_Inquire](/igorpro/extensions/file-loaders/netcdf/netcdf-operations.md#nc_inquire)


<div className="command-signature">

## <strong>NC_DumpErrors</strong>  [/C /Q ] {#nc_dumperrors}

</div>

Returns up to the last 128 errors from the NetCDF library. When executed from the command line the error information is dumped to the history area as well.

### *Flags* {#nc_dumperrors-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Clears the error information after dumping to S_errorInfo |
| <span class="table-cell-nowrap">/Q</span> | Suppress output to history area. |

### *Output Variables* {#nc_dumperrors-output-variables}

|  |  |
| --- | --- |
| S_errorInfo | Collected error messages from the NetCDF library. The format is |
|  | code<space>errorMessage<LF>. |

### *Example* {#nc_dumperrors-example}

```igor
Variable fileID
NC_OpenFile fileID as "hd:Data:test.nc"
// Do NetCDF things here
NC_DumpErrors/C                 // Retrieve collected error information
print S_errorInfo
NC_CloseFile fileID
```

### *See Also* {#nc_dumperrors-see-also}
[StringFromList](/igorpro/commands/stringfromlist.md)