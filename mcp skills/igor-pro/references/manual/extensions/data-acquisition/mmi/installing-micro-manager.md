---
description: "MMI's download and installation of Micro-Manager performs tasks (ex. creating environment variables, running the Micro-Manager installer), that require…"
slug: /extensions/data-acquisition/mmi/installing-micro-manager
---

# Installing Micro-Manager {#installing-micro-manager}

MMI's download and installation of Micro-Manager performs tasks (ex. creating environment variables, running the Micro-Manager installer), that require 'Windows Administrative Privileges.' Before executing each of those tasks, Windows will likely ask for permission to perform these tasks. To simplify the installation of Micro-Manager, we recommend you grant approval. If you do not wish to approve MMI performing these tasks, see the instructions below, under Manual Installation.

MMI uses several Windows environment variables to determine if its required version of Micro-Manager has been properly installed. It relies on a variable called `MM_BIN` to contain the path of the directory where Micro-Manager is installed, i.e. the directory where Micro-Manager's executables (.exe files) and libraries (.dll files) are installed. If `MM_BIN` is missing, MMI assumes Micro-Manager is not yet installed and looks for an environment variable called `MM_INSTALLER` to contain the path of the Micro-Manager installer.

If the variable `MM_INSTALLER` is also missing, MMI will prompt you to run [MMI_DownloadMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_downloadmm), which will, on a computer where the internet is accessible, download the required installer from the Micro-Manager website and save it on your computer. MMI then creates `MM_INSTALLER` and saves in it the path to the downloaded installer.

If `MM_BIN` is missing but `MM_INSTALLER` is present, MMI will prompt you to run [MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm), which runs the previously downloaded installer for Micro-Manager. This operation then creates `MM_BIN` and stores in it the path to the directory where Micro-Manager was installed.

Note that some Windows security software (notably Windows Defender), may attempt to protect you from running the unrecognized installer for Micro-Manager. If you choose to install Micro-Manager, you should override this protection and run the installer. In the case of Windows Defender, this means clicking the 'More info' text and then the button labeled 'Run Anyway' in the dialog that appears.

Once Micro-Manager is successfully installed, MMI's initialization code copies its required interface file, MMCoreDyn.dll into the `MM_BIN` directory, and prepends the `MM_BIN` directory to the system PATH variable.

When Micro-Manager's installation and setup are complete, MMI displays an Igor message box saying, "Successfully installed Micro-Manager - Igor interface." At this point MMI is fully installed. We recommend you read MMI's Preliminary Notes and then [Getting Started with MMI](/igorpro/extensions/data-acquisition/mmi/getting-started-with-mmi.md).

## Micro-Manager, ImageJ, and Java {#micro-manager-imagej-and-java}

A routine installation of Micro-Manager includes its Java-based imaging application, ImageJ.exe. Igor Pro and MMI are independent of both Java and ImageJ, so you may choose to keep or remove ImageJ and Micro-Manager's Java components, as you wish.

If you install Micro-Manager by calling [MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm), you can use the /RJ flag to automatically remove Micro-Manager's Java-based components during installation. If you choose to install Micro-Manager manually (see below), then you will need to manually remove the Java components if you choose.

If you do keep ImageJ and Java installed, you retain the option of running Micro-Manager through ImageJ, as you would any other Windows program. Running Micro-Manager from ImageJ completely bypasses Igor Pro and MMI, presenting you with its standard user interface. This pathway gives you the means to test Micro-Manager's control of a piece of equipment independent of Igor and MMI and can be a valuable debugging aid when developing code for Igor. You can learn more about Micro-Manager's native user-interface at [https://micro-manager.org/Micro-Manager_Project_Overview](https://micro-manager.org/Micro-Manager_Project_Overview).

### *See Also* {#see-also}

[MMI_DownloadMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_downloadmm), [MMI_InstallMM](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_installmm)

## Manually Installing Micro-Manager {#manually-installing-micro-manager}

If for any reason you prefer to install Micro-Manager for Igor yourself, rather than using MMI's built-in operations, you will need to manually perform the steps taken by both MMI_DownloadMM and MMI_InstallMM.

To manually perform the steps of the first operation, MMI_DownloadMM, you will need to use an internet-connected computer to download the proper version of Micro-Manager's installer for Windows and then copy that installer to your Igor PC (ex. by using a USB thumb-drive). The URL for the installer is currently

[https://download.micro-manager.org/nightly/2.0/Windows/MMSetup_64bit_2.0.3_20230929.exe](https://download.micro-manager.org/nightly/2.0/Windows/MMSetup_64bit_2.0.3_20230929.exe)

Once you save the Micro-Manager installer on your Igor PC, create (or revise) a Windows Environment Variable called `MM_INSTALLER`, and assign to it the complete name (path- and file-name) of the installer file, as stored on your Igor PC. Be sure to use an absolute path -- not a relative path -- and use single back-slash characters to separate directory names within the path. To make sure Igor gets the correct value of `MM_INSTALLER`, you should (re)start Igor *after* creating the environment variable.

To manually perform the steps of the second operation, MMI_InstallMM, you will need to:

1. Run the Micro-Manager installer (downloaded by MMI_DownLoadMM, or as above) to install the required version of Micro-Manager. You will need to run the installer as a Windows Administrator, so you may require help from your IT department. When installing Micro-Manager, you will need to choose and later identify the absolute path to the directory where the Micro-Manager's executable files (ex. ImageJ.exe, mmgr_dal_*.dll, etc.) are installed. Different versions of Micro-Manager can reside simultaneously on a single PC, so there is no need to remove any existing copies of Micro-Manager. Instead, it's better to assign a unique name to the directory where Micro-Manager gets installed.

2. Create (or revise) a Windows Environment variable called `MM_BIN` and assign to it the full path to the directory where this version of Micro-Manager has been installed.

3. Add the path to the Micro-Manager installation to the `PATH` Environment Variable. This is best done by adding `%MM_PATH%` to the Path variable, thus incorporating whatever directory is specified by `MM_PATH`.

4. Browse to Igor's MMI sub-directory, typically something like "C:\Program Files\WaveMetrics\Igor Pro 10 Folder\More Extensions (64-bit)\Data Acquisition\MMI" and copy the file called MMCoreDyn.dll to the directory identified by `MM_BIN`. (This may require Administrative Privileges.)

   Copy too, any files in the MMI sub-directory with names of the form mmgr_dal_*.dll from Igor's MMI sub-directory to the directory identified by `MM_BIN`, overwriting any pre-existing files with the same names.

   To make sure Igor uses the proper value of the `MM_BIN` variable, you should (re)start Igor *after* the environment variables are created, edited, and the dialogs closed.

   You can verify that the MMI XOP is properly installed and communicating with Micro-Manager by checking the return value of this MMI function:

   ```igor
   print MMI_GetXOPversion()
   ```

   You should see a response something like

   ```
   MMI64.xop v.1.1.0.17
   ```

   Then run the operation

   ```igor
   MMI_Reset
   ```

   If both MMI_GetXOPversion( ) and MMI_Reset run without reporting errors, MMI and Micro-Manager are correctly installed and running.

Finally, you should also consider whether you wish to keep or delete Micro-Manager's standard user-interface, which uses the Java-based application, ImageJ.exe. See [Micro-Manager, ImageJ, and Java](#micro-manager-imagej-and-java) for details.

### *See Also* {#manually-installing-micro-manager-see-also}

[MMI_Reset](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_reset), [MMI_GetXOPversion](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getxopversion), [Micro-Manager, ImageJ, and Java](#micro-manager-imagej-and-java)

## Preliminary Notes {#preliminary-notes}

### Case Sensitivity {#case-sensitivity}

:::warning
Although Igor Pro is generally case-*insensitive*, Micro-Manager is case-*sensitive*.  Therefore you need to correctly match the cases of strings passed to Micro-Manager.  For example, device-labels using the strings "mycamera" and "MyCamera" are not equivalent -- Micro-Manager considers them separate devices.  This case sensitivity applies to device-labels, device-names, property-names, and property-values.  If you find your calls to MMI are failing unexpectedly, be sure to carefully check the capitalization of the strings you are passing to Micro-Manager.
:::


### Naming Conventions {#naming-conventions}

The names of the MMI functions and operations that correspond to functions in the API for the CMMCore class generally start with the prefix "MMC_" followed by the name of the corresponding Micro-Manager function.  For example, the CMMCore function called loadDevice is exposed by an Igor operation called [MMC_LoadDevice](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_loaddevice).  These 'core' functions in MMI are listed below using the same descriptive categories that Micro-Manager uses to document the functions exposed by CMMCore.  You can find a list of the functions provided by Micro-Manager's CMMCore class at

[https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html](https://micro-manager.org/apidoc/MMCore/latest/class_c_m_m_core.html)

MMI also provides a number of operations & functions that control the internal operations of the interface itself.  The names of these operations and functions generally start with the prefix "MMI_".

### Output Variables & Error Handling {#output-variables-error-handling}

When first called, MMI creates an Igor data folder, called MMI, within Igor's root:packages data folder.  (You can get the path to this data folder by calling the function [MMI_GetDataFolderPath](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getdatafolderpath).)  Once the data folder is created, MMI then creates 3 global variables in that data folder:

|  |  |
| --- | --- |
|  |  |
| `root:packages\:mmI:V_MMIresult` | MMI uses this numeric variable to report the result of each operation and function.  MMI sets the variable to zero to report success, and to a non-zero error code to report failure. |
| `root:packages\:mmI:S_MMIresult` | MMI uses this string variable to log its most recent error message. |
| `root:packages\:mmI:V_MMIverbose` | MMI reads this numeric variable to determine how its functions report errors, as follows: |

```igor
V_MMIverbose = 3        // Write error messages to the history area, and
                        // return error codes to Igor.

V_MMIverbose = 2        // Do not write error messages to the history area, but
                        // do report error codes to Igor.

V_MMIverbose = 1        // Write error messages to the history area, but
                        // do not return error codes to Igor.

V_MMIverbose = 0        // Do not write error messages to the history area, and
                        // do not return error codes to Igor.
```

While the value of V_MMIverbose determines explicitly how *functions* in MMI report errors, *operations* in MMI report their errors according to the states of their /Q and /Z flags:

```igor
/Q=0 (or absent)        // Normal mode: write errors to the history area
/Q=1                    // Quiet mode: do not write errors to the history area

/Z=0 (or absent)        // Normal mode: return error codes to Igor
/Z=1                    // Suppress mode: do not return error codes to Igor
```

MMI records errors in V_MMIresult and S_MMIresult regardless of the state of V_MMIverbose or an operation's /Q and /Z flags.

### Performance Considerations {#performance-considerations}

To optimize performance while acquiring data with MMI, it's good to minimize the number of 'live' images displayed on the screen and the frequency with which Igor updates (refreshes) those images.  Such considerations may not be necessary for streaming at slower frame-rates or small image-sizes (ex. from a webcam) but may become critical when acquiring from high-speed or high-resolution cameras, or when performing complex image-processing during acquisition.

You have several options to control how images are displayed during acquisition:

- If you choose to show [the Data Browser](/igorpro/igor-basics/data-folders.md#the-data-browser), you may want to make sure it does not display a plot of the wave receiving the incoming image-stream.  You can either clear the browser's Plot checkbox (see [Display Checkboxes](/igorpro/igor-basics/data-folders.md#display-checkboxes)) to prevent it from displaying plots of any waves, or use the browser's main list to display some variable or wave other than the wave receiving the incoming images.  This will ensure the browser doesn't display the acquisition wave.

- You can decide whether (or not) to display the recipient wave at all during acquisition.  Doing so may be critical to some experiments but may not be required for others.

- You can use [MMI_GetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_getsequencerelaydivisor) and [MMI_SetSequenceRelayDivisor](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_setsequencerelaydivisor) to control what fraction of acquired images are actually relayed to the wave during sequential (streaming) acquisition.  Setting the relay-divisor to values greater than 1 instructs MMI to relay only 1/n images to Igor for analysis & display, but it does not change how MMI writes images to HDF5 data-files.  Thus the relay-divisor lets you adjust the richness (and burden) of Igor's real-time display & processing of images without interfering with how MMI saves images to file for later analysis.

### Images in Igor Waves {#images-in-igor-waves}

The digital imaging community generally counts rows of image pixels starting from the top and running to the bottom of an image and counts columns from the left edge of the image to the right.  These notes will refer to these as image-rows and image-columns, respectively.

Igor counts rows in a two-dimensional wave starting from the top and running to the bottom of a table displaying that wave's data and it counts columns from left to right of that table.  These notes will refer to these as Igor-rows and Igor-columns, respectively.

When Micro-Manager acquires and holds an image internally, the image's pixels are arrayed in the computer's memory in 'row-major order', starting with the left-most pixel of the topmost image-row.  Consecutive positions in memory contain the next pixel in the image-row, advancing from left to the right along the image-row until reaching its right-most pixel.  The next position in memory holds the left-most pixel of the second image-row, after which the left-to-right advance continues.

In contrast, when Igor stores a two-dimensional wave in memory, it uses 'column-major order', starting with the value in the first Igor-column and first Igor-row.  Consecutive positions in memory contain the next value in the first Igor-column, advancing from top to bottom along the Igor-column until reaching the bottom (i.e. the last Igor-row).  The next position in memory holds the top-most value of the second Igor-column, after which the top-to-bottom advance continues.

One consequence of this 'row-order' vs 'column-order' difference is that an image acquired by Micro-Manager and stored directly in memory managed by Igor as a two-dimensional wave will appear rotated when examined in an Igor table.  That is, each image-row is interpreted as an Igor-column and each image-column is interpreted as an Igor-row.   (This effect is common when handling digital images as Igor waves.  See [Image X and Y Coordinates](/igorpro/graphing/image-plots.md#image-x-and-y-coordinates) in Igor's help for [Image Plots](/igorpro/graphing/image-plots.md).)

When Igor graphs a wave, points taken from consecutive Igor-rows are generally arrayed horizontally, along the x axis of the graph.  The magnitudes of the values contained within the wave are generally displayed vertically, along the y axis, with larger values at positions closer to the top of the display.  These conventions produce graphs of the familiar form y = f(x).

In contrast, when a digital image is displayed (graphed) on the screen, consecutive image-rows are typically arrayed vertically, with the first image-row (row 0) at the top of the display and the last image-row at the bottom.  This amounts to an inversion of the vertical axis: lower coordinates (for the image-row) are near the top of the display, while higher coordinates (for the image-row) are near the bottom.

Thus images acquired by Micro-Manager and stored directly in memory managed by Igor as a two-dimensional wave will (by default) be displayed with an inversion of their vertical axis.  (This inversion too is common when handling digital images as Igor waves.  See [Image Orientation](/igorpro/graphing/image-plots.md#image-orientation) in Igor's help for [Image Plots](/igorpro/graphing/image-plots.md).)

To streamline its operation and optimize performance, MMI stores images acquired from Micro-Manager directly into Igor's waves, leaving any rotation or reorientation of the acquired images to you the user, to perform when best for you.

#### *See Also* {#preliminary-notes-see-also}

[Image Plots](/igorpro/graphing/image-plots.md), [Image X and Y Coordinates](/igorpro/graphing/image-plots.md#image-x-and-y-coordinates), [Image Orientation](/igorpro/graphing/image-plots.md#image-orientation)

[https://en.wikipedia.org/wiki/Row-_and_column-major_order](https://en.wikipedia.org/wiki/Row-_and_column-major_order)

### Working with Color Images {#working-with-color-images}

Many scientific cameras record only the intensity of the light incident on each pixel, ignoring the light's color and creating monochromatic (a.k.a. grayscale or black and white) images.  Other cameras (ex. most webcams and some machine-vision cameras), produce color images by recording the intensities of light at each pixel in each of several different color-bands (ex. Red, Green, and Blue).  To correctly interpret the color of images recorded by such cameras, it is crucial to understand the order in which the camera places the color information in memory.

Micro-manager delivers each pixel in a color image to MMI as a triplet of values, containing the red, green, and blue intensities, generally in that R-G-B order.  Some cameras deliver 4 values for each pixel, appending an 'Alpha' (opacity) value after the red, green, and blue intensities.  Some cameras however deliver their color information in the reverse order: as B-G-R triplets, or B-G-R-A quadruplets.  For example, Micro-Manager's 'OpenCVgrabber' camera-device uses the B-G-R ordering when delivering color images to MMI.

MMI is written to handle both R-G-B and B-G-R triplets (and their corresponding quadruplets) and knows to expect B-G-R triplets from OpenCVgrabber.  However, you may encounter other cameras where MMI gets the color-order wrong, reversing the red and blue color-channels it delivers to Igor.  To resolve this problem, MMI provides a color-order flag (/CLRO) for most of its image-acquisition operations, which allows you to override MMI's default color-ordering while performing that operation.

#### *See Also* {#preliminary-notes-see-also}

[https://en.wikipedia.org/wiki/RGBA_color_model](https://en.wikipedia.org/wiki/RGBA_color_model), [https://learnopencv.com/why-does-opencv-use-bgr-color-format/](https://learnopencv.com/why-does-opencv-use-bgr-color-format/), [MMC_GetImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_getimage), [MMC_SnapImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_snapimage), [MMC_StartSequenceAcquisition](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmc_startsequenceacquisition), [MMI_GrabImage](/igorpro/extensions/data-acquisition/mmi/micro-manager-methods.md#mmi_grabimage), [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera), [MMI_ModifyCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_modifycamera)