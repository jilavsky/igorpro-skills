---
description: "The TDM XOP provides access to National Instruments' TDM (Technical Data Management) files which are typically produced by NI's LabVIEW and DIAdem programs."
slug: /extensions/file-loaders/tdm/tdm-xop
---

The TDM XOP provides access to National Instruments' TDM (Technical Data Management) files which are typically produced by NI's LabVIEW and DIAdem programs. It provides a high-level interface through the [TDMLoadData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmloaddata) and [TDMSaveData](/igorpro/extensions/file-loaders/tdm/tdm-xop-operations.md#tdmsavedata) functions and a low-level interface through the TDM XOP functions.

TDM XOP runs on Windows only. This version requires Igor Pro 8.00 or later and supports long object names.

You can access the TDMLoadData operation via an Igor command or via the `Data→Load Waves→Load TDM File` menu item. To simply load a TDM file into Igor, the Load TDM File menu item is all that you need to know about.

The TDMSaveData operation is accessible via an Igor command only.

Some advanced applictions may require that you write Igor user-defined procedures to call the low-level TDM XOP functions.

TDM XOP is based on National Instruments' DIAdem Connectivity Library. As of this writing, National Instruments supplies the DIAdem Connectivity Library for Windows only, so TDM XOP runs on Windows only.

There are two types of TDM files: .tdm (TDM) and .tdms (TDMS). The "S" in TDMS stands for "streaming." The TDMS format is newer and is recommended by National Instruments.

TDM files, whether .tdm or .tdms, contain 1D data sets called channels organized in groups called channel groups. Channel groups can not contain other channel groups. Channels may contain integer or floating point data or string data.

Software that writes a TDM file can attach properties to the file as a whole, to a channel group and to a channel. The properties, which can be numeric, string or timestamp, can be used to document conditions associated with a file, channel group or channel.

## Background Information {#background-information}

The following web page gives background information on TDM files:

- National Instruments Technical Data Management Model: [http://zone.ni.com/devzone/cda/tut/p/id/3727](http://zone.ni.com/devzone/cda/tut/p/id/3727)

## Installing TDM XOP {#installing-tdm-xop}

This version of TDM XOP requires Igor Pro 8.00 or later and runs on Windows 64-bit only.
The TDM XOP depends on dynamic libraries supplied by National Instruments which in turn depend on Microsoft dynamic libraries that you may or may not already have.

|  |  |
| --- | --- |
| DIADEM Connectivity Library (low-level API) | [https://www.ni.com/content/dam/web/product-documentation/c_dll_tdm.zip](https://www.ni.com/content/dam/web/product-documentation/c_dll_tdm.zip) |

## Installing the 64-bit Version of the TDM XOP {#installing-the-64-bit-version-of-the-tdm-xop}

Here are the procedures to install the necessary libraries and activate the 64-bit version of the TDM XOP for use with IGOR64:


1. Download the "c_tdm_dll" package from the downloads section at [http://www.ni.com/white-paper/3727/en/](http://www.ni.com/white-paper/3727/en/).

2. Unzip the downloaded package to create the "c_tdm_dll" directory which contains the National Instruments' TDM support files.

3. Copy the entire contents of "c_tdm_dll/dev/bin/64-bit" to the folder containing the Igor64 application file. In Igor8, the path to this folder will be something like:

	C:\Program Files\WaveMetrics\Igor Pro 8 Folder\IgorBinaries_x64

:::note
You may not need to do the following step because you may already have the required Microsoft DLLs or later versions of them. You can skip this step and do it later only if Igor reports an error when you try to access the TDM XOP.
:::

4.	Download and install the following "Visual C++ 2015 Redistributable Package (x64)" from Microsoft:

	[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

5. Create a shortcut for the TDM64.xop file and put the shortcut in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details).

6. Restart Igor.

	As of this writing (October 2, 2019), the version of c_tdm_dll is 17.0 and the required files and folders from /dev/bin/64-bit are:

    ```
    DataModels (folder)
    dacasr.dll
    nilibddc.dll
    tdms_ebd.dll
    Uds.dll
    usiEx.dll
    usiPluginTDM.dll
    uspTdms.dll
    xerces-c_3_1_usi.dll
    ```

These Microsoft DLLs installed in step 4 above are also required.

The TDM XOP relies only on these files. It does not require the installation of any other National Instruments software.

If you ever want to uninstall TDM XOP, you must remove all of these TDM files from the IgorBinaries_x64 folder, and also remove the shortcut from the "Igor Extensions (64-bit)" folder, and then restart Igor.


## Testing the TDM Installation {#testing-the-tdm-installation}

In Igor, choose `Data→Load Waves→Load TDM File` and select a TDM file. It should be loaded into a new data folder in the current data folder.

## Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.00 | Initial release. |
| 1.01 | The Data→Load Waves→Load TDM File menu item did not properly escape the Windows file path that it put in the command line. This could lead to an error in opening the file. The menu item is now changed to use Macintosh-style paths to avoid this issue of escaping Windows backslash characters. |
|  | Added special handling to TDMLoadData for channels consisting of 0 elements. The TDM library DDC_GetDataValues returns an error if asked to get 0 elements. |
|  | Fixed problem of name conflicts in TDMLoadData when loading channel groups whose names exceed 31 characters. |
|  | Fixed problem of name conflicts in TDMLoadData when loading channels whose names exceed 31 characters. |
|  | Suppressed "variable renamed because of a conflict" warning messages in TDMLoadData. They were annoying. |
| 1.50 | This release requires Igor Pro 6.38 or later. |
|  | This release includes a 64-bit version as well as a 32-bit version. |
|  | This version supports the TDM waveform properties wf_start_time, wf_start_offset, wf_increment, and wf_xunit_string, which are described at: [http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/](http://zone.ni.com/reference/en-XX/help/370859H-01/tdmdatamodel/tdmdatamodel/tdm_tdxdata_waveform/) |
|  | Added the TDMLoadData /XSCL flag which allows you to set the X scaling and X units properties of Igor waves from TDM channels containing the wf_start_time, wf_start_offset, wf_increment, and wf_xunit_string properties. |
|  | When you choose Data→Load Waves→Load TDM File, the command generated uses the /XSCL=15 flag which causes TDMLoadWave to use the waveform channel properties to set the X scaling and X units of the loaded waves. |
|  | Added the TDMSaveData /XSCL flag. |
|  | If you omit the /XSCL flag or specify /XSCL=-1, TDMSaveData writes the waveform channel property wf_start_time or wf_start_offset, as well as the wf_increment and wf_xunit_string waveform channel properties. |
|  | TDMLoadData and TDMSaveData now properly set V_Flag to -1 if the user cancels from the Open or Save File dialog. |
| 1.60 | This release requires Igor Pro 8.00 or later and supports long object names. It was compiled using version 13.0 of the National Instruments TDM support files. |
|  | Previous TDM XOPs require Visual C++ 2005 runtime libraries from Microsoft. This version requires Visual C++ 2010 runtime libraries. See the installation instructions above for details. |