---
description: "The GetCamera operation provides information about cameras connected to your computer, their current settings, and the options they support."
slug: /commands/getcamera
---

<div className="command-signature">

## <strong>GetCamera</strong>  [/DEF/Q /W=<em>winName</em> /Z ] <em>keyword</em>=<em>value</em> {#getcamera}

</div>

The GetCamera operation provides information about cameras connected to your computer, their current settings, and the options they support.

Except for the availableCameras keyword, you must either include the /DEF flag or specify the name (e.g., Camera0) of the camera window of interest using the /W flag.

GetCamera was added in Igor Pro 7.00, and deprecated in Igor Pro 10.00.

Use [MMI_GetCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getcamera) instead.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEF</span> | Applies the GetCamera operation to the computer's default camera. Note that the default camera does not have to be represented by an open viewfinder window but it must be connected to the computer. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the camera window to target. Use the name of the camera window, e.g., camera0, not the name/description of the camera. |
|  | If the camera window is embedded in a graph the name would have the form e.g., `graph0#CM0`. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode, do not print diagnostics to the history area of the command window. |
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. Sets V_Flag to zero or to a non-zero error code. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| aperture | Returns the current aperture setting or -1 if the aperture setting is not supported by the camera's driver. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "aperture:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| availableCameras | Returns the description of each available camera in the semicolon-separated string S_cameraNames. |
|  | If you omit the /Q flag, the operation prints a list of available cameras to the history area of the command window. |
|  | The availableCameras keyword is different from all others in that it does not require that you specify a camera via /W or /DEF flags and it can't be used in combination with any other keyword. |
| colorFilter | Returns the current color filter. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "colorFilter:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
|  | Supported filters include: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Filter***</td></tr><tr><td>0</td><td>None</td></tr><tr><td>1</td><td>Grayscale</td></tr><tr><td>2</td><td>Negative</td></tr><tr><td>3</td><td>Solarize</td></tr><tr><td>4</td><td>Sepia</td></tr><tr><td>5</td><td>Posterize</td></tr><tr><td>6</td><td>Whiteboard</td></tr><tr><td>7</td><td>Blackboard</td></tr><tr><td>8</td><td>Aqua</td></tr><tr><td>1000</td><td>Start of vendor-specific color filters</td></tr></tbody></table>
| contrast | Returns the contrast level in the range [-1,1]. |
|  | Return -1 if contrast control is not supported by the camera's driver. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "contrast:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| customFocusPoint | Returns the custom focus point as a pair of values (left,top) in the range [0,1] as fractions of the image measured from the top-left corner. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "customFocusPoint:(\<value\>,\<value\>)". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the text after the colon and then [sscanf](/igorpro/commands/sscanf.md) to parse the result into numeric variables. |
| denoisingLevel | Returns the denoising level in the range [-1,1]. |
|  | Return s-1 if denoising level is not supported by the camera's driver. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "denoisingLevel:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| description | Returns the description of the current camera. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "Description:\<value\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| deviceName | Returns the device name for the specified camera. This is usually a hex number. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "DeviceName:\<value\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| digitalZoom | Returns the current digital zoom level. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "digitalZoom:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| exposureCompensation | Returns the current exposure compensation. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "exposureCompensation:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| focusMode | Returns the current focus mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "focusMode:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
|  | Supported focus modes are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Focus Mode***</td></tr><tr><td>1</td><td>Manual</td></tr><tr><td>2</td><td>Hyperfocal</td></tr><tr><td>4</td><td>Infinity</td></tr><tr><td>8</td><td>Auto focus</td></tr><tr><td>16</td><td>Continuous</td></tr><tr><td>32</td><td>Macro</td></tr></tbody></table>
| <span class="table-cell-nowrap">isColorFilterSupported = *cf*</span> |  |
|  | Returns true or false for the specified color filter. |
|  | See the colorFilter keyword for supported color filter codes. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isColorFilterSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| <span class="table-cell-nowrap">isFlashModeSupported = *fm*</span> |  |
|  | Returns true or false for the specified flash mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isFlashModeSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
|  | Supported flash modes are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Flash Mode***</td></tr><tr><td>1</td><td>Auto</td></tr><tr><td>2</td><td>Off</td></tr><tr><td>4</td><td>On</td></tr><tr><td>8</td><td>Redeye reduction</td></tr><tr><td>16</td><td>Fill</td></tr><tr><td>32</td><td>Torch</td></tr><tr><td>64</td><td>Video light</td></tr><tr><td>128</td><td>Front curtain</td></tr><tr><td>256</td><td>Rear curtain</td></tr><tr><td>512</td><td>Manual</td></tr></tbody></table>
| isFlashReady | Returns the readiness state of the camera flash. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isFlashReady:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| <span class="table-cell-nowrap">isFocusModeSupported = *fm*</span> |  |
|  | Returns true or false for the specified focus mode. |
|  | See the focusMode keyword for supported focus mode codes. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isFocusModeSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| <span class="table-cell-nowrap">isFocusPointModeSupported = *fpm*</span> |  |
|  | Returns true or false for the specified focus point mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isFocusPointModeSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
|  | Supported focus point modes are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Focus Point Mode***</td></tr><tr><td>0</td><td>Auto</td></tr><tr><td>1</td><td>Center</td></tr><tr><td>2</td><td>Face detection</td></tr><tr><td>3</td><td>Custom point</td></tr></tbody></table>
| isIPAvailable | Returns the availability of the image processing. Image processing provides control over white balance, contrast, saturation, sharpening and denoising. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isIPAvailable:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
| <span class="table-cell-nowrap">isMeteringModeSupported = *mm*</span> |  |
|  | Returns true or false for the specified metering mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isMeteringModeSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
|  | Supported metering modes are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Metering Mode***</td></tr><tr><td>1</td><td>Matrix</td></tr><tr><td>2</td><td>Average</td></tr><tr><td>3</td><td>Spot</td></tr></tbody></table>
| <span class="table-cell-nowrap">isWBModeSupported = *wbm*</span> |  |
|  | Returns true or false for the specified white balance mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "isWBModeSupported:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
|  | See the whiteBalanceMode keyword for supported white balance modes. |
| manualWhiteBalance | Returns the current color temperature in degrees Kelvin. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "manualWhiteBalance:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| maximumDigitalZoom | Returns the maximum value of digital zoom. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "maximumDigitalZoom:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| maximumOpticalZoom | Returns the maximum value of optical zoom |
|  | The value is returned in the S_info output variable as a keyword/value pair: "maximumOpticalZoom:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| opticalZoom | Returns the current optical zoom level. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "opticalZoom:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| orientation | Returns the angle of the camera sensor relative to its natural orientation in steps of 90 degrees. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "orientation:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| position | Returns the position of the camera. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "position:\<value\>" where \<value\> is true or false. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the value. |
|  | Supported positions are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Position***</td></tr><tr><td>0</td><td>UnspecifiedPosition</td></tr><tr><td>1</td><td>BackFace</td></tr><tr><td>2</td><td>FrontFace</td></tr></tbody></table>
| saturation | Returns the saturation level in the range [-1,1]. |
|  | Return -1 if saturation control is not supported by the driver. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "saturation:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| sharpeningLevel | Returns the sharpening level in the range [-1,1]. |
|  | Returns -1 if the driver does not support sharperningLevel control |
|  | The value is returned in the S_info output variable as a keyword/value pair: "sharpeningLevel:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| spotMeteringPoint | Returns a pair of values (left,top) defining a spot metering point measured in fractions of the image from the top-left corner. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "spotMeteringPoint:(\<value\>,\<value\>)". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the text after the colon and then [sscanf](/igorpro/commands/sscanf.md) to parse the result into numeric variables. |
| supportedApertures | Returns a comma-separated list of floating point numbers representing supported apertures. The list will be empty if the driver does not support changing apertures. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "supportedApertures:\<list\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
| supportedISOSensitivities |  |
|  | Returns a comma-separated list of integers representing ISO values. The will be empty if the driver does not provide ISO sensitivities control. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "supportedApertures:\<list\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
| supportedShutterSpeeds |  |
|  | Returns a comma-separated list of floating point numbers representing supprted shutter speeds (in seconds). The list will be empty if the driver does not provide shutter speed control. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "supportedShutterSpeeds:\<list\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
| shutterSpeed | Returns the current shutter speed in seconds. |
|  | Returns -1 if the driver does not support shutter speed control. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "shutterSpeed:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
| viewfinderPixelFormats |  |
|  | Returns a comma-separated list of floating numbers representing supprted viewfinder pixel formats. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "viewfinderPixelFormats:\<list\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
|  | The following pixel format values are defined: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***Pixel Format***</td></tr><tr><td>1</td><td>ARGB32</td></tr><tr><td>2</td><td>ARGB32_Premultiplied</td></tr><tr><td>3</td><td>RGB32</td></tr><tr><td>4</td><td>RGB24</td></tr><tr><td>5</td><td>RGB565</td></tr><tr><td>6</td><td>RGB555</td></tr><tr><td>7</td><td>ARGB8565_Premultiplied</td></tr><tr><td>8</td><td>BGRA32</td></tr><tr><td>9</td><td>BGRA32_Premultiplied</td></tr><tr><td>10</td><td>BGR32</td></tr><tr><td>11</td><td>BGR24</td></tr><tr><td>12</td><td>BGR565</td></tr><tr><td>13</td><td>BGR555</td></tr><tr><td>14</td><td>BGRA5658_Premultiplied</td></tr><tr><td>15</td><td>AYUV444</td></tr><tr><td>16</td><td>Format_AYUV444_Premultiplied</td></tr><tr><td>17</td><td>YUV444</td></tr><tr><td>18</td><td>YUV420P</td></tr><tr><td>19</td><td>YV12</td></tr><tr><td>20</td><td>UYVY</td></tr></tbody></table>
| viewfinderFrameRateRanges |  |
|  | Returns comma-separated list of floating point pairs of form "(minFrameRate,maxFrameRate)". |
|  | The list is returned in the S_info output variable. It is not a keyword/value pair. Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
|  | See [ModifyCamera](/igorpro/commands/modifycamera.md) with the keyword setFrameRate for further information. |
| viewfinderResolutions | Returns comma-separated list of number pairs of form "(width,height)". |
|  | The value is returned in the S_info output variable as a keyword/value pair: "viewfinderResolutions:\<list\>". Use [StringByKey](/igorpro/commands/stringbykey.md) to get the list. |
| whiteBalanceMode | Returns the current white balance mode. |
|  | The value is returned in the S_info output variable as a keyword/value pair: "whiteBalanceMode:\<value\>". Use [NumberByKey](/igorpro/commands/numberbykey.md) to get the value. |
|  | Supported white balance modes are: |
|  |<table class="nested-table"><tbody><tr><td>***Value***</td><td>***White Balance Mode***</td></tr><tr><td>0</td><td>Auto</td></tr><tr><td>1</td><td>Manual</td></tr><tr><td>2</td><td>Sunlight</td></tr><tr><td>3</td><td>Cloudy</td></tr><tr><td>4</td><td>Shade</td></tr><tr><td>5</td><td>Tungsten</td></tr><tr><td>6</td><td>Fluorescent</td></tr><tr><td>7</td><td>Flash</td></tr><tr><td>8</td><td>Sunset</td></tr><tr><td>1000</td><td>Start of vendor-specific white balance modes</td></tr></tbody></table>

### *Details* {#details}
The GetCamera operation includes a broad range of options that may not be supported in practice by either the operating system or the camera driver. Some results are undefined when the driver does not support the corresponding feature.

Except for the availableCameras keyword, you must either include the /DEF flag or specify the name (e.g., Camera0) of the camera window of interest using the /W flag.

### *Output Variables* {#output-variables}
The availableCameras keyword returns a semicolon-separated list for camera descriptions in S_cameraNames.

All other keywords return their results in S_info as a string list with keyword:value pairs separated by semicolons. When the result for any keyword consists of multiple possible values they are separated by commas.

### *Output Variables* {#getcamera-output-variables}
GetCamera sets the following output variables:


|  |  |
| --- | --- |
| V_flag | 0 if the operation succeeded or a non-zero error code. |
| S_cameraNames | Set by the availableCameras keyword only to a semicolon-separated list of camera descriptions. |
| S_info | Set by all keywords except availableCameras to a keyword:value pair terminated by a semicolon. When the result for any keyword consists of multiple possible values they are separated by commas. |

### *See Also* {#see-also}
[ModifyCamera](/igorpro/commands/modifycamera.md), [NewCamera](/igorpro/commands/newcamera.md), [MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md)