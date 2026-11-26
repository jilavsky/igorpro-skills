---
description: "The VISA XOP adds the following low-level functions to Igor. These functions provide direct access to VISA library functions."
slug: /extensions/data-acquisition/visa/visa-xop-functions
---

The VISA XOP adds the following low-level functions to Igor. These functions provide direct access to VISA library functions. VISA library functions that are not supported by VISA XOP are also noted in this list.

:::note
In addition to these low-level functions, VISA XOP also adds higher-level [VISA XOP Operations](#visa-xop-operations).
:::

## Resource Manager {#resource-manager}

| Function | Details |
| --- | --- |
| [viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm) | Opens a session with the VISA default resource manager. |
| [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen) | Opens a session with an instrument. |
| [viFindRsrc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindrsrc) | Find what instruments are available for use. |
| [viFindNext](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindnext) | Used with viFindRsrc to find successive instruments. |
| viParseRsrc | viParseRsrc is not supported by VISA XOP. |
| viParseRsrcEx | viParseRsrcEx is not supported by VISA XOP. |

## Resource Template {#resource-template}

| Function | Details |
| --- | --- |
| [viClose](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viclose) | Closes a session opened with viOpenDefaultRM or viOpen. |
| [viSetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattribute) | Sets a numeric attribute of a VISA interface or instrument. |
| [viSetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattributestring) | Sets a string attribute of a VISA interface or instrument. |
| [viGetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattribute) | Gets a numeric attribute of a VISA interface or instrument. |
| [viGetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattributestring) | Gets a string attribute of a VISA interface or instrument. |
| [viStatusDesc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vistatusdesc) | Returns a string description of a VISA status code. |
| [viTerminate](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viterminate) | Terminates an asynchronous job. |
| [viLock](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vilock) | Locks a resource. |
| [viUnlock](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunlock) | Unlocks  resource. |
| [viEnableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vienableevent) | Enables event notification. |
| [viDisableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidisableevent) | Disables event notification. |
| [viDiscardEvents](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidiscardevents) | Discards event notifications. |
| [viWaitOnEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwaitonevent) | Waits until an event has occurred. |
| viInstallHandler | viInstallHandler is not supported by VISA XOP. |
| viUninstallHandler | viUninstallHandler is not supported by VISA XOP. |

## Basic I/O {#basic-i-o}

| Function | Details |
| --- | --- |
| [viRead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viread) | Reads data into a string variable. |
| viReadAsync | viReadAsync is not supported by VISA XOP. |
| viReadToFile | viReadToFile is not supported by VISA XOP. |
| [viWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwrite) | Writes data from a string variable. |
| viWriteAsync | viWriteAsync is not supported by VISA XOP. |
| viWriteFromFile | viWriteFromFile is not supported by VISA XOP. |
| [viAssertTrigger](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viasserttrigger) | Generates a trigger signal. |
| [viReadSTB](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vireadstb) | Reads an instrument's status byte. |
| [viClear](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viclear) | Performs a "device-clear" operation. |

## Formatted and Buffered I/O {#formatted-and-buffered-i-o}

| Function | Details |
| --- | --- |
| viSetBuf | viSetBuf is not supported by VISA XOP. |
| viFlush | viFlush is not supported by VISA XOP. |
| viBufWrite | viBufWrite is not supported by VISA XOP. |
| viBufRead | viBufRead is not supported by VISA XOP. |
| viPrintf | viPrintf is not supported by VISA XOP. |
| viVPrintf | viVPrintf is not supported by VISA XOP. |
| viSPrintf | viSPrintf is not supported by VISA XOP. |
| viVSPrintf | viVSPrintf is not supported by VISA XOP. |
| viScanf | viScanf is not supported by VISA XOP. |
| viVScanf | viVScanf is not supported by VISA XOP. |
| viSScanf | viSScanf is not supported by VISA XOP. |
| viVSScanf | viVSScanf is not supported by VISA XOP. |
| viQueryf | viQueryf is not supported by VISA XOP. |
| viVQueryf | viVQueryf is not supported by VISA XOP. |

## Memory I/O {#memory-i-o}

| Function | Details |
| --- | --- |
| [viIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin8) | Reads a one-byte value from a VXI board. Not supported by TekVISA. |
| [viOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout8) | Writes a one-byte value to a VXI board. Not supported by TekVISA. |
| [viIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin16) | Reads a two-byte value from a VXI board. Not supported by TekVISA. |
| [viOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout16) | Writes a two-byte value to a VXI board. Not supported by TekVISA. |
| [viIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin32) | Reads a four-byte value from a VXI board. Not supported by TekVISA. |
| [viOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout32) | Writes a four-byte value to a VXI board. Not supported by TekVISA. |
| [viMoveIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein8) | Reads multiple one-byte values from a VXI board. Not supported by TekVISA. |
| [viMoveOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout8) | Writes multiple one-byte values to a VXI board. Not supported by TekVISA. |
| [viMoveIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein16) | Reads multiple two-byte values from a VXI board. Not supported by TekVISA. |
| [viMoveOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout16) | Writes multiple two-byte values to a VXI board. Not supported by TekVISA. |
| [viMoveIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein32) | Reads multiple four-byte values from a VXI board. Not supported by TekVISA. |
| [viMoveOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout32) | Writes multiple four-byte values to a VXI board. Not supported by TekVISA. |
| viMoveAsync | viMoveAsync is not supported by VISA XOP. |
| [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress) | Maps VXI register space into memory space. Not supported by TekVISA. |
| [viUnmapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunmapaddress) | Frees up memory space previously mapped by viMapAddress. Not supported by TekVISA. |
| [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8) | Reads a one-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |
| [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8) | Writes a one-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |
| [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16) | Reads a two-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |
| [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16) | Writes a two-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |
| [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32) | Reads a four-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |
| [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32) | Writes a four-byte value using an address obtained from viMapAddress. Not supported by TekVISA. |

## Shared Memory {#shared-memory}

| Function | Details |
| --- | --- |
| [viMemAlloc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemalloc) | Allocates memory on a VXI board. Not supported by TekVISA. |
| [viMemFree](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemfree) | Frees memory on a VXI board. Not supported by TekVISA. |

## Interface Specific {#interface-specific}

| Function | Details |
| --- | --- |
| [viGpibControlREN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolren) | Controls the GPIB remote enable signal. Not supported by TekVISA. |
| [viGpibControlATN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolatn) | Controls the GPIB attention signal. Not supported by TekVISA. |
| [viGpibSendIFC](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibsendifc) | Sends the GPIB interface-clear signal. Not supported by TekVISA. |
| [viGpibCommand](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcommand) | Sends controller GPIB command bytes to the GPIB bus. Not supported by TekVISA. |
| [viGpibPassControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibpasscontrol) | Passes GPIB control to another controller. Not supported by TekVISA. |
| [viVxiCommandQuery](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vivxicommandquery) | Sends a command or query to a VXI device. Not supported by TekVISA. |
| [viAssertUtilSignal](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viassertutilsignal) | Controls a utility bus signal. Not supported by TekVISA. |
| [viAssertIntrSignal](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viassertintrsignal) | Controls an interrupt signal. Not supported by TekVISA. |
| [viMapTrigger](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimaptrigger) | Maps a trigger source to a trigger destination. Not supported by TekVISA. |
| [viUnmapTrigger](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunmaptrigger) | Unmaps a trigger signal. Not supported by TekVISA. |
| [viUsbControlOut](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viusbcontrolout) | Sends data to a USB device. Not supported by TekVISA. |
| [viUsbControlIn](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viusbcontrolin) | Reads data from a USB device. Not supported by TekVISA. |


## Errors and Status Codes From VISA XOP Functions {#errors-and-status-codes-from-visa-xop-functions}

When you call a VISA function from Igor, you are calling an Igor function added by the VISA XOP. The VISA XOP in turn calls a VISA library function.
Each VISA library function returns a status code which indicates if the function succeeded or failed. Status codes greater than or equal to zero indicate success. Status codes less than zero indicate failure.

Each VISA XOP function calls one VISA library function. The function result returned by the Igor VISA function is the status code returned by the VISA library function. In the event of a failure (status code less than zero) you can get a human-readable message by calling viStatusDesc. See the example under [viStatusDesc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vistatusdesc). There is one special status code. -1 indicates that an error occurred in the VISA XOP function before it made any calls to the corresponding VISA library function.

In addition to the status code which is returned to your user-defined Igor function, each VISA XOP function returns an error code to Igor. Your user-defined Igor function does not see this error code. If the error code is non-zero, Igor aborts function execution and reports the error to the user. VISA XOP functions do not return errors to Igor to indicate a failure status returned by a VISA library function. They return errors to Igor only to indicate programming errors such as "out-of-memory" or passing a null (uninitialized) string variable as a parameter. You can test for Igor errors by calling [GetRTError](/igorpro/commands/getrterror.md), but in general this is not necessary because they are programming errors that need to be fixed by the Igor programmer (you), not VISA library failures that need to be gracefully handled by your code.

See the example under [viFindRsrc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindrsrc) for an example of handling VISA library failure status codes.
<br>



<div className="command-signature">

## <strong>viOpenDefaultRM</strong> (<em>session</em>) {#viopendefaultrm}

</div>

Opens the VISA default resource manager and returns a session ID via *session* .

The function result is a VISA status code.

### *Parameters* {#parameters}
*session*  is an output. On return it contains a session ID which can be passed to viOpen to open an instrument session.

### *Details* {#details}
You must open a default resource manager session before doing anything else with VISA.

See the VISA library documentation for further details.

See [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen) for an example.

### *See Also* {#see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viClose](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viclose)








<div className="command-signature">

## <strong>viOpen</strong> (<em>session</em> , <em>resourceName</em> , <em>accessMode</em> , <em>openTimeout</em> , <em>instr</em> ) {#viopen}

</div>

Opens a session with the instrument specified by resourceName.

The function result is a VISA status code.

### *Parameters* {#viopen-parameters}
*session* is a value returned by viOpenDefaultRM.

*instr* is an output. On return it contains an instrument session ID which can be passed to viRead, viWrite, viClose and so on.

### *Details* {#viopen-details}
See the VISA library documentation for further details.

### *Examples* {#examples}

```igor
Variable defaultRM, instr
String resourceName = "GPIB0::1::INSTR"

viOpenDefaultRM(defaultRM)
viOpen(defaultRM, resourceName, 0, 0, instr)

// Do something with instr
viClose(instr)
viClose(defaultRM)
```

### *See Also* {#viopen-see-also}
[viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm), [viClose](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viclose)








<div className="command-signature">

## <strong>viFindRsrc</strong> (<em>session</em> , <em>expr</em> , <em>findList</em> , <em>retcnt</em> , <em>instrDesc</em> ) {#vifindrsrc}

</div>

Finds the first resource matching *expr*  and sets up for subsequent calls to viFindNext.

The function result is a VISA status code.

### *Parameters* {#vifindrsrc-parameters}
*session* is a value returned by viOpenDefaultRM.

*expr* is is a regular expression indicating what type of resources you want to find. See National Instruments' documentation for viFindRsrc for the regular expression rules. They are different from Igor's regular expression rules.

*findList* is an output. It is used with subsequent calls to viFindNext.

*retcnt* is the number of resources that match *expr*  and is used to control the number of subsequent calls to viFindNext.

*instrDesc* is an output. It is the description of the first resource found and can be passed to viOpen.

### *Details* {#vifindrsrc-details}
Unlike calling viFindRsrc from C, when calling from Igor, you can not pass NULL for the *findList*  parameter. Thus you must call viClose on the VISA object whose reference is returned in *findList* .

The value returned in findList is a VISA object and must be passed to viClose when you are finished with it.

See the VISA library documentation for further details.

### *Examples* {#vifindrsrc-examples}

```igor
Function Example()
    Variable defaultRM=0, findList=0, retcnt
    String expr, instrDesc
    Variable i, status=0

    do		// Just a structure to break out of in case of error
        expr = "ASRL?*INSTR"			// Match all serial instruments.
        status = viOpenDefaultRM(defaultRM)
        if (status < 0)
            break
        endif

        status = viFindRsrc(defaultRM, expr, findList, retcnt, instrDesc)
        if (status < 0)
            break
        endif

        if (retcnt <= 0)
            break
        endif

        i = 1
        do
            Printf "Instrument %d: %s\r", i, instrDesc
            i += 1

            if (i > retcnt)
                break
            endif

            status = viFindNext(findList, instrDesc)
            if (status < 0)
                break
            endif

        while(1)
    while(0)

    if (status < 0)
        String errorDesc
        Variable viObject

        viObject = findList

        if (viObject == 0)
            viObject = defaultRM
        endif

        viStatusDesc(viObject, status, errorDesc)
        Printf "VISA Error: %s\r", errorDesc
    endif

    if (findList != 0)
        viClose(findList)
    endif

    if (defaultRM != 0)
        viClose(defaultRM)
    endif

    return status
End
```

### *See Also* {#vifindrsrc-see-also}
[viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm), [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viFindNext](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindnext)








<div className="command-signature">

## <strong>viFindNext</strong> (<em>findList</em> , <em>instrDesc</em> ) {#vifindnext}

</div>

Finds the next resource. viFindNext is called after viFindRsrc.

The function result is a VISA status code.

### *Parameters* {#vifindnext-parameters}
*findList* is an object reference returned by viFindRsrc.

*instrDesc* is an output. It is the description of the next resource found and can be passed to viOpen.

### *Details* {#vifindnext-details}
See the VISA library documentation for further details.

### *Examples* {#vifindnext-examples}
See the example under [viFindRsrc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindrsrc).

### *See Also* {#vifindnext-see-also}
[viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm), [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viFindRsrc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vifindrsrc)








<div className="command-signature">

## <strong>viClose</strong> (<em>session</em> ) {#viclose}

</div>

Closes a session.

The function result is a VISA status code.

### *Parameters* {#viclose-parameters}
*session* is a value returned by viOpenDefaultRM or viOpen.

### *Details* {#viclose-details}
See the VISA library documentation for further details.

See [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen) for an example.

### *See Also* {#viclose-see-also}
[viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm), [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen)








<div className="command-signature">

## <strong>viSetAttribute</strong> (<em>vi</em> , <em>attribute</em> , <em>attrState</em>  ) {#visetattribute}

</div>

Sets the value of a numeric attribute of a VISA interface or instrument .

The function result is a VISA status code.

### *Parameters* {#visetattribute-parameters}
*vi* is a VISA object reference obtained from viOpen.

*attribute* is an attribute constant as defined in the VISA.ipf Igor procedure file.

*attrState* is the new value to which the attribute is to be set.

### *Details* {#visetattribute-details}
viSetAttribute works with numeric attributes only. It does not work with string attributes. For string attributes, use [viSetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattributestring).

viSetAttribute does not support attributes of type ViAddr, ViBuf or ViAUInt8, or with any attributes not defined in VISA.h from VISA 3.0, or with any non-standard attributes such as VI_ATTR_PXI_* and VI_ATTR_USB_*.

See the VISA library documentation for viSetAttribute further details.

### *Example* {#example}

```igor
Function VISASetAttrBaud(instr, baud)
    Variable instr			// An instrument referenced obtained from viOpen
    Variable baud
    Variable status

    status = viSetAttribute(instr, VI_ATTR_ASRL_BAUD, baud)
    return status
End
```

### *See Also* {#visetattribute-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viSetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattributestring), [viGetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattribute)








<div className="command-signature">

## <strong>viSetAttributeString</strong> (<em>vi</em> , <em>attribute</em> , <em>attrStateStr</em>  ) {#visetattributestring}

</div>

Sets the value of a string attribute of a VISA interface or instrument .

The function result is a VISA status code.

### *Parameters* {#visetattributestring-parameters}
*vi* is a VISA object reference obtained from viOpen.

*attribute* is an attribute constant as defined in the VISA.ipf Igor procedure file.

*attrStateStr* is the new value to which the attribute is to be set.

### *Details* {#visetattributestring-details}
viSetAttributeString does not correspond to a VISA library function of the same name. It corresponds viSetStringAttribute for ViString and ViRsrc-type attributes.

As of this writing, VISA defines no read/write attributes of these types.

viSetAttributeString works with ViString and ViRsrc-type attributes only. It does not work with numeric attributes. For numeric attributes, use [viSetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattribute).

viSetAttributeString does not support attributes of type ViAddr, ViBuf or ViAUInt8, or with any attributes not defined in VISA.h from VISA 3.0, or with any non-standard attributes such as VI_ATTR_PXI_* and VI_ATTR_USB_*.

See the VISA library documentation for viSetAttribute further details.



### *See Also* {#visetattributestring-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viSetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattribute), [viGetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattributestring)








<div className="command-signature">

## <strong>viGetAttribute</strong> (<em>vi</em> , <em>attribute</em> , <em>attrState</em>  ) {#vigetattribute}

</div>

Gets the value of a numeric attribute of a VISA interface or instrument which is returned via *attrState* .

The function result is a VISA status code.

### *Parameters* {#vigetattribute-parameters}
*vi* is a VISA object reference obtained from viOpen.

*attribute* is an attribute constant as defined in the VISA.ipf Igor procedure file.

*attrState* is an output. On return it contains the value of the attribute.

### *Details* {#vigetattribute-details}
viGetAttribute works with numeric attributes only. It does not work with string attributes. For string attributes, use [viGetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattributestring).

viGetAttribute does not support attributes of type ViAddr, ViBuf or ViAUInt8, or with any attributes not defined in VISA.h from VISA 3.0, or with any non-standard attributes such as VI_ATTR_PXI_* and VI_ATTR_USB_*.

See the VISA library documentation for viGetAttribute further details.

### *Example* {#vigetattribute-example}

```igor
Function VISAGetAttrBaud(instr, baud)
    Variable instr			// An instrument referenced obtained from viOpen
    Variable &baud			// Output

    Variable status
    status = viGetAttribute(instr, VI_ATTR_ASRL_BAUD, baud)
    return status
End
```

### *See Also* {#vigetattribute-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattributestring), [viSetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattribute)








<div className="command-signature">

## <strong>viGetAttributeString</strong> (<em>vi</em> , <em>attribute</em> , <em>attrStateStr</em>  ) {#vigetattributestring}

</div>

Gets the value of a string attribute of a VISA interface or instrument which is returned via *attrStateStr* .

The function result is a VISA status code.

### *Parameters* {#vigetattributestring-parameters}
*vi* is a VISA object reference obtained from viOpen.

*attribute* is an attribute constant as defined in the VISA.ipf Igor procedure file.

*attrStateStr* is an output. On return it contains the value of the attribute.

### *Details* {#vigetattributestring-details}
viGetAttributeString does not correspond to a VISA library function of the same name. It corresponds viGetStringAttribute for ViString and ViRsrc-type attributes.

viGetAttributeString works with ViString and ViRsrc-type attributes only. It does not work with numeric attributes. For numeric attributes, use [viGetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattribute).

viGetAttributeString does not support attributes of type ViAddr, ViBuf or ViAUInt8, or with any attributes not defined in VISA.h from VISA 3.0, or with any non-standard attributes such as VI_ATTR_PXI_* and VI_ATTR_USB_*.

### *Example* {#vigetattributestring-example}

```igor
Function VISAGetAttrRsrcClass(instr, name)
    Variable instr			// An instrument referenced obtained from viOpen
    String &name			// Output

    Variable status
    status = viGetAttributeString(instr, VI_ATTR_RSRC_NAME, name)
    return status
End
```

### *See Also* {#vigetattributestring-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGetAttributeString](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigetattributestring), [viSetAttribute](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visetattribute)








<div className="command-signature">

## <strong>viStatusDesc</strong> (<em>vi</em> , <em>status</em> , <em>desc</em> ) {#vistatusdesc}

</div>

Returns via *desc* a string description of a VISA status code.

The function result is a VISA status code.

### *Parameters* {#vistatusdesc-parameters}
*vi* is a value returned by viOpenDefaultRM or viOpen.

*status* is a result returned by any VISA library call.

*desc* is a string variable. On return it contains a description of the status code.

### *Details* {#vistatusdesc-details}
See the VISA library documentation for further details.

### *Example* {#vistatusdesc-example}

```igor
// ReportVISAError is defined in the VISA.ipf procedure file.

Function ReportVISAError(name, session, status)
    String name                 // VISA function name, e.g., viRead or other identifier
    Variable session            // Session ID obtained from viOpen
    Variable status             // Status code from VISA library

    String desc
    viStatusDesc(session, status, desc)
    Printf "%s error (%x): %s\r", name, status, desc
    Beep
End

// This function illustrates the use of ReportVISAError which calls viStatusDesc.

Function Test()
    Variable status
    Variable defaultRM
    String resourceName = "GPIB0::1::INSTR"

    Variable instr = 0
    status = viOpenDefaultRM(defaultRM)

    if (status < 0)
    ReportVISAError("viOpenDefaultRM", instr, status)
    return status               // Failure
    endif

    status = viOpen(defaultRM, resourceName, 0, 0, instr)
    if (status < 0)
    viClose(defaultRM)
    ReportVISAError("viOpen", instr, status)
    return status               // Failure
    endif

    // Do something with instr

    viClose(instr)
    viClose(defaultRM)
    return 0                    // Success
End
```

### *See Also* {#vistatusdesc-see-also}
[viOpenDefaultRM](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopendefaultrm), [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen)








<div className="command-signature">

## <strong>viTerminate</strong> (<em>vi</em> , <em>degree</em> , <em>jobId</em> ) {#viterminate}

</div>

Requests termination of an operation.

The function result is a VISA status code.

### *Parameters* {#viterminate-parameters}
*vi* is a value returned by viOpenDefaultRM or viOpen.

*degree* must always be zero.

*jobId* specifies the operation to terminate.

### *Details* {#viterminate-details}
See the VISA library documentation for further details.

This function is untested.








<div className="command-signature">

## <strong>viLock</strong> (<em>vi</em> , <em>lockType</em> , <em>timeout</em> , <em>requestedKeyStr</em> , <em>accessKeyStr</em> ) {#vilock}

</div>

Sets access mode for a resource.

The function result is a VISA status code.

### *Parameters* {#vilock-parameters}
*vi* is a value returned by viOpen.

*lockType* is `VI_EXCLUSIVE_LOCK` or `VI_SHARED_LOCK`.

*timeout* specifies the time in milliseconds to wait for resource to be free.

*requestedKeyStr* is the key to use for a shared lock. It is ignored if lockType is `VI_EXCLUSIVE_LOCK`.

*accessKeyStr* is an output. It is set to "" if lockType is `VI_EXCLUSIVE_LOCK`.

### *Details* {#vilock-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vilock-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viUnlock](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunlock)








<div className="command-signature">

## <strong>viUnlock</strong> (<em>vi</em>) {#viunlock}

</div>

Releases a lock.

The function result is a VISA status code.

### *Parameters* {#viunlock-parameters}
*vi* is a value returned by viOpen.

### *Details* {#viunlock-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viunlock-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viLock](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vilock)








<div className="command-signature">

## <strong>viEnableEvent</strong> (<em>vi</em> , <em>eventType</em> , <em>mechanism</em>, <em>context</em> ) {#vienableevent}

</div>

Tells the VISA library that you are interested in the specified event.

Later you would use [viWaitOnEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwaitonevent) to see if the event occurred.

The function result is a VISA status code.

### *Parameters* {#vienableevent-parameters}
*vi* is a session identifier returned by viOpen.

*eventType* is one of the `VI_EVENT` constants defined in VISA.h (for C) and VISA.ipf (for Igor).

*mechanism* specifies how the event is to be handled. With VISA XOP, the only legal value is `VI_QUEUE`.

*context* must always be zero.

### *Details* {#vienableevent-details}
See the VISA library documentation for further details.

### *See Also* {#vienableevent-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viDisableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidisableevent), [viDiscardEvents](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidiscardevents), [viWaitOnEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwaitonevent)








<div className="command-signature">

## <strong>viDisableEvent</strong> (<em>vi</em> , <em>eventType</em> , <em>mechanism</em>, <em>context</em> ) {#vidisableevent}

</div>

Tells the VISA library that you are not interested in the specified event.

The function result is a VISA status code.

### *Parameters* {#vidisableevent-parameters}
*vi* is a session identifier returned by viOpen.

*eventType* is one of the `VI_EVENT` constants defined in VISA.h (for C) and VISA.ipf (for Igor).

*mechanism* specifies how the event is to be handled. With VISA XOP, the only legal value is `VI_QUEUE`.

*context* must always be zero.

### *Details* {#vidisableevent-details}
See the VISA library documentation for further details.

### *See Also* {#vidisableevent-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viEnableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vienableevent), [viDiscardEvents](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidiscardevents), [viWaitOnEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwaitonevent)








<div className="command-signature">

## <strong>viDiscardEvents</strong> (<em>vi</em> , <em>eventType</em> , <em>mechanism</em>, <em>context</em> ) {#vidiscardevents}

</div>

Discards specified events in the event queue.

The function result is a VISA status code.

### *Parameters* {#vidiscardevents-parameters}
*vi* is a session identifier returned by viOpen.

*eventType* is one of the `VI_EVENT` constants defined in VISA.h (for C) and VISA.ipf (for Igor).

*mechanism* specifies how the event is to be handled. With VISA XOP, the only legal value is `VI_QUEUE`.

*context* must always be zero.

### *Details* {#vidiscardevents-details}
See the VISA library documentation for further details.

### *See Also* {#vidiscardevents-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viEnableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vienableevent), [viDisableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidisableevent), [viWaitOnEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwaitonevent)








<div className="command-signature">

## <strong>viWaitOnEvent</strong> (<em>vi</em> , <em>inEventType</em> , <em>timeout</em> , <em>outEventType</em> , <em>outContext</em>) {#viwaitonevent}

</div>

Waits till the specified event occurs or until a timeout occurs.

The function result is a VISA status code.

### *Parameters* {#viwaitonevent-parameters}
*vi* is a session identifier returned by viOpen.

*inEventType* is one of the `VI_EVENT` constants defined in VISA.h (for C) and VISA.ipf (for Igor).

*timeout* is the maximum time in milliseconds to wait for the event to occur.

*outEventType* is an output and returns the type of event that occurred. It is one of the `VI_EVENT` constants defined in VISA.h (for C) and VISA.ipf (for Igor).

*outContext* is an output and identifies a unique occurrence of an event. If viWaitOnEvent succeeds then you must call viClose on *outContext* when you are finished with the event.

### *Details* {#viwaitonevent-details}
See the VISA library documentation for further details.

### *See Also* {#viwaitonevent-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viEnableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vienableevent), [viDisableEvent](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidisableevent), [viDiscardEvents](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vidiscardevents)








<div className="command-signature">

## <strong>viRead</strong> (<em>vi</em> , <em>buf</em> , <em>cnt</em> , <em>retCnt</em>) {#viread}

</div>

Reads data from an instrument into an Igor string variable.

For reading into a numeric wave, use [VISAReadWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadwave) or [VISAReadBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinary).

The function result is a VISA status code.

### *Parameters* {#viread-parameters}
*vi* is a session identifier returned by viOpen.

*buf* is the string variable to receive the data read from the instrument.

*cnt* is the number of bytes to read.

*retCnt* is an output and returns the number of bytes actually read.

### *Details* {#viread-details}
When reading binary data into a string, the VISA library may terminate the read prematurely unless you set the appropriate attributes. See [VISA Library Terminator Character Issues](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-library-terminator-character-issues) for details.

See the VISA library documentation for further details.

### *See Also* {#viread-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwrite), [VISARead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visaread), [VISAReadWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadwave), [VISAReadBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinary)








<div className="command-signature">

## <strong>viWrite</strong> (<em>vi</em> , <em>buf</em> , <em>cnt</em> , <em>retCnt</em>) {#viwrite}

</div>

Writes data from an Igor string variable to an instrument.

For reading into a numeric wave, use [VISAWriteWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritewave) or [VISAWriteBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritebinary).

The function result is a VISA status code.

### *Parameters* {#viwrite-parameters}
*vi* is a session identifier returned by viOpen.

*buf* is the string to write to the instrument.

*cnt* is the number of bytes to write. It must not be larger than the number of bytes in the string variable.

*retCnt* is an output and returns the number of bytes actually written.

### *Details* {#viwrite-details}
See the VISA library documentation for further details.

### *See Also* {#viwrite-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viRead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viread), [VISAWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawrite), [VISAWriteWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritewave), [VISAWriteBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritebinary)








<div className="command-signature">

## <strong>viAssertTrigger</strong> (<em>vi</em> , <em>protocol</em>  ) {#viasserttrigger}

</div>

Asserts a hardware or software trigger.

The function result is a VISA status code.

### *Parameters* {#viasserttrigger-parameters}
*vi* is a session identifier returned by viOpen.

*protocol* is one of the VI_TRIG constants defined in VISA.ipf.

### *Details* {#viasserttrigger-details}
See the VISA library documentation for further details.

### *See Also* {#viasserttrigger-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viRead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viread), [viWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwrite)








<div className="command-signature">

## <strong>viReadSTB</strong> (<em>vi</em> , <em>status</em>) {#vireadstb}

</div>

Reads an instrument's status byte.

The function result is a VISA status code.

### *Parameters* {#vireadstb-parameters}
*vi* is a session identifier returned by viOpen.

*status* is an output and returns the instrument's status byte.

### *Details* {#vireadstb-details}
See the VISA library documentation for further details.

### *See Also* {#vireadstb-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viRead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viread), [viWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwrite)








<div className="command-signature">

## <strong>viClear</strong> (<em>vi</em>  ) {#viclear}

</div>

Performs a "device-clear" operation on the instrument. What this means depends on the instrument.

The function result is a VISA status code.

### *Parameters* {#viclear-parameters}
*vi* is a session identifier returned by viOpen.

### *Details* {#viclear-details}
See the VISA library documentation for further details.

### *See Also* {#viclear-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viRead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viread), [viWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viwrite)








<div className="command-signature">

## <strong>viIn8</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em>) {#viin8}

</div>

Reads a one-byte value from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viin8-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a variable to receive the value read from the board.

### *Details* {#viin8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viin8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout8), [viMoveIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein8), [viMoveOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout8)








<div className="command-signature">

## <strong>viOut8</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em>) {#viout8}

</div>

Writes a one-byte value to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viout8-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a value to write to the board.

### *Details* {#viout8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viout8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin8), [viMoveIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein8), [viMoveOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout8)








<div className="command-signature">

## <strong>viIn16</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em>) {#viin16}

</div>

Reads a two-byte value from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viin16-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a variable to receive the value read from the board.

### *Details* {#viin16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viin16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout16), [viMoveIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein16), [viMoveOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout16)








<div className="command-signature">

## <strong>viOut16</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em>) {#viout16}

</div>

Writes a two-byte value to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viout16-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a value to write to the board.

### *Details* {#viout16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viout16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin16), [viMoveIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein16), [viMoveOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout16)








<div className="command-signature">

## <strong>viIn32</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em>) {#viin32}

</div>

Reads a four-byte value from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viin32-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a variable to receive the value read from the board.

### *Details* {#viin32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viin32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout32), [viMoveIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein32), [viMoveOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout32)








<div className="command-signature">

## <strong>viOut32</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>val</em> ) {#viout32}

</div>

Writes a four-byte value to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viout32-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*val* is a value to write to the board.

### *Details* {#viout32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viout32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin32), [viMoveIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein32), [viMoveOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout32)








<div className="command-signature">

## <strong>viMoveIn8</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>length</em> , <em>buf</em> ) {#vimovein8}

</div>

Reads multiple one-byte values from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimovein8-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of one-byte values to read.

*buf*  is a wave to receive the values read from the board. The wave must be a signed or unsigned byte (8-bit integer) wave and must be at least as long as *length*.

### *Details* {#vimovein8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimovein8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin8), [viOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout8), [viMoveOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout8)








<div className="command-signature">

## <strong>viMoveOut8</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>length</em> , <em>buf</em> ) {#vimoveout8}

</div>

Writes multiple one-byte values to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimoveout8-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of one-byte values to write.

*buf*  is a wave containing the values write to the board. The wave must be a signed or unsigned byte (8-bit integer) wave and must be at least as long as *length*.

### *Details* {#vimoveout8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimoveout8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin8), [viOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout8), [viMoveIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein8)








<div className="command-signature">

## <strong>viMoveIn16</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>length</em> , <em>buf</em> ) {#vimovein16}

</div>

Reads multiple two-byte values from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimovein16-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of two-byte values to read.

*buf* is a wave to receive the values read from the board. The wave must be a signed or unsigned short (16-bit integer) wave and must be at least as long as *length*.

### *Details* {#vimovein16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimovein16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin16), [viOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout16), [viMoveOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout16)








<div className="command-signature">

## <strong>viMoveOut16</strong> (<em>vi</em> , <em>space</em> , <em>offset</em> , <em>length</em> , <em>buf</em> ) {#vimoveout16}

</div>

Writes multiple two-byte values to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimoveout16-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of two-byte values to write.

*buf*  is a wave containing the values write to the board. The wave must be a signed or unsigned short (16-bit integer) wave and must be at least as long as *length*.

### *Details* {#vimoveout16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimoveout16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin16), [viOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout16), [viMoveIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein16)



<div className="command-signature">

## <strong>viMoveIn32</strong> (<em>vi</em>, <em>space</em>, <em>offset</em>, <em>length</em>, <em>buf</em>) {#vimovein32}

</div>

Reads multiple four-byte values from a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimovein32-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of four-byte values to read.

*buf* is a wave to receive the values read from the board. The wave must be a signed or unsigned long (32-bit integer) and must be at least as long as *length*.

### *Details* {#vimovein32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimovein32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin32), [viOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout32), [viMoveOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout32)




<div className="command-signature">

## <strong>viMoveOut32</strong> (<em>vi</em>, <em>space</em>, <em>offset</em>, <em>length</em>, <em>buf</em> ) {#vimoveout32}

</div>

Writes multiple four-byte values to a VXI board. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimoveout32-parameters}
*vi* is a session identifier returned by viOpen.

*space* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE`.

*offset* is the offset of the register to read.

*length* is the number of four-byte values to write.

*buf* is a wave containing the values write to the board. The wave must be a signed or unsigned long (32-bit integer) wave and must be at least as long as *length*.

### *Details* {#vimoveout32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimoveout32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viin32), [viOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viout32), [viMoveIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein32)



<div className="command-signature">

## <strong>viMapAddress</strong> (<em>vi</em>, <em>mapSpace</em>, <em>mapOffset</em>, <em>mapSize</em> , <em>access</em>, <em>suggested</em>, <em>address</em> ) {#vimapaddress}

</div>

Maps VXI register space into memory space. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is a VISA status code.

### *Parameters* {#vimapaddress-parameters}
*vi* is a session identifier returned by viOpen.

*mapSpace* is `VI_A16_SPACE`, `VI_A24_SPACE` or `VI_A32_SPACE` (defined in VISA.ipf).

*mapSize* specifies the number of bytes to map.

*access* must always be zero.

*suggested* is a suggested memory address or VI_NULL.

*address* is an output and specifies the mapped address. This is passed to one of the viPeek or viPoke routines.

### *Details* {#vimapaddress-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimapaddress-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viUnmapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunmapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)




<div className="command-signature">

## <strong>viUnmapAddress</strong> (<em>vi</em>) {#viunmapaddress}

</div>

Frees up memory space previously mapped by viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is a VISA status code.

### *Parameters* {#viunmapaddress-parameters}
*vi* is a session identifier returned by viOpen.

### *Details* {#viunmapaddress-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viunmapaddress-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)




<div className="command-signature">

## <strong>viPeek8</strong> (<em>vi</em>, <em>address</em>, <em>val</em>) {#vipeek8}

</div>

Reads a one-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipeek8-parameters}
*vi* is a session identifier returned by viOpen.

*address* is an address obtained from viMapAddress.

*val* is an output and is the value read.

### *Details* {#vipeek8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipeek8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)



<div className="command-signature">

## <strong>viPoke8</strong> (<em>vi</em> , <em>address</em>, <em>val</em>) {#vipoke8}

</div>

Writes a one-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipoke8-parameters}
*vi* is a session identifier returned by viOpen.

*address* is an address obtained from viMapAddress.

*val* is the value to be written.

### *Details* {#vipoke8-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipoke8-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)


<div className="command-signature">

## <strong>viPeek16</strong> (<em>vi</em>, <em>address</em>, <em>val</em>) {#vipeek16}

</div>

Reads a two-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipeek16-parameters}
*vi* is a session identifier returned by viOpen.

*val* is an output and is the value read.

*address* is an address obtained from viMapAddress.

### *Details* {#vipeek16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipeek16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)




<div className="command-signature">

## <strong>viPoke16</strong> (<em>vi</em>, <em>address</em>, <em>val</em>) {#vipoke16}

</div>

Writes a two-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipoke16-parameters}
*vi* is a session identifier returned by viOpen.

*address* is an address obtained from viMapAddress.

*val* is the value to be written.

### *Details* {#vipoke16-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipoke16-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)



<div className="command-signature">

## <strong>viPeek32</strong> (<em>vi</em>, <em>address</em>, <em>val</em>) {#vipeek32}

</div>

Reads a four-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipeek32-parameters}
*vi* is a session identifier returned by viOpen.

*val* is an output and is the value read.

*address* is an address obtained from viMapAddress.

### *Details* {#vipeek32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipeek32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)



<div className="command-signature">

## <strong>viPoke32</strong> (<em>vi</em>, <em>address</em>, <em>val</em>) {#vipoke32}

</div>

Writes a four-byte value using an address obtained from viMapAddress. Not supported by TekVISA.

This function is for expert VXI bus users.

The function result is always VI_SUCCESS (0).

### *Parameters* {#vipoke32-parameters}
*vi* is a session identifier returned by viOpen.

*address* is an address obtained from viMapAddress.

*val* is the value to be written.

### *Details* {#vipoke32-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vipoke32-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapAddress](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimapaddress), [viPeek8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek8), [viPoke8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke8), [viPeek16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek16), [viPoke16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke16), [viPeek32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipeek32), [viPoke32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vipoke32)



<div className="command-signature">

## <strong>viMemAlloc</strong> (<em>vi</em>, <em>size</em>, <em>offset</em>) {#vimemalloc}

</div>

Allocates memory on a VXI board. The memory can be accessed using viMove functions. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimemalloc-parameters}
*vi* is a session identifier returned by viOpen.

*size* is the number of bytes to allocate.

*offset* is an output and is used with viMove functions to access the memory.

### *Details* {#vimemalloc-details}
Call [viMemFree](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemfree) to free the memory.

See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimemalloc-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMemFree](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemfree), [viMoveIn8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein8), [viMoveOut8](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout8), [viMoveIn16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein16), [viMoveOut16](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout16), [viMoveIn32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimovein32), [viMoveOut32](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimoveout32)



<div className="command-signature">

## <strong>viMemFree</strong> (<em>vi</em>, <em>offset</em>) {#vimemfree}

</div>

Frees memory allocated with [viMemAlloc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemalloc). Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimemfree-parameters}
*vi* is a session identifier returned by viOpen.

*offset* is the value returned by viMemAlloc.

### *Details* {#vimemfree-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimemfree-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMemAlloc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimemalloc)



<div className="command-signature">

## <strong>viGpibControlREN</strong> (<em>vi</em>, <em>mode</em>) {#vigpibcontrolren}

</div>

Controls the GPIB remote-enable line. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vigpibcontrolren-parameters}
*vi* is a session identifier returned by viOpen.

*mode* specifies the state of the REN line.

### *Details* {#vigpibcontrolren-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vigpibcontrolren-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGpibControlATN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolatn), [viGpibSendIFC](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibsendifc), [viGpibCommand](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcommand), [viGpibPassControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibpasscontrol)



<div className="command-signature">

## <strong>viGpibControlATN</strong> (<em>vi</em>, <em>mode</em>) {#vigpibcontrolatn}

</div>

Controls the GPIB attention line. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vigpibcontrolatn-parameters}
*vi* is a session identifier returned by viOpen.

*mode* specifies the state of the ATN line.

### *Details* {#vigpibcontrolatn-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vigpibcontrolatn-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGpibControlREN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolren), [viGpibSendIFC](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibsendifc), [viGpibCommand](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcommand), [viGpibPassControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibpasscontrol)




<div className="command-signature">

## <strong>viGpibSendIFC</strong> (<em>vi</em>) {#vigpibsendifc}

</div>

Sends the GPIB interface-clear signal. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vigpibsendifc-parameters}
*vi* is a session identifier returned by viOpen.

### *Details* {#vigpibsendifc-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vigpibsendifc-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGpibControlREN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolren), [viGpibControlATN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolatn), [viGpibCommand](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcommand), [viGpibPassControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibpasscontrol)




<div className="command-signature">

## <strong>viGpibCommand</strong> (<em>vi</em>, <em>cmd</em>, <em>cnt</em>, <em>retCnt</em>) {#vigpibcommand}

</div>

Controls the GPIB attention line. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vigpibcommand-parameters}
*vi* is a session identifier returned by viOpen.

*cmd* is a signed or unsigned byte (8-bit integer) wave containing the data to sent. It must be at least as long as *cnt* .

*cnt* is the number of bytes to write.

*retCnt* is an output and returns the number of bytes actually written.

### *Details* {#vigpibcommand-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vigpibcommand-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGpibControlREN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolren), [viGpibControlATN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolatn), [viGpibSendIFC](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibsendifc), [viGpibPassControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibpasscontrol)



<div className="command-signature">

## <strong>viGpibPassControl</strong> (<em>vi</em>, <em>primAddr</em>, <em>secAddr</em>) {#vigpibpasscontrol}

</div>

Passes GPIB control to another controller. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vigpibpasscontrol-parameters}
*vi* is a session identifier returned by viOpen.

*primAddr* is the primary address of the new controller.

*secAddr* is the secondary address of the new controller or `VI_NO_SEC_ADDR` (a constant defined in VISA.ipf).

### *Details* {#vigpibpasscontrol-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vigpibpasscontrol-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viGpibControlREN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolren), [viGpibControlATN](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcontrolatn), [viGpibSendIFC](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibsendifc), [viGpibCommand](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vigpibcommand)




<div className="command-signature">

## <strong>viVxiCommandQuery</strong> (<em>vi</em>, <em>mode</em>, <em>cmd</em>, <em>response</em>) {#vivxicommandquery}

</div>

Sends a command or query to a VXI device. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vivxicommandquery-parameters}
*vi* is a session identifier returned by viOpen.

*mode* determines whether to send a command and/or get a response.

*cmd* is the command to send.

*response* is an output and returns the response from the device.

### *Details* {#vivxicommandquery-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vivxicommandquery-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen)



<div className="command-signature">

## <strong>viAssertUtilSignal</strong> (<em>vi</em>, <em>line</em>) {#viassertutilsignal}

</div>

Controls a utility bus signal. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viassertutilsignal-parameters}
*vi* is a session identifier returned by viOpen.

*line* is `VI_UTIL_ASSERT_SYSRESET`, `VI_UTIL_ASSERT_SYSFAIL` or `VI_UTIL_DEASSERT_SYSFAIL`.

### *Details* {#viassertutilsignal-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viassertutilsignal-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viAssertIntrSignal](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viassertintrsignal)



<div className="command-signature">

## <strong>viAssertIntrSignal</strong> (<em>vi</em>, <em>mode</em>, <em>statusID</em>) {#viassertintrsignal}

</div>

Controls a utility bus signal. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viassertintrsignal-parameters}
*vi* is a session identifier returned by viOpen.

*mode* specifies how to assert interrupt.

*statusID* is the value used during interrupt acknowledgment.

### *Details* {#viassertintrsignal-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viassertintrsignal-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viAssertUtilSignal](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viassertutilsignal)


<div className="command-signature">

## <strong>viMapTrigger</strong> (<em>vi</em>, <em>trigSrc</em>, <em>trigDest</em>, <em>mode</em>) {#vimaptrigger}

</div>

Maps a trigger source to a trigger destination. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#vimaptrigger-parameters}
*vi* is a session identifier returned by viOpen.

*trigSrc* specifies the trigger source.

*trigSrc* specifies the trigger destination.

*mode* must always be zero.

### *Details* {#vimaptrigger-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#vimaptrigger-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viUnmapTrigger](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viunmaptrigger)


<div className="command-signature">

## <strong>viUnmapTrigger</strong> (<em>vi</em>, <em>trigSrc</em>, <em>trigDest</em>) {#viunmaptrigger}

</div>

Unmaps a trigger signal. Not supported by TekVISA.

The function result is a VISA status code.

### *Parameters* {#viunmaptrigger-parameters}
*vi* is a session identifier returned by viOpen.

*trigSrc* specifies the trigger source.

*trigSrc* specifies the trigger destination.

### *Details* {#viunmaptrigger-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viunmaptrigger-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viMapTrigger](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vimaptrigger)





<div className="command-signature">

## <strong>viUsbControlOut</strong> (<em>vi</em>, <em>bmRequestType</em>, <em>bRequest</em>, <em>wValue</em>, <em>wIndex</em>, <em>wLength</em>, <em>buf</em> ) {#viusbcontrolout}

</div>

Sends data to a USB device. Not supported by TekVISA.

Use of this function requires a detailed knowledge of the low-level operation of the USB.

The function result is a VISA status code.

### *Parameters* {#viusbcontrolout-parameters}
*vi* is a session identifier returned by viOpen.

*bmRequestType*, *bRequest*, *wValue*, *wIndex*, *wLength* are explained in the NI-VISA Programmers Manual.

*buf* is a signed or unsigned byte (8-bit integer) wave containing the data to sent. It must be at least as long as *wLength*.

### *Details* {#viusbcontrolout-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viusbcontrolout-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viUsbControlIn](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viusbcontrolin)








<div className="command-signature">

## <strong>viUsbControlIn</strong> (<em>vi</em>, <em>bmRequestType</em>, <em>bRequest</em>, <em>wValue</em>, <em>wIndex</em>, <em>wLength</em>, <em>buf</em>, <em>retCnt</em>) {#viusbcontrolin}

</div>

Reads data from a USB device. Not supported by TekVISA.

Use of this function requires a detailed knowledge of the low-level operation of the USB.

The function result is a VISA status code.

### *Parameters* {#viusbcontrolin-parameters}
*vi* is a session identifier returned by viOpen.

*bmRequestType*, *bRequest*, *wValue*, *wIndex*, *wLength* are explained in the NI-VISA Programmers Manual.

*buf* is a signed or unsigned byte (8-bit integer) wave into which data is read. It must be at least as long as *wLength*.

### *Details* {#viusbcontrolin-details}
See the VISA library documentation for further details.

This function is untested.

### *See Also* {#viusbcontrolin-see-also}
[viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen), [viUsbControlOut](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viusbcontrolout)


## VISA XOP Operations {#visa-xop-operations}

The VISA XOP adds the following command line operations to Igor. These operations provide higher level capabilities than the VISA XOP functions.

| Operation | Details |
| --- | --- |
| [VISAControl](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visacontrol) | Controls various aspects of the VISA XOP |
| [VISARead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visaread) | For reading ASCII data into Igor variables or strings |
| [VISAWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawrite) | For writing ASCII data strings |
| [VISAReadWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadwave) | For reading ASCII data into Igor waves |
| [VISAWriteWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritewave) | For writing ASCII data from Igor waves |
| [VISAReadBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinary) | For reading binary data into Igor variables or strings |
| [VISAWriteBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritebinary) | For writing binary data from Igor variables or strings |
| [VISAReadBinaryWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinarywave) | For reading binary data into Igor waves |
| [VISAWriteBinaryWave](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawritebinarywave) | For writing binary data from Igor waves |

The VISARead, VISAWrite, VISAReadWave, VISAWriteWave, VISAReadBinary, VISAWriteBinary, VISAReadBinaryWave and VISAWriteBinaryWave, operations are collectively called "read/write" operations. These work at a level higher than the VISA XOP functions. For most data transfer operations, you can use these high level calls.

(In addition to these higher-level operations, VISA XOP also adds low-level [VISA XOP Functions](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md).)

### Errors and Status Codes From VISA XOP Operations {#errors-and-status-codes-from-visa-xop-operations}

VISA XOP operations return an error to Igor in the event of an error, whether this is an Igor error (e.g., "attempt to use a null wave") or a VISA library error (e.g., VI_ERROR_TMO). This is in contrast to low-level VISA XOP functions which do not return VISA library errors as errors to Igor.

In addition, the operations set the variables V_flag and V_status which you can use to determine what occurred. V_flag gives information about the overall success of the operation. V_status is the status code returned from the last VISA library function call made by the operation or -1 if the error occurred before any calls the the library.

When the operation returns an error to Igor, by default Igor will stop running procedures and display an error dialog. For most purposes this is sufficient. However if you are trying to write a bulletproof set of routines for use by a wide audience you may want to implement more sophisticated error handling. In that case, you must check for runtime errors after calling the operation.

Here is an example. The function result is an Igor error code, 0 for success or a non-zero value indicating an error occurred. In addition, the function returns the VISA library status code via the output parameter status.

```igor
Function Test(instr, status)
    Variable instr      // An instrument referenced obtained from viOpen.
    Variable &status    // Output: Status code from VISA library or -1.

    Variable err = 0
    Variable v1
    VISARead instr, v1  // Sets V_flag and V_status.

    // Check for VISA library error
    err = GetRTError(1) // Clear runtime error so Igor will not abort

    if (err != 0)       // VISARead failed?
        status = V_status
        return err      // Let calling routine deal with error if any.
    endif

    status = VI_SUCCESS
    return 0	// 0 indicates success.
End
```

For an example of printing an error message based on a VISA status code, see the example under [viStatusDesc](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#vistatusdesc).

### VISA XOP Operations Versus NIGPIB2 and VDT2 Operations {#visa-xop-operations-versus-nigpib2-and-vdt2-operations}

The VISA XOP operations are very similar to operations provided by Igor's NIGPIB2 and VDT2 XOPs. If you have used NIGPIB2 or VDT2, the VISA XOP operations work nearly the same.

The only major difference is that the VISA XOP operations take a session parameter which identifies the instrument you want to work with. You obtain a value for the session parameter using the viOpen function. This is in contrast to NIGPIB2 operations which work on a device specified using the "GPIB device" command and VDT2 operations which work on a serial port specified using the VDTOperationsPort operation.

<div className="command-signature">

### <strong>VISAControl</strong>  [/Q] <em>testMode</em>=<em>mode</em>, <em>dumpTestBuffer</em>, <em>clearTestBuffer</em>, <em>killIO</em> {#visacontrol}

</div>

The VISAControl operation provides control over miscellaneous VISA XOP features.

VISAControl sets V_Flag to zero if no error occurred or to non-zero if an error did occur.

#### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Do not report errors to Igor. |
|  | Without /Q, if an error occurs during execution of VISAControl, VISAControl returns an error to Igor which causes function execution to abort. |

#### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">testMode = *mode*</span> | mode=1 puts VISA XOP in a test mode. This is used only by WaveMetrics for self-testing of VISA XOP. |
| dumpTestBuffer | Dumps the test data buffer. This is used only by WaveMetrics for self-testing of VISA XOP. |
| clearTestBuffer | Clears the test data buffer. This is used only by WaveMetrics for self-testing of VISA XOP. |
| killIO | Closes all open default resource manager sessions which in turn closes all open sessions of all kinds. |
|  | Use this during development to return the VISA library to an initialized state. After you execute VISAControl killIO, any sessions that you obtained from viOpen are no longer valid. |
|  | VISA XOP also closes all open VISA sessions when Igor quits. |

<div className="command-signature">

### <strong>VISARead</strong>  [/T=<em>termStr</em> /N=<em>n</em> /Q] <em>session</em>, <em>variableName</em> [, <em>variableName</em>] {#visaread}

</div>

Reads from the device specified by session into one or more string or numeric variables.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

When used from the command line or in a macro, *variableName* must be the name of a local or global variable in the current data folder. When used from a user function, *variableName* can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr* is a string or string expression specifying characters which terminate a read of a single variable. The default is /T=",\\r\\t". |
|  | If *termStr* is not "", VISARead reads bytes one-at-a-time and is not affected by the VISA `VI_ATTR_TERMCHAR` or `VI_ATTR_ASRL_END_IN` attributes. It terminates the read only when a terminator specified by /T is received or (with GPIB devices) the END signal is received. |
|  | If *termStr* is "", VISARead reads the number of bytes specified by /N=*n* in one VISA library call. This runs quickly but the VISA library may terminate the read prematurely unless you set the appropriate attributes. See [VISA Library Terminator Character Issues](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-library-terminator-character-issues) for details. |
| <span class="table-cell-nowrap">/N = *n*</span> | n is maximum number of characters to read for each variable. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

#### *Details* {#visa-xop-operations-details}
VISARead sets the variable V_Flag to the number of items read.

VISARead internally calls the VISA library viRead function and sets the variable V_status to the status code returned from the last call to viRead or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

Here is a discussion of how VISARead goes about trying to read into its argument list.

If the /T=*termStr* flag is present, it specifies a terminator character or characters. The terminator is the character that ends input into a string or numeric variable. The default is /T=",\\r\\t" so that a comma, carriage return or tab ends a read. When dealing with a GPIB device, the read is also ended if the talker asserts the GPIB END signal.

:::note
VISARead is not affected by the VISA `VI_ATTR_TERMCHAR` attribute. It terminates the read only when a terminator specified by /T is received or (with GPIB devices) the `END` signal is received.
:::

/N=n is an optional maximum number of characters to be read into a string or numeric variable. The default is /N=255.

If /Q is present and a timeout occurs, VISARead aborts after setting the variable V_Flag to the number of items read but does not put up an error message and does not halt procedure execution. This allows a procedure to handle a timeout in its own way.

When reading a string, VISARead reads until the next terminator is encountered. The terminator is not put into the string. The next read starts after the terminator.

Do not use VISARead to read binary data or anything that contains a null character (ASCII 0). Use [VISAReadBinary](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visareadbinary) instead.

When reading a numeric variable, VISARead first skips any non-numeric characters and then reads a number. If the *variableName* refers to a complex variable, VISARead reads two numbers from the device and stores both the real and imaginary parts of the variable.

#### *Example* {#visa-xop-operations-example}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    Variable v1, v2
    String s1
    VISARead instr, v1, s1, v2
End
```

This reads from the device referenced by instr into variable v1, string variable s1 and variable v2.

#### *Terminators* {#terminators}

There are three common cases to consider:

1. Instruments that send CR as terminator
2. Instruments that send CR and LF as terminator
3. Instruments that send neither CR nor LF but use the END line only.

You must determine what terminator your instrument sends from its documentation.

The following examples show how you would read a response in the three cases into a string variable. str1 is an Igor string variable.

```igor
// CR terminator
String str1
VISARead str1	// Read the string till CR

// CRLF terminator
String str1, lf
VISARead/T="\r\n" str1, lf	// Read the string till CR, then read LF.

// END terminator
String str1
VISARead str1	// Read the string till END
```

The following examples show how you would read a response in the three cases into a numeric variable.

```igor
// CR terminator
Variable v0
VISARead v0	// Read the number till CR

// CRLF terminator
Variable v0
String lf
VISARead/T="\r\n" v0, lf	// Read the number till CR, then read LF.

// END terminator
VISARead v0	// Read the string till END
```

If you expected \<number\>\<comma\>\<number\>\<comma\>\<number\>\<crlf\>, here is what you would do:

```igor
Variable v0, v1, v2
String lf
VISARead/T=",\r\n" v0, v1, v2, lf
```

When dealing with a GPIB device, you may want to read every character into a string until END is asserted. To do this you can specify an empty terminator:

```igor
VISARead/T="" str1
```




<div className="command-signature">

### <strong>VISAReadWave</strong>  [ /R=[<em>start</em>, <em>end</em>] /T=<em>termStr</em> /N=<em>n</em> /Q ] <em>session</em>, <em>waveName</em> [, <em>waveName</em>] {#visareadwave}

</div>

Reads data from device into waves.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and VISAReadWave reads two values for each wave point.

Assuming the the /R flag is omitted, data is stored into point 0 of each wave, then point 1 of each wave, and so on.

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = n</span> | n is maximum number of characters to read for each value. The default is 255. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/R = [ *start*, *end* ]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to read data into. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | *termStr* is a string or string expression specifying characters which terminate a read of a single number. The default is /T=",\\r\\t". |
|  | If *termStr* is not "", VISAReadWave reads bytes one-at-a-time and is not affected by the VISA `VI_ATTR_TERMCHAR` or `VI_ATTR_ASRL_END_IN` attributes. It terminates the read only when a terminator specified by /T is received or (with GPIB devices) the END signal is received. |
|  | If *termStr* is "", VISAReadWave reads the number of bytes specified by /N=*n* in one VISA library call. This runs quickly but the VISA library may terminate the read prematurely unless you set the appropriate attributes. See [VISA Library Terminator Character Issues](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-library-terminator-character-issues) for details. |

#### *Details* {#visa-xop-operations-details}
If the /R flag is omitted, VISAReadWave stores values in point 0 through point n-1 where n is the number of points in the first wave.

VISAReadWave sets the variable V_flag to the number of  individual numbers read.

VISAReadWave internally calls the VISA library viRead function and sets the variable V_status to the status code returned from the last call to viRead or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

VISAReadWave works with 64-bit integer data but is limited to 53 bits of precision. See [VISA XOP 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-xop-64-bit-integer-limitations) for details.

#### *Example* {#visa-xop-operations-example}

```igor
Function Test(instr)
    Variable instr              // An instrument referenced obtained from viOpen

    WAVE wave1, wave2, wave3    // Reference to waves in current data folder.
    VISAReadWave instr, wave1, wave2, wave3
End
```

This reads from the device into wave1, wave2 and wave3. It reads until it has put a value in each point of each wave.

#### *Terminators* {#visa-xop-operations-terminators}

See the discussion of terminators for the [VISARead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visaread) operation.





<div className="command-signature">

### <strong>VISAReadBinary</strong>  [ /B /Q /S=<em>strLen</em> /T=<em>termStr</em> /TYPE=<em>type</em> /Y={<em>offset</em> , <em>multiplier</em> }] <em>session</em>, <em>variableName</em> [,<em>variableName</em>] {#visareadbinary}

</div>

Reads binary data into Igor strings and variables. The binary data can be read as integers of one, two or four bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

When used from the command line or in a macro, *variableName* must be the name of a local or global variable in the current data folder. When used from a user function, *variableName* can be the name of a local variable or the name of an NVAR or SVAR referencing a global variable in any data folder.

If /S=*strLen* is used, the arguments are expected to be string variables and bytes are read up to *strLen* bytes or until a byte is read from GPIB with END asserted or until a byte specified by /T=*termStr* is read.

If /S=*strLen* is NOT used, the arguments are expected to be numeric variables into which data is to be read.

Reading binary data into strings is used mostly to skip a number of bytes or until a certain byte is received. To read actual ASCII data into strings, use [VISARead](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visaread) instead of VISAReadBinary.

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Indicates that multi-byte data is to be received low-byte-first. Without /B, multi-byte data is received high-byte-first. This flag affects receiving of numeric data only, not string data. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/S = *strLen*</span> | If present, the variables are expected to be string variables. Bytes are read up to *strLen* bytes or until a byte is read with END asserted or until a byte specified by /T=*termStr* is read. |
| <span class="table-cell-nowrap">/T = *termStr*</span> | Specifies a terminator character when reading bytes into strings. The default value is "" (no terminators). The read will be faster if no terminators are specified. This has no effect when reading into numeric variables. |
|  | If *termStr* is not "", VISAReadBinary reads bytes one-at-a-time and is not affected by the VISA `VI_ATTR_TERMCHAR` or `VI_ATTR_ASRL_END_IN` attributes. It terminates the read only when a terminator specified by /T is received or (with GPIB devices) the END signal is received. |
|  | If *termStr* is "", VISAReadBinary reads the number of bytes specified by /N=*n* in one VISA library call. This runs quickly but the VISA library may terminate the read prematurely unless you set the appropriate attributes. See [VISA Library Terminator Character Issues](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-library-terminator-character-issues) for details. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type* . The default value is 8 (signed byte). |
| <span class="table-cell-nowrap">/Y = {o, m}</span> | o is offset, m is multiplier. /Y is used to scale integer data into real numbers. output data = (input data + offset) * multiplier. |

#### *Details* {#visa-xop-operations-details}
If a numeric variable is complex, VISAReadBinary reads two values for that variable.

VISAReadBinary sets the variable V_flag, after creating it if necessary, to the number of  items read.

VISAReadBinary internally calls the VISA library viRead function and sets the variable V_status to the status code returned from the last call to viRead or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

VISAReadBinary works with 64-bit integer data but is limited to 53 bits of precision. See [VISA XOP 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-xop-64-bit-integer-limitations) for details.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr  // An instrument referenced obtained from viOpen

    // Read 10 bytes or until END is received into string variable str1.
    String str1
    VISAReadBinary/S=10 instr, str1

    // Read two-byte signed integer binary numbers into the numeric variables v0 and v1.
    Variable v0, v1
    VISAReadBinary/TYPE=(0x10) instr, v0, v1        // Read big-endian data.
    VISAReadBinary/TYPE=(0x10)/B instr, v0, v1      // Read little-endian data.

    // Read four-byte IEEE single-precision floating point binary numbers into v0 and v1.
    VISAReadBinary/TYPE=2 instr, v0, v1             // Read big-endian data.
    VISAReadBinary/TYPE=2/B instr, v0, v1           // Read little-endian data.
End
```

<div className="command-signature">

### <strong>VISAReadBinaryWave</strong>  [ /B /Q /TYPE=<em>type</em> /Y={<em>offset</em>, <em>multiplier</em>} ] <em>session</em>, <em>waveName</em> [,<em>waveName</em>] {#visareadbinarywave}

</div>

Reads binary data into the numeric waves named in wavelist. The waves can be of any numeric data type, real or complex.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Indicates that multi-byte data is to be received low-byte-first. Without /B, multi-byte data is received high-byte-first. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format of the incoming binary data. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |
| <span class="table-cell-nowrap">/Y = {o, m}</span> | o is offset, m is multiplier. /Y is used to scale integer data into real numbers. |
|  | <code class="igor">output data = (input data + offset) * multiplier</code> |
#### *Details* {#visa-xop-operations-details}
When reading binary data into a string, the VISA library may terminate the read prematurely unless you set the appropriate attributes. See [VISA Library Terminator Character Issues](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-library-terminator-character-issues) for details.

If multiple waves are specified, all of the values for the first wave are read, followed by all of the values for the second wave, and so on.

If a wave is complex, VISAReadBinaryWave reads two values for each point in that wave. This is true regardless of the /TYPE=*type* flag.

VISAReadBinaryWave sets the variable V_flag, after creating it if necessary, to the number of  waves (not points) read.

VISAReadBinaryWave internally calls the VISA library viRead function and sets the variable V_status to the status code returned from the last call to viRead or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    // Reads two-byte signed integer binary numbers into each point of wave.
    VISAReadBinaryWave/TYPE=(0x10) instr, wave0                     // Big-endian data.
    VISAReadBinaryWave/TYPE=(0x10)/B instr, wave0                   // Little-endian data.

    // Reads a four byte signed integer binary number into each point of wave0,
    // wave1 and wave2. All of wave0 is read first, then all of wave1, then all of wave2.
    VISAReadBinaryWave/TYPE=(0x20) instr, wave0, wave1, wave2       // Big-endian data.
    VISAReadBinaryWave/TYPE=(0x20)/B instr, wave0, wave1, wave2     // Little-endian data.

    // Reads two-byte signed integer binary numbers into each point of wave.
    // Then it adds 0 to each point and multiplies by .25. This would be used
    // to scale integer data where 1 count represents .25 volts, for example.
    VISAReadBinaryWave/TYPE=(0x10)/Y={0,0.25} instr, wave0          // Big-endian data.
    VISAReadBinaryWave/TYPE=(0x10)/Y={0,0.25}/B instr, wave0        // Little-endian data.
End
```

<div className="command-signature">

### <strong>VISAWrite</strong>  [/Q] <em>session</em>, <em>str</em> {#visawrite}

</div>

Transmits contents of the string argument.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

*str* is a string expression.

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

#### *Details* {#visa-xop-operations-details}
VISAWrite sets the variable V_flag to 1 if the write succeeded or to zero otherwise.

VISAWrite internally calls the VISA library viWrite function and sets the variable V_status to the status code returned from the last call to viWrite or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    // Transmits a greeting followed by a carriage return.
    VISAWrite instr, "Hello" + "\r"

    // Transmits the contents of variable v1, the sine of .5 radians and the contents of
    // point 0 of wave1, separated by tabs with a carriage return and linefeed at the end.

    Variable v1 = 1234
    Wave wave1
    String str
    sprintf str, "%g\t%g\t%g\r\n", v1, sin(.5), wave1[0]
    VISAWrite instr, str
End
```




<div className="command-signature">

### <strong>VISAWriteWave</strong>  [ /R=[<em>start</em>, <em>end</em>] /F={<em>numericFormatStr</em>, <em>leaderStr</em>, <em>separatorStr</em>, <em>terminatorStr</em>}  /Q ] <em>session</em>, <em>waveName</em> [,<em>waveName</em>] {#visawritewave}

</div>

Transmits contents of wave or waves as text.

The waves must be 1-dimensional and can be numeric or text waves. For numeric waves only, complex waves are supported and VISAWriteWave writes two values for each wave point.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F = {*numericFormatStr, leaderStr, separatorStr, terminatorStr* }</span> |  |
|  | *numericFormatStr* is the numeric format string used to generate the output text for each numeric wave point. VISAWriteWave passes this string to the C sprintf function. The default value is "%g". |
|  | Only numeric formats are allowed. *numericFormatStr* must end with a numeric conversion character. See [Printf](/igorpro/commands/printf.md) for details on formats. |
|  | *leaderStr* is text that is inserted at the start of each line of data. The default is "". |
|  | *separatorStr* is text that is inserted between each pair of points. The default is "\\t" (tab). |
|  | *terminatorStr* is text that is written at the end of each line of data. The default is "\\r" (carriage-return). |
| <span class="table-cell-nowrap">/R = [start,end]</span> | Specifies the starting and ending point numbers for a range of the waves that you want to write data from. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |

#### *Details* {#visa-xop-operations-details}
If the /R flag is omitted, VISAWriteWave writes values for point 0 through point n-1 where n is the number of points in the first wave.

VISAWriteWave sets the variable V_flag, after creating it if necessary, to the number of individual numbers written.

VISAWriteWave internally calls the VISA library viWrite function and sets the variable V_status to the status code returned from the last call to viWrite or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

VISAWriteWave works with 64-bit integer data but is limited to 53 bits of precision. See [VISA XOP 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-xop-64-bit-integer-limitations) for details.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    // Transmits contents of the waves as text, using 15 digits of precision
    // with a comma between numbers and CRLF at the end of each line.
    VISAWriteWave/F={"%.15g", "", ",", "\r\n"} instr, wave1, wave2, wave3
End
```

<div className="command-signature">

### <strong>VISAWriteBinary</strong>  [ /B /Q /TYPE=<em>type</em> ] <em>session</em>, <em>argument</em> [,<em>argument</em>] {#visawritebinary}

</div>

Transmits contents of the argument or arguments as binary data. The binary data can be sent as integers of one-, two- or four-bytes, 32-bit IEEE floating point or 64-bit IEEE floating point.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

*argument* is a numeric expression.

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Indicates that multi-byte data is to be sent low-byte-first. Without /B, multi-byte data is sent high-byte-first. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |

#### *Details* {#visa-xop-operations-details}
VISAWriteBinary sets the variable V_flag, after creating it if necessary, to the number of  items written.

VISAWriteBinary internally calls the VISA library viWrite function and sets the variable V_status to the status code returned from the last call to viWrite or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

VISAWriteBinary can not transmit strings. Use [VISAWrite](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#visawrite) for that. VISAWriteBinary can also not transmit complex values.

VISAWriteBinary works with 64-bit integer data but is limited to 53 bits of precision. See [VISA XOP 64-bit Integer Limitations](/igorpro/extensions/data-acquisition/visa/visa-xop.md#visa-xop-64-bit-integer-limitations) for details.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    // Writes 123 and -456 as two byte signed integer binary numbers.
    VISAWriteBinary/TYPE=(0x10) instr, 123, -456        // Big-endian
    VISAWriteBinary/TYPE=(0x10)/B instr, 123, -456      // Little-endian

    // Writes 2*PI and -PI/2 as 32-bit IEEE floating point binary numbers
    VISAWriteBinary/TYPE=2 instr, 2*PI, -PI/2           // Big-endian
    VISAWriteBinary/TYPE=2/B instr, 2*PI, -PI/2         // Little-endian
End
```

<div className="command-signature">

### <strong>VISAWriteBinaryWave</strong>  [ /B /Q /TYPE=<em>type</em> ] <em>session</em>, <em>waveName</em> [,<em>waveName</em>] {#visawritebinarywave}

</div>

Writes binary data from the listed waves. The waves can be of any numeric data type.

#### *Parameters* {#visa-xop-operations-parameters}
*session* is a session to an instrument obtained by calling [viOpen](/igorpro/extensions/data-acquisition/visa/visa-xop-functions.md#viopen).

#### *Flags* {#visa-xop-operations-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Indicates that multi-byte data is to be sent low-byte-first. Without /B, multi-byte data is sent high-byte-first. |
| <span class="table-cell-nowrap">/Q</span> | Specifies no error message on timeout. |
| <span class="table-cell-nowrap">/TYPE = *type*</span> | Specifies the format in which the binary data is transmitted. See [WaveType](/igorpro/commands/wavetype.md) for the definition of *type*. The default value is 8 (signed byte). |

#### *Details* {#visa-xop-operations-details}
The waves can be of any numeric data type, real or complex.

If multiple waves are specified, all of the values for the first wave are written, followed by all of the values for the second wave, and so on.

If a wave is complex, VISAWriteBinaryWave writes two values for each point in that wave. This is true regardless of the /TYPE=*type* flag.

VISAWriteBinaryWave sets the variable V_flag, after creating it if necessary, to the number of  waves (not points) written.

VISAWriteBinaryWave internally calls the VISA library viWrite function and sets the variable V_status to the status code returned from the last call to viWrite or -1 if the error occurred before any calls the the library. This can be used to determine what went wrong in the event of an error.

#### *Examples* {#visa-xop-operations-examples}

```igor
Function Test(instr)
    Variable instr	// An instrument referenced obtained from viOpen

    // Writes each point of wave0 as a two-byte signed integer binary number.
    VISAWriteBinaryWave/TYPE=(0x10) instr, wave0                    // Big-endian
    VISAWriteBinaryWave/TYPE=(0x10)/B instr, wave0                  // Little-endian

    // Writes all of wave0 as a four-byte signed integer binary number,
    // followed by all of wave1 and then all of wave2.
    VISAWriteBinaryWave/TYPE=(0x20) instr, wave0, wave1, wave2      // Big-endian
    VISAWriteBinaryWave/TYPE=(0x20)/B instr, wave0, wave1, wave2    // Little-endian

    // Writes each point of wave0 as a 32-bit IEEE floating point binary number.
    VISAWriteBinaryWave/TYPE=2 instr, wave0                         // Big-endian
    VISAWriteBinaryWave/TYPE=2/B instr, wave0                       // Little-endian
End
```