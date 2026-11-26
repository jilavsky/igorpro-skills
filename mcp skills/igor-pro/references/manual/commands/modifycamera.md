---
description: "The ModifyCamera operation is used to change the settings of the named camera."
slug: /commands/modifycamera
---

<div className="command-signature">

## <strong>ModifyCamera</strong>  /W=<em>winName</em>  [ /Z ]  <em>keyword</em>=<em>value</em> {#modifycamera}

</div>

The ModifyCamera operation is used to change the settings of the named camera.

You must specify the camera window of interest using the /W flag.

:::warning
ModifyCamera was added in Igor Pro 7.00, and deprecated in Igor Pro 10.00.
Use [MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera) instead.
:::

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the camera window to target. Use the name of the camera window, e.g., camera0, not the name/description of the camera. |
|  | If the camera window is embedded in a graph the name would have the form e.g., Graph0#CM0. |
| <span class="table-cell-nowrap">/TO = *ms*</span> | *ms* is a timeout in milliseconds. The capture of an image is terminated if it takes longer than *ms* milliseconds to complete. |
|  | In the case of sequential capture, the timeout is applied to the first frame only. |
|  | If capture is terminated due to timeout, IGOR returns a "timeout while writing data" error. |
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. Sets V_Flag to zero or to a non-zero error code. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| cancelCapture | Cancels a capture in progress, if any. |
| <span class="table-cell-nowrap">capture[ = *dataFolderAndName*]</span> |  |
|  | Captures a single frame and store it in a wave. |
|  | *dataFolderAndName* is a data folder path to a wave or a simple name of a wave in the current data folder. The wave may or may not exist when you invoke capture. If it does exist, it is overwritten. |
|  | If you omit =*dataFolderAndName*, ModifyCamera creates the wave with the name M_Frame in the current data folder. |
|  | The created wave is a three-layer RGB wave of type unsigned byte. |
|  | It is best to use the capture keyword without any other keywords because the order of execution of keywords is unspecified. |
|  | ModifyCamera executes the capture before returning control to Igor. The time required is hardware-dependent and sets the speed limit when capturing a sequence of frames. |
| <span class="table-cell-nowrap">customFocusPoint = {*fx*,*fy*}</span> |  |
|  | Specifies a custom focus point where fx and fy are in the range [0,1] in relative frame coordinates measured from the top-left corner of the frame. You must invoke setFocusPointMode before other keywords to set a custom focus point. |
| <span class="table-cell-nowrap">grabSequence = {*nf* ,*dt* }</span> | Grabs a sequence of *nf* frames every *dt* milliseconds and stores the frames in the 4D wave M_FrameSequence in the current data folder. |
|  | *nf* and *dt* are integers greater than or equal to 1. |
|  | Time resolution is on the order of 1 millisecond and may be further degraded by hardware limitations. |
| grabToFunction | Starts a continuous loop of grabbing camera frames and passing them to the user function specified by the grabFunctionName keyword. The loop is terminated when the user function returns a negative number or a timeout occurs. For details, see ***GrabToFunction Details*** below. |
| <span class="table-cell-nowrap">grabFunctionName = *func*</span> |  |
|  | Sets the user function that is called continuously when you execute the grabToFunction keyword. For details, see ***GrabToFunction Details*** below. |
| <span class="table-cell-nowrap">setPixelFormat = *pixelFormatStr*</span> |  |
|  | *pixelFormatStr* is a string containg one of the following: |
|  | ARGB32, ARGB32_Premultiplied, RGB32, RGB24, RGB565, RGB555, ARGB8565_Premultiplied, BGRA32, BGRA32_Premultiplied, BGR32, BGR24, BGR565, BGR555, BGRA5658_Premultiplied, AYUV444, Format_AYUV444_Premultiplied, YUV444, YUV420P, YV12, UYVY, YUYV, NV12, NV21, Format_IMC1, Format_IMC2, Format_IMC3, Format_IMC4, Format_Y8, Format_Y16, Format_Jpeg, Format_CameraRaw, Format_AdobeDng, Format_User |
|  | While the various "Premultiplied" formats are supported, they are not useful because all exports are strictly in RGB (no alpha). Also, since the capture results in an RGB wave, any pixel format choice here would potentially entail additional time-consuming conversions from the internal format to RGB. |
| searchAndLock | In stillImage capture mode, this keyword instructs the camera to search and lock the focus in preparation for a capture. |
| <span class="table-cell-nowrap">setAspectRatio = {*w*,*h*}</span> | Sets the viewing aspect ratio in pixels. |
| setAutoAperture | Tells the camera driver to determine the best aperture setting. |
| setAutoISOSensitivity | Tells the camera driver to determine the optimal ISO setting. |
| setAutoShutterSpeed | Tells the camera driver to determine the optimal shutter speed. |
| <span class="table-cell-nowrap">setCaptureMode = *cm*</span> | Sets the capture mode: |
|  |<table class="nested-table"><tbody><tr><td>cm&nbsp;=&nbsp;0:</td><td>Preview</td></tr><tr><td>cm&nbsp;=&nbsp;1:</td><td>Still image</td></tr><tr><td>cm&nbsp;=&nbsp;2:</td><td>Video capture</td></tr></tbody></table>
| <span class="table-cell-nowrap">setColorFilter = *cf*</span> | Sets the color filter that is applied to the input. Supported filters include: |
|  |<table class="nested-table"><tbody><tr><td>**Value**</td><td>**Filter**</td></tr><tr><td>0</td><td>None</td></tr><tr><td>1</td><td>Grayscale</td></tr><tr><td>2</td><td>Negative</td></tr><tr><td>3</td><td>Solarize</td></tr><tr><td>4</td><td>Sepia</td></tr><tr><td>5</td><td>Posterize</td></tr><tr><td>6</td><td>Whiteboard</td></tr><tr><td>7</td><td>Blackboard</td></tr><tr><td>8</td><td>Aqua</td></tr><tr><td>1000</td><td>Start of vendor-specific color filters</td></tr></tbody></table>
| <span class="table-cell-nowrap">setContrast = *contrast*</span> | Sets the contrast in the range [-1,1]. The default is 0. |
| <span class="table-cell-nowrap">setDenoising = *dn*</span> | Sets denoising in the range [-1,1]. The default is 0. |
| <span class="table-cell-nowrap">setExposureComp = *ec*</span> | Sets exposure compensation in ev units. |
| <span class="table-cell-nowrap">setExposureMode = *em*</span> | Sets the camera's exposure mode. The following modes are supported: |
|  |<table class="nested-table"><tbody><tr><td>**em**</td><td>**Exposure Mode**</td></tr><tr><td>0</td><td>Auto</td></tr><tr><td>1</td><td>Manual</td></tr><tr><td>2</td><td>Portrait</td></tr><tr><td>3</td><td>Night</td></tr><tr><td>4</td><td>Backlight</td></tr><tr><td>5</td><td>Spotlight</td></tr><tr><td>6</td><td>Sports</td></tr><tr><td>7</td><td>Snow</td></tr><tr><td>8</td><td>Beach</td></tr><tr><td>9</td><td>Large aperture</td></tr><tr><td>10</td><td>Small aperture</td></tr><tr><td>11</td><td>Action</td></tr><tr><td>12</td><td>Landscape</td></tr><tr><td>13</td><td>Night portrait</td></tr><tr><td>14</td><td>Theater</td></tr><tr><td>15</td><td>Sunset</td></tr><tr><td>16</td><td>Steady photo</td></tr><tr><td>17</td><td>Fireworks</td></tr><tr><td>18</td><td>Party</td></tr><tr><td>19</td><td>Candlelight</td></tr><tr><td>20</td><td>Barcode</td></tr><tr><td>1000</td><td>Start of vendor-specific exposure modes</td></tr></tbody></table>
| <span class="table-cell-nowrap">setFlashMode = *fm*</span> | Sets the operating mode of the camera's flash.  Supported flash modes are: |
|  |<table class="nested-table"><tbody><tr><td>**fm**</td><td>**Flash Mode**</td></tr><tr><td>1</td><td>Auto</td></tr><tr><td>2</td><td>Off</td></tr><tr><td>4</td><td>On</td></tr><tr><td>8</td><td>Redeye reduction</td></tr><tr><td>16</td><td>Fill</td></tr><tr><td>32</td><td>Torch</td></tr><tr><td>64</td><td>Video light</td></tr><tr><td>128</td><td>Front curtain</td></tr><tr><td>256</td><td>Rear curtain</td></tr><tr><td>512</td><td>Manual</td></tr></tbody></table>
| <span class="table-cell-nowrap">setFocusMode = *fm*</span> | Sets the camera's focus mode. Supported focus modes are: |
|  |<table class="nested-table"><tbody><tr><td>**fm**</td><td>**Focus Mode**</td></tr><tr><td>1</td><td>Manual</td></tr><tr><td>2</td><td>Hyperfocal</td></tr><tr><td>4</td><td>Infinity</td></tr><tr><td>8</td><td>Auto focus</td></tr><tr><td>16</td><td>Continuous</td></tr><tr><td>32</td><td>Macro</td></tr></tbody></table>
| <span class="table-cell-nowrap">setFocusPointMode = *fpm*</span> |  |
|  | Sets the camera's focus point mode. Supported focus point modes are: |
|  |<table class="nested-table"><tbody><tr><td>**Value**</td><td>**Focus Point Mode**</td></tr><tr><td>0</td><td>Auto</td></tr><tr><td>1</td><td>Center</td></tr><tr><td>2</td><td>Face detection</td></tr><tr><td>3</td><td>Custom point</td></tr></tbody></table>
| <span class="table-cell-nowrap">setFrameRate = {*min*,*max*}</span> |  |
|  | Sets the frame rate in the range [*min,max*]. |
| <span class="table-cell-nowrap">setManualAperture = *fn*</span> | Sets the aperture to a specific f-number. You may want to check that *fn* is in the supported range. See [GetCamera](/igorpro/commands/getcamera.md) supportedApertures. |
| <span class="table-cell-nowrap">setManualIsoSensitivity = *isoInt*</span> |  |
|  | Sets the ISO manually to *isoInt*. You may want to check that *isoInt* is in the supported list. See [GetCamera](/igorpro/commands/getcamera.md) supportedIsoSensitivities. |
| <span class="table-cell-nowrap">setManualShutterSpeed = *ss*</span> |  |
|  | Sets manual shutter speed to *ss* , in seconds. You may want to check that *ss* is within supported range. See [GetCamera](/igorpro/commands/getcamera.md) supportedShutterSpeeds. |
| <span class="table-cell-nowrap">setManualWB = *temp*</span> | Sets the manual white balance to the specified temperature in degrees Kelvin. |
| <span class="table-cell-nowrap">setMeteringMode = *mm*</span> | Sets the metering mode. Supported metering modes are: |
|  |<table class="nested-table"><tbody><tr><td>**mm**</td><td>**Metering Mode**</td></tr><tr><td>1</td><td>Matrix</td></tr><tr><td>2</td><td>Average</td></tr><tr><td>3</td><td>Spot</td></tr></tbody></table>
| <span class="table-cell-nowrap">setPixelFormat = *pf*</span> | The following pixel format values are defined: |
|  |<table class="nested-table"><tbody><tr><td>**pf**</td><td>**Pixel Format**</td></tr><tr><td>1</td><td>ARGB32</td></tr><tr><td>2</td><td>ARGB32_Premultiplied</td></tr><tr><td>3</td><td>RGB32</td></tr><tr><td>4</td><td>RGB24</td></tr><tr><td>5</td><td>RGB565</td></tr><tr><td>6</td><td>RGB555</td></tr><tr><td>7</td><td>ARGB8565_Premultiplied</td></tr><tr><td>8</td><td>BGRA32</td></tr><tr><td>9</td><td>BGRA32_Premultiplied</td></tr><tr><td>10</td><td>BGR32</td></tr><tr><td>11</td><td>BGR24</td></tr><tr><td>12</td><td>BGR565</td></tr><tr><td>13</td><td>BGR555</td></tr><tr><td>14</td><td>BGRA5658_Premultiplied</td></tr><tr><td>15</td><td>AYUV444</td></tr><tr><td>16</td><td>Format_AYUV444_Premultiplied</td></tr><tr><td>17</td><td>YUV444</td></tr><tr><td>18</td><td>YUV420P</td></tr><tr><td>19</td><td>YV12</td></tr><tr><td>20</td><td>UYVY</td></tr></tbody></table>
|  | While the various "Premultiplied" formats are supported, they are not useful because all exports are strictly in RGB (no alpha). Also, since the capture results in an RGB wave, any pixelFormat choice here would potentially entail additional time-consuming conversions from the internal format to RGB. |
| <span class="table-cell-nowrap">setResolution = {*w*,*h*}</span> | Sets the resolution to *w* (width) and *h* (height). You may want to check that you are using values supported by the driver. See [GetCamera](/igorpro/commands/getcamera.md) viewfinderResolutions. |
| <span class="table-cell-nowrap">setSaturation = *st*</span> | Sets the saturation change in the range [-1,1]. The default is 0. |
| <span class="table-cell-nowrap">setSharpening = *sr*</span> | Sets the sharpening change in the range [-1,1]. The default is 0. |
| <span class="table-cell-nowrap">setSpotMeteringPoint = {*x*,*y*}</span> |  |
|  | Sets the metering point. *x* and *y* are the horizontal and vertical fractions of the frame measured from the top-left corner and in the range [0,1]. |
| <span class="table-cell-nowrap">setWBMode = *wb*</span> | Sets the white balance mode. Supported white balance modes are: |
|  |<table class="nested-table"><tbody><tr><td>**wb**</td><td>**White Balance Mode**</td></tr><tr><td>0</td><td>Auto</td></tr><tr><td>1</td><td>Manual</td></tr><tr><td>2</td><td>Sunlight</td></tr><tr><td>3</td><td>Cloudy</td></tr><tr><td>4</td><td>Shade</td></tr><tr><td>5</td><td>Tungsten</td></tr><tr><td>6</td><td>Fluorescent</td></tr><tr><td>7</td><td>Flash</td></tr><tr><td>8</td><td>Sunset</td></tr><tr><td>1000</td><td>Start of vendor-specific white balance modes</td></tr></tbody></table>
| startPreview | Starts live video in the camera window. |
| stopPreview | Stops live video in the camera window. |
| unlock | Unlocks focus and return to focus searching. See the searchAndLock keyword. |
| <span class="table-cell-nowrap">zoomTo = {*opticalZoom*, *digitalZoom*}</span> |  |
|  | Sets the camera's optical and digital zoom values. There may be a delay before the optical zoom attains the requested value. |

### *Details* {#details}
This operation includes a broad range of keywords corresponding to options that may not be supported in practice by either the system or the specific camera driver. In most sitations the operation will not return an error in response to an unsupported request. The only reliable way to determine if a requested setting is supported is to execute [GetCamera](/igorpro/commands/getcamera.md) with the appropriate keyword.

### *GrabToFunction Details* {#grabtofunction-details}
The grabToFunction keyword starts a continuous loop of grabbing camera frames and passing them to the user function specified by the grabFunctionName keyword.

The function takes two parameters: a wave that contains the RGB image data and a counter specifying the zero-based index of the current frame.

The function must return a negative number to terminate frame grabbing or 0 to continue frame grabbing.

The function must not attempt to display, kill or modify the input wave.

To see how this works, paste these functions into your procedure window:


```igor
Function MyGrabFunction(frameWave, frameIndex)
	Wave frameWave
	Variable frameIndex		// Zero-based frame index number

	ImageThreshold/M=1/Q/P=0 frameWave
	Wave M_ImageThresh
	if (WinType("DemoGraph") == 0)
		NewImage/N=DemoGraph M_ImageThresh
	else
		DoUpdate/W=DemoGraph
	endif
	
	// Terminate after a 100 image grabs
	if (frameIndex >= 100)
		Print "Finished 100 frames"
		return -1		// Tells grabToFunction to terminate
	endif
	
	// Support termination using the escape key:
	if(GetKeyState(0) & 32)
		Print "Frame grabbing aborted by escape key"
		return -1		// Tells grabToFunction to terminate
	endif

	return 0			// Tells grabToFunction to continue
End	

Function StartFrameGrabbing()
	if (WinType("DemoCamera") == 0)
		NewCamera/N=DemoCamera
	endif
	ModifyCamera/W=DemoCamera grabFunctionName=MyGrabFunction
	Print "Starting frame grabbing"
	ModifyCamera/W=DemoCamera grabToFunction
End
```

Now execute this command line:


```igor
StartFrameGrabbing()
```

### *Output Variables* {#output-variables}
ModifyCamera sets the following output variable:


|  |  |
| --- | --- |
| V_flag | 0 if the operation succeeded or a non-zero error code. |

### *See Also* {#see-also}
[NewCamera](/igorpro/commands/newcamera.md), [GetCamera](/igorpro/commands/getcamera.md), [MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md)