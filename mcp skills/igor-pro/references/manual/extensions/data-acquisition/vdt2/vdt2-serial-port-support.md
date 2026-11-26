---
description: "VDT2 is an Igor extension that implements a dumb terminal emulator (VDT stands for \"Very Dumb Terminal\")."
slug: /extensions/data-acquisition/vdt2/vdt2-serial-port-support
---

VDT2 is an Igor extension that implements a dumb terminal emulator (VDT stands for "Very Dumb Terminal"). VDT2 also allows you to control serial port communications from Igor procedures. The main use for VDT2 is to communicate with an instrument or another computer using the operations that VDT2 adds to Igor.

Source code for VDT2 is supplied with the Igor XOP Toolkit.

This version of VDT2 requires Igor Pro 8.00 or later because it supports long object names and paths.

VDT2 sprang from VDT, an earlier XOP that is no longer shipped as of Igor Pro 7. If you are converting procedures that use VDT to use VDT2, see [Changes in VDT2 Relative to VDT](#changes-in-vdt2-relative-to-vdt) for an explanation of the differences.

VDT2 adds a submenu to Igor's Misc menu. It adds a full featured text window with scrolling, find, replace, undo and other amenities. It also adds a number of command line operations to Igor. These operations allow you to configure a port and to communicate with it from the command line or from an Igor procedure. You can use the operations to control an instrument or to communicate with another computer.

To activate the 64-bit version of VDT2, create a shortcut for VDT2-64.xop file, put the shortcut in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details) and then launch Igor. A VDT2 item will be added to Igor's Misc menu.

The VDT2 Settings dialog, accessed via the `Misc→VDT2` submenu, allows you to open and close specific serial ports, designate a given serial port for terminal or operation use, and set serial port parameters such as baud rate, number of stop bits, and so on.

The simplest thing you can do with VDT2 is to use it as a dumb terminal. First connect your computer to another device and make sure that the serial parameters on both ends are compatible. Next designate the port as the terminal port, using the Terminal Port submenu in the VDT2 menu. Next display the VDT2 terminal window by choosing `Misc→VDT2→Open VDT2 Window`. Now you can type in the VDT2 window. Your keystrokes will be transmitted to the other device. If the other device sends characters to the computer, you will see them in the VDT2 window.

## VDT2 Hardware Issues {#vdt2-hardware-issues}

Many manufacturers sell USB-to-serial adapters but they all use a small number of underlying chipsets. Users have reported problems using some chipsets and success using others. The symptom is that reads time out under some circumstances. The cause is unknown though we suspect that it is related to the size of the buffer in the chipset.
Because of this problem we strongly recommend that you use a serial adapter that is based on the FTDI chipset which has been reported to work without problems. These are available from:
	[http://www.gearmo.com/product-category/usb-to-serial-adapters/](http://www.gearmo.com/product-category/usb-to-serial-adapters/)

	[http://www.serialgear.com/usb-to-serial-adapter.html](http://www.serialgear.com/usb-to-serial-adapter.html)

	[http://www.usconverters.com/](http://www.usconverters.com/)

Make sure to purchase an adapter that uses an FTDI chipset.

Problems have been reported with adapters from Sabrent and CablesToGo.

:::note
**Update**: In August of 2015 we successfully used adapters from Sabrent. The adapters use the Prolific "PL2303TA" chip. We used version the Prolific serial driver for Macintosh and the Prolific serial driver for Windows. Operation was reliable up to 460800 baud, unreliable at 921600 baud. We updated to the latest driver in 2018 and it appeared to work on Mac OS 10.13 and Windows 10.
:::

:::note
**Update**: In August of 2020 we successfully used an adapter from DTech on Mac OS 10.14. The adapters use the Prolific "PL2303RA" chip. We successfully ran VDT2 self tests at up to 921600 baud, but you should start with a low baud rate to avoid buffer overrun problems.
:::

## VDT2 Submenu Items {#vdt2-submenu-items}
Here are the items in the VDT2 submenu.

## Open VDT2 Window {#open-vdt2-window}
Opens the VDT2 dumb terminal window.

## VDT2 Settings {#vdt2-settings}
Displays a dialog that allows you to set communications parameters such as baud rate, stop bits, etc.

## Terminal Port {#terminal-port}
Lets you specify which physical port is to be used for dumb terminal functions.

## Save File {#save-file}
Allows you to save the contents of the VDT2 window in a text file.

## Insert File {#insert-file}
Allows you to insert the contents of a text file into the VDT2 window.

## Send File {#send-file}
Using the Send File item, you can instruct VDT2 to send a text file to the designated terminal port. VDT2 will send the entire file unless you select Stop Sending File from the VDT2 menu before the entire file has been sent. The Stop Sending File item appears only after you have instructed VDT2 to send a file.

## Receive File {#receive-file}
Using the Receive File item, you can instruct VDT2 to receive a text file from the designated terminal port. Since VDT2 has no way of knowing when it has received all of the file, you must select Stop Receiving File from the VDT2 menu when the entire file has been transfered. The Stop Receiving File item appears only after you have instructed VDT2 to receive a file.

## Send VDT2 Text {#send-vdt2-text}
The next item says either Send VDT2 Text or Send Selected Text, depending on whether there is text selected in the VDT2 window. It sends text from the VDT2 window to the designated terminal port. VDT2 will send the text unless you select Stop Sending Text from the VDT2 menu before the entire text has been sent. The Stop Sending Text item appears only after you have instructed VDT2 to send text.

## Operations Port {#operations-port}
Lets you specify which physical port is to be used for command line operations.

## Reset Serial Ports {#reset-serial-ports}
If you connect or disconnect a USB-to-serial adapter, you can choose Reset Serial Ports to force VDT2 to rescan for available ports. This also terminates any serial I/O, closes any ports opened by VDT2, and resets VDT2 port settings to default values. See also [Detecting Serial Port Hardware Changes](#detecting-serial-port-hardware-changes).

## Supported VDT2 Ports {#supported-vdt2-ports}
When VDT2 first executes, it determines what serial ports are installed on the machine and displays those ports in the VDT2 Settings dialog, and in the Terminal Port and Operations Port submenus of the VDT2 menu.

If you connect a USB-to-serial adapater after starting VDT2, you can force VDT2 to recognize the new port by choosing [Reset Serial Ports](#reset-serial-ports) from the VDT2 menu.

On Windows, prior to VDT2 version 2.20, if VDT2 was unable to detect any serial ports, it defaulted to COM1...COM8. This was done because ancient versions of Windows did not provide a reliable way to know what serial ports were available. Now, if VDT2 detects no ports when it is started, it lists no ports.

Although Windows documentation suggests that parallel ports should work just like serial ports, we have not been able to get parallel ports to work. Thus LPT1 and LPT2 are not supported by VDT2.

## Port Name Usage In VDT2 Operations {#port-name-usage-in-vdt2-operations}
You can see what ports are available by looking at the VDT2 Settings dialog or via the [VDTGetPortList2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtgetportlist2) operation.

Long ago Macintosh machines had built-in serial ports named Modem and Printer and Windows had built-in serial ports named COM1 through COM3.  On Windows VDT2 translates Modem to COM1 and Printer to COM2. These translations are obsolete and you should not rely on them.

If the name of the port is not a standard Igor name then you must quote the name with single quotes.

## The Terminal Port and the Operations Port {#the-terminal-port-and-the-operations-port}
VDT2 can be used in two ways: as a dumb terminal and to communicate with an instrument (or possibly another computer) under control of procedures that you write. Most likely you are using VDT2 for instrument control. However, while you are establishing communications and writing procedures, you may find it handy to be able to manually communicate with the instrument using the dumb terminal mode.

## The Terminal Port {#the-terminal-port}
You can designate a physical communications port as the "terminal port". This means that this is the port that you are going to use for dumb terminal functions. Dumb-terminal functions include sending characters that you type in the VDT2 window, displaying received characters in the VDT2 window, sending files, and receiving files. You can designate the terminal port using the Terminal Port submenu of the VDT2 menu, using the VDT2 Settings dialog, or using the VDTTerminalPort2 operation. If you do not plan to use VDT2 

## The Operations Port {#the-operations-port}
You can designate a physical communications port as the "operations port". This means that this is the port to be used by VDT2 operations such as [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2), [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2), [VDTReadBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinary2), [VDTWriteBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritebinary2), and so on. You can designate the operations port using the Operations Port submenu of the VDT2 menu, using the VDT2 Settings dialog, or using the [VDTOperationsPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtoperationsport2) operation. If you do not plan to use VDT2 operations, you can leave the operations port set to "Off line".

You can specify the communications port for a particular command using the /P=*portName* flag. This overrides the currently set operations port for that command. See [Specifying the Operation Port Using the /P Flag](#specifying-the-operation-port-using-the-p-flag) for details.

If the terminal port and operations port are set to the same physical port and you invoke an operation that reads or writes characters, VDT2 automatically sets the terminal port to off line. This prevents the dumb terminal emulator from interfering with procedures that communicate with other devices.

## Specifying the Operation Port Using the /P Flag {#specifying-the-operation-port-using-the-p-flag}

Starting with VDT2 version 3.00, shipped with Igor Pro 8.05, you can specify the communications port for a particular command using the /P=*portName* flag. This overrides the currently set operations port for that command.

You can use /P=*portName* with the following VDT2 operations:

```
VDT2, VDTGetStatus2
VDTRead2, VDTReadWave2, VDTReadBinary2, VDTReadBinaryWave2, VDTRead2Hex2, VDTReadHexWave2
VDTWrite2, VDTWriteWave2, VDTWriteBinary2, VDTWriteBinaryWave2, VDTWrite2Hex2, VDTWriteHexWave2
```

When calling a VDT2 operation from a preemptive thread, you must specify the port using /P=*portName*.

Thanks to Michael Huth of byte-physics ([https://www.byte-physics.de](https://www.byte-physics.de)) for contributing the /P=*portName* feature.

## Opening and Closing Ports {#opening-and-closing-ports}
Opening a port is the process in which VDT2 tells the operating system that it intends to use the port. If the port does not exist, is in use by another program, or is not configured correctly in the operating system control panels, VDT2 receives an error from the OS and  reports the error to you. If everything goes right, VDT2 gets permission from the OS to use the port.

Once you have designated a terminal port or operations port, if you try to use the port and if it is not already open, VDT2 automatically opens it. For the terminal port, this happens when you type in the VDT2 window. For the operations port, it happens when you invoke a VDT2 operation that sends or receives characters.

You can also open a port by choosing an item from the Terminal Port or Operations Port submenu of the VDT2 menu, using the VDT2 Settings dialog, or by invoking the [VDTOpenPort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtopenport2) operation. The main reason for opening a port explicitly is to be sure that VDT2 can open the port before you proceed with other things. Another reason is if you are using VDT2 as a dumb terminal and you expect to receive characters before you send them. VDT2 will not display received characters in the VDT2 window until the terminal port is opened. If neither of these reasons apply, you can let VDT2 open the port automatically.

VDT2 automatically closes all open ports when you quit Igor. You can also close ports using the VDT2 Settings dialog or the [VDTClosePort2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtcloseport2) operation. The main reason to close a port explicitly is if you want to free it for use by another program.

## Terminal Port On Line/Off Line {#terminal-port-on-line-off-line}

If the terminal port is set to "Off line" then it is off line. Otherwise, it is on line. These terms pertain to what occurs in the VDT2 window when you type and when the device to which you are connected sends characters.

If the terminal port is on line and you type in the VDT2 window, the characters you type are entered in the window (if local echo is on) *and*  transmitted to the port. Characters received at the port from the other device are displayed in the VDT2 window.

If the terminal port is off line and you type in the VDT2 window, the characters you type are entered in the window but *not*  transmitted to the port. Characters received at the port from the other device are stored in the port's input buffer, not put into the VDT2 window.

You should set the terminal port to on line when you want to use VDT2 as a dumb terminal. If you want to use the same physical port for command line operations, you can set the terminal port to off line. If the terminal port and operations port are set to the same physical port and you invoke an operation that reads or writes characters, VDT2 automatically sets the terminal port to off line.

## Aborting VDT2 Operations {#aborting-vdt2-operations}

If VDT2 is trying to send characters or read characters via the terminal or operations ports and if handshaking is not working, VDT2 will hang up. You can abort any VDT2 operation by pressingCtrl-Break. You may have to hold the keys pressed momentarily to make sure VDT2 notices.

## Detecting Serial Port Hardware Changes {#detecting-serial-port-hardware-changes}

In VDT2 version 2.20 or later, it is possible to detect and adapt to the addition or removal of serial ports while Igor is running. This typically occurs when the user connects or disconnects a USB-to-serial adapter.

You can force VDT2 to rescan for available ports by choosing [Reset Serial Ports](#reset-serial-ports) from the VDT2 submenu. This function shows how you can do it programmatically:

```igor
// HandlePortListChange()
// Returns 0 if the available ports have not changed, 1 if they have changed.
// If the available ports have changed, resets all ports to initial states.
Function HandlePortListChange()     // Returns 1 if available ports changed
    // Get a list of serial ports available when VDT2 was initialized
    VDTGetPortList2
    String originalPortList = S_VDT

    // Get a list of serial ports available now
    VDTGetPortList2/SCAN
    String currentPortList = S_VDT

    if (CmpStr(currentPortList,originalPortList) == 0)
        Print "No serial port changes detected"
        return 0
    endif

    // resetPorts can not be used with other keywords
    VDT2 resetPorts
    Print "Serial port changes detected - all ports were reset"
    return 1
End
```

The resetPorts keyword must be the only keyword in the VDT2 command.

The resetPorts keyword sets the terminal port and operations port to Off Line. It aborts any serial I/O in progress and closes all open ports. It then rescans the available hardware to create a new port list.

If you execute resetPorts, this leaves VDT2 in an initialized state as if you restarted Igor. You must reinitialize any required settings.

## Hardware Changes on Windows {#hardware-changes-on-windows}
On Windows, for historical reasons, if no ports are connected, VDT2 defaults to "COM1;COM2;COM3;COM4;COM5;COM6;COM7;COM8;" and VDTGetPortList2/SCAN returns the same.

If you connect a single port, VDTGetPortList2/SCAN returns just the name of that port. If you execute VDT2 resetPorts, just that port will be available. On Windows 10, the port appears in the Device Manager control panel under "Ports (COM & LPT)".

On disconnecting and reconnecting the adapter, the port name may change, for example, from COM3 to COM4. The same may occur on restarting the system.

## Serial Port Pinout {#serial-port-pinout}

Many usb-to-serial adapters use DB9 connectors. Here is the pinout:

| Pin | Name | Description/Notes |
| --- | --- | --- |
| 1 | DCD | Data Carrier Detect. Usually not used. |
| 2 | RxD | Receive Data line. |
| 3 | TxD | Transmit Data line. |
| 4 | DTR | Data Terminal Ready. Used for DTR/CTS handshaking. |
| 5 | GND | Logic ground. |
| 6 | DSR | Data Set Ready. Usually not used. |
| 7 | RTS | Request to Send. Usually not used. |
| 8 | CTS | Clear to Send. Used for DTR/CTS handshaking. |
| 9 |  | Ring Detect. Usually not used. |

## Handshaking {#handshaking}

The purpose of handshaking is to prevent the sender from sending more bytes than the receiver can store. To do this, the receiver must somehow signal to the sender to stop transmitting bytes when the receiver's buffer is full. Windows serial drivers support XON/XOFF handshaking, hardware handshaking or no handshaking. VDT2 presents the choice of handshaking through the VDT2 Settings dialog and also through the VDT2 command line operation.

In XON/XOFF handshaking, the two devices agree that a special byte value will have the meaning "stop sending" (XOFF) and another character will mean "resume sending" (XON). VDT2 uses the standard XON/XOFF values: decimal 17 (control-Q) for XON and decimal 19 (control-S) for XOFF.

When the receiver's input buffer is approaching full, it sends the XOFF character, telling the sender to stop sending characters. When the receiver's input buffer has a decent amount of free space, it then sends the XON character, telling the sender to resume sending characters. Even if you use XON/XOFF handshaking, you should use a fairly large input buffer size. This is because after the receiver sends the XOFF character, it takes the sender some time to stop transmitting characters. During this time, the receiver's input buffer must store the characters.

:::note
If you are doing binary transfers, you can not use XON/XOFF handshaking because the binary data may contain these values.
:::

In hardware handshaking, two signal lines are used: CTS and DTR. CTS means "clear to send". This is an input to the sender and tells the sender when it has permission to transmit bytes to the receiver. The CTS line for each device must be connected to the other device's DTR line, which usually requires a special cable. DTR means "data terminal ready". This an output from the receiver. To use hardware handshaking, choose CTS-DTR in the VDT2 Settings dialog or use the VDT2 operation.

Usually the best option is to use no handshaking at all (choose None in the VDT2 Settings dialog). Instead use a large input buffer. You can specify this in the VDT2 Settings dialog or via the VDT2 operation. VDT2 supports an input buffer of any size, but the operating system may have a limit.

## Terminators In Write Operations {#terminators-in-write-operations}

Most instruments require that you send a special character to mark the end of a command. This is usually a carriage return (CR - ASCII 13) or linefeed (LF - ASCII 10). Some instruments require both CR and LF (CRLF). You should consult the instrument's documentation to be sure what it requires.

In a literal string a single backslash is an escape character used to embed non-printing characters such as CR and LF. CR is represented as "\\r", LF is represented as "\\n" and CRLF is represented as "\\r\\n".

Here are example commands using VDTWrite2:

```igor
VDTWrite2 "IDN?\r"      // Send command followed by CR
VDTWrite2 "IDN?\n"      // Send command followed by LF
VDTWrite2 "IDN?\r\n"    // Send command followed by CRLF
```

## Terminators In Read Operations {#terminators-in-read-operations}

An instrument that sends ASCII data in response to a command will usually transmit a special character to mark the end of the transmission. This is usually a carriage return (CR - ASCII 13) or linefeed (LF - ASCII 10). Some instruments will send both CR and LF (CRLF). You should consult the instrument's documentation to be sure what it sends.

You must tailor your [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2) operation according to what the instrument sends. For example, if an instrument sends CRLF, you could execute this:

```igor
String response, junk
VDTRead2/T="\n" response
```

The /T flag tells VDTRead2 that a read is to terminate on an LF. VDTRead2 starts reading characters, storing them in the string variable response. When it receives the LF, it terminates the read into response. The CR will wind up in response but the LF will not.

## Input Buffer Limitations {#input-buffer-limitations}

The input buffer size that you request is just a [recommendation](IgorAction:BrowseURL__"https://msdn.microsoft.com/en-us/library/windows/desktop/aa363439(v=vs.85).aspx") to the serial driver.

The size of buffer you need depends on many factors but if you're in doubt, try 8192. When you enter the VDT2 Settings dialog, the dialog shows the actual size of the input buffer, which may be different from the size you requested.

## VDT2 64-bit Integer Limitations {#vdt2-64-bit-integer-limitations}

As of Igor Pro 7.00, Igor supports 64-bit signed and unsigned integer waves as well as 64-bit signed and unsigned function parameters and local variables. VDT2 operations work with 64-bit integer values but are limited to 53 bits of precision. This means they work correctly with values up to about 9 quadrillion and produce incorrect results with larger values. This limitation stems from of the use of double-precision floating point variables, which store 53 bits for the significand, in the internal VDT2 code and in Igor itself. Removing this limitation would require major rewrites and is not practical.

This limitation affects the following operations:

```
VDTReadBinary2, VDTWriteBinary2, VDTReadWave2, VDTWriteWave2
```

A workaround is to use VDTReadBinaryWave2 and VDTWriteBinaryWave2 which work with 64-bit integer values of any magnitude.

## Calling VDT2 Operations From a Preemptive Thread {#calling-vdt2-operations-from-a-preemptive-thread}

Starting with VDT2 version 3.00, shipped with Igor Pro 8.05, you can call VDT2 operations from an Igor preemptive thread.

VDT2 can run in only one thread at a time. If you create multiple threads that call VDT2 operations, one of your threads will gain access to VDT2. Your other threads will wait until the first thread finishes at which time another thread will gain access to VDT2.

It is up to you to ensure that a given serial port is used in only one thread at a time. This includes the terminal port; if you are using a port in a preemptive thread, do not use it as the terminal port.

Thanks to Michael Huth of byte-physics ([https://www.byte-physics.de](https://www.byte-physics.de)) for contributing the thread feature.

## Changes in VDT2 Relative to VDT {#changes-in-vdt2-relative-to-vdt}

VDT2 is a successor the the original VDT XOP. The main changes are that VDT2 requires Igor Pro 5.00 or later, can be invoked from user-defined functions, and uses somewhat different syntax. The following paragraphs describe the changes in more detail, to allow you to convert procedures using VDT to VDT2.



Using the VDT operation, it was permissible to modify settings for more than one port in a single command. Using [VDT2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdt2), you must not modify settings for multiple ports in a single command.



The VDT operation executed the keywords in the order they appeared in the command. The VDT2 operation executes keywords in a preset order, regardless of the order they appear in the command. This distinction will probably not matter to you.

For all read and write operations, the timeout parameter, specified by /O, is the total number of seconds allowed for the entire operation. Previously this parameter had a different interpretation for each operation.



The VDTRead operation previously accepted a circumflex (^) character in the parameter to the /T flag, which modified the behavior of VDTRead2. [VDTRead2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtread2) does not support this.

The internal number parsing done by VDTRead2 has been simplified.



The VDTReadWave /R flag previously accepted parameters in terms of X values or point numbers. VDTReadWave2 accepts point numbers only.



The VDTReadBinary /F, /L and /W flags have been replaced in [VDTReadBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinary2) by the /TYPE flag.



The VDTReadBinaryWave /F, /L and /W flags have been replaced in [VDTReadBinaryWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadbinarywave2) by the /TYPE flag.



The VDTReadHex operation treated incoming data as signed. [VDTReadHex2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtreadhex2) treats it as unsigned. For example, when reading "FF", VDTReadHex returned -1 while VDTReadHex2 returns 255.



The VDTWrite operation previously accepted a list of arguments that could be numbers or strings. [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) accepts just a single string argument. As illustrated in the help for VDTWrite2, you can use the sprintf operation to generate a string containing the values from other variables.



The VDTWrite operation by default sent a carriage return character at the end of the transmission. The [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) operation does not do this. If you want to send a carriage return, carriage return/linefeed or other terminator, you must include it in the string parameter. See [Terminators In Write Operations](#terminators-in-write-operations).



The [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) operation does not accept the /F flag.



The /F flag for the [VDTWriteWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritewave2) operation has been changed completely. See the documentation for VDTWriteWave2.



The VDTWriteBinary /F, /L and /W flags have been replaced in [VDTWriteBinary2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritebinary2) by the /TYPE flag. VDTWriteBinary2 can no longer transmit strings. Use [VDTWrite2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwrite2) for that.



The VDTWriteBinaryWave /F, /L and /W flags have been replaced in [VDTWriteBinaryWave2](/igorpro/extensions/data-acquisition/vdt2/vdt2-operations.md#vdtwritebinarywave2) by the /TYPE flag.



The Quit VDT menu item was removed from the VDT submenu. This was necessary because VDT2 operations can be compiled into user functions. You can use the "VDT2 killio" command to kill any I/O in progress and the VDTClosePort2 operation to close any open ports.



### Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.00 | Initial release of VDT2. |
| 1.01 | First Mac OS X-compatible version of VDT2. |
| 1.02 | Fixed /Q flag in VDTRead2 operation. |
| 1.10 | Created Mac OS X universal binary (for PowerPC and Intel) version of VDT2. Tested on PowerPC and Intel Macintosh. |
| 1.11 | Fixed bugs in VDTReadWave2 and VDTReadHexWave2 which prevented V_VDT from being set to the correct value. |
| 1.12 | If a timeout or abort (cmd-dot on Macintosh, Ctrl-Break on Windows) occurs while reading a string using VDTRead2 or VDTReadBinary2, any characters received prior to the timeout or abort are stored in the string. |
| 1.13 | Supported long file names on Macintosh. |
| 1.14 | Added support for 128000 and 256000 baud. These rates may not work on all machines. They do not appear to work on Mac OS X but are more likely to work on Windows. |
| 1.15 | Added support for 460800 and 921600 baud. |
|  | <div><Admonition type="warning"><p>Your hardware may not support high baud rates and the serial input buffer may be too small to work at high baud rates. You should always verify that you can communicate at a lower baud rate before trying the higher rates.</p></Admonition></div> |
|  | As of this writing the highest [officially supported baud rate](IgorAction:BrowseURL__"https://msdn.microsoft.com/en-us/library/windows/desktop/aa363214(v=vs.85).aspx") on Windows is 256000. |
| 1.16 | Revamped VDT2 to use the new menu API provided in XOP Toolkit 6.32. |
| 1.17 | Fixed Mac OS X version of VDT2. Previously if you turned odd parity on, it would stay as odd parity even if you set the port to even parity. |
| 2.00 | This is the first version that runs in 64 bits on Macintosh. It requires Igor Pro 7.00. |
| 2.01 | Recompiled with XOP Toolkit 7.01 to support Igor Pro 8 on 64-bit Macintosh. |
| 2.10 | This version of the VDT2 XOP requires Igor Pro 8.00 or later because it supports [long object names](/igorpro/igor-basics/using-igor.md#long-object-names). |
| 2.20 | Added the resetPorts keyword for VDT2. See [Detecting Serial Port Hardware Changes](#detecting-serial-port-hardware-changes) for details. |
|  | Added the /SCAN flag for VDTGetPortList2. See [Detecting Serial Port Hardware Changes](#detecting-serial-port-hardware-changes) for details. |
|  | Previously on Window, if VDT2 was unable to detect any serial ports, it defaulted to COM1...COM8. This was done because ancient versions of Windows did not provide a reliable way to know what serial ports were available. Now, if VDT2 detects no ports when it is started, it lists no ports. If you connect a USB-to-serial adapater after starting VDT2, you can force it to recognize the new port by choosing [Reset Serial Ports](#reset-serial-ports) from the VDT2 menu. |
| 2.21 | Fixed a Windows bug which caused VDTGetPortList2/SCAN to return a truncated result if the list of port names exceeded 7 bytes. |
| 3.00 | All of the VDT2 operations are now threadsafe. See [Calling VDT2 Operations from a Preemptive Thread](#calling-vdt2-operations-from-a-preemptive-thread) for details. |
|  | Added /P=portName flag to various VDT2 operations. See [Specifying the Operation Port Using the /P Flag](#specifying-the-operation-port-using-the-p-flag) for details. |