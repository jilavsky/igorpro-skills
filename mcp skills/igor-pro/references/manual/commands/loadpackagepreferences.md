---
description: "The LoadPackagePreferences operation loads preference data previously stored on disk by the SavePackagePreferences operation."
slug: /commands/loadpackagepreferences
---

<div className="command-signature">

## <strong>LoadPackagePreferences</strong>  [ /MIS=<em>mismatch</em>  /P=<em>pathName</em> ] <em>packageName</em> , <em>prefsFileName</em>, <em>recordID</em>, <em>prefsStruct</em> {#loadpackagepreferences}

</div>

The LoadPackagePreferences operation loads preference data previously stored on disk by the [SavePackagePreferences](/igorpro/commands/savepackagepreferences.md) operation. The data is loaded into the specified structure.

:::warning
The package preferences structure must not use fields of type Variable, String, WAVE, NVAR, SVAR or FUNCREF because these fields refer to data that may not exist when LoadPackagePreferences is called.
:::

If the /P flag is present then the location on disk of the preference file is determined by *pathName* and *prefsFileName* . However in the usual case the /P flag will be omitted and the preference file is located in a file named *prefsFileName* in a directory named *packageName* in the Packages directory in Igor's preferences directory.

:::warning
You must choose a very distinctive name for packageName as this is the only thing preventing collisions between your package and someone else's package. If you use a name longer than 31 bytes, your package will require Igor Pro 8.00 or later. 
:::

### *Parameters* {#parameters}
*packageName* is the name of your package of Igor procedures. It is limited to 31 bytes and must be a legal name for a directory on disk. This name must be very distinctive as this is the only thing preventing collisions between your package and someone else's package. If you use a name longer than 31 bytes, your package will require Igor Pro 8.00 or later.

*prefsFileName* is the name of a preference file to be loaded by LoadPackagePreferences. It should include an extension, typically ".bin".

*prefsStruct* is the structure into which data from disk, if it exists, will be loaded.

*recordID* is a unique positive integer that you assign to each record that you store in the preferences file. If you store more than one structure in the file, you would use distinct recordIDs to identify which structure you want to load. In the simple case you will store just one structure in the preference file and you can use 0 (or any positive integer of your choice) as the recordID.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/MIS = *mismatch*</span> | Controls what happens if the number of bytes in the file does not match the size of the structure: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Returns an error. This is the default behavior if /MIS is omitted.</td></tr><tr><td>1:</td><td>Returns the smaller of the size of the structure and the number of bytes in the file. Does not return an error. Use this if you want to read and update old versions of a preferences structure.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the directory to look in for the file specified by *prefsFileName.* |
|  | *pathName* is the name of an existing symbolic path. See [Symbolic Paths](/igorpro/igor-basics/experiments-files-and-folders.md#symbolic-paths) for details. |
|  | /P=$\<empty string variable\> acts as if the /P flag were omitted. |

### *Details* {#details}
LoadPackagePreferences sets the following output variables:

|  |  |
| --- | --- |
| V_flag | Set to 0 if no error occurred or to a nonzero error code. |
|  | If the preference file does not exist, V_flag is set to zero so you must use V_bytesRead to detect that case. |
| V_bytesRead | Set to the number of bytes read from the file. This will be zero if the preference file does not exist. |
| V_structSize | Set to the size in bytes of *prefsStruct*. This may be useful in handling structure version changes. |

After calling LoadPackagePreferences if V_flag is nonzero or V_bytesRead is zero then you need to create default preferences as illustrated by the example referenced below.

V_bytesRead, in conjunction with the /MIS flag, makes it possible to check for and deal with old versions of a preferences structure by checking the version field (typically the first field) of an older or newer version structure. However in most cases it is sufficient to omit the /MIS flag and treat incompatible preference data the same as missing preference data.

### *Examples* {#examples}
See the example under [Saving Package Preferences in a Special-Format Binary File](/igorpro/advanced-topics.md#saving-package-preferences-in-a-special-format-binary-file).

### *See Also* {#see-also}
[SavePackagePreferences](/igorpro/commands/savepackagepreferences.md)

### *Demos* {#demos}
[Open Package Preferences Demo](#igor-pxp/Examples/Programming/Package__Preferences__Demo.pxp)