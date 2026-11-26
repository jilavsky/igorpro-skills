---
description: "These keywords appear after a macro or function declaration and tell Igor that the macro or function is a special type of procedure."
slug: /programming/keywords/procedure-subtype-keywords
---

These keywords appear after a macro or function declaration and tell Igor that the macro or function is a special type of procedure. For example, marking a procedure as Graph or GraphStyle tells Igor that the name of the procedure should appear in the Windows→Graph Macros submenu.

<div className="command-signature">

## <strong>ButtonControl</strong> {#buttoncontrol}

</div>

ButtonControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined button control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [Button](/igorpro/commands/button.md) for details on creating a button control.

<div className="command-signature">

## <strong>CameraWindow</strong> {#camerawindow}

</div>

CameraWindow is no longer supported, as of Igor 10.00.

CameraWindow was a procedure subtype keyword that identified a macro as being a camera window recreation macro. It was automatically used by Igor when Igor created a window recreation macro for a camera window. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>CDFFunc</strong> {#cdffunc}

</div>

CDFFunc is a procedure subtype keyword that identifies a function as being suitable for calling from the [StatsKSTest](/igorpro/commands/statskstest.md) operation.

<div className="command-signature">

## <strong>CheckboxControl</strong> {#checkboxcontrol}

</div>

CheckBoxControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined checkbox control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [Checkbox](/igorpro/commands/checkbox.md) for details on creating a checkbox control.

<div className="command-signature">

## <strong>CursorStyle</strong> {#cursorstyle}

</div>

CursorStyle is a procedure subtype keyword that puts the name of the procedure in the "Style function" submenu of the Cursor Info pop-up menu. It is automatically used by Igor when Igor creates a cursor style function. To have Igor create a cursor style function, select "Save style function" in the "Style function" submenu of the Cursor Info pop-up menu.

See also [Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors).

<div className="command-signature">

## <strong>DrawUserShape</strong> {#drawusershape}

</div>

DrawUserShape is a procedure subtype keyword that marks a function as suitable for drawing a user-defined drawing object. See [Operations[DrawUserShape]](/igorpro/commands/drawusershape.md).

<div className="command-signature">

## <strong>FitFunc</strong> {#fitfunc}

</div>

Marks a user function as a user-defined curve fit function. By default, only functions marked with this keyword are displayed in the Function menu in the Curve Fit dialog.

If you wish other functions to be displayed in the Function menu, you can check the checkbox labelled "Show old-style functions (missing FitFunc keyword)".

<div className="command-signature">

## <strong>GizmoPlot</strong> {#gizmoplot}

</div>

GizmoPlot is a procedure subtype keyword that identifies a macro as being a Gizmo recreation macro. It is automatically used by Igor when Igor creates a window recreation macro for a Gizmo plot. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>Graph</strong> {#graph}

</div>

Graph is a procedure subtype keyword that identifies a macro as being a graph recreation macro. It is automatically used by Igor when Igor creates a window recreation macro for a graph. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>GraphMarquee</strong> {#graphmarquee}

</div>

GraphMarquee is a procedure subtype keyword that puts the name of the procedure in the graph Marquee menu. See [Marquee Menus](/igorpro/user-interface/user-defined-menus.md#marquee-menus) for details.

<div className="command-signature">

## <strong>GraphStyle</strong> {#graphstyle}

</div>

GraphStyle is a procedure subtype keyword that puts the name of the procedure in the Style pop-up menu of the New Graph dialog and in the Graph Macros menu. It is automatically used by Igor when Igor creates a graph style macro. To have Igor create a graph style macro, use the Windows→Control→Window Control dialog. See [Graph Style Macros](/igorpro/graphing/graphs.md#graph-style-macros) for details.

<div className="command-signature">

## <strong>GridStyle</strong> {#gridstyle}

</div>

GridStyle is a procedure subtype keyword that puts the name of the procedure in the Grid→Style Function submenu of the mover pop-up menu in the drawing tool palette. You can have Igor automatically create a grid style function for you by choosing Save Style Function from that submenu.

<div className="command-signature">

## <strong>Layout</strong> {#layout}

</div>

Layout is a procedure subtype keyword that identifies a macro as being a page layout recreation macro. It is automatically used by Igor when Igor creates a window recreation macro for a layout. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>LayoutMarquee</strong> {#layoutmarquee}

</div>

LayoutMarquee is a procedure subtype keyword that puts the name of the procedure in the layout Marquee menu. See [Marquee Menus](/igorpro/user-interface/user-defined-menus.md#marquee-menus) for details.

<div className="command-signature">

## <strong>LayoutStyle</strong> {#layoutstyle}

</div>

LayoutStyle is a procedure subtype keyword that puts the name of the procedure in the Style pop-up menu of the New Layout dialog and in the Layout Macros menu. It is automatically used by Igor when Igor creates a layout style macro. To have Igor create a layout style macro, use the Windows→Control→ Window Control dialog. See [Page Layout Style Macros](/igorpro/graphing/making-figures/page-layouts.md#page-layout-style-macros) for details.

<div className="command-signature">

## <strong>ListBoxControl</strong> {#listboxcontrol}

</div>

ListBoxControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined listbox control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [ListBox](/igorpro/user-interface/controls.md#listbox) for details on creating a listbox control.

<div className="command-signature">

## <strong>Panel</strong> {#panel}

</div>

Panel is a procedure subtype keyword that identifies a macro as being a control panel recreation macro. It is automatically used by Igor when Igor creates a window recreation macro for a control panel. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>PopupMenuControl</strong> {#popupmenucontrol}

</div>

PopupMenuControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined pop-up menu control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [PopupMenu](/igorpro/commands/popupmenu.md) for details on creating a popup menu control.

<div className="command-signature">

## <strong>SetVariableControl</strong> {#setvariablecontrol}

</div>

SetVariableControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined SetVariable control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [SetVariable](/igorpro/user-interface/controls.md#setvariable) for details on creating a SetVariable control.

<div className="command-signature">

## <strong>SliderControl</strong> {#slidercontrol}

</div>

SliderControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined slider control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [Slider](/igorpro/commands/slider.md) for details on creating a slider control.

<div className="command-signature">

## <strong>TabControl</strong> {#tabcontrol}

</div>

TabControl is a procedure subtype keyword that identifies a macro or function as being an action procedure for a user-defined tab control. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details. See [Operations[TabControl]](/igorpro/commands/tabcontrol.md) for details on creating a tab control.

<div className="command-signature">

## <strong>Table</strong> {#table}

</div>

Table is a procedure subtype keyword that identifies a macro as being a table recreation macro. It is automatically used by Igor when Igor creates a window recreation macro for a table. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) and [Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro) for details.

<div className="command-signature">

## <strong>TableStyle</strong> {#tablestyle}

</div>

TableStyle is a procedure subtype keyword that puts the name of the procedure in the Style pop-up menu of the New Table dialog and in the Table Macros menu. It is automatically used by Igor when Igor creates a table style macro. To have Igor create a table style macro, use the Windows→Control→Window Control dialog. See [Table Style Macros](/igorpro/igor-basics/tables.md#table-style-macros) for details.