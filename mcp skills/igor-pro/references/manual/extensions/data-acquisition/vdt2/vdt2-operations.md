---
description: "Here are the command line operations added by VDT2. They can be invoked from the command line or from macros, just like built-in Igor operations."
slug: /extensions/data-acquisition/vdt2/vdt2-operations
---

Here are the command line operations added by VDT2. They can be invoked from the command line or from macros, just like built-in Igor operations. To successfully use these operations you need to know a bit about serial communications and what your other device expects to receive and what it sends.

| Operation | Details |
| --- | --- |
| [VDTGetPortList2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtgetportlist2) | Returns a list of supported ports in the string variable S_VDT. |
| [VDTOpenPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtopenport2) | Opens a port for use by VDT2. You don't necessarily need to use this operation because VDT2 will  |automatically open ports as you use them.
| [VDTClosePort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtcloseport2) | Closes a port so that it can be used by other programs. You don't necessarily need to use this  |operation because VDT2 will automatically close ports when you quit Igor.
| [VDTTerminalPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtterminalport2) | Designates the physical port to be used for dumb terminal functions. |
| [VDTOperationsPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtoperationsport2) | Designates the physical port to be used for command line operations. |
| [VDTGetStatus2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtgetstatus2) | Returns information regarding the state of the operations ports, such as error status. This is  |intended as a diagnostic aid when communication is not working.
| [VDT2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdt2) | Sets port parameters and input buffer size. Use the killio keyword to clear the input buffer of any  |garbage before starting a new dialog with the other device.
| [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2) | Reads ASCII data from the operations port into Igor numeric and string variables. |
| [VDTReadBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinary2) | Reads binary data from the operations port into Igor numeric and string variables. |
| [VDTReadWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadwave2) | Reads ASCII data from the operations port into Igor numeric or text waves. |
| [VDTReadBinaryWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinarywave2) | Reads binary data from the operations port into Igor numeric waves. |
| [VDTReadHex2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadhex2) | Reads ASCII hexadecimal data from the operations port into Igor numeric variables. |
| [VDTReadHexWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadhexwave2) | Reads ASCII hexadecimal data from the operations port into Igor numeric waves. |
| [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) | Writes an ASCII string to the operations port. |
| [VDTWriteBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritebinary2) | Writes numeric values as binary to the operations port. |
| [VDTWriteWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritewave2) | Writes numeric or text wave values as ASCII to the operations port. |
| [VDTWriteBinaryWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritebinarywave2) | Writes numeric wave values as binary to the operations port. |
| [VDTWriteHex2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritehex2) | Writes a single integer numeric value as hexadecimal. |
| [VDTWriteHexWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritehexwave2) | Writes numeric wave values as ASCII hexadecimal to the operations port. |

<div className="command-signature">

## <strong>VDT2</strong>  [/P=<em>portName</em> ] [ <em>abort</em>, <em>baud</em>=<em>n</em>, <em>buffer</em>=<em>n</em>, <em>databits</em>=<em>n</em>, <em>echo</em>=<em>n</em>, <em>in</em>=<em>n</em>, <em>killio</em>, <em>line</em>=<em>n</em>, <em>out</em>=<em>n</em>, <em>parity</em>=<em>n</em>, <em>port</em>=<em>n</em>, <em>resetPorts</em>, <em>rts</em>=<em>v</em>, <em>stopbits</em>=<em>n</em>, <em>terminalEOL</em>=<em>t</em> ] {#vdt2}

</div>

Controls serial port hardware and VDT2 input/output settings.

VDT2 executes keywords in a preset order, regardless of the order they appear in the command. The abort and killio keywords are serviced first, followed by the port keyword, followed by the others.

Do not use any keyword more than once in a single VDT2 command. VDT2 will ignore all but the last occurrence of a particular keyword. To change settings for multiple serial ports, you must use multiple VDT2 commands.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDT2 operates on the named port. |
|  | If you omit /P=*portName*, VDT2 operates on the current operations port. If you have not selected an operations port, VDT2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDT2 from a preemptive thread, you must include /P=*portName*. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| abort | Aborts the terminal operations Send File, Receive File, or Send VDT2 Text started from the VDT2 submenu if they are in progress. |
|  | The abort keyword is not allowed in a preemptive thread. |
| <span class="table-cell-nowrap">baud = n</span> | Sets baud rate. n must be one of the following: 300, 600, 1200, 2400, 4800, 9600, 19200, 38400, 57600, 115200, 128000, 230400, 256000, 460800, 921600. |
|  | <div><Admonition type="warning"><p>Your hardware may not support high baud rates and the serial input buffer may be too small to work at high baud rates. You should always verify that you can communicate at a lower baud rate before trying the higher rates.</p></Admonition></div> |
| <span class="table-cell-nowrap">buffer = n</span> | n=number size of input buffer in bytes (32 or greater). This isnot guaranteed to work on Windows. See [Input Buffer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#input-buffer-limitations). |
| <span class="table-cell-nowrap">databits = n</span> | n=7 or 8 for 7 or 8 databits. |
| <span class="table-cell-nowrap">echo = n</span> | n=0 for no local echo, 1 for local echo. This affects the terminal port only. |
| <span class="table-cell-nowrap">in = n</span> | n=0 for no input handshake, 1 for CTS/DTR, 2 for XON/XOFF. |
| <span class="table-cell-nowrap">line = n</span> | n=0 for offline, n=1 for online. This is archaic. Use the [VDTTerminalPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtterminalport2) operation instead, as explained below. |
| killio | Halts any pending IO and clears input buffer. |
| <span class="table-cell-nowrap">out = n</span> | n=0 for no output handshake, 1 for CTS/DTR, 2 for XON/XOFF. |
| <span class="table-cell-nowrap">parity = n</span> | n=0 for no parity, 1 for odd parity, 2 for even parity. |
| <span class="table-cell-nowrap">port = n</span> | Sets the operations port. This is archaic. Use the [VDTOperationsPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtoperationsport2) operation instead. |
|  | Windows: n=0 or n=1 selects the COM1 port. |
| resetPorts | Resets all serial ports to the state they would be in if VDT2 were relaunched. |
|  | resetPorts was added in VDT2 version 2.20 to provide a way to adapt if serial ports are added or removed from the machine while Igor is running. See [Detecting Serial Port Hardware Changes](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#detecting-serial-port-hardware-changes) for details. |
|  | resetPorts must be the only keyword in the VDT2 command. |
|  | The resetPorts keyword is not allowed in a preemptive thread. |
| <span class="table-cell-nowrap">stopbits = n</span> | n=1 or 2 for 1 or 2 stop bits. |
| <span class="table-cell-nowrap">terminalEOL = t</span> | t=0 for carriage return, 1 for linefeed, 2 for carriage return plus linefeed. This determines what VDT2 sends in dumb-terminal mode when you press the return or enter keys. It affects the terminal port only. |
| <span class="table-cell-nowrap">rts = n</span> | n=0 to disable the RTS line, n=1 to enable it. The default is 1. |
|  | This keyword is provided for extremely rare situations where the device you are connected to requires that the RTS line be disabled. |

### *Details* {#details}

:::warning
Your hardware may not support high baud rates and the serial input buffer may be too small to work at high baud rates. You should always verify that you can communicate at a lower baud rate before trying the higher rates.
:::

You are not guaranteed to get the input buffer that you request.  See [Input Buffer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#input-buffer-limitations) for details.

Online means that characters that come into the designated terminal port are sent to the VDT2 window and characters that you type while the VDT2 window is active are sent to the designated terminal port. In previous versions of VDT, which supported only one open port at a time, the command "VDT2 line=1" set the open port to online. Because VDT2 can now open multiple ports simultaneously, the command "VDT2 line=1" does nothing. This is because VDT2 has no way to know which port to make the terminal port. Instead, you must use the [VDTTerminalPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtterminalport2) operation to designate the terminal port and make it online.

Offline means that characters that come into the terminal port are stored in a buffer for later access and that characters that you type while the VDT2 window is active are not sent to the terminal port. The command "VDT2 line=0" sets the terminal port to off line and is equivalent to the more modern "VDTTerminalPort2 None" command.

The VDT2 operation does not open the port if it is not already open. It does save the settings to be used when the port is opened later. You can open the port explicitly using [VDTOpenPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtopenport2) or you can allow the port to be opened automatically the first time you execute a command, such as VDTRead2 or VDTWrite2, that needs to read data from or write data to the port. See [Opening and Closing Ports](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#opening-and-closing-ports) for details.



<div className="command-signature">

## <strong>VDTGetPortList2</strong>  [ /SCAN ] {#vdtgetportlist2}

</div>

Returns a semicolon-separated list of serial port names in the string variable S_VDT.

### *Flags* {#vdtgetportlist2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SCAN</span> | /SCAN was added in VDT2 version 2.20 to provide a way to adapt if serial ports are added or removed from the machine while Igor is running. |

### *Details* {#vdtgetportlist2-details}
If /SCAN is omitted, VDTGetPortList2 returns a semicolon-separated list of the ports available when Igor was launched or the last time VDT2 resetPorts was executed. This is the normal use of VDTGetPortList2.

If /SCAN is present, VDTGetPortList2 returns a semicolon-separated list of the ports currently available on the machine. See [Detecting Serial Port Hardware Changes](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#detecting-serial-port-hardware-changes) for details.


<div className="command-signature">

## <strong>VDTOpenPort2</strong>  <em>portName</em> {#vdtopenport2}

</div>

Opens the named port, preparing it for use. If the port is already open, VDTOpenPort2 does nothing.

If the port name is not a standard Igor name then you must quote it with single quotes.

### *Parameters* {#vdtopenport2-parameters}
See [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations) for information on port names.

### *Details* {#vdtopenport2-details}
It is not really necessary to call VDTOpenPort2 because VDT2 will automatically open the port if you try to use it either as a dumb terminal via the VDT2 window or via VDT2 command line operations. See [Opening and Closing Ports](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#opening-and-closing-ports) for details.



<div className="command-signature">

## <strong>VDTClosePort2</strong>  <em>portName</em> {#vdtcloseport2}

</div>

Closes the named port, freeing it for use by another program. If the port is already closed, VDTClosePort2 does nothing.

If the port name is not a standard Igor name then you must quote it with single quotes.

### *Parameters* {#vdtcloseport2-parameters}
See [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations) for information on port names.

### *Details* {#vdtcloseport2-details}
It is not really necessary to call VDTClosePort2 because VDT2 will automatically close the port when you quit Igor. See [Opening and Closing Ports](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#opening-and-closing-ports) for details.


<div className="command-signature">

## <strong>VDTOperationsPort2</strong>  [<em>portName</em> ] {#vdtoperationsport2}

</div>

Designates a port as the port to use for command line operations, if you provide a port name. Reports which port is designated as the operations port.

If the port name is not a standard Igor name then you must quote it with single quotes.

### *Parameters* {#vdtoperationsport2-parameters}
If you provide a port name, then VDTOperationsPort2 sets the operations port.

See [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations) for information on port names.

If you specify an existing port, VDTOperationsPort2 designates the port as the operations port.

If you specify None, VDTOperationsPort2 sets the operations port to off line.

### *Details* {#vdtoperationsport2-details}
See [The Terminal Port and the Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-terminal-port-and-the-operations-port) for a discussion of the functions of the operations port.

Whether you provide a port name or not, VDTOperationsPort2 sets the string variable S_VDT to contain the name of the previously designated operations port. This will be something like Printer, Modem, COM1, COM2 or None if no terminal port is selected.


<div className="command-signature">

## <strong>VDTTerminalPort2</strong>  [<em>portName</em> ] {#vdtterminalport2}

</div>

Designates a port as the port to use for terminal functions, if you provide a port name. Reports which port is designated as the terminal port.

If the port name is not a standard Igor name then you must quote it with single quotes.

### *Parameters* {#vdtterminalport2-parameters}
If you provide a port name, then VDTTerminalPort2 sets the terminal port.

See [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations) for information on port names.

If you specify an existing port, VDTTerminalPort2 designates the port as the terminal port.

If you specify None, VDTTerminalPort2 sets the terminal port to "off line".

### *Details* {#vdtterminalport2-details}
See [The Terminal Port and the Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-terminal-port-and-the-operations-port) for a discussion of the functions of the terminal port.

Whether you provide a port name or not, VDTTerminalPort2 sets the string variable S_VDT to contain the name of the previously designated terminal port. This will be something like Printer, Modem, COM1, COM2 or None if no terminal port is selected.


<div className="command-signature">

## <strong>VDTGetStatus2</strong>  [/P=<em>portName</em> ] <em>channelNumber</em>, <em>whichStatus</em>, <em>options</em> {#vdtgetstatus2}

</div>

Returns information regarding the state of the operations port, such as error status. This is intended as a diagnostic aid when communications is not working and is usually not needed.

The status value is always returned via the Igor variable V_VDT.

The information which VDTGetStatus2 returns depends on the information available from the serial driver. This varies quite a but from one operating system to another. As a result, most of the capabilities of VDTGetStatus2 are platform-dependent and should be avoided. The only form which you can rely on on all operating systems is:

```igor
// Check if characters wait to be read in the input buffer
VDTGetStatus2 0, 0, 0
```

This sets the variable V_VDT to the number of characters in the input buffer.

The other features of VDTGetStatus2 are platform-dependent as noted below. They should be avoided.

Note that most problems in serial communications come because of one of the following problems.

You don't have a firm understanding of the characters (including terminator and separator characters) that the device expects to receive and sends. See the documentation for the device and [Terminators In Write Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-write-operations).

You don't have a firm understanding of the characters (including terminator and separator characters) that VDT2 expects to receive and sends. See [Terminators In Read Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-read-operations) and the description of the VDT2 operation that you are using (e.g., [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2)).

VDT2 and the device are not using the same serial port parameters (e.g., baud rate).

You have data overruns because the VDT2 serial buffer is not big enough, because handshaking is not working (see [Handshaking](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#handshaking)) or because the cable is not correct (see [Serial Port Pinout](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#serial-port-pinout)).

### *Flags* {#vdtgetstatus2-flags}

|  |  |
| --- | --- |
| /P=*portName* | If you specify /P=*portName*, VDTGetStatus2 operates on the named port.
|  | If you omit /P=*portName*, VDTGetStatus2 operates on the current operations port. If you have not selected an operations port, VDTGetStatus2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTGetStatus2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTGetStatus2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |

### *Parameters* {#vdtgetstatus2-parameters}

|  |  |
| --- | --- |
| channelNumber | Windows does not support independent status for input and output so this parameter is irrelevant and the status returned is the combined status of the input and output channels. The value has meaning only for some of the whichStatus codes.
| whichStatus | Specifies what kind of status information you want. Codes 0 and 1 are the most useful. The remaining codes are included for completeness but are of little use, except possibly for a serial communications expert. |
|  | 0: Sets V_VDT to the number of characters received via the serial port and which are waiting to be read. Regardless of the channelNumber parameter, this applies to the input channel only. |
|  | 1: Sets V_VDT to the error status of the specified channel. Interpretation of this value is discussed below. |
|  | 2: Obsolete |
|  | 3: Sets V_VDT to the truth that a read is pending. This is meaningful for the input channel only. This should always be false because VDT2 does synchronous reads only. This means that VDT2 will not return to IGOR until the read operation is completed. |
|  | 4: Sets V_VDT to the truth that a write is pending. This is meaningful for the output channel only. This should always be false because VDT2 does synchronous writes only. This means that VDT2 will not return to IGOR until the write operation is completed. |
|  | 5: Sets V_VDT to the truth that the serial driver has suspended output because the Clear-To-Send (CTS) line is negated. This is meaningful for the output channel only. When hardware handshaking is used, the receiver negates the CTS line when its input buffer is nearly full to tell the sender to stop sending data. |
|  | 6: Obsolete. |
| options | This parameter has meaning only if whichStatus is 1 (get error status). For other whichStatus codes, pass 0 for this parameter. |
|  | If whichStatus is 1 and options is 1, VDTGetStatus2 clears the error status for the channel in question. If options is 0, VDTGetStatus2 does not clear the error status, so if any error status bits are set, subsequent calls to VDTGetStatus2 will still see the same error bits. |

### *Details* {#vdtgetstatus2-details}
The meaning of the V_VDT value for the error status (whichStatus==1) is a follows:


|  |  |
| --- | --- |
| Bit 0: | A software overrun error occurred. A software overrun occurs if the serial driver input buffer is filled up and more characters arrive from the sender. Possible solutions are to increase the size of the serial buffer (using the "VDT2 buffer" command or the VDT2 Settings dialog), to use hardware or XON/XOFF handshaking, or to reduce the baud rate.
|  | To test bit 0, use "if ((V_VDT %& 1) != 0)". |
| Bit 3: | The break signal was asserted. The receiver detects a break signal occurs if the serial cable is disconnected, if the sender is powered off, or if some other event causes a disruption in the connection. |
|  | To test bit 3, use "if ((V_VDT %& 8) != 0)". |
| Bit 4: | A parity error occurred. The most likely cause for a parity error is that you have not configured the VDT2 parity setting to match the parity used by the device that you are talking to. A much less likely cause is noise on the serial cable. |
|  | To test bit 4, use "if ((V_VDT %& 16) != 0)". |
| Bit 5: | A hardware overrun error occurred. This means that the receiver has received a character before the preceding character was read by the serial driver. The most likely cause for this is that something happened, such as formatting a floppy disk or some other high priority hardware event, so that the serial driver did not get a chance to run for too long a period. A less likely possiblity is a bug in the serial driver or some other software conflict. |
|  | To test bit 5, use "if ((V_VDT %& 32) != 0)". |
| Bit 6: | A framing error occurred. The most likely cause for a framing error is that you have not configured the VDT2 baud rate or stop bits settings to match the baud rate and stop bits used by the device that you are talking to. A much less likely cause is noise on the serial cable. |
|  | To test bit 6, use "if ((V_VDT %& 64) != 0)". |
| Bit 8: | If set, indicates that a "parallel device not selected" error occurred. |
|  | To test bit 8, use "if ((V_VDT %& 256) != 0)". |
| Bit 9: | If set, indicates that a "general I/O" error occurred. |
|  | To test bit 9, use "if ((V_VDT %& 512) != 0)". |
| Bit 10: | If set, indicates that a "requested mode not supported" error occurred. |
|  | To test bit 10, use "if ((V_VDT %& 1024) != 0)". |
| Bit 11: | If set, indicates that a "parallel device out of paper" error occurred. |
|  | To test bit 11, use "if ((V_VDT %& 2048) != 0)". |
| Bit 12: | If set, indicates that a "parallel device timed out" error occurred. |
|  | To test bit 12, use "if ((V_VDT %& 4096) != 0)". |
| Bit 13: | If set, indicates that a "output buffer overrun" error occurred. |
|  | To test bit 13, use "if ((V_VDT %& 8192) != 0)". |

The error status codes for the input and output channels are accumulated until something happens to clear them. This means that if an error condition occurs, the corresponding bit in the error status code will be set and it will stay set until the error status code is cleared. The error status codes are cleared when:

- You call VDTGetStatus2 with whichStatus==1 and options==1.
- You execute "VDT2 KillIO".
- You change the serial port parameters, such as baud rate, stop bits, etc.
- You abort an interactive I/O operation (send file, receive file, send selected text).

The reason for not clearing the error status code each time you read it is that you may have more than one place in your program that needs to check for serial port errors.



<div className="command-signature">

## <strong>VDTRead2</strong>  [ /N=<em>n</em> /O=<em>n</em> /P=<em>portName</em> /Q /T=<em>termStr</em> ] <em>variableName</em> [ , <em>variableName</em> ] {#vdtread2}

</div>

Reads characters from the operations port into the string or numeric variables specified as arguments.

### *Parameters* {#vdtread2-parameters}
When used from the command line or in a macro, *variableName*  must be the name of a local or global variable in the current data folder. When used from a user function, *variableName*  can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

### *Flags* {#vdtread2-flags}

|  |  |
| --- | --- |
| /N=n | n is maximum number of characters to read for a particular string or variable.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTRead2 operates on the named port. |
|  | If you omit /P=*portName*, VDTRead2 operates on the current operations port. If you have not selected an operations port, VDTRead2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTRead2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTRead2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Tells VDTRead2 that you want no error message in the event of a timeout. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr*  is the terminator string expression and specifies which character or characters will terminate the read. |

### *Details* {#vdtread2-details}
VDTRead2 sets the variable V_VDT to the number of items read. You can use V_VDT to tell if the operation completed successfully or timed out.

Here is a discussion of how VDTRead2 goes about trying to read into its argument list.

If the /T=*termStr*  flag is present, it specifies a terminator character or characters. The terminator is the character that ends input into a string or numeric variable. The default is /T=",\r\t" so that a comma, carriage return or tab ends a read.

/N=n is an optional maximum number of characters to be read into a string or numeric variable. The default is /N=255 for a string variable and /N=16 for a numeric variable.

If /Q is present and a timeout occurs, VDTRead2 aborts after setting the variable V_VDT to the number of items read but does not put up an error message and does not halt procedure execution. This allows a procedure to handle a timeout in its own way.

If a timeout or abort (Ctrl-Break) occurs while reading a string, any characters received prior to the timeout or abort are stored in the string.

When reading a string, VDTRead2 reads until the next terminator is encountered. The terminator is not put into the string. The next read starts after the terminator.

Do not use VDTRead2 to read binary data or anything that contains a null character (ASCII 0). Use [VDTReadBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinary2) instead.

When reading a numeric variable, VDTRead2 first skips any non-numeric characters and then reads a number. If the *variableName*  refers to a complex variable, VDTRead2 reads two numbers from the device and stores both the real and imaginary parts of the variable.

### *Example* {#example}

```igor
VDTRead2/O=10 v1, s1, v2
```

Reads from the serial port into variable v1, string variable s1 and variable v2. If 10 seconds elapses while VDTRead2 is trying to read a character, it aborts with a timeout error.

### *See Also* {#see-also}
[Terminators In Read Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-read-operations)


<div className="command-signature">

## <strong>VDTReadWave2</strong>  [ /R=[ <em>start</em> , <em>end</em>  ] /T=<em>termStr</em>  /O=<em>n</em> /P=<em>portName</em> /N=<em>n</em> /Q ] <em>waveName</em>  [, <em>waveName</em> ] {#vdtreadwave2}

</div>

Reads data from device into waves.

### *Parameters* {#vdtreadwave2-parameters}
The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and VDTReadWave2 reads two values for each wave point.

Assuming the the /R flag is omitted, data is stored into point 0 of each wave, then point 1 of each wave, and so on.

### *Flags* {#vdtreadwave2-flags}

|  |  |
| --- | --- |
| /N=n | n is maximum number of characters to read for each value.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTReadWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTReadWave2 operates on the current operations port. If you have not selected an operations port, VDTReadWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTReadWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTReadWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/R = [ *start*, *end*  ]</span> |  |
|  | Specifies the starting and ending point numbers for a range of the waves that you want to read data into. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr*  is a string or string expression specifying characters which terminate a read. |

### *Details* {#vdtreadwave2-details}
If the /R flag is omitted, VDTReadWave2 stores values in point 0 through point n-1 where n is the number of points in the first wave.

VDTReadWave2 sets the variable V_VDT to the number of  individual numbers read.

VDTReadWave2 works with 64-bit integer data but is limited to 53 bits of precision. See [VDT2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#vdt2-64-bit-integer-limitations) for details.

### *Example* {#vdtreadwave2-example}

```igor
VDTReadWave2 wave1, wave2, wave3
```

This reads from the device into wave1, wave2 and wave3. It reads until it has put a value in each point of each wave.

### *See Also* {#vdtreadwave2-see-also}
[Terminators In Read Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-read-operations)


<div className="command-signature">

## <strong>VDTReadBinary2</strong>   [ /B /O=<em>n</em> /P=<em>portName</em> /Q /S=<em>strLen</em>  /T=<em>termStr</em>  /TYPE=<em>type</em>  /Y={<em>offset</em> , <em>multiplier</em> } ] <em>variableName</em>  [,<em>variableName</em> ] {#vdtreadbinary2}

</div>

Reads binary data into Igor strings and variables. The binary data can be read as integers of one, two or four bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

### *Parameters* {#vdtreadbinary2-parameters}
When used from the command line or in a macro, *variableName*  must be the name of a local or global variable in the current data folder. When used from a user function, *variableName*  can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

If /S=*strLen*  is used, the arguments are expected to be string variables and bytes are read up to *strLen*  bytes or until a byte specified by /T=*termStr*  is read.

If /S=*strLen*  is NOT used, the arguments are expected to be numeric variables into which data is to be read.

Reading binary data into strings is used mostly to skip a number of bytes or until a certain byte is received. To read actual ASCII data into strings, use [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2) instead of VDTReadBinary2.

### *Flags* {#vdtreadbinary2-flags}

|  |  |
| --- | --- |
| /B | Indicates that multi-byte data is to be received low-byte-first. Without /B, multi-byte data is received high-byte-first. This flag affects receiving of numeric data only, not string data.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTReadBinary2 operates on the named port. |
|  | If you omit /P=*portName*, VDTReadBinary2 operates on the current operations port. If you have not selected an operations port, VDTReadBinary2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTReadBinary2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTReadBinary2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/S = *strLen*</span> | If present, the variables are expected to be string variables. Bytes are read up to *strLen*  bytes or until a byte specified by /T=*termStr*  is read. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | Specifies a terminator character when reading bytes into strings. The default value is "" (no terminators). The read will be faster if no terminators are specified. This has no effect when reading into numeric variables. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type* . The default value is 8 (signed byte). |
| <span class="table-cell-nowrap">/Y = {o, m}</span> | o is offset, m is multiplier. /Y is used to scale integer data into real numbers. output data = (input data + offset) * multiplier. |

### *Details* {#vdtreadbinary2-details}
If a numeric variable is complex, VDTReadBinary2 reads two values for that variable.

VDTReadBinary2 sets the variable V_VDT to the number of  items read.

If a timeout or abort (Ctrl-Break on Windows) occurs while reading a string, any characters received prior to the timeout or abort are stored in the string.

VDTReadBinary2 works with 64-bit integer data but is limited to 53 bits of precision. See [VDT2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#vdt2-64-bit-integer-limitations) for details.

### *Examples* {#examples}

This command reads 10 bytes into string variable str1.

```igor
String str1
VDTReadBinary2/S=10 str1
```

This command reads two byte signed integer binary numbers into the numeric variables v0 and v1.

```igor
Variable v0, v1
VDTReadBinary2/TYPE=(0x10) v0, v1
```

This command reads four byte IEEE single-precision floating point binary numbers into v0 and v1. Normally, the high order byte of each number would be expected first but because /B is used, in this example, the low order byte is expected first.

```igor
Variable v0, v1
VDTReadBinary2/TYPE=2/B v0, v1
```


<div className="command-signature">

## <strong>VDTReadBinaryWave2</strong>  [ /B /O=<em>n</em> /P=<em>portName</em> /Q /TYPE=<em>type</em>  /Y={<em>offset</em> , <em>multiplier</em> } ]  <em>waveName</em>  [,<em>waveName</em>] {#vdtreadbinarywave2}

</div>

Reads binary data into the waves named in wavelist. The waves can be of any numeric data type, real or complex.

### *Flags* {#vdtreadbinarywave2-flags}

|  |  |
| --- | --- |
| /B | Indicates that multi-byte data is to be received low-byte-first. Without /B, multi-byte data is received high-byte-first. This flag affects receiving of numeric data only, not string data.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTReadBinaryWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTReadBinaryWave2 operates on the current operations port. If you have not selected an operations port, VDTReadBinaryWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTReadBinaryWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTReadBinaryWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type* . The default value is 8 (signed byte). |
| /Y={*o*, *m*} | *o* is offset, *m* is multiplier. /Y is used to scale integer data into real numbers. 
|  | <code class="igor">output data = (input data + offset) * multiplier</code> |

### *Details* {#vdtreadbinarywave2-details}
If multiple waves are specified, all of the values for the first wave are read, followed by all of the values for the second wave, and so on.

If a wave is complex, VDTReadBinaryWave2 reads two values for each point in that wave. This is true regardless of the /TYPE=*type*  flag.

VDTReadBinaryWave2 sets the variable V_VDT to the number of  waves (not points) read.

VDTReadBinaryWave2 works with 64-bit integer data but is limited to 53 bits of precision. See [VDT2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#vdt2-64-bit-integer-limitations) for details.

### *Examples* {#vdtreadbinarywave2-examples}

This command reads two byte signed integer binary numbers into each point of wave.

```igor
VDTReadBinaryWave2/TYPE=(0x10) wave0
```

This command reads a four byte signed integer binary number into each point of wave0, wave1 and wave2. All of wave0 is read first, then all of wave1, then all of wave2.

```igor
VDTReadBinaryWave2/TYPE=(0x20) wave0, wave1, wave2
```

This command reads eight-byte IEEE floating point binary numbers into wave0. Because /B is used the low order byte of each point is expected first.

```igor
VDTReadBinaryWave2/B/TYPE=4 wave0
```

This command reads two-byte signed integer binary numbers into each point of wave. Then it adds 0 to each point and multiplies by .25. This would be used to scale integer data where 1 count represents .25 volts, for example.

```igor
VDTReadBinaryWave2/TYPE=(0x10)/Y={0,0.25} wave0
```

<div className="command-signature">

## <strong>VDTReadHex2</strong>  [ /W /L /O=<em>n</em> /P=<em>portName</em> /Q ] <em>variableName</em>  [,<em>variableName</em> ] {#vdtreadhex2}

</div>

Reads hex data from the operations port into the specified numeric variables.

### *Flags* {#vdtreadhex2-flags}

|  |  |
| --- | --- |
| /W | Reads 4 hex digits and treats them as 16 bit unsigned integer.
| <span class="table-cell-nowrap">/L</span> | Reads 8 hex digits and treats them as 32 bit unsigned integer. |
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTReadHex2 operates on the named port. |
|  | If you omit /P=*portName*, VDTReadHex2 operates on the current operations port. If you have not selected an operations port, VDTReadHex2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTReadHex2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTReadHex2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

If neither /W nor /L are present, it reads 2 hex digits and treats them as an 8 bit unsigned integer.

### *Details* {#vdtreadhex2-details}
Incoming values are treated as unsigned. That is, if the data being read is "FF", this is interpreted as 0xFF (255 decimal), not -1.

If a numeric variable is complex, VDTReadHex2 reads two values for that variable.

VDTReadHex2 sets the variable V_VDT to the number of  numbers read.


<div className="command-signature">

## <strong>VDTReadHexWave2</strong>  [ /W /L /O=<em>n</em> /P=<em>portName</em> /Q ] <em>waveName</em>  [,<em>waveName</em> ] {#vdtreadhexwave2}

</div>

Reads hex data from the operations port into the specified waves.

### *Flags* {#vdtreadhexwave2-flags}

|  |  |
| --- | --- |
| /W | Reads 4 hex digits and treats them as 16 bit unsigned integer.
| <span class="table-cell-nowrap">/L</span> | Reads 8 hex digits and treats them as 32 bit unsigned integer. |
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTReadHexWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTReadHexWave2 operates on the current operations port. If you have not selected an operations port, VDTReadHexWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTReadHexWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTReadHexWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

If neither /W nor /L are present, it reads 2 hex digits and treats them as an 8 bit unsigned integer.

Incoming values are treated as unsigned if the wave is an unsigned integer type. Otherwise, incoming values are treated as signed.

VDTReadHexWave2 works with any type of numeric wave.

If the wave is real, one hex number is read for each point in the wave. If the wave is complex, two hex numbers are read for each point in the wave.

VDTReadHexWave2 sets the variable V_VDT to the number of  numbers read.



<div className="command-signature">

## <strong>VDTWrite2</strong>  [ /O=<em>n</em> /P=<em>portName</em> /Q ] <em>str</em> {#vdtwrite2}

</div>

Transmits the contents of the string argument via the operations port.

### *Flags* {#vdtwrite2-flags}

|  |  |
| --- | --- |
| /O=n | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout.
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWrite2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWrite2 operates on the current operations port. If you have not selected an operations port, VDTWrite2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWrite2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWrite2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Tells VDTWrite2 that you want no error message in the event of a timeout. |

### *Details* {#vdtwrite2-details}
VDTWrite2 sets the variable V_VDT to 1 if the write succeeded or to zero otherwise.

VDTWrite2 does not automatically send a terminator character, such as carraige return or linefeed. You must explicitly specify it if your instrument requires it, as many do. See [Terminators In Write Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-write-operations) for details.

### *Examples* {#vdtwrite2-examples}

This command transmits a greeting followed by a carriage return and linefeed.

```igor
VDTWrite2 "Hello" + "\r\n"
```

This example transmits the contents of variable v1, the sine of .5 radians and the contents of point 0 of wave1, separated by tabs with a carriage return and linefeed at the end.

```igor
String str
sprintf str, "%g\t%g\t%g\r\n", v1, sin(.5), wave1[0]
VDTWrite2 str
```

### *See Also* {#vdtwrite2-see-also}
[Terminators In Write Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-write-operations)


<div className="command-signature">

## <strong>VDTWriteWave2</strong>  [ /F={<em>numericFormatStr</em>, <em>leaderStr</em>, <em>separatorStr</em>, <em>terminatorStr</em> } /O=<em>n</em> /P=<em>portName</em> /Q  /R=[ <em>start</em> , <em>end</em>  ] ] <em>waveName</em>  [,<em>waveName</em>] {#vdtwritewave2}

</div>

Transmits contents of wave or waves as text.

The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and VDTWriteWave2 writes two values for each wave point.

### *Parameters* {#vdtwritewave2-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F = {*numericFormatStr, leaderStr, separatorStr, terminatorStr* }</span> |  |
|  | *numericFormatStr*  is the numeric format string used to generate the output text for each numeric wave point. VDTWriteWave2 passes this string to the C sprintf function. The default value is "%g". |
|  | Only numeric formats are allowed. *numericFormatStr*  must end with a numeric conversion character. See [Printf](/igorpro/commands/printf.md) for details on formats. |
|  | *leaderStr*  is text that is inserted at the start of each line of data. The default is "". |
|  | *separatorStr*  is text that is inserted between each pair of points. The default is "\\t" (tab). |
|  | *terminatorStr*  is text that is written at the end of each line of data. The default is "\\r" (carriage-return). |
| <span class="table-cell-nowrap">/R = [start,end]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to write data from. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWriteWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWriteWave2 operates on the current operations port. If you have not selected an operations port, VDTWriteWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWriteWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWriteWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

### *Details* {#vdtwritewave2-details}
If the /R flag is omitted, VDTWriteWave2 writes values for point 0 through point n-1 where n is the number of points in the first wave.

VDTWriteWave2 sets the variable V_VDT to the number of individual numbers written.

VDTWriteWave2 works with 64-bit integer data but is limited to 53 bits of precision. See [VDT2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#vdt2-64-bit-integer-limitations) for details.

### *Examples* {#vdtwritewave2-examples}

This command transmits contents of the waves as text, using 15 digits of precision, with a comma between numbers and CRLF at the end of each line.

```igor
VDTWriteWave2/F={"%.15g", "", ",", "\r\n"} wave1,wave2,wave3
```

### *See Also* {#vdtwritewave2-see-also}
[Terminators In Write Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-write-operations)


<div className="command-signature">

## <strong>VDTWriteBinary2</strong>  [ /B /O=<em>n</em> /P=<em>portName</em> /Q /TYPE=<em>type</em>  ] <em>argument</em>  [,<em>argument</em> ] {#vdtwritebinary2}

</div>

Transmits contents of the argument or arguments as binary data. The binary data can be sent as integers of one, two or four bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

### *Parameters* {#vdtwritebinary2-parameters}
*argument*  is a numeric expression.

### *Flags* {#vdtwritebinary2-flags}

|  |  |
| --- | --- |
| /B | Indicates that multi-byte data is to be sent low-byte-first. Without /B, multi-byte data is sent high-byte-first.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWriteBinary2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWriteBinary2 operates on the current operations port. If you have not selected an operations port, VDTWriteBinary2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWriteBinary2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWriteBinary2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type* . The default value is 8 (signed byte). |

### *Details* {#vdtwritebinary2-details}
VDTWriteBinary2 sets the variable V_VDT to the number of  items written.

VDTWriteBinary2 can not transmit strings. Use [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) for that. VDTWriteBinary2 can also not transmit complex values.

VDTWriteBinary2 works with 64-bit integer data but is limited to 53 bits of precision. See [VDT2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#vdt2-64-bit-integer-limitations) for details.

### *Examples* {#vdtwritebinary2-examples}

This command writes 123 and -456 as two byte signed integer binary numbers. The high order byte of each number is transfered first.

```igor
VDTWriteBinary2/TYPE=(0x10) 123, -456
```

This command writes 2*PI and -PI/2 as 32-bit IEEE floating point binary numbers. Normally, the high order byte of each number would be transfered first but because /B is used, in this example, the low order byte is transfered first.

```igor
VDTWriteBinary2/TYPE=2/B 2*PI, -PI/2
```


<div className="command-signature">

## <strong>VDTWriteBinaryWave2</strong>  [ /B /O=<em>n</em> /P=<em>portName</em> /Q /TYPE=<em>type</em>  ] <em>waveName</em>  [,<em>waveName</em>] {#vdtwritebinarywave2}

</div>

Writes binary data from the waves named in wavelist. The waves can be of any numeric data type.

### *Flags* {#vdtwritebinarywave2-flags}

|  |  |
| --- | --- |
| /B | Indicates that multi-byte data is to be sent low-byte-first. Without /B, multi-byte data is sent high-byte-first.
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWriteBinaryWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWriteBinaryWave2 operates on the current operations port. If you have not selected an operations port, VDTWriteBinaryWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWriteBinaryWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWriteBinaryWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |

### *Details* {#vdtwritebinarywave2-details}
The waves can be of any numeric data type, real or complex.

If multiple waves are specified, all of the values for the first wave are written, followed by all of the values for the second wave, and so on.

If a wave is complex, VDTWriteBinaryWave2 writes two values for each point in that wave. This is true regardless of the /TYPE=*type*  flag.

VDTWriteBinaryWave2 sets the variable V_VDT to the number of  waves (not points) written.

### *Examples* {#vdtwritebinarywave2-examples}

This command writes each point of wave0 as a two-byte signed integer binary number.

```igor
VDTWriteBinaryWave2/TYPE=(0x10) wave0
```

This command writes all of wave0 as a four-byte signed integer binary number, followed by all of wave1 and then all of wave2.

```igor
VDTWriteBinaryWave2/TYPE=(0x20) wave0, wave1, wave2
```

This command writes each point of wave0 as a 32-bit IEEE floating point binary number. Because /B is used the low order byte of each point is written first.

```igor
VDTWriteBinaryWave2/TYPE=2/B wave0
```


<div className="command-signature">

## <strong>VDTWriteHex2</strong>  [ /W /L /O=<em>n</em> /P=<em>portName</em> /Q ]  <em>argument</em>  [,<em>argument</em> ] {#vdtwritehex2}

</div>

Writes each numeric argument as hexadecimal.

### *Flags* {#vdtwritehex2-flags}

|  |  |
| --- | --- |
| /W | Writes 4 hex digits.
| <span class="table-cell-nowrap">/L</span> | Writes 8 hex digits. |
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWriteHex2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWriteHex2 operates on the current operations port. If you have not selected an operations port, VDTWriteHex2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWriteHex2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWriteHex2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

If neither /W nor /L are present, it writes 2 hex digits.

When writing 2 hex digits, values of v in the range -128 to 255 are valid.  If v is not in this range, the output is undefined.

When writing 4 hex digits, values of v in the range -32768 to 65535 are valid.  If v is not in this range, the output is undefined.

When writing 8 hex digits, values of v in the range -2147483648 to 4294967295 are valid.  If v is not in this range, the output is undefined.



<div className="command-signature">

## <strong>VDTWriteHexWave2</strong>  [ /F={<em>leaderStr</em>, <em>separatorStr</em>, <em>terminatorStr</em> } /L /O=<em>n</em> /P=<em>portName</em> /Q /R=[ <em>start</em> , <em>end</em>  ] /W ] <em>waveName</em>  [,<em>waveName</em>] {#vdtwritehexwave2}

</div>

Transmits contents of wave or waves as hexadecimal.

The waves must be 1-dimensional numeric waves. For complex waves,  VDTWriteHexWave2 writes two values for each wave point.

### *Parameters* {#vdtwritehexwave2-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F = {*leaderStr, separatorStr, terminatorStr* }</span> |  |
|  | *leaderStr*  is text that is inserted at the start of each line of data. The default is "". |
|  | *separatorStr*  is text that is inserted between each pair of points. The default is "". |
|  | *terminatorStr*  is text that is written at the end of each line of data. The default is "". |
| <span class="table-cell-nowrap">/L</span> | Writes 8 hex digits and treats them as 32 bit unsigned integer. |
| <span class="table-cell-nowrap">/R = [start,end]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to write data from. |
| <span class="table-cell-nowrap">/O = n</span> | n is a timeout value in seconds. If entire operation can't be completed in n seconds, it aborts. If you omit /O or if n is zero, there is no timeout. |
| <span class="table-cell-nowrap">/P = *portName*</span> | If you specify /P=*portName*, VDTWriteHexWave2 operates on the named port. |
|  | If you omit /P=*portName*, VDTWriteHexWave2 operates on the current operations port. If you have not selected an operations port, VDTWriteHexWave2 returns an error. |
|  | If *portName* is "", /P is ignored as if it were omitted altogether. |
|  | If the port name is not a standard Igor name then you must quote it with single quotes. |
|  | When calling VDTWriteHexWave2 from a preemptive thread, you must include /P=*portName*. |
|  | The /P=*portName* flag for VDTWriteHexWave2 was added in VDT2 version 3.00, shipped with Igor Pro 8.05. |
|  | For background information, see [Port Name Usage In VDT2 Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#port-name-usage-in-vdt2-operations), [The Operations Port](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#the-operations-port), and [Specifying the Operation Port Using the /P Flag](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#specifying-the-operation-port-using-the-p-flag). |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/W</span> | Writes 4 hex digits and treats them as 16 bit unsigned integer. |

If neither /W nor /L are present, it writes 2 hex digits per number and treats them as an 8 bit unsigned integer.

### *Details* {#vdtwritehexwave2-details}
VDTWriteHexWave2 works with any type of numeric wave.

If the wave is real, one hex number is written for each point in the wave. If the wave is complex, two hex numbers are written for each point in the wave.

If the /R flag is omitted, VDTWriteHexWave2 writes values for point 0 through point n-1 where n is the number of points in the first wave.

VDTWriteHexWave2 sets the variable V_VDT to the number of individual numbers written.

### *See Also* {#vdtwritehexwave2-see-also}
[Terminators In Write Operations](/igorpro/extensions/data-acquisition/vdt2/vdt2-serial-port-support.md#terminators-in-write-operations)