---
description: "The following external functions are used with 700B amplifiers. The following external functions are used with 700A amplifiers."
slug: /extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference
---

| Command | Details |
| --- | --- |
| [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers) | Obtain information about all available 700A and 700B servers. |
| [AxonTelegraphSetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphsettimeoutms) | Set the timeout value for amplifier communication. |
| [AxonTelegraphGetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgettimeoutms) | Get the timeout value for amplifier communication. |


The following external functions are used with **700B** amplifiers.

| Command | Details |
| --- | --- |
| [AxonTelegraphGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatanum) | Get the value of a single numeric property. |
| [AxonTelegraphGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastring) | Get the value of a single string property. |
| [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct) | Store the value of all properties of a server into an Igor structure. |


The following external functions are used with **700A** amplifiers.

| Command | Details |
| --- | --- |
| [AxonTelegraphAGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatanum) | Get the value of a single numeric property. |
| [AxonTelegraphAGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastring) | Get the value of a single string property. |
| [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct) | Store the value of all properties of a server into an Igor structure. |


<div className="command-signature">

## <strong>AxonTelegraphFindServers</strong>  [/Z[=<em>z</em>]] {#axontelegraphfindservers}

</div>

Find all available telegraph servers and save information about those servers into a wave named W_TelegraphServers.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z[ = z]</span> | Suppress error generation. Use this if you want to handle errors yourself. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all.</td></tr><tr><td>/Z=1:</td><td>Same as /Z alone. Any errors will not stop procedure execution. If there is an error the code for the error will be stored in V_Flag.</td></tr></tbody></table>

### *Details* {#details}
AxonTelegraphFindServers sets the following outputs:

|  |  |
| --- | --- |
| W_TelegraphServers | A 2D signed 32-bit integer wave containing information about each telegraph server that was identified.  Column 0 contains the serial number of the server (or -1 if the server represents a 700A amplifier).  Column 1 contains the channel ID of the server.  Column 2 contains the Com Port ID of the server.  Column 3 contains the Axo Bus ID of the server.  If the server represents a 700B amplifier, the value of the Com Port ID and Axo Bus ID column for the amplifier will be -1. |
| V_Flag | Set to zero if the operation succeeds without error or to a non-zero error code if it fails. |

:::note
You can use the value of the serial number column (column 0) to determine the hardware type of the telegraph server.  If the server represents a 700A amplifier, the serial number will always be -1 because 700A amplifiers do not use the serial number parameter.  Likewise, if the amplifier is a 700B amplifier, the serial number will be a non-negative value, but the Com Port ID and Axo Bus ID values will be -1.
:::

### *Examples* {#examples}

```igor
AxonTelegraphFindServers        // Simplest form
AxonTelegraphFindServers/Z=1    // Suppress any errors
```


<div className="command-signature">

## <strong>AxonTelegraphSetTimeoutMs</strong> (<em>timeoutMs</em>) {#axontelegraphsettimeoutms}

</div>

Set the timeout value for communicating with the telegraph server, in milliseconds.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *timeoutMs* | The duration of the timeout, in milliseconds.  The default timeout value is 1000 ms. The maximum timeout allowed is 15 seconds. Values of *timeoutMs* that are greater than 15000 will be shortened to 15000 ms. |

### *Details* {#axontelegraphsettimeoutms-details}

All routines provided by this XOP, with the exception of this function and [AxonTelegraphGetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgettimeoutms), send a message to any telegraph servers that are listening instructing the server to send the XOP information.  For the AxonTelegraphFindServers operation, the XOP will wait the entire duration of the timeout period so that there is ample time for all available servers to respond.  For other routines provided by this XOP, the XOP will wait until the telegraph server has responded or the duration of the timeout, whichever is shorter. When the XOP is loaded the default value of the timeout is 1000 ms.  Any changes to the timeout made using this function are retained until another change is made or until the XOP is unloaded from memory, which happens when Igor is restarted.

If the timeout is too short it is possible that servers that are present on the system might not be identified, or that data is not retrieved as expected.  A timeout value of between one and three seconds should be sufficient in most cases.

### *Examples* {#axontelegraphsettimeoutms-examples}

```igor
AxonTelegraphSetTimeoutMs(1000) // Set the timeout value to 1 second.
AxonTelegraphSetTimeoutMs(50)   // Set the timeout value to 50 ms.
```

### *See Also* {#see-also}

[AxonTelegraphGetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgettimeoutms)


<div className="command-signature">

## <strong>AxonTelegraphGetTimeoutMs</strong> () {#axontelegraphgettimeoutms}

</div>

Get the current timeout value used for communication with the telegraph server, in milliseconds.

### *Example* {#example}

```igor
Variable timeout = AxonTelegraphGetTimeoutMs()
print timeout                                   // prints 1000
AxonTelegraphSetTimeoutMs(100)
timeout = AxonTelegraphGetTimeoutMs()
print timeout                                   // prints 100
```

### *See Also* {#axontelegraphgettimeoutms-see-also}
[AxonTelegraphSetTimeoutMs](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphsettimeoutms)


<div className="command-signature">

## <strong>AxonTelegraphGetDataNum</strong> (<em>serialNumber</em>, <em>channelID</em>, <em>parameterNameString</em>) {#axontelegraphgetdatanum}

</div>

Get the numerical value of a single parameter from one 700B telegraph server.

### *Parameters* {#axontelegraphgetdatanum-parameters}

|  |  |
| --- | --- |
| *serialNumber* | The serial number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *parameterNameString* | A string containing the name of a single parameter that should be returned. The parameter name is case-sensitive. Valid values for *parameterNameString* are given in the details section below. |

### *Details* {#axontelegraphgetdatanum-details}
Use this function if you wish to retrieve the numeric value of a single parameter of a 700B telegraph server, such as the gain, mode, or lowpass filter frequency setting.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.  Though several calls could be made to this function to retrieve multiple parameters, doing so could be slow if the system is busy.  To retrieve all of the properties of the amplifier at once, use [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct).

The allowed values for the *parameterNameString* parameter are given in the table below*.*  The parameters that are available through this function fall into two broad categories: actual values of a setting (such as gain) and numerical representations of the name of a setting or state (such as amplifier mode).  For those parameters that represent the name of a setting, you can use the [AxonTelegraphGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastring) function to retrieve the name of a specific setting in a string.

Parameter names that return the value of a setting:

| Name | Description |
| --- | --- |
| Alpha | Output gain for primary output signal |
| ScaleFactor | Gain scale factor (for Alpha == 1) of primary output signal |
| LPFCutoff | Primary output lowpass filter cutoff frequency, in Hz<sup>a</sup> |
| MembraneCap | Membrane capacitance<sup>b</sup> |
| ExtCmdSens | External command sensitivity<sup>c</sup> |
| RawScaleFactor | Gain scale factor (for Alpha == 1) of secondary output signal |
| SecondaryAlpha | Output gain for secondary output |
| SecondaryLPFCutoff | Secondary output lowpass filter cutoff frequency, in Hz<sup>a</sup> |
| SeriesResistance | Measured series resistance<sup>d</sup> |

<sup>a</sup> A value of 1.0e5 means that the lowpass filter is being bypassed.

<sup>b</sup> A value of 0 means that capacitance was not measured.

<sup>c</sup> In units of V/V for voltage clamp, A/V for current clamp, and 0 for I=0 mode.

<sup>d</sup> A value of 0 means that series resistance was not measured.

Parameter names that return the numerical representation of a setting:

| Name | Description |
| --- | --- |
| OperatingMode | The amplifier mode |
| ScaledOutSignal | Type of signal represented by primary output |
| ScaleFactorUnits | Value representing units for primary output signal |
| RawOutSignal | Type of signal represented by secondary output |
| HardwareType | Value representing amplifier model |
| RawScaleFactorUnits | Value representing units for secondary output signal |

### *Examples* {#axontelegraphgetdatanum-examples}

```igor
print AxonTelegraphGetDataNum(0, 1, "Alpha")        // prints 200
print AxonTelegraphGetDataNum(0, 1, "HardwareType") // prints 1
print AxonTelegraphGetDataNum(0, 1, "MembraneCap")  // prints 3.3e-11
```

### *See Also* {#axontelegraphgetdatanum-see-also}
[AxonTelegraphGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastring), [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)

<div className="command-signature">

## <strong>AxonTelegraphGetDataString</strong> (<em>serialNumber</em>, <em>channelID</em>, <em>parameterNameString</em>, <em>stringLengthFlag</em>) {#axontelegraphgetdatastring}

</div>

Get the string representation of a single parameter from one 700B telegraph server.

### *Parameters* {#axontelegraphgetdatastring-parameters}

|  |  |
| --- | --- |
| *serialNumber* | The serial number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *parameterNameString* | A string containing the name of a single parameter that should be returned. The parameter name is case-sensitive. Valid values for *parameterNameString* are given in the details section below. |
| *stringLengthFlag* | Pass 0 to return the short name of a parameter or 1 for the long name. |

### *Details* {#axontelegraphgetdatastring-details}
Use this function if you wish to retrieve the string value of a single parameter of a 700B telegraph server.  The function is only applicable to parameters that describe a setting or state, such as the amplifier mode or name of the units being measured.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.  Though several calls could be made to this function to retrieve multiple parameters, doing so could be slow if the system is busy.  To retrieve all of the properties of the amplifier at once, use [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct).

The allowed values for the *parameterNameString* parameter are given in the table below*.*  The numerical representation of each of these parameters is also available by calling the function  [AxonTelegraphGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatanum).

| Name | Description |
| --- | --- |
| OperatingMode | The amplifier mode |
| ScaledOutSignal | Type of signal represented by primary output |
| ScaleFactorUnits | Value representing units for primary output signal |
| RawOutSignal | Type of signal represented by secondary output |
| HardwareType | Value representing amplifier model |
| RawScaleFactorUnits | Value representing units for secondary output signal |

Some parameters have both a short and a long version.  For example, the ScaledOutSignal parameter might be either "Membrane current" or "Im".  For other parameters, there is only one version of the string.  In those cases the value of *stringLengthFlag* is ignored.

### *Note* {#note}
In some cases the string value of ScaledOutSignal and/or RawOutSignal is "Unknown".  This happens when the values of the corresponding numerical parameters are out of the range of values that are defined in the software development toolkit provided by Axon.  These out of range values only occur for output types that are unlikely to be used, so it is unlikely that you will have this problem.

### *Examples* {#axontelegraphgetdatastring-examples}

```igor
print AxonTelegraphGetDataString(0, 1, "ScaledOutSignal", 0)    // prints "Vm"
print AxonTelegraphGetDataString(0, 1, "ScaledOutSignal", 1)    // prints "Membrane potential"
print AxonTelegraphGetDataString(0, 1, "ScaleFactorUnits", 0)   // prints "V/nA"
```


### *See Also* {#axontelegraphgetdatastring-see-also}
[AxonTelegraphGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatanum), [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)


<div className="command-signature">

## <strong>AxonTelegraphGetDataStruct</strong> (<em>serialNumber</em>, <em>channelID</em>, <em>stringLengthFlag</em>, <em>dataStruct</em>) {#axontelegraphgetdatastruct}

</div>

Get the numeric values and string representations of all parameters from one 700B telegraph server and stores all values in a structure.

### *Parameters* {#axontelegraphgetdatastruct-parameters}

|  |  |
| --- | --- |
| *serialNumber* | The serial number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *stringLengthFlag* | Pass 0 to return the short name of a parameter or 1 for the long name. See the details section of [AxonTelegraphGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastring) for more information on this parameter. |
| *dataStruct* | An instance of the AxonTelegraph_DataStruct structure.  With the exception of the version field of this structure, all fields are output fields and will be overwritten by the XOP. |

### *Details* {#axontelegraphgetdatastruct-details}
Use this function if you wish to retrieve the numeric values and string representations of all parameters from one 700B telegraph server.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.

This function expects that the data structure passed as the *dataStruct* parameter contains certain fields of a certain size.  One of these fields is the version field.  Before calling this function you must set the version field of your Igor structure to a valid value.  Currently, the only valid value is the number 13.  If dataStruct.version is not a valid value, this function will return a run time error in order to prevent a potential crash, which could result if the *dataStruct* structure parameter is not the same type of structure that the XOP expects.

Because this function takes an Igor structure as one of its parameters, it must be called from within another Igor function.

The AxonTelegraph_DataStruct structure is defined below.  You must copy this structure definition into an Igor procedure window to define it.  You may change the name of the structure, if you wish, but must not change the name, order, or data types of the structure's fields.

```igor
Structure AxonTelegraph_DataStruct
    uint32 Version	// Structure version.  Value should always be 13.
    uint32 SerialNum
    uint32 ChannelID
    uint32 ComPortID
    uint32 AxoBusID
    uint32 OperatingMode
    String OperatingModeString
    uint32 ScaledOutSignal
    String ScaledOutSignalString
    double Alpha
    double ScaleFactor
    uint32 ScaleFactorUnits
    String ScaleFactorUnitsString
    double LPFCutoff
    double MembraneCap
    double ExtCmdSens
    uint32 RawOutSignal
    String RawOutSignalString
    double RawScaleFactor
    uint32 RawScaleFactorUnits
    String RawScaleFactorUnitsString
    uint32 HardwareType
    String HardwareTypeString
    double SecondaryAlpha
    double SecondaryLPFCutoff
    double SeriesResistance
EndStructure
```
:::note
In some cases the value of ScaledOutSignalString and/or RawOutSignalString is "Unknown".  This happens when the values of the corresponding numerical parameters ScaledOutSignal and RawOutSignal are out of the range of values that are defined in the software development toolkit provided by Axon.  These out of range values only occur for output types that are unlikely to be used, so it is unlikely that you will have this problem.
:::

### *Examples* {#axontelegraphgetdatastruct-examples}

```igor
Function GetAxonTeleServerInfo()
    STRUCT AxonTelegraph_DataStruct tds
    tds.version = 13
    AxonTelegraphGetDataStruct(0, 1, 1, tds)
    print tds
End
```

### *See Also* {#axontelegraphgetdatastruct-see-also}
[AxonTelegraphGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatanum), [AxonTelegraphGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastring), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)

<div className="command-signature">

## <strong>AxonTelegraphAGetDataNum</strong> (<em>comPortID</em>, <em>axoBusID</em>, <em>channelID</em>, <em>parameterNameString</em>) {#axontelegraphagetdatanum}

</div>

Get the numerical value of a single parameter from one 700A telegraph server.

### *Parameters* {#axontelegraphagetdatanum-parameters}

|  |  |
| --- | --- |
| *comPortID* | The Com Port ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *axoBusID* | The Axo Bus ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *parameterNameString* | A string containing the name of a single parameter that should be returned. The parameter name is case-sensitive. Valid values for *parameterNameString* are given in the details section below. |

### *Details* {#axontelegraphagetdatanum-details}
Use this function if you wish to retrieve the numeric value of a single parameter of a 700A telegraph server, such as the gain, mode, or lowpass filter frequency setting.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.  Though several calls could be made to this function to retrieve multiple parameters, doing so could be slow if the system is busy.  To retrieve all of the properties of the amplifier at once, use [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct).

The allowed values for the *parameterNameString* parameter are given in the table below*.*  The parameters that are available through this function fall into two broad categories: actual values of a setting (such as gain) and numerical representations of the name of a setting or state (such as amplifier mode).  For those parameters that represent the name of a setting, you can use the [AxonTelegraphAGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastring) function to retrieve the name of a specific setting in a string.

Parameter names that return the value of a setting:

| Name | Description |
| --- | --- |
| Alpha | Output gain for primary (scaled) output signal |
| ScaleFactor | Gain scale factor (for Alpha == 1) of primary (scaled) output signal |
| LPFCutoff | Primary (scaled) output lowpass filter cutoff frequency, in Hz<sup>a</sup> |
| MembraneCap | Membrane capacitance<sup>b</sup> |
| ExtCmdSens | External command sensitivity<sup>c</sup> |
| RawScaleFactor | Gain scale factor (for Alpha == 1) of secondary (raw) output signal<sup>e</sup> |
| SecondaryAlpha | Output gain for secondary (raw) output<sup>e</sup> |
| SecondaryLPFCutoff | Secondary (raw) output lowpass filter cutoff frequency, in Hz<sup>a,</sup><sup>e</sup> |
| SeriesResistance | Measured series resistance<sup>d,</sup><sup>e</sup> |

Parameter names that return the numerical representation of a setting:

| Name | Description |
| --- | --- |
| OperatingMode | The amplifier mode |
| ScaledOutSignal | Type of signal represented by primary (scaled) output |
| ScaleFactorUnits | Value representing units for primary (scaled) output signal |
| RawOutSignal | Type of signal represented by secondary (raw) output |
| HardwareType | Value representing amplifier model |
| RawScaleFactorUnits | Value representing units for secondary (raw) output signal<sup>e</sup> |

<sup>a</sup> A value of 1.0e5 means that the lowpass filter is being bypassed.

<sup>b</sup> A value of 0 means that capacitance was not measured.

<sup>c</sup> In units of V/V for voltage clamp, A/V for current clamp, and 0 for I=0 mode.

<sup>d</sup> A value of 0 means that series resistance was not measured.

<sup>e </sup>This value may not be available for 700A servers but reading it will not produce an error.



### *Examples* {#axontelegraphagetdatanum-examples}

```igor
print AxonTelegraphAGetDataNum(1, 0, 1, "Alpha")            // prints 200
print AxonTelegraphAGetDataNum(1, 0, 1, "HardwareType")     // prints 1
print AxonTelegraphAGetDataNum(1, 0, 1, "MembraneCap")      // prints 3.3e-11
```

### *See Also* {#axontelegraphagetdatanum-see-also}
[AxonTelegraphAGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastring), [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)


<div className="command-signature">

## <strong>AxonTelegraphAGetDataString</strong> (<em>comPortID</em>, <em>axoBusID</em>, <em>channelID</em>, <em>parameterNameString</em>, <em>stringLengthFlag</em>) {#axontelegraphagetdatastring}

</div>

Get the string representation of a single parameter from one 700A telegraph server.

### *Parameters* {#axontelegraphagetdatastring-parameters}

|  |  |
| --- | --- |
| *comPortID* | The Com Port ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *axoBusID* | The Axo Bus ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *parameterNameString* | A string containing the name of a single parameter that should be returned. The parameter name is case-sensitive. Valid values for *parameterNameString* are given in the details section below. |
| *stringLengthFlag* | Pass 0 to return the short name of a parameter or 1 for the long name. |

### *Details* {#axontelegraphagetdatastring-details}
Use this function if you wish to retrieve the string value of a single parameter of a 700A telegraph server.  The function is only applicable to parameters that describe a setting or state, such as the amplifier mode or name of the units being measured.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.  Though several calls could be made to this function to retrieve multiple parameters, doing so could be slow if the system is busy.  To retrieve all of the properties of the amplifier at once, use [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct).

The allowed values for the *parameterNameString* parameter are given in the table below*.*  The numerical representation of each of these parameters is also available by calling the function  [AxonTelegraphAGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatanum).

| Name | Description |
| --- | --- |
| OperatingMode | The amplifier mode |
| ScaledOutSignal | Type of signal represented by primary (scaled) output |
| ScaleFactorUnits | Value representing units for primary (scaled) output signal |
| RawOutSignal | Type of signal represented by secondary (raw) output |
| HardwareType | Value representing amplifier model |
| RawScaleFactorUnits | Value representing units for secondary (raw) output signal<sup>a</sup> |

<sup>a </sup>This value may not be available for 700A servers but reading it will not produce an error.

Some parameters have both a short and a long version.  For example, the ScaledOutSignal parameter might be either "Membrane current" or "Im".  For other parameters, there is only one version of the string.  In those cases the value of *stringLengthFlag* is ignored.

:::note
In some cases the string value of ScaledOutSignal and/or RawOutSignal is "Unknown".  This happens when the values of the corresponding numerical parameters are out of the range of values that are defined in the software development toolkit provided by Axon.  These out of range values only occur for output types that are unlikely to be used, so it is unlikely that you will have this problem.
:::

### *Examples* {#axontelegraphagetdatastring-examples}

```igor
print AxonTelegraphAGetDataString(1, 0, 1, "ScaledOutSignal", 0)    // prints "Vm"
print AxonTelegraphAGetDataString(1, 0, 1, "ScaledOutSignal", 1)    // prints "Membrane potential"
print AxonTelegraphAGetDataString(1, 0, 1, "ScaleFactorUnits", 0)   // prints "V/nA"
```

### *See Also* {#axontelegraphagetdatastring-see-also}
[AxonTelegraphAGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatanum), [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)



<div className="command-signature">

## <strong>AxonTelegraphAGetDataStruct</strong> (<em>comPortID</em>, <em>axoBusID</em>, <em>channelID</em>, <em>stringLengthFlag</em>, <em>dataStruct</em>) {#axontelegraphagetdatastruct}

</div>

Get the numeric values and string representations of all parameters from one 700A telegraph server and stores all values in a structure.

### *Parameters* {#axontelegraphagetdatastruct-parameters}

|  |  |
| --- | --- |
| *comPortID* | The Com Port ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *axoBusID* | The Axo Bus ID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *channelID* | The channelID number of the server, as provided by [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers). |
| *stringLengthFlag* | Pass 0 to return the short name of a parameter or 1 for the long name. See the details section of [AxonTelegraphAGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastring) for more information on this parameter. |
| *dataStruct* | An instance of the AxonTelegraph_DataStruct structure.  With the exception of the version field of this structure, all fields are output fields and will be overwritten by the XOP. |

### *Details* {#axontelegraphagetdatastruct-details}
Use this function if you wish to retrieve the numeric values and string representations of all parameters from one 700A telegraph server.  Calls to this function will return after the XOP receives data from the telegraph server or waits the duration of the timeout period.

This function expects that the data structure passed as the *dataStruct* parameter contains certain fields of a certain size.  One of these fields is the version field.  Before calling this function you must set the version field of your Igor structure to a valid value.  Currently, the only valid value is the number 13.  If dataStruct.version is not a valid value, this function will return a run time error in order to prevent a potential crash, which could result if the *dataStruct* structure parameter is not the same type of structure that the XOP expects.

Because this function takes an Igor structure as one of its parameters, it must be called from within another Igor function.

The AxonTelegraph_DataStruct structure is defined below.  You must copy this structure definition into an Igor procedure window to define it.  You may change the name of the structure, if you wish, but must not change the name, order, or data types of the structure's fields.

```igor
Structure AxonTelegraph_DataStruct
    uint32 Version	// Structure version.  Value should always be 13.
    uint32 SerialNum
    uint32 ChannelID
    uint32 ComPortID
    uint32 AxoBusID
    uint32 OperatingMode
    String OperatingModeString
    uint32 ScaledOutSignal
    String ScaledOutSignalString
    double Alpha
    double ScaleFactor
    uint32 ScaleFactorUnits
    String ScaleFactorUnitsString
    double LPFCutoff
    double MembraneCap
    double ExtCmdSens
    uint32 RawOutSignal
    String RawOutSignalString
    double RawScaleFactor
    uint32 RawScaleFactorUnits
    String RawScaleFactorUnitsString
    uint32 HardwareType
    String HardwareTypeString
    double SecondaryAlpha
    double SecondaryLPFCutoff
    double SeriesResistance
EndStructure
```

:::note
In some cases the value of ScaledOutSignalString and/or RawOutSignalString is "Unknown".  This happens when the values of the corresponding numerical parameters ScaledOutSignal and RawOutSignal are out of the range of values that are defined in the software development toolkit provided by Axon.  These out of range values only occur for output types that are unlikely to be used, so it is unlikely that you will have this problem.
:::

For simplicity, the same structure definition is used by [AxonTelegraphGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphgetdatastruct) and [AxonTelegraphAGetDataStruct](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastruct).  However, some of the properties that are available for 700B servers may not be available for 700A servers.  See the description of the [AxonTelegraphAGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatanum) function for additional information.

### *Examples* {#axontelegraphagetdatastruct-examples}

```igor
Function GetAxonTeleServerInfo()
    STRUCT AxonTelegraph_DataStruct tds
    tds.version = 13
    AxonTelegraphAGetDataStruct(1, 0, 1, 1, tds)
    print tds
End
```

### *See Also* {#axontelegraphagetdatastruct-see-also}
[AxonTelegraphAGetDataNum](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatanum), [AxonTelegraphAGetDataString](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphagetdatastring), [AxonTelegraphFindServers](/igorpro/extensions/data-acquisition/axontelegraph/axontelegraph-xop-operation-and-function-reference.md#axontelegraphfindservers)