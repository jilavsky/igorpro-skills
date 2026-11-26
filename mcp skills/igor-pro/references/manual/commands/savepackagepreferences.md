---
description: "The SavePackagePreferences operation saves preference data in the specified structure so that it can be accessed later via the LoadPackagePreferences operation."
slug: /commands/savepackagepreferences
---

<div className="command-signature">

## <strong>SavePackagePreferences</strong>  [ /FLSH=<em>flush</em>  /KILL /P=<em>pathName</em> ]   <em>packageName</em> , <em>prefsFileName</em>, <em>recordID</em> , <em>prefsStruct</em> {#savepackagepreferences}

</div>

The SavePackagePreferences operation saves preference data in the specified structure so that it can be accessed later via the [LoadPackagePreferences](/igorpro/commands/loadpackagepreferences.md) operation.

:::note
The package preferences structure must not use fields of type Variable, String, WAVE, NVAR, SVAR or FUNCREF because these fields refer to data that may not exist when LoadPackagePreferences is called.
:::

The structure can use fields of type char, uchar, int16, uint16, int32, uint32, int64, uint64, float and double as well as fixed-size arrays of these types  and substructures with fields of these types.

The data is stored in memory and by default flushed to disk when the current experiment is saved or closed and when Igor quits.

If the /P flag is present then the location on disk of the preference file is determined by *pathName* and *prefsFileName*. However in the usual case the /P flag will be omitted and the preference file is located in a file named *prefsFileName* in a directory named *packageName* in the Packages directory in Igor's preferences directory.

:::note
You must choose a very distinctive name for packageName  as this is the only thing preventing collisions between your package and someone else's package.
:::

See [Saving Package Preferences](/igorpro/advanced-topics.md#saving-package-preferences) for background information and examples.

### *Parameters* {#parameters}
*packageName* is the name of your package of Igor procedures. It is limited to 255 bytes and must be a legal name for a directory on disk. This name must be very distinctive as this is the only thing preventing collisions between your package and someone else's package.

*prefsFileName* is the name of a preference file to be saved by SavePackagePreferences. It should include an extension, typically ".bin".

*prefsStruct* is the structure containing the data to be saved in the preference file on disk.

*recordID* is a unique positive integer that you assign to each record that you store in the preferences file. If you store more than one structure in the file, you would use distinct recordIDs to identify which structure you want to save. In the simple case you will store just one structure in the preference file and you can use 0 (or any positve integer of your choice) as the recordID.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FLSH = *flush*</span> | Controls when the data is actually written to the preference file: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Data will be flushed to disk when the current experiment is saved, reverted or closed or when Igor quits. This is the default behavior used when /FLSH is omitted and is recommended for most purposes.</td></tr><tr><td>1:</td><td>Data is flushed to disk immediately.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/KILL</span> | Instead of saving *prefsStruct* under the specified record ID, that record is deleted from the package's preference if it exists. If it does not exist, nothing is done and no error is returned. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the directory in which to save the file specified by *prefsFileName*. |
|  | *pathName* is the name of an existing symbolic path. See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details. |
|  | /P=$<*empty string variable*> acts as if the /P flag were omitted. |

### *Details* {#details}
SavePackagePreferences sets the following output variables:


|  |  |
| --- | --- |
| V_flag | Set to 0 if preferences were successfully saved or to a nonzero error code if they were not saved. The latter case is unlikely and would indicate some kind of corruption such as if Igor's preferences directory were deleted. |
| V_structSize | Set to the size in bytes of *prefsStruct*. This may be useful in handling structure version changes. |

### *Examples* {#examples}
See the example under [Saving Package Preferences in a Special-Format Binary File](/igorpro/advanced-topics.md#saving-package-preferences-in-a-special-format-binary-file).

### *See Also* {#see-also}
[LoadPackagePreferences](/igorpro/commands/loadpackagepreferences.md)

### *Demos* {#demos}
[Open Package Preferences Demo](#igor-pxp/Examples/Programming/Package__Preferences__Demo.pxp)