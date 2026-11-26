---
description: "This file describes what is new in Igor Pro 10 relative to Igor Pro 9. It references topics in other help files."
slug: /igor-pro-10/what-s-new-in-igor-pro-10
---

# What's New in Igor Pro 10? {#what-s-new-in-igor-pro-10}

This file describes what is new in Igor Pro 10 relative to Igor Pro 9. It references topics in other help files.

We maintain a list of Frequently Asked Questions about new and changed features at: [https://www.wavemetrics.com/support/faq](https://www.wavemetrics.com/support/faq)


## Version Compatibility in Igor Pro 10 {#version-compatibility-in-igor-pro-10}

Igor Pro 10 can read files created by all earlier versions of Igor.

If you do not use features that are introduced in Igor Pro 10, then experiment files saved by Igor Pro 10 are readable by earlier versions.

Once you use features added in Igor Pro 10 and save an experiment file, that file may cause errors if you try to read it in an earlier version of Igor. Just in case you need to go back to an earlier version of Igor, it is a good idea to make backup copies of all your Igor files now.

Some behaviors have changed slightly in Igor Pro 10. These changes may affect some existing Igor experiments. See [Behavior Changes in Igor Pro 10](#behavior-changes-in-igor-pro-10) for details.

### Igor Pro 10 is a 64-bit Application {#igor-pro-10-is-a-64-bit-application}
Unlike Igor Pro versions 7-9, which shipped as both 32-bit and 64-bit applications, Igor Pro 10 is 64-bit only. This means that any XOPs you use with Igor Pro 10 must also be 64-bit.

Igor Pro 10 is a native x64 application and WaveMetrics only supports running Igor Pro 10 on machines with Intel/AMD CPUs. However, the Igor Pro 10 installer should also allow Igor to be installed on Windows ARM64 machines (both virtual and non-virtual). In order to run Igor 10, your machine/OS will need to support x64 emulation (we recommend Windows 11 24H2 or later for best results). Note that WaveMetrics does not explicitly support running Igor Pro 10 under ARM emulation, but we may do so in the future. Please report bugs to us if you are using such a configuration, but realize that our ability to fix them may be limited.

### Igor Pro 10 Language Support {#igor-pro-10-language-support}
Igor Pro 10 automatically uses the language of your operating system to determine the language that is used for the user interface and documentation. In earlier versions, WaveMetrics provided separate English and Japanese applications which required separate licenses. This means that if you run Igor and your OS language is Japanese, Igor will also use Japanese. You can change this behavior if you want. See [Language Selection](/igorpro/igor-basics/using-igor.md) for more information. Currently almost all documentation is in English only. This might change in the future.


## Features Removed From Igor Pro 10 {#features-removed-from-igor-pro-10}
- The PDF manual has been removed.

- The operations [NewCamera](/igorpro/commands/newcamera.md), [ModifyCamera](/igorpro/commands/modifycamera.md) and [GetCamera](/igorpro/commands/getcamera.md) are no longer supported. Camera support is provided using the MMI XOP (see below).

## XOP Changes in Igor Pro 10 {#xop-changes-in-igor-pro-10}
### New XOPs in Igor Pro 10: {#new-xops-in-igor-pro-10}
- The new MMI XOP, which uses the popular Micro-Manager project, allows you to control a wide range of hardware such as scientific cameras, light-sources, shutters, filter-wheels, XY- and Z-axis stages, etc. See [MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md) for details.

### XOPs Removed From Igor Pro 10 {#xops-removed-from-igor-pro-10}

- The MultiClamp700xCommander XOP has been removed. It was considered obsolete in Igor Pro 9 and was 32-bit only. A 64-bit fork of the XOP, maintained by a third-party, is available at [https://github.com/AllenInstitute/mcc-xop](https://github.com/AllenInstitute/mcc-xop). WaveMetrics has not used this third-party XOP and cannot provide support.

- The IgorGIS XOP has been removed. It was marked as obsolete in Igor Pro 9 because we no longer have the expertise to maintain the XOP, update third-party libraries it uses when security fixes are available, and answer support questions. If you have the 64-bit IgorGIS64.xop that shipped with Igor Pro 9 you can likely still use that XOP with Igor Pro 10.

### Packages Made Obsolete in Igor Pro 10 {#packages-made-obsolete-in-igor-pro-10}

The usual reason for making a package obsolete is that a newer, better way to accomplish it is available. Since you may have old experiment files that depend on such packages, we never actually remove them.

- The Percentile and Box Plot package is obsolete and has been moved to the WaveMetrics Procedures\\Obsolete folder. References to the package have been removed from the Packages menus. You can still use it, but the built-in box plots are superior (see [Box Plots and Violin Plots](/igorpro/graphing/graphs.md#box-plots-and-violin-plots)). If you really want to use the procedure package:

    ```igor
    #include <Percentile and Box Plot>
    ```

## Guide To Igor Pro 10 Improvements {#guide-to-igor-pro-10-improvements}

Here are the Igor Pro 10 improvements discussed in this file

[Python Integration in Igor Pro 10](#python-integration-in-igor-pro-10)<br>
[Performance Improvements in Igor Pro 10](#performance-improvements-in-igor-pro-10)<br>
[Display Improvements in Igor Pro 10](#display-improvements-in-igor-pro-10)<br>
[User-Interface Improvements in Igor Pro 10](#user-interface-improvements-in-igor-pro-10)<br>
[Behavior Changes in Igor Pro 10](#behavior-changes-in-igor-pro-10)<br>
[Programming Changes in Igor Pro 10](#programming-changes-in-igor-pro-10)<br>
[Programming Improvements in Igor Pro 10](#programming-improvements-in-igor-pro-10)<br>
[Function and Operation Improvements in Igor Pro 10](#function-and-operation-improvements-in-igor-pro-10)<br>
[Data Browser Improvements in Igor Pro 10](#data-browser-improvements-in-igor-pro-10)<br>
[Window Browser Improvements in Igor Pro 10](#window-browser-improvements-in-igor-pro-10)<br>
[Dialog Improvements in Igor Pro 10](#dialog-improvements-in-igor-pro-10)<br>
[Graphing Improvements in Igor Pro 10](#graphing-improvements-in-igor-pro-10)<br>
[Box and Violin Plot Improvements in Igor Pro 10](#box-and-violin-plot-improvements-in-igor-pro-10)<br>
[Table Improvements in Igor Pro 10](#table-improvements-in-igor-pro-10)<br>
[Page Layout Improvements in Igor Pro 10](#page-layout-improvements-in-igor-pro-10)<br>
[Notebook Improvements in Igor Pro 10](#notebook-improvements-in-igor-pro-10)<br>
[Help Improvements in Igor Pro 10](#help-improvements-in-igor-pro-10)<br>
[Graphics Export Improvements in Igor Pro 10](#graphics-export-improvements-in-igor-pro-10)<br>
[Procedure Window Improvements in Igor Pro 10](#procedure-window-improvements-in-igor-pro-10)<br>
[Gizmo Improvements in Igor Pro 10](#gizmo-improvements-in-igor-pro-10)<br>
[Drawing Improvements in Igor Pro 10](#drawing-improvements-in-igor-pro-10)<br>
[Annotation Improvements in Igor Pro 10](#annotation-improvements-in-igor-pro-10)<br>
[Control and Control Panel Improvements in Igor Pro 10](#control-and-control-panel-improvements-in-igor-pro-10)<br>
[Analysis Improvements in Igor Pro 10](#analysis-improvements-in-igor-pro-10)<br>
[Statistics Improvements in Igor Pro 10](#statistics-improvements-in-igor-pro-10)<br>
[Matrix Improvements in Igor Pro 10](#matrix-improvements-in-igor-pro-10)<br>
[Multipeak Fitting Improvements in Igor Pro 10](#multipeak-fitting-improvements-in-igor-pro-10)<br>
[Image Processing Improvements in Igor Pro 10](#image-processing-improvements-in-igor-pro-10)<br> 
[Data Import And Export Improvements in Igor Pro 10](#data-import-and-export-improvements-in-igor-pro-10)<br>
[Miscellaneous Improvements in Igor Pro 10](#miscellaneous-improvements-in-igor-pro-10)<br>
[New And Improved Packages in Igor Pro 10](#new-and-improved-packages-in-igor-pro-10)<br>
[New And Improved Example Experiments in Igor Pro 10](#new-and-improved-example-experiments-in-igor-pro-10)<br>

## Python Integration in Igor Pro 10 {#python-integration-in-igor-pro-10}

Igor Pro is now capable of direct, bi-directional communication with the Python programming language (see [Python Overview](/igorpro/python/python-overview.md)).

Call your favorite Python libraries from Igor procedure code using the [Python](/igorpro/commands/python.md) and [PythonFile](/igorpro/commands/pythonfile.md) operations, or execute Python code line-by-line using our dedicated [Python Console](/igorpro/python/python-overview.md#python-console) at Python🠖Open Console.

<img src="MD_images/Whats_New_In_Igor_Pro_10/python_console.png" alt="Python Console" width="75%"/>

The igorpro Python module that is shipped with Igor Pro 10 provides an intuitive API for passing data back and forth between Python and Igor (see [Python Module Reference](/igorpro/python/python-module-reference.md)). It has built-in conversions with the NumPy library ([https://numpy.org/](https://numpy.org/)), so that passing waves into analysis functions that expect a NumPy array is relatively simple:

```python
import igorpro
import numpy as np

# Get a list of Igor waves inside a data folder
dataset = igorpro.folder('root:analysis').waves()
for wave in dataset:
    # Convert each wave into a numpy array and run the analysis
    results = runCalculations(wave.asarray())
```

Pass Python objects back to Igor, which are automatically converted into the appropriate Igor types:
```igor
// Run a Python function that returns a numpy array, and return it to an existing Igor wave
Make/FREE arrayFromPython
Python execute = "arr : ndarray = waveAnalysis()", array = {"arr", arrayFromPython}
```

## Performance Improvements in Igor Pro 10 {#performance-improvements-in-igor-pro-10}

- Improved performance of [NewPath](/igorpro/commands/newpath.md) and [IndexedFile](/igorpro/commands/indexedfile.md), particularly in code similar to the `PrintFoldersAndFiles` example function in the [IndexedDir](/igorpro/commands/indexeddir.md) help topic.

- When running on Windows 11, [MultiThread](/igorpro/programming/keywords/other-programming-keywords.md#multithread) and [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md) can now use as many logical processors (threads) as the hardware supports. Previously Igor only used up to 100 logical processors even if more were available. Due to operating system limitations, when running on Windows 10 only 64 logical processors can be used.

## Display Improvements in Igor Pro 10 {#display-improvements-in-igor-pro-10}

Qt and WaveMetrics have improved the handling of screens having various Windows Display Settings scaling factors:

- Improved quality of graphics for a variety of applications when displaying on a monitor with a fractional scaling factor (that is, Display Scaling Factor of percentages not an integer multiple of 100%). This work is happening incrementally-please tell us if you use such a monitor and find something ugly at 125%, 150%, 175%.

- Improved handling of mixed monitor resolution. If you move Igor's MDI window (the big window containing all graphs, tables, etc.) from a one monitor to another with different Display Scaling Factor, you will see graphs redraw, etc. to adjust to the new resolution.

With that said, there are still some known problems that sometimes happen when using a scaling factor that is not a multiple of 100%:

- Graphics glitches around window frames:

    <img src="MD_images/Whats_New_In_Igor_Pro_10/window_scaling_glitches.png" alt="Window scaling glitches" width="75%"/>

    You can temporarily clear these glitches by resizing Igor's main window slightly or by minimizing and then restoring the main window.

- Text glitches (seen here on the rotated `0` characters on the left axis):

    <img src="MD_images/Whats_New_In_Igor_Pro_10/text_scaling_glitches.png" alt="Text scaling glitches"/>

    These glitches are not known to occur when exporting graphics or copying to the clipboard.

- Sizing/positioning glitches

    We see issues in which the size or position of some part of a window changes by a small amount (usually 1 or 2 pixels) when moved or resized. The example below shows title bar buttons that are slightly different sizes but the same thing can be seen with drawing of objects in windows such as axes, tick labels, etc.

   <img src="MD_images/Whats_New_In_Igor_Pro_10/titlebar_scaling_glitches.png" alt="Title bar scaling glitches"/>

- Window title bar buttons sometimes do not work

    In some cases clicking on the minimize, maximize, and/or normalize buttons in a window's toolbar has no effect. Other than changing the display's scaling factor, a workaround for this is to use a different style. Select the Misc🠖Miscellaneous Settings menu item to open the Miscellaneous Settings dialog, then select the Miscellaneous category, then check the Use Fusion Style checkbox.

    A temporary workaround is to right-click on the title bar and use the contextual menu to control the window instead of clicking the buttons.

Setting your display scaling factor to 100% or 200% in Windows Settings typically eliminates all of these issues. We will continue to work to address these kind of problems, but we think some of them are problems in Qt, so our ability to fix or workaround the problems may be limited.

Since it is difficult to test multiple configurations and situations, if you encounter apparent scaling problems other than those above, please report the problems to support@wavemetrics.com. Make sure that you include the information in the Help🠖System Information dialog.

## User-Interface Improvements in Igor Pro 10 {#user-interface-improvements-in-igor-pro-10}

- [Control Panel Expansion](/igorpro/user-interface/controls.md#control-panel-expansion) can be disabled in the Misc🠖Miscellaneous Settings dialog.

- Experiment startup commands and recreation macros can be viewed in the File🠖Experiment Info dialog.

- The Graph🠖Select Control submenu previews which control will be selected by drawing a red rectangle around it.

- Added a grid submenu to the draw tools contextual menu. Right-click in a control or graph while in Draw mode and select Grid to use (see [Modes of Operation](/igorpro/user-interface/controls.md#modes-of-operation)).

## Behavior Changes in Igor Pro 10 {#behavior-changes-in-igor-pro-10}

- The default behavior of scrolling the mouse wheel in a Gizmo window has been changed from rotate to zoom. You can change this setting in the Gizmo category of the Misc🠖Miscellaneous Settings dialog.

- [Listbox](/igorpro/user-interface/controls.md#listbox) controls using special mode 1 and 2 (see the Listbox *special* keyword) now honor the control's font settings when drawing the title on the picture in each listbox cell. Because previously the text was drawn using some poorly defined default font, this will cause a slight change in Listbox controls that don't set font, font size or font style. In our testing the font size before this fix was 10, the default is 12. If you have set font, font size or font style, you will see a potentially large change in appearance because those settings will now be honored.

- Menu item text sent to [PopupMenu](/igorpro/commands/popupmenu.md) action procedures has (the rarely used) menu accelerator '&' character(s) removed so that the text looks like what you see in the menu item. This applies in other cases where the menu item text is returned to, say, [ControlInfo](/igorpro/commands/controlinfo.md), [GetLastUserMenuInfo](/igorpro/commands/getlastusermenuinfo.md), and [DoIgorMenu](/igorpro/commands/doigormenu.md) via ``S_value`` or [PopupContextualMenu](/igorpro/commands/popupcontextualmenu.md) via ``S_selection``. [PopupMenu](/igorpro/commands/popupmenu.md) ``popMatch`` accepts strings with or without the accelerator '&' characters for backwards compatibility. This mostly applies to menu items with "&&" in them that are intended to display a single "&", but that didn't display properly in PopupMenus before Igor 10.

- **Printing from threads:** In Igor Pro 10, limits on the number of history lines that could be printed from an Igor pre-emptive thread (see [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)) have been removed. Igor 10 also improves ordering of output lines between the main thread and preemptive threads. These changes affect anything that puts text into the history window. That includes the [Print](/igorpro/commands/print.md) and [printf](/igorpro/commands/printf.md) operations and any operation that prints results in the history, such as [CurveFit](/igorpro/commands/curvefit.md). We presume that use of the Print and printf operations in threaded code is primarily for debugging, and that you will want to see all of your printed output. Removing the limit, however, has the potential to print huge amounts of text to the history, with extreme effects on performance.

- Because of the possibility of harmful effects of runaway printing from threads, we have added a new [SetIgorOption](/igorpro/commands/setigoroption.md) keyword that allows you to reestablish limits. For more information, see the `Printing from Threads` subsection in the documentation for the [Print](/igorpro/commands/print.md) operation.

- When dragging drawing objects to resize, reposition, or rotate, the drag is now live. That is, the objects are changed as you drag. Previously, an outline showed the result you would get and the objects weren't changed until you released the mouse.

- Graph🠖Show Trace Info Tags and Table🠖Show Column Info Tags no longer affect the display of tooltips which are controlled by a tooltip hook function. Programmers are encouraged to add an easy way to their UI for users to turn on and off any tooltips that are controlled by tooltip hook functions.

- [CleanupName](/igorpro/commands/cleanupname.md) no longer ignores the *maxBytes* parameter when called from a threadsafe user-defined function.

## Programming Changes in Igor Pro 10 {#programming-changes-in-igor-pro-10}

- In Igor 10, graph window hook functions are now called for mouse move, mouse down, and mouse up when the mouse is over an annotation. In Igor 9 and earlier this event was claimed by Igor and never arrived at the window hook function.

- Igor 10 no longer marks an experiment as needing to be saved when a global variable or string is assigned to the same value it already had. If this change causes a problem in your code, call the [ExperimentModified](/igorpro/commands/experimentmodified.md) command to mark the experiment as needing to be saved.

- As of Igor 10, the main Procedure window may now have a regular module name defined for it with:

    ```igor
    #pragma moduleName = name
    ```

    See [The ModuleName Pragma](/igorpro/programming/programming.md#the-modulename-pragma).

- Igor 10's compiler will refuse to compile "unreachable" code in switch and strswitch statements, such as the two print statements in this code:

    ```igor
    switch(val)
        print "001" // Igor 10 will stop compiling here because this code will never be executed
        case 1:
        ...
        break
        print "002" // same thing: a compile error because of unreachable code
        break
        default:
        ...
        break
    endswitch
    ```

- Debug on User Abort no longer invokes the debugger if a programmatic [Abort](/igorpro/commands/abort.md),  [AbortOnRTE](/igorpro/programming/keywords/flow-control.md#abortonrte) or [AbortOnValue](/igorpro/programming/keywords/flow-control.md#abortonvalue) operation is called; the debugger is invoked only when the **user** aborts execution by clicking the Abort button in the status bar when it is relabeled to "Debug". See [Debugging on Error](/igorpro/programming/debugging.md#debugging-on-error).

- The [AnnotationInfo](/igorpro/commands/annotationinfo.md) function now returns "" if the window has no annotations or if the named annotation does not exist. Before Igor 10 these conditions would cause a runtime error.

- The [PauseForUser](/igorpro/commands/pauseforuser.md) operation now issues an error if your main window or target window are missing or of the wrong type.

## Programming Improvements in Igor Pro 10 {#programming-improvements-in-igor-pro-10}

- Constants in other independent modules or regular modules can be referenced just like functions can using double or triple names.

- Static constants in regular modules can be accessed by double names.

    For example:
    ```igor
    switch(val)
        case OtherIM#regularModuleInOtherIM#staticConstantName:
        ...
        break
        case OtherRegularModule#staticConstantName:
        ...
        break
    endswitch
    ```

- Errors in preemptive threads now return nearly as much information as those in the main thread.

- [The Debugger](/igorpro/programming/debugging.md#the-debugger) Objects List and structure contents can be sorted by name or type.

- The Debugger's tooltip and expression inspectors show the value of a symbolic path when given the literal symbolic name of the path. A new Symbolic Paths inspector has also been added.

- When calling a function through [Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment) auto indexing The Debugger now shows in the caller function the current values of [p](/igorpro/commands/p.md), [q](/igorpro/commands/q.md), [r](/igorpro/commands/r.md), [s](/igorpro/commands/s.md) in use by the called function.

- The Debugger can step into/through [Threadsafe Functions](/igorpro/programming/programming.md#threadsafe-functions) called from the main thread.

- Graph style macros that take a string and a variable as the first two parameters can be used as append style macros:

    - The graph name and number of already-existing traces in that graph are passed in, and any remaining parameters are not filled in (which might invoke a [Missing Parameter Dialog](/igorpro/user-interface/dialog-help.md#missing-parameter-dialog)).
    - See [Dialog Improvements in Igor Pro 10](#dialog-improvements-in-igor-pro-10) for how these graph style macros with parameters can be used in the append dialogs.

- [Line Continuation](/igorpro/programming/programming.md#line-continuation) is now supported nearly everywhere in both functions and macros, as long as the escaped line ending does not split a simple name over two lines. Compound name components can be on successive lines, though.

    ```igor
    // Compound name components can be on successive lines:
    Macro CallStaticFunction()
        Variable v1= MyModule#functionInMyModule() // usual syntax to call Static Functions
        // demonstrate a compound name with line continuation
        Variable v2 = MyModule \
                    #        \
                    functionInMyModule()
        Print v1,v2
    EndMacro

    // Line continuation can also be applied to a line-ending comment:
    Function [WAVE w] // output wave \
        Example4(String name,       // input: created wave's name \
                Variable length,    // input: # of points \
                Variable avg,       // input: mean value  \
                Variable noise)     // input: gnoise value
        Make/O/N=(length) $name \
                            = avg + gnoise(noise)
        WAVE w= $name
    End
    ```

- A DFREF can now be used with the [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax) in the output list:

    ```igor
    [DFREF dfr] = MRSFunctionReturningDFREF()

    Function [DFREF df] MRSFunctionReturningDFREF()
        DFREF currentDF = GetDataFolderDFR()
        NewDataFolder/O currentDF:subfolder     // create a subfolder
        DFREF df = currentDF:subfolder          // and return a reference to it
    End
    ```

- [WaveHash](/igorpro/commands/wavehash.md) and [Hash](/igorpro/commands/hash.md) now support four SHA3 variants as well as the four xxHash algorithms. The xxHash algorithms are non-cryptographic hash algorithms that are substantially faster than most other supported algorithms and have other desirable behavior. See [xxHash](https://github.com/Cyan4973/xxHash/) for more information on these algorithms.

## Function and Operation Improvements in Igor Pro 10 {#function-and-operation-improvements-in-igor-pro-10}

- [GetFileFolderInfo](/igorpro/commands/getfilefolderinfo.md) now returns Windows-only file version information in S_languageAndCharsetList and S_versionInfo and accepts the /LANG=languageCode /CSET=charSetCode flags.

- [ListToTextWave](/igorpro/commands/listtotextwave.md) operation: if new optional *keySepStr* is specified (and isn't ""), returns 2-column text wave with keys in column 0 and values in column 1 with Column dimension labels of "key" and "value".

- [IgorInfo](/igorpro/commands/igorinfo.md)(0) returns SCALE=1 or 2 and RESOLUTION=*dpi* for each screen. SCALE is the display's magnification value as an integer; it will be 2 when you choose 200% for "Scale and layout" in the Display Settings control panel. *dpi* is the logical screen resolution, aka DPI, typically 96 on Windows.

- [IgorInfo](/igorpro/commands/igorinfo.md)(17) returns the current experiment's startup commands and recreation macros.

- [IgorInfo](/igorpro/commands/igorinfo.md)(18) returns the truth that the existing experiment is closing.

- [FunctionInfo](/igorpro/commands/functioninfo.md)("") now returns information for the running function.

- Added color support in [DoAlert](/igorpro/commands/doalert.md) and [Abort](/igorpro/commands/abort.md) by allowing HTML. For example:

    ```igor
    DoAlert 0, "<p style=\"color:red;\">This is red text.</p><p>Click <a href=\"https://www.wavemetrics.com/\">here to buy Igor</a>.</p>"
    ```

- [Printf](/igorpro/commands/printf.md), [sprintf](/igorpro/commands/sprintf.md), etc. have new %W2P and %W3P options that interpret the precision parameter as the total number of significant digits instead of the number of fractional digits as for %W0P and %W1P.

    - Flag-digits 0 and 1 interpret the precision value in "%.\<precision\>W..." as the number of digits in the **fractional** part of the printed number. Flag-digits 0 and 1 precede Igor 10.

    - Flag-digits 2 and 3 interpret the precision value in "%.\<precision\>W..." as the **total** number of digits used to print the **integer and fractional** parts of the printed number. The printed value is rounded to that number of digits, similar to how %g interprets \<precision\>. Flag-digits 2 and 3 were added for Igor 10.

    - **%W Examples**
        ```igor
        printf "%.2W0PHz", 12.342E6     // prints 12.34MHz
        printf "%.2W1PHz", 12.342E6     // prints 12.34 MHz
        printf "%.0W0Ps", 12.342E-6     // prints 12µs
        printf "%.0W1Ps", 12.342E-9     // prints 12 ns
        printf "%.2W2PHz", 12.342E3     // prints 12KHz
        printf "%.4W3PHz", 12.342E3     // prints 12.34 KHz
        printf "%.2W2PV", -12.342E-3    // prints -12mV
        printf "%.4W3Ps", -12.342E-12   // prints 12.34 ps
        ```

- Added the [Say](/igorpro/commands/say.md) text-to-speech operation.

- [SplitWave](/igorpro/commands/splitwave.md) now accepts /SCL=1 to copy the scaling and dimension labels from the source wave to the destination waves.

- [ImageTransform](/igorpro/commands/imagetransform.md) now supports the use of the /DEST flag so users can specify the output wave for the operation. /FREE is also supported to create free output waves in user functions.

- [ModifyImage](/igorpro/commands/modifyimage.md) includes the *hide* keyword to hide or show an image.

- [Display](/igorpro/commands/display.md), [Edit](/igorpro/commands/edit.md), [NewPanel](/igorpro/commands/newpanel.md), [NewGizmo](/igorpro/commands/newgizmo.md), [NewLayout](/igorpro/commands/newlayout.md), [NewNotebook](/igorpro/commands/newnotebook.md), [NewWaterfall](/igorpro/commands/newwaterfall.md), [NewImage](/igorpro/commands/newimage.md), and [OpenNotebook](/igorpro/commands/opennotebook.md) operations support a new /K=4 option which kills those windows with no dialog and is not saved with the experiment.

- [NewImage](/igorpro/commands/newimage.md) and [AppendImage](/igorpro/commands/appendimage.md) support 10 new packing modes for direct color images via the /PACK flag.

- [SpecialDirPath](/igorpro/commands/specialdirpath.md) can return the location of the folder containing crash minidumps and other diagnostics by using the new "Igor Diagnostics" *dirIDStr* string.

- [SoundLoadWave](/igorpro/commands/soundloadwave.md) can load more kinds of audio files, including μ-law, A-Law, AIFF and AIFC, WAVE, .mp3 and .mpeg4.

- [PlaySound](/igorpro/commands/playsound.md) plays unsigned 8-bit sound waves properly.

- [ImageLoad](/igorpro/commands/imageload.md) is now capable of loading TIFF files that use JPEG compression. This requires that the LibTIFF library be used to load the file. See the ImageLoad documentation for the /BIGT flag and the ***Loading TIFF Files*** section for more information.

- [PauseForUser](/igorpro/commands/pauseforuser.md) has improved error messages for cases in which the names of the main or target windows are incorrect. They now tell you which window is incorrect or missing.

- [TraceInfo](/igorpro/commands/traceinfo.md) now returns the full path of a trace's contour Z wave as the value of the CONTOURZWAVE keyword. This path is empty if the trace is not associated with a contour plot.

## Data Browser Improvements in Igor Pro 10 {#data-browser-improvements-in-igor-pro-10}

- When browsing an experiment, it is now possible to add the Points and Dimensionality columns to the object list. It is also possible to sort by these fields even if they are not displayed in the object list.

- Resizing columns by dragging the divider in the object list now gives better results.

## Window Browser Improvements in Igor Pro 10 {#window-browser-improvements-in-igor-pro-10}

- The Window Browser now shows a window's unnamed and named window hooks and tooltip hooks, if any of those are set.

## Dialog Improvements in Igor Pro 10 {#dialog-improvements-in-igor-pro-10}

- Added graph style macro support to the Append Traces and Append Category Traces dialogs (before Igor 10 only the Display and New Category Plot dialogs had graph style macro support.)

- Added separate memories of user's selection of style macro that persist between Igor invocations. This allows a user to set up their preferred Display style macros and their preferred Append style macros only once and use them always.

- If the selected style macro (which normally has no parameters) **does** have two or more parameters, then **the graph name and number of already-existing traces in that graph are passed in**, and any remaining parameters are not filled in (which might invoke a [Missing Parameter Dialog](/igorpro/user-interface/dialog-help.md#missing-parameter-dialog)).

- Reorder Images dialog (Image🠖Reorder Images) now supports multiple image layers. See [ReorderImages](/igorpro/commands/reorderimages.md).

## Graphing Improvements in Igor Pro 10 {#graphing-improvements-in-igor-pro-10}

- Added a second layer for displaying image plots. The new layer displays an image above traces and axes. See [Creating an Image Plot](/igorpro/graphing/image-plots.md#creating-an-image-plot), [AppendImage](/igorpro/commands/appendimage.md), [NewImage](/igorpro/commands/newimage.md), [ReorderImages](/igorpro/commands/reorderimages.md), [ImageInfo](/igorpro/commands/imageinfo.md).

- Added support for 10 new image color packing modes in [NewImage](/igorpro/commands/newimage.md), [AppendImage](/igorpro/commands/appendimage.md) and [ModifyImage](/igorpro/commands/modifyimage.md) operations.

- Added two color tables: RedYellowGreen (256 colors) and RedYellowGreen10 (10 colors).

- Improved marker standoff ([ModifyGraph](/igorpro/commands/modifygraph.md) mstandoff) for text markers. Previously, the standoff was computed for whatever non-text marker happened to be specified. Now standoff is computed from the text bounding box.

- Marker standoff now takes marker stroke thickness into account. Previously, a large value of marker stroke thickness
([ModifyGraph](/igorpro/commands/modifygraph.md) mrkThick) would eat into the space reserved for marker standoff. This can cause small changes in the appearance of existing graphs.

- Marker standoff can now be applied on a point-by-point basis (see [Customize at Point](/igorpro/graphing/graphs.md#customize-at-point)).

- Graph preferences useComma, useDotForX, and useLongMinus can now be captured in the Capture Prefs dialog for graph windows.

- [RemoveContour](/igorpro/commands/removecontour.md) has a new /Z (ignore errors) flag.

## Box and Violin Plot Improvements in Igor Pro 10 {#box-and-violin-plot-improvements-in-igor-pro-10}

- [Box Plots and Violin Plots](/igorpro/graphing/graphs.md#box-plots-and-violin-plots) can now be plotted on a log Y axis.

## Table Improvements in Igor Pro 10 {#table-improvements-in-igor-pro-10}

- The table contextual menu now has Cut, Copy, Paste, Insert Paste, and Clear menu items. Right-click in a table to use them.

## Page Layout Improvements in Igor Pro 10 {#page-layout-improvements-in-igor-pro-10}

- Added new layout-only margin guides ML, MT, MR, and MB (Margin Left, Margin Top, Margin Right, and Margin Bottom). These guides are more useful than the frame guides which are outside of the page's printable area. Margin guides adjust to the margins set in the Page Size dialog.

- Dragging a guide in a page layout indicates its position in the status readout at the bottom of the window.

  Fractions of the printable page width or height are also displayed. Holding the Shift key down constrains dragged guides to some rational fraction of the printable page width or height (see [Guides Mode for Laying Out Subwindows](/igorpro/graphing/making-figures/subwindows.md#guides-mode-for-laying-out-subwindows)).

- Using the scroll wheel while holding down the Ctrl key changes the magnification level of the layout.

- Holding down the Shift key while using the arrow keys to move a layout object accelerates the movement by a factor of ten.

## Notebook Improvements in Igor Pro 10 {#notebook-improvements-in-igor-pro-10}

- Using the scroll wheel while holding down the Ctrl key changes the magnification level of the notebook.

- Special characters for `Note`, `Warning`, and `Caution` symbols can now be used in formatted notebooks. Use the Notebook🠖Special menu item or the `Insert` popup in the ruler toolbar.

## Help Improvements in Igor Pro 10 {#help-improvements-in-igor-pro-10}

- Using the scroll wheel while holding down the Ctrl key changes the magnification level of the help document.

- Starting with Igor Pro 9, Igor sometimes left help files for XOPs open after startup. This was of little consequence, but meant that there was an extra help window open and an extra entry in the Help🠖Help Windows list. This has been fixed for Igor Pro 10. Note that if you intentionally open an XOP's help file, the window will stay open as you expect.

- The list of help topics in the Topics list of the Help Browser's "Help Topics" tab is now properly ordered when "Sort topics" is unchecked. This was broken since Igor Pro 7.

## Graphics Export Improvements in Igor Pro 10 {#graphics-export-improvements-in-igor-pro-10}

- Error bars are now exported to SVG correctly. Previously, the clipping of error bars when exporting to SVG format was incorrect. Error bars and error boxes that should have been outside the plot area were drawn in the resulting SVG image. Clipping is now correctly handled during SVG export and error bars that are outside of the plot area in Igor Pro will not appear in an exported SVG image. Error shading also exports correctly to SVG and was never an issue.

:::note
Error ellipses will still not properly clip when exporting to SVG. Please zoom the plot area in or out to achieve the necessary result. 
:::


## Procedure Window Improvements in Igor Pro 10 {#procedure-window-improvements-in-igor-pro-10}

#### Code Folding {#code-folding}
Procedure windows now support code folding. Clicking the code folding arrows in the left margin toggles whether a code block is hidden or visible. Hovering the mouse over the ellipsis indicator to the right of a folded code block temporarily reveals the hidden code:

<img src="MD_images/Whats_New_In_Igor_Pro_10/codeFolding_hoverIndicator.png" alt="Code Folding Hover Margin" width="40%"/>

There is a right-click menu item that allows users to fold/unfold multiple code blocks at once. Code folding can be turned on and off in Misc🠖Miscellaneous Settings under the Text Editing section.

#### Statement Completion {#statement-completion}
Completion suggestions are now offered for operation keywords and special functions (i.e. MatrixOP and APMath). General improvements to code completion in various contexts have been made.

#### Syntax Highlighting {#syntax-highlighting}
Operation keywords now have syntax highlighting, which is configurable in Misc🠖Miscellaneous Settings under the Text Editing section.

#### Go to User Function {#go-to-user-function}
Clicking on a user-defined function while holding down the Ctrl key will navigate to the top of the function definition. 

#### Scroll Magnification {#scroll-magnification}
Using the scroll wheel while holding down the Ctrl key changes the magnification level of the procedure window.

#### Persistent Function Hints {#persistent-function-hints}
Function hints that appear in the status bar at the bottom of the procedure window no longer disappear while typing out the arguments of a function or operation call. 

#### External Editors {#external-editors}
A new Tools icon in the procedure window status bar makes it easy to open the file associated with the procedure file in an external text editor. This only works for procedure windows that represent stand-alone files.

## Gizmo Improvements in Igor Pro 10 {#gizmo-improvements-in-igor-pro-10}

- Rotating and panning a Gizmo scene with the mouse now supports holding down the Shift key to fix the axis of rotation/pan. Holding Control temporarily switches between rotation and pan mode. 

- 3D scatter plots now support 'projection' of the 3D data onto one or more 2D planes, which are controlled in the Gizmo scatter plot dialog. This feature adds the projection, projectRGBA, and projectMarkerSize properties to the ModifyGizmo operation.

- Marker quality in 3D scatter plots can now be directly customized by the user using the quadricFacets property in the ModifyGizmo operation. The number of facets used for drawing the markers is accessed through the Gizmo scatter plot dialog in the 'Shape and Size' tab.

- Gizmo box object now supports a color property (faceColor) for each face of the cube.

- Improved drawing of annotations in Gizmos on displays with Windows Display Settings scale factor of non-integer multiples of 100%.

## Drawing Improvements in Igor Pro 10 {#drawing-improvements-in-igor-pro-10}

- The [DrawArc](/igorpro/commands/drawarc.md) command has a new /ORIG flag which completes the arc by drawing lines to the origin. (If the arc has arrows, they still point to the first or last point of the arc's curve, not to the origin.)

- Graphs have two new drawing layers that draw above (in front of) annotations. The two layers are ProgTop and UserTop. See [Drawing Layers](/igorpro/graphing/drawing.md#drawing-layers).

- The various drawing commands, [DrawLine](/igorpro/commands/drawline.md), [DrawRect](/igorpro/commands/drawrect.md), etc. will not create draw objects with coordinates that are Inf or NaN. Previously that wasn't checked, and a copy of such an object caused a crash.

- Editing [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md) objects displays editing hints on where to click and modifier keys to hold down for anchor or control point constraints and shape completion.

- It is easier to drag a [DrawBezier](/igorpro/commands/drawbezier.md) object's control handle independent of the corresponding control handle by holding down the Alt key when clicking or dragging the control handle. In this mode the mouse cursor now changes to a distinctive "convert control point" cursor.

- It is easier to "close" (join the ends) of [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md) objects; the mouse cursor now changes to a "close" cursor which has a small circle added to the crosshair cursor.

- Added more contextual menus for editing [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md) objects, including new "Complete Polygon" and "Complete Bezier" items. In edit mode you can right-click an anchor, control point, or segment to display these contextual menus.

- [DrawAction](/igorpro/commands/drawaction.md) with the *commands* keyword now initializes the *S_recreation* string to an empty string instead of a null string when there are no drawing objects. It also sets *V_flag* to the number of drawing objects in the list in *S_recreation*.

- The recreation macros for [DrawPoly](/igorpro/commands/drawpoly.md) and [DrawBezier](/igorpro/commands/drawbezier.md) objects now start a new line when a NaN coordinate is encountered. This makes it easier to identify segments of a polygon or Bezier.

- For the same reason [DrawBezier](/igorpro/commands/drawbezier.md) object recreation macros put the initial segment's 4 xy points (starting anchor, control point 1, control point 2, ending anchor for the first segment and starting anchor for the next segment) on the first line, and each following segment's 3 xy points (control point 1, control point 2, ending anchor) on successive lines.

## Annotation Improvements in Igor Pro 10 {#annotation-improvements-in-igor-pro-10}

- Added additional error checking during parsing of [Annotation Text Escape Codes](/igorpro/graphing/annotations.md#annotation-text-escape-codes) in annotations, labels, and controls.

## Control and Control Panel Improvements in Igor Pro 10 {#control-and-control-panel-improvements-in-igor-pro-10}

- Control recreation macros use integers instead of coordinate.00 whenever possible; non-integer coordinates still use %.2f format.

- It is now possible to lay out controls in a control panel using guide lines. For information on using guides with controls, see [Laying Out Controls in Guides Mode](/igorpro/user-interface/controls.md#laying-out-controls-in-guides-mode). Previously, we called these guide lines "subwindow guides" 
but since we have expanded the scope of these guide lines, we now call them "guides". Each control has six anchors that can be attached to guides.
Those anchors are Left, Horizontal Center, Right, Top, Vertical Center, and Bottom. Attaching one anchor will cause a control to move, following the guide to which it is attached.
Attaching two anchors will cause a control to resize, if that is allowed.

- The drawing tool palette has a new button for "Guides Mode" which allows you to edit guides and use the guides to control subwindow and control layouts. For basic information on guides, Guides Mode, and subwindows, see [Subwindow User-Interface Concepts](/igorpro/graphing/making-figures/subwindows.md#subwindow-user-interface-concepts).

- For information on using guides with subwindows, see [Guides Mode for Laying Out Subwindows](/igorpro/graphing/making-figures/subwindows.md#guides-mode-for-laying-out-subwindows). That help topic existed previously, with the name "Subwindow Layout Mode and Guides". Along with a change in the topic title, we have substantially rewritten the section for clarity and to reflect the new features.

- Using guides to lay out controls makes it much easier to create control panels in which the controls move and resize in useful ways. For instance, it is very easy to create a [ListBox](/igorpro/user-interface/controls.md#listbox) control that occupies a constant fraction of a control panel window as the window is resized.

- Dragging a guide while holding the Shift key down constrains dragged guides to the nearest rational fraction of the panel width or height. The fraction chosen is indicated by an overlaid graphic.

- It is now possible to create and edit guides without requiring the creation of an active subwindow. This is necessary to allow editing guides for controls.

- To support attachment of controls to guides, the various control operations now have a "guides" keyword to 
specify the attachment of anchors on the controls to the guides. See, for instance, [Button](/igorpro/commands/button.md).

- Checkboxes and disclosure controls in [ListBox](/igorpro/user-interface/controls.md#listbox) control cells now respond correctly to control panel expansion.

- Fixed a bug that existed in Igor Pro 9: A ListBox control with disabled cells do not respond to mouse clicks, and therefor are not selectable via a mouse click. However, if you dragged the mouse across a disabled cell, it could be selected. That loophole has now been closed.


## Analysis Improvements in Igor Pro 10 {#analysis-improvements-in-igor-pro-10}

- It is now possible to use static functions for the derivative function with the [IntegrateODE](/igorpro/commands/integrateode.md) operation. It requires 
that the procedure window has a `ModuleName` specification, and you must name the function
using the full `ModuleName#FunctionName`. See [Procedure Modules](/igorpro/advanced-topics.md#procedure-modules).

- Changed [binomial](/igorpro/commands/binomial.md)(n,k) to return 0 when k>n.

- Added [Interp4D](/igorpro/commands/interp4d.md) and [Interp4DPath](/igorpro/commands/interp4dpath.md) functions.

## Statistics Improvements in Igor Pro 10 {#statistics-improvements-in-igor-pro-10}
- Added to [WaveStats](/igorpro/commands/wavestats.md) optional parameters for the /W flag that support complete bypass of the creation and initialization of the various V_ variables.

## Matrix Improvements in Igor Pro 10 {#matrix-improvements-in-igor-pro-10}

- Added to [MatrixOP](/igorpro/commands/matrixop.md) the following functions: subtractMin(), indexMatch(), removeCol(), removeCols(), scaleLayers(), scaleChunks(), subtractRows(), subtractCols(), quatFromSpherical(), quatInverse(), median(), zapZeros(), replaceInfs(), enoise(), setType(), rowDiff(),
binMean(), binVar(), limit(), not().

- Changed MatrixOP integer conversion functions: uint8(), int8(), uint16(), int16(), uint32() and int32() to return 0 for NaN input and return the largest/smallest value for +-INF.

- MatrixOP compile is now testing for errors previously reported only at runtime.

## Multipeak Fitting Improvements in Igor Pro 10 {#multipeak-fitting-improvements-in-igor-pro-10}
Thanks to the hard work and generosity of Igor power user Stephan Thürmer (AKA "chozo" in the Igor Forums), the Multipeak Fitting package continues to be updated and improved.

- Increased robustness in many areas by improved error handling, especially in regards to out-of-bounds data, empty waves, and NaNs.

- Added support for hold-strings waves.

- 100% and 200% display scaling now both supported.

- Copy/paste shortcuts now work directly in the table UI.

- Auto-locate no longer returns any zero-width peaks.

- Multiple alert and error message improvements.

## Image Processing Improvements in Igor Pro 10 {#image-processing-improvements-in-igor-pro-10}

- Fixed [ImageSeedFill](/igorpro/commands/imageseedfill.md) which ignored ROI wave when working on 2D source image.

- Changed [ImageLoad](/igorpro/commands/imageload.md) with the /LTMD flag so that the tag text wave consists of single tags per row starting with the formal name of the tag.  To the extent possible the tags are now listed in increasing order.

## Data Import And Export Improvements in Igor Pro 10 {#data-import-and-export-improvements-in-igor-pro-10}

- [HDF5SaveData](/igorpro/commands/hdf5savedata.md) Now supports /TRAN=2 and /TRAN=3 for better control over transposing of multi-dimensional data. In particular, /TRAN=3 uses automatic multithreading to accelerate execution.

- The HDF5 library was updated to 1.14.6. Also new are the BLOSC2 and ZSTD dynamic filter plugins, see [HDF5 Dynamically Loaded Filters](/igorpro/data/igor-hdf5-guide.md#hdf5-dynamically-loaded-filters).

- [XLLoadWave](/igorpro/commands/xlloadwave.md) now loads non-ASCII worksheet names from Excel files that use the Excel 97-2003 file format (BIFF8).

## Miscellaneous Improvements in Igor Pro 10 {#miscellaneous-improvements-in-igor-pro-10}

- Added new [graphemeLength](/igorpro/commands/graphemelength.md) and [UTF8CharLength](/igorpro/commands/utf8charlength.md) functions to aid in parsing and manipulating Strings containing UTF-8 text. See also [Characters Versus Bytes](/igorpro/igor-basics/text-encodings.md#characters-versus-bytes).

## New And Improved Packages in Igor Pro 10 {#new-and-improved-packages-in-igor-pro-10}

#### Heat Map and Dendrogram package {#heat-map-and-dendrogram-package}

- Dendrogram plots can now be created in a subwindow.

- Accessor functions have been added to help programmers who want to use the dendrogram plots from their own code. This includes a setting that preserves the dendrogram structures so that a new dendrogram can be made reusing those structures.

## New And Improved Example Experiments in Igor Pro 10 {#new-and-improved-example-experiments-in-igor-pro-10}

### Modified Example Experiments in Igor Pro 10 {#modified-example-experiments-in-igor-pro-10}
- File🠖Example Experiments🠖Analysis🠖Spherical Triangulation Demo<br>[SphericalTriangulationDemo.pxp](#igor-pxp/Examples/Analysis/SphericalTriangulationDemo.pxp)

### New Example Experiments in Igor Pro 10 {#new-example-experiments-in-igor-pro-10}
- File🠖Example Experiments🠖Tutorials🠖Wave Scaling Tutorial<br>
 [Wave Scaling Tutorial.pxp](<IgorPXP:Learning Aids:Tutorials:Wave Scaling Tutorial.pxp>)

- File🠖Example Experiments🠖Python🠖Machine Learning  demonstrates a simple machine learning task using the TensorFlow Python library<br>
[MachineLearningDemo.pxp](#igor-pxp/Examples/Python/MachineLearningDemo.pxp)