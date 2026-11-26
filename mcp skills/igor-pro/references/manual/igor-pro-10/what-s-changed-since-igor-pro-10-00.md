---
description: "This file describes significant changes made to Igor Pro and supporting files since the initial release of Igor Pro 10.00."
slug: /igor-pro-10/what-s-changed-since-igor-pro-10-00
---

# What's Changed Since Igor Pro 10.00? {#what-s-changed-since-igor-pro-10-00}

This file describes significant changes made to Igor Pro and supporting files since the initial release of Igor Pro 10.00. If WaveMetrics has told you that an issue you reported has been resolved for the next version, it will be included even if it is not listed below. Here are the updates in reverse chronological order:

- xxxx: [Update 10.06](#update-10-06)
- November 14, 2026: [Update 10.05](#update-10-05)
- November 3, 2026: [Update 10.04](#update-10-04)
- June 16, 2026: [Update 10.03](#update-10-03)
- May 13, 2026: [Update 10.02](#update-10-02)
- April 29, 2026: [Update 10.01](#update-10-01)
- April 22, 2026: [Update 10.01B01](#update-10-01b01)
- October 15, 2025: Release 10.00. See [What's New in Igor Pro 10?](/igorpro/igor-pro-10/what-s-new-in-igor-pro-10.md) for changes since Igor Pro 9.

## Update 10.06 {#update-10-06}

### Igor Application {#igor-application}

#### New Features {#new-features}

#### Bug Fixes {#bug-fixes}

- Fixed crash in [SoundLoadWave](/igorpro/commands/soundloadwave.md) when loading to an existing wave without specifying the /O overwrite flag.


## Update 10.05 {#update-10-05}

### Igor Application {#update-10-05-igor-application}

#### New Features {#update-10-05-new-features}

- You can now use AI agents to work in Igor for you. Ask an agent in an AI app such as Visual Studio Code, Claude Code, Cursor, or Codex to write and debug Igor procedures, load and analyze data, make and refine graphs, or explain how an Igor operation works. The agent does the work in your running copy of Igor and checks the results itself, by reading compile errors and command output and by looking at images of your graphs. This works through the new `Igor Pro MCP Server`, which uses the Model Context Protocol (MCP). MCP is an open standard that lets large language models (LLMs) such as GPT, Claude, and Gemini communicate with and take action in an external application such as Igor Pro. For more information about MCP, see [https://modelcontextprotocol.io/](https://modelcontextprotocol.io/).

  The Igor Pro MCP Server provides tools that AI agents use to work in Igor and get feedback. For example, AI agents can:

  - Open and compile procedure files, receiving compile errors as feedback
  - Execute Igor commands and call built-in and user-defined functions
  - Look up the documentation for built-in operations and functions at [https://docs.wavemetrics.com/igorpro/commands](https://docs.wavemetrics.com/igorpro/commands)
  - Capture images of Igor windows for visual feedback
  - Inspect the state of Igor and get information about the current experiment
  - Launch and quit Igor

  The Igor Pro 10.05 installer includes the server installer. To install the server for your Windows user account, choose `Help🠖AI Tools🠖Install/Repair Igor Pro MCP Server` or click the AI apps button in the status bar. When Igor checks for updates, it also checks for server updates. Use the `Help🠖AI Tools` submenu to choose whether AI apps can connect to Igor now or whenever Igor starts. To set up your AI app to use the server, see [https://docs.wavemetrics.com/igorpro/mcp-server](https://docs.wavemetrics.com/igorpro/mcp-server).

- The Python console's `igorpro.fn` completion now shows Igor function names.

#### Bug Fixes {#update-10-05-bug-fixes}

- Fixed range-based loops so they use the iterated wave's current data, type, and point count on each iteration. Changes to a wave made in the loop body, including resizing, retyping, or killing it, are now handled correctly.

- Fixed a bug where pressing the Down Arrow key in the Python console could clear the current entry, including a partially entered multiline statement.

- Fixed rendering artifacts in dense line graphs that use miter or bevel joins.

- Fixed display-scaling drift caused by truncation when scaling and restoring window coordinates.

- Fixed crashes when operations such as [FuncFit](/igorpro/commands/funcfit.md), [FindRoots](/igorpro/commands/findroots.md), [Optimize](/igorpro/commands/optimize.md), [Integrate1D](/igorpro/commands/integrate1d.md), [IntegrateODE](/igorpro/commands/integrateode.md), or [StatsKSTest](/igorpro/commands/statskstest.md) called user functions that had been scanned but not compiled. These operations now report that the procedure must be compiled. Also fixed a crash when [StatsResample](/igorpro/commands/statsresample.md) /JCKN was run from the command line. 

- Fixed a problem introduced in Igor Pro 10.04 that caused some procedures using [ErrorBars](/igorpro/commands/errorbars.md) with the `nochange` keyword to no longer compile.

- Fixed a potential buffer overflow in the Error Bars dialog

## Update 10.04 {#update-10-04}

### Igor Application {#update-10-04-igor-application}

#### New Features {#update-10-04-new-features}

- Added a Simplified Chinese language translation of the user interface (menus, dialogs, etc. but not documentation). As with the German translation added in Igor Pro 10.01, we used AI for the translation so there may be mistakes. Open the Miscellaneous Settings dialog (Misc🠖Miscellaneous Settings menu item) and select the Environment category to select a language. If your OS language is Simplified Chinese, Igor asks you if you want to use the Simplified Chinese translation when it starts. Igor will remember your selection.

- [? :](/igorpro/programming/operators/operator-reference.md#conditional) works with string values, not just numeric values:
  ```igor
  String str = (num > 0) ? "something" : "nothing"
  ```

- Performance when displaying large images has been significantly improved, especially when logarithmic color scaling is enabled, resulting in much more responsive window resizing. Actual performance gains will vary depending on your hardware and image size. See the following benchmark comparison for drawing a large, 14000 x 4000 point image:

  <img src="MD_images/Whats_Changed_Since_Igor_Pro_10/ImageDrawBenchmark.png" alt="Image Drawing Benchmark" width="75%"/>

- An improved algorithm for drawing line graphs is presented as an experimental feature, which can be enabled or disabled by choosing Misc🠖Experimental Features. Enabling it produces significantly faster drawing of simple line graphs than the legacy renderer with much higher quality output, especially when using transparency, thicker lines widths, or data with lots of noise. See the following benchmark comparison for graph updates with a 1000 point sine wave and a 1000 point wave of pure noise:

  <img src="MD_images/Whats_Changed_Since_Igor_Pro_10/GraphDrawBenchmark.png" alt="Graph Drawing Benchmark" width="75%"/>

- Improved performance of loops (`for`, `while`, and `do-while`) and wave assignment statements in user functions by reducing the overhead of checking for user aborts. A simple wave assignment statement that does very little work per point now runs about 40% faster.

- Python 3.15 is now supported.

- The debugger can now display information about the selected wave, such as its type, dimensions, scaling, units, size, modification date, and wave note, similar to the information shown in the Data Browser. Choose Show Wave Info from the same popup menu that offers Show Waves in Table and Show Waves in Graph.

- You can now rename a trace by right-clicking it in a graph and choosing Rename *traceName*... from the contextual menu.

- The Abort button in the status bar is now shown and can be clicked during [PauseForUser](/igorpro/commands/pauseforuser.md), so you can abort a procedure that is waiting for the user.

- Added /D flag to [PolygonOp](/igorpro/commands/polygonop.md) to create double precision output waves.

- Improved performance for statement completion and help templates.

- `igorpro.wave.createfrom` and `igorpro.wave.set_data` now accept collections of `igorpro.wave` or `igorpro.folder` objects, which lets you create and set the contents of wave reference waves and data folder reference waves from Python. For example:

  ```python
  # Create a wave reference wave from a list of Igor waves
  sourceWaves = [igorpro.wave.create(f'source{x}') for x in range(3)]
  waveRefs = igorpro.wave.createfrom('waveRefs', sourceWaves)
  ```

- The `set_scale` method of the `igorpro.wave` Python class can now copy the scaling, units, and full scale from another wave. For example:

  ```python
  w.set_scale(otherWave, 'delta')
  ```

- Added a `set_note` method to the `igorpro.wave` Python class to set or append to a wave's note.

- Procedure files can now add items to the Python menu using `Menu "Python"`, and [HideIgorMenus](/igorpro/commands/hideigormenus.md), [ShowIgorMenus](/igorpro/commands/showigormenus.md), and [SetIgorMenuMode](/igorpro/commands/setigormenumode.md) now work with the Python menu.

- Tab labels now respect escape characters and render correctly for multi-line labels.

#### Changed Behavior {#changed-behavior}

- When a trace's marker can't be drawn, Igor now draws a ? in its place instead of drawing nothing. This happens when the marker number is invalid or when a custom marker's `SetWindow markerHook` function is missing, uncompiled, or does not draw the marker. Previously a markers-only trace with such a marker silently disappeared.

- [Histogram](/igorpro/commands/histogram.md) no longer reports an error when the bin width specified with /B={binStart, binWidth, numBins} is zero. Instead it uses a bin width of 1 with the bins centered on binStart. This also fixes problems in the image histogram, contrast, and range dialogs for images in which every pixel has the same value.

- [CurveFit](/igorpro/commands/curvefit.md) now reports an error when the /CMAG, /XW, /XHLD, /XD, or /XR flags are used without the /ODR setting they require (nonzero /ODR for /CMAG, /ODR=2 or 3 for the others) when the command is executed from the command line or via [Execute](/igorpro/commands/execute.md). Compiled code already reported this error.

- [PythonFile](/igorpro/commands/pythonfile.md) no longer reports an error when the Python script calls `sys.exit()` with no argument or with an exit code of 0. A non-zero exit code or a string argument is reported as an error.

- The Python function `os.abort()` now raises an exception instead of terminating Igor.

- When Python fails to initialize, Igor now reports the specific error right away instead of waiting for a timeout and reporting a generic error.

- [PauseForUser](/igorpro/commands/pauseforuser.md) now honors the idle period set by [SetIdlePeriod](/igorpro/commands/setidleperiod.md) while waiting for the user.

- When you click the button to install a license for all users in the license dialog, the values you already entered are now transferred to the new instance of Igor so you don't need to enter them again.

#### Bug Fixes {#update-10-04-bug-fixes}

- Fixed a bug that could prevent saving an experiment containing a formatted notebook after Igor had been open for a long time. This happened when Windows Storage Sense or the user deleted the temporary file that Igor uses for the notebook.

- Fixed several crashes that could occur when procedure files are reloaded from disk after being modified by another program, including when a reload happened during a compile or when a command was sent via an XOP or ActiveX Automation during a compile.

- Fixed a crash that could occur when a queued control action procedure for a ListBox or SetVariable control ran after the control's wave was killed or recreated, for example when killing a panel.

- Fixed a crash (introduced in 10.03) when [Grep](/igorpro/commands/grep.md) was used with a text wave in a preemptive thread.

- Fixed a crash when the [Dir](/igorpro/commands/dir.md) operation was used with a string expression in a user function.

- Fixed a crash when drawing a [ColorScale](/igorpro/commands/colorscale.md) for an image using XY subset color autoscaling (`ModifyImage ctabAutoscale=1`) when the image was scrolled entirely off the plot area.

- Fixed a crash when [ReorderTraces](/igorpro/commands/reordertraces.md) /R was used with a graph created with [Display](/igorpro/commands/display.md) /VERT.

- Fixed a crash (introduced in Igor Pro 10) in [ImageHistModification](/igorpro/commands/imagehistmodification.md) when used with a 3D unsigned byte wave.

- Fixed a crash when aborting Python code that was run from Igor.

- Fixed a bug in [ImageInterpolate](/igorpro/commands/imageinterpolate.md) when using the *Affine2D* keyword with a 3D wave that could cause a crash or incorrect results.

- Fixed a bug in [Interp4DPath](/igorpro/commands/interp4dpath.md) that could cause incorrect results or a crash when a path point fell outside the range of the source wave.

- Fixed a potential crash in [Project](/igorpro/commands/project.md) when more than 10 values were passed to the /P flag. Igor now reports an error instead.

- Fixed a crash when clicking a resize handle of a selected control or draw object after a previous click on a control or draw object in a window that was since closed.

- Fixed a bug (introduced in Igor Pro 10) that caused image plots on log axes to be drawn, autoscaled, and tagged incorrectly when an edge of the image fell at zero or a negative value.

- [area](/igorpro/commands/area.md) and [faverage](/igorpro/commands/faverage.md) now support 64-bit integer waves. Previously they returned NaN. Sums of 64-bit integer values are also now computed without losing precision.

- Fixed a bug in [WaveStats](/igorpro/commands/wavestats.md) that could give incorrect minimum or maximum values, or locations, for complex integer waves when multithreading was used.

- Fixed a rounding error in [ImageInterpolate](/igorpro/commands/imageinterpolate.md) when using the *Affine2D* keyword that was causing output wave dimensions to be off-by-one.

- Fixed a bug in [ImageEdgeDetection](/igorpro/commands/imageedgedetection.md) that produced incorrect results when using the Prewitt method.

- Fixed a bug where [HDF5LoadImage](/igorpro/commands/hdf5loadimage.md) converted only the first image of an image stack to RGB.

- Fixed a bug where [Grep](/igorpro/commands/grep.md) with /LIST but no separator, used in a user function, returned a list with no separators instead of using the default semicolon separator.

- Fixed a bug (introduced in 10.02) that caused procedures to auto-compile when a procedure file was opened.

- Fixed a bug that caused procedures to be compiled a second time after clicking the Compile button.

- Fixed a spurious compile error ("P or X used outside of a wave assignment loop") for a multidimensional wave assignment to a single element that uses p, q, r, or s on the right side, such as `w[0][0] = w[p+1][q+1]`.

- Fixed a spurious compile error involving [ErrorBars](/igorpro/commands/errorbars.md) with the BOX keyword followed by `nochange`, for example `ErrorBars data, BOX, nochange, nochange`.

- Fixed a bug in the debugger's expression evaluation where a dimension label (as in `wave[%label]`) was replaced with the value of a local variable of the same name.

- Fixed a bug where drawing a graph that uses a custom marker hook function could change debugger settings, silently disabling NVAR SVAR WAVE checking.

- Fixed several problems that occurred when modifying a graph, for example changing a trace's color, while a trace was being edited with [GraphWaveEdit](/igorpro/commands/graphwaveedit.md). Previously this could partially exit edit mode, and the modifications could be lost when exiting edit mode or using undo or redo, or omitted from window recreation macros.

- Fixed several problems with [PauseForUser](/igorpro/commands/pauseforuser.md): spurious "UpdtDisplay: recursion attempted" messages, a hang when quitting Igor, redraw problems, and the ability to activate windows other than the one(s) the user is supposed to interact with.

- Fixed a bug in [LoadPICT](/igorpro/commands/loadpict.md) that prevented loading SVG files that don't start with an XML declaration (`<?xml ...?>`). SVG files downloaded from some web services omit the declaration.

- Fixed [SoundLoadWave](/igorpro/commands/soundloadwave.md) so that a /S start time of 0 is accepted and /Q suppresses the error dialog for bad /S times. Negative /S times now consistently report an error.

- [Secs2Date](/igorpro/commands/secs2date.md) now honors an empty separator string when the format is -2.

- Fixed a bug in the Curve Fitting dialog that could report a spurious error about the number of coefficients after choosing a fit function with a different number of coefficients.

- Fixed a bug where selected draw text in a graph or page layout was not aligned with the text it highlights on high-DPI displays.

- Pressing Ctrl+C in the Python console now interrupts running Python code.

- Fixed a bug in [PythonFile](/igorpro/commands/pythonfile.md) where adjacent quoted arguments in the args parameter were merged into a single argument.

- Fixed a bug where [PythonFile](/igorpro/commands/pythonfile.md) could fail to find a Python file after an earlier Python command failed while retrieving return values.

- Fixed a memory leak each time Python code raised an exception.

- Fixed bugs in the [Notebook](/igorpro/commands/notebook.md) operation where out-of-range values wrapped around to incorrect values instead of being clipped. This affected the pageMargins, margins, and startPage keywords and, in user functions, color components above 65535. Also, in user functions, an explicit alpha of 0 in a Notebook color is now honored instead of being treated as opaque, matching the behavior on the command line.

- When `\s()` in an annotation refers to a graph or trace that does not exist, the ? placeholder is now centered within the annotation instead of extending above it.

- Fixed a bug in Gizmo color scaling where values above the top of the color range were drawn using the color for values below the range.

- Fixed a bug in Gizmo scatter objects that caused drop lines in the Y direction to be drawn to the wrong location.

- Fixed [AppendToGizmo](/igorpro/commands/appendtogizmo.md) /D so that it adds attributes to the display list. Also, AppendToGizmo /N with a nonexistent Gizmo window now reports "Expected Gizmo window."

- Fixed a bug in [ModifyGizmo](/igorpro/commands/modifygizmo.md) in user functions where outputResFactor was applied as userLevel.

- Fixed a bug in Gizmo where the back face shininess value of the shininess attribute was ignored and the front face value was used for both faces.

- Gizmo pie wedge objects now draw correctly when the end angle is less than the start angle, and draw nothing when the start and end angles are equal.

- Fixed the enable state of the cloud color checkbox and popup menu in the Gizmo isosurface dialog.

### Procedures {#procedures}

- The Global Fit package (Analysis🠖Global Fit) now supports fitting with errors in the independent variable (X) as well as the dependent variable (Y), using the same [Errors in Variables: Orthogonal Distance Regression](/igorpro/analysis/curve-fitting.md#errors-in-variables-orthogonal-distance-regression) machinery available in the Curve Fitting dialog. Assign an X Weight wave for a data set on the Data Weighting sub-panel to enable it. This release also includes several accompanying bug fixes: sub-panels are now reliably closed along with the main panel, and a missing weight or mask wave now aborts the fit with a clear error instead of proceeding silently.

- PeakFunctions2.ipf - Fixed several bugs affecting the reported ± uncertainty of peak coefficients and derived values in Multipeak Fitting and Curve Fitting (the fitted values themselves were not affected): the ExpConvExp peak's Location uncertainty omitted the contribution from the peak's own position parameter, and had a sign error in its degenerate-width branch; the Doniach-Sunjic peak's Location uncertainty applied a sign factor to the wrong pair of cross terms; the GaussConvExp (EMG) and LorentzianHeight peaks' Area uncertainty was scaled using the peak amplitude instead of the peak area; the LogNormal peak's Area and FWHM uncertainties erroneously squared the covariance terms, inflating them; the Voigt and VoigtArea peaks' FWHM uncertainty forced a covariance term to be positive instead of preserving its true sign; and the Voigt and VoigtArea peaks' Amplitude uncertainty omitted a sign factor for the GaussFWHM and LorentzFWHM parameters, which the amplitude formula uses only via absolute value, producing an incorrectly signed propagated error whenever either coefficient was negative.

- Multipeak Fitting.ipf - Fixed several issues in the Post-Collision Interaction (PCI) peak shapes: PCI Threshold no longer returns zero at x = 0, PCI Threshold now automatically switches to the PCI Approximation shape instead of producing invalid results when an unsupported asymmetry value is encountered, and a sign error in the initial-guess calculation was fixed. The PCI Threshold (Strict) shape's polarization-dependent asymmetry factor also had a sign and ratio error in its high-excess-energy branch, causing a discontinuity in the peak shape at the boundary between the two energy branches instead of matching smoothly. Added a new "2nd Electron" derived parameter reporting the calculated partner-electron energy for the PCI peak shapes.

- Multipeak Fitting.ipf - The Total Area uncertainty reported when simultaneously fitting multiple peaks now accounts for the covariance between peaks, instead of assuming each peak's contribution is independent.

- Varimax.ipf - Fixed a sign-flip bug and a bug where communalities were normalized along the wrong axis, either of which could produce incorrect Varimax-rotated factors.

- fuzzyClasses.ipf - Fixed a bug where two of the four fuzzy membership terms used each other's variance value, which could produce membership values that do not sum to 1.

- PeakFunctions2.ipf - Fixed a bug where switching a peak's fit function to Voigt in Multipeak Fitting left the width and height fields blank (NaN) instead of populating them from the existing coefficients.

- WMFitFunctions.ipf - Fixed the built-in DoG (Difference of Gaussians) fit function's surround term, which diverged for points far from the peak center instead of decaying to zero.

- Bivariate Histogram 2.ipf - Fixed BiHistWave() so that points falling below the histogram's X or Y range are excluded instead of being written into an incorrect bin.

- Log Histogram.ipf - Fixed a bug where a value falling exactly at (or beyond) the last bin's upper edge was written one element past the end of the destination wave instead of being excluded.

- leastSquaresEstimate.ipf - Fixed a bug that caused the function to read one wave element past its final computed estimate instead of returning that estimate.

- FilterDialog.ipf - Fixed the "dB min -50" scaling option in the Filter Design Laboratory's frequency response display, which reported magnitudes 2.5 times too large.

- WMBatchCurveFitResults.ipf - Fixed the nearest-point search used when displaying Batch Curve Fitting results, which applied an extra square root to only one of its two axis terms, distorting the distance metric.

- PeakFunctions2.ipf - Improved numerical instability in large Voigt shapes by replacing a piece of the shape expression with a better built-in Igor expression. `erfc(shape)*exp(shape^2)` was changed to `erfcx(shape)`.

- Global Fit 2.ipf - Corrected the displayed Voigt fit function equation so that it matches the formula actually used by the fit; the fit results themselves were not affected.

- Global Fit 2.ipf - Fixed a bug (introduced in Igor Pro 10) where entering the number of coefficients for a user-defined fit function that lacks Curve Fitting dialog comments did not fill in the Coefficients list.

- WMBatchCurveFit.ipf, Scatter Dot Plot.ipf, Color Table Control Panel.ipf - Fixed control placement on Windows that mixed points and panel coordinates. This caused controls in the Batch Curve Fitting and Scatter Dot Plot panels to overlap when the panels were first opened.

### Examples {#examples}

- Layout Demo.pxp - Updated to walk you through creating a multi-panel figure from graphs in a page layout.


## Update 10.03 {#update-10-03}

### Igor Application {#update-10-03-igor-application}

#### New Features {#update-10-03-new-features}

- The [igorpro.fn](/igorpro/python/python-module-reference.md#igorpro-fn) submodule now supports calling Igor user functions defined in independent or regular modules.

  For the independent module function `Analysis#processData()` defined in Igor:

  ```igor
  #pragma independentModule = Analysis

  function processData()
    ...
    return result
  end
  ```

  ```python
  # In Python, call the 'processData' function in the 'Analysis' independent module
  result = igorpro.fn.analysis.processData()
  ```

- The prefix and postfix increment ([++](/igorpro/programming/operators/operator-reference.md#increment)) and decrement ([--](/igorpro/programming/operators/operator-reference.md#decrement)) operators can now be applied
  to global variable references in Igor procedure code. For example:

  ```igor
  Function test()
    NVAR globalNumber = root:myGlobalVar
    globalNumber = 10

    // Postfix increment
    Variable result = globalNumber++  // result = 10; globalNumber = 11
    
    // Prefix decrement
    result = --globalNumber           // result = 9; globalNumber = 9
  End
  ``` 

- Added a key binding to temporarily override snapping to drawing guides. Hold down Caps Lock while dragging an object to suspend snap-to-guide.

#### Changed Behavior {#update-10-03-changed-behavior}

- Improved [ImageThreshold](/igorpro/commands/imagethreshold.md) Fuzzy threshold methods (/M=4 and /M=5) to provide better threshold values.

- The Find in All Windows command now uses the text under the cursor as the initial search string, matching the behavior of the regular Find command.


#### Bug Fixes {#update-10-03-bug-fixes}

- Fixed a bug in [MLLoadWave](/igorpro/commands/mlloadwave.md) where the operation's output variables where not set correctly when run from a user function.

- Fixed a crash that could occur when drawing certain TIFF images (1 bit per pixel with LZW compression) in a page layout.

- Fixed several problems interacting with draw object handles that extend beyond the page boundary in a page layout. Resizing and moving with those handles, cursor changes, and right-click contextual menus now work in the margin area. This was also broken in Igor Pro 9.

- Fixed incorrect handle highlighting (and a crash) when changing the layout expansion while drawing or editing polygons and Beziers in a page layout.

- Fixed a spurious compile error that occurred when a structure variable expression was combined with another expression.

- Fixed a spurious compile error involving a [FUNCREF](/igorpro/programming/keywords/object-reference-keywords.md#funcref) and a global string variable that have the same name.

- Fixed a bug in [SplitWave](/igorpro/commands/splitwave.md) when splitting a wave-reference wave or a data folder-reference wave (a wave whose elements are [WAVE](/igorpro/programming/keywords/object-reference-keywords.md#wave) or [DFREF](/igorpro/programming/keywords/object-reference-keywords.md#dfref) references). Only the first output wave received the correct references; the second and subsequent output waves had their references written to the wrong positions, so they contained incorrect or missing references. Numeric and text waves were not affected.

- Fixed a crash that could occur when free data folders stored in a thread queue were prematurely disposed.

- Fixed a bug in [Histogram](/igorpro/commands/histogram.md) where the square-root-of-counts destination wave specified with /N=destWave was created with the wrong name and as single precision instead of double precision.

- [KMeans](/igorpro/commands/kmeans.md) now sets the documented V_flag output variable.

- Fixed a bug in [FindValue](/igorpro/commands/findvalue.md) where the /RMD range was limited incorrectly for complex waves.

- Fixed a bug in [FindDuplicates](/igorpro/commands/findduplicates.md) that produced incorrect results for complex waves when the tolerance was zero.

- Fixed a bug in [ImageTransform](/igorpro/commands/imagetransform.md) where input waves used by the putRow and putCol keywords were not protected and could be overwritten when /DEST was used.

- Improved the error message reported when an unknown or inappropriate name is used where a number is expected. The message is now clearer instead of always reporting "expected number".

### Procedures {#update-10-03-procedures}

- Multipeak Fitting.ipf - The Multipeak Fit GUI now computes derived peak values (such as FWHM and peak area) for each peak after a fit. The results are stored in new "Peak N CoefsDER" waves alongside the existing peak coefficient waves.

- Multipeak Fitting.ipf - The Estimate Now button now bases its estimates on the currently visible graph range, so zooming in or out before clicking Estimate Now changes the result. Previously the estimate ignored the displayed range.

- Multipeak Fitting.ipf - Fixed a regression where finding peaks in the residuals could report many spurious peaks when the peaks are negative. This was visible in example 3 of the Multipeak Fit Demo experiment.

- Split Axis.ipf - The Split Axis package now copies error bars onto the split traces.


## Update 10.02 {#update-10-02}

### Igor Application {#update-10-02-igor-application}

#### New Features {#update-10-02-new-features}

- [PlaySound](/igorpro/commands/playsound.md) added /PAUS and /GO flags for pausing and resuming asynchronous sound playback.

- [FUNCREF](/igorpro/programming/keywords/object-reference-keywords.md#funcref) can now be properly passed by reference and returned from functions.

#### Changed Behavior {#update-10-02-changed-behavior}

- The `/UNATTENDED` command line flag now skips the license activation dialog.

- In 10.01, bitwise operators ([&](/igorpro/programming/operators/operator-reference.md#bitwise-and), [|](/igorpro/programming/operators/operator-reference.md#bitwise-or), and [%^](/igorpro/programming/operators/operator-reference.md#bitwise-xor)) returned incorrect large negative values when either operand was `NaN`. Bitwise operators are now defined to treat `NaN`, `Inf`, and `-Inf` operands as 0, matching the behavior in Igor 9 and 10.00.


#### Bug Fixes {#update-10-02-bug-fixes}

- Fixed a bug (introduced in 10.01) where layout draw objects selected a phantom object after drawing.

- [FuncFit](/igorpro/commands/funcfit.md) and [FuncFitMD](/igorpro/commands/funcfitmd.md) now support user-defined fit functions with complex independent variables in multidimensional curve fitting.

- Fixed a Qt library bug that resulted in a crash/exception during startup on machines running old versions of Windows 10.

- Fixed a crash in [FuncFit](/igorpro/commands/funcfit.md) when the fit function had no parameters.

- Fixed line continuation anomalies in the compiler.

- Fixed various Ctrl+F (Find), Ctrl+R (Replace), and Ctrl+G (Go To Line) bugs in procedure windows, the command window, and notebooks.


## Update 10.01 {#update-10-01}

All changes from [Update 10.01B01](#update-10-01b01) as well as the following changes:

### Igor Application {#update-10-01-igor-application}

#### Bug Fixes {#update-10-01-bug-fixes}
- Fixed a crash in [ConvexHull](/igorpro/commands/convexhull.md).

- Fixed a problem that caused incorrect rendering when exporting a cropped multipage layout as PDF. Previously the first page was rendered correctly but the rest of the pages might have been rendered with the wrong aspect ratio and/or bounding box.


## Update 10.01B01 {#update-10-01b01}

### Igor Application {#update-10-01b01-igor-application}

#### New Features {#update-10-01b01-new-features}

- Added a German language translation of the user interface (menus, dialogs, etc. but not documentation). We used AI for the translation (with partial human review) so there may be mistakes. Open the Miscellaneous Settings dialog (Misc🠖Miscellaneous Settings menu item) and select the Environment category to select a language. If your OS language is German Igor should ask you if you want to use the German language when it starts. Igor will remember your selection.

    We might use a similar process for additional languages. If you are interested in helping translate Igor, please see our post at [https://www.wavemetrics.com/forum/general/help-us-translate-igor-pro](https://www.wavemetrics.com/forum/general/help-us-translate-igor-pro) for additional information.

- Documentation for Igor Pro is now available online at [https://docs.wavemetrics.com](https://docs.wavemetrics.com).

- [PlaySound](/igorpro/commands/playsound.md) entirely rewritten to achieve gap-less playback of queued sounds. Added /STOP flag to stop any asynchronously playing sounds.

- Python 3.14 is now supported in Igor Pro 10.01.

:::note
Our support for Python 3.14 is currently limited to the 'standard' installation of Python 3.14, not the free-threaded installation.
:::

- Added the [igorpro.fn](/igorpro/python/python-module-reference.md#igorpro-fn) submodule for Python. This submodule allows users to directly call — and return values from — built-in, external, and user-defined Igor functions. 

  For example, to call Igor's built-in SortList function, you can now write:

  ```python
  # Descending sort. 'sorted' will hold: 'a;c;d;e;g;x;'
  sorted = igorpro.fn.sortlist('x;c;e;g;d;a', ';', 1)
  ```

  `igorpro.fn` supports returning real and complex numbers, strings, wave references, and data folder references from Igor functions.

- Using the Igor64.exe command line flag `/START=3` now prints startup information to standard output (stdout). This can be useful if you are running Igor via some automated process.

- [MatrixOP](/igorpro/commands/matrixop.md) /KCLS flag has been extended to support the third dimension.

- Improved performance of all-at-once threadsafe curve fitting by approximately 50%. The unperturbed model calculation is now run inside the parallel multithreading loop.

- Added a flag (`/CPAD`) to [ImageTransform](/igorpro/commands/imagetransform.md) padImage that supports symmetric padding around the image in either mirroring the edge data or repeating the last pixel values.

- Gizmo, Igor's 3D graphing tool, now supports rendering of exported graphics and page layout images when the Gizmo window is hidden. Previously, a Gizmo page layout object displayed a blank box with the message, "Cannot draw a hidden Gizmo". See [Gizmo Overview](/igorpro/graphing/3d-graphics.md#gizmo-overview) to learn about Gizmo.

#### Changed Behavior {#update-10-01b01-changed-behavior}

- The `_labels_` keyword used in [Display](/igorpro/commands/display.md), [AppendToGraph](/igorpro/commands/appendtograph.md), and [ReplaceWave](/igorpro/commands/replacewave.md) commands is no longer translated in localized versions of Igor. Previously, Japanese Igor translated this keyword to `_ラベル_`, which caused errors when experiments or procedure files were shared between different language versions. Commands now always use `_labels_` regardless of language. For backward compatibility, Igor still accepts `_ラベル_` when parsing commands, but always generates `_labels_` when creating commands.

:::note
Experiments or procedure files created with Igor Pro 10.01 or later that use the `_labels_` keyword will cause errors when opened with Japanese Igor Pro 8 through 10.00, since those versions only recognized the translated `_ラベル_` keyword. When opening an experiment file, a dialog will appear allowing you to edit the failed command- simply replace `_labels_` with `_ラベル_` to resolve the error.
:::

- Improved error checking for inputs to the [IntegrateODE](/igorpro/commands/integrateode.md) operation. This includes checking numeric inputs for proper range, forbidding `NaN` and `Inf` values, and checking for missing waves or waves with incorrect type or size. This could potentially cause errors in "working" code, but the errors flagged would have caused incorrect behavior that could be hard to debug.

- Bitwise operators ([|](/igorpro/programming/operators/operator-reference.md#bitwise-or), [&](/igorpro/programming/operators/operator-reference.md#bitwise-and), [~](/igorpro/programming/operators/operator-reference.md#bitwise-complement), and [%^](/igorpro/programming/operators/operator-reference.md#bitwise-xor)) no longer convert their operands to unsigned integers with truncation. They now convert their operands to signed integers, so that signed operands produce the expected result.

- `#pragma independentModule=ProcGlobal` is now a compilation error. This was never valid but was previously silently accepted.

- Igor now checks the Python version before initialization and gives a clear error message if the version is unsupported.

- [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) saves waves more efficiently when data folders contain many waves. This also applies to saving a packed HDF5 experiment.

#### Bug Fixes {#update-10-01b01-bug-fixes}

- Fixed a bug in the Text Marker dialog that caused a mismatch between the text anchor point widget and the anchor point in the generated command.

- Improved rendering of EMF pictures in notebooks and help files.

- Control position and sizes accept floating point values.

- Controls are more accurately positioned and sized when control panel expansion is other than a multiple of 100%.

- XOPs can now be used as fit functions. Previous incorrect behavior was that any fit using a non-threadsafe external fit function would result in a singular matrix error. This has been fixed. Threadsafe external fit functions were not affected by this bug and continue to execute normally.

- Fixed a bug that caused layouts to be the wrong size and position when printed.

- Fixed a bug that could result in incorrect triggering of trace drag in a graph subwindow if you clicked first in the graph subwindow and then quickly clicked and held in some other area of the window containing that graph subwindow.

- Fixed a bug that caused too many calls to a window hook function for Resize events.

- Fixed a bug in the [FindPeak](/igorpro/commands/findpeak.md) operation that caused a crash when finding peaks in a wave with more than a million data points. The fix both prevents the crash and improves performance on these large waves by a factor as large as 40.

- Fixed a bug that could prevent drawing of graph draw objects that use axis coordinates.

- Fixed a bug that incorrectly limited dragging of Layout Guides when a subwindow was activated.

- Fixed a potential crash if you killed a wave while in Edit Wave mode in a graph window.

- Fixed a bug that caused custom colors added in the Select Color dialog (what you get when you click the Other... button in a color picker) to not be saved and restored across Igor sessions.

- Fixed a bug where Python code completion results were not sorted.

- Fixed a bug where collections of Python booleans (lists, arrays, tuples) could not be returned to Igor.

- Fixed a bug where Python `import` could not find modules in the current working directory.

- Fixed a bug where the Python console window was not shown and raised when selecting Open Console from the Python menu.

- Fixed Python console docking and undocking coordinate issues on multi-monitor setups.

- Fixed a bug where the code completion popup did not offer suggestions for module-qualified functions (e.g., `myModule#funcName`). Also improved completion within independent modules to offer functions from the entire module namespace, not just the current file.

- Fixed a bug in [ImageRegistration](/igorpro/commands/imageregistration.md) that caused a memory issue when processing stacks.

- Fixed a crash in [WaveStats](/igorpro/commands/wavestats.md) and incorrect wave creation in [MatrixOP](/igorpro/commands/matrixop.md) related to the /KCLS flag with certain dimension configurations.

- Fixed bugs in [ImageEdgeDetection](/igorpro/commands/imageedgedetection.md) boundary processing.

- Fixed a bug where the [ImageMorphology](/igorpro/commands/imagemorphology.md) /S flag was incorrectly changed to /H. The documented /S flag is now used.

- Fixed a bug in [DuplicateDataFolder](/igorpro/commands/duplicatedatafolder.md) that could corrupt a pre-existing local string variable when it shared an internal pointer with a global string being overwritten.

- Fixed a bug where [MoveWave](/igorpro/commands/movewave.md) incorrectly cleared the contents of wave-reference waves when moving free waves through a free data folder.

- Fixed a bug where [ReorderTraces](/igorpro/commands/reordertraces.md) with an invalid trace name could delete traces from the graph before reporting the error.

- Fixed a bug in the [ReorderTraces](/igorpro/commands/reordertraces.md) and [ReorderImages](/igorpro/commands/reorderimages.md) dialog that caused it to fail when the same wave appeared in a graph more than once.

- Fixed a bug where [IntegrateODE](/igorpro/commands/integrateode.md) programmed stop (derivative function returning 1) did not take effect immediately and could delay for a long time with small internal step sizes.

- Fixed a bug in [IntegrateODE](/igorpro/commands/integrateode.md) using the BDF method where an error weighting wave could cause incorrect results or errors due to uninitialized memory.

- Fixed a bug where string functions such as [TrimString](/igorpro/commands/trimstring.md) truncated strings at embedded null bytes instead of preserving the full string content.

- Fixed a bug where [RemoveFromTable](/igorpro/commands/removefromtable.md) incorrectly applied column type restrictions that should only apply to [AppendToTable](/igorpro/commands/appendtotable.md).

- Fixed a crash when dragging a subwindow resize handle.

- Fixed a crash when using the graph contextual menu in certain configurations.

- Fixed a potential crash when XOP functions use structs with threadsafe pointers. Also fixed incorrect complex return values from external functions used by [SumSeries](/igorpro/commands/sumseries.md).

- Fixed a potential crash when checking structs for external curve fitting functions.

- Fixed a crash during mouse release on exterior subwindows when the window is destroyed during event handling.

- Fixed a bug where tags attached to hidden traces or images were not hidden.

- Fixed Gizmo axis labels being clipped at the top.

- Fixed a bug where Gizmo surface objects with `NaN`-containing matrix waves did not draw when using constant color.

- Fixed a bug where free axes positioned relative to perpendicular axes did not reserve room for axis labels during graph recreation.

- Fixed a bug where column grid lines in table subwindows within layouts were not drawing correctly at certain display scalings.

- Fixed a bug where table subwindow column widths shifted incorrectly during resolution changes in layouts.

- Fixed a bug where table subwindows in layouts were continuously repainting, causing excessive drawing and performance issues.

- Fixed a bug where right-clicking a table subwindow did not activate it before showing the contextual menu.

- Fixed several issues with Find (Ctrl+F), Replace (Ctrl+R), and Go To Line (Ctrl+G) keyboard shortcuts in procedure windows, the command window, and plain text edit fields. The cursor now correctly focuses on the appropriate text field when switching between Find and Replace modes.

- Fixed a bug where the STFT dialog "From Target" toggle did not work correctly.

- Fixed a bug where 8-bit AIFF and AIFC audio files were loaded with corrupted (unsigned instead of signed) sample data.

- Fixed a bug where [DoIgorMenu](/igorpro/commands/doigormenu.md) did not update associated graphs while a dialog was open.

- Fixed duplicate ruler IDs in notebooks that caused rulers to switch unexpectedly when adjusted.

- Fixed a bug where the compiler gave a confusing error instead of "Expected a wave reference" in certain scenarios.

- Fixed inconsistent error messages in [ControlBar](/igorpro/commands/controlbar.md) between compiled and interpreted code paths.

- [CurveFit](/igorpro/commands/curvefit.md) now accepts wave subranges when using an X wave. Previously, subranges were rejected even when the subrange size matched the X wave size. This has been a bug for decades.

- Fixed a bug where dashed lines with `NaN` coordinates could cause rendering issues.

- Fixed a bug in the [area](/igorpro/commands/area.md) function where the trapezoidal end-point correction was discarded, producing incorrect results. The [faverage](/igorpro/commands/faverage.md) function was also affected.

- Fixed bugs in [MatrixOP](/igorpro/commands/matrixop.md) `crossCovar` and `binVar`. `crossCovar` was squaring the wrong input's data, and `binVar` was summing deviations instead of squared deviations.

### Procedures {#update-10-01b01-procedures}

- IFDL.ipf - Resized the IFDL panel to show entire title.

### Examples {#update-10-01b01-examples}

- All Controls Demo.pxp - Modernized for Igor 10.

- Resize Panel and List Demo.pxp - explains 3 different ways to resize controls in a panel:
  1. custom window hook
  2. generalized window hook with ResizeControls.ipf
  3. user guides introduced in Igor 10