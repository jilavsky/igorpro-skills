---
description: "The AxonTelegraph XOP provides a way to read the telegraph \"outputs\" of an Axon *MultiClamp 700A or 700B amplifier from within the Windows version of Igor Pro."
slug: /extensions/data-acquisition/axontelegraph/axontelegraph-xop
---

The AxonTelegraph XOP provides a way to read the telegraph "outputs" of an Axon \*MultiClamp 700A or 700B amplifier from within the Windows version of Igor Pro.  These amplifiers are computer-controlled, dual-channel patch clamp and current clamp amplifiers.  The 700A connects to the computer via a serial port; the 700B via a USB connection.

This XOP uses part of a software developers toolkit, provided by Axon, to communicate with the amplifier.

:::note
This XOP does not provide a way to control the amplifier from Igor Pro.  Instead, it is expected that the user will use another program, typically the MultiClamp Commander application that comes with the amplifier, to control it.  This XOP only allows Igor to read the current settings, such as gain, mode, and lowpass filter frequency, from the amplifier.
:::

**\*** Now owned by Molecular Devices.

## Index of AxonTelegraph XOP Topics {#index-of-axontelegraph-xop-topics}

- [Installing The AxonTelegraph XOP](#installing-the-axontelegraph-xop)
- [AxonTelegraph XOP Details](#axontelegraph-xop-details)
- [AxonTelegraph XOP Usage](#axontelegraph-xop-usage)
- [AxonTelegraph XOP Operation and Function Reference](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md)

## Installing The AxonTelegraph XOP {#installing-the-axontelegraph-xop}

Version 3.00 and later of this XOP requires Igor Pro 8.00 or later. If you are using an earlier version of Igor Pro, you must also use an earlier version of this XOP.

1. Make a shortcut for the following file:

    ```
    Igor Pro Folder\More Extensions (64-bit)\Data Acquisition\AxonTelegraph.xop
    ```

    Move this shortcut into "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details). This activates the AxonTelegraph XOP for the 64-bit version of Igor Pro.


2. Restart Igor Pro.

To uninstall the AxonTelegraph XOP, delete the shortcuts created above and restart Igor.

## AxonTelegraph XOP Details {#axontelegraph-xop-details}

### Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.00 | Initial release. |
| 2.00 | Updated XOP to support Igor 7. |
| 3.00 | Updated XOP to support Igor 8 and long wave names. |

### Terminology {#terminology}

The following terms are used in the description of the operation and functions provided by the AxonTelegraph XOP.

|  |  |
| --- | --- |
| Serial number | An integer that uniquely identifies a physical 700B amplifier.  The serial number for all available devices can be obtained by using the [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers) operation.  The author of this XOP assumes that the serial number obtained from this operation is identical to the serial number physically affixed to an amplifier, but is not certain that this is true. If there is any discrepancy, always use the serial number obtained from [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers).  Not used for 700A servers. |
| Channel ID | An integer that uniquely identifies one channel of a 700A or 700B server.  As far as this author knows this will always be 1 or 2, as both amplifier types have two channels. |
| Axo Bus ID | A number from 0 to 9 used in combination with the Channel ID and the Com Port ID to identify a 700A telegraph server.  Not used for 700B servers. |
| Com Port ID | A number from 1 to 4 that identifies the serial COM port the physical amplifier is connected to.  Not used for 700B servers. |
| Server | A computer process with which this XOP receives telegraph data.  For 700A amplifiers, each unique combination of Axo Bus ID, Com Port ID, and Channel ID identifies a server.  For 700B amplifiers, each unique combination of one serial number and one channel ID identifies a server. The MultiClamp Commander application, which is typically used to control the amplifier's settings, provides two servers, one for channel 1 and one for channel 2.  Servers can also be created by using other software, such as the MCTeleServer executable that is included in the Axon Telegraph software development kit. |
| Timeout | All routines provided by this XOP that request information from a server do so by sending a "message" to the server.  When the server receives this request, it will respond to the XOP with its own message.  When [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers) is called, the XOP will wait for the duration of the timeout to help ensure that all available telegraph servers are found.  For all other functions the XOP will wait until it receives a data packet or the timeout is reached if no packet is received.  For more information see [AxonTelegraphSetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphsettimeoutms). |

## AxonTelegraph XOP Usage {#axontelegraph-xop-usage}

In order to use any of the functions or operations provided by the AxonTelegraph XOP, at least one telegraph server must be available for the XOP to communicate with.  The MultiClamp Commander software application, which comes with the amplifier, typically serves this role.  Note that it is possible to run the MultiClamp Commander application, and use the calls provided by this XOP, even if no amplifiers are connected to the computer.  This makes it possible to write and test code that uses the calls this XOP provides without needing to have an amplifier attached to the same computer.

**Using the Axon Telegraph Monitor panel**

Included in the same directory as this help file and the AxonTelegraph XOP file is an Igor Pro procedure file named AxonTelegraphMonitor.ipf.  This procedure file provides code that creates an Igor panel that allows you to monitor the telegraph readings from a telegraph server.  Note that it is not possible to control the amplifier settings from this panel because this XOP does not provide any abilities to control the amplifier, only to read the telegraph settings.

To use the panel you must first open the AxonTelegraphMonitor.ipf procedure file in Igor and then compile your procedures.  When you do so a `Misc→Axon Telegraph Monitor` menu item will be created.  Select the menu item to open the panel.

First click on the "Find servers" button at the top of the panel so that all available telegraph servers can be found.  Next, select one of the telegraph servers from the "Select server" popup menu.  When you select a server, the displays on the panel will show you the current values for that server.  If you wish to monitor the server's settings and have any changes be automatically reflected in the panel, click the "Start monitoring" button.

Clicking the Start monitoring causes a background task to be activated that checks the telegraph settings two times per second.  Values will continue to update on the panel when they are changed until you click the "Stop monitoring" button.  Monitoring will also stop if the panel window is closed.  The timeout value used by the XOP can also be set by using the "Timeout" control.

<img src="MD_images/AxonTelegraph Help/multiclamp.png" width="100%"/>