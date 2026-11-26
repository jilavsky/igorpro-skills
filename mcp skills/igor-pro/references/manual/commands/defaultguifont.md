---
description: "The DefaultGUIFont operation changes the default font for user-defined controls and other Graphical User Interface elements."
slug: /commands/defaultguifont
---

<div className="command-signature">

## <strong>DefaultGUIFont</strong>  [/W=<em>winName</em> /Mac/Win] <em>group</em>= {<em>fNameStr</em>, <em>fSize</em>, <em>fStyle</em> } [, ...] {#defaultguifont}

</div>

The DefaultGUIFont operation changes the default font for user-defined controls and other Graphical User Interface elements.

### *Parameters* {#parameters}
*fNameStr* is the name of a font, *fSize*  is the size and *fStyle*  is a bitwise parameter with each bit controlling one aspect of the font style. See [Button](/igorpro/commands/button.md) for details about these parameters.

*group*  may be one of the following:


|  |  |
| --- | --- |
| all | All controls |
| button | Button and default CustomControl |
| checkbox | CheckBox controls |
| tabcontrol | TabControl controls |
| popup | Affects the font for text used in the icon (not the title) of a PopupMenu control. The text in the popped state is set by the system and cannot be changed. The title of a PopupMenu is affected by the all group but the icon text is not. |
| panel | Sets the default font for draw text in a panel. |
| graph | Sets the default font for overlay graphs. Size is used only if `ModifyGraph gfSize= -1`; style is not used. |
| table | Sets the default font for overlay tables. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Mac</span> | Changes control fonts only on Macintosh computers running Igor 9 or earlier. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Affects the named window or subwindow. When omitted, sets an experiment-wide default. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Win</span> | Changes  control fonts only only on Windows, and it affects the experiment whenever it is used on Windows. |

### *Details* {#details}
Although designed to be used before controls are created, calling DefaultGUIFont will update all affected windows with controls. This makes it easy to experiment with fonts. Keep in mind that fonts can cause compatibility problems when moving between machines or platforms.

The /Win flag indicates the platform on which the fonts are to be used. If the current platform is not the one specified, then the settings are not used but are remembered for use in window recreation macros or experiment recreation. This allows a user to create an experiment that will use different fonts depending on the current platform.

If the /W flag is used then the font settings apply only to the specified window (Graph or Panel.) If the /W flag is not used, then the settings are global to the experiment.

:::note
Use `/W=#` to refer to the current active subwindow.
:::

*fNameStr*  may be an empty string ("") to clear a group. Setting the font name to "_IgorSmall","_IgorMedium" or "_IgorLarge" will use Igor's own defaults.

### *Default Fonts and Sizes* {#default-fonts-and-sizes}
Igor's standard defaults for controls is the equivalent to setting all to "_IgorSmall", tabcontrol to "_IgorMedium" and button to "_IgorLarge". Use a *fSize*  of zero to also get the standard default for size. The three default fonts and sizes are all the same.


| Control | Font | Font Size |
| --- | --- | --- |
| Button | MS Shell Dlg+ | 12 |
| Checkbox | MS Shell Dlg | 12 |
| GroupBox | MS Shell Dlg | 12 |
| ListBox | MS Shell Dlg | 12 |
| PopupMenu* | MS Shell Dlg | 12 |
| SetVariable | MS Shell Dlg | 12 |
| Slider | MS Shell Dlg | 12 |
| TabControl | MS Shell Dlg | 12 |
| TitleBox | MS Shell Dlg | 12 |
| ValDisplay | MS Shell Dlg | 12 |

\* For the PopupMenu font or the popup menu itself, both fonts are MS Shell Dlg 12.

\+ MS Shell Dlg is a "virtual font name" which maps to Tahoma on Windows XP, to MS Sans Serif on Windows 7, and to Segoe UI on Windows 8 and Windows 10.

### *Example* {#example}

```igor
DefaultGUIFont/Mac all={"Zapf Chancery",12,0},panel={"geneva",12,3}
DefaultGUIFont/Win all={"Century Gothic",12,0},panel={"arial",12,3}
NewPanel
Button b0
DrawText 40,43,"Some text"
```

### *See Also* {#see-also}
[DefaultGUIControls](/igorpro/commands/defaultguicontrols.md)

[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Window Position Coordinates](/igorpro/user-interface/platform-related-issues.md#window-position-coordinates) and [Points Versus Pixels](/igorpro/user-interface/platform-related-issues.md#points-versus-pixels) for explanations of how font sizes in panels are interpreted for various screen resolutions.

### *Demos* {#demos}
[Open All Controls Demo](#igor-pxp/Examples/Feature__Demos__2/All__Controls__Demo.pxp)