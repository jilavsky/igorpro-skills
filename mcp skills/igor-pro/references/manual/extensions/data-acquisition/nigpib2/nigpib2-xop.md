---
description: "NIGPIB2 is an Igor external operation (XOP) that permits you to control a National Instruments GPIB board from Igor procedures."
slug: /extensions/data-acquisition/nigpib2/nigpib2-xop
---

NIGPIB2 is an Igor external operation (XOP) that permits you to control a National Instruments GPIB board from Igor procedures.

This version of NIGPIB2 requires Igor Pro 8.00 it is available for 64-bit versions of Igor.

NIGPIB2 adds no menu items or dialogs to Igor. It does add operations that you can call from the command line or, more likely, from user-defined functions.

## Setup {#setup}

A National Instruments GPIB interface and the NI-488.2 driver, supplied by National Instruments, must be installed on your system.

We recommend that you update your NI-488.2 driver to version 14.0 or later, though earlier versions may work.

If you are running NIGPIB2 with Igor6, and you do not have the Visual Studio 2013 runtime libraries on your system, you need to download and install them. They are available from:

[http://www.microsoft.com/en-us/download/details.aspx?id=40784](http://www.microsoft.com/en-us/download/details.aspx?id=40784)

## Activating NIGPIB2 {#activating-nigpib2}

To use NIGPIB2 with IGOR64 (Igor7 or later), create an alias for the NIGPIB2-64.xop file, put the alias in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details) and then launch Igor. The command line operations described below will be added to Igor Pro.

## NIGPIB2 Operation Types {#nigpib2-operation-types}

NIGPIB2 adds two types of operations to Igor's repertoire. The first type gives you access to the NI-488.2 driver supplied by National Instruments. This type is called an NI-488 operation in this documentation and is invoked using the [NI4882](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#ni4882) operation. The second type of operation is a higher level operation that allows reading (e.g., [GPIBRead2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibread2)) and writing (e.g., [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2)) of data to and from Igor variables, strings and waves. This type is called a GPIB operation.

NIGPIB2 adds three types of operations to Igor's repertoire:

***Traditional NI488.2 Calls***

These are ancient yet still serviceable calls that address a GPIB device via a "unit descriptor" which you obtain from the NI488.2 driver using the ibfind and ibdev calls. NIGPIB2 supports these calls through the [NI4882](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#ni4882) operation.

***Multi-Device NI488.2 Calls***

These are newer calls that address a GPIB device via a board ID and a GPIB address. They do not require unit descriptors. NIGPIB2 supports these calls through the [NI4882](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#ni4882) operation.

***High-Level Calls***

These are high-level GPIB operations, such as [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2) and [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2), that build upon the NI488.2 driver calls to present a higher-level interface for reading and writing Igor variables, strings and waves. They require unit descriptors obtained using the ibfind and ibdev calls. For most purposes we recommend that you use these high-level GPIB operations.

## GPIB Programming Prerequisites {#gpib-programming-prerequisites}

To use an NI-488 operation, you need at least a basic understanding of the National Instruments GPIB hardware and the National Instruments NI-488.2 driver. Consult the NI-488.2 documentation installed with the driver.

The NI documentation is typically installed here:

```
C:\Program Files (x86)\National Instruments\NI-488.2\Help\GPIBHELP.chm
```

When you interface an instrument to Igor using NIGPIB2, you are dealing with software in the instrument, with the NI-488.2 driver software, and with the NIGPIB2 software. Interactions between these software elements can make interfacing difficult. You need to be thoroughly familiar with the instrument's GPIB capabilities and expectations and with the behavior of the NIGPIB2 XOP to succeed.

Specifically you need to know exactly what the instrument expects to receive as a command and exactly what the form of its response is, especially as relates to terminator characters (carriage-return and/or linefeed). And you need to know how to use the NIGPIB2 operations to accomodate the instrument's behavior.

The National Instruments configuration programs allow you to set many important operating parameters for each GPIB board in your system and for each device connected to each board. Usually the defaults work fine. Consult National Instruments documentation.

The exact settings you use depend on the instrument you are talking to. The important thing is that you know what your instrument expects and what the NIGPIB2 operations do so that you can coordinate them.

## A Simple GPIB Example {#a-simple-gpib-example}

Here is a minimal example in which we communicate with an instrument at GPIB address 1.

Global variables gGPIBBoardRef and gGPIBDeviceRef hold unit descriptors used to access the GPIB interface and the GPIB device which is the instrument that we want to control. This example is hardwired to a board named "gpib0" and to a device at GPIB address 1.

We use the NI-488.2 driver ibfind routine to obtain a unit desciptor for the GPIB interface. We use the ibdev routine to obtain a unit descriptor for the GPIB device.

We then use the "GPIB2 board" and "GPIB2 device" commands to tell NIGPIB2 which interface and device to use for high-level GPIB commands like GPIBWrite2 and GPIBRead2.

```igor
Function SetupGPIB()
    // Create global variables
    Variable/G root:gGPIBBoardRef = 0
    Variable/G root:gGPIBDeviceRef = 0

    // Get board descriptor
    NVAR gGPIBBoardRef = root:gGPIBBoardRef
    NI4882 ibfind={"gpib0"}; gGPIBBoardRef = V_flag
    GPIB2 board = gGPIBBoardRef     // Tell NIGPIB2 which board to communicate with

    // Get device descriptor for device at GPIB address 1
    NVAR gGPIBDeviceRef = root:gGPIBDeviceRef
    NI4882 ibdev={0,1,0,13,1,0}; gGPIBDeviceRef = V_flag
    GPIB2 device = gGPIBDeviceRef   // Tell NIGPIB2 which device to communicate with
End
```

:::note
Each time you call ibfind or ibdev, the NI-488.2 driver returns a new unit descriptor. Don't call ibfind or ibdev over and over again because the driver will eventually run out of unit descriptors and return an error.
:::

Once we have called SetupGPIB, we can use high level GPIB operations to send commands and read responses:

```igor
Function TestGPIBHighLevel()
    // Send a command to the device
    // This sends no terminator but the END signal is asserted with the last character
    GPIBWrite2 "ID?"

    // Read a response from the device
    String response
    GPIBRead2 /T="" response        // Read until END signal
    Print response
End
```

It is usually not necessary, but we can also call low-level NI-488 commands which map directly to the traditional functions provided by the NI-488.2 driver:

```igor
Function TestGPIBLowLevel()
    NVAR gGPIBDeviceRef = root:gGPIBDeviceRef

    // Send a command to the device
    String cmd = "ID?"
    Variable count = strlen(cmd)
    NI4882 ibwrt={gGPIBDeviceRef,cmd,count}

    // Read a response from the device
    count = 100	// ibrd will read till END signal
    NI4882 ibrd={gGPIBDeviceRef,count}
    String response = S_Value       // S_Value is set by NI4882 ibrd
    Print response
End
```

The traditional NI-488 low-level commands like ibfind, ibdev, ibrd and ibwrt take a unit descriptor as a parameter. High-level NIGPIB2 operations like GPIBWrite2 and GPIBRead2 use the unit descriptors specified via the "GPIB board" and "GPIB device" commands.

We can also call the multi-device NI-488.2 commands which map directly to the multi-device functions provided by the NI-488.2 driver. These have the virtue of using a board index number (typically 0), and a GPIB device address directly rather than unit descriptors. However they are cumbersome because they work with buffer waves rather than string variables.

## NIGPIB2 64-bit Integer Limitations {#nigpib2-64-bit-integer-limitations}

As of Igor Pro 7.00, Igor supports 64-bit signed and unsigned integer waves as well as 64-bit signed and unsigned function parameters and local variables. NIGPIB2 operations work with 64-bit integer values but are limited to 53 bits of precision. This means they work correctly with values up to about 9 quadrillion and produce incorrect results with larger values. This limitation stems from of the use of double-precision floating point variables, which store 53 bits for the [significand](IgorAction:BrowseURL__"https://en.wikipedia.org/wiki/Significand"), in the internal NIGPIB2 code and in Igor itself. Removing this limitation would require major rewrites and is not practical.

This limitation affects the following operations:

[GPIBReadBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinary2), [GPIBWriteBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinary2), [GPIBReadWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadwave2), [GPIBWriteWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritewave2)

A workaround is to use [GPIBReadBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinarywave2) and [GPIBWriteBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinarywave2) which work with 64-bit integer values of any magnitude.

## NIGPIB2 Binary Operations Byte Order {#nigpib2-binary-operations-byte-order}

The GPIBReadBinary2, GPIBReadBinaryWave2, GPIBWriteBinary2 and GPIBWriteBinaryWave2 operations read and write binary data. If you use them you need to make sure that the byte order they use is consistent with the requirements of your instrument. You specify the byte order for these operations using the /B flag.

The /B flag means "low byte first", also called "little endian". Omitting the /B flag means "high byte first", also called big-endian.

In NIGPIB2 version 1.11, which is shipped with Igor7 but not with Igor6, we added the following optional syntax:

```igor
/B=0		// Always high byte first
/B=1		// Always low byte first
```

If you use /B=0 or /B=1, as appropriate, your code will work across platforms but will require NIGPIB2 version 1.11 or later.
Although version 1.11 is not shipped with Igor6, it has been subjected to basic testing and appears to work with Igor6.

## Additional Documentation {#additional-documentation}

In addition to this help file, Igor Technical Note #019 describes using NIGPIB2 to drive a Tektronix digital oscilloscope. You can find this technical note in the Technical Notes folder.

## Changes in NIGPIB2 Relative to NIGPIB {#changes-in-nigpib2-relative-to-nigpib}

NIGPIB2 is a successor the the original NIGPIB XOP. The main changes are that NIGPIB2 requires Igor Pro 5.00 or later, can be invoked from user-defined functions, and uses somewhat different syntax. The following paragraphs describe the changes in more detail, to allow you to convert procedures using NIGPIB to NIGPIB2.

NI488 commands used to have a syntax like this:

```igor
NI488 ibwrt ud, str, count
```

To support compilation in user functions, NIGPIB2 uses syntax is like this:

```igor
NI4882 ibwrt={ud, str, count}
```

Similar syntax changes were made to the other operations. For example, the old syntax was

```igor
GPIB board, gBoardUnitDescriptor
```

The new syntax is:

```igor
GPIB2 board=gBoardUnitDescriptor
```

The following NI488 keywords used to return results via an Igor numeric variable whose name you specified in the command. NI4882 returns results via the V_flag variable:

```
ibask, ibfind, iblines, ibln, ibrpp, ibrsp, FindRQS, PPoll, ReadStatusByte,
TestSRQ, WaitSRQ
```

The ibrsp keyword previously always returned a positive number. Now, following the NI prototype for the ibrsp function, if the high bit of the serial poll response byte is set, the value returned via V_flag will be negative, because of sign extension.

The ibrd NI488 keyword used to return results via an Igor string variable whose name you specified in the command. NI4882 returns results via the S_value variable.

The ibllo call is no longer supported by the NI-488.2 driver. Use NI4882 SendLLO instead.

The [GPIB2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpib2) operation does not accept the /O flag or the quit keyword. It also no longer accepts the ShowBuffer and ClearBuffer keywords.

The GPIBRead operation previously accepted a circumflex (^) character in the parameter to the /T flag, which modified the behavior of GPIBRead2. [GPIBRead2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibread2) does not support this.

The internal number parsing done by GPIBRead2 has been simplified.

The GPIBReadWave /R flag previously accepted parameters in terms of X values or point numbers. GPIBReadWave2 accepts point numbers only.

The GPIBReadBinary /F, /L and /W flags have been replaced in [GPIBReadBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinary2) by the /TYPE flag.

The GPIBReadBinaryWave /F, /L and /W flags have been replaced in [GPIBReadBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinarywave2) by the /TYPE flag.

The GPIBWrite operation previously accepted a list of arguments that could be numbers or strings. [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2) accepts just a single string argument. As illustrated in the help for GPIBWrite2, you can use the sprintf operation to generate a string containing the values from other variables.

The GPIBWrite2 operation does not accept the /F flag.

The /F flag for the [GPIBWriteWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritewave2) operation has been changed completely. See the documentation for GPIBWriteWave2.

The GPIBWriteBinary /F, /L and /W flags have been replaced in [GPIBWriteBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinary2) by the /TYPE flag. GPIBWriteBinary2 can no longer transmit strings. Use [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2) for that.

The GPIBWriteBinaryWave /F, /L and /W flags have been replaced in [GPIBWriteBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinarywave2) by the /TYPE flag.

If you use GPIBReadBinary2, GPIBReadBinaryWave2, GPIBWriteBinary2 or GPIBWriteBinaryWave2, use either /B=0 (high byte first) or /B=1 (low byte first) to specify the byte order. See [NIGPIB2 Binary Operations Byte Order](#nigpib2-binary-operations-byte-order) for details.

NIGPIB used an input buffer. NIGPIB2 does not use an input buffer. It never reads more bytes from the bus than necessary to satisfy the current command. For most applications, this distinction is immaterial.

## Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.00 | This is the first release of NIGPIB2. |
| 1.01 | Fixed problem of the NI4882 operation not declaring the V_flag and S_value output variables. |
| 1.02 | Fixed a leak in NI-488 ibrd. |
| 1.03 | Made Macintosh universal to run on PowerPC and Intel. Replaced NIGPIB2_OSX.xop with NIGPIB2.xop. No changes were made to the Windows version. |
| 1.04 | The GPIBRead2 /Q flag did not work. This is now fixed. |
| 1.10 | This version is the first that supports IGOR64 on Macintosh. |
|  | This version is based on version 14.0 of the NI-488.2 driver. This driver version does not support the ibbna keyword which now returns an error. |
| 1.11 | Added /B=byteOrder to [GPIBReadBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinary2), [GPIBWriteBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinary2), [GPIBReadBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinarywave2) and [GPIBWriteBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinarywave2). See [NIGPIB2 Binary Operations Byte Order](#nigpib2-binary-operations-byte-order) for details. |
| 1.12 | Recompiled with XOP Toolkit 7.01 to support Igor Pro 8 on 64-bit Macintosh. |
| 2.00 | Recompiled with long name and path support for Igor8. This version requires Igor Pro 8.00 or later. |