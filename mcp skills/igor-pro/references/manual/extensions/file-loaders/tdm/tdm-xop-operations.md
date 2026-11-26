---
description: "This section documents the TDM XOP operations. TDMLoadData is a high-level operation that loads the entirety of a TDM file into an Igor data folder."
slug: /extensions/file-loaders/tdm/tdm-xop-operations
---

# TDM XOP Operations {#tdm-xop-operations}

This section documents the TDM XOP operations.

[TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) is a high-level operation that loads the entirety of a TDM file into an Igor data folder.

[TDMSaveData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavedata) is a high-level operation that saves an Igor data folder to a TDM file.

For most purposes, these high-level operations will suffice and you do not need to use the low-level TDM XOP functions, but if you do, see [TDM XOP Functions Overview](#tdm-xop-functions-overview).
<br>

<div className="command-signature">

## <strong>TDMLoadData</strong>  [ /I=[<em>mode</em> ]  /PROP=<em>propertyFlags</em>  /O[=<em>overwriteMode</em> ]  /P=<em>pathName</em>  /Q[=<em>quietMode</em> ]  /T=<em>topLevelDFPathStr</em>   /XSCL=<em>xScalingMode</em> ]  <em>filePathStr</em> {#tdmloaddata}

</div>

The TDMLoadData operation loads data from the specified file which must be a National Intruments TDM file with a .tdm or .tdms extension.

TDMLoadData loads all data into a data folder created in the current data folder. The new top-level data folder is specified by the /T flag or is based on the file name if /T is omitted.

By default, TDMLoadData loads file properties into numeric and string variables in the top-level data folder. You can skip loading file properties using the /PROP flag.

TDMLoadData then loads each channel group into a separate sub-data folder which we will call the channel group data folder. It loads the channel group's properties into numeric and string variables in the channel group data folder. You can skip loading channel group properties using the /PROP flag.

It then loads the channels for a given channel group into waves in the channel group data folder. It stores channel properties as keyword-value pairs in the wave's note. You can skip loading channel properties using the /PROP flag.

If you use the /XSCL flag, which was added in TDM version 1.50, TDMLoadData uses TDM waveform channel properties to set the X scaling and X units of waves that it loads. This use of these properties is controlled by /XSCL, independent of /PROP. The /XSCL flag is described in detail below.

### *Parameters* {#parameters}
*filePathStr*  is a simple file name, partial file path or full file path. It can use either Macintosh HFS or Windows-style path syntax. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming paths.

If *filePathStr*  is a simple file name or partial file path, it is relative to the symbolic path specified by *pathName*. For details on symbolic paths, see [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths).

If *filePathStr*  is "" or if /I is used, TDMLoadData displays an Open File dialog from which you can select the file to load. An Open File dialog is also displayed if *filePathStr*  and *pathName*  do not reference an existing file.

### *Flags* {#flags}

|  |  |  |  |
| --- | --- | --- | --- |
| <span class="table-cell-nowrap">/I = [*mode*]</span> | Sets interactive mode. |  |  |
|  | /I by itself is equivalent to /I=1. |  |  |
|  | If /I is omitted or /I=0 is used, TDMLoadData does not display an Open File dialog but just loads the data from the file specified by *pathName* and *filePathStr*. |  |  |
|  | If /I or /I=1 is used, TDMLoadData displays an Open File dialog and then loads the data. |  |  |
|  | If /I=2 is used, TDMLoadData displays an Open File dialog but does not load the data. It just sets the output variables as described below. You can use this to allow the user to choose a file which you will open with low-level TDM XOP functions (e.g., [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex)). |  |  |
|  | If /I=3 is used, TDMLoadData displays an Open File dialog only if *pathName* and *filePathStr* do not fully specify a file. Whether a dialog is displayed or not, it just sets the output variables as described below and does not actually load any data. You can use this to allow the user to choose a file which you will open with low-level TDM XOP functions (e.g., [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex)). |  |  |
|  | If /I is omitted or /I=0 is specified and the file specified by *pathName* and *filePathStr* does not exist, TDMLoadData displays an Open File dialog as if /I=1 or /I=2 were present. |  |  |
| <span class="table-cell-nowrap">/PROP = *propertyFlags*</span> | *propertyFlags* controls whether properties are loaded. *propertyFlags* is a bitwise parameter defined as follows: |  |  |
|  | **propertyFlags** | **Bit Number** | **Loads This Type of Property** |
|  | 1 | 0 | File properties |
|  | 2 | 1 | Channel group properties |
|  | 4 | 2 | Channel properties |
|  | If no /PROP is specified, all of these property types are loaded. This is equivalent to /PROP=7. All other bits are reserved and should be set to zero. |  |  |
| <span class="table-cell-nowrap">/O[ = *overwriteMode* ]</span> | If /O is omitted or *overwriteMode* is 0, if there is an existing data folder whose name conflicts with the new top-level data folder, TDMLoadData generates a unique name for the new top-level data folder. |  |  |
|  | If /O=1 is used, if there is an existing data folder whose name conflicts with the new top-level data folder, the data is loaded anyway and any conflicting waves and variables are overwritten. Any non-conflicting waves and variables are left intact. |  |  |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder that *filePathStr* is relative to. *pathName*  is the name of an existing symbolic path. |  |  |
|  | For details on symbolic paths, see [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths). |  |  |
| <span class="table-cell-nowrap">/Q[ = *quietMode* ]</span> | If /Q or /Q=1 is present, this suppresses the normal messages in the history area. |  |  |
|  | If /Q is omitted or /Q=0 is present, the normal messages are printed in the history area. |  |  |
| <span class="table-cell-nowrap">/T = *topLevelDFPathStr*</span> | *topLevelDFPathStr* specifies the path to the new top-level data folder. |  |  |
|  | The trailing colon in *topLevelDFPathStr* can be present or omitted. In other words, "root:TDMData" and "root:TDMData:" are equivalent and both specify that the top-level data folder is TDMData in the root data folder. |  |  |
|  | Liberal names within *topLevelDFPathStr* may be quoted or not. |  |  |
|  | If /T is omitted or if *topLevelDFPathStr* is "", the top-level data folder is created in the current data folder and its name is a possibly-cleaned up version of the file name with the extension removed. By "file name", we mean the actual file name, not the name property of the file object in the TDM file. |  |  |
|  | The root data folder can not be the top-level data folder so /T="root:" is illegal. |  |  |
|  | Here are some examples of legal *topLevelDFPathStr* values assuming that we want to use TDMData as the name for the top-level data folder: |  |  |
|  | <code class="igor">/T="root:TDMData"           // Create TDMData in root&#10;/T=":TDMData"               // Create TDMData in current data folder&#10;/T="root:MyData:TDMData"    // Create TDMData in root:MyData</code> |  |  |
|  | In all of these examples, if the TDMData folder does not already exist, it is created. The parent of the top-level data folder (e.g., MyData in the third example) must already exist. |  |  |
|  | If the specified top-level data folder does exist and overwrite is off, a unique name is generated for the top-level data folder. If it does exist and overwrite is on, the existing data folder is reused. |  |  |
| <span class="table-cell-nowrap">/XSCL = *xScalingMode*</span> | This flag was added in TDM XOP version 1.50. It controls how TDMLoadData sets the X scaling and X units properties of waves created when loading TDM channels. |  |  |
|  | If *xScalingMode* is 0, TDMLoadData does not set the wave's X scaling or X units, leaving the default settings, x0=0 and dx=0 (point scaling) with X units="". For backward compatibility, this is the default behavior if you omit /XSCL. |  |  |
|  | If *xScalingMode* is non-zero, it is a bitwise setting. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |  |  |
|  | The bits of *xScalingMode*  are defined as follows: |  |  |
|  | **Bit 0**:   Sets the wave's x0 property as follows: |  |  |
|  | If the channel has a wf_start_time property and it is  greater than zero, TDMLoadData sets the wave's x0 property to the date/time specified by wf_start_time. It also sets the wave's X units to "dat" as this is necessary for Igor to display the X data as date/time values - see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves) for details. |  |  |
|  | **Bit 1**:   Sets the wave's x0 property as follows: |  |  |
|  | If the channel has a wf_start_offset property and it is greater than zero, TDMLoadData sets the wave's x0 property to the offset in seconds specified by wf_start_offset. |  |  |
|  | If bit 0 is set and the channel has a greater-than-zero wf_start_time property, bit 0 controls and bit 1 has no effect. |  |  |
|  | **Bit 2**:   Sets the wave's dx property as follows: |  |  |
|  | If the channel has a wf_increment property and it is non-zero, TDMLoadData sets the wave's dx property to the increment in seconds specified by wf_increment. |  |  |
|  | **Bit 3**:   Sets the wave's X units as follows: |  |  |
|  | If the channel has a wf_xunit_string property and it is non-empty, TDMLoadData sets the wave's X units property to the specified units. However, TDMLoadData does not do this if the units were set to "dat" because bit 0 of *xScalingMode*  was set and the channel has a greater-than-zero wf_start_time property. |  |  |
|  | See **Channel Wave X Scaling and X Units**  below for further discussion. |  |  |

### *Details* {#details}
If /I is omitted or /I=0 is specified and the file specified by *pathName* and *filePathStr* does not exist, TDMLoadData displays an Open File dialog as if /I=1 or /I=2 were present.

To find what objects were created by TDMLoadData, you can use the S_topLevelDF output variable to find the top-level data folder and the [CountObjects](/igorpro/commands/countobjects.md) and [GetIndexedObjName](/igorpro/commands/getindexedobjname.md) functions to determine what sub-data folders, waves and variables were created.

If the TDM file contains groups or channels with names longer than Igor's 31-character limit, TDMLoadData truncates the names to fit. After truncating, TDMLoadData resolves any conflicts among the truncated names by adding a suffix (0, 1, 2 . . .) to the conflicting name.

Long file, group or channel *property*  names are handled differently. If there is a conflict after truncating the names, the later property overwrites the earlier property. This should rarely be a problem because property names tend to be short.

Timestamp data is loaded in Igor date/time format, namely, seconds since January 1, 1904. See [Date Values](/igorpro/igor-basics/tables.md#date-values) for details.

### *File and Group Properties* {#file-and-group-properties}
File and channel group properties are loaded into Igor global numeric and string variables. If a property name conflicts with the name of another Igor object, TDMLoadData changes the name. For example, the name of the TDM file datetime property conflicts with the Igor datetime function and therefore is loaded as datetime0.

TDM properties can exist but have no value. This is the case for the TDM file datetime property until it is explicitly set. TDMLoadData loads numeric properties with no value as NaN and string properties with no value as the empty string ("").

### *Channel Properties* {#channel-properties}
TDMLoadData uses the built-in name and unit_string channel properties to set the wave's name and data units. This is done regardless of the /PROP flag. As described in this section, all other channel properties are loaded only if permitted by the /PROP flag or if /PROP is omitted.

If you use the /XSCL flag, TDMLoadData uses TDM waveform channel properties to set the X scaling and X units of waves that it loads. This use of these properties is controlled by /XSCL, independent of /PROP.

The rest of this section discusses channel properties stored in the wave's note if permitted by /PROP.

Channel properties are stored in the corresponding wave's note. Each property is stored on a separate line of the wave note and is preceded by one of these preamble strings which identify the line as representing a TDM property of a particular type:

```
TDMUInt8:
TDMInt16:
TDMInt32:
TDMFloat:
TDMDouble:
TDMTimestamp:
TDMString:
```

The preamble string is followed by a keyword=value pair which specifies the property name and the property value. A carriage return character marks the end of the value. For example, assuming that a channel named ch0 has a minimum property equal to -17.3, that property would be represented in the wave's note by this line:

```
TDMDouble:minimum=-17.3<CR>
```

This line defines a "wave note channel property" - the representation of a TDM channel property stored in a wave note.

You could extract this property using:

```igor
String key = "TDMDouble:minimum"
Variable minimum = NumberByKey(key, note(ch0), "=", "\r")
```

If the description property is "Beam 1", the corresponding line in the wave note would be:

```
TDMString:description=Beam 1<CR>
```

You could extract this property using:

```igor
String key = "TDMString:description"
String description = StringByKey(key, note(ch0), "=", "\r")
```

Properties in TDM files can exist but have no value. For example, the built-in channel minimum and maximum properties have no value by default. Numeric properties that have no value in the TDM file are set to NaN in the wave note. String properties that have no value in the TDM file are set to "" in the wave note.

### *Escaping of Tab, CR, LF and Backslash Characters in Wave Note Channel Properties* {#escaping-of-tab-cr-lf-and-backslash-characters-in-wave-note-channel-properties}
If a string property contains tab, carriage-return (CR), linefeed (LF) or backslash characters, TDMLoadData escapes them during the process of setting the wave note, replacing tab with "\\t", CR with "\\r", LF with "\\n" and backslash with "\\\\". In this uncommon case, you need to reconstruct the original string property by un-escaping the value, like this:

```igor
String key = "TDMString:description"
String text = note(ch0)
String description = StringByKey(key, text, "=", "\r")
description = UnEscapeStr(description)
```

where UnEscapeStr is a user-defined function that reverses the escaping process.

In most cases your channel string properties will not contain tabs, CRs, LFs or backslashes so you won't need to unescape them. If you do need it, here is the definition of UnEscapeStr:

```igor
// UnEscapeStr(str)
// Converts escape sequences "\t", "\r", "\n" and "\\" in str to tab, CR, LF and backslash respectively.
// Used for unescaping text in wave note escaped by TDMLoadData when TDMLoadData created the wave
// from a channel and stored the channel's properties as key=value pairs in the wave note.
// Example:
//	Assume wave0 was created by TDMLoadData and contains a string property named StringProperty which may
//	have contained tabs, CRs, LFs and backslashes. These characters would have been converted to escape
//	sequences by TDMLoadData as the string property was stored as a key=value pair in the wave note.
//	Here we extract the value of the string property and then reverse the effect of escaping the characters:
//		String key = "TDMString:StringProperty"
//		String text = note(wave0)
//		String stringProperty =  StringByKey(key, text, "=", "\r")	// Get string property with escape sequences
//		stringProperty = UnEscapeStr(stringProperty)			// Convert escape sequences to regular characters
Function/S UnEscapeStr(str)
    String str					// String possibly containing \t, \r, \n and \\ to represent tab, CR, LF and backslash.

    String outStr = ""
    Variable len = strlen(str)
    String ch, nextCh

    Variable i

    for(i=0; i<len; i+=1)
        ch = str[i]
        if (CmpStr(ch,"\\") == 0)
            if (i < len-1)
                nextCh = str[i+1]
                strswitch(nextCh)
                    case "t":
                        ch = "\t"
                        i += 1
                        break;
                    case "r":
                        ch = "\r"
                        i += 1
                        break;
                    case "n":
                        ch = "\n"
                        i += 1
                        break;
                    case "\\":
                        ch = "\\"
                        i += 1
                        break;
                endswitch
            endif
        endif
        outStr += ch
    endfor

    return outStr
End
```

### *Channel Wave X Scaling and X Units* {#channel-wave-x-scaling-and-x-units}
By default, TDMLoadData does not set the X scaling of waves created by loading channels. In version 1.50 or later of the XOP, you can use the /XSCL flag to control how X scaling is set. In this case, TDMLoadData uses waveform channel properties described at: [http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/](http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/)

Use /XSCL=5 to set the wave's X scaling as a date/time value, if the channel has a wf_start_time property and it is greater than zero. In this case, TDMLoadWave also sets the wave's X units to "dat" as this is necessary for Igor to display the X data as date/time values - see [Date/Time Waves](/igorpro/igor-basics/waves.md#date-time-waves) for details.

Use /XSCL=14 to set the wave's X scaling as a non-date/time value (e.g., seconds or volts), if the channel has a wf_offset property and it is greater than zero.

Use /XSCL=12 to set the wave's delta X property, if the channel has a wf_offset property and it is greater than zero, leaving its x0 property at 0.

The wf_start_time property of a TDM channel is a timestamp property. National Instruments uses a 128-bit number to represent timestamps. Igor supports only 64-bit numbers. Consequently some precision is lost when you load a timestamp into Igor. However 64-bits permits representing seconds the 5 decimal digits of precision, which is sufficient for most applications.

### *Output Variables* {#output-variables}
TDMLoadData sets the following variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if the operation succeeded or a non-zero Igor error code if it failed. |
| V_TDMResult | Set to 0 if the operation succeeded or to a DIAdem Connectivity Library error code if an error occurred in a library call. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details. |
| S_fileName | Name of the file being loaded. |
| S_path | File system path to the folder containing the file. |
| S_topLevelDF | Set to the full path to the top-level data folder into which TDMLoadData loaded the data. The path ends with a trailing colon. |


S_Path is in Macintosh HFS format and includes a trailing colon so that S_path+S_fileName forms a valid full path to the file that was loaded.

When TDMLoadData presents an Open File dialog and the user cancels, V_flag is set to 0 and S_fileName is set to "".

### *See Also* {#see-also}
[TDM XOP](/igorpro/extensions/file-loaders/tdm/tdm-xop.md) for overview information.

The [TDMSaveData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavedata) operation.





<div className="command-signature">

## <strong>TDMSaveData</strong>  [ /I=[<em>mode</em> ]  /MAPN=<em>nameMap</em> /O[=<em>overwriteMode</em> ] /P=<em>pathName</em>  /PROP=<em>propertyFlags</em>  /Q[=<em>quietMode</em> ] /T=<em>topLevelDFPathStr</em>   /XSCL=<em>xScalingMode</em> ] <em>filePathStr</em> {#tdmsavedata}

</div>

The TDMSaveData operation saves data from an Igor data folder to the specified file which must have a .tdm or .tdms extension.

The data to be saved is in the "top-level data folder" which is the current data folder or a data folder specified via the /T flag.

TDMSaveData has to map Igor data to the structure of a TDM file. The TDM model consists of a file which contains channel groups which contain channels. Channel groups can not contain other groups. Properties can be attached to the file, to channel groups and to channels.

For the purposes of discussing TDMSaveData, we define the following terms:

|  |  |
| --- | --- |
| *Channel wave* | A wave containing data to be saved in a channel in the TDM file. |
| *Channel group data folder* | A data folder containing zero or more channel waves. |
| *File data folder* | A data folder containing channel group data folders. |
| *Top-level data folder* | Same as file data folder. |

To use TDMSaveWave, you must create a data folder hierarchy that matches this model. For example, your hierarchy may look like this:

```
root
    File                    // Top-level or "file" data folder
        ChannelGroup0
            wave0
            wave1
        ChannelGroup1
            wave0
            wave1
```

In this example, File is the top-level or "file data folder", ChannelGroup0 and ChannelGroup1 are channel group data folders, and wave0 and wave1 are channel waves. You would specify root:File as the top-level data folder using the /T flag.

The file data folder may contain file properties in the form of Igor numeric and string variables.

Channel group data folders may also contain group properties in the form of Igor numeric and string variables.

Channel waves may contain properties encoded in the wave note. This is described below under Channel Properties.

In TDM version 1.50 or later, if you omit /XSCL or specify /XSCL=-1, TDMSaveData writes the waveform channel property wf_start_time or wf_start_offset, as well as the wf_increment and wf_xunit_string waveform channel properties. These waveform channel properties are described at: [http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/](http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/). TDMSaveData writes the wf_start_time property if the wave's X units are "dat", signifying that the wave's X values are date/time values. Otherwise it writes the wf_start_offset property. It always writes the wf_increment and wf_xunit_string waveform channel properties.

When it loads a TDM file, the [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) operation creates a file data folder, channel group data folders and channel waves as well as file, channel group and channel properties. The TDMSaveData operation expects to operate on a data folder with the same structure. For example, no waves in the file data folder are saved to the TDM file because a channel must reside in a channel group in the TDM model. If a channel group data folder contains a sub-data folder, it is ignored because channel groups can not contain groups in the TDM model.

By default, TDMSaveData maps Igor variables to file properties and channel group properties. It also maps channel wave note contents to channel properties as described below. You can skip saving properties using the /PROP flag.

### *Parameters* {#tdmsavedata-parameters}
*filePathStr*  is a simple file name, partial file path or full file path. It can use either Macintosh HFS or Windows-style path syntax. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming paths.

If *filePathStr*  is a simple file name or partial file path, it is relative to the symbolic path specified by *pathName*. For details on symbolic paths, see [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths).

The file name extension must be either ".tdm" or ".tdms" because that is how the DIAdem library determines whether to create a TDM of TDMS (streaming) file.

If *filePathStr*  is "" or if /I is used, TDMSaveData displays a Save File dialog in which you can specify the file to be saved. A Save File dialog is also displayed if *filePathStr*  and *pathName*  do not reference a valid location at which the file can be created.

### *Flags* {#tdmsavedata-flags}

|  |  |  |  |
| --- | --- | --- | --- |
| <span class="table-cell-nowrap">/I = [*mode*]</span> | Sets interactive mode. |  |  |
|  | /I by itself is equivalent to /I=1. |  |  |
|  | If /I is omitted or /I=0 is used, TDMSaveData does not display a Save File dialog but just saves the data from the file specified by *pathName* and *filePathStr*. |  |  |
|  | If /I or /I=1 is used, TDMSaveData displays a Save File dialog and then saves the data. |  |  |
|  | If /I=2 is used, TDMSaveData displays a Save File dialog but does not save the data. It just sets the output variables as described below. You can use this to allow the user to choose a file which you will create with low-level TDM XOP functions (e.g., [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile)). |  |  |
|  | If /I=3 is used, TDMSaveData displays a Save File dialog only if *pathName* and *filePathStr* do not fully specify a file. Whether a dialog is displayed or not, it just sets the output variables as described below and does not save the data. You can use this to allow the user to specify a file which you will create with low-level TDM XOP functions (e.g., [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile)). |  |  |
|  | If /I is omitted or /I=0 is specified and *pathName* and *filePathStr* do not specify a valid file path then TDMSaveData displays a Save File dialog as if /I=1 or /I=2 were present. |  |  |
| <span class="table-cell-nowrap">/MAPN = *nameMap*</span> | Maps Igor names to TDM file names. See Name Mapping below. |  |  |
| <span class="table-cell-nowrap">/O[ = *overwriteMode* ]</span> | If /O is omitted or *overwriteMode* is 0, if there is an existing file whose name conflicts with the new file, TDMSaveData returns an error. |  |  |
|  | If /O=1 is used, if there is an existing file whose name conflicts with the new file, TDMSaveData deletes the existing file before creating the new file. |  |  |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder that *filePathStr* is relative to. *pathName*  is the name of an existing symbolic path. |  |  |
|  | For details on symbolic paths, see [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths). |  |  |
| <span class="table-cell-nowrap">/PROP = *propertyFlags*</span> | *propertyFlags*  controls whether properties are saved. *propertyFlags*  is a bitwise parameter defined as follows: |  |  |
|  | **propertyFlags** | **Bit Number** | **Saves This Type of Property** |
|  | 1 | 0 | File properties |
|  | 2 | 1 | Channel group properties |
|  | 4 | 2 | Channel properties |
|  | If no /PROP is specified, all of these property types are saved. This is equivalent to /PROP=7. All other bits are reserved and should be set to zero. |  |  |
| <span class="table-cell-nowrap">/Q[ = *quietMode* ]</span> | If /Q or /Q=1 is present, this suppresses the normal messages in the history area. |  |  |
|  | If /Q is omitted or /Q=0 is present, the normal messages are printed in the history area. |  |  |
| <span class="table-cell-nowrap">/T = *topLevelDFPathStr*</span> | *topLevelDFPathStr*  specifies the path to the top-level data folder containing the data to be saved. It can be a full data folder path or a partial path relative to the current data folder. |  |  |
|  | The trailing colon in *topLevelDFPathStr*  can be present or omitted. In other words, "root:TDMData" and "root:TDMData:" are equivalent and both specify that the top-level data folder is TDMData in the root data folder. |  |  |
|  | Liberal names within *topLevelDFPathStr*  may be quoted or not. |  |  |
|  | If /T is omitted or if *topLevelDFPathStr* is "", the current data folder is the top-level data folder. |  |  |
| <span class="table-cell-nowrap">/XSCL = *xScalingMode*</span> | This flag was added in TDM XOP version 1.50. It controls whether TDMSaveData creates waveform channel properties when writing TDM channels. |  |  |
|  | If *xScalingMode*  is -1, TDMSaveData writes the waveform channel property wf_start_time or wf_start_offset channel property, as well as the wf_increment and wf_xunit_string waveform channel properties. This is the default if /XSCL is omitted. |  |  |
|  | If *xScalingMode*  is 0, TDMSaveData does not write waveform channel properties. |  |  |
|  | See **Channel Properties**  below for details. |  |  |

### *Details* {#tdmsavedata-details}
If /I is omitted or /I=0 is specified and *pathName* and *filePathStr* do not fully specify the location of the new file, TDMSaveData displays a Save File dialog as if /I=1 or /I=2 were present.

Igor date/time waves (double-precision waves with "dat" as the data units - see [Date Values](/igorpro/igor-basics/tables.md#date-values) for details) are saved as TDM timestamp channels.

### *File and Group Properties* {#tdmsavedata-file-and-group-properties}
Igor global and numeric variables in the file data folder and the channel group data folders are stored as TDM file and channel folder properties.

If a variable name is the same as the name of an existing TDM property, the existing property is overwritten unless one is numeric and the other is string in which case the variable is not saved as a property. When a property is overwritten, its data type remains unchanged.

If there is no existing property and the name of the Igor global numeric variable contains "date" (case-insensitive) and the value interpreted as an Igor date/time value falls in the range 1972-1-1 to 2072-1-1 or is NaN, that variable is saved as a TDM timestamp value. Otherwise it is saved as double-precision.

### *Channel Properties* {#tdmsavedata-channel-properties}
When TDMSaveData creates a channel, it sets the built-in unit_string property to the data units of the wave being saved. The built-in name property is set the same as the wave name and the built-in description property is set to "Created by TDMSaveData in Igor Pro". These built-in properties are set regardless of the /PROP flag because they are parameters of the DIAdem library DDC_CreateChannel call. You can override these values and/or create additional channel properties as described in this section.

In TDM version 1.50 or later, if you omit the /XSCL flag or specify /XSCL=-1, TDMSaveData writes the waveform channel property wf_start_time or wf_start_offset, as well as the wf_increment and wf_xunit_string waveform channel properties. These waveform channel properties are described at: [http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/](http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/). TDMSaveData writes the wf_start_time property if the wave's X units are "dat", signifying that the wave's X values are date/time values. Otherwise it writes the wf_start_offset property. It always writes the wf_increment and wf_xunit_string waveform channel properties.

The rest of this section discusses channel properties stored in the wave's note if permitted by /PROP.

When [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) loads a TDM file, it stores channel properties in the wave note of the channel wave in special format that looks like this:

```
TDMDouble:minimum=-17.3<CR>
```

This line defines a "wave note channel property" - the representation of a TDM channel property stored in a wave note. In this example, it represents a double-precision TDM channel property named minimum whose value is -17.3. Other data types are TDMUInt8, TDMInt16, TDMInt32, TDMFloat, TDMDouble, TDMTimestamp, and TDMString.

A wave note may contain any number of wave note channel properties, one per line. They are typically created by TDMLoadData but you can also create them yourself so that channels saved by TDMSaveData will have the properties you want.

TDMSaveData creates channel properties from the channel wave note provided that the wave note has that format. For example, if the wave note contains this:

```
TDMDouble:minimum=-17.3<CR>
```

then TDMSaveData creates a channel properties named minimum and sets it to -17.3.

TDMSaveData scans the entire wave note looking for lines of that format and creates channel properties. Lines in the wave note not of this format are ignored.

If a string value in a wave note channel property contains escape codes for tabs, carriage-returns, linefeeds and backslashes, TDMSaveData will convert them to tab, carriage-return (CR), linefeed (LF) or backslash characters respectively. This is the inverse of the process applied by TDMLoadData when it loads channel properties into the wave note.

For further discussion of wave note channel properties, see the Channel Properties section under [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata).

### *Channel Data* {#channel-data}
TDMSaveData saves Igor wave data in TDM channels.

TDM does not support complex data so Igor complex data is saved in a TDM channel with twice the number of points as the Igor wave and with the real data in the even-numbered points and imaginary data in the odd-numbered points.

TDM does not support signed 8-bit data so signed 8-bit Igor waves are saved in unsigned 8-bit channels.

TDM does not support unsigned 16-bit data so unsigned 16-bit Igor waves are saved in signed 16-bit channels.

TDM does not support unsigned 32-bit data so unsigned 32-bit Igor waves are saved in signed 32-bit channels.

Igor date/time waves (double-precision waves with "dat" as data units) are saved in TDM timestamp channels.

Igor text waves are stored in TDM string channels.

### *Name Mapping* {#name-mapping}
You may want to save an Igor object in a TDM file using a name that is not legal in Igor. For example, you may want to save a channel named "time". "time" is the name of an Igor built-in function and you can not use it as a wave name. In this case, you can use a different name for the Igor wave and the TDM channel. You do this via the /MAPN flag ("map name"). For example, if you have a wave named "time0" that you want to save as a TDM channel named "time", you would use this code:

```igor
String nameMap = "time0:time;"
TDMSaveData /MAPN=nameMap . . .
```

This tells TDMSaveData to save any Igor object named "time0" using the TDM name "time".

The *nameMap* parameter to the /MAPN flag can have any number of Igor/TDM name pairs. The Igor name comes first followed by a colon followed by the TDM name followed by a semicolon. The trailing semicolon is required.

The MAPN flag does not affect wave note channel properties, described above, because these are stored as text in the wave note so their names do not need to be legal Igor object names.

There is one built-in mapping for the datetime property, which is a built-in TDM property of type timestamp. "datetime" is the name of an Igor built-in function. When a TDM file is loaded via TMDLoadData, an Igor variable named datetime0 is created instead of datetime to avoid a conflict with the Igor datetime function. When TDMSaveData saves an Igor variable named datetime0 as a property, it saves it under the name datetime instead of datetime0. This mapping is automatic and does not require the use of the /MAPN flag.

### *Output Variables* {#tdmsavedata-output-variables}
TDMSaveData sets the following variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if the operation succeeded or a non-zero Igor error code if it failed. |
| V_TDMResult | Set to 0 if the operation succeeded or to a DIAdem Connectivity Library error code if an error occurred in a library call. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details. |
| S_fileName | Name of the file being saved. |
| S_path | File system path to the folder containing the file. |
| S_topLevelDF | Set to the full path to the top-level data folder saved by TDMSaveData. The path ends with a trailing colon. |

S_path is in Macintosh HFS format and includes a trailing colon so that S_path+S_fileName forms a valid full path to the file that was saved.

When TDMSaveData presents a Save File dialog and the user cancels, V_flag is set to 0 and S_fileName is set to "".

### *See Also* {#tdmsavedata-see-also}
[TDM XOP](/igorpro/extensions/file-loaders/tdm/tdm-xop.md) for overview information.

The [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) operation.





## TDM XOP Functions Overview {#tdm-xop-functions-overview}

The TDM XOP functions provide access to the DIAdem Connectivity Library functions that allow you to create, read and write TDM (.tdm or .tdms) files in Igor. For most purposes, you do not need to use these low-level functions but can use the high-level [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) and [TDMSaveData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavedata) operations instead. If those operations are not sufficient, you can use these flexible low-level functions instead. However this requires and understanding of TDM files and familiarity with Igor programming.

The DIAdem function names start with DDC_, for example, DDC_CreateFile. Most of the DIAdem library functions are mapped to low-level TDM XOP functions whose names start with TDM, for example, [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile).

Many of the TDM XOP functions have pass-by-reference output parameters (used for returning information to the calling user-defined function) and therefore can not be called from Igor's command line or from macros which do not support pass-by-reference. To use the TDM XOP functions you will need to write Igor user-defined functions.

The DIAdem library uses handles to refer to files, channel groups and channels. A handle is a number that identifies an object to the library. You can think of a handle as an ID number for a file, channel group or channel. You receive these handles via calls such as [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex), [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups) and [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels), and store them in Igor variables. You later pass them to other library functions to identify the file, channel group or channel you want to access.

The DIAdem library handles are actually pointers to structures maintained by the library. This means that, if you pass a bad handle to a DDC function, it may crash. A bad handle is a handle that is uninititalized, references an object associated with a file that has been closed, or references a deleted object. The moral is: Be careful to pass only valid handles to the TDM XOP functions.

## TDM XOP Function Result Codes {#tdm-xop-function-result-codes}

All TDM XOP functions return a DIAdem library result code, which we will call a TDM result code, as the direct function result. These codes are documented in National Instruments' nilibddc.h file. However in most cases you will not need to know the meaning of the error codes because the [TDMGetLibraryErrorDescription](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetlibraryerrordescription) function translates error codes into human-readable error messages. A result code of zero indicates success.

TDM result codes are generated by the DIAdem connectivity library and returned by TDM XOP functions to your user-defined function for you to handle as you wish. Igor-related errors, which are usually user-level programming errors such as passing an uninitialized string for an input parameter or passing the wrong type of wave, are not reported through the TDM XOP function result but instead generate an Igor error. An Igor error causes Igor to stop running procedures and display an error message. Normally this is what you would want. However, if you want to detect and handle Igor error yourself, you can intercept them by calling [GetRTError](/igorpro/commands/getrterror.md) after calling a TDM XOP function.

## TDM XOP Function Example {#tdm-xop-function-example}

The LowLevelTDMReadDemo example in this section illustrates using TDM XOP functions to load the contents of a TDM file into Igor. The data is loaded into a newly-created data folder named based on the TDM file's name property. LowLevelTDMReadDemo then creates a sub-data folder for each channel group in the file and loads the channels of each group into the corresponding group sub-data folder.

LowLevelTDMReadDemo starts by calling [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex) to open the file. Like all TDM XOP functions, TDMOpenFileEx returns a TDM result code as the function result and like many TDM XOP functions, it returns another value via a pass-by-reference parameter. In this case the parameter is named fileH and receives the value of a TDM file handle which is later passed to other TDM XOP functions.

Next LowLevelTDMReadDemo calls [TDMGetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertystr) to get some file-level string properties. It then creates a top-level data folder to hold the data to be loaded.

Next LowLevelTDMReadDemo calls [TDMGetNumGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumgroups) and [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups) to get an array of channel group handles. It then enters the channel group loop. In this loop, it creates a sub-data folder for each channel group and gets an array of channel handles using [TDMGetNumChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumchannels) and [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

Inside the channel group loop is the channel loop. This uses [TDMGetNumDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumdatavalues) and [TDMGetDataType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatatype) to create a wave of the right size and type for each channel and then loads the channel data using [TDMGetDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavalues).

The function result returned by LowLevelTDMReadDemo is 0 if everything worked or a non-zero TDM result code. In the event of an error, LowLevelTDMReadDemo uses [TDMGetLibraryErrorDescription](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetlibraryerrordescription) to translate the result code into an error message and displays the message.

This example is general in that it can load any TDM file. If you are working with TDM files of a specific format, for example if you know there is always one channel group containing four 16-bit signed integer channels, you can write a simpler function.

```igor
// LowLevelTDMReadDemo(fullPath)
// fullPath is a full Macintosh HFS or Windows-style path to a .tdm or .tdms file.
// Loads all of the groups and channels into a new data folder based on the file name.
// Each channel group is loaded into a sub-data folder and each channel is loaded into its group data folder.
// The function returns 0 if everything worked or a non-zero DIAdem Connectivity Library error code.
Function LowLevelTDMReadDemo(fullPath)
   String fullPath         // Full HFS or Windows-style path to the .tdm or .tdms file

   String origDFSave = GetDataFolder(1)

   Variable tdmResult = 0

   Variable fileH = 0, groupH = 0, channelH = 0 // Handles to TDM objects

   try
      tdmResult = TDMOpenFileEx(fullPath, "", 1, fileH)
      AbortOnValue tdmResult, 1
      
      String fileName
      tdmResult = TDMGetFilePropertyStr(fileH, "name", fileName)
      AbortOnValue tdmResult, 1
      
      String fileDescription
      tdmResult = TDMGetFilePropertyStr(fileH, "description", fileDescription)
      AbortOnValue tdmResult, 1

      Printf "File name=\"%s\",  description=\"%s\"\r", fileName, fileDescription
      
      // Create the file-level data folder
      String fileDFName = CleanupName(fileName, 0)
      if (CheckName(fileDFName, 11))
         fileDFName = UniqueName(fileDFName, 11, 0)
      endif
      NewDataFolder/O/S $fileDFName    // Groups will be loaded into this file-level data folder.
      
      Variable numGroups
      tdmResult = TDMGetNumGroups(fileH, numGroups)
      AbortOnValue tdmResult, 1
      Printf "File has %d groups\r", numGroups

      // Get an array of group handles
      Make/O/D/N=(numGroups) tempTDMGroups = 0
      tdmResult = TDMGetGroups(fileH, tempTDMGroups, numGroups)
      AbortOnValue tdmResult, 1
      
      Variable group
      for(group=0; group<numGroups; group+=1)			
         groupH = tempTDMGroups[group]

         String groupName
         tdmResult = TDMGetGroupPropertyStr(groupH, "name", groupName)
         AbortOnValue tdmResult, 1
         
         Variable numChannels
         tdmResult = TDMGetNumChannels(groupH, numChannels)
         AbortOnValue tdmResult, 1

         Printf "\tGroup %d: name=%s, numChannels=%d\r", group, groupName, numChannels

         // Get an array of channel handles
         Make/O/D/N=(numChannels) tempTDMChannels = 0 // Create this temp wave in the file level data folder
         tdmResult = TDMGetChannels(groupH, tempTDMChannels, numChannels)
         AbortOnValue tdmResult, 1
      
         // Create the group-level data folder
         String groupDFName = CleanupName(groupName, 0)
         if (CheckName(groupDFName, 11))
            groupDFName = UniqueName(groupDFName, 11, 0)
         endif
         NewDataFolder/O/S $groupDFName         // Channels will be loaded into this group-level data folder.
         
         Variable channel
         for(channel=0; channel<numChannels; channel+=1)				
            channelH = tempTDMChannels[channel]
            
            String channelName
            tdmResult = TDMGetChannelPropertyStr(channelH, "name", channelName)
            AbortOnValue tdmResult, 1
            
            String channelDescription
            tdmResult = TDMGetChannelPropertyStr(channelH, "description", channelDescription)
            AbortOnValue tdmResult, 1

            Variable numPoints
            tdmResult = TDMGetNumDataValues(channelH, numPoints)
            AbortOnValue tdmResult, 1

            Printf "\t\tChannel %d: name=%s, numPoints=%d, description=\"%s\"", channel, channelName, numPoints, channelDescription
            
            Variable dataType
            tdmResult = TDMGetDataType(channelH, dataType)
            AbortOnValue tdmResult, 1
            
            // Make sure the wave name is legal and does not conflict with other types of Igor objects.
            String wName = CleanupName(channelName, 0)
            Variable nameCheck = CheckName(wName, 1)
            if (nameCheck)
               // There is a name conflict.
               if (WaveExists($wName))
                  // The conflict is with a wave.
                  if (dataType==23 && WaveType($wName)!=0)  // We can't overwrite a numeric wave with a text wave
                     wName = UniqueName(wName, 1, 0)        // Create a unique name.
                  endif
                  if (dataType!=23 && WaveType($wName)==0)  // We can't overwrite a text wave with a numeric wave
                     wName = UniqueName(wName, 1, 0)        // Create a unique name.
                  endif
                  // If there is no type conflict then we will overwrite the existing wave.
               else
                  // The conflict is with another type of object. Generate a unique name.
                  wName = UniqueName(wName, 1, 0)           // Create a unique name.
               endif
            endif
            
            // Make the output wave with the right data type and number of points. Then get the data from the TDM file.
            switch(dataType)	// The TDM data type codes are defined in the nilibddc.h file which is part of the NI DIAdem Connectivity Library.
               case 5:              // Unsigned byte
                  Make/O/B/U/N=(numPoints) $wName
                  Wave w = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, w)
                  break
               
               case 2:              // 16-bit signed integer
                  Make/O/W/N=(numPoints) $wName
                  Wave w = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, w)
                  break
               
               case 3:              // 32-bit signed integer
                  Make/O/I/N=(numPoints) $wName
                  Wave w = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, w)
                  break
                  
               case 9:              // Single-precision floating point
                  Make/O/N=(numPoints) $wName
                  Wave w = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, w)
                  break
                  
               case 10:             // Double-precision floating point
                  Make/O/D/N=(numPoints) $wName
                  Wave w = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, w)
                  break
               
               case 23:             // String
                  Make/O/T/N=(numPoints) $wName
                  Wave tw = $wName
                  tdmResult = TDMGetDataValues(channelH, 0, numPoints, tw)
                  break
                  
               case 30:             // Timestamp
                  wName = ""
                  Printf " - Skipping timestamp channel to keep the demo simple."
                  break				
            endswitch
            AbortOnValue tdmResult, 1
            
            if (strlen(wName) > 0)
               Printf " - Created wave %s.", wName
            endif
            Printf "\r"             // CR
         endfor
         
         SetDataFolder ::           // Back to the file-level data folder.		
      endfor	
   catch
      if (tdmResult != 0)
         String errorMessage = "TDM Library Error: " + TDMGetLibraryErrorDescription(tdmResult)
         DoAlert 0, errorMessage
      endif
   endtry

   if (fileH != 0)
      TDMCloseFile(fileH)        // This also closes all group and channel handles.
   endif

   KillWaves/Z tempTDMGroups, tempTDMChannels

   SetDataFolder origDFSave

   return tdmResult
End
```

## TDM XOP Functions Versus DIAdem Library Functions {#tdm-xop-functions-versus-diadem-library-functions}

The name of each TDM XOP function starts with TDM. Most of the TDM XOP functions have the same name as the corresponding DIAdem library function except that the DIAdem function names start with DDC_ instead of TDM. However, this rule is sometimes bended because of Igor's 31 character limit on function names, as explained in the following paragraphs.

DIAdem library function names that end with "TimestampComponents" are mapped to XOP functions that end with "Time" to fit in Igor's 31 character limit. For example, the DIAdem library DDC_SetDataValuesTimestampComponents routine is mapped to the [TDMSetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavaluestime) TDM XOP routine.

DIAdem library function names that contain "ChannelGroup" are mapped to TDM XOP functions that contain "Group" to fit in Igor's 31 character limit. For example, the DIAdem library function DDC_GetChannelGroupPropertyType is mapped to the TDM XOP function [TDMGetGroupPropertyType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytype).

The DIAdem library functions names that end with "Length" are mapped to TDM XOP functions that end with "Len" to fit in Igor's 31 character limit. For example, the DIAdem library function DDC_GetFileStringPropertyLength is mapped to the TDM XOP function [TDMGetFileStringPropertyLen](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilestringpropertylen).

In addition to name changes, there are other differences between the DIAdem library functions and the TDM XOP functions.
DIAdem library functions that get or set properties map to two separate TDM XOP functions - one for numeric properties and another for string properties. For example, the DIAdem library DDC_SetFileProperty function maps to the TDM XOP [TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum) for numeric properties and to the [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr) for string properties.

The DIAdem library functions that create a property include a parameter to set the initial value of the property. The corresponding TDM XOP functions omit this parameter. Consequently, you must create the property and then set its value in a subsequent step. For example, call [TDMCreateFileProperty](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefileproperty) followed by [TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum), [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr) or [TDMSetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertytime).

The DIAdem library functions that return property names (e.g., DDC_GetFilePropertyNames) include a "numPropertyNames" parameter. The corresponding TDM XOP (e.g., TDMGetFilePropertyNames) function does not have this parameter and instead returns a semicolon-separated list of all property names.

To read and write timestamp data, use [TDMGetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavaluestime) and [TDMSetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavaluestime), not [TDMGetDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavalues) and [TDMSetDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavalues).

To read and write file, channel group and channel timestamp properties, use [TDMGetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertytime) and [TDMSetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertytime), [TDMGetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytime) and [TDMSetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertytime), [TDMGetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertytime) and [TDMSetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertytime).

## DIAdem Library Data Type Codes {#diadem-library-data-type-codes}

Some TDM XOP functions require or return DIAdem library data type codes defined in nilibddc.h. Here is Igor code to define the DIAdem data type codes:

```igor
static Constant kTDMDataTypeUInt8 = 5
static Constant kTDMDataTypeInt16 = 2
static Constant kTDMDataTypeInt32 = 3
static Constant kTDMDataTypeFloat = 9
static Constant kTDMDataTypeDouble = 10
static Constant kTDMDataTypeString = 23
static Constant kTDMDataTypeTimestamp = 30
```

### *TDM XOP Object Management Functions* {#tdm-xop-object-management-functions}

|  |  |  |
| --- | --- | --- |
| [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile) | [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) | [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex) |
| [TDMSaveFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavefile) | [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile) |  |
| [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) | [TDMRemoveGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmremovegroup) | [TDMCloseGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosegroup) |
| [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) | [TDMRemoveChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmremovechannel) | [TDMCloseChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosechannel) |

### *TDM XOP Data Storage Functions* {#tdm-xop-data-storage-functions}

|  |  |  |
| --- | --- | --- |
| [TDMGetDataType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatatype) | [TDMGetNumGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumgroups) | [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups) |
| [TDMGetNumChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumchannels) | [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels) |  |
| [TDMGetNumDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumdatavalues) | [TDMGetDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavalues) | [TDMGetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavaluestime) |
| [TDMSetDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavalues) | [TDMAppendDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmappenddatavalues) | [TDMReplaceDataValues](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmreplacedatavalues) |
| [TDMSetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavaluestime) | [TDMAppendDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmappenddatavaluestime) | [TDMReplaceDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmreplacedatavaluestime) |

### *TDM XOP File Property Functions* {#tdm-xop-file-property-functions}

|  |  |  |
| --- | --- | --- |
| [TDMCreateFileProperty](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefileproperty) |  |  |
| [TDMGetNumFileProperties](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumfileproperties) | [TDMGetFilePropertyNames](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertynames) |  |
| [TDMFilePropertyExists](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmfilepropertyexists) | [TDMGetFilePropertyType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertytype) | [TDMGetFileStringPropertyLen](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilestringpropertylen) |
| [TDMGetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertynum) | [TDMGetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertystr) | [TDMGetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertytime) |
| [TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum) | [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr) | [TDMSetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertytime) |

### *TDM XOP Channel Group Property Functions* {#tdm-xop-channel-group-property-functions}

|  |  |
| --- | --- |
| [TDMCreateGroupProperty](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreategroupproperty) |  |
| [TDMGetNumGroupProperties](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumgroupproperties) | [TDMGetGroupPropertyNames](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertynames) |
| [TDMGroupPropertyExists](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgrouppropertyexists) | [TDMGetGroupPropertyType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytype)    [TDMGetGroupStringPropertyLen](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroupstringpropertylen) |
| [TDMGetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertynum) | [TDMGetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertystr)       [TDMGetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytime) |
| [TDMSetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertynum) | [TDMSetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertystr)       [TDMSetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertytime) |

### *TDM XOP Channel Property Functions* {#tdm-xop-channel-property-functions}

|  |  |
| --- | --- |
| [TDMCreateChannelProperty](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatechannelproperty) |  |
| [TDMGetNumChannelProperties](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumchannelproperties)   [TDMGetChannelPropertyNames](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertynames) |  |
| [TDMChannelPropertyExists](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmchannelpropertyexists)         [TDMGetChannelPropertyType](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertytype)     [TDMGetChannelStringPropertyLen](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelstringpropertylen) |  |
| [TDMGetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertynum)     [TDMGetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertystr)        [TDMGetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertytime) |  |
| [TDMSetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertynum)     [TDMSetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertystr)        [TDMSetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertytime) |  |

### *TDM XOP Miscellaneous Property Functions* {#tdm-xop-miscellaneous-property-functions}

|  |  |
| --- | --- |
| [TDMGetLibraryErrorDescription](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetlibraryerrordescription) |  |

## TDM XOP Functions {#tdm-xop-functions}

This section documents the TDM XOP functions. See [TDM XOP Function Example](#tdm-xop-function-example) for an example and Background Information for pointers to further documentation on TDM and the DIAdem Connectivity Library.
<br>

<div className="command-signature">

### <strong>TDMCreateFile</strong> (<em>filePathStr</em>, <em>fileTypeStr</em>, <em>nameStr</em>, <em>descriptionStr</em>, <em>titleStr</em>, <em>authorStr</em>, <em>fileH</em> ) {#tdmcreatefile}

</div>

TDMCreateFile creates a TDM or TDMS file.

#### *Parameters* {#tdm-xop-functions-parameters}
*filePathStr*  is the full Macintosh HFS or Windows-style path to the file to be created. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh HFS and Windows paths. *filePathStr*  should have a .tdm or .tdms extension.

*fileTypeStr*  is "TDM" to create a TDM file, "TDMS" to create a TDMS file, or "" to determine the file type by the file name extension in *filePathStr* .

*nameStr*  is the value for the file-level name property.

*descriptionStr*  is the value for the file-level description property.

*titleStr*  is the value for the file-level title property.

*authorStr*  is the value for the file-level author property.

*fileH*  is a pass-by-reference numeric output parameter. If TDMCreateFile succeeds, the handle to the created file is returned in *fileH*.

#### *Details* {#tdm-xop-functions-details}
TDMCreateFile returns an error if the file already exists. If you want to overwrite the file, call [DeleteFile](/igorpro/commands/deletefile.md)/Z before TDMCreateFile.

Call [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile) to close the file. Call [TDMSaveFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavefile) to save the file.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMOpenFile</strong> (<em>filePathStr</em>, <em>fileTypeStr</em> , <em>fileH</em> ) {#tdmopenfile}

</div>

Opens an existing TDM or TDMS file.

#### *Parameters* {#tdm-xop-functions-parameters}
*filePathStr*  is the full Macintosh HFS or Windows-style path to the file to be created. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh HFS and Windows paths. *filePathStr*  should have a .tdm or .tdms extension.

*fileTypeStr*  is "TDM" to open a TDM file, "TDMS" to open a TDMS file, or "" to determine the file type by the file name extension in *filePathStr* .

*fileH*  is a pass-by-reference numeric output parameter. If TDMOpenFile succeeds, the handle to the created file is returned in *fileH* .

#### *Details* {#tdm-xop-functions-details}
To open the file for read only, use [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

Call [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile) to close the file. Call [TDMSaveFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavefile) to save the file if you write to it.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.

#### *See Also* {#tdm-xop-functions-see-also}
[TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex)





<div className="command-signature">

### <strong>TDMOpenFileEx</strong> (<em>filePathStr</em>, <em>fileTypeStr</em>, <em>readOnly</em>, <em>fileH</em> ) {#tdmopenfileex}

</div>

Opens an existing TDM or TDMS file for read/write or read only.

#### *Parameters* {#tdm-xop-functions-parameters}
*filePathStr*  is the full Macintosh HFS or Windows-style path to the file to be created. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details about Macintosh HFS and Windows paths. *filePathStr*  should have a .tdm or .tdms extension.

*fileTypeStr*  is "TDM" to open a TDM file, "TDMS" to open a TDMS file, or "" to determine the file type by the file name extension in *filePathStr* .

*readOnly*  is 1 to open for read only or 0 to open for read/write.

*fileH*  is a pass-by-reference numeric output parameter. If TDMOpenFile succeeds, the handle to the created file is returned in *fileH* .

#### *Details* {#tdm-xop-functions-details}
Call [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile) to close the file. Call [TDMSaveFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavefile) to save the file if you write to it.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMSaveFile</strong> (<em>fileH</em> ) {#tdmsavefile}

</div>

Saves changes made to the file identified by fileH.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMCloseFile</strong> (<em>fileH</em> ) {#tdmclosefile}

</div>

Closes the file identified by fileH.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMAddGroup</strong> (<em>fileH</em>, <em>nameStr</em>, <em>descriptionStr</em>, <em>groupH</em> ) {#tdmaddgroup}

</div>

Adds a channel group to a file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*nameStr*  is the value for the channel group name property.

*descriptionStr*  is the value for the channel group description property.

*groupH*  is a pass-by-reference numeric output parameter. If TDMAddGroup succeeds, the handle to the created group is returned in *groupH*.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMRemoveGroup</strong> (<em>groupH</em> ) {#tdmremovegroup}

</div>

Removes the specified channel group from its file.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMCloseGroup</strong> (<em>groupH</em> ) {#tdmclosegroup}

</div>

Closes the specified channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

#### *Details* {#tdm-xop-functions-details}
You don't need to explicitly close a channel group as it will be closed when you call [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMAddChannel</strong> (<em>groupH</em>, <em>dataType</em> , <em>nameStr</em>, <em>descriptionStr</em>, <em>unitStr</em>, <em>channelH</em> ) {#tdmaddchannel}

</div>

Adds a channel to a channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*dataType*  is a DIAdem library data type code for the channel. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

*nameStr*  is the value for the channel name property.

*descriptionStr*  is the value for the channel description property.

*channelH*  is a pass-by-reference numeric output parameter. If TDMAddChannel succeeds, the handle to the created channel is returned in *channelH*.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMRemoveChannel</strong> (<em>channelH</em> ) {#tdmremovechannel}

</div>

Removes the specified channel from its group.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMCloseChannel</strong> (<em>channelH</em> ) {#tdmclosechannel}

</div>

Closes the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

#### *Details* {#tdm-xop-functions-details}
You don't need to explicitly close a channel as it will be closed when you call [TDMCloseFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmclosefile).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetDataType</strong> (<em>channelH</em>, <em>dataType</em> ) {#tdmgetdatatype}

</div>

Gets the DIAdem library data type code for the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*dataType*  is an pass-by-reference numeric output parameter which is set to the DIAdem library data type code for the channel. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetNumGroups</strong> (<em>fileH</em>, <em>numGroups</em> ) {#tdmgetnumgroups}

</div>

Gets the number of channel groups in the file referenced by fileH.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*numGroups*  is a pass-by-reference numeric output parameter which is set to the number of channel groups in the file.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetGroups</strong> (<em>fileH</em>, <em>groupsWave</em>, <em>numGroupsToGet</em> ) {#tdmgetgroups}

</div>

Gets handles for channel groups in the specified file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*groupsWave*  is a double-precision floating point wave which receives the channel group handles. This wave must have at least *numGroupsToGet*  points.

*numGroupsToGet*  is the number of channel group handles to get. Usually you will obtain this from [TDMGetNumGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumgroups).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetNumChannels</strong> (<em>groupH</em>, <em>numChannels</em> ) {#tdmgetnumchannels}

</div>

Gets the number of channels in the channel group referenced by groupH.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*numChannels*  is a pass-by-reference numeric output parameter which is set to the number of channels in the group.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetChannels</strong> (<em>groupH</em>, <em>channelsWave</em>, <em>numChannelsToGet</em> ) {#tdmgetchannels}

</div>

Gets handles for channels in the specified group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*channelsWave*  is a double-precision floating point wave which receives the channel handles. This wave must have at least *numChannelsToGet*  points.

*numChannelsToGet*  is the number of channel handles to get. Usually you will obtain this from [TDMGetNumChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetnumchannels).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.





<div className="command-signature">

### <strong>TDMGetNumDataValues</strong> (<em>channelH</em>, <em>numDataValues</em> ) {#tdmgetnumdatavalues}

</div>

Gets the number of data values in the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*numDataValues*  is a pass-by-reference numeric output parameter which is set to the number of data values in the specified channel.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetDataValues</strong> (<em>channelH</em>, <em>indexOfFirstValueToGet</em>, <em>numDataValuesToGet</em>, <em>dataWave</em> ) {#tdmgetdatavalues}

</div>

Stores the data values from the specified channel in *dataWave .*

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*indexOfFirstValueToGet*  is the zero-based index of the first data value to get.

*numDataValuesToGet*  is the number of data values to get.

*dataWave*  is the wave into which the data values are to be stored. The wave must have the same data type as the channel and must have at least *numDataValuesToGet*  points. See [TDM XOP Function Example](#tdm-xop-function-example) for an example of creating an appropriate wave for a given channel.

#### *Details* {#tdm-xop-functions-details}
Use this function for numeric or string channels. Use [TDMGetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavaluestime) for timestamp channels.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details

#### *See Also* {#tdm-xop-functions-see-also}
[TDM XOP Function Example](#tdm-xop-function-example), [TDMGetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetdatavaluestime)





<div className="command-signature">

### <strong>TDMGetDataValuesTime</strong> (<em>channelH</em>, <em>indexOfFirstValueToGet</em>, <em>numDataValuesToGet</em>, <em>yearWave</em>, <em>monthWave</em>, <em>dayWave</em>, <em>hourWave</em>, <em>minuteWave</em>, <em>secondWave</em>, <em>millisecondWave</em>, <em>weekDayWave</em> ) {#tdmgetdatavaluestime}

</div>

Gets timestamp data from a timestamp channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*indexOfFirstValueToGet*  is the zero-based index of the first data value to get.

*numDataValuesToGet*  is the number of data values to get.

*yearWave*  is an unsigned integer wave to receive the year component of the timestamp.

*monthWave*  is an unsigned integer wave to receive the month component.

*dayWave*  is an unsigned integer wave to receive the day component.

*hourWave*  is an unsigned integer wave to receive the hour component.

*minuteWave*  is an unsigned integer wave to receive the minute component.

*secondWave*  is an unsigned integer wave to receive the second component.

*millisecondWave*  is a double-precision floating point wave to receive the millisecond component.

*weekDayWave*  is an unsigned integer wave to receive the day-of-week value associated with the timestamp.

#### *Details* {#tdm-xop-functions-details}
All of the output waves must have the right data type and at least *numDataValuesToGet* points.

Note that all output waves are unsigned integer (e.g., Make/U/I) except for *millisecondWave* which is double-precision floating point (Make/D).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetDataValues</strong> (<em>channelH</em>, <em>dataWave</em>, <em>numDataValuesToSet</em> ) {#tdmsetdatavalues}

</div>

Stores the data values from *dataWave* in the specified channel*.*

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*dataWave*  is the wave containing the data to be stored in the channel. The wave must have the same data type as the channel and must have at least *numDataValuesToSet*  points.

*numDataValuesToSet*  is the number of data values to store in the channel.

#### *Details* {#tdm-xop-functions-details}
Point 0 of *dataWave* is the source of the first data value stored in the channel.

Use this function for numeric or string channels. Use [TDMSetDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetdatavaluestime) for timestamp channels.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMAppendDataValues</strong> (<em>channelH</em>, <em>dataWave</em>, <em>numDataValuesToAppend</em> ) {#tdmappenddatavalues}

</div>

Appends the data values from *dataWave* to the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH* is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*dataWave* is the wave containing the data to be appended to the channel. The wave must have the same data type as the channel and must have at least *numDataValuesToAppend*  points.

*numDataValuesToAppend* is the number of data values to append to the channel.

#### *Details* {#tdm-xop-functions-details}
Point 0 of *dataWave* is source of the first data value appended to the channel.

Use this function for numeric or string channels. Use [TDMAppendDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmappenddatavaluestime) for timestamp channels.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMReplaceDataValues</strong> (<em>channelH</em>, <em>indexOfFirstValueToReplace</em>, <em>dataWave</em>, <em>numDataValuesToReplace</em> ) {#tdmreplacedatavalues}

</div>

Replaces the data values from *dataWave* in the specified channel*.*

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*indexOfFirstValueToReplace*  is the zero-based index of the first value in *channelH*  to be replaced.

*dataWave*  is the wave containing the data to replace data in the channel. The wave must have the same data type as the channel and must have at least *numDataValuesToReplace*  points.

*numDataValuesToReplace*  is the number of data values to replace in the channel.

#### *Details* {#tdm-xop-functions-details}
Replacing is not supported for data that has already been saved to a TDMS (streaming) file.

Point 0 of *dataWave* is the source of the first replacement data value for the channel.

Use this function for numeric or string channels. Use [TDMReplaceDataValuesTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmreplacedatavaluestime) for timestamp channels.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetDataValuesTime</strong> (<em>channelH</em>, <em>yearWave</em>, <em>monthWave</em>, <em>dayWave</em>, <em>hourWave</em>, <em>minuteWave</em>, <em>secondWave</em>, <em>millisecondWave</em>, <em>numDataValuesToSet</em> ) {#tdmsetdatavaluestime}

</div>

Sets timestamp data in a timestamp channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*yearWave*  is an unsigned integer wave containing the year component of the timestamp.

*monthWave*  is an unsigned integer wave containing the month component.

*dayWave*  is an unsigned integer wave containing the day component.

*hourWave*  is an unsigned integer wave containing the hour component.

*minuteWave*  is an unsigned integer wave containing the minute component.

*secondWave*  is an unsigned integer wave containing the second component.

*millisecondWave*  is a double-precision floating point wave containing the millisecond component.

*numDataValuesToSet*  is the number of data values to set in the channel.

#### *Details* {#tdm-xop-functions-details}
All of the input waves must have the right data type and at least *numDataValuesToSet* points.

Note that all input waves are unsigned integer (e.g., Make/U/I) except for *millisecondWave* which is double-precision floating point (Make/D).

Point 0 of the input waves is the source of the first data value for the channel.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMAppendDataValuesTime</strong> (<em>channelH</em>, <em>yearWave</em>, <em>monthWave</em>, <em>dayWave</em>, <em>hourWave</em>, <em>minuteWave</em>, <em>secondWave</em>, <em>millisecondWave</em>, <em>numDataValuesToAppend</em> ) {#tdmappenddatavaluestime}

</div>

Appends timestamp data in a timestamp channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*yearWave*  is an unsigned integer wave containing the year component of the timestamp.

*monthWave*  is an unsigned integer wave containing the month component.

*dayWave*  is an unsigned integer wave containing the day component.

*hourWave*  is an unsigned integer wave containing the hour component.

*minuteWave*  is an unsigned integer wave containing the minute component.

*secondWave*  is an unsigned integer wave containing the second component.

*millisecondWave*  is a double-precision floating point wave containing the millisecond component.

*numDataValuesToAppend*  is the number of data values to append to the channel.

#### *Details* {#tdm-xop-functions-details}
All of the input waves must have the right data type and at least *numDataValuesToAppend* points.

Note that all input waves are unsigned integer (e.g., Make/U/I) except for *millisecondWave* which is double-precision floating point (Make/D).

Point 0 of the input waves is the source of the first data value to append to the channel.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMReplaceDataValuesTime</strong> (<em>channelH</em>, <em>indexOfFirstDataValueToReplace</em>, <em>yearWave</em>, <em>monthWave</em>, <em>dayWave</em>, <em>hourWave</em>, <em>minuteWave</em>, <em>secondWave</em>, <em>millisecondWave</em>, <em>numDataValuesToReplace</em> ) {#tdmreplacedatavaluestime}

</div>

Replaces timestamp data in a timestamp channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*indexOfFirstValueToReplace*  is the zero-based index of the first value in *channelH*  to be replaced.

*yearWave*  is an unsigned integer wave containing the year component of the timestamp.

*monthWave*  is an unsigned integer wave containing the month component.

*dayWave*  is an unsigned integer wave containing the day component.

*hourWave*  is an unsigned integer wave containing the hour component.

*minuteWave*  is an unsigned integer wave containing the minute component.

*secondWave*  is an unsigned integer wave containing the second component.

*millisecondWave*  is a double-precision floating point wave containing the millisecond component.

*numDataValuesToReplace*  is the number of data values to replace in the channel.

#### *Details* {#tdm-xop-functions-details}
All of the input waves must have the right data type and at least *numDataValuesToReplace* points.

Note that all input waves are unsigned integer (e.g., Make/U/I) except for *millisecondWave* which is double-precision floating point (Make/D).

Point 0 of the input waves is the source of the first replacement data value for the channel.

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details.



<div className="command-signature">

### <strong>TDMCreateFileProperty</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmcreatefileproperty}

</div>

Creates a new property for the specified file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  is the name of the property to create.

*dataType*  is the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetNumFileProperties</strong> (<em>fileH</em>, <em>numProperties</em> ) {#tdmgetnumfileproperties}

</div>

Gets the number of properties associated with the specified file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*numProperties*  is a pass-by-reference numeric output parameter which is set to the number of properties on the specified file.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFilePropertyNames</strong> (<em>fileH</em>, <em>propertyNamesStr</em> ) {#tdmgetfilepropertynames}

</div>

Gets a semicolon-separated list the names of the properties associated with the specified file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNamesStr*  is a pass-by-reference string output parameter which is set to a semicolon-separated list of property names for the specified file.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMFilePropertyExists</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>exists</em> ) {#tdmfilepropertyexists}

</div>

Tells you if a property with the specified name exists on the file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*exists*  is a pass-by-reference numeric output parameter which is set to 1 if the property exists and 0 if it does not.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFilePropertyType</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmgetfilepropertytype}

</div>

Gets the DIAdem library data type code for the specified file property.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*dataType*  is a pass-by-reference numeric output parameter which is set to the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFileStringPropertyLen</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>length</em> ) {#tdmgetfilestringpropertylen}

</div>

Gets the length of the value of a string property of the specified file.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*length*  is a pass-by-reference numeric output parameter which is set to the number of characters in the value of the specified file property.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFilePropertyNum</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmgetfilepropertynum}

</div>

Gets the specified file numeric property.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*value* is a pass-by-reference numeric output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a string file property, use [TDMGetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertystr). To get the value of a timestamp file property, use [TDMGetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFilePropertyStr</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmgetfilepropertystr}

</div>

Gets the specified file string property.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*valueStr* is a pass-by-reference string output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a numeric file property, use [TDMGetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertynum). To get the value of a timestamp file property, use [TDMGetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetFilePropertyTime</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em>, <em>weekDay</em> ) {#tdmgetfilepropertytime}

</div>

Gets the specified file timestamp property.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*year*  is a pass-by-reference numeric output parameter which receives the year component of the timestamp.

*month*  is a pass-by-reference numeric output parameter which receives the month component.

*day*  is a pass-by-reference numeric output parameter which receives the day component.

*hour*  is a pass-by-reference numeric output parameter which receives the hour component.

*minute*  is a pass-by-reference numeric output parameter which receives the minute component.

*second*  is a pass-by-reference numeric output parameter which receives the second component.

*millisecond*  is a pass-by-reference numeric output parameter which receives the millisecond component.

*weekDay*  is a pass-by-reference numeric output parameter which receives the day-of-week value associated with the timestamp.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second*, *millisecond* and *dayOfWeek*  are numeric values.

To get the value of a numeric file property, use [TDMGetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertynum). To get the value of a string file property, use [TDMGetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetfilepropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetFilePropertyNum</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmsetfilepropertynum}

</div>

Sets the specified file numeric property to the specified numeric value.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*value* is the numeric value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a string file property, use [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr). To set the value of a timestamp file property, use [TDMSetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetFilePropertyStr</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmsetfilepropertystr}

</div>

Sets the specified file string property to the specified string value.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*valueStr*  is the string value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a numeric file property, use [TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum). To set the value of a timestamp file property, use [TDMSetFilePropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetFilePropertyTime</strong> (<em>fileH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em> ) {#tdmsetfilepropertytime}

</div>

Sets the specified file timestamp property to the specified value.

#### *Parameters* {#tdm-xop-functions-parameters}
*fileH*  is a file handle obtained from [TDMCreateFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmcreatefile), [TDMOpenFile](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfile) or [TDMOpenFileEx](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmopenfileex).

*propertyNameStr*  contains the name of the property of interest.

*year*  is the year component of the timestamp.

*month*  is the month component.

*day*  is the day component.

*hour*  is the hour component.

*minute*  is the minute component.

*second*  is the second component.

*millisecond*  is the millisecond component.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second and millisecond*  are numeric values.

To set the value of a numeric file property, use [TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum). To set the value of a string file property, use [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details

#### *See Also* {#tdm-xop-functions-see-also}
[TDMSetFilePropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertynum), [TDMSetFilePropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetfilepropertystr)





<div className="command-signature">

### <strong>TDMCreateGroupProperty</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmcreategroupproperty}

</div>

Creates a new property for the specified channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  is the name of the property to create.

*dataType*  is the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetNumGroupProperties</strong> (<em>groupH</em>, <em>numProperties</em> ) {#tdmgetnumgroupproperties}

</div>

Gets the number of properties associated with the specified channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*numProperties*  is a pass-by-reference numeric output parameter which is set to the number of properties on the specified channel group.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupPropertyNames</strong> (<em>groupH</em>, <em>propertyNamesStr</em> ) {#tdmgetgrouppropertynames}

</div>

Gets a semicolon-separated list the names of the properties associated with the specified channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNamesStr*  is a pass-by-reference string output parameter which is set to a semicolon-separated list of property names for the specified channel group.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGroupPropertyExists</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>exists</em> ) {#tdmgrouppropertyexists}

</div>

Tells you if a property with the specified name exists on the channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*exists*  is a pass-by-reference numeric output parameter which is set to 1 if the property exists and 0 if it does not.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupPropertyType</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmgetgrouppropertytype}

</div>

Gets the DIAdem library data type code for the specified channel group property.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*dataType*  is a pass-by-reference numeric output parameter which is set to the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupStringPropertyLen</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>length</em> ) {#tdmgetgroupstringpropertylen}

</div>

Gets the length of the value of a string property of the specified channel group.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*length*  is a pass-by-reference numeric output parameter which is set to the number of characters in the value of the specified channel group property.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupPropertyNum</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmgetgrouppropertynum}

</div>

Gets the specified channel group numeric property.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*value* is a pass-by-reference numeric output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a string channel group property, use [TDMGetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertystr). To get the value of a timestamp channel group property, use [TDMGetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupPropertyStr</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmgetgrouppropertystr}

</div>

Gets the specified channel group string property.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*valueStr* is a pass-by-reference string output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a numeric channel group property, use [TDMGetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertynum). To get the value of a timestamp channel group property, use [TDMGetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetGroupPropertyTime</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em>, <em>weekDay</em> ) {#tdmgetgrouppropertytime}

</div>

Gets the specified channel group timestamp property.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*year*  is a pass-by-reference numeric output parameter which receives the year component of the timestamp.

*month*  is a pass-by-reference numeric output parameter which receives the month component.

*day*  is a pass-by-reference numeric output parameter which receives the day component.

*hour*  is a pass-by-reference numeric output parameter which receives the hour component.

*minute*  is a pass-by-reference numeric output parameter which receives the minute component.

*second*  is a pass-by-reference numeric output parameter which receives the second component.

*millisecond*  is a pass-by-reference numeric output parameter which receives the millisecond component.

*weekDay*  is a pass-by-reference numeric output parameter which receives the day-of-week value associated with the timestamp.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second*, *millisecond* and *dayOfWeek*  are numeric values.

To get the value of a numeric channel group property, use [TDMGetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertynum). To get the value of a string channel group property, use [TDMGetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgrouppropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetGroupPropertyNum</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmsetgrouppropertynum}

</div>

Sets the specified channel group numeric property to the specified numeric value.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*value* is the numeric value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a string channel group property, use [TDMSetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertystr). To set the value of a timestamp channel group property, use [TDMSetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetGroupPropertyStr</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmsetgrouppropertystr}

</div>

Sets the specified channel group string property to the specified string value.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*valueStr*  is the string value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a numeric channel group property, use [TDMSetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertynum). To set the value of a timestamp channel group property, use [TDMSetGroupPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetGroupPropertyTime</strong> (<em>groupH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em> ) {#tdmsetgrouppropertytime}

</div>

Sets the specified channel group timestamp property to the specified value.

#### *Parameters* {#tdm-xop-functions-parameters}
*groupH*  is a channel group handle obtained from [TDMAddGroup](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddgroup) or [TDMGetGroups](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetgroups).

*propertyNameStr*  contains the name of the property of interest.

*year*  is the year component of the timestamp.

*month*  is the month component.

*day*  is the day component.

*hour*  is the hour component.

*minute*  is the minute component.

*second*  is the second component.

*millisecond*  is the millisecond component.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second and millisecond*  are numeric values.

To set the value of a numeric channel group property, use [TDMSetGroupPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertynum). To set the value of a string channel group property, use [TDMSetGroupPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetgrouppropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMCreateChannelProperty</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmcreatechannelproperty}

</div>

Creates a new property for the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  is the name of the property to create.

*dataType*  is the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetNumChannelProperties</strong> (<em>channelH</em>, <em>numProperties</em> ) {#tdmgetnumchannelproperties}

</div>

Gets the number of properties associated with the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*numProperties*  is a pass-by-reference numeric output parameter which is set to the number of properties on the specified channel.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelPropertyNames</strong> (<em>channelH</em>, <em>propertyNamesStr</em> ) {#tdmgetchannelpropertynames}

</div>

Gets a semicolon-separated list the names of the properties associated with the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNamesStr*  is a pass-by-reference string output parameter which is set to a semicolon-separated list of property names for the specified channel.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMChannelPropertyExists</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>exists</em> ) {#tdmchannelpropertyexists}

</div>

Tells you if a property with the specified name exists on the channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*exists*  is a pass-by-reference numeric output parameter which is set to 1 if the property exists and 0 if it does not.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelPropertyType</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>dataType</em> ) {#tdmgetchannelpropertytype}

</div>

Gets the DIAdem library data type code for the specified channel property.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*dataType*  is a pass-by-reference numeric output parameter which is set to the DIAdem library data type code for the new property. See [DIAdem Library Data Type Codes](#diadem-library-data-type-codes).

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelStringPropertyLen</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>length</em> ) {#tdmgetchannelstringpropertylen}

</div>

Gets the length of the value of a string property of the specified channel.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*length*  is a pass-by-reference numeric output parameter which is set to the number of characters in the value of the specified channel property.

#### *Details* {#tdm-xop-functions-details}
The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelPropertyNum</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmgetchannelpropertynum}

</div>

Gets the specified channel numeric property.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*value* is a pass-by-reference numeric output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a string channel property, use [TDMGetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertystr). To get the value of a timestamp channel property, use [TDMGetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelPropertyStr</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmgetchannelpropertystr}

</div>

Gets the specified channel string property.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*valueStr* is a pass-by-reference string output parameter which receives the property's value.

#### *Details* {#tdm-xop-functions-details}
To get the value of a numeric channel property, use [TDMGetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertynum). To get the value of a timestamp channel property, use [TDMGetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetChannelPropertyTime</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em>, <em>weekDay</em> ) {#tdmgetchannelpropertytime}

</div>

Gets the specified channel timestamp property.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*year*  is a pass-by-reference numeric output parameter which receives the year component of the timestamp.

*month*  is a pass-by-reference numeric output parameter which receives the month component.

*day*  is a pass-by-reference numeric output parameter which receives the day component.

*hour*  is a pass-by-reference numeric output parameter which receives the hour component.

*minute*  is a pass-by-reference numeric output parameter which receives the minute component.

*second*  is a pass-by-reference numeric output parameter which receives the second component.

*millisecond*  is a pass-by-reference numeric output parameter which receives the millisecond component.

*weekDay*  is a pass-by-reference numeric output parameter which receives the day-of-week value associated with the timestamp.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second*, *millisecond* and *dayOfWeek*  are numeric values.

To get the value of a numeric channel property, use [TDMGetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertynum). To get the value of a string channel property, use [TDMGetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannelpropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetChannelPropertyNum</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>value</em> ) {#tdmsetchannelpropertynum}

</div>

Sets the specified channel numeric property to the specified numeric value.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*value* is the numeric value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a string channel property, use [TDMSetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertystr). To set the value of a timestamp channel property, use [TDMSetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetChannelPropertyStr</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>valueStr</em> ) {#tdmsetchannelpropertystr}

</div>

Sets the specified channel string property to the specified string value.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*valueStr*  is the string value to which the property is to be set.

#### *Details* {#tdm-xop-functions-details}
To set the value of a numeric channel property, use [TDMSetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertynum). To set the value of a timestamp channel property, use [TDMSetChannelPropertyTime](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertytime).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMSetChannelPropertyTime</strong> (<em>channelH</em>, <em>propertyNameStr</em>, <em>year</em>, <em>month</em>, <em>day</em>, <em>hour</em>, <em>minute</em>, <em>second</em>, <em>millisecond</em> ) {#tdmsetchannelpropertytime}

</div>

Sets the specified channel timestamp property to the specified value.

#### *Parameters* {#tdm-xop-functions-parameters}
*channelH*  is a channel handle obtained from [TDMAddChannel](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmaddchannel) or [TDMGetChannels](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmgetchannels).

*propertyNameStr*  contains the name of the property of interest.

*year*  is the year component of the timestamp.

*month*  is the month component.

*day*  is the day component.

*hour*  is the hour component.

*minute*  is the minute component.

*second*  is the second component.

*millisecond*  is the millisecond component.

#### *Details* {#tdm-xop-functions-details}
*year*, *month*, *day*, *hour*, *minute*, *second and millisecond*  are numeric values.

To set the value of a numeric channel property, use [TDMSetChannelPropertyNum](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertynum). To set the value of a string channel property, use [TDMSetChannelPropertyStr](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsetchannelpropertystr).

The function result is a DIAdem library result code or 0 if there was no error. See [TDM XOP Function Result Codes](#tdm-xop-function-result-codes) for details





<div className="command-signature">

### <strong>TDMGetLibraryErrorDescription</strong> (<em>errorCode</em> ) {#tdmgetlibraryerrordescription}

</div>

Returns an error string corresponding to the specified DIAdem library error code.

#### *Parameters* {#tdm-xop-functions-parameters}
*errorCode*  is a DIAdem library error code returned by a TDM XOP function.

#### *Details* {#tdm-xop-functions-details}
The function result is a string containing the error message corresponding to the error code. Use this to display a human-readable error message to the user.