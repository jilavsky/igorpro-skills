---
description: "Micro-Manager provides interfaces for a wide array of hardware. These interfaces, called 'device adapters' are written by different people and companies, and…"
slug: /extensions/data-acquisition/mmi/getting-started-with-mmi
---

# Getting Started with MMI {#getting-started-with-mmi}

Micro-Manager provides interfaces for a wide array of hardware.  These interfaces, called 'device adapters' are written by different people and companies, and each may support several different types of device (ex. one or more cameras, one or more light sources, filter wheels, etc.).  A list of device adapters and an introduction to using them is available at [https://micro-manager.org/Device_Support](https://micro-manager.org/Device_Support).  Under Windows, Micro-Manager's device-adapters are implemented as dynamic link libraries (.dll) files with names that match the pattern:

```
mmgr_dal_<*root-name*>.dll
```

For example:

```
mmgr_dal_SutterLambda.dll
mmgr_dal_OpenCVgrabber.dll
```

**Notes**:

1. MMI is currently limited to using device-adapters whose files are in the root of the Micro-Manager directory tree (the directory identified by the MM_BIN environment variable).


2. Micro-Manager's device-adapters are not replacements for the Windows 'device drivers' that are often required for scientific devices.  In fact, Micro-Manager's device-adapters generally depend on those device-drivers.  Correctly installing a device's hardware and device-drivers is a prerequisite for working with the device in Micro-Manager.  Before attempting to work with a new device from Micro-Manager or Igor, you should check the instructions provided by the device's manufacturer and verify that the hardware and any needed device drivers are installed and working correctly.


3. Each type of device supported by a device adapter is identified by a unique *name* assigned by the author of the device adapter.  As the user, you must assign a unique *label* to each instance of each device.  Once you assign a label to one instance of a device, you then use that label in all subsequent commands for that instance.

	The first steps in using a piece of hardware are to 1) load the appropriate device-adapter, 2) create an instance of the device of interest, and 3) assign that instance a unique label.  The operation [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice) performs these steps, taking as arguments the label you wish to assign that instance, the root name of its associated device adapter, and the name of the type of device you want to load.

	For example, this call to MMC_LoadDevice loads an instance of the demonstration camera named 'DCam', from the device adapter named 'mmgr_dal_DemoCamera.dll', and assigns that instance the label:

	```igor
	// Usage:
	// 		MMC_LoadDevice <device Label>, <root of device adapter>, <name of device-type>
	MMC_LoadDevice "myDemoCam", "DemoCamera", "DCam"
	```


	A loaded device can later be released by calling [MMC_UnloadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_unloaddevice).

	After you load a device, but before you attempt to use it, you must call [MMC_InitializeDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializedevice) to initialize its hardware and interface, e.g.

	```igor
	// Usage:
	//		MMC_InitializeDevice <device Label>
	MMC_InitializeDevice "myDemoCam"
	```

## First Light {#first-light}

After you initialize the device, you assign it to its role, identifying the device by its label

```igor
// Usage:
//		MMC_SetCameraDevice <device label>
MMC_SetCameraDevice "myDemoCam"
```

At this point, Micro-Manager's demonstration camera is ready to use.  The next steps are 1) prepare a wave to receive its images, and 2) instruct MMI to use that wave when snapping images.

```igor
make myImageWave              // Create the numeric wave
MMI_BindImageWave myImageWave // Tell MMI this wave is to receive snapshot data
                              // Note: MMI will redimension the wave
                              // to hold a single frame from the camera
```

Once a wave is bound, calling [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage) will take a picture and transfer the acquired image to the bound Igor wave.  With both the camera and the recipient wave ready, you can now snap a picture

```igor
MMC_SnapImage // if an image-wave is already bound,
              // this operation also writes the image to the wave
```

and tell Igor to display the image

```igor
NewImage myImageWave
```

<img src="MD_images/MMI Help/First_Light_0.png" width="100%"/>

That's it.  With 7 instructions (listed below), Igor can instruct Micro-Manager to snap an image from a supported camera, load the image into a wave, and display the wave.

```igor
MMC_LoadDevice "myDemoCam", "DemoCamera", "DCam"
MMC_InitializeDevice "myDemoCam"
MMC_SetCameraDevice "myDemoCam"
make myImageWave
MMI_BindImageWave myImageWave
MMC_SnapImage
NewImage myImageWave
```

When the bound wave is no longer needed for snapping images, you should release it by calling [MMI_ReleaseImageWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releaseimagewave).

If you have a webcam connected to your computer, you will likely be able to acquire images from it by using the device-adapter called 'OpenCVgrabber.'  The corresponding call to [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice) would be something like

```igor
MMC_LoadDevice "myWebCam", "OpenCVgrabber", "OpenCVgrabber"
```

The remaining 6 steps would follow the example above, with "myWebCam" replacing "myDemoCam".

## Streaming Images {#streaming-images}

In addition to snapping individual images, both Micro-Manager and MMI support 'image-streaming' -- the continuous acquisition, display, and (optional) storage of images.  Note Micro-Manager generally uses the term 'sequential' acquisition to mean the same thing as streaming acquisition.  To stream images from a camera, the camera-device must be loaded, initialized, and set into its role as camera, just as for snapping images (above).

```igor
MMC_LoadDevice "myWebCam", "OpenCVgrabber", "OpenCVgrabber"
MMC_InitializeDevice "myWebCam"
MMC_SetCameraDevice "myWebCam"
```

As above, create a wave to receive the incoming stream of images and call [MMI_BindSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_bindsequencewave) to inform MMI that it should use this wave for its image stream.  (You can bind the same wave for both single snapshots and image-streaming.)

```igor
make mySequenceWave
MMI_BindSequenceWave mySequenceWave
```

Display the wave in an Igor image-window

```igor
NewImage mySequenceWave
```

and call [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition) to start streaming images to the wave

```igor
MMC_StartSequenceAcquisition
```

When things are done, call [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition) to halt the sequence (stream)

```igor
MMC_StopSequenceAcquisition
```

Thus with 8 Igor statements you can initialize, start, and stop continuous image-streaming into a wave.  When the bound Igor wave is no longer needed for streaming, you should release it by calling [MMI_ReleaseSequenceWave](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_releasesequencewave).

## Saving Images and Streams {#saving-images-and-streams}

Individually snapped images can be stored directly from Igor, either from the command line or by opening the 'Save Waves ... ' submenu under Igor's Data menu.

MMI provides an additional mechanism to save an incoming stream of images directly into a HDF5 file during acquisition.  After they are properly closed at the end of acquisition, such HDF5 files can then be opened and loaded back into Igor for post-acquisition analysis.  For background on HDF5 files, see [https://www.hdfgroup.org/solutions/hdf5/](https://www.hdfgroup.org/solutions/hdf5/).

To save an incoming stream of images to an HDF5 file, first be sure to configure a camera and MMI to acquire an image-stream, as described in [Streaming Images](#streaming-images), above.  Call [MMI_OpenH5stream](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5stream), instructing MMI to prepare its 'HDF5 stream handler' to manage the HDF5 file and to route images to the file as they arrive:

```igor
MMI_OpenH5stream // create the handler
```

Call [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file), instructing the stream-handler to create the HDF5 file to receive the images:

```igor
variable V_myH5fileID // remembers the ID of the file
MMI_OpenH5file V_myH5fileID, "C:\\Users\\Igor\\Desktop\\webcam_stream.h5"
```

If you use Windows path notation, be sure to use 'doubled' backslash characters to separate names within the path.  Because of Igor's long association with MacOS you can also use Macintosh HFS path notation, where colons (':') separate names in the path.  For more details, see [MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file).

Call [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group) to instruct the stream-handler to create an HDF5 group within the file to receive the images:

```igor
variable V_myH5groupID                      // to remember the ID of the group
MMI_OpenH5group V_myH5groupID, "firstGroup" // group name is optional
```

Once you have launched the stream-handler and opened a file and group, you can call [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition) and [MMC_StopSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_stopsequenceacquisition) to start & stop acquisition of the stream.  MMI will (to the best of its ability) append each incoming image as a separate Dataset in the active group of the active file.

As soon as acquisition to the group is complete, you should call [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group) to close the group and reduce risk of inadvertent corruption.

```igor
MMI_CloseH5group V_myH5groupID
```

At this point the previous group has been closed, but you may continue writing to the file if you create a new group with its own unique name:

```igor
MMI_OpenH5group V_myH5groupID, "secondGroup"
```

This second group too should be closed when its acquisition completes:

```igor
MMI_CloseH5group V_myH5groupID
```

When all acquisition to the file is done, you should similarly close the file:

```igor
MMI_CloseH5file V_myH5fileID
```

At this point, each group in the named HDF5 file holds an array of Datasets, each containing one of the streamed images.  The HDF5 Attributes of each group contain the property-settings for the camera (at the time the group was opened), and the Attributes of each Dataset contain the meta-data Micro-Manager assigned to each image.  You can open any or all of the images into Igor waves, using either Igor's command line functions, or the HDF5 Browser, available in the 'Load Waves' submenu of Igor's Data menu.

This Igor function illustrates the process: from initializing the camera to preparing the stream and HDF5 components, through acquiring the stream and closing the HDF5 components.  To help clarify the sequence of operations, this sample code performs no error checking.  We recommend you include error checking in your code.

```igor
Function MMI_HDF5demo(variable numFrames, string fileName)
    variable v_h5FileID, v_h5groupID
    MMI_Reset // clean start for this example

    // Prepare the camera
    MMC_LoadDevice "myWebCam", "OpenCVgrabber", "OpenCVgrabber"
    MMC_Initializedevice "myWebCam"
    MMC_SetCameraDevice "myWebCam"

    // prepare the streaming wave
    make /O m_img
    MMI_BindSequenceWave m_img
    newimage m_img // this optional step is not required for writing to HDF5

    // Prepare for HDF5 output
    MMI_Openh5Stream
    MMI_Openh5File /o v_h5fileID, fileName
    MMI_OpenH5Group v_h5GroupID, "group1"

    // start the acquisition
    mmc_StartSequenceAcquisition /Q /N=(numFrames)

    // wait for acquisition to finish
    do
        sleep /t 1
    while (MMC_isSequenceRunning())

    // Close HDF5 machinery
    mmi_CloseH5group v_H5groupID
    mmi_CloseH5file v_H5fileID
    mmi_CloseH5stream

    mmi_ReleaseSequenceWave
End
```

### *See Also* {#see-also}

[MMI_OpenH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5file), [MMI_CloseH5file](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5file), [MMI_OpenH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_openh5group), [MMI_CloseH5group](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_closeh5group), [HDF5 in Igor Pro](/igorpro/data/igor-hdf5-guide.md)

## Next Steps {#next-steps}

Every device in Micro-Manager has an associated list of 'properties' that describe and adjust the device's operation.  You can change (or set) the values of some properties.  Such properties are said to be writable or 'read-write'.  Other properties cannot be changed -- you can only read (or get) their values -- they are said to be 'read-only'.

To read or write any of a device's properties, the device must first be loaded using [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice) and initialized using [MMC_InitializeDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_initializedevice).  After those steps are taken, you can call [MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist) to get a two-dimensional Igor text wave containing a list of the device's properties: their names, descriptions, values, limits, and data types.  You can 'get' the current value of any single property using the functions [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric) and [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring).  You can 'set' the value of any 'read-write' property using the operation [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty).

### *See Also* {#next-steps-see-also}

[MMI_GetDevicePropertyList](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdevicepropertylist), [MMC_GetPropertyNumeric](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertynumeric), [MMC_GetPropertyString](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getpropertystring), [MMC_SetProperty](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_setproperty)