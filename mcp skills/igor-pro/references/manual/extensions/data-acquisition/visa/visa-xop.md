---
description: "VISA (Virtual Instrument Software Architecture) is an instrument control system defined by the VXIplug&play Systems Alliance which is part of the IVI…"
slug: /extensions/data-acquisition/visa/visa-xop
---

VISA (Virtual Instrument Software Architecture) is an instrument control system defined by the VXIplug&play Systems Alliance which is part of the IVI Foundation ([https://www.ivifoundation.org/specifications/default.html#vxiplugplay-specifications](https://www.ivifoundation.org/specifications/default.html#vxiplugplay-specifications)). It enables a program to control VISA-compliant instruments connected to a computer through serial port, GPIB, Ethernet, VXI bus, USB, and other media.

With USB, only instruments that support the [USBTMC protocol](IgorAction:BrowseURL__"https://knowledge.ni.com/KnowledgeArticleDetails?id=kA03q000000x1qzCAA") are supported. If in doubt check with your instrument vendor. To interface with non-USBTMC instruments via USB, you need to write your own XOP that uses a vendor-supplied library.

There are several implementations of the VISA library. The most prominent is NI-VISA from National Instruments. It is the only implementation that we have used.

To use VISA with Igor you need to understand the basics of VISA. The National Instruments NI-VISA User Manual presents the basics of VISA very well. It is written for C programmers but you need to understand the same concepts to use VISA from Igor. Even if you are using a different VISA implementation, we recommend that you read the first five chapters of the NI VISA User Manual. You can download the NI-VISA User Manual from [http://www.ni.com/pdf/manuals/370423a.pdf](http://www.ni.com/pdf/manuals/370423a.pdf).

This version of VISA XOP requires Igor Pro 8.00 or later because it supports long object names and paths. It runs on Windows in 64 bits (VISA64.xop).

You must have an implementation of VISA, such as NI-VISA, installed on your machine. You need to consult the documentation from your VISA library vendor to learn how to configure the VISA system.

The VISA XOP adds no menu items or dialogs to Igor. It does add a set of operations and functions which you can call from Igor user-defined functions. The [VISA XOP Functions](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md) are low-level functions that map directly to VISA library functions. The [VISA XOP Operations](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visa-xop-operations) are higher level operations similar to operations added by Igor's NIGPIB2 XOP. For most applications you will rely on the high-level operations and the basic low-level functions such as viOpen and viClose.

An Igor procedure file, VISA.ipf, is also provided. It defines constants that you need when calling the VISA XOP functions.

VISA XOP supports a subset of the capability of the VISA library. This subset will be sufficient for most data acquisitions tasks. Capabilities not supported include:

- Formatted I/O
- Asynchronous I/O
- Event handler callbacks

When you interface an instrument to Igor using VISA, you are dealing with software in the instrument, with the VISA library and with the VISA XOP. Interactions between these software elements can make interfacing difficult. You can speed development and avoid frustration by eliminating unknowns. You need a basic understanding of VISA, a good understanding the instrument's capabilities and expectations, and a good understanding of the VISA XOP to succeed.

VISA XOP is thread-safe. See [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking) for information on multithreaded programming.

## Installing VISA and VISA XOP {#installing-visa-and-visa-xop}

You must install a VISA library implementation (e.g., NI-VISA, TekVISA or Agilent VISA) on your machine. If you don't already have a VISA library that came with from your instrument supplier, NI-VISA is recommended.

You should be able to find a link to the NI-VISA installer for your platform at [https://www.ni.com/en-us/support/downloads/drivers/download.ni-visa.html](https://www.ni.com/en-us/support/downloads/drivers/download.ni-visa.html). You will need to read the documentation for the installed implementation to learn how to configure it for your hardware.

Starting with Mac OS 11.4, the operating system does not load kernel extensions required by the NI-VISA driver by default, causing Igor to crash. To make the drivers work, you need to do extra steps described at [https://www.wavemetrics.com/forum/general/ni-visa-driver-mac-os-12-monterey](https://www.wavemetrics.com/forum/general/ni-visa-driver-mac-os-12-monterey).

To activate the 64-bit version of VISA XOP, create a shortcut for the VISA64.xop file and put it in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details).

Also activate VISA.ipf as a global procedure file by making a shortcut  for the VISA.ipf file and putting the it in "Igor Pro User Files/Igor Procedures" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details).

Now relaunch Igor.


## VISA XOP 64-bit Integer Limitations {#visa-xop-64-bit-integer-limitations}

Igor Pro 7 and later support 64-bit signed and unsigned integer waves as well as 64-bit signed and unsigned function parameters and local variables. VISA XOP operations work with 64-bit integer values but are limited to 53 bits of precision. This means they work correctly with values up to about 9 quadrillion and produce incorrect results with larger values. This limitation stems from of the use of double-precision floating point variables, which store 53 bits for the significand, in the internal VISA XOP code and in Igor itself. Removing this limitation would require major rewrites and is not practical.

This limitation affects the following operations:
[VISAReadBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinary), [VISAWriteBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritebinary), [VISAReadWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadwave), [VISAWriteWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritewave)

A workaround is to use VISAReadBinaryWave and VISAWriteBinaryWave which work with 64-bit integer values of any magnitude.

## VISA Library Terminator Character Issues {#visa-library-terminator-character-issues}

When reading data, by default the VISA library stops reading when it encounters a terminator character. The terminator character defaults to linefeed (decimal value 10).

This may cause problems with the viRead function and the VISARead, VISAReadWave, VISAReadBinary, and VISAReadBinaryWave operations. Problems are most likely with the VISAReadBinary and VISAReadBinaryWave.

This default behavior causes a problem if you read binary data using VISAReadBinary or VISAReadBinaryWave. If the binary data happens to contain a byte with decimal value 10, the VISA library stops reading.

To fix this, you need to set two attributes, like this:

```igor
viSetAttribute(session, VI_ATTR_TERMCHAR_EN, 0)	// Disable terminator character detection
viSetAttribute(session, VI_ATTR_ASRL_END_IN, 0)	// Disable terminator character detection for serial ports
```

The `VI_ATTR_TERMCHAR_EN` attribute works for all types of I/O except for serial port I/O. The `VI_ATTR_ASRL_END_IN` attribute works for serial port I/O. This is explained at [https://www.ni.com/tutorial/4256/en/#toc2](https://www.ni.com/tutorial/4256/en/#toc2) - see "Termination Character Enabled" (`VI_ATTR_TERMCHAR_EN`) and "Serial End Modes for Reads" (`VI_ATTR_ASRL_END_IN`).

We recommending setting both of the attributes as shown above so that terminator character detection will be disabled regardless of the type of instrument you are communicating with.

This problem also affects the viRead function and the VISARead and VISAReadWave operations.

In the case of viRead, it always terminates on a terminator character unless you use the commands above to disable terminator character detection. If you intend to read a certain number of bytes regardless of what they might be, use the commands above.

In the case of VISARead and VISAReadWave, if you omit /T=termStr or specify something other than "" for termStr, these operations read bytes one-at-a-time and the VISA library treatment of terminator characters does not come into play. However, if you specify /T="", they read the number of bytes specified by /N=n in one call to the VISA library. In this case, the presence of a terminator character stops reading before n bytes have been read unless you set the attributes shown above. If you use /T="" with VISARead or VISAReadWave, use the commands above to disable terminator character detection.

### Revision Notes {#revision-notes}

| Version | Notes |
| ------ | ----- |
| 1.00 | This is the first release of the VISA XOP. |
| 1.01 | Now runs on Intel Mac OS X as well as PowerPC Mac OS X. |
| 1.02 | Fixed leaks in viWrite, viSetAttributeString and viLock. Fixed a leak in viRead that occurred only if the cnt parameter was greater than 1024. |
| 1.03 | On Intel Macintosh only, byte swapping for `VISAReadBinary`, `VISAReadBinaryWave`, `VISAWriteBinary` and `VISAWriteBinaryWave` was backwards. If you specified /B (low-byte-first), meaning that you were reading or writing little-endian data, the data was byte-swapped when it should not have been. Conversely, if you omitted /B, meaning that you were reading or writing big-endian data, the data was not byte-swapped when it should have been. This has been fixed. If you are using these operations on Intel Macintosh then this fix will break your code. You need to remove /B if you are using it and add it if you are not using it. |
| 1.04 | Added support for reading the `VI_ATTR_USB_RECV_INTR_DATA` attribute using the viGetAttributeString function. |
| 1.10 | This version requires Igor Pro 6.20 or later. It is the first that supports IGOR64 on Macintosh. |
|  | This version supports reading and writing 64-bit integer values using `VISAReadBinary`, `VISAWriteBinary`, `VISAReadBinaryWave`, and `VISAWriteBinaryWave`. |
|  | In this version, if you call VISARead with /T="" (no terminators), VISARead attempts to read the number of bytes specified by the /N flag in one call rather than reading one byte at a time. This is similar to the behavior of VISAReadBinary and provides faster speed. |
| 1.11 | Recompiled with XOP Toolkit 7.01 to support Igor Pro 8 on 64-bit Macintosh. |
| 1.20 | Made VISA XOP thread safe but this has not been thoroughly tested. |
| 1.30 | This version of the VISA XOP requires Igor Pro 8.00 or later because it supports long object names. |
| 1.31 | Removed calls to `WatchCursor` from `VISARead`, `VISAReadBinary`, `VISAWrite`, and `VISAWriteBinary`. These `WatchCursor` calls caused a bug dialog to be displayed if these operations were called from a pre-emptive thread. |

## VISA Procedure File {#visa-procedure-file}

The VISA.ipf Igor procedure file defines in Igor many of the constants defined by the VISA library. You will need these constants when calling VISA XOP functions. For example, VISA.ipf defines the constant `VI_ATTR_ASRL_BAUD` which you would pass to the VISA XOP function viSetAttribute to set the baud rate of a serial port.