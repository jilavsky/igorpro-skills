---
description: "This help file describes the WaveMetrics-supplied extensions. Igor includes a feature for extending its capabilities."
slug: /extensions/xop-index
---

# External Operations Index {#external-operations-index}

This help file describes the WaveMetrics-supplied extensions.

Igor includes a feature for extending its capabilities. We call this the External Operation or XOP feature. An XOP, which is also called an Igor extension, is a piece of separately compiled code that Igor can call to accomplish things that are not built into the Igor application program.

XOPs come in 32-bit and 64-bit varieties. Because almost all Igor users now run the 64-bit version of Igor, this and following sections focus on 64-bit XOPs.

XOPs that are in "Igor Pro Folder/Igor Extensions (64-bit)" and in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details) when Igor is launched are immediately available for use.

Extensions installed in "Igor Pro Folder/More Extensions (64-bit)" must be activated before you can use them. See [Activating 64-bit Extensions](/igorpro/igor-basics/using-igor.md#activating-64-bit-extensions) for instructions.

Igor Pro comes with XOPs for other jobs such as communicating via serial or GPIB ports, accessing SQL databases, importing data from NetCDF and TDM files, and more.

Below we show you where the XOP files were installed, so you can activate them more easily.

### *See also* {#see-also}
[Igor Extensions](/igorpro/igor-basics/using-igor.md#igor-extensions), [Activating 64-bit Extensions](/igorpro/igor-basics/using-igor.md#activating-64-bit-extensions)



## XOPs in More Extensions {#xops-in-more-extensions}

The "More Extensions (64-bit)" folder in the Igor Pro Folder contains WaveMetrics XOPs that you can activate. See [Activating 64-bit Extensions](/igorpro/igor-basics/using-igor.md#activating-64-bit-extensions) for instructions.

The XOPs in the "More Extensions (64-bit)" folder are sorted into subfolders:

### Data Acquisition XOPs {#data-acquisition-xops}

[AxonTelegraph XOP](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop.md) - Windows only. Provides routines that support reading of the telegraph outputs (eg. gain and mode) of an Axon (now Molecular Devices) MultiClamp 700B patch clamp amplifier.

[MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md) - Provides an interface between Igor and Micro-Manager, an open-source software package for automating light microscopy.  Working through Micro-Manager, MMI enables Igor to acquire images from a wide range of cameras and control devices such as light-sources, filter wheels, stages, etc.

[NIGPIB2 XOP](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md) - Controls a National Instruments GPIB board from Igor's command line or from an Igor procedure. A National Instruments GPIB card and the NI-488 driver, supplied by National Instruments, must be installed on your system.

[VDT2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdt2) - Implements a Very Dumb Terminal emulator. VDT2 adds a submenu to Igor's Misc menu. It adds a full featured text window with scrolling, find, replace, undo, and other amenities. VDT2 also allows you to control serial port communications from Igor procedures. It also adds a number of VDTxxx2 operations to configure and communicate with a port. You can use the operations to control an instrument or to communicate with another computer.

[VISA XOP](/igorpro/extensions/data-acquisition/visa/visa-xop.md) - VISA (Virtual Instrument Software Architecture) is an instrument control system which enables a program to control VISA-compliant instruments connected to a computer through serial port, GPIB, Ethernet, VXI bus and other media.

### File Loader XOPs {#file-loader-xops}

[HDF Loader XOP](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-xop.md) - Reads data from HDF files that conform to HDF version 3 (rev4) or earlier. Adds the [HDFInfo](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfinfo), [HDFReadImage](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadimage), [HDFReadSDS](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadsds), and [HDFReadVSet](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadvset) operations. Support for HDF5 is built into Igor Pro 9 and later.

[NETCDF XOP](/igorpro/extensions/file-loaders/netcdf/netcdf-xop.md) - Imports data from NetCDF Classic and NetCDF 64-bit offset files.

[NILoadWave XOP](/igorpro/extensions/file-loaders/niloadwave-xop.md) - Imports data from Nicolet files. Adds a menu item to Igor's Load Wave File... submenu and the NILoadWave operation. NILoadWave loads Nicolet WFT files but not WFF files. It handles multisegment files and waveforms with up to three zones. It does not handle WFF files.

[TDM XOP](/igorpro/extensions/file-loaders/tdm/tdm-xop.md) - loads and saves National Instruments' TDM data files. Adds a Load TDM File menu item to the Load Waves submenu.

### Utility XOPs {#utility-xops}

[SQL XOP](/igorpro/extensions/utilities/sql/sql-xop.md) - SQL XOP provides access to relational databases from IGOR procedures.