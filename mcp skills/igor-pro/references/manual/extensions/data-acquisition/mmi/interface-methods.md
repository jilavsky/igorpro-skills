---
description: "Downloads and stores the Windows installer for the version of Micro-Manager appropriate for the running version of MMI."
slug: /extensions/data-acquisition/mmi/interface-methods
---

# Interface Summary {#interface-summary}

### Supervisory Interface {#supervisory-interface}

|  |  |
| --- | --- |
| [MMI_DownloadMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_downloadmm) | Downloads and stores the Windows installer for the version of Micro-Manager appropriate for the running version of MMI. |
| [MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm) | Runs the Windows installer downloaded by MMI_DownloadMM, installing Micro-Manager on the computer, and preparing Micro-Manager to work with MMI. |
| [MMI_GetMMstatus](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getmmstatus) | Reports the status of the installation of Micro-Manger. |
| [MMI_GetXOPversion](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getxopversion) | Returns an Igor string containing the version number of the MMI XOP. |
| [MMI_GetDataFolderPath](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdatafolderpath) | Returns an Igor string containing the absolute path to the data folder MMI uses to report the outcomes of its functions and operations. |
| [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist) | Returns an Igor text wave |
| [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset) | Resets the interface between Igor and Micro-Manager, releasing all bound waves and closing all open files.  Also releases and re-creates the Micro-Manager core, the stream manager, and the default stream-sinks. |
| [MMI_Shutdown](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_shutdown) | Closes the interface between Igor and Micro-Manager, releasing all resources and waves, closing all open HDF5 files, and deleting the MMI reporting variables. |
| [MMI_GetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getsequencerelaydivisor) | Returns the frequency (1/n) with which the Igor stream-manager relays incoming frames from an active stream to the recipient Igor wave. |
| [MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor) | Sets the frequency (1/n) with which the Igor stream-manager relays incoming frames from the active stream to the recipient Igor wave. |
| [MMI_BindImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimagewave) | Tells MMI to hold the named Igor wave for receiving images acquired by calls to [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage). |
| [MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave) | Tells MMI to release the Igor wave held for receiving images acquired by calls to [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage). |
| [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave) | Tells MMI to hold the named Igor wave for receiving sequentially acquired images using [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition). |
| [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave) | Tells MMI to release the Igor wave held for receiving images acquired through streaming operations. |
| [MMI_GetUpdateState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_getupdatestate) | Reports whether MMI has modified the bound sequence-wave.  The result can be used to determine when and how to call DoUpdate. |
| [MMI_DoUpdate](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_doupdate) | Performs the same check as [MMI_GetUpdateState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_getupdatestate) and immediately calls [DoUpdate](/igorpro/commands/doupdate.md) if the sequence-wave has been modified. |
| [MMI_BindImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindimageprocessor) | Tells MMI which user-provided function should be called to process each single image after acquisition. |
| [MMI_ReleaseImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimageprocessor) | Tells MMI that no user-provided function should be called following acquisition of each single image. |
| [MMI_BindSequenceProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequenceprocessor) | Tells MMI which user-provided function should be called to process images acquired during sequential acquisition. |
| [MMI_ReleaseSequenceProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequenceprocessor) | Tells MMI that no user-provided function should be called to process images acquired during sequential acquisition. |
| [MMI_BindMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindmetadatawave) | Tells MMI to hold the named Igor text wave for receiving the metadata from sequentially acquired images. |
| [MMI_ReleaseMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasemetadatawave) | Tells MMI to release the Igor text wave held for receiving the metadata from sequentially acquired images. |
| [MMI_WaitForSequenceCompletion](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_waitforsequencecompletion) | Tells MMI to wait until Micro-Manager has no sequential-acquisition underway. |
| [MMI_OpenH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5stream) | Creates and initializes an instance of the HDF5 streamer, if one does not already exist. |
| [MMI_CloseH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5stream) | Closes and deletes the current HDF5 streamer, if one exists, first closing all files or groups currently open. |
| [MMI_IsH5streamOpen](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_ish5streamopen) | Reports if the HDF5 streamer is open. |
| [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) | Instructs the HDF5 streamer to open an HDF5 file with the proposed name, returning a unique numeric identifier, the fileID. |
| [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file) | Instructs the HDF5 streamer to close the HDF5 file identified by the provided fileID. |
| [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file) | Instructs the HDF5 streamer to set as 'active' the HDF5 file identified by the provided ID. |
| [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group) | Instructs the HDF5 streamer to open an HDF5 group within a previously opened HDF5 file.  Returns a unique numeric identifier, the groupID. |
| [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group) | Instructs the HDF5 streamer to close the HDF5 group identified by the provided groupID. |
| [MMI_SelectH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5group) | Instructs the HDF5 streamer to set as 'active' the HDF5 group identified by the provided groupID. |
| [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist) | Gets a list of properties for the device whose label is specified.  The list includes the name, value, type, whether the property can be changed, and (if applicable), minimum and maximum permissible values. |
| [MMI_GetEstMaxFrameCount](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getestmaxframecount) | Returns the maximum number of frames that MMI estimates can be acquired and appended directly into memory. |
| [MMI_GetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdisableddevices) | Returns a list of Micro-Manager devices marked as disabled for use by MMI. |
| [MMI_SetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setdisableddevices) | Defines the list of Micro-Manager devices to be marked as disabled for use by MMI. |
| [MMI_AddDisabledDevice](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_adddisableddevice) | Adds one or more devices to the existing list marked as disabled for use by MMI. |
| [MMI_IsDeviceDisabled](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_isdevicedisabled) | Reports whether a specified device is in the list marked as disabled for use by MMI. |
| [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) | A substitute for Igor's previous GetCamera operation. |
| [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera) | A substitute for Igor's previous NewCamera operation. |
| [MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera) | A substitute for Igor's previous ModifyCamera operation. |

### Micro-Manager Interface {#micro-manager-interface}

### Initialization and Setup {#initialization-and-setup}

|  |  |
| --- | --- |
| [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice) | Creates and assigns an identifying label to a new software device-interface for a supported piece of hardware (ex. camera, shutter, filter-wheel, light-source, etc.). |
| [MMC_UnloadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloaddevice) | Releases a device-interface created by a previous call to MMC_LoadDevice. |
| [MMC_UnloadAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloadalldevices) | Releases all previously created device-interfaces. |
| [MMC_InitializeAllDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializealldevices) | Initializes all previously created device-interfaces and their corresponding hardware. |
| [MMC_InitializeDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializedevice) | Initializes the device-interface and the corresponding hardware associated with the provided device-label. |
| [MMC_Reset](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_reset) | Resets Micro-Manager's core, releasing all previously created device-interfaces. |
| [MMC_UpdateCoreProperties](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_updatecoreproperties) | Updates Micro-Manager's core properties (its set of assigned devices), using the currently loaded devices. |
| [MMC_GetCoreErrorText](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcoreerrortext) | Returns the Micro-Manager error text corresponding to the specified numeric error code. |
| [MMC_GetVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getversioninfo) | Returns the version number of Micro-Manager's core. |
| [MMC_GetAPIVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getapiversioninfo) | Returns the version numbers of Micro-Manager's Module-API and Device-API. |
| [MMC_SaveSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemstate) | Saves the current state of the system (i.e. the status of writable properties) to the named file. |
| [MMC_LoadSystemState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemstate) | Loads the current state of the system (i.e. the status of writable properties) from the named file. |
| [MMC_SaveSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_savesystemconfig) | Saves the current configuration of the system (devices loaded, their labels, etc.) to the named file. |
| [MMC_LoadSystemConfig](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loadsystemconfig) | Installs the current configuration of the system (devices loaded, their labels, etc.) from the named file. |

### Logging and Log Management {#logging-and-log-management}

|  |  |
| --- | --- |
| [MMC_SetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setprimarylogfile) | Sets the named file as Micro-Manager's primary log file. |
| [MMC_GetPrimaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getprimarylogfile) | Returns a string containing the name of Micro-Manager's primary log file. |
| [MMC_LogMessage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_logmessage) | Appends a message to Micro-Manager's primary log file. |
| [MMC_EnableDebugLog](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_enabledebuglog) | Enables or disables logging of Micro-Manager's debug messages. |
| [MMC_DebugLogEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_debuglogenabled) | Returns a numeric value indicating whether logging of debug messages is enabled. |
| [MMC_EnableStdErrLog](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_enablestderrlog) | Enables or disables sending Micro-Manager's log messages to the 'standard error' (stderr) file.  This is primarily for those developing code for Micro-Manager. |
| [MMC_StdErrLogEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stderrlogenabled) | Returns a numeric value indicating whether log messages are being sent to the 'standard error' (stderr) file.  This is primarily for those developing code for Micro-Manager. |
| [MMC_StartSecondaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsecondarylogfile) | Starts Micro-Manager's capturing of logging output into an additional file. |
| [MMC_StopSecondaryLogFile](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsecondarylogfile) | Halts Micro-Manager's capturing of logging output into an additional file. |

### Device Listing {#device-listing}

|  |  |
| --- | --- |
| [MMC_GetAvailableDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getavailabledevices) | Gets a list of the names of the devices available from the specified module (device-adapter), each together with its device-type and description. |
| [MMC_GetLoadedDevices](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getloadeddevices) | Gets a list of the names of the currently loaded devices. |
| [MMC_GetDeviceAdapterNames](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdeviceadapternames) | Gets a list of root-names for all discoverable device-adapters. |

### Generic Device Control {#generic-device-control}

|  |  |
| --- | --- |
| [MMC_GetDeviceType](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicetype) | Returns the device-type for a device specified by its label. |
| [MMC_GetDeviceName](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicename) | Returns the device-name for a device specified by its label. |
| [MMC_GetDeviceLibrary](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getdevicelibrary) | Returns the root-name of the device-adapter for a device specified by its label. |
| [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring) | Returns a string containing the value of a named property for a device specified by its label. |
| [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric) | Returns a numeric value containing the value of a named property for a device specified by its label. |
| [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty) | Sets the value of the named property for a device specified by its label. |
| [MMC_GetAllowedPropertyValues](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getallowedpropertyvalues) | Gets a list of allowed text values for the named string property for the device whose label is specified. |
| [MMC_IsPropertyReadOnly](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ispropertyreadonly) | Reports if named property of the named device is (or is not) a read-only property. |
| [MMC_IsPropertyPreInit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ispropertypreinit) | Reports if named property of the named device must be defined prior to initialization. |
| [MMC_HasPropertyLimits](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_haspropertylimits) | Reports if named numeric property of the named device has defined upper- and lower-limits to its permitted values. |
| [MMC_GetPropertyLowerLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertylowerlimit) | Reports the minimum permitted value of the named numeric property of the named device. |
| [MMC_GetPropertyUpperLimit](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertyupperlimit) | Reports the maximum permitted value of the named numeric property of the named device. |
| [MMC_GetTimeoutMs](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_gettimeoutms) | Returns Micro-Manager's timeout period. |
| [MMC_SetTimeoutMs](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_settimeoutms) | Sets Micro-Manager's timeout period. |

### Management of Current Device for Specific Roles {#management-of-current-device-for-specific-roles}

|  |  |
| --- | --- |
| [MMC_GetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcameradevice) | Returns the Micro-Manager label for the active camera. |
| [MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice) | Sets the currently active camera. |
| [MMC_GetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getshutterdevice) | Returns the Micro-Manager label for the active shutter. |
| [MMC_SetShutterDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutterdevice) | Sets the currently active shutter. |
| [MMC_GetFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getfocusdevice) | Returns the Micro-Manager label for the active focus device. |
| [MMC_SetFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setfocusdevice) | Sets the currently active focus device. |
| [MMC_GetXYStageDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getxystagedevice) | Returns the Micro-Manager label for the active XY stage. |
| [MMC_SetXYStageDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setxystagedevice) | Sets the active XY stage. |
| [MMC_GetAutoFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getautofocusdevice) | Returns the Micro-Manager label for the active auto-focus device. |
| [MMC_SetAutoFocusDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setautofocusdevice) | Sets the currently active auto-focus device. |
| [MMC_GetSLMDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getslmdevice) | Returns the Micro-Manager label for the active spatial light modulator (SLM). |
| [MMC_SetSLMDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setslmdevice) | Sets the active spatial light modulator (SLM). |
| [MMC_SetGalvoDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setgalvodevice) | Returns the Micro-Manager label for the active galvanometer beam-steering device. |
| [MMC_GetGalvoDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getgalvodevice) | Sets the active galvanometer beam-steering device. |

### Image Acquisition {#image-acquisition}

|  |  |
| --- | --- |
| [MMC_GetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getroi) | Returns a wave containing the ROI (Region Of Interest) for the specified camera. |
| [MMC_SetROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setroi) | Sets the ROI for the specified camera from the specified Igor wave. |
| [MMC_ClearROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_clearroi) | Resets the ROI for the active camera to the camera's full sensor. |
| [MMC_IsMultiROISupported](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroisupported) | Reports whether the active camera supports the use of multiple ROIs. |
| [MMC_IsMultiROIEnabled](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_ismultiroienabled) | Reports whether the active camera is currently using multiple ROIs. |
| [MMC_GetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getmultiroi) | Returns a wave describing the set of ROIs in use in the active camera. |
| [MMC_SetMultiROI](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setmultiroi) | Defines the set of ROIs to use in the active camera. |
| [MMC_GetNumberOfComponents](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getnumberofcomponents) |  |
|  | Returns the number of components (color channels) acquired by the active camera. |
| [MMC_GetExposure](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getexposure) | Returns the exposure time of the currently active camera, in milliseconds. |
| [MMC_SetExposure](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setexposure) | Sets the exposure time of the active camera, in milliseconds. |
| [MMC_InitializeCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializecircularbuffer) | Resets Micro-Manager's circular buffer, based on the dimensions of the images expected from the active camera. |
| [MMC_ClearCircularBuffer](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_clearcircularbuffer) | Clears the contents of Micro-Manager's circular buffer, erasing any images that may be present. |
| [MMC_GetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcircularbuffersize) | Returns the size of Micro-Manager's Circular Buffer, in MB. |
| [MMC_SetCircularBufferSize](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcircularbuffersize) | Sets the size of Micro-Manager's Circular Buffer, in MB. |
| [MMC_SetAutoShutter](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setautoshutter) | Enables or disables automatic opening and closing of the active shutter when images are acquired. |
| [MMC_SetShutterOpen](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setshutteropen) | Sets the open or closed state of the specified shutter. |
| [MMC_GetImageWidth](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimagewidth) | Returns the horizontal size (i.e. number of columns) of the image buffer, in pixels. |
| [MMC_GetImageHeight](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimageheight) | Returns the vertical size (i.e. number of rows) of the image buffer, in pixels. |
| [MMC_GetImageBitDepth](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimagebitdepth) | Returns the number of bits used to encode the intensity of each image pixel. |
| [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage) | Acquires a single image from the currently active camera. |
| [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage) | Retrieves a previously acquired image and writes it to a wave. |
| [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage) | Acquires a single image and writes it to a wave with finer control than MMC_GetImage. |
| [MMC_PrepareSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_preparesequenceacquisition) |  |
|  | Prepares the camera for starting a sequential acquisition. |
| [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition) |  |
|  | Launches a sequential acquisition. |
| [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition) |  |
|  | Halts a previously started sequential acquisition. |
| [MMC_IsSequenceRunning](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_issequencerunning) | Reports whether Micro-Manager is currently executing a sequential acquisition. |

### State Device Control {#state-device-control}

|  |  |
| --- | --- |
| [MMC_GetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getstate) | Returns the current numeric state of the specified device. |
| [MMC_DefineStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_definestatelabel) | Defines a state-label (a string) for the specified state of the specified device. |
| [MMC_SetState](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstate) | Sets the state of the specified device to the specified numeric state. |
| [MMC_SetStateLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setstatelabel) | Sets the state of the specified device to the numeric state previously defined for the specified state-label. |

### Hub and Peripheral Devices {#hub-and-peripheral-devices}

|  |  |
| --- | --- |
| [MMC_GetParentLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getparentlabel) | Identifies the 'parent' of a Micro-Manager device by returning the label of the parent-device. |
| [MMC_SetParentLabel](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setparentlabel) | Binds a Micro-Manager device to its 'parent' by specifying the label of the parent-device. |

## Interface Methods {#interface-methods}

<div className="command-signature">

### <strong>MMI_DownloadMM</strong>  /Q /Z /R /FILE=<em>fileName</em> /V=<em>verboseMode</em> /SRC=<em>pathName</em> /URL=<em>sourceURL</em> /DEST=<em>destPath</em> {#mmi_downloadmm}

</div>

Downloads and stores the Windows installer for the version of Micro-Manager appropriate for the running version of MMI.

#### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/DEST = *destPath*</span> | Specifies the path of the directory where the downloaded file is to be stored, overriding the destination directory normally selected by MMI, either the DESKTOP or TEMP directory, as set by the Windows environment variables. |
| <span class="table-cell-nowrap">/FILE = *fileName*</span> | Specifies the name of the installation file to be downloaded, overriding the default name stored within MMI. |
| <span class="table-cell-nowrap">/R</span> | 'Report' mode instructs MMI to simply report (without downloading) the default URL from which it would normally download the Micro-Manager installer.  MMI reports the URL by writing the string into Igor's history and to the global variable S_MMIresult in the MMI data folder. |
| <span class="table-cell-nowrap">/SRC = *pathName*</span> | Specifies the absolute path to a local copy of the Windows Micro-Manager installer.  The /SRC option takes precedence over the /URL and /FILE options. |
| <span class="table-cell-nowrap">/URL = *sourceURL*</span> | Specifies the name of the internet URL from which the file is to be downloaded, overriding the default name stored within MMI. |
| <span class="table-cell-nowrap">/V = *verboseMode*</span> | Sets the level of diagnostic messages printed in the history area of the command window.  *verboseMode* is also passed internally as the /V flag to Igor's [URLRequest](/igorpro/commands/urlrequest.md) operation.  *verboseMode* overrides the state of the /Q flag. |
|  |<table class="nested-table"><tbody><tr><td>/V=0:</td><td>Do not print any diagnostic messages. This is the default.</td></tr><tr><td>/V=1:</td><td>Prints an error message if a run time error occurs.</td></tr><tr><td>/V=2:</td><td>Prints full debugging information.</td></tr></tbody></table>

#### *Details* {#details}
If no flags are specified, MMI calls Igor's [URLRequest](/igorpro/commands/urlrequest.md) operation to perform the download and to save the received file.

Users installing MMI on computers isolated from the internet can download the Micro-Manager installer using some other, internet-connected computer, and then move the installer to the internet-isolated computer (ex. by using a thumb-drive).  In such cases, use the /SRC option to specify the path to the installer on the thumb-drive.

#### *See Also* {#see-also}

[MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm)





<div className="command-signature">

### <strong>MMI_InstallMM</strong>   /Q /Z /O /RJ /DIR=<em>destFolder</em> {#mmi_installmm}

</div>

Runs the Windows installer downloaded by MMI_DownloadMM, installing Micro-Manager on the computer, and prepares Micro-Manager to work with MMI

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/O</span> | 'Override' mode instructs MMI to install Micro-Manager even if it finds evidence of an existing installation.  If the /O flag is not used, the operation will halt if it finds evidence that its version of Micro-Manager is (or has been) previously installed. |
| <span class="table-cell-nowrap">/DIR = *destFolder*</span> | Specifies the path of the directory to be the root of the new installation of Micro-Manager.  If specified, this overrides the default location determined by the `PROGRAMFILES` environment variable and the name of the Windows installer. |
| <span class="table-cell-nowrap">/RJ</span> | The 'Remove Java' option instructs MMI to install Micro-Manager normally, but then to remove Micro-Manager's Java components after installation completes.  (This is intended mostly for labs concerned about the security implications of running Java code.)  Note though that choosing the /RJ option will make it impossible to run this installation of Micro-Manager as a free standing program. |

#### *Details* {#interface-methods-details}
MMI calls Igor's [URLRequest](/igorpro/commands/urlrequest.md) operation to perform the download and save the received file.

#### *See Also* {#interface-methods-see-also}

[MMI_DownloadMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_downloadmm)







<div className="command-signature">

### <strong>MMI_GetMMstatus</strong>  ( ) {#mmi_getmmstatus}

</div>

Returns a string describing the installation status of MMI's required version of Micro-Manager.

#### *Parameters* {#parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Example* {#example}
If MMI's version of Micro-Manager is properly installed, then typing the command

```igor
print MMI_GetMMstatus()
```

will yield a confirmation similar to:

```
Micro-Manager is installed and ready.
```

If MMI's version of Micro-Manager is not properly installed, the command will yield an error message containing details of the problem it encountered.

#### *See Also* {#interface-methods-see-also}

[Installing Micro-Manager](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md), [Manually Installing Micro-Manager](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#manually-installing-micro-manager), [MMI_DownloadMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_downloadmm), [MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm), [MMI_GetXOPversion](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getxopversion), [MMC_GetVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getversioninfo), [MMC_GetAPIversionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getapiversioninfo)





<div className="command-signature">

### <strong>MMI_GetXOPversion</strong>  ( ) {#mmi_getxopversion}

</div>

Returns an Igor string containing the version number of the MMI XOP.  For example, typing the following on Igor's command line

```igor
print MMI_GetXOPversion()
```

evokes the response

```
MMI.xop v.1.1.0.19
```

#### *See Also* {#interface-methods-see-also}

[MMC_GetVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getversioninfo), [MMC_GetAPIVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getapiversioninfo)





<div className="command-signature">

### <strong>MMI_GetDataFolderPath</strong>  ( ) {#mmi_getdatafolderpath}

</div>

Returns a string containing the absolute path to the data folder MMI uses to report the outcomes of its functions and operations.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Example* {#interface-methods-example}
Typing the command:

```igor
print MMI_GetDataFolderPath()
```

evokes a response of the form:

```
root:packages:MMI
```

#### *See Also* {#interface-methods-see-also}

[Output Variables & Error Handling](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#output-variables-error-handling)





<div className="command-signature">

### <strong>MMI_Reset</strong> {#mmi_reset}

</div>

Resets the MMI interface.  MMI_Reset halts any running sequences, releases any bound waves (image-wave, stream-wave, & metadata-wave), releases any bound processing functions, terminates the stream-manager, and resets and releases the Micro-Manager core, releasing all devices.  It then creates new instances of the Micro-Manager core and the stream-manager.

#### *See Also* {#interface-methods-see-also}

[MMI_Shutdown](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_shutdown), [MMC_Reset](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_reset), [MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave), [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave),  [MMI_ReleaseMetaDataWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasemetadatawave), [MMI_ReleaseImageProcessor](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimageprocessor)



<div className="command-signature">

### <strong>MMI_Shutdown</strong>  /Q /Z /DF {#mmi_shutdown}

</div>

Closes the interface between Igor and Micro-Manager, releasing all resources and waves, closing all open HDF5 files, and deleting MMI's Igor variables S_MMIresult, S_MMImessage, V_MMIverbose, V_MMIresult.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, MMI_Shutdown always returns success. |
| <span class="table-cell-nowrap">/DF</span> | Instructs MMI to also remove its data folder (root:packages\:mmI) *and any waves and variables it contains*, after deleting the variables it maintains there.  Note that using the /DF flag may result in an error if waves within that folder are in use (ex. in a graph or table). |

#### *Details* {#interface-methods-details}
Repeated calls to MMI_Shutdown take no further actions and simply return to the caller.

#### *See Also* {#interface-methods-see-also}

[MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset)







<div className="command-signature">

### <strong>MMI_GetDevicePropertyList</strong>  /Q /Z deviceLabel [, <em>recipientWave</em>, <em>prefix</em>] {#mmi_getdevicepropertylist}

</div>

Gets a list of properties for the device whose label is specified.  The list includes the name, value, type, whether the property can be changed, and (if applicable), minimum and maximum permissible values.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *deviceLabel* | A string containing the case-sensitive Micro-Manager label of the chosen device. |
| *recipientWave* | An optional name for the text wave to receive the list of properties for the chosen device.  If this parameter is omitted, MMI will create a text wave in the current data folder, using the base name "M_DeviceProperties." |
| *prefix* | An optional string containing text to add as a prefix to each element in the recipient wave.  This provides an simple means to insert [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) in each element, and hence a way to format the text when displayed in Igor controls, such as Listboxes. |

#### *See Also* {#interface-methods-see-also}

[MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty), [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring), [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric)





<div className="command-signature">

### <strong>MMI_GetSequenceRelayDivisor</strong>  ( ) {#mmi_getsequencerelaydivisor}

</div>

Returns a numeric value reflecting the frequency with which images in the incoming image-stream will be relayed to the designated Igor wave.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Details* {#interface-methods-details}
The integer value returned should be interpreted as the denominator of a fraction of the form 1/*n*, indicating that only '1 frame out of n' will be relayed to the Igor wave.  Thus a return value of 2 indicates that every second frame will be relayed to Igor.  A return value of 10 indicates that only 1 frame out of every 10 received will be relayed to Igor.

#### *See Also* {#interface-methods-see-also}

[MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor)







<div className="command-signature">

### <strong>MMI_SetSequenceRelayDivisor</strong>  /Q /Z newValue {#mmi_setsequencerelaydivisor}

</div>

Sets the frequency with which images in the incoming image-stream will be relayed to the chosen Igor wave.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *newValue* | A numeric value between 1 and (2e32)-1.  This should be interpreted as the denominator of a fraction of the form 1/n indicating that only '1 frame out of n' is to be relayed to the Igor wave. |

#### *Details* {#interface-methods-details}
Setting the stream relay-divisor to a value of 2 indicates that every 2nd image should be passed to the recipient wave.  Setting the divisor to a value of 10 instructs MMI that only every 10th wave should be passed to the recipient wave.  By relaying only a fraction of incoming images to Igor's recipient wave, you can reduce the time Igor spends refreshing the image, providing more time for acquisition and / or saving the incoming stream to a file.

The divisor's default value, installed upon startup or reset, is 1.  Permitted values are positive integers between 1 and (2e32)-1.

Note that the stream relay-divisor has no direct effect on the HDF5 streamer -- every sequentially acquired (streamed) image is relayed to the HDF5 streamer, independent of the value of the relay-divisor.

#### *See Also* {#interface-methods-see-also}

[MMI_GetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getsequencerelaydivisor), [MMI_OpenH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5stream)







<div className="command-signature">

### <strong>MMI_OpenH5stream</strong>  /Q /Z {#mmi_openh5stream}

</div>

Creates and initializes the HDF5 streamer, if it isn't already open.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | None. |

#### *Details* {#interface-methods-details}
To maintain the best possible performance, MMI does not automatically create an instance of the HDF5 streamer, which coordinates writing sequentially acquired (streamed) images to an HDF5 file.  Therefore the user must create an instance of the HDF5 streamer prior to attempting to store streamed images to an HDF5 file.

The stream relay-divisor only changes the frequency with which streamed images are relayed to Igor during acquisition.  The stream relay-divisor has no effect on how streamed images are written to HDF5 files.  Every sequentially acquired (streamed) image is relayed to the HDF5 streamer, independent of the value of the relay-divisor.

#### *See Also* {#interface-methods-see-also}

[MMI_CloseH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5stream), [MMI_IsH5streamOpen](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_ish5streamopen), [MMI_GetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getsequencerelaydivisor), [MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor)







<div className="command-signature">

### <strong>MMI_CloseH5stream</strong>  /Q /Z {#mmi_closeh5stream}

</div>

Closes and deletes the HDF5 streamer, if one exists, first closing any open HDF5 files and groups.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | None. |

#### *Details* {#interface-methods-details}
Calling MMI_CloseH5Stream automatically closes all open HDF5 groups and files.  Thus it may be easier to call MMI_CloseH5Stream instead of individually closing each open group and file.  If, however, you need to close specific group(s) or file(s), but not all, then you should separately call [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group) and [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file) for just those groups and files.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5stream), [MMI_IsH5streamOpen](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_ish5streamopen), [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file), [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group)







<div className="command-signature">

### <strong>MMI_IsH5streamOpen</strong>  ( ) {#mmi_ish5streamopen}

</div>

Returns a numeric value reporting whether the HDF5 streamer is currently open.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Returns* {#returns}

|  |  |
| --- | --- |
|  | Returns 1 if the HDF5 streamer is open. |
|  | Returns 0 if the HDF5 streamer is closed. |

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5stream), [MMI_CloseH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5stream)





<div className="command-signature">

### <strong>MMI_OpenH5file</strong>  /Q /Z /O fileID, <em>fileName</em> {#mmi_openh5file}

</div>

Creates a new HDF5 file with the specified filename, selects that file as the currently active file, and returns a unique file ID.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/O</span> | 'Overwrite' mode instructs MMI to replace any pre-existing file that has the same name.  If a named file exists and the /O flag is not specified, then the existing file is re-opened and subsequent calls to [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group) will append new groups to the pre-existing file. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *fileID* | A real (non-complex) numeric variable which will receive the ID number assigned to the newly created HDF5 file.  The file ID number will be an integer greater than or equal to 1. |
| *fileName* | A string that specifies the path- and file-name of the HDF5 file to be created.  Simple filenames and relative paths are interpreted relative to the location of the file MMI64.xop, usually c:\Program Files\Wavemetrics\Igor 10 Pro Folder\More Extensions (64-bit)\Data Acquisition\MMI.  We recommend you use a full path to specify your destination file. |
|  | If you use Windows path notation, you should use 'doubled' backslash characters as separators, ex. |
|  | <code class="igor">MMI_OpenH5file v_FileID, "c:\\\\temp\\\\myHDF5file.h5"</code> |
|  | MMI also supports the use of Macintosh HFS path separators (even though MMI runs only under Windows), ex. |
|  | <code class="igor">MMI_OpenH5file v_FileID, "c:temp:myHDF5file.h5"</code>
|  | See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for more details. |

#### *Details* {#interface-methods-details}
MMI_OpenH5file assumes its incoming images will be acquired using the current configuration of the currently active camera.  The operation thus prepares internally to match the format of the images (ex. image-width and -height, number of bits-per-pixel, number of color-planes, etc.) from that camera.

MMI requires that images from separate cameras (or separate configurations of a camera) be written either to separate HDF5 files, or that a given HDF5 file be closed and re-opened with a different active camera.  To ensure an HDF5 file will be configured for a specific camera, you can set active camera by calling [MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice) prior to calling MMI_OpenH5file.

Incorrect results will likely occur if you stream images into an HDF5 file from a camera or configuration *other* than that which was active when the file was opened.  Be sure to use [MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice) and [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file) in tandem to keep the active camera and active HDF5 file in step with one another.

Although several HDF5 files and groups (see below) may be open simultaneously, only one file and one group may be active (selected) at a time.

Recall too that Windows protects the contents of certain folders (ex. c:\Program Files and c:\Windows) and generally prevents apps from creating or modifying files in those folders or their sub-folders.  Consequently MMI_OpenH5file will likely fail if you attempt to create an HDF5 file within any of the Windows-protected folders.  To avoid such difficulties, you should consider calling Igor's [SpecialDirPath](/igorpro/commands/specialdirpath.md) function, which can return the path to several writable folders.

#### *See Also* {#interface-methods-see-also}

[MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice), [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file), [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file), [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group), [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators), [SpecialDirPath](/igorpro/commands/specialdirpath.md)







<div className="command-signature">

### <strong>MMI_CloseH5file</strong>  /Q /Z fileID {#mmi_closeh5file}

</div>

Closes an HDF5 file opened by a previous call to [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file).

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *fileID* | The ID number which was assigned to the HDF5 file by the corresponding call to [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file).  The file ID number must be an integer with value greater than or equal to 1. |

#### *Details* {#interface-methods-details}
MMI_CloseH5file automatically closes any HDF5 groups currently open within that file.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file), [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file)







<div className="command-signature">

### <strong>MMI_SelectH5file</strong>  /Q /Z fileID {#mmi_selecth5file}

</div>

Selects an HDF5 file previously opened by a call to [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) as the currently active HDF5 file.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *fileID* | The ID number of the file to be selected.  fileID must have been previously assigned to the HDF5 file by a call to MMI_OpenH5file. |

#### *Details* {#interface-methods-details}
Although several HDF5 files and groups (see below) may be open simultaneously, only one file and one group may be active at a time.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file), [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file), [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group)







<div className="command-signature">

### <strong>MMI_OpenH5group</strong>   /Q /Z /F=<em>H5fileID</em> <em>groupID</em> [, <em>groupName</em>] {#mmi_openh5group}

</div>

Creates an HDF5 group within a previously opened HDF5 file, selects that group as the file's active group, and returns an ID number for the new group within the specified file.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/F = *H5fileID*</span> | The ID number of the HDF5 file in which the group is to be created.  This is the fileID returned by [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) operation.  Using the /F flag does not 'select' the specified HDF5 file as the active file.  It simply lets you create an HDF5 group within the specified file.  Be sure to call [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file) to select the active HDF5 file. |
| *groupID* | A real (non-complex) numeric variable which will receive the ID number assigned to the newly created HDF5 group.  The group ID number will be an integer greater than or equal to 1. |
| *groupName* | An optional string specifying the unique name to be assigned to the newly created group.  If no groupName is specified, the operation will create and assign the new group a unique name, as described below.  Although groupName must be unique within the specified file, the same group name may be used in separate files. |

#### *Details* {#interface-methods-details}
Although several HDF5 groups and files may be open simultaneously, only one file and one group may be active at a time.

Once an HDF5 group is closed, it cannot be re-opened.

Names created by the operation are based on a Windows UUID created when the operation executes.  Created names will have the form "Group_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx".

Note that while the groupID returned by MMI_OpenH5group is unique within its HDF5 file, it is not guaranteed to be unique across all open HDF5 files.  That is, several open HDF5 files may each contain groups with identical groupIDs.  To uniquely specify a group among several open HDF5 files, be sure to use both the fileID and the groupID.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file), [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file), [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group), [MMI_SelectH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5group), [https://en.wikipedia.org/wiki/Universally_unique_identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier)







<div className="command-signature">

### <strong>MMI_CloseH5group</strong>  /Q /Z /F=<em>H5fileID</em> <em>groupID</em> {#mmi_closeh5group}

</div>

Closes an HDF5 group previously created by a call to [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group).

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/F = *H5fileID*</span> | The ID number of the HDF5 file containing the group to be closed.  This is the fileID returned by [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) operation. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *groupID* | The ID number previously assigned to the HDF5 group.  This is the groupID returned by [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group). |

#### *Details* {#interface-methods-details}
MMI cannot currently re-open an HDF5 group for writing, once it is closed.  An HDF5 group may later be re-opened for reading data.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group), [MMI_SelectH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5group), [HDF5 in Igor Pro](/igorpro/data/igor-hdf5-guide.md)







<div className="command-signature">

### <strong>MMI_SelectH5group</strong>  /Q /Z /F=<em>H5fileID</em> <em>groupID</em> {#mmi_selecth5group}

</div>

Selects an HDF5 group (and optionally an HDF5 file), as the currently active group (and file).  The file and group must have been previously opened by calls to [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) and [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group).

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/F = *H5fileID*</span> | The ID number of the HDF5 file containing the group to be selected.  This is the fileID returned by [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file) operation.  If the /F flag is omitted, the operation attempts to select the specified group within the currently active HDF5 file. |

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| *groupID* | The ID number of the group to be selected.  groupID must have been previously assigned by an earlier call to MMI_OpenH5group. |

#### *Details* {#interface-methods-details}
Because multiple HDF5 files and groups may be open simultaneously, callers should use caution to ensure they are selecting an existing and appropriate group and file.

#### *See Also* {#interface-methods-see-also}

[MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group), [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group), [MMI_SelectH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_selecth5file)







<div className="command-signature">

### <strong>MMI_GetEstMaxFrameCount</strong>  ( ) {#mmi_getestmaxframecount}

</div>

Returns an estimate of the maximum number of images from the currently active camera and configuration that can be stored in a wave, given the physical memory available on this PC.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Returns* {#interface-methods-returns}

|  |  |
| --- | --- |
|  | Returns the [floor](/igorpro/commands/floor.md) of the ratio of the size of available physical memory to the size of each frame acquired by the current selected camera, as stored in a wave. |

#### *Details* {#interface-methods-details}
To obtain a valid result, a camera device must have been previously loaded, initialized, and selected.

#### *Example* {#interface-methods-example}

```igor
MMC_LoadDevice "myDemoCam", "DemoCamera", "DCam"
MMC_InitializeDevice "myDemoCam"
MMC_S
print MMI_GetEstMaxFrameCount()
```

```
  9520      // estimated max. number of frames (from the demoCamera) that will fit in a wave
            // N.B. Your result will likely differ
```

```igor
MMC_LoadDevice "myWebCam", "OpenCVgrabber", "OpenCVgrabber"
MMC_InitializeDevice "myWebCam"
MMC_SetCameraDevice "myWebCam"
print MMI_GetEstMaxFrameCount()
```

```
  2703      // est max. number of frames (from the webCam) that will fit in a wave
            // N.B. Your result will likely differ
```

#### *See Also* {#interface-methods-see-also}

[floor](/igorpro/commands/floor.md), [MMC_SetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setcameradevice), [MMC_GetCameraDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getcameradevice)







<div className="command-signature">

### <strong>MMI_GetDisabledDevices</strong>  ( ) {#mmi_getdisableddevices}

</div>

Returns a string containing the current list of devices marked as disabled for use by MMI.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
|  | (None) |

#### *Returns* {#interface-methods-returns}


|  |  |
| --- | --- |
|  | Returns an Igor string containing a semicolon delimited list of case-sensitive device-specifiers.  Each device-specifier is composed of one module-name and one device-name, themselves separated by a colon (":"), ex. "TwainCamera:TwainCam;pizza:pepperoni". |

#### *Details* {#interface-methods-details}
Attempting to load or initialize a device, i.e. calling MMC_LoadDevice or MMC_InitializeDevice may, under some circumstances, lead to errors that can cause MMI and Igor to crash.  For example, attempting to load a TWAIN camera on a PC that has only partial, or obsolete support for TWAIN devices, can crash MMI and Igor.

Users can prevent such crashes by 'disabling' the offending devices: adding them to a list of devices that MMI prevents from being used.  MMI stores its list of disabled devices in Igor's XOP preferences, making it unique to each PC, but remembered from session to session.

#### *See Also* {#interface-methods-see-also}

[MMI_SetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setdisableddevices), [MMI_AddDisabledDevice](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_adddisableddevice), [MMI_IsDeviceDisabled](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_isdevicedisabled)







<div className="command-signature">

### <strong>MMI_SetDisabledDevices</strong>  /Q /Z /D deviceList {#mmi_setdisableddevices}

</div>

Defines the list of Micro-Manager devices to be marked as disabled for use by MMI.  Disabling a device prevents MMI from loading or initializing that device.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/D</span> | 'Default' mode instructs MMI to restore its default list of disabled devices.  The deviceList keyword is ignored when the /D flag is specified. |

#### *Keywords* {#keywords}

|  |  |
| --- | --- |
| deviceList | A semicolon delimited list of case-sensitive device-specifiers, each of which composed of one module-name and one device-name, separated by a colon, ex. "TwainCamera:TwainCam;pizza:pepperoni". |

#### *Details* {#interface-methods-details}
MMI validates that each device-specifier in the list meets the format of \<module-name\>:\<device-name\> but makes no attempt to validate individual module-names or device-names.  Each time the list of disabled devices changes, MMI unloads any previously loaded devices whose module- and device-name appear in the updated list.

Calling MMI_SetDisabledDevices overrides any previously defined list of disabled devices.  Passing an empty list to MMI_SetDisabledDevices clears any previously defined list of disabled devices.

#### *See Also* {#interface-methods-see-also}

[MMI_GetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdisableddevices), [MMI_AddDisabledDevice](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_adddisableddevice), [MMI_IsDeviceDisabled](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_isdevicedisabled)







<div className="command-signature">

### <strong>MMI_AddDisabledDevice</strong>  /Q /Z deviceList {#mmi_adddisableddevice}

</div>

Appends one or more devices to the list of Micro-Manager devices marked as disabled for use by MMI.  Disabling a device prevents MMI from loading or initializing that device.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

#### *Keywords* {#interface-methods-keywords}

|  |  |
| --- | --- |
| deviceList | A semicolon delimited list of case-sensitive device-specifiers, each of which composed of one module-name and one device-name, separated by a colon, ex. "TwainCamera:TwainCam". |

#### *Details* {#interface-methods-details}
MMI validates that each device-specifier in the list meets the format of \<module-name\>:\<device-name\> but makes no attempt to validate individual module-names or device-names.  Each time the list of disabled devices changes, MMI unloads any previously loaded devices whose module- and device-name appear in the updated list.

#### *See Also* {#interface-methods-see-also}

[MMI_GetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdisableddevices), [MMI_SetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setdisableddevices), [MMI_IsDeviceDisabled](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_isdevicedisabled)







<div className="command-signature">

### <strong>MMI_IsDeviceDisabled</strong>  (<em>device</em>-<em>specifier</em>) {#mmi_isdevicedisabled}

</div>

Reports whether the specified device is in the list marked as disabled for use by MMI.

#### *Parameters* {#interface-methods-parameters}

|  |  |
| --- | --- |
| device-specifier | A string containing the case-dependent specifier (module-name and device-name) for the device to be sought within the currently active list of disabled devices.  The device-specifier is composed of one module-name and one device-name, themselves separated by a colon (":"), ex. "TwainCamera:TwainCam". |

#### *Returns* {#interface-methods-returns}

Returns a numeric value: 0 if the specified device is not in the list of disabled devices, and 1 if the specified device is in the list.

#### *Details* {#interface-methods-details}
Attempting to load or initialize a device, i.e. calling MMC_LoadDevice or MMC_InitializeDevice may, under some circumstances, lead to errors that can cause MMI and Igor to crash.  For example, attempting to load a TWAIN camera on a PC that has only partial, or obsolete support for TWAIN devices, can crash MMI and Igor.

Users can prevent such crashes by 'disabling' the offending devices: adding them to a list of devices that MMI prevents from being used.  MMI stores its list of disabled devices in Igor's XOP preferences, making it unique to each PC, but remembered from session to session.

#### *See Also* {#interface-methods-see-also}

[MMI_GetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdisableddevices), [MMI_SetDisabledDevices](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setdisableddevices), [MMI_AddDisabledDevice](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_adddisableddevice)







<div className="command-signature">

### <strong>MMI_GetCamera</strong>  /Q /Z /DEF /DRVR /L=<em>cameraLabel</em> /W=<em>winName</em> <em>keyword</em>[=<em>value</em>] {#mmi_getcamera}

</div>

MMI_GetCamera uses Micro-Manager to provide information about cameras connected to your computer, their current settings, and the options they support, providing a substitute for the GetCamera operation that was part of Igor Pro since v.7.

MMI_GetCamera generally responds by writing a string containing a keyword/value pair to a variable called S_info in the current data folder.  If a keyword is not supported, the value reported is -1.

Except when using the availablecameras keyword, calls to MMI_GetCamera must specify the camera to be accessed by using one of the /DEF, /L, or /W flags.

MMI_GetCamera accepts the new 'properties' keyword to provide a list of the properties exposed by the chosen camera.  (See the properties keyword, and the Details section.)

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/DEF</span> | Applies the MMI_GetCamera operation to the computer's default camera. Note that the default camera does not have to be represented by an open viewfinder window but it must be connected to the computer. |
| <span class="table-cell-nowrap">/DRVR</span> | Valid only with the *availablecameras* keyword, the /DRVR flag instructs MMI to list all cameras whose device-adapters can be loaded even if the corresponding hardware is not connected to the computer.  Using the /DRVR flag generates a longer list of available cameras, but that list will likely include many that are not connected.  The /DRVR flag is also available for use with the /S flag in [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera). |
| <span class="table-cell-nowrap">/L = *cameraLabel*</span> | Specifies the chosen camera by a string containing the camera's case-sensitive Micro-Manager device-label. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the chosen camera from the named graph window. *winName* is the name of the   graph window showing the camera's images, e.g., graph0, not the name/description of the camera.  MMI extracts the Micro-Manager label for the camera from the Notes of the named window. |
|  | If the graph window is embedded within some other graph, *winName* takes the form \<parent graph name\>#\<image graph name\>, e.g. summary0#graph0. |

#### *Keywords* {#interface-methods-keywords}

|  |  |
| --- | --- |
| aperture | The keyword 'aperture' is not supported. |
| availableCameras |  |
|  | Returns the description of each discoverable camera in the semicolon-separated string S_CameraNames.  The availableCameras keyword is different from other keywords in that it does not require you specify a camera via /W or /DEF flags and it can't be used in combination with any other keyword.  If you omit the /Q flag, the operation also prints the list of available cameras to the history area of the command window. |
|  | MMI constructs the list of available cameras by attempting, one at a time, to load each device of type 'Camera' that is supported by each device-adapter.  When a camera-device loads successfully,  MMI checks its available properties, searching for a property named 'Camera'.  If a 'Camera' property is found, MMI enumerates each possible value for the 'Camera' property, adding each value to the list of available cameras. |
|  | If the /DRVR flag is asserted, MMI adds each discovered adapter-device pair to the list, even if no 'Camera' property is discovered. |
|  | Because the process of building the list of cameras is tied to Micro-Manager and its available device-adapters, the set of cameras identified, and their order in the list will almost certainly be different than the list of cameras returned by Igor's previous GetCamera operation. |
|  | Every camera listed in S_CameraNames contains the two identifiers "Adapter:" and "Name:", with a '#' character as a separating delimiter.  Those identifiers contain the names of each camera's Micro-Manager module (device-adapter) and device-name, e.g. |
|  | <code class="igor">Adapter:DemoCamera#Name:DCam;</code> |
|  | Some cameras (notably those implemented by the adapter OpenCVgrabber) also include the additional identifier "Property:" which contains the value of the 'Camera' property corresponding to a physical device, e.g. |
|  | <code class="igor">Adapter:OpenCVgrabber#Name:OpenCVgrabber#Property:Live Streamer CAM 313;</code> |
| colorFilter | The keyword 'colorFilter' is not supported. |
| contrast | The keyword 'contrast' is not supported. |
| customFocusPoint |  |
|  | The keyword 'customFocusPoint' is not supported. |
| denoisingLevel | The keyword 'denoisingLevel' is not supported. |
| description | Returns the description of the current camera. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "Description:\<value\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| deviceName | Returns the device name for the specified camera. This is usually a hex number. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "DeviceName:\<value\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| digitalZoom | The keyword 'digitalZoom' is not supported. |
| exposureCompensation |  |
|  | The keyword 'exposureCompensation' is not supported. |
| focusMode | The keyword 'focusMode' is not supported. |
| <span class="table-cell-nowrap">isColorFilterSupported = *cf*</span> |  |
|  | The keyword 'isColorFilterSupported' is not supported. |
| <span class="table-cell-nowrap">isFlashModeSupported = *fm*</span> |  |
|  | The keyword 'isFlashModeSupported' is not supported. |
| isFlashReady | The keyword 'isFlashReady' is not supported. |
| <span class="table-cell-nowrap">isFocusModeSupported = *fm*</span> |  |
|  | The keyword 'isFocusModeSupported' is not supported. |
| <span class="table-cell-nowrap">isFocusPointModeSupported = *fpm*</span> |  |
|  | The keyword 'isFocusPointModeSupported' is not supported. |
| isIPAvailable | The keyword 'isIPAvailable' is not supported. |
| <span class="table-cell-nowrap">isMeteringModeSupported = *mm*</span> |  |
|  | The keyword 'isMeteringModeSupported' is not supported. |
| <span class="table-cell-nowrap">isWBModeSupported = *wbm*</span> |  |
|  | The keyword 'isWBModeSupported' is not supported. |
| manualWhiteBalance |  |
|  | The keyword 'manualWhiteBalance' is not supported. |
| maximumDigitalZoom |  |
|  | The keyword 'maximumDigitalZoom' is not supported. |
| maximumOpticalZoom |  |
|  | The keyword 'maximumOpticalZoom' is not supported. |
| opticalZoom | The keyword 'opticalZoom' is not supported. |
| orientation | The keyword 'orientation' is not supported. |
| position | The keyword 'position' is not supported. |
| properties | Returns a two-dimensional text wave called M_cameraProperties in the current data folder which lists the properties the camera presents to Micro-Manager.  For each property, the wave reports the property's name, current value, type (integer, string, float), the minimum and maximum acceptable values (if available), and whether each property is read-only (its value is fixed) or is read-write (its value can be changed by calling [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)). |
| saturation | The keyword 'saturation' is not supported. |
| sharpeningLevel | The keyword 'sharpeningLevel' is not supported. |
| spotMeteringPoint | The keyword 'spotMeteringPoint' is not supported. |
| supportedApertures |  |
|  | The keyword 'supportedApertures' is not supported. |
| supportedISOSensitivities |  |
|  | The keyword 'supportedISOSensitivities' is not supported. |
| supportedShutterSpeeds |  |
|  | The keyword 'supportedShutterSpeeds' is not supported. |
| shutterSpeed | Returns the current shutter speed (exposure time) in seconds. |
|  | Returns -1 if the driver does not support shutter speed control. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "shutterSpeed:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| viewfinderPixelFormats |  |
|  | The keyword 'viewfinderPixelFormats' is not supported. |
| viewfinderFrameRateRanges |  |
|  | The keyword 'viewfinderFrameRateRanges' is not supported. |
| viewfinderResolutions |  |
|  | The keyword 'viewfinderResolutions' is not supported. |
| whiteBalanceMode |  |
|  | The keyword 'whiteBalanceMode' is not supported. |

#### *Details* {#interface-methods-details}
Except for the availableCameras keyword, you must either include the /DEF flag or specify either the camera's Micro-Manager label (using the /L flag) or the name of the camera window (using the /W flag).

Most of the keywords supported by Igor's previous GetCamera operation do not correspond to features available from Micro-Manager's supported cameras.  Thus many of those older keywords, although accepted by MMI_GetCamera, are unsupported.

Unless Quiet mode is selected, MMI_GetCamera reports to the history section of Igor's Command Window each time an unsupported keyword is entered.

Like Igor's previous GetCamera operation, MMI_GetCamera accepts a broad range of options that may not be supported in practice, by either the operating system or the camera driver. Some results are undefined when the driver does not support the corresponding feature.

Each device running in Micro-Manager exposes a number of parameters (called 'properties') that can refine operation of the device.  You can change the values of many, but not all, of these properties to adjust the operation of the device.  You can use the information provided by the properties keyword, together with the [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty) operation to change the camera's properties and adjust its operation to meet your needs.

#### *Output Variables* {#output-variables}
MMI_GetCamera sets the following output variables:


|  |  |
| --- | --- |
| root:packages\:mmI:V_MMIresult | 0 if the operation succeeded or a non-zero error code. |
| root:packages\:mmI:S_MMIresult | An empty string if the operation succeeded, or an error message. |
| S_CameraNames | Set by the availableCameras keyword only to a semicolon-separated list of camera descriptions. |
| S_info | Set by all keywords except availableCameras to a keyword:value pair terminated by a semicolon. When the result for any keyword consists of multiple possible values they are separated by commas. |

#### *See Also* {#interface-methods-see-also}

[MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera), [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera), [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)





<div className="command-signature">

### <strong>MMI_ModifyCamera</strong>  /Q /Z /L=<em>labelStr</em> /TO=<em>ms</em> /CLRO=<em>colorOrder</em> /W=<em>windowName</em> <em>keyword</em>=<em>value</em> {#mmi_modifycamera}

</div>

MMI_ModifyCamera uses Micro-Manager to change the settings of the specified camera, providing a substitute for the ModifyCamera operation that was part of Igor Pro since v.7.

MMI_ModifyCamera adjusts the settings of the currently active camera or the camera specified by the /L flag.

Because Micro-Manager's interface to its cameras relies on the variable sets of properties supported by each camera, MMI_ModifyCamera cannot provide a consistent interface across all cameras.  Hence MMI_ModifyCamera does not implement many of the keywords provided by the now obsolete ModifyCamera operation.

Because of the variability in the sets of properties supported by individual cameras, MMI_ModifyCamera does not provide access to most of the properties exposed by individual cameras.

To streamline users updating old code and to minimize compilation errors, MMI_ModifyCamera accepts the same keywords as ModifyCamera.  Calling MMI_ModifyCamera with unsupported keywords will produce run-time warnings unless the /Q flag is used.

Users can modify the operation of any specific camera using the set of properties exposed by that camera.  For more about cameras and their properties, see Details below, and [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty).

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |
| <span class="table-cell-nowrap">/L = *labelStr*</span> | Specifies the chosen camera by a string containing the camera's case-sensitive Micro-Manager device-label. |
| <span class="table-cell-nowrap">/TO = *ms*</span> | *ms* is a timeout in milliseconds. The capture of an image is terminated if it takes longer than *ms* milliseconds to complete.  In the case of sequential capture, the timeout is applied to the first frame only.  If capture is terminated due to timeout, IGOR returns a "timeout while writing data" error. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGBA) in the string. |
| <span class="table-cell-nowrap">/W = *windowName*</span> | Assumes that *windowName* is the name of a graph created by a previous call to MMI_NewCamera and that the micro-manager label of the camera to be modified is contained within the notes for that window. |

#### *Keywords* {#interface-methods-keywords}

|  |  |
| --- | --- |
| cancelCapture |  |
|  | Cancels a capture in progress, if any. |
| <span class="table-cell-nowrap">capture[ = *dataFolderAndName*]</span> |  |
|  | Captures a single frame and store it in a wave. *dataFolderAndName*  is a data folder path to a wave or a simple name of a wave in the current data folder. The wave may or may not exist when you invoke capture. If it does exist, it is overwritten.  If it does not, it will be created. |
|  | If you omit =*dataFolderAndName*, ModifyCamera creates the wave with the name M_Frame in the current data folder. |
|  | The created wave is a three-layer RGB wave of type unsigned byte. |
|  | It is best to use the capture keyword without any other keywords because the order of execution of keywords is unspecified. |
|  | ModifyCamera executes the capture before returning control to Igor. The time required is hardware-dependent and sets the speed limit when capturing a sequence of frames. |
| <span class="table-cell-nowrap">customFocusPoint = {*fx*,*fy*}</span> |  |
|  | The keyword 'customFocusPoint' is not supported. |
| <span class="table-cell-nowrap">grabSequence = {*nf*,*dt*}</span> |  |
|  | The keyword 'grabSequence' is not supported. |
| grabToFunction |  |
|  | The keyword 'grabToFunction' is not supported. |
| <span class="table-cell-nowrap">grabFunctionName = *func*</span> |  |
|  | The keyword 'grabFunctionName' is not supported. |
| <span class="table-cell-nowrap">setPixelFormat = *pixelFormatStr*</span> |  |
|  | The keyword 'setPixelFormat' is not supported. |
| searchAndLock |  |
|  | The keyword 'searchAndLock' is not supported. |
| <span class="table-cell-nowrap">setAspectRatio = {*w*,*h*}</span> |  |
|  | The keyword 'setAspectRatio' is not supported. |
| setAutoAperture |  |
|  | The keyword 'setAutoAperture' is not supported. |
| setAutoISOSensitivity |  |
|  | The keyword 'setAutoISOSensitivity' is not supported. |
| setAutoShutterSpeed |  |
|  | The keyword 'setAutoShutterSpeed' is not supported. |
| <span class="table-cell-nowrap">setCaptureMode = *cm*</span> |  |
|  | The keyword 'setCaptureMode' is not supported. |
| <span class="table-cell-nowrap">setColorFilter = *cf*</span> |  |
|  | The keyword 'setColorFilter' is not supported. |
| <span class="table-cell-nowrap">setContrast = *contrast*</span> |  |
|  | The keyword 'setContrast' is not supported. |
| <span class="table-cell-nowrap">setDenoising = *dn*</span> |  |
|  | The keyword 'setDenoising' is not supported. |
| <span class="table-cell-nowrap">setExposureComp = *ec*</span> |  |
|  | The keyword 'setExposureComp' is not supported. |
| <span class="table-cell-nowrap">setExposureMode = *em*</span> |  |
|  | The keyword 'setExposureMode' is not supported. |
| <span class="table-cell-nowrap">setFlashMode = *fm*</span> |  |
|  | The keyword 'setFlashMode' is not supported. |
| <span class="table-cell-nowrap">setFocusMode = *fm*</span> |  |
|  | The keyword 'setFocusMode' is not supported. |
| <span class="table-cell-nowrap">setFocusPointMode = *fpm*</span> |  |
|  | The keyword 'setFocusPointMode' is not supported. |
| <span class="table-cell-nowrap">setFrameRate = {*min*,*max*}</span> |  |
|  | The keyword 'setFrameRate' is not supported. |
| <span class="table-cell-nowrap">setManualAperture = *fn*</span> |  |
|  | The keyword 'setManualAperture' is not supported. |
| <span class="table-cell-nowrap">setManualIsoSensitivity = *isoInt*</span> |  |
|  | The keyword 'setManualIsoSensitivity' is not supported. |
| <span class="table-cell-nowrap">setManualShutterSpeed = *ss*</span> |  |
|  | The keyword 'setManualShutterSpeed' is not supported. |
| <span class="table-cell-nowrap">setManualWB = *temp*</span> |  |
|  | The keyword 'setManualWB' is not supported. |
| <span class="table-cell-nowrap">setMeteringMode = *mm*</span> |  |
|  | The keyword 'setMeteringMode' is not supported. |
| <span class="table-cell-nowrap">setPixelFormat = *pf*</span> |  |
|  | The keyword 'setPixelFormat' is not supported. |
| <span class="table-cell-nowrap">setResolution = {*w*,*h*}</span> |  |
|  | The keyword 'setResolution' is not supported. |
| <span class="table-cell-nowrap">setSaturation = *st*</span> |  |
|  | The keyword 'setSaturation' is not supported. |
| <span class="table-cell-nowrap">setSharpening = *sr*</span> |  |
|  | The keyword 'setSharpening' is not supported. |
| <span class="table-cell-nowrap">setSpotMeteringPoint = {*x*,*y*}</span> |  |
|  | The keyword 'setSpotMeteringPoint' is not supported. |
| <span class="table-cell-nowrap">setWBMode = *wb*</span> |  |
|  | The keyword 'setWBMode' is not supported. |
| startPreview |  |
|  | Starts sequential acquisition to the currently bound sequence-wave, or into the wave used by the most recent call to [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera). |
| stopPreview |  |
|  | Stops any active sequential acquisition. |
| unlock |  |
|  | The keyword 'unlock' is not supported. |
| <span class="table-cell-nowrap">zoomTo = {*opticalZoom*, *digitalZoom*}</span> |  |
|  | The keyword 'zoomTo' is not supported. |

#### *Details* {#interface-methods-details}
Like Igor's previous ModifyCamera operation, MMI_ModifyCamera accepts a broad range of options that may not be supported in practice by either the operating system or the camera driver.

In most situations the operation will not return an error in response to an unsupported request. The only reliable way to determine if a requested setting is supported is to execute [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) with the corresponding keyword.

Most of the keywords supported by Igor's previous ModifyCamera operation do not correspond to features available from Micro-Manager's supported cameras.  Thus many of those older keywords, although accepted by MMI_ModifyCamera, are unsupported.

Each device running in Micro-Manager exposes a number of parameters (called 'properties') many of which can be adjusted to refine operation of the device.  You can use the information provided by the [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) operation with the 'properties' keyword, together with the [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty) operation to change the camera's properties and adjust its operation to meet your needs.

#### *Output Variables* {#interface-methods-output-variables}
MMI_ModifyCamera sets the following output variables:


|  |  |
| --- | --- |
| root:packages\:mmI:V_MMIresult | 0 if the operation succeeded or a non-zero error code. |
| root:packages\:mmI:S_MMIresult | An empty string if the operation succeeded, or an error message. |

#### *See Also* {#interface-methods-see-also}

[MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera), [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera), [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)





<div className="command-signature">

### <strong>MMI_NewCamera</strong>  /Q /Z /DEST=<em>dataFolderAndName</em> /DRVR /HIDE=<em>h</em> /HOST=<em>hcSpec</em> /K=<em>k</em> /L=<em>label</em> /CLRO=<em>colorOrder</em> /O /S=<em>sequence</em>  /N=<em>winName</em> /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>) {#mmi_newcamera}

</div>

MMI_NewCamera uses Micro-Manager to create a new graph window to display live video from supported cameras, providing a substitute for the NewCamera operation that was part of Igor Pro since v.7.

#### *Flags* {#interface-methods-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | 'Quiet' mode instructs MMI not to write internal messages or errors to the history area. |
| <span class="table-cell-nowrap">/Z</span> | 'Suppress' mode instructs MMI to return normally to Igor, even when an error occurs.  When the /Z flag is used, it is left to the user to check for errors, reported by non-zero values in the numeric variable V_MMIresult.  If an error occurs, an error message is written to the global string variable S_MMIresult. |

/DEST=*dataFolderAndName*


|  |  |
| --- | --- |
|  | Direct the sequence of images to a specific destination wave. *dataFolderAndName* is a data folder path to a wave or a simple name of a wave in the current data folder. The wave may or may not exist. If the destination wave does not exist, it will be created.  If the wave already exists, MMI will report an error unless the /O (overwrite) flag is also used. |
| <span class="table-cell-nowrap">/DRVR</span> | Valid only when used together with the /S flag, the /DRVR flag instructs MMI to include in its list of cameras, all those cameras whose device-adapters can be loaded, even if the corresponding hardware is not actually connected to the computer.  The /DRVR flag generates a longer list of available cameras, but will likely include many cameras that are not connected.  The /DRVR flag is also available for use with the *availablecameras* keyword in [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera). |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new camera window in the host window or subwindow specified by *hcSpec*. The host window or subwindow must be a control panel or a graph.  See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on the window naming-hierarchy required when identifying a subwindow with *hcSpec*, |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/L = *label*</span> | Specifies the Micro-Manager device-label of the camera to use.  *label* is a case-sensitive string. |
| <span class="table-cell-nowrap">/CLRO = *colorOrder*</span> | Setting the color-order flag overrides MMI's default color-ordering when moving the retrieved image to the destination wave.  The color-order flag applies only when working with multi-layer color (ex. RGB, RGBA, BGR, BGRA) images and is ignored when working with grayscale (monochrome) images.  *colorOrder* is a case-insensitive string of three or four characters where the first three characters are either "rgb" or "bgr".  MMI currently ignores any fourth letter (ex. RGBA) in the string. |
| <span class="table-cell-nowrap">/N = *name*</span> | Specifies the name to use for the created graph window, if that name is not already in use. If it is already in use, then *name*0, *name*1, etc. are tried until an unused window name is found.  If you omit /N, MMI_NewCamera uses names like Graph, Graph0, Graph1, etc.  MMI_NewCamera sets S_name to the chosen name. |
| <span class="table-cell-nowrap">/O</span> | 'Overwrite' mode instructs MMI to replace any pre-existing wave that has the same name as the destination wave. |
| <span class="table-cell-nowrap">/S = *n*</span> | Selects camera *n*  from the sequence of available cameras on the current machine. *n*  is zero-based. See also the *availableCameras* keyword for [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) . |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Sets the window location. Coordinates are in points for top-level windows. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  | 1. When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size. |
|  | 2. When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame. |

If present, MMI_NewCamera sets V_Flag to 0 if the operation succeeded or to a non-zero error code.

#### *Details* {#interface-methods-details}
If you have a single camera connected to your computer, you can generally display live video by simply executing MMI_NewCamera without any flags or keywords.

You can control the resulting graph window like other Igor target windows, using MoveWindow, SetWindow, etc.

If you have more than one camera connected to your computer, you can specify which camera to acquire from by using the /L flag with the camera's (pre-assigned) Micro-Manager device label (see [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice)), or by using the /S flag and the camera's zero-based sequence number within the list of available cameras.  (See [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) and the *availableCameras* keyword.)

Igor saves the created graph windows with the experiment and opens them in live mode if it finds a matching camera when you re-open the experiment. If you do not have a matching camera, Igor still displays the camera window although with a missing camera indicator.

By default each call to MMI_NewCamera creates a uniquely named wave to hold the acquired images.  To prevent inadvertent changes to this wave, MMI locks any waves it creates before acquisition begins.  The wave remains locked until the corresponding graph window is killed, the user halts the camera (ex. [MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera) stoppreview), or calls [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave) or [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset).

#### *Output Variables* {#interface-methods-output-variables}
MMI_NewCamera sets the following output variables:


|  |  |
| --- | --- |
| root:Packages\:mmI:V_MMIresult | 0 if the operation succeeded or a non-zero error code. |
| root:Packages\:mmI:S_MMIresult | An empty string if the operation succeeded, or an error message. |
| S_Name | The name of the new camera window. |

#### *See Also* {#interface-methods-see-also}

[MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera), [MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera), [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave), [MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset), [Working with Color Images](/igorpro/extensions/data-acquisition/mmi/installing-micro-manager.md#working-with-color-images)





<div className="command-signature">

### <strong>MMI_GetXOPversion</strong>  ( ) {#mmi_getxopversion}

</div>

Returns an Igor string containing the version number of the MMI XOP.  For example, typing the following on Igor's command line

```igor
print MMI_GetXOPversion()
```

evokes the response

```
MMI.xop v.1.1.0.19
```

#### *See Also* {#interface-methods-see-also}

[MMC_GetVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getversioninfo), [MMC_GetAPIVersionInfo](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getapiversioninfo)