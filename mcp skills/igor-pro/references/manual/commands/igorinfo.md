---
description: "The IgorInfo function returns information about the Igor application and the environment in which it is running."
slug: /commands/igorinfo
---

<div className="command-signature">

## <strong>IgorInfo</strong> (<em>selector</em>) {#igorinfo}

</div>

The IgorInfo function returns information about the Igor application and the environment in which it is running.

### *Details* {#details}
*selector* is a number from 0 to 18.

### *Selector = 0* {#selector-0}
If *selector* is 0, IgorInfo returns a collection of assorted information. The result string contains five kinds of information. Each group is prefaced by a keyword and a colon, and terminated with a semicolon.


| Keyword | Information Following Keyword For IgorInfo(0) |
| --- | --- |
| FREEMEM | The amount of free virtual memory available to Igor. |
| PHYSMEM | The amount of total physical memory available to Igor. Added in Igor Pro 7.00. |
| USEDPHYSMEM | The amount of used physical memory used by Igor. Added in Igor Pro 7.00. |
| IGORKIND | The type of Igor application: |
|  |<table class="nested-table"><tbody><tr><td>&quot;pro&quot;:</td><td>Igor Pro 32-bit</td></tr><tr><td>&quot;pro&nbsp;demo&quot;:</td><td>Igor Pro 32-bit in demo mode</td></tr><tr><td>&quot;pro64&quot;:</td><td>Igor Pro 64-bit</td></tr><tr><td>&quot;pro64&nbsp;demo&quot;:</td><td>Igor Pro 64-bit in demo mode</td></tr></tbody></table>
|  | "pro64" and "pro64 demo" are returned by the 64-bit version of Igor Pro 7.00 or later. |
|  | The presence of "demo" indicates that Igor is running in demo mode, either because the user's fully-functional demo period has expired or because the user chose to run in demo mode using the License dialog. |
| IGORVERS | The version number of the Igor application. Also see IGORFILEVERSION returned by IgorInfo(3). |
| NSCREENS | Number of screens currently attached to the computer and used for the desktop. |
| SCREEN1 | A description of the characteristics of  screen 1, the main screen on the system. |
|  | The format of the SCREEN1 description is: |
|  | SCREEN1:DEPTH=*bitsPerPixel*, RECT=*left*, *top*, *right*, *bottom*, SCALE=*scale*[, DEVICENAME=*deviceName*] ; |
|  | *left*, *top*, *right*, and *bottom* are all in pixels. |
|  | *scale* is the display's magnification value as an integer. *scale* will be 2 when you choose 200% for "Scale and layout" in the Display Settings control panel (this would be a normal choice for a high-res display). |
|  | SCALE was added in Igor Pro 10.00. |
|  | *deviceName* is the name of the screen, if known, typically "DISPLAY1", etc., else it is listed as "\_unknown\_". |
|  | If there are multiple screens, there will be additional SCREEN keywords, such as SCREEN2 and SCREEN3. |
|  | Note that in a two-display system, if Display 2 has "Make this my main display" checked, it will be listed as SCREEN1 with a DEVICENAME=DISPLAY2, and Display 1 will be listed as SCREEN2 with a DEVICENAME=DISPLAY1. |
|  | DEVICENAME was added in Igor Pro 10.00. |

### *Selector = 1* {#selector-1}
IgorInfo(1) returns the name of the current Igor experiment.

Use IgorInfo(12) to get the file name including the extension.

Use IgorInfo(17) to get the experiment's startup commands and recreation macros.

### *Selector = 2* {#selector-2}
IgorInfo(2) returns the name of the current platform: "Windows".

### *Selector = 3* {#selector-3}
IgorInfo(3) returns a collection of more detailed information about the operating system, localization information, and the actual file version of the Igor executable. The keywords are "OS", "OSVERSION", "LOCALE", and "IGORFILEVERSION".


| Keyword | Information Following Keyword For IgorInfo(3) |
| --- | --- |
| IGORFILEVERSION | The actual version number of the Igor application file. |
|  | The version number format is a period-separated list of four numbers. Igor Pro 7.02 returns "7.0.2.X" where X is a subminor revision number. A revision to Igor Pro 7.02 would be indicated in the last digit, such as "7.0.2.12". |
| LOCALE | Country for which this version of Igor is localized. "Japan" for the Japanese language version of Igor, "US" for all other languages. |
|  | <div><Admonition type="warning"><p>This keyword is obsolete starting in Igor Pro 10. It will continue to be provided, but all new code should use the ISOLOCALE keyword instead.</p></Admonition></div> |
| ISOLOCALE | Returns the language and territory that represents Igor's current language as a string of the form "language_territory", where language is a lowercase two-letter ISO 639 language code, and territory is an uppercase two- or three-letter ISO 3166 territory code. If the locale has no specified territory, only the language name is returned. |
| OS | Description of operating system. |
|  | It is something like "Microsoft Windows 10 Home (21H1)". The actual build number and format of the text will vary with the operating system and service pack. |
| OSVERSION | Operating system number. |
|  | This is something like "10.0.19043.1466". |

### *Selector = 4* {#selector-4}
IgorInfo(4) returns the name of the current processor architecture. Currently this is always "Intel".

### *Selector = 5* {#selector-5}
IgorInfo(5) returns, as a string, the serial number of the program if it is registered or "\_none\_" if it isn't registered. Use [str2num](/igorpro/commands/str2num.md) to store the result in a numeric variable. str2num returns NaN if the program isn't registered.

### *Selector = 6* {#selector-6}
IgorInfo(6) returns, as a string, the version of the Qt library under which Igor is running, for example, "5.9.4". This selector value was added in Igor Pro 7.00.

### *Selector = 7* {#selector-7}
IgorInfo(7) returns, as a string, the name of the current user. This selector value was added in Igor Pro 7.00.

### *Selector = 8* {#selector-8}
IgorInfo(8) is no longer used and always returns an empty string. This selector value was added in Igor Pro 8.00.

### *Selector = 9* {#selector-9}
IgorInfo(9) returns "admin" if Igor's process is being run as an administrator. Otherwise it returns "". This selector value was added in Igor Pro 8.00.

### *Selector = 10* {#selector-10}
IgorInfo(10) returns a semicolon-separated list containing the names of activated XOPs. This selector value was added in Igor Pro 8.00.

### *Selector = 11* {#selector-11}
IgorInfo(11) returns a string specifying the type of the current experiment. This will be one of the following:


|  |  |
| --- | --- |
| "Packed" | Current experiment file is a .pxp file |
| "HDF5 packed" | Current experiment file is a .h5xp file |
| "Unpacked" | Current experiment file is a .uxp file |
| "" | Current experiment was never saved to a file |

See [Saving Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#saving-experiments) for a discussion of the various experiment file formats.

### *Selector = 12* {#selector-12}
IgorInfo(12) returns a string specifying the name of the current experiment file including the extension. If the experiment was never saved to a file, it returns "".

This selector value was added in Igor Pro 9.00.

Use IgorInfo(1) to get the file name without the extension.

### *Selector = 13* {#selector-13}
IgorInfo(13) returns a collection of information about the autosave settings. See [Autosave](/igorpro/igor-basics/experiments-files-and-folders.md#autosave) for background information.

This selector value was added in Igor Pro 9.00.

### *Selector = 14* {#selector-14}
IgorInfo(14) returns a collection of information about the HDF5 default compression settings. See [HDF5 Default Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-default-compression) for background information.

This selector value was added in Igor Pro 9.00.

The keywords are as follows:

| Keyword | Information Following Keyword For IgorInfo(13) |
| --- | --- |
| ENABLED |<table class="nested-table"><tbody><tr><td>0:</td><td>Autosave is disabled</td></tr><tr><td>1:</td><td>Autosave is enabled</td></tr></tbody></table>
| MODE |<table class="nested-table"><tbody><tr><td>1:</td><td>Direct mode (saves to original files)</td></tr><tr><td>2:</td><td>Indirect mode (saves to .autosave files)</td></tr></tbody></table>
| INTERVAL | The interval in minutes between autosaves if autosave is enabled. |
| OPTIONS | A bitwise value with each bit indicating if a given feature is off (bit is 0) or on (bit is 1): |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Autosave entire experiment</td></tr><tr><td>Bit&nbsp;1:</td><td>Autosave standalone procedure files</td></tr><tr><td>Bit&nbsp;2:</td><td>Autosave standalone plain text notebooks</td></tr><tr><td>Bit&nbsp;3:</td><td>Autosave standalone formatted text notebooks</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |

See [Autosave](/igorpro/igor-basics/experiments-files-and-folders.md#autosave) for details.

### *Selector = 15* {#selector-15}
IgorInfo(15) returns a string specifying the default experiment file format.

This selector value was added in Igor Pro 9.00.

The returned value will be one of the following:


|  |  |
| --- | --- |
| "Packed" | Default experiment file format is .pxp |
| "HDF5 packed" | Default experiment file format is .h5xp |
| "Unpacked" | Default experiment file format is .uxp |

See [Saving Experiments](/igorpro/igor-basics/experiments-files-and-folders.md#saving-experiments) for a discussion of the various experiment file formats.

### *Selector = 16* {#selector-16}
IgorInfo(16) returns the total number of waves of all kinds (global, free, local) that currently exist. This selector value was added in Igor Pro 9.00.

IgorInfo(16) can help advanced Igor programmers detect wave leaks in their procedures. For details, see [Detecting Wave Leaks](/igorpro/programming/programming-techniques.md#detecting-wave-leaks).

### *Selector = 17* {#selector-17}
IgorInfo(17) returns the returns the experiment's startup commands and recreation macros. This selector value was added in Igor Pro 10.00.

### *Selector = 18* {#selector-18}
IgorInfo(18) returns "1" if the experiment is closing, otherwise "0".

This is useful in [BeforeExperimentSaveHook](/igorpro/advanced-topics.md#beforeexperimentsavehook) to decide whether to, for example, remove large temporary waves so that they are not saved with the experiment, but to leave them alone if the experiment will remain open.

This selector value was added in Igor Pro 10.00.

### *Examples* {#examples}

```igor
Print NumberByKey("NSCREENS", IgorInfo(0))  // Number of active displays
Function RunningWindows()                   // Returns 1 if Windows
	return Cmpstr(IgorInfo(2),"Windows") == 0
End
```

### *See Also* {#see-also}
[StringByKey](/igorpro/commands/stringbykey.md), [NumberByKey](/igorpro/commands/numberbykey.md)