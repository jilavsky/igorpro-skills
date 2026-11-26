---
description: "The ControlInfo operation returns information about the state or status of the named control in a graph or panel window or subwindow."
slug: /commands/controlinfo
---

<div className="command-signature">

## <strong>ControlInfo</strong>  [/W=<em>winName</em> ] <em>controlName</em> {#controlinfo}

</div>

The ControlInfo operation returns information about the state or status of the named control in a graph or panel window or subwindow.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/G [ = *doGlobal*]</span> | If *doGlobal* is non-zero or absent, the position returned via V_top and V_left is in global screen coordinates rather relative to the window containing the control. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Looks for the control in the named graph or panel window or subwindow. If /W is omitted, ControlInfo looks in the top graph or panel window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Parameters* {#parameters}
*controlName* is the name of a control in the window specified by /W or in the top graph or panel window. *controlName*  may also be the keyword `kwBackgroundColor` to set V_Red, V_Green, V_Blue and V_Alpha, the keyword `kwControlBar`, `kwControlBarTop`, or `kwControlBarBottom` to set V_Height, the keyword `kwControlBarLeft` or `kwControlBarRight` to set V_Width, or the keyword `kwSelectedControl` to set S_Value and V_flag.

### *Details* {#details}
Information for all controls is returned via the following string and numeric variables. Coordinates are returned in [control panel units](/igorpro/user-interface/controls.md#control-panel-units).

|  |  |
| --- | --- |
| `S_recreation` | Commands to recreate the named control. |
| `S_title` | Title of the named control. |
| `V_disable` | Control's disable state: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Normal (enabled, visible).</td></tr><tr><td>1:</td><td>Hidden.</td></tr><tr><td>2:</td><td>Disabled, visible.</td></tr></tbody></table>
| `V_Height`, `V_Width`, `V_top`, `V_left`, `V_right`, `V_pos`, `V_align` |  |
|  | Dimensions and position of the named control in [control panel units](/igorpro/user-interface/controls.md#control-panel-units). |
|  | `V_right`, `V_pos`, and `V_align` were added in Igor Pro 8.00 and depend on whether the align keyword was applied to the control (e.g., Button *name* align=1). |
|  | `V_align` is 1 if the the align keyword was applied to the control or to 0 otherwise. |
|  | `V_pos` is the horizontal coordinate used to position the control. It represents the position of the left end of the control if the align keyword was omitted or of the right end if the align keyword was applied. |
|  | `V_left` and `V_right` are the the horizontal coordinates of the left and right ends of the control regardless of whether the align keyword was applied or not. |
|  |  |

The kind of control is returned in `V_flag` as a positive or negative integer. A negative value indicates the control is incomplete or otherwise not active. If `V_flag` is zero, then the named control does not exist. Information returned for specific control types is as follows:

- [Button](/igorpro/commands/button.md)

|  |  |
| --- | --- |
| `V_flag` | 1 |
| `V_Value` | Tick count of last mouse up. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [Chart](/igorpro/commands/chart.md)

|  |  |
| --- | --- |
| `V_flag` | 6 or -6 |
| `V_Value` | Current point number. |
| `S_Value` | Keyword-packed information string. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [CheckBox](/igorpro/commands/checkbox.md)

|  |  |
| --- | --- |
| `V_flag` | 2 |
| `V_Value` | 0 if it is deselected or 1 if it is selected. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [CustomControl](/igorpro/user-interface/controls.md#customcontrol) 

|  |  |
| --- | --- |
| `V_flag` | 12 |
| `V_Value` | Tick count of last mouse up. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [GroupBox](/igorpro/user-interface/controls.md#groupbox)

|  |  |
| --- | --- |
| `V_flag` | 9 |
| `S_Value` | Title text. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [ListBox](/igorpro/user-interface/controls.md#listbox)

|  |  |
| --- | --- |
| `V_flag` | 11 |
| `V_Value` | Currently selected row (valid for mode 1 or 2 or modes 5 and 6 when no selWave is used). If no list row is selected, then it is set to -1. |
| `V_selCol` | Currently selected column (valid for modes 5 and 6 when no selWave is used). |
| `V_horizScroll` | Number of pixels the list has been scrolled horizontally to the right. |
| `V_vertScroll` | Number of pixels the list has been scrolled vertically downwards. |
| `V_rowHeight` | The height of a row in pixels. |
| `V_startRow` | The current top visible row. |
| `S_columnWidths` |  |
|  | A comma-separated list of column widths in pixels. |
| `S_DataFolder` | Full path to listWave (if any). |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
| `S_Value` | Name of listWave (if any). |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [PopupMenu](/igorpro/commands/popupmenu.md)

|  |  |
| --- | --- |
| `V_flag` | 3 or -3 |
| `V_Red`, `V_Green`, `V_Blue`, `V_Alpha` |  |
|  | For color array pop-up menus, these are the encoded color values. |
| `V_Value` | Current item number (counting from one). |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
| `S_Value` | Text of the current item. If PopupMenu is a color array then it contains color values encoded as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [SetVariable](/igorpro/user-interface/controls.md#setvariable)

|  |  |
| --- | --- |
| `V_flag` | 5 or -5 |
| `V_Value` | Value of the variable. If the SetVariable is used with a string variable, then it is the interpretation of the string as a number, which will be NaN if conversion fails. |
| `S_DataFolder` | Full path to the variable. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
| `S_Value` | Name of the variable or, if the value was set using _STR: syntax, the string value itself. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [Slider](/igorpro/commands/slider.md) 

|  |  |
| --- | --- |
| `V_flag` | 7 |
| `V_Value` | Numeric value of the variable. |
| `S_DataFolder` | Full path to the variable. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
| `S_Value` | Name of the variable. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |
|  |  |

- [TabControl](/igorpro/user-interface/controls.md#tabcontrol) 

|  |  |
| --- | --- |
| `V_flag` | 8 |
| `V_Value` | Number of the current tab. |
| `S_UserData` | Primary (unnamed) user data text. For any named user data, you must use the [GetUserData](/igorpro/commands/getuserdata.md) function. |
| `S_Value` | Tab text. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- [Operations[TitleBox]](/igorpro/commands/titlebox.md)

|  |  |
| --- | --- |
| `V_flag` | 10 |
| `S_DataFolder` | Full path if text is from a string variable. |
| `S_Value` | Name if text is from a string variable. |
| `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left` |  |
|  | See descriptions above. |
| `V_right`, `V_pos`, `V_align` |  |
|  | See ***TitleBox Positioning*** under [Operations[TitleBox]](/igorpro/commands/titlebox.md) for details. |

- [ValDisplay](/igorpro/commands/valdisplay.md) 

|  |  |
| --- | --- |
| `V_flag` | 4 or -4 |
| `V_Value` | Displayed value. |
| `S_Value` | Text of expression that ValDisplay evaluates. |
    | `S_recreation`, `V_disable`, `V_Height`, `V_Width`, `V_top`, `V_left`,<br>`V_right`, `V_pos`, `V_align` |  |
|  | See descriptions above. |

- ***kwBackgroundColor***

|  |  |
| --- | --- |
| `V_Red`, `V_Green`, `V_Blue`, `V_Alpha` |  |
|  | If *controlName* is kwBackgroundColor then it is the color of the control panel background. This color is usually the default user interface background color, as set by the Appearance tab of the Display Properties, until changed by ModifyPanel cbRGB. |

- ***kwControlBar** or **kwControlBarTop***

|  |  |
| --- | --- |
| `V_Height` | The height in pixels of the top control bar area in a graph as set by [ControlBar](/igorpro/commands/controlbar.md). |

- ***kwControlBarBottom***

|  |  |
| --- | --- |
| `V_Height` | The height in pixels of the bottom control bar area in a graph as set by [ControlBar](/igorpro/commands/controlbar.md)/B. |

- ***kwControlBarLeft***

|  |  |
| --- | --- |
| `V_Width` | The width in pixels of the left control bar area in a graph as set by [ControlBar](/igorpro/commands/controlbar.md)/L. |

- ***kwControlBarRight***

|  |  |
| --- | --- |
| `V_Width` | The width in pixels of the right control bar area in a graph as set by [ControlBar](/igorpro/commands/controlbar.md)/R. |

- ***kwSelectedControl***

|  |  |
| --- | --- |
| `V_flag` | Set to 1 if a control is selected or 0 if not. |
|  | [SetVariable](/igorpro/user-interface/controls.md#setvariable) and [ListBox](/igorpro/user-interface/controls.md#listbox) controls can be selected, most other controls cannot. |
| `S_Value` | Name of selected control (if any) or "". |

The following applies only to the keyword-packed information string stored in S_value for a chart recorder. S_value will consist of a sequence of sections with the form:  "*keyword*:*value*;" You can pick a value out of a keyword-packed string using the [NumberByKey](/igorpro/commands/numberbykey.md) and [StringByKey](/igorpro/commands/stringbykey.md) functions. Here are the keywords for S_value for a chart recorder:


| Keyword | Type | Meaning |
| --- | --- | --- |
| `FNAME` | string | Name of the FIFO chart is monitoring. |
| `LHSAMP` | number | Left hand sample number. |
| `NCHANS` | number | Number of channels displayed in chart recorder. |
| `PPSTRIP` | number | The chart recorder's points per strip value. |
| `RHSAMP` | number | Right hand sample number (same as V_value). |

In addition, ControlInfo writes fields to `S_value` for each channel in the chart recorder. The keyword for the field is a combination of a name and a number that identify the field and the channel to which it refers. For example, if channel 4 is named "Pressure" then the following would appear in the S_value string: "CHNAME4:Pressure". In the following table, the channel's number is represented by #:


| Keyword | Type | Meaning |
| --- | --- | --- |
| `CHCTAB#` | number | Channel's color table value as set by Chart ctab keyword. |
| `CHGAIN#` | number | Channel's gain value as set by Chart gain keyword. |
| `CHNAME#` | string | Name of channel defined by FIFO. |
| `CHOFFSET#` | number | Channel's offset value as set by Chart offset keyword. |

### *Examples* {#examples}

```igor
ControlInfo myChart; Print S_Value
```

Results in the following being printed to the history area:


```igor
FNAME:myFIFO;NCHANS:1;PPSTRIP:1100;RHSAMP:271;LHSAMP:-126229;
```

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

The [ControlInfo](/igorpro/commands/controlinfo.md) operation for information about the control.

The [GetUserData](/igorpro/commands/getuserdata.md) function for retrieving named user data.