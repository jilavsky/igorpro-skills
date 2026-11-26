---
description: "NIGPIB2 adds the following command line operations to Igor: NI4882 For accessing the National Instruments driver."
slug: /extensions/data-acquisition/nigpib2/nigpib2-command-line-operations
---

NIGPIB2 adds the following command line operations to Igor:

[NI4882](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#ni4882)	For accessing the National Instruments driver

[GPIB2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpib2)	For setting up NIGPIB2 XOP and misc GPIB control

[GPIBRead2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibread2)	For reading ASCII data into Igor variables or strings

[GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2)	For writing ASCII data strings

[GPIBReadWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadwave2)	For reading ASCII data into Igor waves

[GPIBWriteWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritewave2)	For writing ASCII data from Igor waves

[GPIBReadBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinary2)	For reading binary data into Igor variables or strings

[GPIBWriteBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinary2)	For writing binary data from Igor variables or strings

[GPIBReadBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinarywave2)	For reading binary data into Igor waves

[GPIBWriteBinaryWave2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwritebinarywave2)	For writing binary data from Igor waves

The GPIBRead2, GPIBWrite2, GPIBReadWave2, GPIBWriteWave2, GPIBReadBinary2, GPIBWriteBinary2, GPIBReadBinaryWave2 and GPIBWriteBinaryWave2, operations are collectively called "read/write" operations. These work at a level higher than the ibrd and ibwrt calls supplied by the National driver. For most data transfer operations, you can use these high level calls. For some setup and bus management operations, you need to use the low level NI-488 calls.

<div className="command-signature">

## <strong>NI4882</strong>  [/Q] <em>keyword</em> = \\{<em>parameters</em>...\\} {#ni4882}

</div>

The NI4882 operation provides low-level access to the National Instruments NI-488 GPIB driver.

All of the calls supported by the NI-488.2 driver C language interface are supported by the NI4882 operation and behave as documented in the NI-488.2 driver manual except for differences described below.

The NI-488.2 driver supports two families of calls: "traditional calls" which identify the device of interest using a "unit descriptor" (now called a "device descriptor" in NI's documentation) and newer "multi-device" calls which identify the device using a zero-based board ID number and a GPIB address.

Most applications will use just a few of these calls and many need just the ibfind or ibdev calls and can use high-level NIGPIB2 calls for all device communications.

The ibfind call is used to obtain the unit descriptor for a GPIB interface (a board in the computer or a GPIB interface connected via USB or Ethernet). It obtains the unit descriptor by name, usually "gpib0" for the first GPIB interface.

The ibdev call is used to obtain the unit descriptor for a device on the bus (an instrument) based on its GPIB address. ibfind can also be used for this purpose but National Instruments recommends using ibdev because it does not require configuring the device name.

:::note
Each time you call ibfind or ibdev, the NI-488.2 driver returns a new unit descriptor. Don't call ibfind or ibdev over and over again because the driver will eventually run out of unit descriptors and return an error.
:::

The NI4882 operation reports errors as described below under Details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | If an NI-488.2 driver error occurs, NIGPIB2 stores it in V_iberr but does not report it to Igor. This allows your procedure to handle the error. |

### *Parameters* {#parameters}
The keyword specifies what action you want the NI4882 operation to take. Each keyword has its own set of parameters. The parameters always appear within braces. For example:

```igor
NI4882 ibwrt={ud, str, cnt}
```

The keywords supported are listed below. There is an example and some general information below that.

The keywords and their parameters follow the NI-488.2 driver calls closely with a few exceptions, documented below.

### *Parameter Types* {#parameter-types}
For all calls, the "ud" parameter is a NI-488.2 driver board or device unit descriptor which you get using the NI4882 ibfind or NI4882 ibdev calls.

Parameters which are character arrays in the NI-488.2 driver C language interface are strings in the NI4882 operation.

The "boardID" parameter is used in NI-488.2 calls and is a board index number, 0 for the gpib0 board, for example.

The "address" parameter is used in NI-488.2 calls and is single GPIB address.

The "addressListWave" parameter is used in NI-488.2 calls and is a real numeric wave containing a list of GPIB addresses with a -1 value to mark the end of the list. If you forget the -1, NIGPIB2 will add it for you to its internal copy of the address list. The address list is limited to 100 addresses.

The "resultListWave" parameter is used in NI-488.2 calls and is a real numeric wave into which NIGPIB2 puts results from calls to the NI driver. When you make a call to NI4882 that uses a result list wave, NIGPIB2 stores values in the wave, starting at point 0. If necessary to store all of the result values, NIGPIB2 will add points to the result list wave. It never deletes points from the wave.

The "bufferWave" parameter is used in NI-488.2 calls and is a real or complex, numeric wave into which NIGPIB2 puts results from calls to the NI driver. When you make a call to NI4882 that uses a buffer wave, NIGPIB2 stores byte values in the wave, starting at the first byte in the wave. It stores the number of bytes that it stored in the buffer wave in the variable V_ibcnt. If necessary to store all of the bytes, NIGPIB2 will add points to the buffer wave. It never deletes points from the wave. When you make the buffer wave, use the numeric type appropriate to the data that you are expecting to receive. For example, if you are expecting signed 16 bit integers, use Make/Y=(0x10) aBufferWave.

### *NI4882 Keywords* {#ni4882-keywords}
Here are the NI4882 calls. For details on the behavior of the calls, consult your National Instruments NI-488.2 documentation.

### *Traditional Keywords* {#traditional-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">NI4882 ibask = {*ud*, *option*}</span> | Returns NI-488.2 driver configuration information. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 ibcac = {*ud*, *v*}</span> | Makes your interface the active controller ("controller-in-charge"). |
| <span class="table-cell-nowrap">NI4882 ibclr = {*ud*}</span> | Sends a device clear message to an instrument. |
| <span class="table-cell-nowrap">NI4882 ibcmd = {*ud*, cmd, cnt}</span> | Sends a command over the GPIB bus. |
|  | cmd is a string expression of unlimited length. If cnt is less than or equal to zero, the actual length of the string expression is sent to the NI-488.2 driver. |
| <span class="table-cell-nowrap">NI4882 ibconfig = {*ud*, option, value}</span> |  |
|  | Changes NI-488.2 driver configuration parameters. |
| <span class="table-cell-nowrap">NI4882 ibdev = {*boardIndex*, *pad*, *sad*, *tmo*, *eot*, *eos*}</span> |  |
|  | Obtains a device descriptor from the NI-488.2 driver based on the device's GPIB address. This descriptor is used as the ud parameter passed with other NI4882 keywords. |
|  | The output from the ibdev call is stored in V_flag. This will be either a device descriptor or a -1. |
| <span class="table-cell-nowrap">NI4882 ibdma = {*ud*, *v*}</span> | Enables or disables direct memory access. |
| <span class="table-cell-nowrap">NI4882 ibeos = {*ud*, *v*}</span> | Changes end-of-string value. |
| <span class="table-cell-nowrap">NI4882 ibeot = {*ud*, *v*}</span> | Enables or disables the END message. |
| <span class="table-cell-nowrap">NI4882 ibfind = {*udname*}</span> | Obtains an interface board or GPIB device descriptor from the NI-488.2 driver based on a name as set in the NI configuration program. |
|  | Stores the board or device unit descriptor in V_flag. |
|  | udname is a string expression of no more than 255 characters. Usually it is "gpib0". |
|  | NI recommends that you use ibdev instead for obtaining the unit descriptor for a GPIB device. However, you can obtain the unit descriptor for a GPIB interface (a "board") only through ibfind. |
| <span class="table-cell-nowrap">NI4882 ibgts = {*ud*, *v*}</span> | Switches board from active controller to standby. |
| <span class="table-cell-nowrap">NI4882 ibist = {*ud*, *v*}</span> |  |
| <span class="table-cell-nowrap">NI4882 iblines = {*ud*}</span> | Reads the state of the GPIB control lines. |
|  | The response is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 ibln = {*ud*, *pad*, *sad*}</span> | Checks if there is a device at a particular GPIB address. |
|  | The output is stored in V_flag which will be non-zero if a listener is detected. |
| <span class="table-cell-nowrap">NI4882 ibloc = {*ud*}</span> | Puts device in local operation mode. |
| <span class="table-cell-nowrap">NI4882 iblock = {*ud*}</span> | Lock an interface. |
| <span class="table-cell-nowrap">NI4882 ibonl = {*ud*, *v*}</span> | Switches a device to online of offline. |
| <span class="table-cell-nowrap">NI4882 ibpad = {*ud*, *v*}</span> | Changes a device's primary GPIB address. |
| <span class="table-cell-nowrap">NI4882 ibpct = {*ud*}</span> | Passes control from one controller to another. |
| <span class="table-cell-nowrap">NI4882 ibppc = {*ud*, *v*}</span> | Configures parallel polls. |
| <span class="table-cell-nowrap">NI4882 ibrd = {*ud*, *cnt*}</span> | Reads data from a device. |
|  | The output is stored in S_value. |
| <span class="table-cell-nowrap">NI4882 ibrdf = {*ud*, *flname*}</span> | Reads data from a device into a file. |
|  | flname is a string expression of unlimited length. |
| <span class="table-cell-nowrap">NI4882 ibrpp = {*ud*}</span> | Requests a parallel poll. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 ibrsc = {*ud*, *v*}</span> | Requests or releases system control |
| <span class="table-cell-nowrap">NI4882 ibrsp = {*ud*,}</span> | Requests a serial poll. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 ibrsv = {*ud*, *v*}</span> | Requests service. |
| <span class="table-cell-nowrap">NI4882 ibsad = {*ud*, *v*}</span> | Sets a device's secondary address. |
| <span class="table-cell-nowrap">NI4882 ibsic = {*ud*}</span> | Sends an Interface Clear message to the GPIB bus. |
| <span class="table-cell-nowrap">NI4882 ibsre = {**ud*, *v*}</span> | Sends a remote-enable message to a device. |
| <span class="table-cell-nowrap">NI4882 ibtmo = {*ud*, *v*}</span> | Sets the timeout for a device. |
| <span class="table-cell-nowrap">NI4882 ibtrg = {*ud*}</span> | Triggers a device. |
| <span class="table-cell-nowrap">NI4882 ibunlock = {*ud*}</span> | Unlocks an interface. |
| <span class="table-cell-nowrap">NI4882 ibwait = {*ud*, *mask*}</span> | Waits for a specified event. |
| <span class="table-cell-nowrap">NI4882 ibwrt = {*ud*, *str*, *cnt*}</span> | Writes data to a device. |
|  | str is a string expression of unlimited length. |
| <span class="table-cell-nowrap">NI4882 ibwrtf = {*ud*, *flname*}</span> | Writes data in a file to a device. |
|  | flname is a string expression of no more than 255 characters. |

The following NI-488 traditional driver calls are not supported by NI4882: ibcmda, ibcnotify, ibrda, ibstop, ibwrta.

### *Multi-Device Keywords* {#multi-device-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">NI4882 AllSpoll = {*boardID*, *addressListWave*, *resultListWave*}</span> |  |
|  | Conducts a serial poll. |
|  | The number of items stored in *resultListWave* is stored in V_ibcnt. |
| <span class="table-cell-nowrap">NI4882 DevClear = {*boardID*, *address*}</span> |  |
|  | Sends a device clear message to a device. |
| <span class="table-cell-nowrap">NI4882 DevClearList = {*boardID*, *addressListWave*}</span> |  |
|  | Sends a device clear message to multiple devices. |
| <span class="table-cell-nowrap">NI4882 EnableLocal = {*boardID*, *addressListWave*}</span> |  |
|  | Enables front-panel operation of devices. |
| <span class="table-cell-nowrap">NI4882 EnableRemote = {*boardID*, *addressListWave*}</span> |  |
|  | Enables GPIB remote control of devices. |
| <span class="table-cell-nowrap">NI4882 FindLstn = {*boardID*, *addressListWave*, *resultListWave*, *limit*}</span> |  |
|  | Identifies devices on the GPIB bus that are listening. |
|  | The number of items stored in *resultListWave* is stored in V_ibcnt. |
| <span class="table-cell-nowrap">NI4882 FindRQS = {*boardID*, *addressListWave*}</span> |  |
|  | Determines which device is signaling a service request. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 PassControl = {*boardID*, *address*}</span> |  |
|  | Passes control from one controller to another. |
| <span class="table-cell-nowrap">NI4882 PPoll = {*boardID*}</span> | Conducts a parallel poll. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 PPollConfig = {*boardID*, *address*, *dataLine*, *lineSense*}</span> |  |
|  | Configures devices for a parallel poll. |
| <span class="table-cell-nowrap">NI4882 PPollUnconfig = {*boardID*, *addressListWave*}</span> |  |
|  | Unconfigures devices for a parallel poll. |
| <span class="table-cell-nowrap">NI4882 RcvRespMsg = {*boardID*, *bufferWave*, *count*, *termination*}</span> |  |
|  | Reads data from a device that is addressed to talk. |
| <span class="table-cell-nowrap">NI4882 ReadStatusByte = {*boardID*, *address*}</span> |  |
|  | Returns a device's serial poll status byte. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 Receive = {*boardID*, *address*, *bufferWave*, *count*, *termination*}</span> |  |
|  | Reads data from an instrument. |
| <span class="table-cell-nowrap">NI4882 ReceiveSetup = {*boardID*, *address*}</span> |  |
|  | Sets up the talker and listener in preparation for calling Receive. |
| <span class="table-cell-nowrap">NI4882 ResetSys = {*boardID*, *addressListWave*}</span> |  |
|  | Resets devices on the bus. |
| <span class="table-cell-nowrap">NI4882 Send = {*boardID*, *address*, *bufferWave*, *count*, *eotMode*}</span> |  |
|  | Sends data to a device. |
| <span class="table-cell-nowrap">NI4882 SendCmds = {*boardID*, *bufferWave*, *count*}</span> |  |
|  | Sends special GPIB command byte data. |
| <span class="table-cell-nowrap">NI4882 SendDataBytes = {*boardID*, *bufferWave*, *count*, *eotMode*}</span> |  |
|  | Sends data to devices that are addressed to listen. |
| <span class="table-cell-nowrap">NI4882 SendIFC = {*boardID*}</span> | Sends the Interface Clear message. |
| <span class="table-cell-nowrap">NI4882 SendList = {*boardID*, *addressListWave*, *bufferWave*, *count*, *eotMode*}</span> |  |
|  | Sends data to multiple devices. |
| <span class="table-cell-nowrap">NI4882 SendLLO = {*boardID*}</span> | Sends the Local Lockout message to all devices on the GPIB bus. |
| <span class="table-cell-nowrap">NI4882 SendSetup = {*boardID*, *addressListWave*}</span> |  |
|  | Does setup in preparation for calling SendDataBytes. |
| <span class="table-cell-nowrap">NI4882 SetRWLS = {*boardID*, *addressListWave*}</span> |  |
|  | Puts device in "remote with lockout" state. |
| <span class="table-cell-nowrap">NI4882 TestSRQ = {*boardID*}</span> | Checks the state of the service request line. |
|  | The output is stored in V_flag. |
| <span class="table-cell-nowrap">NI4882 TestSys = {*boardID*, *addressListWave*, *resultListWave*}</span> |  |
|  | Tells devices to do a self-test. |
|  | The number of devices that failed is stored in V_ibcnt. |
| <span class="table-cell-nowrap">NI4882 Trigger = {*boardID*, *address*}</span> |  |
|  | Sends a trigger message to a device. |
| <span class="table-cell-nowrap">NI4882 TriggerList = {*boardID*, *addressListWave*}</span> |  |
|  | Sends a trigger message to multiple devices. |
| <span class="table-cell-nowrap">NI4882 WaitSRQ = {*boardID*}</span> | Waits until a device assers the service request line. |
|  | The output is stored in V_flag. |

### *Details* {#details}
After each NI-488 call, NI4882 sets the Igor variables V_ibsta, V_iberr, and V_ibcnt equal to the NI-488.2 driver variables ibsta, iberr and ibcnt.

V_ibsta contains a status word condition. If an error occurred, bit 15 will be set. If a timeout occurred, bit 14 will be set.

V_iberr contains an NI-488.2 driver error code. It is meaningful only if the error bit of V_ibsta is set.

V_ibcnt contains a count of items transmitted or received.

You can send multiple keywords in one command to NI4882. For example:

```igor
NI4882 ibwrt={DVM,"F3R1X5P2G0",10} ibrd={DVM,100}
```

However, if you want to check V_ibsta to see if an error occurred or if you need to know the value of V_ibcnt, you must execute only one keyword.

### *Errors* {#errors}
There are two kinds of errors that can occur during an NI4882 command. NI4882 may detect an error such as an invalid parameter or the NI-488.2 driver may detect an error. For example,

```igor
NI4882 ibfind={gpib0}
```

generates an error because the NI4882 expects a string as the parameter. Parameter errors are always reported by NIGPIB2 to Igor.

On the other hand,

```igor
NI4882 ibfind={"gpib99"}
```

generates an NI-488.2 driver error ("board or device not recognized") because "gpib99" is not the name of a board or device known by the NI-488.2 driver.

When the NI4882 operation finishes, it stores the values in the NI-488.2 driver's internal ibsta, iberr and ibcnt variables in the corresponding Igor variables (V_ibsta, V_iberr, V_ibcnt). If a parameter error or other non-driver error (e.g., out-of-memory) occurred, NI4882 always reports it to Igor as a fatal error. This causes procedure execution to halt and Igor reports the error to the user which is usually what you want. However, you can prevent procedure execution from halting by calling [GetRTError](/igorpro/commands/getrterror.md)(1) in which case you should handle or report the error yourself.

If the internal ibsta variable indicates that an NI-488.2 driver error or timeout occurred and if the /Q flag was not used, NI4882 reports the error to Igor as a fatal error. If the /Q flag was used, NI4882 does not report the error to Igor, allowing you to handle or report it yourself.

This snippet shows how to handle a driver error or timeout yourself:

```igor
Function Test(ud)
    Variable ud             // Device unit descriptor

    NI4882 /Q ibrd={ud,100} // Read up to 100 characters
    if (V_ibsta & 0x8000)
        Printf "NI-488.2 driver returned error number %d\r", V_iberr
        if (V_ibsta & 0x4000)
            Print "NI-488.2 driver timed out during read"
        endif
    else
        Print "NI-488.2 read %s bytes\r", V_ibcnt
    endif
End
```

### *Timeouts* {#timeouts}

NI4882 as well as the GPIB operations will time out after the NI-488.2 driver timeout expires. You set this timeout using NI configuration program or using the NI4882 ibdev command or using the NI4882 ibtmo command.

### *Example 1* {#example-1}
Consider the following Igor commands:


1. Variable/G DVM
2. String response
3. `NI4882 ibdev={0,1,0,13,1,0}; DVM = V_flag`
4. `NI4882 ibwrt={DVM,"F3R1X5P2G0",10}`
5. `NI4882 ibrd={DVM,100}; response = S_value`
6. Print response

Line 1 creates the global variable, DVM, to contain the unit descriptor for the device at GPIB address 1.

Line 2 creates a string variable to contain characters read from the GPIB using the ibrd keyword.

Line 3 invokes the ibdev call to obtain a unit descriptor for the device connected to the first GPIB interface (first parameter) at GPIB address 1 (second parameter). This call puts the result from the ibdev call into the Igor variable DVM for future use. The last four parameters specify the secondary address (0 for none), timeout period (13=10 seconds), END-enable (1=turned on) and end-of-string-enable (0=turned off).

Line 4 writes a string to the DVM. 10 is the number of characters from the string to be written.

Line 5 reads a response from the DVM and puts it into the Igor string variable named "response". It reads up to 100 characters or until the DVM asserts the END line.

### *Example 2* {#example-2}
This example illustrates the use of several NI-488.2 "multi-device" functions. The multi-device functions are more flexible than the traditional functions and are not needed for most applications.

InitBoardAndDevice sets up some global variables used by the other procedures.

```igor
Function InitBoardAndDevice()
    Variable/G gBoardID, gDeviceAddress
    gBoardID = 0                        // 0 for gpib0
    gDeviceAddress = 1                  // 1 for dev1
End
```

DevClearList illustrates how to send a device clear to a list of devices, in this case, the devices at address 1 and address 2 on the GPIB bus.

```
Function DevClearList()
    Make/O gAddressList = {1, 2, -1}    // -1 is NOADDR - marks end of list.
    NI4882 DevClearList={gBoardID,gAddressList}
End
```


FindListeners returns, in the wave gResultList, a list of addresses of existing devices. In this example, it tests for the presence of devices at addresses 1, 2, and 3.

```igor
Function FindListeners()
    Make/O gAddressList = {1, 2, 3, -1} // -1 is NOADDR - marks end of list.
    Make/O/N=0 gResultList
    NI4882 FindLstn={gBoardID,gAddressList,gResultList,5}
    Printf "Number of responses: %d\r", V_ibcnt
End
```

TestSendAndReceive illustrates the use of the Send and Receive keywords. It sends the command "ID?" to the device and then stores the result in bufferWave.

```igor
Function TestSendAndReceive()
    Variable DABend = 0x02      // Means assert END with last output byte.
    Variable STOPend = 0x100    // Means stop receiving when END is asserted.
    Make/O/N=3/B bufferWave = { char2num("I"), char2num("D"), char2num("?") }

    NI4882 Send={gBoardID,gDeviceAddress,bufferWave,3,DABend}           // Send bytes.
    NI4882 Receive={gBoardID,gDeviceAddress,bufferWave,1000,STOPend}    // Read 1000 bytes or until END is asserted.
End
```


<div className="command-signature">

## <strong>GPIB2</strong>  [/Q] <em>keyword</em> [= <em>parameters</em> ] {#gpib2}

</div>

The GPIB2 operation provides a high-level interface to the GPIB board and device and other miscellaneous functions.

### *Flags* {#gpib2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | GPIB2 sets V_Flag to zero if no error occurred or to non-zero if an error did occur. If the error is a timeout, GPIB2 does not report it to Igor so that your procedure can handle the error. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">board = *ud*</span> | Used in preparation for GPIB2 InterfaceClear (see below). ud is the board unit descriptor for the GPIB2 board which is to be cleared. |
| <span class="table-cell-nowrap">device = *ud*</span> | Used in preparation for GPIB2 read/write operations. ud is the device unit descriptor for a GPIB board or device with which read/write operations are to be done. |
| InterfaceClear | Sends the interface clear message to the GPIB bus connected to the board specified by the GPIB2 board operation. |
| KillIO | Initializes NIGPIB2 and sends the interface clear message. This is the best way to clear things up after a hangup when you want to start fresh. |
| DeviceClear | Sends a device clear to the device specified by a previous GPIB2 device command. |
| GotoLocal | Sends a goto local message to the device specified by a previous GPIB2 device command. |
| ReadSerialPoll | Reads the serial poll status of the device specified by a previous GPIB2 device command into V_spr. If the /Q flag is present, a timeout error is not reported back to Igor but the V_Flag variable is set to 0 if no timeout occurred or to non-zero if a timeout occurred. |

### *Example* {#example}
This function sets the GPIB board gpib0 and the GPIB device at address 1 to be the active board and device as far as GPIB read/write operations are concerned. It calls GPIB2 KillIO to make sure that NIGPIB2 is in an initialized state and send the Interface Clear message.

```igor
Function InitBoardAndDevice()
    // These variables are useful for NI-488.2 calls using the NI4882 command.
    Variable/G gBoardAddress = 0, gDeviceAddress = 1

    // These variables are useful for pre-NI-488.2 keywords and for the
    // GPIB board and GPIB device calls.
    Variable/G gBoardUnitDescriptor, gDeviceUnitDescriptor

    // Find the unit descriptors.
    NI4882 ibfind={"gpib0"}; gBoardUnitDescriptor = V_flag
    NI4882 ibdev={0,1,0,13,1,0}; gDeviceUnitDescriptor = V_flag

    // Set active board and device for high-level GPIB operations.
    GPIB2 board=gBoardUnitDescriptor        // Board to use for GPIB InterfaceClear command.
    GPIB2 device=gDeviceUnitDescriptor      // Device to use for GPIBXXX operations.

    // Make sure we are in a clean state.
    GPIB2 KillIO                            // Inits NIGPIB2 and sends Interface Clear message.
End
```


### *Timeouts* {#gpib2-timeouts}
The GPIB2 operation will time out after the NI-488.2 driver timeout expires. You set this timeout using National's control panels or using the NI4882 ibtmo operation.


<div className="command-signature">

## <strong>GPIBRead2</strong>  [ /T=<em>termStr</em> /N=<em>n</em> /Q] <em>variableName</em> [ , <em>variableName</em> ] {#gpibread2}

</div>

Reads from the active device into string or numeric variables.

### *Parameters* {#gpibread2-parameters}
When used from the command line or in a macro, *variableName* must be the name of a local or global variable in the current data folder. When used from a user function, *variableName* can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

### *Flags* {#gpibread2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr* is a string or string expression specifying characters which terminate a read. The default is /T=",\\r\\t". |
| <span class="table-cell-nowrap">/N = n</span> | n is maximum number of characters to read for each variable. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

### *Details* {#gpibread2-details}
GPIBRead2 sets the variable V_Flag to the number of items read.

Here is a discussion of how GPIBRead2 goes about trying to read into its argument list.

If the /T=*termStr*  flag is present, it specifies a terminator character or characters. The terminator is the character that ends input into a string or numeric variable. The default is /T=",\\r\\t" so that a comma, carriage return or tab ends a read. The read is also ended if the talker asserts the `GPIB END` signal.

/N=n is an optional maximum number of characters to be read into a string or numeric variable. The default is /N=255.

If /Q is present and a timeout occurs, GPIBRead2 aborts after setting the variable V_Flag to the number of items read but does not put up an error message and does not halt procedure execution. This allows a procedure to handle a timeout in its own way.

When reading a string, GPIBRead2 reads until the next terminator is encountered. The terminator is not put into the string. The next read starts after the terminator.

Do not use GPIBRead2 to read binary data or anything that contains a null character (ASCII 0). Use [GPIBReadBinary2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibreadbinary2) instead.

When reading a numeric variable, GPIBRead2 first skips any non-numeric characters and then reads a number. If the *variableName* refers to a complex variable, GPIBRead2 reads two numbers from the device and stores both the real and imaginary parts of the variable.

### *Example* {#gpibread2-example}

```igor
Variable v1, v2
String s1
GPIB2 device=unitDeviceDescriptor   // Unit descriptor from ibfind or ibdev
GPIBRead2 v1, s1, v2
```

This reads from the active device, specified via the GPIB2 command, into variable v1, string variable s1 and variable v2.

### *Terminators* {#terminators}
There are three common cases to consider:

Instruments that send CR as terminator

Instruments that send CR and LF as terminator

Instruments that send neither CR nor LF but use the END line only.

You must determine what terminator your instrument sends from its documentation.

The following examples show how you would read a response in the three cases into a string variable. str1 is an Igor string variable.

```igor
// CR terminator
String str1
GPIBRead2 str1	// Read the string till CR

// CRLF terminator
String str1, lf
GPIBRead2/T="\r\n" str1, lf	// Read the string till CR, then read LF.

// END terminator
String str1
GPIBRead2 str1	// Read the string till END
```

The following examples show how you would read a response in the three cases into a numeric variable.

```igor
// CR terminator
Variable v0
GPIBRead2 v0	// Read the number till CR

// CRLF terminator
Variable v0
String lf
GPIBRead2/T="\r\n" v0, lf	// Read the number till CR, then read LF.

// END terminator
GPIBRead2 v0	// Read the string till END
```

If you expected \<number\>\<comma\>\<number\>\<comma\>\<number\>\<crlf\>, here is what you would do:

```igor
Variable v0, v1, v2
String lf
GPIBRead2/T=",\r\n" v0, v1, v2, lf
```

You may want to read every character into a string until END is asserted. To do this you can specify an empty terminator:

```igor
GPIBRead2/T="" str1
```

<div className="command-signature">

## <strong>GPIBReadWave2</strong>  [ /R=[ <em>start</em> , <em>end</em>  ] /T=<em>termStr</em> /N=<em>n</em> /Q ] <em>waveName</em>  [, <em>waveName</em> ] {#gpibreadwave2}

</div>

Reads data from device into waves.

### *Parameters* {#gpibreadwave2-parameters}
The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and GPIBReadWave2 reads two values for each wave point.

Assuming the the /R flag is omitted, data is stored into point 0 of each wave, then point 1 of each wave, and so on.

### *Flags* {#gpibreadwave2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = n</span> | n is maximum number of characters to read for each value. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/R = [ *start*, *end* ]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to read data into. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr* is a string or string expression specifying characters which terminate a read. |

### *Details* {#gpibreadwave2-details}
If the /R flag is omitted, GPIBReadWave2 stores values in point 0 through point n-1 where n is the number of points in the first wave.

GPIBReadWave2 sets the variable V_flag to the number of  individual numbers read.

GPIBReadWave2 works with 64-bit integer data but is limited to 53 bits of precision. See [NIGPIB2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-64-bit-integer-limitations) for details.

### *Example* {#gpibreadwave2-example}

```igor
GPIB2 device=unitDeviceDescriptor   // Unit descriptor from ibfind or ibdev
GPIBReadWave2 wave1, wave2, wave3
```

This reads from the device into wave1, wave2 and wave3. It reads until it has put a value in each point of each wave.

### *Terminators* {#gpibreadwave2-terminators}
See the discussion of terminators for the [GPIBRead2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibread2) operation.



<div className="command-signature">

## <strong>GPIBReadBinary2</strong>   [ <em>flags</em> ] <em>variableName</em>  [,<em>variableName</em> ] {#gpibreadbinary2}

</div>

Reads binary data into Igor strings and variables. The binary data can be read as integers of one, two or four bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

### *Parameters* {#gpibreadbinary2-parameters}
When used from the command line or in a macro, *variableName* must be the name of a local or global variable in the current data folder. When used from a user function, *variableName* can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

If /S=*strLen* is used, the arguments are expected to be string variables and bytes are read up to *strLen* bytes or until a byte is read with END asserted or until a byte specified by /T=*termStr* is read.

If /S=*strLen* is NOT used, the arguments are expected to be numeric variables into which data is to be read.

Reading binary data into strings is used mostly to skip a number of bytes or until a certain byte is received. To read actual ASCII data into strings, use [GPIBRead2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibread2) instead of GPIBReadBinary2.

### *Flags* {#gpibreadbinary2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Multi-byte data is received low-byte-first. Without /B, multi-byte data is received high-byte-first. This flag affects receiving of numeric data only, not string data. |
|  | See [NIGPIB2 Binary Operations Byte Order](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-binary-operations-byte-order) for details. |
| <span class="table-cell-nowrap">/B = *byteOrder*</span> | *byteOrder*=0: Multi-byte data is received high-byte-first. |
|  | *byteOrder*=1: Multi-byte data is received low-byte-first. |
|  | This form of the /B flag requires NIGPIB2 version 1.11 or later. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/S = *strLen*</span> | If present, the variables are expected to be string variables. Bytes are read up to *strLen* bytes or until a byte is read with END asserted or until a byte specified by /T=*termStr* is read. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | Specifies a terminator character when reading bytes into strings. The default value is "" (no terminators). The read will be faster if no terminators are specified. This has no effect when reading into numeric variables. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |
| <span class="table-cell-nowrap">/Y = {*o*, *m*}</span> | *o* is offset, *m* is multiplier. /Y is used to scale integer data into real numbers. |
|  | <code class="igor">output data = (input data + offset) * multiplier</code> |

### *Details* {#gpibreadbinary2-details}
If a numeric variable is complex, GPIBReadBinary2 reads two values for that variable.

GPIBReadBinary2 sets the variable V_flag, after creating it if necessary, to the number of  items read.

GPIBReadBinary2 works with 64-bit integer data but is limited to 53 bits of precision. See [NIGPIB2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-64-bit-integer-limitations) for details.

### *Examples* {#examples}
This command tells the NI-488.2 driver which device to communicate with.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
```

This command reads 10 bytes or until END is received into string variable str1.

```igor
String str1
GPIBReadBinary2/S=10 str1
```

This command reads two-byte signed integer binary numbers into the numeric variables v0 and v1 using low-byte-first byte order.

```igor
Variable v0, v1
GPIBReadBinary2/TYPE=(0x10)/B=1 v0, v1
```

This command reads IEEE single-precision floating point binary numbers into v0 and v1 using low-byte-first byte order.

```igor
Variable v0, v1
GPIBReadBinary2/TYPE=2/B=1 v0, v1
```

<div className="command-signature">

## <strong>GPIBReadBinaryWave2</strong>  [ <em>flags</em> ]  <em>waveName</em>  [,<em>waveName</em>] {#gpibreadbinarywave2}

</div>

Reads binary data into the numeric waves named in wavelist. The waves can be of any numeric data type, real or complex.

### *Flags* {#gpibreadbinarywave2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Multi-byte data is received low-byte-first. Without /B, multi-byte data is received high-byte-first. This flag affects receiving of numeric data only, not string data. |
|  | See [NIGPIB2 Binary Operations Byte Order](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-binary-operations-byte-order) for details. |
| /B=*byteOrder* |<table class="nested-table"><tbody><tr><td>*byteOrder*=0:</td><td>Multi-byte data is received high-byte-first.</td></tr><tr><td>*byteOrder*=1:</td><td>Multi-byte data is received low-byte-first.</td></tr></tbody></table>
|  | This form of the /B flag requires NIGPIB2 version 1.11 or later. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type* . The default value is 8 (signed byte). |
| <span class="table-cell-nowrap">/Y = {*o*, *m*}</span> | *o* is offset, *m* is multiplier. /Y is used to scale integer data into real numbers. |
|  | <code class="igor"> output data = (input data + offset) * multiplier</code> |

### *Details* {#gpibreadbinarywave2-details}
If multiple waves are specified, all of the values for the first wave are read, followed by all of the values for the second wave, and so on.

If a wave is complex, GPIBReadBinaryWave2 reads two values for each point in that wave. This is true regardless of the /TYPE=*type* flag.

GPIBReadBinaryWave2 sets the variable V_flag, after creating it if necessary, to the number of  waves (not points) read.

### *Examples* {#gpibreadbinarywave2-examples}
This command tells the NI-488.2 driver which device to communicate with.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
```

This command reads two-byte signed integer binary numbers into each point of wave using low-byte-first byte order.

```igor
GPIBReadBinaryWave2/TYPE=(0x10)/B=1 wave0
```

This command reads a four-byte signed integer binary number into each point of wave0, wave1 and wave2 using low-byte-first byte order. All of wave0 is read first, then all of wave1, then all of wave2.

```igor
GPIBReadBinaryWave2/TYPE=(0x20)/B=1 wave0, wave1, wave2
```

This command reads eight-byte IEEE floating point binary numbers into wave0 using low-byte-first byte order.

```igor
GPIBReadBinaryWave2/B/TYPE=4/B=1 wave0
```

This command reads two-byte signed integer binary numbers into each point of wave using low-byte-first byte order. Then it adds 0 to each point and multiplies by .25. This would be used to scale integer data where 1 count represents .25 volts, for example.

```igor
GPIBReadBinaryWave2/TYPE=(0x10)/B=1/Y={0,0.25} wave0
```


<div className="command-signature">

## <strong>GPIBWrite2</strong>  [ /Q ] <em>str</em> {#gpibwrite2}

</div>

Transmits contents of the string argument.

### *Parameters* {#gpibwrite2-parameters}
*str*  is a string expression.

### *Flags* {#gpibwrite2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

### *Details* {#gpibwrite2-details}
GPIBWrite2 sets the variable V_flag to 1 if the write succeeded or to zero otherwise.

### *Examples* {#gpibwrite2-examples}
This command tells the NI-488.2 driver which device to communicate with.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
```

This command transmits a greeting followed by a carriage return.

```igor
GPIBWrite2 "Hello" + "\r"
```

This example transmits the contents of variable v1, the sine of .5 radians and the contents of point 0 of wave1, separated by tabs with a carriage return and linefeed at the end.

```igor
String str
sprintf str, "%g\t%g\t%g\r\n", v1, sin(.5), wave1[0]
GPIBWrite2 str
```


<div className="command-signature">

## <strong>GPIBWriteWave2</strong>  [ /R=[ <em>start</em> , <em>end</em>  ] /F={<em>numericFormatStr</em>, <em>leaderStr</em>, <em>separatorStr</em>, <em>terminatorStr</em> }  /Q ] <em>waveName</em>  [,<em>waveName</em>] {#gpibwritewave2}

</div>

Transmits contents of wave or waves as text.

The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and GPIBWriteWave2 writes two values for each wave point.

### *Parameters* {#gpibwritewave2-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F = {*numericFormatStr, leaderStr, separatorStr, terminatorStr* }</span> |  |
|  | *numericFormatStr*  is the numeric format string used to generate the output text for each numeric wave point. GPIBWriteWave2 passes this string to the C sprintf function. The default value is "%g". |
|  | Only numeric formats are allowed. *numericFormatStr* must end with a numeric conversion character. See [Printf](/igorpro/commands/printf.md) for details on formats. |
|  | *leaderStr* is text that is inserted at the start of each line of data. The default is "". |
|  | *separatorStr* is text that is inserted between each pair of points. The default is "\\t" (tab). |
|  | *terminatorStr* is text that is written at the end of each line of data. The default is "\\r" (carriage-return). |
| <span class="table-cell-nowrap">/R = [start,end]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to write data from. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

### *Details* {#gpibwritewave2-details}
If the /R flag is omitted, GPIBWriteWave2 writes values for point 0 through point n-1 where n is the number of points in the first wave.

GPIBWriteWave2 sets the variable V_flag, after creating it if necessary, to the number of individual numbers written.

GPIBWriteWave2 works with 64-bit integer data but is limited to 53 bits of precision. See [NIGPIB2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-64-bit-integer-limitations) for details.

### *Examples* {#gpibwritewave2-examples}
This command transmits contents of the waves as text, using 15 digits of precision, with a comma between numbers and CRLF at the end of each line.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
GPIBWriteWave2/F={"%.15g", "", ",", "\r\n"} wave1,wave2,wave3
```

<div className="command-signature">

## <strong>GPIBWriteBinary2</strong>  [ <em>flags</em> ] <em>argument</em>  [,<em>argument</em> ] {#gpibwritebinary2}

</div>

Transmits contents of the argument or arguments as binary data. The binary data can be sent as integers of one, two or four bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

### *Parameters* {#gpibwritebinary2-parameters}
*argument* is a numeric expression.

### *Flags* {#gpibwritebinary2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Multi-byte data is sent low-byte-first. Without /B, multi-byte data is sent high-byte-first. This flag affects sending of numeric data only, not string data. |
|  | See [NIGPIB2 Binary Operations Byte Order](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-binary-operations-byte-order) for details. |
| /B=*byteOrder* |<table class="nested-table"><tbody><tr><td>*byteOrder*=0:</td><td>Multi-byte data is sent high-byte-first.</td></tr><tr><td>*byteOrder*=1:</td><td>Multi-byte data is sent low-byte-first.</td></tr></tbody></table>
|  | This form of the /B flag requires NIGPIB2 version 1.11 or later. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |

### *Details* {#gpibwritebinary2-details}
GPIBWriteBinary2 sets the variable V_flag, after creating it if necessary, to the number of  items written.

GPIBWriteBinary2 can not transmit strings. Use [GPIBWrite2](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-command-line-operations.md#gpibwrite2) for that. GPIBWriteBinary2 can also not transmit complex values.

GPIBWriteBinary2 works with 64-bit integer data but is limited to 53 bits of precision. See [NIGPIB2 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-64-bit-integer-limitations) for details.

### *Examples* {#gpibwritebinary2-examples}
This command tells the NI-488.2 driver which device to communicate with.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
```

This command writes 123 and -456 as two-byte signed integer binary numbers using low-byte-first byte order. The high order byte of each number is transfered first.

```igor
GPIBWriteBinary2/TYPE=(0x10)/B=1 123, -456
```

This command writes 2*PI and -PI/2 as 32-bit IEEE floating point binary numbers using low-byte-first byte order.

```igor
GPIBWriteBinary2/TYPE=2/B=1 2*PI, -PI/2
```


<div className="command-signature">

## <strong>GPIBWriteBinaryWave2</strong>  [ <em>flags</em> ] <em>waveName</em>  [,<em>waveName</em>] {#gpibwritebinarywave2}

</div>

Writes binary data from the waves named in wavelist. The waves can be of any numeric data type.

### *Flags* {#gpibwritebinarywave2-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Multi-byte data is sent low-byte-first. Without /B, multi-byte data is sent high-byte-first. This flag affects sending of numeric data only, not string data. |
|  | See [NIGPIB2 Binary Operations Byte Order](/igorpro/extensions/data-acquisition/nigpib2/nigpib2-xop.md#nigpib2-binary-operations-byte-order) for details. |
| /B=*byteOrder* |<table class="nested-table"><tbody><tr><td>*byteOrder*=0:</td><td>Multi-byte data is sent high-byte-first.</td></tr><tr><td>*byteOrder*=1:</td><td>Multi-byte data is sent low-byte-first.</td></tr></tbody></table>
|  | This form of the /B flag requires NIGPIB2 version 1.11 or later. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |

### *Details* {#gpibwritebinarywave2-details}
The waves can be of any numeric data type, real or complex.

If multiple waves are specified, all of the values for the first wave are written, followed by all of the values for the second wave, and so on.

If a wave is complex, GPIBWriteBinaryWave2 writes two values for each point in that wave. This is true regardless of the /TYPE=*type* flag.

GPIBWriteBinaryWave2 sets the variable V_flag, after creating it if necessary, to the number of  waves (not points) written.

### *Examples* {#gpibwritebinarywave2-examples}
This command tells the NI-488.2 driver which device to communicate with.

```igor
GPIB2 device=unitDeviceDescriptor	// Unit descriptor from ibfind or ibdev
```

This command writes each point of wave0 as a two-byte signed integer binary number using low-byte-first byte order.

```igor
GPIBWriteBinaryWave2/TYPE=(0x10)/B=1 wave0
```

This command writes all of wave0 as a four-byte signed integer binary number using low-byte-first byte order, followed by all of wave1 and then all of wave2.

```igor
GPIBWriteBinaryWave2/TYPE=(0x20)/B=1 wave0, wave1, wave2
```

This command writes each point of wave0 as a 32-bit IEEE floating point binary number using low-byte-first byte order.

```igor
GPIBWriteBinaryWave2/TYPE=2/B=1 wave0
```