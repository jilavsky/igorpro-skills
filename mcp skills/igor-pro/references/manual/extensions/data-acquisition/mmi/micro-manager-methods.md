---
description: "Instructs Micro-Manager to create and open a new interface for the device specified by moduleName and deviceName, assigning that interface the identity…"
slug: /extensions/data-acquisition/mmi/micro-manager-methods
---

# Micro-Manager Methods {#micro-manager-methods}

### Initialization and Setup {#initialization-and-setup}

<div className="command-signature">

## <strong>MMC_LoadDevice</strong>   /Q /Z deviceLabel, <em>moduleName</em>, <em>deviceName</em> {#mmc_loaddevice}

</div>

Instructs Micro-Manager to create and open a new interface for the device specified by moduleName and deviceName, assigning that interface the identity specified by deviceLabel.  Call [MMC_GetAvailableDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getavailabledevices) to obtain a list of devices supported by a specific module (device-adapter).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *deviceLabel* | An Igor string containing the case-sensitive label to be used to identify the instance of the device created by this operation. |
| *moduleName* | An Igor string containing the 'root' of the name of the Micro-Manager device-adapter to be used for this device.  (See [Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md) for more about the filenames used for device-adapters.)  For example, if you want to load a device from the device-adapter embodied by the file mmgr_dal_SutterLambda.dll, the moduleName parameter would be "SutterLambda". |
| *deviceName* | An Igor string containing the case-sensitive name of the device you want to load from the adapter.  This name is set by the author of the device-adapter, and your parameter must match exactly one of devices supported by the module. |

### *See Also* {#see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_GetAvailableDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getavailabledevices), [MMC_UnloadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloaddevice)





<div className="command-signature">

## <strong>MMC_UnloadDevice</strong>   /Q /Z deviceLabel {#mmc_unloaddevice}

</div>

Instructs Micro-Manager to release its interface for the device specified by deviceLabel.  The specified device must have been created previously through a call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice).

### *Flags* {#mmc_unloaddevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_unloaddevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | An Igor string containing the case-sensitive label of the device to be released.  deviceLabel must have been used in the preceding call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice) that created the interface. |

### *See Also* {#mmc_unloaddevice-see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice), [MMC_UnloadAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloadalldevices)





<div className="command-signature">

## <strong>MMC_UnloadAllDevices</strong>   /Q /Z {#mmc_unloadalldevices}

</div>

Instructs Micro-Manager to delete its interfaces for all currently loaded devices.

### *Flags* {#mmc_unloadalldevices-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *See Also* {#mmc_unloadalldevices-see-also}

[MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice), [MMC_UnloadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloaddevice)





<div className="command-signature">

## <strong>MMC_InitializeAllDevices</strong>   /Q /Z {#mmc_initializealldevices}

</div>

Instructs Micro-Manager to initialize the interfaces for all its currently loaded devices.

### *Flags* {#mmc_initializealldevices-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *See Also* {#mmc_initializealldevices-see-also}

[MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice), [MMC_InitializeDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializedevice)





<div className="command-signature">

## <strong>MMC_InitializeDevice</strong>   /Q /Z deviceLabel {#mmc_initializedevice}

</div>

Instructs Micro-Manager to initialize its interface for the device specified by deviceLabel.  The specified device must have been created previously through a call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice).

### *Flags* {#mmc_initializedevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_initializedevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | An Igor string containing the case-sensitive label of the 'device' to be initialized. |

### *See Also* {#mmc_initializedevice-see-also}

[MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice), [MMC_InitializeAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializealldevices)





<div className="command-signature">

## <strong>MMC_Reset</strong>   /Q /Z {#mmc_reset}

</div>

Resets Micro-Manager's core, unloading all devices and resetting its internal configuration.

### *Flags* {#mmc_reset-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *See Also* {#mmc_reset-see-also}

[MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset), [MMC_UnloadAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloadalldevices)





<div className="command-signature">

## <strong>MMC_UpdateCoreProperties</strong>   /Q /Z {#mmc_updatecoreproperties}

</div>

Updates Micro-Manager's set of core properties (selected camera, shutter, wheel, etc.) from currently loaded devices.

### *Flags* {#mmc_updatecoreproperties-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *See Also* {#mmc_updatecoreproperties-see-also}

[MMC_InitializeAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializealldevices)





<div className="command-signature">

## <strong>MMC_GetCoreErrorText</strong>  (<em>errCode</em>) {#mmc_getcoreerrortext}

</div>

Returns a string containing the Micro-Manager error text corresponding to the specified error code.

### *Parameters* {#mmc_getcoreerrortext-parameters}

|  |  |
| --- | --- |
| errCode | A number or Igor numeric variable indicating the Micro-Manager error-code whose error text is to be returned. |





<div className="command-signature">

## <strong>MMC_GetVersionInfo</strong>  ( ) {#mmc_getversioninfo}

</div>

Returns a string containing the version number of Micro-Manager's core.  For example, typing the following on Igor's command line

```igor
print MMC_GetVersionInfo()
```

evokes the response

```
MMCore version 10.4.0
```

### *See Also* {#mmc_getversioninfo-see-also}

[MMC_GetAPIVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getapiversioninfo), [MMI_GetXOPversion](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getxopversion)



<div className="command-signature">

## <strong>MMC_GetAPIVersionInfo</strong>  ( ) {#mmc_getapiversioninfo}

</div>

Returns a string containing the version numbers of Micro-Manager's Module-API and Device-API.  For example, typing the following on Igor's command line

```igor
print MMC_GetAPIVersionInfo()
```

evokes the response

```
Device API version 71, Module API version 10
```

### *See Also* {#mmc_getapiversioninfo-see-also}

[MMC_GetVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getversioninfo), [MMI_GetXOPversion](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getxopversion)





<div className="command-signature">

## <strong>MMC_SaveSystemState</strong>   /Q /Z fileName {#mmc_savesystemstate}

</div>

Saves the current state of the Micro-Manager system (i.e. the status of writable properties) as text, to the named file.  The file created can be used later by [MMC_LoadSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemstate) to re-install the state into Micro-Manager.

### *Flags* {#mmc_savesystemstate-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_savesystemstate-parameters}

|  |  |
| --- | --- |
| *fileName* | A string that specifies the path- and file-name of the file to receive the state information. |

### *Details* {#details}
This operation will overwrite any existing file with the same name.  Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_savesystemstate-see-also}

[MMC_LoadSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemstate), [MMC_SaveSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemconfig), [MMC_LoadSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemconfig)







<div className="command-signature">

## <strong>MMC_LoadSystemState</strong>   /Q /Z fileName {#mmc_loadsystemstate}

</div>

Loads the state of the Micro-Manager system (i.e. the status of writable properties) from the named file, created by a previous call to [MMC_SaveSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemstate).

### *Flags* {#mmc_loadsystemstate-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_loadsystemstate-parameters}

|  |  |
| --- | --- |
| *fileName* | A string that specifies the path- and file-name of the file containing the state information to be loaded. |

### *Details* {#mmc_loadsystemstate-details}
Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_loadsystemstate-see-also}

[MMC_SaveSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemstate), [MMC_SaveSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemconfig), [MMC_LoadSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemconfig)







<div className="command-signature">

## <strong>MMC_SaveSystemConfig</strong>   /Q /Z fileName {#mmc_savesystemconfig}

</div>

Instructs Micro-Manager to save the current system configuration (devices loaded, their labels, etc.) to a text file in Micro-Manager's standard file format.  The file created can be used later to re-install the configuration by calling [MMC_LoadSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemconfig).

### *Flags* {#mmc_savesystemconfig-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_savesystemconfig-parameters}

|  |  |
| --- | --- |
| *fileName* | A string that specifies the path- and file-name of the file to receive the configuration. |

### *Details* {#mmc_savesystemconfig-details}
This operation will overwrite any existing file with the same name.  Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_savesystemconfig-see-also}

[MMC_LoadSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemconfig)







<div className="command-signature">

## <strong>MMC_LoadSystemConfig</strong>   /Q /Z fileName {#mmc_loadsystemconfig}

</div>

Instructs Micro-Manager to load the system's configuration from a text file created by a previous call to [MMC_SaveSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemconfig).

### *Flags* {#mmc_loadsystemconfig-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_loadsystemconfig-parameters}

|  |  |
| --- | --- |
| *fileName* | A string that specifies the path- and file-name of the file that contains the system configuration to be loaded. |

### *Details* {#mmc_loadsystemconfig-details}
Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_loadsystemconfig-see-also}

[MMC_SaveSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemconfig)




### Logging and Log Management {#logging-and-log-management}


<div className="command-signature">

## <strong>MMC_SetPrimaryLogFile</strong>   /Q /Z logFileName [, <em>truncate</em>] {#mmc_setprimarylogfile}

</div>

Sets the named file as Micro-Manager's primary log file.

### *Flags* {#mmc_setprimarylogfile-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setprimarylogfile-parameters}

|  |  |
| --- | --- |
| *logFileName* | An Igor string specifying the full pathname of the file to be Micro-Manager's primary log file.  If the filename is omitted or if a NULL ("") filename is entered, Micro-Manager's primary log file is disabled. |
| *truncate* | An optional numeric parameter (with default value of zero), which specifies how to handle a pre-existing file with the same pathname.  If truncate is zero, new entries are appended to the previous contents of the file.  If truncate is non-zero, the previous contents of the file are erased before new entries are appended. |

### *Details* {#mmc_setprimarylogfile-details}
Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_setprimarylogfile-see-also}

[MMC_GetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getprimarylogfile), [MMC_LogMessage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_logmessage)







<div className="command-signature">

## <strong>MMC_GetPrimaryLogFile</strong>  ( ) {#mmc_getprimarylogfile}

</div>

Returns a string containing the complete pathname of Micro-Manager's primary log file.

### *See Also* {#mmc_getprimarylogfile-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_LogMessage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_logmessage)


<div className="command-signature">

## <strong>MMC_LogMessage</strong>   /Q /Z message [,<em>debugOnly</em>] {#mmc_logmessage}

</div>

Appends a message to Micro-Manager's primary log file.

### *Flags* {#mmc_logmessage-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_logmessage-parameters}

|  |  |
| --- | --- |
| *message* | An Igor string specifying the message to be appended to the log file. |
| *debugOnly* | An optional numeric parameter (with default value of zero).  If debugOnly is non-zero, the message is appended to the log file only when debug-logging is enabled.  If debugOnly is zero, the message is always appended to the log file. |

### *See Also* {#mmc_logmessage-see-also}

[MMC_GetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getprimarylogfile), [MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_EnableDebugLog](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_enabledebuglog)





<div className="command-signature">

## <strong>MMC_EnableDebugLog</strong>   /Q /Z enableState {#mmc_enabledebuglog}

</div>

Enables or disables logging of Micro-Manager's debug messages.

### *Flags* {#mmc_enabledebuglog-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_enabledebuglog-parameters}

|  |  |
| --- | --- |
| *enableState* | A numeric value that sets the enabled state for debug messages.  Setting enableState to zero disables logging of debug messages.  Setting enableState to any non-zero value enables logging of debug messages. |

### *See Also* {#mmc_enabledebuglog-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_LogMessage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_logmessage), [MMC_DebugLogEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_debuglogenabled)





<div className="command-signature">

## <strong>MMC_DebugLogEnabled</strong>  ( ) {#mmc_debuglogenabled}

</div>

### *Parameters* {#mmc_debuglogenabled-parameters}

|  |  |
| --- | --- |
|  | (None) |

### *Returns* {#returns}
A numeric value indicating whether debug logging is enabled.

### *See Also* {#mmc_debuglogenabled-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_EnableDebugLog](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_enabledebuglog)





<div className="command-signature">

## <strong>MMC_EnableStdErrLog</strong>   /Q /Z enableState {#mmc_enablestderrlog}

</div>

Enables or disables Micro-Manager's sending log messages to standard error output.

### *Flags* {#mmc_enablestderrlog-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_enablestderrlog-parameters}

|  |  |
| --- | --- |
| *enableState* | A numeric value that sets the enabled state for sending log messages to stderr.  Setting enableState to zero disables sending log messages to stderr.  Setting enableState to any non-zero value enables sending log messages to stderr. |

### *See Also* {#mmc_enablestderrlog-see-also}

[MMC_StdErrLogEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stderrlogenabled)





<div className="command-signature">

## <strong>MMC_StdErrLogEnabled</strong>  ( ) {#mmc_stderrlogenabled}

</div>

### *Parameters* {#mmc_stderrlogenabled-parameters}

|  |  |
| --- | --- |
|  | (None) |

### *Returns* {#mmc_stderrlogenabled-returns}
A numeric value indicating whether logging output is directed to standard error.

### *See Also* {#mmc_stderrlogenabled-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_EnableStdErrLog](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_enablestderrlog)







<div className="command-signature">

## <strong>MMC_StartSecondaryLogFile</strong>  (<em>logFileName</em>, <em>enableDebug</em>, <em>truncate</em>, <em>synchronous</em>) {#mmc_startsecondarylogfile}

</div>

Starts Micro-Manager's capturing of logging messages into an additional output file.  Returns a numeric value identifying the secondary log file created.

### *Parameters* {#mmc_startsecondarylogfile-parameters}

|  |  |
| --- | --- |
| *logFileName* | A string specifying the path- and file-name of the secondary logfile to be used. |
| *enableDebug* | A numeric value specifying whether debugging messages should be logged to the secondary file, independent of whether debugging messages are logged to the primary log file.  When set to zero, debug messages will be excluded from the secondary log file.  When set to any non-zero value, debug messages will be included in the secondary log file. |
| *truncate* | A numeric value specifying how to handle any pre-existing file that has the same pathname as specified by *logFileName*.  When set to zero, new log messages are appended to the pre-existing file.  When set to any non-zero value, any pre-existing file is cleared before  new log messages are written to the file. |
| *synchronous* | A numeric value specifying whether writes to the secondary logging file must complete before logging functions return to their caller.  When set to zero, writes to the secondary log file are executed asynchronously.  When set to any non-zero value, writes to the secondary log file are performed synchronously, ensuring that writes are complete when the logging function returns to its caller.  Micro-Manager states that synchronous writes help in some debugging situations, but at a cost in performance. |

### *Returns* {#mmc_startsecondarylogfile-returns}

|  |  |
| --- | --- |
|  | A numeric value identifying the secondary log file created.  This identifier is required when calling [MMC_StopSecondaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsecondarylogfile). |

### *Details* {#mmc_startsecondarylogfile-details}
Be sure to use double back-slash characters to separate names within a compound pathname.

### *See Also* {#mmc_startsecondarylogfile-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_StopSecondaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsecondarylogfile)





<div className="command-signature">

## <strong>MMC_StopSecondaryLogFile</strong>  /Q /Z fileHandle {#mmc_stopsecondarylogfile}

</div>

Halts Micro-Manager's recording of logging messages into the secondary log file specified by the fileHandle.

### *Flags* {#mmc_stopsecondarylogfile-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_stopsecondarylogfile-parameters}

|  |  |
| --- | --- |
| *fileHandle* | A numeric identifier of the selected secondary logfile into which logging is to be halted. |

### *See Also* {#mmc_stopsecondarylogfile-see-also}

[MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile), [MMC_StartSecondaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsecondarylogfile)



### Device Listing {#device-listing}

<div className="command-signature">

## <strong>MMC_GetDeviceAdapterNames</strong>  /Q /Z [destinationWave] {#mmc_getdeviceadapternames}

</div>

Gets a list of root-names for all discoverable device-adapters.

### *Flags* {#mmc_getdeviceadapternames-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_getdeviceadapternames-parameters}

|  |  |
| --- | --- |
| *destinationWave* | An optional Igor text wave which is to receive the list of devices.  If no existing wave is specified, the results will be written to a new text wave in the current data folder named W_MMCdeviceAdapters. |

### *Details* {#mmc_getdeviceadapternames-details}
Recall that, under Windows, Micro-Manager's device-adapters are implemented as .dll files with names that match the pattern:

```
mmgr_dal_<*root-name*>.dll
```

MMC_GetDeviceAdapterNames returns a list of the root-names of the device-adapters that are accessible to Micro-Manager.

### *See Also* {#mmc_getdeviceadapternames-see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename)







<div className="command-signature">

## <strong>MMC_GetAvailableDevices</strong>  /Q /Z /O moduleName [, <em>destinationWave</em>] {#mmc_getavailabledevices}

</div>

Gets a list of the names of the devices available from the specified module (device-adapter), each together with its device-type and description.

### *Flags* {#mmc_getavailabledevices-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_getavailabledevices-parameters}

|  |  |
| --- | --- |
| *moduleName* | The 'root' name of the module (device-adapter) whose devices are to be listed.  The root name of a Micro-Manager module is embedded in the name of the .dll file implementing the device-adapter, as follows: |
|  | `mmgr_dal_<*root-name*>.dll` |
| *destinationWave* | An optional Igor text wave which is to receive the list of devices.  If no existing wave is specified, the results will be written to a new text wave in the current data folder named W_MMCavailDevices. |

### *Details* {#mmc_getavailabledevices-details}
MMC_GetDeviceAdapterNames returns a list of the root-names of the device-adapters that are accessible to Micro-Manager.

### *See Also* {#mmc_getavailabledevices-see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_GetLoadedDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getloadeddevices), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype), [MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename), [MMC_GetDeviceLibrary](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicelibrary)







<div className="command-signature">

## <strong>MMC_GetLoadedDevices</strong>  /Q /Z destTextWave {#mmc_getloadeddevices}

</div>

Gets a list of the names of the devices loaded into Micro-Manager's core.

### *Flags* {#mmc_getloadeddevices-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_getloadeddevices-parameters}

|  |  |
| --- | --- |
| *destTextWave* | An optional Igor text wave which is to receive the list of devices.  If no existing wave is specified, the results will be written to a new text wave in the current data folder named W_MMCloadedDevices. |

### *See Also* {#mmc_getloadeddevices-see-also}

[MMC_GetLoadedDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getloadeddevices), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype), [MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename), [MMC_GetDeviceLibrary](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicelibrary)



### Generic Device Control {#generic-device-control}

<div className="command-signature">

## <strong>MMC_GetDeviceName</strong>  (<em>deviceLabel</em>) {#mmc_getdevicename}

</div>

Returns the device-name for a specified device-label.

### *Parameters* {#mmc_getdevicename-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive Micro-Manager device-label assigned by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *Returns* {#mmc_getdevicename-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive Micro-Manager device-name for to device whose label was provided. |

### *See Also* {#mmc_getdevicename-see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_GetDeviceLibrary](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicelibrary), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetDeviceLibrary</strong>  (<em>deviceLabel</em>) {#mmc_getdevicelibrary}

</div>

Returns the root-name of the library (device-adapter) for a specified device-label.

### *Parameters* {#mmc_getdevicelibrary-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *Returns* {#mmc_getdevicelibrary-returns}

|  |  |
| --- | --- |
|  | A string containing the root-name of the library (device-adapter) implementing the interface to the device specified by the device-label. |

### *See Also* {#mmc_getdevicelibrary-see-also}

[Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md), [MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetDeviceType</strong>  (<em>deviceLabel</em>) {#mmc_getdevicetype}

</div>

Returns the device-type for a specified device-label.

### *Parameters* {#mmc_getdevicetype-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *Returns* {#mmc_getdevicetype-returns}

|  |  |
| --- | --- |
|  | A numeric value encoding the type of device represented by the specified device-label. |

### *Details* {#mmc_getdevicetype-details}
The returned numeric value encodes the device-type as follows:

| Code | Device Type |
| --- | --- |
| 0 | UnknownType |
| 1 | AnyType |
| 2 | CameraDevice |
| 3 | ShutterDevice |
| 4 | StateDevice |
| 5 | StageDevice |
| 6 | XYStageDevice |
| 7 | SerialDevice |
| 8 | GenericDevice |
| 9 | AutoFocusDevice |
| 10 | CoreDevice |
| 11 | ImageProcessorDevice |
| 12 | SignalIODevice |
| 13 | MagnifierDevice |
| 14 | SLMDevice |
| 15 | HubDevice |
| 16 | GalvoDevice |



### *See Also* {#mmc_getdevicetype-see-also}

[MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename), [MMC_GetDeviceLibrary](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicelibrary)


<div className="command-signature">

## <strong>MMC_GetPropertyNumeric</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_getpropertynumeric}

</div>

Returns a double containing the numeric value of the named property for the specified device.

### *Parameters* {#mmc_getpropertynumeric-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A string containing the case-sensitive name of the property whose value is sought. |

### *Returns* {#mmc_getpropertynumeric-returns}

|  |  |
| --- | --- |
|  | A real, numeric value containing the value of the named property. |

### *Details* {#mmc_getpropertynumeric-details}
Use this function to get the values of any of Micro-Manager's numeric property-types -- floats and integers.

### *See Also* {#mmc_getpropertynumeric-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist)**,** [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring)**,** [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)







<div className="command-signature">

## <strong>MMC_GetPropertyString</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_getpropertystring}

</div>

Returns a string containing the value of the named property for the specified device.

### *Parameters* {#mmc_getpropertystring-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A string containing the case-sensitive name of the property whose value is sought. |

### *Returns* {#mmc_getpropertystring-returns}

|  |  |
| --- | --- |
|  | A string containing the value of the named property. |

### *See Also* {#mmc_getpropertystring-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)





<div className="command-signature">

## <strong>MMC_GetAllowedPropertyValues</strong>  /Q /Z deviceLabel, <em>propertyName</em> [, <em>destTextWave</em>] {#mmc_getallowedpropertyvalues}

</div>

Returns a list of allowed string values for the named property for the device specified by the device-label.  Only available for properties using string-values.

### *Flags* {#mmc_getallowedpropertyvalues-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_getallowedpropertyvalues-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A string containing the case-sensitive name of the property whose values are sought. |
| *destTextWave* | An optional Igor text wave which is to receive the list of allowed values.  If no existing wave is specified, the results will be written to a new text wave in the current data folder named W_MMCallowedPropertyValues. |

### *See Also* {#mmc_getallowedpropertyvalues-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)





<div className="command-signature">

## <strong>MMC_IsPropertyReadOnly</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_ispropertyreadonly}

</div>

Reports if named property of the specified device is read-only -- it cannot be assigned a new value.

### *Parameters* {#mmc_ispropertyreadonly-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A case-sensitive string that specifies the name of the property being checked. |

### *Returns* {#mmc_ispropertyreadonly-returns}

|  |  |
| --- | --- |
|  | A numeric value (0 or 1), where |
|  | 1 indicates the property is read-only, |
|  | 0 indicates the property is not read-only |

### *See Also* {#mmc_ispropertyreadonly-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist)





<div className="command-signature">

## <strong>MMC_IsPropertyPreInit</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_ispropertypreinit}

</div>

Reports if named property of the specified device must be assigned a value prior to the device being initialized.

### *Parameters* {#mmc_ispropertypreinit-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A case-sensitive string that specifies the name of the property being checked. |

### *Returns* {#mmc_ispropertypreinit-returns}

|  |  |
| --- | --- |
|  | A numeric value (0 or 1), where |
|  | 1 indicates the property must be assigned its value before the device is initialized, |
|  | 0 indicates the property should be assigned its value after the device is initialized |

### *See Also* {#mmc_ispropertypreinit-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)





<div className="command-signature">

## <strong>MMC_HasPropertyLimits</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_haspropertylimits}

</div>

Reports if the named numeric property of the specified device has defined upper- and lower-limits to its permitted values.

### *Parameters* {#mmc_haspropertylimits-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A case-sensitive string that specifies the name of the property being checked. |

### *Returns* {#mmc_haspropertylimits-returns}

|  |  |
| --- | --- |
|  | A numeric value (0 or 1), where |
|  | 1 indicates the property has defined upper- and lower-limits, |
|  | 0 indicates the property does not have defined upper- and lower-limits |

### *See Also* {#mmc_haspropertylimits-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyLowerLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertylowerlimit), [MMC_GetPropertyUpperLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertyupperlimit)





<div className="command-signature">

## <strong>MMC_GetPropertyLowerLimit</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_getpropertylowerlimit}

</div>

Returns the minimum permitted value of the named numeric property of the specified device.

### *Parameters* {#mmc_getpropertylowerlimit-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A case-sensitive string that specifies the name of the property being checked. |

### *Returns* {#mmc_getpropertylowerlimit-returns}

|  |  |
| --- | --- |
|  | A double containing the minimum permitted value of the named property in the specified device.  Returns 0 if no minimum value is defined for the property.  Returns an error if the property does not exist or is of a non-numeric type. |

### *See Also* {#mmc_getpropertylowerlimit-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyLowerLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertylowerlimit), [MMC_GetPropertyUpperLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertyupperlimit)





<div className="command-signature">

## <strong>MMC_GetPropertyUpperLimit</strong>  (<em>deviceLabel</em>, <em>propertyName</em>) {#mmc_getpropertyupperlimit}

</div>

Returns the maximum permitted value of the named numeric property of the specified device.

### *Parameters* {#mmc_getpropertyupperlimit-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| *propertyName* | A case-sensitive string that specifies the name of the property being checked. |

### *Returns* {#mmc_getpropertyupperlimit-returns}

|  |  |
| --- | --- |
|  | A double containing the maximum permitted value of the named property in the specified device.  Returns 0 if no maximum value is defined for the property.  Returns an error if the property does not exist or is of a non-numeric type. |

### *See Also* {#mmc_getpropertyupperlimit-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyLowerLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertylowerlimit), [MMC_GetPropertyUpperLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertyupperlimit)





<div className="command-signature">

## <strong>MMC_SetProperty</strong>  /Q /Z /FREE /F=<em>floatValue</em> /I=<em>integerValue</em> /S=<em>stringValue</em> <em>deviceLabel</em>, <em>propertyName</em> {#mmc_setproperty}

</div>

Sets the specified value into the named property of the specified device.

### *Flags* {#mmc_setproperty-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/FREE</span> | When the /FREE flag is omitted, MMI automatically compares a passed numeric value to the property's minimum and maximum permitted values, if they are available from Micro-Manager.  If the passed value is outside the limits set by the minimum and maximum values, MMI reports an error and returns without attempting to assign the value to the property.  By setting the /FREE flag, MMI assigns the passed numeric value to the property without performing (i.e. 'free of') any bounds checking on the value passed.  If the passed value is outside the permitting limits, Micro-Manager returns an error and leaves the property with its previous value. |
| <span class="table-cell-nowrap">/F = *floatValue*</span> | Used to set the value of numeric properties that accept floating-point (non-integer) values. |
| <span class="table-cell-nowrap">/I = *integerValue*</span> | Used to set the value of numeric properties that accept only integer values. |
| <span class="table-cell-nowrap">/S = *stringValue*</span> | Used to set the value of properties that accept only string values. |

### *Parameters* {#mmc_setproperty-parameters}

|  |  |
| --- | --- |
| deviceLabel | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |
| propertyName | A case-sensitive string that specifies the name of the property whose value is being assigned. |

### *Details* {#mmc_setproperty-details}
It is important to note that many numeric properties do not provide explicit minimum and maximum limits.  Thus when assigning numeric property values without the /FREE flag, MMI attempts to check the proposed value against Micro-Manager's limits for that property, but if no such limits are available, MMI attempts to assign the proposed value to the property without checks, as if the /FREE flag were set.  Users should consider using the /Q and /Z flags to manage MMI's reporting of the errors that may result.

### *See Also* {#mmc_setproperty-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric), [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring)







<div className="command-signature">

## <strong>MMC_GetTimeoutMs</strong>  ( ) {#mmc_gettimeoutms}

</div>

Returns Micro-Manager's timeout period.

### *Parameters* {#mmc_gettimeoutms-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_gettimeoutms-returns}

|  |  |
| --- | --- |
|  | A numeric value reporting Micro-Manager's internal time-out setting, as an integer number of milliseconds (1 millisecond = 0.001 second). |

### *See Also* {#mmc_gettimeoutms-see-also}

[MMC_SetTimeOutMs](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_settimeoutms)





<div className="command-signature">

## <strong>MMC_SetTimeoutMs</strong>  /Q /Z timeOutValue {#mmc_settimeoutms}

</div>

Sets Micro-Manager's timeout period.

### *Flags* {#mmc_settimeoutms-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_settimeoutms-parameters}

|  |  |
| --- | --- |
| *timeOutValue* | A numeric expression specifying the new timeout value, as a positive integer number of milliseconds (1 millisecond = 0.001 second).  The value is passed to Micro-Manager as a signed, 32-bit integer.  Hence the maximum permitted value is 2<sup>31</sup> - 1 = 2,147,483,647. |

### *See Also* {#mmc_settimeoutms-see-also}

[MMC_GetTimeOutMs](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_gettimeoutms)




### Management of 'current' Device for Specific Roles {#management-of-current-device-for-specific-roles}

<div className="command-signature">

## <strong>MMC_GetCameraDevice</strong>  ( ) {#mmc_getcameradevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected camera.

### *Parameters* {#mmc_getcameradevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getcameradevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected camera, or an empty string if none is currently selected. |

### *See Also* {#mmc_getcameradevice-see-also}

[MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice)



<div className="command-signature">

## <strong>MMC_SetCameraDevice</strong>  /Q /Z deviceLabel {#mmc_setcameradevice}

</div>

Sets the specified device as Micro-Manager's active camera.

### *Flags* {#mmc_setcameradevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setcameradevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setcameradevice-see-also}

[MMC_GetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcameradevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetShutterDevice</strong> {#mmc_getshutterdevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected shutter.

### *Parameters* {#mmc_getshutterdevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getshutterdevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected shutter, or an empty string if none is currently selected. |

### *See Also* {#mmc_getshutterdevice-see-also}

[MMC_SetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutterdevice)





<div className="command-signature">

## <strong>MMC_SetShutterDevice</strong>  /Q /Z deviceLabel {#mmc_setshutterdevice}

</div>

Sets the specified device as Micro-Manager's active shutter.

### *Flags* {#mmc_setshutterdevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setshutterdevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setshutterdevice-see-also}

[MMC_GetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getshutterdevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetFocusDevice</strong> {#mmc_getfocusdevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected focus device.

### *Parameters* {#mmc_getfocusdevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getfocusdevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected focus device, or an empty string if none is currently selected. |

### *See Also* {#mmc_getfocusdevice-see-also}

[MMC_SetFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setfocusdevice)





<div className="command-signature">

## <strong>MMC_SetFocusDevice</strong>  /Q /Z deviceLabel {#mmc_setfocusdevice}

</div>

Sets the specified device as Micro-Manager's active focus device.

### *Flags* {#mmc_setfocusdevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setfocusdevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setfocusdevice-see-also}

[MMC_GetFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getfocusdevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetXYStageDevice</strong> {#mmc_getxystagedevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected XY stage.

### *Parameters* {#mmc_getxystagedevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getxystagedevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected XY stage, or an empty string if none is currently selected. |

### *See Also* {#mmc_getxystagedevice-see-also}

[MMC_SetXYStageDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setxystagedevice)





<div className="command-signature">

## <strong>MMC_SetXYStageDevice</strong>  /Q /Z deviceLabel {#mmc_setxystagedevice}

</div>

Sets the specified device as Micro-Manager's active XY stage device.

### *Flags* {#mmc_setxystagedevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setxystagedevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setxystagedevice-see-also}

[MMC_GetXYStageDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getxystagedevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetAutoFocusDevice</strong> {#mmc_getautofocusdevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected auto-focus device.

### *Parameters* {#mmc_getautofocusdevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getautofocusdevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected auto-focus device, or an empty string if none is currently selected. |

### *See Also* {#mmc_getautofocusdevice-see-also}

[MMC_SetAutoFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setautofocusdevice)





<div className="command-signature">

## <strong>MMC_SetAutoFocusDevice</strong>  /Q /Z deviceLabel {#mmc_setautofocusdevice}

</div>

Sets the specified device as Micro-Manager's active autofocus device.

### *Flags* {#mmc_setautofocusdevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setautofocusdevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setautofocusdevice-see-also}

[MMC_GetAutoFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getautofocusdevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)





<div className="command-signature">

## <strong>MMC_GetSLMDevice</strong> {#mmc_getslmdevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected spatial light modulator (SLM).

### *Parameters* {#mmc_getslmdevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getslmdevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected spatial light modulator (SLM), or an empty string if none is currently selected. |

### *See Also* {#mmc_getslmdevice-see-also}

[MMC_SetSLMDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setslmdevice)





<div className="command-signature">

## <strong>MMC_SetSLMDevice</strong>  /Q /Z deviceLabel {#mmc_setslmdevice}

</div>

Sets the specified device as Micro-Manager's active spatial light modulator.

### *Flags* {#mmc_setslmdevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setslmdevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setslmdevice-see-also}

[MMC_GetSLMDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getslmdevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)



<div className="command-signature">

## <strong>MMC_GetGalvoDevice</strong> {#mmc_getgalvodevice}

</div>

Returns a string containing the Micro-Manager label for the currently selected galvanometer beam-steering device.

### *Parameters* {#mmc_getgalvodevice-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getgalvodevice-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive label for the currently selected galvanometer beam-steering device, or an empty string if none is currently selected. |

### *See Also* {#mmc_getgalvodevice-see-also}

[MMC_SetGalvoDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setgalvodevice)





<div className="command-signature">

## <strong>MMC_SetGalvoDevice</strong>  /Q /Z deviceLabel {#mmc_setgalvodevice}

</div>

Sets the specified device as Micro-Manager's active galvanometer device.

### *Flags* {#mmc_setgalvodevice-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setgalvodevice-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive label assigned to the device by a previous call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice). |

### *See Also* {#mmc_setgalvodevice-see-also}

[MMC_GetGalvoDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getgalvodevice), [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype)



### Image Acquisition {#image-acquisition}

<div className="command-signature">

## <strong>MMC_SnapImage</strong>  /Q /Z /U /CLRO=<em>colorOrder</em> {#mmc_snapimage}

</div>

Acquires one image from the active camera.  If a wave is already bound for the acquisition of single images, the acquired image is also retrieved and written to the bound wave.

### *Flags* {#mmc_snapimage-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/U</span> | Unlock bound image wave, if needed, prior to moving the image-data into the wave.  If the /U flag is omitted and the wave is locked, MMI will raise an error, as it will be unable to write the image into the wave. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGB**A**) in the string. |

### *Details* {#mmc_snapimage-details}
If MMC_SnapImage is called when no wave is bound to receive the image, then the acquired image remains in Micro-Manager's internal image buffer until it is either retrieved to a wave by calling [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage), or it is overwritten by another call to MMC_SnapImage.

### *See Also* {#mmc_snapimage-see-also}

[MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage), [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave), [MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)





<div className="command-signature">

## <strong>MMC_GetImage</strong>  /Q /Z /CLRO=<em>colorOrder</em> [<em>destinationWave</em>] {#mmc_getimage}

</div>

Retrieves a single image, acquired by a previous call to [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), and transfers that image to a wave.

### *Flags* {#mmc_getimage-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGB**A**) in the string. |

### *Parameters* {#mmc_getimage-parameters}

|  |  |
| --- | --- |
| *destinationWave* | The optional name of a numeric wave that is to receive the acquired image.  If an imageWave is specified, that wave (rather than any previously bound image-wave), receives the acquired image. |

### *Details* {#mmc_getimage-details}
If no imageWave is specified, the image is written to the wave specified by the most recent call to [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave).  If no imageWave is specified and no wave has been bound for the acquisition of single images, an error occurs.

If an Igor image-processor function has been specified by a previous call to [MMI_BindImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimageprocessor), that function will be called after the image is written to the wave.

### *See Also* {#mmc_getimage-see-also}

[MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave), [MMI_BindImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimageprocessor), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)







<div className="command-signature">

## <strong>MMI_GrabImage</strong>  /Q /Z /ORIG={<em>row</em>,<em>column</em>,<em>layer</em>,<em>chunk</em>} /CLRO=<em>colorOrder</em> [<em>destinationWave</em>] {#mmi_grabimage}

</div>

Acquires a single image and writes it to a wave with finer control than [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage).  MMI_GrabImage enables you to acquire and store a series of images in a single Igor wave.

### *Flags* {#mmi_grabimage-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/ORIG = {*row*,*column*,*layer*,*chunk*}</span> |  |
|  | An optional set of four integers that specify a vector to the image's origin within the destination wave.  The origin defines where the first (top-, left-most) pixel of the acquired image is to be written.  If the /ORIG flag is omitted, the acquired image is written to the wave with an origin vector of {0, 0, 0, 0}, i.e. with the top, left pixel of the image at the first row, column, layer and chunk. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGBA) in the string. |

### *Parameters* {#mmi_grabimage-parameters}

|  |  |
| --- | --- |
| *destinationWave* | The optional name of a numeric wave that is to receive the acquired image.  If an imageWave is specified, that wave (rather than any previously bound image-wave), receives the acquired image. |

### *Details* {#mmi_grabimage-details}
If no imageWave is specified, the image is written to the wave specified by the most recent call to [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave).  If no destinationWave is specified and no wave has been bound for the acquisition of single images, an error occurs.

Recall that each row in the acquired image is written to a column in the destination wave.  Thus when sizing a wave for side-by-side display of multiple images, be sure to set the number of columns in the wave to a multiple of the number of rows in the image, and the number of rows in the wave to a multiple of the number of columns in the image.

Similarly, recall that when working with multi-color (ex. RGB) images, each color plane is written to a separate layer in the destination wave.

### *See Also* {#mmi_grabimage-see-also}

[MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage), [MMC_GetNumberOfComponents](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getnumberofcomponents), [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)







<div className="command-signature">

## <strong>MMC_GetNumberOfComponents</strong>  ( ) {#mmc_getnumberofcomponents}

</div>

Returns the number of components (color channels) acquired by the active camera.

### *Parameters* {#mmc_getnumberofcomponents-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getnumberofcomponents-returns}

|  |  |
| --- | --- |
|  | A real, numeric value containing the number of components (color channels) acquired by the active camera. |

### *Details* {#mmc_getnumberofcomponents-details}
MMC_GetNumberOfComponents returns 1 for monochromatic cameras and either 3 or 4 for color cameras that return RGB or RGBA images, respectively.  Note too that MMI currently omits the A (alpha) component when transferring RGBA images to Igor's waves.

When MMI transfers a color image to a wave, each color component is written to a separate layer in the wave.  Hence waves intended to hold RGB color images acquired via MMI should contain at least 3 layers.

### *See Also* {#mmc_getnumberofcomponents-see-also}

[Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves), [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)



<div className="command-signature">

## <strong>MMC_GetExposure</strong>  (<em>cameraLabel</em>) {#mmc_getexposure}

</div>

Returns the exposure time (in milliseconds), of the specified camera.

### *Parameters* {#mmc_getexposure-parameters}

|  |  |
| --- | --- |
| *cameraLabel* | A string containing the case-sensitive Micro-Manager label of the specified camera.  If the parameter is an empty string (""), then the function returns the exposure time of the currently active camera. |

### *Returns* {#mmc_getexposure-returns}

|  |  |
| --- | --- |
|  | A real, numeric value containing the camera's exposure time, in milliseconds. |

### *See Also* {#mmc_getexposure-see-also}

[MMC_SetExposure](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setexposure)


<div className="command-signature">

## <strong>MMC_SetExposure</strong>  /Q /Z /L=<em>cameraLabel</em> <em>exposureTime</em> {#mmc_setexposure}

</div>

Sets the exposure time of the active camera.

### *Flags* {#mmc_setexposure-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | An optional string containing the case-sensitive Micro-Manager label of the camera whose exposure time is to be set.  If the /L flag is not specified, the specified exposure time is installed in the currently active camera. |

### *Parameters* {#mmc_setexposure-parameters}

|  |  |
| --- | --- |
| *exposureTime* | A numeric value that specifies the new exposure time (in milliseconds) that is to be applied to the specified camera. |

### *Details* {#mmc_setexposure-details}
Each camera has its own range of valid exposure times.  For most cameras, you can determine the range of valid exposure times by reviewing a list of the camera's properties, as reported by [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist).

### *See Also* {#mmc_setexposure-see-also}

[MMC_GetExposure](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getexposure), [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist)







<div className="command-signature">

## <strong>MMC_SetROI</strong>  /Q /Z /L=<em>cameraLabel</em> <em>ROIwave</em> {#mmc_setroi}

</div>

Sets the ROI (Region Of Interest) for the specified camera from the specified Igor wave.

### *Flags* {#mmc_setroi-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | A string containing the case-sensitive Micro-Manager label of the camera whose ROI is to be set.  If the /L flag is absent, the operation applies the ROI to the currently active camera. |

### *Parameters* {#mmc_setroi-parameters}

|  |  |
| --- | --- |
| *ROIwave* | The name of a real, numeric wave that holds the new specifications for the ROI. |

### *Details* {#mmc_setroi-details}
The ROI is specified as a sequence of four integers {x, y, xSize, ySize}, where x and y are the horizontal and vertical coordinates of the upper-left pixel in the region, and xSize and ySize are the horizontal and vertical sizes of the region.

If ROIwave is a one-dimensional wave, then the specification is taken from first four points along the ROW dimension.  If ROIwave is a multi-dimensional wave, then the specification is taken from the first four points along the COLUMN dimension in ROW 0.

This scheme provides a flexible way to define an ROI: whether from a simple numeric wave or by using the description of an ROI returned by from a previous call to [MMC_GetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getroi) or [MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi).

### *See Also* {#mmc_setroi-see-also}

[MMC_GetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getroi), [MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)







<div className="command-signature">

## <strong>MMC_GetROI</strong>  /Q /Z /L=<em>cameraLabel</em> [<em>destinationWave</em>] {#mmc_getroi}

</div>

Returns a wave containing the ROI (Region Of Interest) for the specified camera.

### *Flags* {#mmc_getroi-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | A string containing the case-sensitive Micro-Manager label of the camera whose ROI is to be returned.  If the /L flag is omitted, the operation returns the ROI of the currently active camera. |

### *Parameters* {#mmc_getroi-parameters}

|  |  |
| --- | --- |
| *destinationWave* | The optional name of a real, numeric wave that is to receive the ROI. If no destination wave is specified, the operation writes the ROI description to a wave called W_camROIs in the MMI data folder.  If a non-numeric wave by that name already exists in the MMI data folder, the operation creates a uniquely named wave within the MMI data folder and writes the ROI data to that wave. |

### *Details* {#mmc_getroi-details}
The destination wave is redimensioned to 1 row and 4 columns and the description of the active ROI is placed in the first 4 columns of the first row (row 0, columns 0 to 3).  The description of the ROI is returned as a sequence of four integers x, y, xSize, ySize, specifying the x (horizontal) and y (vertical) coordinates of the upper-left pixel in the region, followed by the horizontal and vertical sizes of the region.

If successful, the operation writes the name of the wave receiving the ROI description to the variable S_MMIresult in the MMI data folder.

### *See Also* {#mmc_getroi-see-also}

[MMC_SetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setroi), [MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)







<div className="command-signature">

## <strong>MMC_ClearROI</strong>  /Q /Z {#mmc_clearroi}

</div>

Sets the ROI for the active camera to the camera's full sensor and if successful, resets the circular buffer, clearing any images it may have held.

### *Flags* {#mmc_clearroi-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_clearroi-parameters}

|  |  |
| --- | --- |
|  | None. |

### *See Also* {#mmc_clearroi-see-also}

[MMC_SetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setroi), [MMC_GetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getroi), [MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)





<div className="command-signature">

## <strong>MMC_IsMultiROISupported</strong>  ( ) {#mmc_ismultiroisupported}

</div>

Reports whether the active camera supports the use of multiple simultaneous ROIs.

### *Parameters* {#mmc_ismultiroisupported-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_ismultiroisupported-returns}

|  |  |
| --- | --- |
| 0 | The camera does not support multiple ROIs. |
| 1 | The camera does support multiple ROIs. |

### *See Also* {#mmc_ismultiroisupported-see-also}

[MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [MMC_SetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setmultiroi), [MMC_IsMultiROIEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroienabled), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)



<div className="command-signature">

## <strong>MMC_IsMultiROIEnabled</strong>  ( ) {#mmc_ismultiroienabled}

</div>

Reports whether the active camera is currently using multiple simultaneous ROIs.

### *Parameters* {#mmc_ismultiroienabled-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_ismultiroienabled-returns}

|  |  |
| --- | --- |
| 0 | The camera is not currently using multiple ROIs. |
| 1 | The camera is currently using multiple ROIs. |

### *See Also* {#mmc_ismultiroienabled-see-also}

[MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [MMC_SetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setmultiroi), [MMC_IsMultiROISupported](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroisupported), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)





<div className="command-signature">

## <strong>MMC_SetMultiROI</strong>  /Q /Z ROIwave {#mmc_setmultiroi}

</div>

Defines a set of ROIs to use in the active camera.

### *Flags* {#mmc_setmultiroi-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setmultiroi-parameters}

|  |  |
| --- | --- |
| *ROIwave* | The name of a real, numeric wave that describes the set of ROIs to be applied to the active camera. |

### *Details* {#mmc_setmultiroi-details}
ROIwave must have at least 2 dimensions (ROWS and COLUMNS) and must have at least one row and four columns.  If ROIwave contains multiple layers or chunks, only the first layer in the first chunk (LAYER = 0, CHUNK = 0), is read.  Each row is interpreted as containing the description of one ROI, as a sequence of four integers in columns 0, 1, 2, and 3.  The sequence is interpreted as x, y, xSize, and ySize, specifying the x (horizontal) and y (vertical) coordinates of the upper-left pixel in the region, followed by the horizontal and vertical sizes of the region.

### *See Also* {#mmc_setmultiroi-see-also}

[MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi), [MMC_IsMultiROISupported](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroisupported), [MMC_IsMultiROIEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroienabled), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)







<div className="command-signature">

## <strong>MMC_GetMultiROI</strong>  /Q /Z [ROIwave] {#mmc_getmultiroi}

</div>

Returns a wave describing the set of ROIs in use in the active camera.

### *Flags* {#mmc_getmultiroi-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_getmultiroi-parameters}

|  |  |
| --- | --- |
| *ROIwave* | The optional name of a real, numeric wave that is to receive the list of ROIs. If no destination wave is specified, the operation writes the ROI descriptions to a wave called W_camROIs in the MMI data folder.  If a non-numeric wave already exists by that name in the MMI data folder, the operation creates a uniquely named wave within the MMI data folder and writes the ROI data to that wave. |

### *Details* {#mmc_getmultiroi-details}
The destination wave is redimensioned to n rows and 4 columns where n is the number of ROIs currently set for the camera.  The description of each ROI in the set is placed in the first 4 columns of consecutive rows (columns 0 to 3, in rows 0 to n-1).  The description of each ROI is stored as a sequence of four integers x, y, xSize, ySize, specifying the x (horizontal) and y (vertical) coordinates of the upper-left pixel in the region, followed by the horizontal and vertical sizes of each region.

If successful, the operation also writes the name of the wave receiving the ROI descriptions to the variable S_MMIresult in the MMI data folder.

### *See Also* {#mmc_getmultiroi-see-also}

[MMC_SetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setmultiroi), [MMC_IsMultiROISupported](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroisupported), [MMC_IsMultiROIEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroienabled), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)







<div className="command-signature">

## <strong>MMC_GetImageHeight</strong>  ( ) {#mmc_getimageheight}

</div>

Returns the vertical size (i.e. number of rows) of the image buffer, in pixels.

### *Parameters* {#mmc_getimageheight-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getimageheight-returns}


|  |  |
| --- | --- |
|  | A numeric value containing the integer height of one frame in the image-buffer, in pixels. |

### *See Also* {#mmc_getimageheight-see-also}

[MMC_GetImageWidth](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimagewidth), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)


<div className="command-signature">

## <strong>MMC_GetImageWidth</strong>  ( ) {#mmc_getimagewidth}

</div>

Returns the horizontal size (i.e. number of columns) of the image buffer, in pixels.

### *Parameters* {#mmc_getimagewidth-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getimagewidth-returns}

|  |  |
| --- | --- |
|  | A numeric value containing the integer width of one frame in the image-buffer, in pixels. |

### *See Also* {#mmc_getimagewidth-see-also}

[MMC_GetImageHeight](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimageheight), [Images in Igor Waves](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#images-in-igor-waves)




<div className="command-signature">

## <strong>MMC_GetImageBitDepth</strong>  ( ) {#mmc_getimagebitdepth}

</div>

Returns the number of bits used to encode the intensity of each image pixel coming from the active camera.

### *Parameters* {#mmc_getimagebitdepth-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getimagebitdepth-returns}

|  |  |
| --- | --- |
|  | A numeric value containing the integer number of bits used to encode the intensity of each pixel returned by the active camera. |

### *Details* {#mmc_getimagebitdepth-details}
If the camera returns multiple color planes (ex. RGB or RGBA images), the returned value represents the bit-depth of each individual color-plane, not the aggregate bit-depth of all of the color-planes.

### *See Also* {#mmc_getimagebitdepth-see-also}

[MMC_GetNumberOfComponents](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getnumberofcomponents), [https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html](https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html)






<div className="command-signature">

## <strong>MMC_SetAutoShutter</strong>  /Q /Z newState {#mmc_setautoshutter}

</div>

Enables or disables automatic opening and closing of the active shutter when images are acquired.

### *Flags* {#mmc_setautoshutter-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setautoshutter-parameters}

|  |  |
| --- | --- |
| *newState* | A numeric value, either 0 or 1 where: |
|  |<table class="nested-table"><tbody><tr><td>0&nbsp;=</td><td>disable automatic operation of the shutter</td></tr><tr><td>1&nbsp;=</td><td>enable automatic operation of the shutter</td></tr></tbody></table>

### *See Also* {#mmc_setautoshutter-see-also}

[MMC_SetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutterdevice), [MMC_SetShutterOpen](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutteropen)




<div className="command-signature">

## <strong>MMC_SetShutterOpen</strong>  	/Q /Z /L=<em>shutterLabel</em> <em>newState</em> {#mmc_setshutteropen}

</div>

Enables or disables automatic opening and closing of the active shutter when images are acquired.

### *Flags* {#mmc_setshutteropen-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *shutterDevice*</span> | Specifies the chosen shutter by a string containing the shutter's case-sensitive Micro-Manager device-label.  If the /L flag is omitted, the operation sets the state of the currently active shutter. |

### *Parameters* {#mmc_setshutteropen-parameters}

|  |  |
| --- | --- |
| *newState* | A numeric value, either 0 or 1 where 0 indicates the shutter should be closed (i.e. Open is False), and 1 indicates the shutter is to be opened (Open is True). |

### *See Also* {#mmc_setshutteropen-see-also}

[MMC_SetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutterdevice), [MMC_SetAutoShutter](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setautoshutter)





<div className="command-signature">

## <strong>MMC_InitializeCircularBuffer</strong>  /Q /Z {#mmc_initializecircularbuffer}

</div>

Resets the circular buffer, based on the size of images expected from the active camera.

### *Flags* {#mmc_initializecircularbuffer-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmc_initializecircularbuffer-details}
Micro-Manager's circular buffer is also initialized when an ROI is specified or changed.

### *See Also* {#mmc_initializecircularbuffer-see-also}

[MMC_GetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcircularbuffersize), [MMC_SetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcircularbuffersize), [MMC_ClearCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_clearcircularbuffer)







<div className="command-signature">

## <strong>MMC_ClearCircularBuffer</strong>  /Q /Z {#mmc_clearcircularbuffer}

</div>

Clears the contents of Micro-Manager's circular buffer, erasing any images that may be present.

### *Flags* {#mmc_clearcircularbuffer-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmc_clearcircularbuffer-details}
Micro-Manager's circular buffer is also cleared when an ROI is changed and when a acquisition-sequence is started.

### *See Also* {#mmc_clearcircularbuffer-see-also}

[MMC_GetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcircularbuffersize), [MMC_SetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcircularbuffersize), [MMC_InitializeCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializecircularbuffer), [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition)





<div className="command-signature">

## <strong>MMC_GetCircularBufferSize</strong>  ( ) {#mmc_getcircularbuffersize}

</div>

Returns a numeric value reporting the amount of memory (in MB) has been allocated to Micro-Manager's circular buffer.

### *Parameters* {#mmc_getcircularbuffersize-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_getcircularbuffersize-returns}

|  |  |
| --- | --- |
|  | A numeric value reporting the size of the circular buffer, as an integer number of MB. |

### *See Also* {#mmc_getcircularbuffersize-see-also}

[MMC_SetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcircularbuffersize), [MMC_InitializeCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializecircularbuffer), [MMC_ClearCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_clearcircularbuffer)




<div className="command-signature">

## <strong>MMC_SetCircularBufferSize</strong>  /Q /Z BuffSizeInMB {#mmc_setcircularbuffersize}

</div>

Sets the size of Micro-Manager's Circular Buffer, in MB.

### *Flags* {#mmc_setcircularbuffersize-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setcircularbuffersize-parameters}

|  |  |
| --- | --- |
| *BuffSizeInMB* | A integer value specifying, in MB, the new size of Micro-Manager's Circular Buffer. |

### *See Also* {#mmc_setcircularbuffersize-see-also}

[MMC_GetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcircularbuffersize), [MMC_InitializeCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializecircularbuffer), [MMC_ClearCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_clearcircularbuffer)





<div className="command-signature">

## <strong>MMC_IsSequenceRunning</strong>  ( ) {#mmc_issequencerunning}

</div>

Returns a numeric value indicating whether Micro-Manager is currently executing a sequential acquisition.

### *Parameters* {#mmc_issequencerunning-parameters}

|  |  |
| --- | --- |
|  | None. |

### *Returns* {#mmc_issequencerunning-returns}

|  |  |
| --- | --- |
|  | A numeric value containing the integer number of bits used to encode the intensity of each pixel returned by the active camera. |

### *Details* {#mmc_issequencerunning-details}
If the camera returns multiple color planes (ex. RGBA), the returned value represents the bit-depth of each individual color-plane, not the aggregate bit-depth of all of the color-planes.

"This value should be used only as a guideline - it does not guarantee that image buffer will contain only values from the returned dynamic range." [From Micro-Manager API.]

### *See Also* {#mmc_issequencerunning-see-also}

[https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html](https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html)







<div className="command-signature">

## <strong>MMC_PrepareSequenceAcquisition</strong>  /Q /Z /L=<em>cameraLabel</em> {#mmc_preparesequenceacquisition}

</div>

Prepares the camera for starting a sequential acquisition.

### *Flags* {#mmc_preparesequenceacquisition-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | An optional string containing the case-sensitive Micro-Manager label of the specified camera.  If the /L flag is omitted, then the operation prepares the currently active camera for sequential acquisition. |

### *See Also* {#mmc_preparesequenceacquisition-see-also}

[MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition), [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition)





<div className="command-signature">

## <strong>MMC_StartSequenceAcquisition</strong>   /Q /Z /N=<em>imageCount</em> /A /O /CLRO=<em>colorOrder</em> /MD=<em>mode</em>  /I=<em>imageInterval</em> {#mmc_startsequenceacquisition}

</div>

Launches a sequential acquisition.

### *Flags* {#mmc_startsequenceacquisition-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/N = *imageCount*</span> | Specifies the number of images to be acquired in the sequence.  If omitted, MMI starts acquisition of a continuous sequence, overwriting the previous image as each new image is acquired. |
| <span class="table-cell-nowrap">/A</span> | (Valid only when used together with /N flag.) 'Append' mode instructs MMI to append acquired images to the bound streaming wave, rather than overwriting the previously acquired image.  MMI appends acquired images as either consecutive layers (in the case of 2d images), or as consecutive chunks (in the case of 3d images, such as RGB or RGBA). |
| <span class="table-cell-nowrap">/O</span> | 'Overflow' instructs Micro-Manager to stop acquisition if its circular buffer fills. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGBA) in the string. |
| <span class="table-cell-nowrap">/MD = *mode*</span> | Specifies how MMI should handle the metadata for each acquired image.  Modes 1 and 2 are valid only if a text wave was specified to receive the metadata, via a previous call to [MMI_BindMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindmetadatawave). |
|  |<table class="nested-table"><tbody><tr><td>mode&nbsp;=&nbsp;0</td><td>Do not save metadata for acquired images.</td></tr><tr><td></td><td>This is the default case and is equivalent to omitting the/MD flag.</td></tr><tr><td>mode&nbsp;=&nbsp;1</td><td>Save only the metadata for the most recently acquired image.</td></tr><tr><td>mode&nbsp;=&nbsp;2</td><td>Save the metadata for each image as it is acquired.</td></tr><tr><td></td><td>The metadata for each acquired image are appended as consecutive layers to the bound metadata wave.  Applicable only when /A and /N flags are also specified.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/I</span> | Specifies the interval (in milliseconds) between acquisition of consecutive images.  If omitted, the interval is set to the current exposure time of the current camera. |

### *Details* {#mmc_startsequenceacquisition-details}
This operation must be preceded by a call to [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave) to notify MMI which wave is to receive the incoming image stream.

### *See Also* {#mmc_startsequenceacquisition-see-also}

[MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave), [MMI_BindMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindmetadatawave), [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition), [MMC_SetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcircularbuffersize), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)







<div className="command-signature">

## <strong>MMC_StopSequenceAcquisition</strong>   /Q /Z /W /L=<em>cameraLabel</em> /TO=<em>timeOut</em> {#mmc_stopsequenceacquisition}

</div>

Halts a previously started sequential acquisition.

### *Flags* {#mmc_stopsequenceacquisition-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/W</span> | 'Wait' mode instructs MMI to monitor Micro-Manager (for up to 5 seconds), after issuing the 'stop sequence acquisition' command, and not to return to Igor until Micro-Manager reports that sequential acquisition is no longer running.  If Micro-Manager fails to report the of sequential acquisition within the 5 second window, MMI returns a time-out error, `MMIERR_MMTIMEOUT`. |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | Specifies the Micro-Manager label of the camera whose sequential acquisition is to be halted.  MMI currently supports acquisition from only one camera at a time. |
| <span class="table-cell-nowrap">/TO = *timeOut*</span> | Specifies the maximum amount of time, in seconds, that MMI should wait for Micro-Manager to halt acquisition.  MMI uses the timeOut specification only when the /W (wait) flag is also specified.  The timeOut parameter must be between 0 and 2,147,483 seconds.  If no timeOut period is specified, the default is 5 seconds. |

### *See Also* {#mmc_stopsequenceacquisition-see-also}

[MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition), [MMC_IsSequenceRunning](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_issequencerunning)





<div className="command-signature">

## <strong>MMI_BindImageWave</strong>  /Q /Z /U imageWave {#mmi_bindimagewave}

</div>

Defines which wave is to receive single acquired images.

### *Flags* {#mmi_bindimagewave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/U</span> | Unlock wave, if needed, prior to assigning it for sequential acquisition.  If the /U flag is omitted and the wave is locked, MMI will raise an error, as it will be unable to adjust the wave's data-type or dimensions to match the image expected from the camera. |

### *Parameters* {#mmi_bindimagewave-parameters}

|  |  |
| --- | --- |
| *imageWave* | The real, numeric wave which is to receive the images.  Free waves may not be bound as image waves. |

### *Details* {#mmi_bindimagewave-details}
If imageWave is not large enough to accept one frame from the currently active camera, MMI_BindImageWave attempts to redimension the wave to accept one frame.  If imageWave is larger than one frame, its dimensions are not changed.  The same wave may be bound by both [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave) and [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave).

Calling MMI_BindImageWave tells Igor that the wave is 'in use', in the same way a wave is 'in use' when it is displayed in a graph or a table.  Accordingly, such a bound wave cannot be deleted until it is released by a subsequent call to [MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave) or [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset).

### *See Also* {#mmi_bindimagewave-see-also}

[MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave), [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave)







<div className="command-signature">

## <strong>MMI_ReleaseImageWave</strong>  /Q /Z {#mmi_releaseimagewave}

</div>

Releases a wave previously bound for acquiring single images.

### *Flags* {#mmi_releaseimagewave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmi_releaseimagewave-details}
No error occurs when MMI_ReleaseImageWave is called if [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave) has not yet been called, or if no image-wave is currently bound.

### *See Also* {#mmi_releaseimagewave-see-also}

[MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave), [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave)







<div className="command-signature">

## <strong>MMI_BindSequenceWave</strong>  /Q /Z /F /U sequenceWave {#mmi_bindsequencewave}

</div>

Defines which wave is to receive sequentially acquired (streamed) images.

### *Flags* {#mmi_bindsequencewave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/F</span> | 'Freeze' wave dimensions as they are, preventing MMI from adjusting the wave's dimensions to accept exactly one frame (image) from the currently assigned camera.  This flag is useful if you have prepared a wave to accept multiple images, ex. in preparing to call [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition) with the /A (Append) flag. |
| <span class="table-cell-nowrap">/U</span> | Unlock wave, if needed, prior to assigning it for sequential acquisition.  If the /U flag is omitted and the wave is locked, MMI will raise an error, as it will be unable to adjust the wave's data-type or dimensions to match the images expected from the camera. |

### *Parameters* {#mmi_bindsequencewave-parameters}

|  |  |
| --- | --- |
| *sequenceWave* | The numeric wave which is to receive the sequence (stream) of images.  MMI resets the numeric type and the dimensions of the wave to match the size of the images expected from the active camera.  Free waves may not be bound as sequence waves. |

### *Details* {#mmi_bindsequencewave-details}
The same wave may be bound for both snapping single images and for sequential (streaming) acquisition, by specifying the same wave when calling [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave) and [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave).

Calling MMI_BindSequenceWave tells Igor that the wave is 'in use', in the same way a wave is 'in use' when it is displayed in a graph or a table.  Accordingly, such a bound wave cannot be deleted until it is released by a subsequent call to [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave) or [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset).

### *See Also* {#mmi_bindsequencewave-see-also}

[MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave), [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition), [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition)







<div className="command-signature">

## <strong>MMI_ReleaseSequenceWave</strong>  /Q /Z {#mmi_releasesequencewave}

</div>

Releases a wave previously bound for acquiring image-sequences.

### *Flags* {#mmi_releasesequencewave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmi_releasesequencewave-details}
No error occurs when MMI_ReleaseSequenceWave is called if [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave) has not yet been called, or if no sequence-wave is currently bound.

### *See Also* {#mmi_releasesequencewave-see-also}

[MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave), [MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave)







<div className="command-signature">

## <strong>MMI_DoUpdate</strong>  /Q /Z {#mmi_doupdate}

</div>

Checks if the bound sequence-wave has been updated by acquisition of a new image and immediately calls [DoUpdate](/igorpro/commands/doupdate.md) if the wave has been updated.

### *Flags* {#mmi_doupdate-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmi_doupdate-details}
If you run an Igor function while MMI is running a sequential acquisition, Igor does not pre-empt your Igor function to give MMI an opportunity to mark its bound sequence-wave as modified.  In this circumstance, MMI will not be able to alert Igor about the modified sequence-wave until your code gives MMI that opportunity. You have several coding options to give MMI a chance to check for changes in the sequence-wave.

The simplest option is for your code to call [DoXOPIdle](/igorpro/commands/doxopidle.md), which gives all running XOPs a chance to run.  This may however suspend your code for more time than desirable.  Your second, more focused option is to call MMI_DoUpdate.  This function asks MMI to call [DoUpdate](/igorpro/commands/doupdate.md) only if the sequence-wave has been modified.  Calling MMI_DoUpdate permits your code to bypass other XOPs (if any) from running their IDLE event processing.  Your third and even more focused option is to call [MMI_GetUpdateState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_getupdatestate), which will report whether MMI's sequence-wave has been modified, without automatically calling DoUpdate.  The value returned by MMI_GetUpdateState allows your code to decide which, if any, windows to update and when to do so, based on your requirements.

### *See Also* {#mmi_doupdate-see-also}

[MMI_GetUpdateState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_getupdatestate), [DoUpdate](/igorpro/commands/doupdate.md), [DoXOPidle](/igorpro/commands/doxopidle.md)







<div className="command-signature">

## <strong>MMI_GetUpdateState</strong>  ( ) {#mmi_getupdatestate}

</div>

Returns a numeric value; zero if the sequence-wave has not been updated since the last call, or a non-zero value if the sequence-wave has been updated.  This function does not call DoUpdate, leaving to the caller all decisions about which windows to update and when to update them.

### *Parameters* {#mmi_getupdatestate-parameters}

|  |  |
| --- | --- |
|  | (None) |

### *Details* {#mmi_getupdatestate-details}
If you run an Igor function while MMI is running a sequential acquisition, Igor does not pre-empt your Igor function to give the MMI XOP an opportunity to mark its bound sequence-wave as modified.  In this circumstance, MMI will not be able to alert Igor about the modified sequence-wave until your code gives MMI that opportunity. You have several coding options to give the MMI XOP a chance to check for changes in the sequence-wave.

The simplest option is for your code to call [DoXOPIdle](/igorpro/commands/doxopidle.md), which gives all running XOPs a chance to run.  This may however suspend your code for more time than desirable.  Your second, more focused option is to call MMI_DoUpdate.  It calls only the MMI XOP, asking it to call [DoUpdate](/igorpro/commands/doupdate.md) only if the sequence-wave has been modified.  Calling MMI_DoUpdate permits your code to bypass other XOPs (if any) from running their IDLE event processing.  Your third and yet more focused option is to call [MMI_GetUpdateState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_getupdatestate), which will report whether the sequence-wave has been modified, without automatically calling DoUpdate.  The value returned by MMI_GetUpdateState allows your code to decide which, if any, windows to update and when to do so, based on your requirements.

### *See Also* {#mmi_getupdatestate-see-also}

[MMI_DoUpdate](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_doupdate), [DoUpdate](/igorpro/commands/doupdate.md), [DoXOPidle](/igorpro/commands/doxopidle.md)







<div className="command-signature">

## <strong>MMI_BindImageProcessor</strong>  /Q /Z functionName {#mmi_bindimageprocessor}

</div>

Defines a user-provided Igor function which MMI will call after acquisition of each single (non-streaming) image.

### *Flags* {#mmi_bindimageprocessor-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmi_bindimageprocessor-parameters}

|  |  |
| --- | --- |
| *functionName* | A string containing the name of the user-provided Igor function that is to be called each time an image is acquired. |

### *Details* {#mmi_bindimageprocessor-details}
The named function must accept five parameters, and must return a real, double-precision value, as shown here.  The function should return 0 under normal circumstances and return other values only to report errors.

```igor
Function MyImageProcessor (wave imgWave, variable OffRow, variable OffCol, variable OffLayer, variable OffChunk)
    <insert your processing code here>
    return 0
End
```

The function's first parameter must be a reference to a numeric wave.  When MMI calls the specified function, this parameter will contain a reference to the wave that received the newly acquired image.

The function's second through fifth parameters indicate where in the recipient wave the newly acquired image was stored.  When the recipient wave holds only one image, these parameters will all be zero.  If, however, multiple images are being acquired into a single wave via calls to [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), then the parameters form a vector within the wave to the origin (top, left corner) of the newly acquired image.

To halt MMI calls to the bound function upon acquisition of single images, call the operation [MMI_ReleaseImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimageprocessor).

### *See Also* {#mmi_bindimageprocessor-see-also}

[MMI_ReleaseImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimageprocessor), [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage)







<div className="command-signature">

## <strong>MMI_ReleaseImageProcessor</strong>  /Q /Z {#mmi_releaseimageprocessor}

</div>

Instructs MMI to stop calling the user-provided Igor function previously defined for execution following acquisition of each single image.

### *Flags* {#mmi_releaseimageprocessor-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmi_releaseimageprocessor-details}
No error occurs when MMI_ReleaseImageProcessor is called if [MMI_BindImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimageprocessor) has not yet been called, or if no function is currently bound.

### *See Also* {#mmi_releaseimageprocessor-see-also}

[MMI_BindImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimageprocessor)







<div className="command-signature">

## <strong>MMI_BindSequenceProcessor</strong>  /Q /Z functionName {#mmi_bindsequenceprocessor}

</div>

Tells MMI which user-provided function is to be called to process images relayed to Igor during sequential acquisition.

### *Flags* {#mmi_bindsequenceprocessor-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmi_bindsequenceprocessor-parameters}

|  |  |
| --- | --- |
| *functionName* | A string containing the name of the user-provided Igor function used to process images acquired during sequential acquisition. |

### *Details* {#mmi_bindsequenceprocessor-details}
The named function must accept five parameters, and must return a real, double-precision value, as shown here.  The function should return 0 under normal circumstances and return other values only to reprot errors.

```igor
Function MySequenceProcessor (wave imgWave, variable OffRow, variable OffCol, variable OffLayer, variable OffChunk)
    <insert your processing code here>
    return 0
End
```

The function's first parameter must be a reference to a numeric wave.  When MMI calls the specified function, this parameter will contain a reference to the wave that received the newly acquired image.

The function's second through fifth parameters indicate where in the recipient wave the newly acquired image was stored.  When the recipient wave holds only one image, these parameters will all be zero.  If, however, multiple images are being acquired into a single wave via calls to [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), then the parameters form a vector within the wave to the origin (top, left corner) of the newly acquired image.

To halt MMI calls to the bound function upon acquisition of sequential images, call the operation [MMI_ReleaseSequenceProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequenceprocessor).

Note that MMI calls the specified processor-function as part of its response to the 'IDLE message' sent from Igor.  This design carries several important implications, especially when acquiring sequentially at high-frame rates.

The sequence processor cannot process frames at rates faster than the rate at which MMI receives IDLE messages from Igor.  Thus MMI cannot guarantee that the processor function will be able to process every frame acquired by Micro-Manager.  You may want to consider carefully adjusting the frequency with which Igor passes the IDLE message to MMI to help 'tune' performance of your processor function.  See help on Igor's [SetIdlePeriod](/igorpro/commands/setidleperiod.md) operation for more details.

The processor-function runs on Igor's main thread, which is blocked from performing other tasks while the processor function is running.  Thus while your processor function is running, Igor cannot update other windows nor respond to user input from the mouse or keyboard.  Further, if the sequence processor-function hangs or falls into an infinite loop, Igor will hang.

Because the processor-function operates directly on the wave bound for receiving sequentially acquired images, that wave is unavailable to receive new images so long as the processor function is running.  In other words, MMI cannot receive new sequential images from Micro-Manager so long as the processor-function is running.

MMI provides the SequenceRelayDivisor mechanism to throttle the rate at which incoming sequential images are relayed to Igor's bound wave, and thus the rate at which the sequential-processor function is called.  See [MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor) and [MMI_GetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getsequencerelaydivisor) for more details.

### *See Also* {#mmi_bindsequenceprocessor-see-also}

[MMI_ReleaseSequenceProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequenceprocessor), [MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor), [SetIdlePeriod](/igorpro/commands/setidleperiod.md)







<div className="command-signature">

## <strong>MMI_ReleaseSequenceProcessor</strong>  /Q /Z {#mmi_releasesequenceprocessor}

</div>

Tells MMI that no user-provided function is to be called to process images acquired during sequential acquisition.

### *Flags* {#mmi_releasesequenceprocessor-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *See Also* {#mmi_releasesequenceprocessor-see-also}

[MMI_BindSequenceProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequenceprocessor)







<div className="command-signature">

## <strong>MMI_BindMetaDataWave</strong>  /Q /Z /U metaDataWave {#mmi_bindmetadatawave}

</div>

Defines a user-provided Igor text wave into which MMI will write the meta-data of sequentially acquired images.

### *Flags* {#mmi_bindmetadatawave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/U</span> | Unlock wave, if needed, prior to assigning it for sequential acquisition.  If the /U flag is omitted and the wave is locked, MMI will raise an error, as it will be unable to adjust the wave's dimensions to match the number of images expected from the camera. |

### *Parameters* {#mmi_bindmetadatawave-parameters}

|  |  |
| --- | --- |
| *metaDataWave* | The text wave which is to receive the meta-data for sequentially-acquired images.    Free waves may not be bound as meta-data waves. |

### *Details* {#mmi_bindmetadatawave-details}
The meta-data 'mode' dictates which images' meta-data are saved to the wave, and is set by the /MD flag when calling [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition).  If metadata are to be saved, then MMI_BindMetaDataWave must be called before [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition).

Calling MMI_BindMetaDataWave tells Igor that the wave is 'in use', in the same way a wave is 'in use' when it is displayed in a graph or a table.  Accordingly, such a bound wave cannot be deleted until it is released by a subsequent call to [MMI_ReleaseMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasemetadatawave) or [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset).

### *See Also* {#mmi_bindmetadatawave-see-also}

[MMI_ReleaseMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasemetadatawave), [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition)







<div className="command-signature">

## <strong>MMI_ReleaseMetaDataWave</strong>  /Q /Z {#mmi_releasemetadatawave}

</div>

Releases a wave previously bound for acquiring metadata for image-sequences.

### *Flags* {#mmi_releasemetadatawave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Details* {#mmi_releasemetadatawave-details}
No error occurs when MMI_ReleaseMetaDataWave is called if [MMI_BindMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindmetadatawave) has not yet been called, or if no metadata wave is currently bound.

### *See Also* {#mmi_releasemetadatawave-see-also}

[MMI_BindMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindmetadatawave)







<div className="command-signature">

## <strong>MMI_WaitForSequenceCompletion</strong>  /Q /Z /I=<em>intervalMS</em> /T=<em>timeoutSecs</em> {#mmi_waitforsequencecompletion}

</div>

Waits until Micro-Manager has no sequential-acquisition underway.

### *Flags* {#mmi_waitforsequencecompletion-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/I = *intervalMS*</span> | Specifies how long (in milliseconds) the operation should sleep between checking if a sequential acquisition is underway.  If no user-defined interval is defined, MMI will use a default interval of 5 ms between checks. |
| <span class="table-cell-nowrap">/T = *timeOutSecs*</span> | Specifies the time-out period in seconds, i.e. the maximum period of time the operation should continue checking for sequential acquisition to stop.  If sequential acqusition has not halted by the end of the time-out period, the operation will return an error code.  If no time-out interval is specified, the operation will wait indefinitely.  See warnings below. |

### *Details* {#mmi_waitforsequencecompletion-details}

:::caution
Call this operation with care!  This operation runs on Igor's main user-thread and can lock that thread, freezing Igor's user-interface, especially if a long time-out period (or none) is defined.  Consider instead calling the function MMC_IsSequenceRunning from your own Igor procedure.
:::

### *See Also* {#mmi_waitforsequencecompletion-see-also}

[MMC_IsSequenceRunning](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_issequencerunning)




### State Device Control {#state-device-control}


<div className="command-signature">

## <strong>MMC_GetState</strong>  (<em>deviceLabel</em>) {#mmc_getstate}

</div>

Returns the current numeric state of the specified state-device.

### *Parameters* {#mmc_getstate-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the specified state-device. |

### *Returns* {#mmc_getstate-returns}

|  |  |
| --- | --- |
|  | A real, numeric value containing the operational state of the specified device. |

### *See Also* {#mmc_getstate-see-also}

[MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice), [MMC_SetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstate), [MMC_SetStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstatelabel)





<div className="command-signature">

## <strong>MMC_DefineStateLabel</strong>  /Q /Z deviceLabel, <em>stateID</em>, <em>stateLabel</em> {#mmc_definestatelabel}

</div>

Defines a state-label (a string) for the specified state of the specified device.

### *Flags* {#mmc_definestatelabel-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_definestatelabel-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the specified state-device. |
| *stateID* | A real, numeric value specifying the operational state to be linked to the string specified by stateLabel. |
| *stateLabel* | A string containing the case sensitive Micro-Manager label linked to the operational state identified by stateID. |

### *Details* {#mmc_definestatelabel-details}

|  |  |
| --- | --- |
|  | The specified stateLabel can provide a convenient or user-friendly nickname for the operational state specified by the often more abstract numeric stateID. |

### *See Also* {#mmc_definestatelabel-see-also}

[MMC_GetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getstate), [MMC_SetStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstatelabel)





<div className="command-signature">

## <strong>MMC_SetState</strong>  /Q /Z deviceLabel, <em>newStateID</em> {#mmc_setstate}

</div>

Sets the operational state of the specified device using the specified numeric identifier.

### *Flags* {#mmc_setstate-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setstate-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the specified state-device. |
| *newStateID* | A real, numeric value specifying the chosen operational state of the device. |

### *Details* {#mmc_setstate-details}

The specified stateLabel can provide a convenient or user-friendly nickname for the operational state specified by the often more abstract numeric stateID.

### *See Also* {#mmc_setstate-see-also}

[MMC_GetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getstate), [MMC_SetStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstatelabel)





<div className="command-signature">

## <strong>MMC_SetStateLabel</strong>  /Q /Z deviceLabel, <em>newStateLabel</em> {#mmc_setstatelabel}

</div>

Sets the operational state of the specified device using the specified label-string.

### *Flags* {#mmc_setstatelabel-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setstatelabel-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the specified state-device. |
| *newStateLabel* | A string specifying the state-label assigned to the chosen operational state for this device. |

### *Details* {#mmc_setstatelabel-details}

The specified stateLabel can provide a convenient or user-friendly nickname for the operational state specified by the often more abstract numeric stateID.

### *See Also* {#mmc_setstatelabel-see-also}

[MMC_GetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getstate), [MMC_DefineStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_definestatelabel), [MMC_SetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstate)



### Hub and Peripheral Devices {#hub-and-peripheral-devices}

<div className="command-signature">

## <strong>MMC_GetParentLabel</strong>  (<em>childLabel</em>) {#mmc_getparentlabel}

</div>

Identifies the 'parent' of a Micro-Manager device by returning the label of the parent-device.

### *Parameters* {#mmc_getparentlabel-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the device whose parent-device is sought. |

### *Returns* {#mmc_getparentlabel-returns}

|  |  |
| --- | --- |
|  | A string containing the case-sensitive Micro-Manager label of the device previously set as the parent of the specified device. |

### *See Also* {#mmc_getparentlabel-see-also}

[MMC_SetParentLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setparentlabel)





<div className="command-signature">

## <strong>MMC_SetParentLabel</strong>  /Q /Z deviceLabel, <em>parentLabel</em> {#mmc_setparentlabel}

</div>

Sets the parent hub of the specified device, linking the device to the specified hub.

### *Flags* {#mmc_setparentlabel-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

### *Parameters* {#mmc_setparentlabel-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case sensitive Micro-Manager label assigned to the device whose parent-device is being set. |
| *parentHubLabel* | A string containing the case sensitive Micro-Manager label assigned to the parent-device. |

### *See Also* {#mmc_setparentlabel-see-also}

[MMC_GetParentLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getparentlabel)