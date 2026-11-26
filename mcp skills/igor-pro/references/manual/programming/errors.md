---
description: "Igor Pro Error Messages: This file contains reference material. It is not expected to be read from beginning to end."
slug: /programming/errors
---

# Igor Pro Error Messages {#igor-pro-error-messages}

This file contains reference material. It is not expected to be read from beginning to end.

## Errors {#errors}

### A file type specifier must have exactly 4 bytes {#a-file-type-specifier-must-have-exactly-4-bytes}

For example, the type specifier for a plain text file is "TEXT". For an Igor binary wave file it is "IGBW". See [File Types and Extensions](/igorpro/user-interface/platform-related-issues.md#file-types-and-extensions) for a discussion of how Igor maps extensions to file types.

### A movie file is already open {#a-movie-file-is-already-open}

Use the CloseMovie operation to close the open movie before opening a new one.

### A wave must have at least 2 points {#a-wave-must-have-at-least-2-points}

Prior to Igor Pro 3.0, it was necessary to have at least 2 points in a wave. Waves in Igor Pro 3.0 can have zero or one point. Some operations may not work with less than 2 points, however.

### All allocation blocks on the volume are full {#all-allocation-blocks-on-the-volume-are-full}

In other words, the disk is full. Try saving to another disk.

### All waves must have the same number of dimensions and at least two dimensions and same viewed dimensions {#all-waves-must-have-the-same-number-of-dimensions-and-at-least-two-dimensions-and-same-viewed-dimensions}

Igor allows changing views only if the selected columns all have the same number of dimension and are currently showing the same dimensions vertically and horizontally in the table. Select one of the waves at a time and change its view.

### Ambiguous wave point number {#ambiguous-wave-point-number}

Igor expected a single number, such as a point in a wave, but you've specified an entire wave. For example, wave1(0) represents a single number whereas wave1 represents the entire wave.

### An attempt was made to access a wave using an incompatible access mode {#an-attempt-was-made-to-access-a-wave-using-an-incompatible-access-mode}

This error is most likely due to a bug in an Igor extension (XOP).

### An attempt was made to treat a text wave as if it were a numeric wave {#an-attempt-was-made-to-treat-a-text-wave-as-if-it-were-a-numeric-wave}

This typically results from passing a text wave to an Igor operation or function that expects a numeric wave.

### An attempt was made to treat a numeric wave as if it were a text wave {#an-attempt-was-made-to-treat-a-numeric-wave-as-if-it-were-a-text-wave}

This typically results from passing a numeric  wave to an Igor operation or function that expects a text wave.

### An HDF5 object cannot be written because it already exists in the file {#an-hdf5-object-cannot-be-written-because-it-already-exists-in-the-file}

This error occurs if you use [HDF5SaveData](/igorpro/commands/hdf5savedata.md) without the /O flag to write an object to an HDF5 group that already contains an object with the specified name.

It also occurs when saving an HDF5 file if the name of a wave in Igor is the same as the name of a variable in the same data folder. Igor permits such name conflicts but HDF5 does not.

For example, in a new experiment, enter the following function in the procedure window:


```igor
Function CreateWaveVarNameConflict()	// Execute this in a new experiment
    Make/O root:test
    Variable/G root:test
End
```

Now execute this from the command line:


```igor
CreateWaveVarNameConflict()
SaveExperiment/C/F={2,"",0}/P=IgorUserFiles as "Test.h5xp"	// Save as HDF5 packed experiment file
```

This throws an error because Igor attempts to write both the wave and the variable as datasets with the same name in the same HDF5 group.

The solution is to rename the Igor wave or variable and then retry the save. Continuing the example:


```igor
Rename root:test, testWave		// Eliminate name conflict
SaveExperiment/C/F={2,"",0}/P=IgorUserFiles as "Test.h5xp"	// Save as HDF5 packed experiment file
```

Now no error is thrown.

This problem affects saving HDF5 packed experiments manually or using the [SaveExperiment](/igorpro/commands/saveexperiment.md) operation and affects the [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) operation.

For further explanation, see [Object Name Conflicts and HDF5 Files](/igorpro/igor-basics/using-igor.md#object-name-conflicts-and-hdf5-files).

### An invalid index was used to access a wave {#an-invalid-index-was-used-to-access-a-wave}

For a wave of length n, valid point number indices are in the range 0 to n-1.

### An XOP has attempted recursion {#an-xop-has-attempted-recursion}

An external operation or function has made a call to Igor which asked Igor to do something that would call the external operation or function. The most likely cause for this is that the external is executing a Command callback that invokes itself. It will also happen if the external executes a DoUpdate callback and the action procedure for a control calls the same external. Please report this error to the XOP programmer.

### Attempt to operate on a null (missing) wave {#attempt-to-operate-on-a-null-missing-wave}

This occurs in a user function when you reference a wave using a WAVE declaration or a $ expression and that wave does not exist when the function executes. For more information, see [Runtime Lookup Failure](/igorpro/programming/programming.md#runtime-lookup-failure).

### Attempt to use a null string variable {#attempt-to-use-a-null-string-variable}

This occurs in a user function when you try to use it before assigning a value to it. If you want an empty string, assign "" to it (e.g., String str = "").

### Background user function returned error {#background-user-function-returned-error}

For information on the background function, see [SetBackground](/igorpro/commands/setbackground.md) and [CtrlBackground](/igorpro/commands/ctrlbackground.md).

### Bad character in name {#bad-character-in-name}

You have used an illegal character in a name. See [Object Names](/igorpro/igor-basics/using-igor.md#object-names).

### Bad checksum {#bad-checksum}

An Igor binary wave file contains a checksum to make sure that the file is valid. This file's checksum is not correct. The file has been damaged and can't be loaded. This will also happen if you try to load a file that is not an Igor binary wave file as an Igor binary wave file. For programmer-details on the Igor binary wave file, see Igor Technical Note #003.

### Bad Igor text file (BEGIN keyword but no WAVES) {#bad-igor-text-file-begin-keyword-but-no-waves}

The WAVES keyword and the names of waves to be created must appear in an Igor text file before a block of data. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Bad Igor text file (missing keyword IGOR) {#bad-igor-text-file-missing-keyword-igor}

Igor text files must start with the keyword IGOR. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Bad or damaged binary file {#bad-or-damaged-binary-file}

The header information in this file is inconsistent. The file is damaged and can't be loaded. For programmer-details on the Igor binary wave file, see Igor Technical Note #003.

### Bad or missing imaginary number {#bad-or-missing-imaginary-number}

A wave in an Igor text file is specified as complex but Igor can't find the imaginary part. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Bad symbol on WAVES line {#bad-symbol-on-waves-line}

The WAVES keyword and the names of waves to be created must appear in an Igor text file before a block of data. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Both positive & negative error bar waves are missing {#both-positive-negative-error-bar-waves-are-missing}

The syntax for the ErrorBars operation when used to specify error values in waves is as follows:


```igor
ErrorBars wave1, Y wave=(w1,w2)	for upper and lower error bars
ErrorBars wave1, Y wave=(w1,)	for upper error bars only
ErrorBars wave1, Y wave=(,w2)	for lower error bars only
```

### Break must be within a loop {#break-must-be-within-a-loop}

break is used to break out of an iterate-loop or do-while structure.

### Can't add items to this menu {#can-t-add-items-to-this-menu}

A user menu definition can't add an item to an XOP menu or to some Igor menus. See [Built-in Menus That Can Be Extended](/igorpro/user-interface/user-defined-menus.md#built-in-menus-that-can-be-extended) in the Using Igor help file.

### Can't append different x-wave to category axis {#can-t-append-different-x-wave-to-category-axis}

Just one X wave can be used to define an X axis in a category plot. Multiple text waves as for a single category plot can be accommodated if you use more than one horizontal axis.

### Can't append text x-wave to noncategory axis {#can-t-append-text-x-wave-to-noncategory-axis}

You are trying to append a wave versus a text wave using an axis that is already in use with numeric data. You can add a category plot to the graph if you use a new horizontal axis.

### Can't change a special symbolic path {#can-t-change-a-special-symbolic-path}

The home and Igor paths are built in to Igor and you cannot change them.

### Can't change a wave in the middle of a wave assignment {#can-t-change-a-wave-in-the-middle-of-a-wave-assignment}

During a wave assignment, a user or external function attempted to change the number type or length of the wave.

### Can't combine complex wave with real wave {#can-t-combine-complex-wave-with-real-wave}

You may want to use the [real](/igorpro/commands/real.md) and [imag](/igorpro/commands/imag.md) functions. For example, wave0 = real(complexWave0).

### Can't combine real wave with complex wave {#can-t-combine-real-wave-with-complex-wave}

You may want to use the [cmplx](/igorpro/commands/cmplx.md) function. For example, complexWave0 = cmplx(wave0, wave1).

### Can't convert a system file path to a Unicode file path {#can-t-convert-a-system-file-path-to-a-unicode-file-path}

This error should not occur in Igor 7 or later.

### Can't convert a Unicode file path to a system file path {#can-t-convert-a-unicode-file-path-to-a-system-file-path}

This error should not occur in Igor 7 or later.

### Can't cut a mix of rows from one wave and columns from another {#can-t-cut-a-mix-of-rows-from-one-wave-and-columns-from-another}

If all of one or more table columns of a multidimensional wave is selected, Igor cuts the selected table columns. Otherwise, Igor cuts the selected table rows. In this case, you have a mix of these two cases so Igor cannot do the cut. Select data from one of the waves at a time and do the cut.

### Can't delete special symbolic path {#can-t-delete-special-symbolic-path}

The home symbolic path is built in to Igor and can't be deleted.

### Can't do function on this number type {#can-t-do-function-on-this-number-type}

A curve fit cannot be done on a complex wave. You can create a real wave and use the [real](/igorpro/commands/real.md) or [imag](/igorpro/commands/imag.md) function to set the new real wave equal to the real or imaginary part of the complex wave. Then you can do the curve fit on the new real wave.

### Can't find file containing XOP {#can-t-find-file-containing-xop}

This happens if you move or rename an XOP file while Igor is running or double-click an XOP file that was not in "Igor Pro Folder/Igor Extensions" or "Igor Pro User Files/Igor Extensions" when Igor started.

### Can't find the control's action procedure named "^0" {#can-t-find-the-control-s-action-procedure-named-0}

This occurs if the control's action procedure was renamed or deleted.

### Can't open multiple help files with the same file name {#can-t-open-multiple-help-files-with-the-same-file-name}

Prior to Igor 7, Igor allowed you to open two help files with the same name, but it did not work right. Consequently, as of Igor 7, it is an error to attempt to open two help files with the same file name.

If you want to open another help file with the same file name as one that is already open, close the already open file and then open the other one. To close a help file, press Alt while clicking the close box.

### Can't open print record (check print driver) {#can-t-open-print-record-check-print-driver}

Probably there is no printer driver file in the current system file.

### Can't overwrite self {#can-t-overwrite-self}

In a Duplicate command the source wave cannot appear as a destination wave also.

### Can't overwrite a text wave with a numeric wave or vice versa {#can-t-overwrite-a-text-wave-with-a-numeric-wave-or-vice-versa}

If you want to reuse a wave name and change to or from a text wave, kill the wave first with the KillWaves command line operation, or with the Kill Waves item in the Data menu.

### Can't remove a wave that controls an axis {#can-t-remove-a-wave-that-controls-an-axis}

The wave that you tried to remove is supplying the X axis values in a parametric graph so you can't remove it.

### Can't save multiple waves to a single binary file {#can-t-save-multiple-waves-to-a-single-binary-file}

Binary files store one wave per file so you can't specify a file name in a save command if the file format is Igor binary and you also specify multiple waves. If you omit the file name Igor will assign default file names for each wave.

### Can't use $ in this way in a function {#can-t-use-in-this-way-in-a-function}

See [Runtime Lookup of Globals](/igorpro/programming/programming.md#runtime-lookup-of-globals).

### Can't use a parametric X wave here {#can-t-use-a-parametric-x-wave-here}

The command operates only on waves which supply the Y values for a graph. You specified a wave that is supplying X values in a parametric graph.

### Can't use standard axis name on different edge {#can-t-use-standard-axis-name-on-different-edge}

The axis names left, top, right and bottom are reserved for standard axes.

### Can't use wave(x)= in a function. Use x2pnt and wave[p]= instead {#can-t-use-wave-x-in-a-function-use-x2pnt-and-wave-p-instead}

For example,


```igor
wave1(2.3)= 5
```

has to be written as


```igor
wave1[x2pnt(wave1,2.3)]= 5
```

### Conflict creating V_ or S_ local variable. Probably user's NVAR, SVAR or wrong type {#conflict-creating-v_-or-s_-local-variable-probably-user-s-nvar-svar-or-wrong-type}

An operation called in the function creates an output variable or string, and the function has a definition of a local variable or string with a name that conflicts. For instance, the compiler will flag the following code:


```igor
#pragma rtGlobals=1
Function test()
    NVAR V_avg=root:MyAverage 	// Create local name that looks like a 
                    // WaveMetrics variable
    WaveStats junk	// generates error because WaveStats 
                    // creates V_avg variable and the name is taken
end
```

The following is alright because the local variable V_avg can be used for the WaveStats output:


```igor
#pragma rtGlobals=1
Function test()
    Variable V_avg		// Create local name that looks like a 
                            // WaveMetrics variable
    WaveStats junk		// OK- no conflict with local variable of
                            // proper type.
End
```

But this is not accepted because the local variable is the wrong type:


```igor
#pragma rtGlobals=1
Function test()
    Variable/C V_avg		// Create local name that looks like a 
                            // WaveMetrics variable, but complex
    WaveStats junk		// Error- V_avg made by WaveStats is not complex
End
```

### Destination wave must be single precision real for accumulate {#destination-wave-must-be-single-precision-real-for-accumulate}

The accumulate option (/A) in the histogram command does not work with a double precision or complex destination wave. You can convert a wave to single precision using the Redimension operation.

### Expected /N=name {#expected-n-name}

The /C and /K flags in the Tag, TextBox and Legend operations must be followed immediately by /N=name where name is the name of the annotation.

### Expected a wave reference {#expected-a-wave-reference}

This error is be triggered by the stricter compilation turned on by the rtGlobals=3 pragma and by other situations where Igor is expecting a wave reference.

As explained under [The rtGlobals Pragma](/igorpro/programming/programming.md#the-rtglobals-pragma), with rtGlobals=3 in effect you need to use a wave reference in commands that would otherwise not require it. For example:


```igor
#pragma rtGlobals=3
Function Test()
    // Wrong - you need a wave reference
    Display wave0

    // Right - this tells Igor that wave0 is a wave
    Wave wave0
    Display wave0
End
```

This error occurs because, under rtGlobals=3, Igor does not assume that wave0 is a wave - you have to specify that it is a wave using a wave reference. See also [Runtime Lookup of Globals](/igorpro/programming/programming.md#runtime-lookup-of-globals) and [Wave References](/igorpro/programming/programming.md#wave-references).

This error may also occur in other circumstances. The solution is the same - add a wave reference.

### Expected BEGIN keyword after WAVES in Igor Text file {#expected-begin-keyword-after-waves-in-igor-text-file}

See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Expected column name {#expected-column-name}

See [Invalid column name](#invalid-column-name).

### Expected endif {#expected-endif}

There is an if in the procedure that is not matched by an endif.

### Expected fitting function {#expected-fitting-function}

The fitting function keywords used with the CurveFit operation are gauss, lor, exp, dblexp, sin, line and poly. They should not be placed in quotes.

### Expected font name {#expected-font-name}

Expected a font name in quotes, such as "Helvetica".

### Expected graph, table, PICT, or textbox name {#expected-graph-table-pict-or-textbox-name}

If you are trying to use the $ operator in a Layout or AppendToLayout command, you need to put the entire object specification into the string. For example:


```igor
String s = "Graph0(1, 1, 6, 5)/F=1"
Layout/I $s
```

See [Layout](/igorpro/commands/layout.md)ions[Layout] for more examples and details.

### Expected graph size keyword {#expected-graph-size-keyword}

The graph size keywords are: perUnit, aspect and plan. For example:


```igor
Modify width={perUnit,72,bottom}.
```

### Expected loop {#expected-loop}

There is an iterate in the macro that is not matched by a loop. iterate loops are archaic and are included only for backward compatibility.

### Expected menu name {#expected-menu-name}

The menu name must be the name of a built-in or user-defined menu.

### Expected name of active axis {#expected-name-of-active-axis}

The names of the standard axes are bottom, left, top and right. An axis is active if it is displayed on the graph but is not a mirror axis. To find the name of any free axes on a graph, use the Modify Axis dialog.

### Expected name of graph window {#expected-name-of-graph-window}

The name of a graph window is not the same as the window title. It is either a name like Graph0 or Graph1 that Igor automatically assigns when you create a new graph or it is the name of the Window macro that created the graph.

See [Object Names](/igorpro/igor-basics/using-igor.md#object-names) and [Graphs](/igorpro/graphing/graphs.md) for details.

### Expected name of page layout window {#expected-name-of-page-layout-window}

The name of a layout window is not the same as the window title. It is either a name like Layout0 or Layout1 that Igor automatically assigns when you create a new layout or it is the name of the Window macro that created the layout.

See [Object Names](/igorpro/igor-basics/using-igor.md#object-names) and [Page Layouts](/igorpro/graphing/making-figures/page-layouts.md) for details.

### Expected notebook selection keyword {#expected-notebook-selection-keyword}

See [Notebook](/igorpro/commands/notebook.md)ns[Notebook].

### Expected operand {#expected-operand}

Igor found an operator where it expected an operand.

This can also happen if you forget to use a comma after a numeric operand.

### Expected operator {#expected-operator}

Igor found an operand where it expected an operator.

This can also happen if you forget to use a comma after a numeric operand.

### Expected string expression {#expected-string-expression}

A string expression is a string in quotes, a string variable, the result of a string function or a combination of these and the + operator.

### Expected string variable name {#expected-string-variable-name}

A string variable name must start with a letter. Subsequent characters can be ASCII letters, digits or the underscore character. The name can consist of up to 255 bytes. The name must not conflict with the name of any other Igor operation, function, keyword, procedure or variable. Use the Object Status dialog to see what string variables exist.

### Expected variable name {#expected-variable-name}

A variable name must start with a letter. Subsequent characters can be ASCII letters, digits or the underscore character. The name can consist of up to 255 bytes. The name must not conflict with the name of any other Igor operation, function, keyword, procedure or variable. Use the Object Status dialog to see what variables exist.

### Failure to converge during fit {#failure-to-converge-during-fit}

After 40 iterations the curve fit operation was not able to find the best fit.

See [Curve Fitting Troubleshooting](/igorpro/analysis/curve-fitting.md#curve-fitting-troubleshooting).

### Fitting function does not have required form {#fitting-function-does-not-have-required-form}

See [User-Defined Fitting Functions](/igorpro/analysis/curve-fitting.md#user-defined-fitting-functions).

### Flag in wrong place {#flag-in-wrong-place}

The option flags in an operation must follow the operation name directly.

### Formula is too long {#formula-is-too-long}

The text for a dependency formula is limited to 2500 bytes.

### Ill-formed name {#ill-formed-name}

The name of an Igor object must start with an alphabetic character and may contain alphabetic characters or numbers or the underscore character. See [Object Names](/igorpro/igor-basics/using-igor.md#object-names).

### Illegal index value {#illegal-index-value}

The source wave in an IndexSort command must be a valid index wave as created by the MakeIndex command. Specifically the wave must contain integral values from 0 to n-1 where n is the number of points in the destination wave.

### Include file not found {#include-file-not-found}

There are four legal ways to construct an include statement:


```igor
#include <fileNameStr >         // Igor searches for file in the "WaveMetrics Procedures"
                                // folder and all subfolders

#include "fileNameStr "         // Igor searches for file in
                                // "Igor Pro Folder/User Procedures" and in
                                // "Igor Pro User Files/User Procedures" and in
                                // all subfolders

#include "full File Path "      // the file is completely specified. For example:
                                // "Hard Disk:Desktop Folder:Proc0"

#include ":partial File Path "  // the file is specified starting from the Igor folder.
                                // For example: ":Spectroscopy Procedures:Voight Procs"
```



See [The Include Statement](/igorpro/programming/programming-techniques.md#the-include-statement) for details.

### Incompatible binary version {#incompatible-binary-version}

This Igor binary wave file was created by an early version of Igor. The old file format is no longer supported.

### Incompatible number types {#incompatible-number-types}

The destination and X waves in a curve fit must have the same number type as the source wave.

### Incompatible wave lengths {#incompatible-wave-lengths}

The destination and X waves in a curve fit must have the same number of points as the source wave. In some other operations, sorting for example, the source and destinations waves must also have the same number of points.

### Inconsistent type for a wave reference {#inconsistent-type-for-a-wave-reference}

A WAVE declaration in a user function conflicts with another wave or NVAR or SVAR reference or with a local variable name. For example, if you have:


```igor
Wave outputWave
```

in one part of the function, you cannot have


```igor
Wave/C outputWave
```

in another part of the function.

Sometimes this arises because the Igor compiler has automatically created local variables. See [Accessing Variables Used by Igor Operations](/igorpro/programming/macros.md#accessing-variables-used-by-igor-operations) for details.

It can also happen because the compiler has automatically generated a wave reference. See [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details.

It can also happen because the compiler has automatically created an NVAR or SVAR. See [Automatic Creation of WAVE, NVAR and SVAR References](/igorpro/programming/programming.md#automatic-creation-of-wave-nvar-and-svar-references) for details.

### Inconsistent type for a global variable reference {#inconsistent-type-for-a-global-variable-reference}

An NVAR or SVAR in a user function conflicts with another NVAR or SVAR or WAVE reference or with a local variable name. For example, if you have:


```igor
NVAR var1
```

in one part of the function, you cannot have


```igor
SVAR var1
```

in another part of the function.

Sometimes this arises because the Igor compiler has automatically created local variables. See [Accessing Variables Used by Igor Operations](/igorpro/programming/macros.md#accessing-variables-used-by-igor-operations) for details.

It can also happen because the compiler has automatically generated a wave reference. See [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details.

It can also happen because the compiler has automatically created an NVAR or SVAR. See [Automatic Creation of WAVE, NVAR and SVAR References](/igorpro/programming/programming.md#automatic-creation-of-wave-nvar-and-svar-references) for details.

### Insufficient or illegal range {#insufficient-or-illegal-range}

A range of X values specified for an operation such as WaveStats or CurveFit includes points that don't exist or does not include enough points to do the operation.

### Invalid column name {#invalid-column-name}

Column names consist of wave names optionally followed by the suffixes .i (index), .d (data), .id (data and index), or .l (dimension labels). The .d and .id suffixes may be followed by .real or .imag. See [Column Names](/igorpro/igor-basics/tables.md#column-names) for details.

When specifying a column using a string variable, the wave name is stored in the string variable but the suffix is not. For example:


```igor
String name = "wave0"
Edit $name.id
```

### Line too long. Command lines are limited to 2500 bytes {#line-too-long-command-lines-are-limited-to-2500-bytes}

Command lines must be no longer than 2500 bytes. This applies to command lines generated by dialogs, command lines that you enter directly in the command buffer and command lines entered in the command buffer by procedures.

### Loop with no iterate or other flow control mismatch {#loop-with-no-iterate-or-other-flow-control-mismatch}

See [Loops](/igorpro/programming/programming.md#loops) or [If-Else-Endif Statements](/igorpro/programming/programming.md#if-else-endif-statements).

iterate loops are archaic and are included only for backward compatibility.

### Macro nesting overflow {#macro-nesting-overflow}

Macros can be nested to 14 levels. You have nested your macros too deeply. This can occur if a macro calls itself.

### Matlab dynamic libraries are not available {#matlab-dynamic-libraries-are-not-available}

To read Matlab .mat data files Igor needs to link to dynamic libraries that come with Matlab. You can tell Igor where to find these libraries by opening the Load Matlab Binary Data dialog, by choosing Data->Load Waves->Load Matlab MAT File, and clicking the "Find 32-bit Matlab Libraries" button or the "Find 64-bit Matlab Libraries" button. Igor remembers this location for future sessions.

See [Matlab Dynamic Library Issues](/igorpro/data/importing-and-exporting-data.md#matlab-dynamic-library-issues) for further information.

### Menu Compilation Error {#menu-compilation-error}

See [User-defined Menus](/igorpro/user-interface/user-defined-menus.md).

### Missing END or unknown symbol {#missing-end-or-unknown-symbol}

A block of data in an Igor text file must be introduced with the BEGIN keyword and ended with the END keyword. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Name or string too long {#name-or-string-too-long}

Names of most types of objects can be up to 255 bytes, though some are limited to 31 bytes. Wave units are limited to 49 bytes. See [Long Object Names](/igorpro/igor-basics/using-igor.md#long-object-names) for details.

### No background task to control {#no-background-task-to-control}

See [SetBackground](/igorpro/commands/setbackground.md)tBackground].

### No data was found in file {#no-data-was-found-in-file}

See [Importing Data](/igorpro/data/importing-and-exporting-data.md). This explains what Igor is looking for when loading data from a file.

### No data was found in the clipboard {#no-data-was-found-in-the-clipboard}

If you are pasting into the unused cell in a table to create a new wave or waves, this can happen if the clipboard does not contain data formatted as Igor expects. Igor looks for an optional column name followed by data. For example, this would create a numeric wave with a name like wave0:


```
1
2
3
```

This would create a numeric wave named Test1:


```
Test1
1
2
3
```

This would create a text wave named Test2:


```
Test2
One
Two
Three
```

A problem occurs if you are pasting a single text item into the used cell, for example:


```
One
```

In this case, Igor will take One as the name of the wave and will find no wave data. Igor will then report "no data was found in the clipboard". The workaround is to enter any arbitrary text in the unused cell by typing and pressing the Enter key to create a new text wave. Then select the newly-created cell and paste.

If you are using LoadWave, see [Importing Data](/igorpro/data/importing-and-exporting-data.md). This explains what Igor is looking for when loading data from a file or from the clipboard.

### No target window {#no-target-window}

This operation acts on the target window which is the top graph, table, page layout, control panel or XOP target window but there are currently no target windows.

### No wave names found {#no-wave-names-found}

The WAVES keyword and the names of waves to be created must appear in an Igor text file before a block of data. See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Not a parameter name {#not-a-parameter-name}

The name of a parameter in a parameter declaration must match the name used in the macro or function declaration. See [Macro Syntax](/igorpro/programming/macros.md#macro-syntax) or [Function Syntax](/igorpro/programming/programming.md#function-syntax).

### Offset out of range {#offset-out-of-range}

The x and y offset parameters for the Tag and TextBox commands are in terms of percent of the width and height of the graph and therefore should be between -100 and 100.

### Out of memory {#out-of-memory}

There was not enough memory to complete the operation. See [Memory Management](/igorpro/igor-basics/using-igor.md#memory-management) for further information.

### P or X used outside of a wave assignment loop {#p-or-x-used-outside-of-a-wave-assignment-loop}

In Igor Pro 6.3 and later, code of the form:


```igor
wave[index]= <expression using p or x>
```

in a user-defined function generates a compile error. For example, this generates a compile error:


```igor
Function func()
    Wave wave0, wave1
    Variable index = 33
    wave0[index]= wave1[p]	// error is here
End
```

Prior to Igor 7, this error was generated only if rtGlobals=3 was in effect. In Igor 7 and later, it is always generated.

To fix the error, change the wave assignment code to this:


```igor
wave0[index]= wave1[index]
```

**Warning Instead of Error If rtGlobals!=3**

With CatchIllegalPandX, described below, set to 1, you can temporarily get by with a warning rather than an error.

When the code is in a procedure window that begins with #pragma rtGlobals=0, 1, or 2,  Igor posts a warning message instead of stopping compilation with an error. The warning message is:


```igor
WARNING:	P or X used outside of a wave assignment loop. For details execute:
               DisplayHelpTopic "P or X used outside of a wave assignment loop"
            Or execute
            SetIgorOption FuncOptimize, CatchIllegalPandX= 3
            and recompile to find and fix the error.
```

**CatchIllegalPandX**

You can control Igor's detection and reporting of this error using this command:


```igor
SetIgorOption FuncOptimize, CatchIllegalPandX=mode
```

mode=0	Turn off all detection and reporting

mode=1	Turn on the warning only (default in Igor Pro 6.3)

mode=2	Turn on the compile error if compiling with #pragma rtGlobals=3, otherwise a warning is reported

mode=3	Turn on the compile error always (default in Igor Pro 7 and later)

The effect of SetIgorOption lasts until Igor quits running.

**Background**

Since 2004, user-written function code that assigned an expression to a single point of a wave similar to this:


```igor
wave[index]= expression
```

compiled faster code than that used to implement a full wave assignment loop. In this case the usually varying p, q, r, s and x, y, z, t indices are not set and expressions that use them give unexpected results. So:


```igor
wOutput[index]= wInput[p]
```

would likely assign wInput[0] to wOutput[index] regardless of the value of index.

**See also**: [The rtGlobals Pragma](/igorpro/programming/programming.md#the-rtglobals-pragma)

### Parameter not declared {#parameter-not-declared}

The parameters to a macro must be declared in the macro as either Variable or String. The parameters to a function must be declared in the function as Variable, String or Wave. See [The Parameter List and Parameter Declarations](/igorpro/programming/macros.md#the-parameter-list-and-parameter-declarations).

### PICT version is not valid {#pict-version-is-not-valid}

This probably means that the picture is corrupted and can't be used.

### Safe save can't delete original file {#safe-save-can-t-delete-original-file}

As of Igor Pro 9.00, this error code is no longer used.

### Safe save can't delete temporary file {#safe-save-can-t-delete-temporary-file}

As of Igor Pro 9.00, this error code is no longer used.

### Safe save can't delete the previous version of the file {#safe-save-can-t-delete-the-previous-version-of-the-file}

During the save, Igor was unable to delete a previous backup (.prev) of the file being saved.

This error is usually caused by not having sufficient privileges to delete the original file.

You may be able to do a Save As or Save A Copy to a new file.

### Safe save can't finalize the save {#safe-save-can-t-finalize-the-save}

As of Igor Pro 9.00, this error code is no longer used.

### Safe save can't rename new file {#safe-save-can-t-rename-new-file}

During the save, the new data was successfully written to the original file.

An error occurred which prevented the renaming of original file using the new file name.

Your new file should be OK but has the wrong file name.

To save a backup, do a Save As or Save A Copy to a new file.

This error is usually caused by antivirus software that opens the file just as Igor is trying to rename it. If the problem persists, try disabling your antivirus software.

See [Experiment Save Errors](/igorpro/igor-basics/experiments-files-and-folders.md#experiment-save-errors) for further information.

### Safe save can't rename temporary file {#safe-save-can-t-rename-temporary-file}

As of Igor Pro 9.00, this error code is no longer used.

### Safe save can't rename the current version of the file {#safe-save-can-t-rename-the-current-version-of-the-file}

During the save, Igor was unable to rename the original version of the file by appending ".prev" to the file name. Igor does this to preserve the original data while saving a new version of an existing file.

This error is usually caused by not having sufficient privileges to rename the original file.

### Singular matrix or other numeric error {#singular-matrix-or-other-numeric-error}

See [Curve Fitting Troubleshooting](/igorpro/analysis/curve-fitting.md#curve-fitting-troubleshooting).

### Sorry, this operation is not allowed in a function {#sorry-this-operation-is-not-allowed-in-a-function}

See [Operations in Functions](/igorpro/programming/programming.md#operations-in-functions) and [The Execute Operation](/igorpro/programming/programming-techniques.md#the-execute-operation).

### Sorry, you can't call a macro from a function {#sorry-you-can-t-call-a-macro-from-a-function}

See [Operations in Functions](/igorpro/programming/programming.md#operations-in-functions) and [The Execute Operation](/igorpro/programming/programming-techniques.md#the-execute-operation).

### Text encoding conversion error {#text-encoding-conversion-error}

An attempt to convert text from one text encoding to another failed.

This can happen when converting text from a plain text file to UTF-8 for internal use in Igor because Igor's concept of the source text encoding is incorrect or because the file contains invalid text.

It may also happen when converting text from UTF-8 to the file text encoding during a save.

It may also happen when converting text wave text to UTF-8 for internal use.

There are many other circumstances when Igor has to convert text from one text encoding to another. See [Text Encodings](/igorpro/igor-basics/text-encodings.md) for details.

### TextEncoding pragma is invalid {#textencoding-pragma-is-invalid}

The format of a TextEncoding pragma is:

```igor
#pragma TextEncoding = "<text encoding name>"
```

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for details.

### TextEncoding pragma specifies unknown text encoding name {#textencoding-pragma-specifies-unknown-text-encoding-name}

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for the list of recognized text encoding names.

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for details about the TextEncoding pragma.

### The #include file specification is bad {#the-include-file-specification-is-bad}

The #include statement is missing a " or < character at the beginning or is missing a " or > character at the end. Also, the file specification may not exceed 511 bytes. See [The Include Statement](/igorpro/programming/programming-techniques.md#the-include-statement) for details.

### The binary table clipboard data is incompatible with this version of Igor {#the-binary-table-clipboard-data-is-incompatible-with-this-version-of-igor}

The Igor binary table clipboard format represents data that you copy to the clipboard in binary format. This format sometimes changes from one version of Igor to the next as features are added or changed, so you may get this error when copying in one version of Igor and pasting in another.

The Igor binary table clipboard format for IGOR64 is different from the format for IGOR32 for technical reasons so you cannot copy/paste between them.

A workaround for this error is to use the Data Browser Browse Expt button to load data from an Igor experiment file.

### The name of an HDF5 group to be created conflicts with an existing object in the file {#the-name-of-an-hdf5-group-to-be-created-conflicts-with-an-existing-object-in-the-file}

This error occurs when saving an HDF5 file when the name of a data folder in Igor is the same as the name of a wave, numeric variable, or string variable. Igor permits such name conflicts but HDF5 does not.

For example, in a new experiment, execute the following:


```igor
Make/O root:test
NewDataFolder root:test						// OK in Igor but creates name conflict in HDF5
SaveExperiment/C/F={2,"",0}/P=IgorUserFiles as "Test.h5xp"	// Save as HDF5 packed experiment file
```

This throws an error because HDF5 does not allow a group to have the same name as a dataset. (You can save this as a regular packed experiment file [.pxp file] but not as an HDF5 packed experiment file.)

The solution is to rename the Igor wave (or numeric variable or string variable) to eliminate the name conflict and then retry the save. Continuing the example:


```igor
Rename root:test, testWave					// Eliminate name conflict
SaveExperiment/C/F={2,"",0}/P=IgorUserFiles as "Test.h5xp"	// Save as HDF5 packed experiment file
```

Now no error is thrown.

You could also solve the problem by renaming the data folder.

This problem affects saving HDF5 packed experiments manually or using the [SaveExperiment](/igorpro/commands/saveexperiment.md) operation and also affects the [HDF5SaveGroup](/igorpro/commands/hdf5savegroup.md) operation.

For further explanation, see [Object Name Conflicts and HDF5 Files](/igorpro/igor-basics/using-igor.md#object-name-conflicts-and-hdf5-files).

### The text encoding specified by the TextEncoding pragma is not valid for the text in the file {#the-text-encoding-specified-by-the-textencoding-pragma-is-not-valid-for-the-text-in-the-file}

The text in the file contains byte sequences that are illegal in the text encoding specified by the TextEncoding pragma. Change the TextEncoding pragma to the correct text encoding. If you don't know what this means you should consult with the author of the procedure file.

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for the list of recognized text encoding names.

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for details about the TextEncoding pragma.

### The TextEncoding pragma may appear only once in a procedure file {#the-textencoding-pragma-may-appear-only-once-in-a-procedure-file}

Remove the extraneous TextEncoding pragma.

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for details about the TextEncoding pragma.

### That cursor is not on top graph {#that-cursor-is-not-on-top-graph}

There are two cursors named A and B. Operations which access a cursor act on the top graph.

### The first TU location is AFTER the second TU location {#the-first-tu-location-is-after-the-second-tu-location}

This is due to a bug in an XOP. Please notify the XOP programmer. If possible, find a recipe for reproducing the bug.

### The included procedure file "^1" is out of date and needs to be updated {#the-included-procedure-file-1-is-out-of-date-and-needs-to-be-updated}

This occurs when a procedure window includes another procedure file and requires a later version of the included file. For updating WaveMetrics-supplied procedure files, see [Technical Support](/igorpro/igor-basics/using-igor.md#technical-support).

### The PICT does not contain Igor object information {#the-pict-does-not-contain-igor-object-information}

Pictures of Igor graphs, tables and layouts only contain special information that allow Igor to update them in notebooks.

### The TU location character position is out of range {#the-tu-location-character-position-is-out-of-range}

This is due to a bug in an XOP. Please notify the XOP programmer. If possible, find a recipe for reproducing the bug.

### The TU paragraph is out of range {#the-tu-paragraph-is-out-of-range}

This is due to a bug in an XOP. Please notify the XOP programmer. If possible, find a recipe for reproducing the bug.

### The UTF-16 and UTF-32 text encodings are not supported for procedure files. Convert the file to UTF-8. {#the-utf-16-and-utf-32-text-encodings-are-not-supported-for-procedure-files-convert-the-file-to-utf-8}

Igor does not support UTF-16 and UTF-32 for procedure files. You can convert a file to UTF-8 in another program. You can convert it in Igor by opening the procedure file as an Igor notebook (File->Open->Notebook). Then choose Notebook->Select Text Encoding. Convert to UTF-8, save the file, and reopen as a procedure file.

See [Text Encodings](/igorpro/igor-basics/text-encodings.md) for background information.

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for the list of recognized text encoding names.

### There is a conflict between the TextEncoding pragma and the file's text encoding {#there-is-a-conflict-between-the-textencoding-pragma-and-the-file-s-text-encoding}

The procedure file was opened using one text encoding and then a TextEncoding pragma was added or edited using a different text encoding.

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for the list of recognized text encoding names.

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for details about the TextEncoding pragma.

### There is no open file with this reference number {#there-is-no-open-file-with-this-reference-number}

See [Open](/igorpro/commands/open.md)ations[Open].

### There must be two free dimensions: one vertical (-2) and one horizontal (-3) {#there-must-be-two-free-dimensions-one-vertical-2-and-one-horizontal-3}

The ModifyElements operation needs to know which wave element to display along the table vertical dimension and which wave element to display along the table horizontal dimension.

See [ModifyTable Elements Command](/igorpro/igor-basics/tables.md#modifytable-elements-command).

### This function or operation is not available in user functions {#this-function-or-operation-is-not-available-in-user-functions}

See [Operations in Functions](/igorpro/programming/programming.md#operations-in-functions) and [The Execute Operation](/igorpro/programming/programming-techniques.md#the-execute-operation).

### This is not a packed Igor experiment file {#this-is-not-a-packed-igor-experiment-file}

This error occurs if you use the LoadData operation without the /D flag and tell it to load a file that is not a packed Igor experiment file. Either change the file or use the /D flag, to load unpacked data files from a directory.

### To invoke a built-in function you must print or assign the result {#to-invoke-a-built-in-function-you-must-print-or-assign-the-result}

For example:


```igor
area(wave0)							// ERROR
Print area(wave0)						// OK
Variable theArea = area(wave0)		// OK
```

### Too many parameters on command line {#too-many-parameters-on-command-line}

Certain commands like Duplicate and Remove can handle no more than 100 waves names in their parameter lists.

### Unable to open the Excel .xlsx or .xlsm file {#unable-to-open-the-excel-xlsx-or-xlsm-file}

Among other reasons for this error, it occurs if the file you are trying to load is password-protected. XLLoadWave cannot load password-protected Excel files.

### Unexpected end of macro definition {#unexpected-end-of-macro-definition}

Igor hit the end of a macro while a loop or control structure was still open.

Look for an if without an endif, an iterate without a loop, or a do without a while.

### Unknown keyword in Igor Text file {#unknown-keyword-in-igor-text-file}

See [Loading Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-igor-text-files).

### Use '/N=number' or '/N=(expression)' (assuming flag 'N'). If multiple dimensions used (i.e., Make/N), use /N=(n1,n2...) {#use-n-number-or-n-expression-assuming-flag-n-if-multiple-dimensions-used-i-e-make-n-use-n-n1-n2}

In an operation flag such as /N=n, if n is anything other than a literal number, you need to use parentheses.

If the operation and flag might specify multiple dimensions, use parentheses. For example:


```igor
Function ExampleFunc(dim1, dim2, w)
    Variable dim1, dim2
    Wave w

    Redimension/N=5 w				// OK- it's a literal number
    Redimension/N=(dim1) w			// variable name requires parentheses
    Redimension/N=(dim1, dim2) w	// multiple dimensions - use parentheses
    Redimension/N=(5, 10) w			// multiple dimensions - use parentheses
End
```

### User function does not have required form {#user-function-does-not-have-required-form}

A user function that is used for curve fitting must have exactly two parameters. The first is the coefficient wave containing your initial guesses. The second is the independent variable. See [User-Defined Fitting Functions](/igorpro/analysis/curve-fitting.md#user-defined-fitting-functions) for details.

### Wave length must be power of 2 for this operation {#wave-length-must-be-power-of-2-for-this-operation}

See [Fourier Transforms](/igorpro/analysis/signal-processing.md#fourier-transforms).

### WAVES declaration error: Each multidimensional wave must be in its own data block {#waves-declaration-error-each-multidimensional-wave-must-be-in-its-own-data-block}

See [Loading Multidimensional Waves From Igor Text Files](/igorpro/data/importing-and-exporting-data.md#loading-multidimensional-waves-from-igor-text-files).

### WAVES declaration error: Improper specification of wave dimension sizes {#waves-declaration-error-improper-specification-of-wave-dimension-sizes}

In an Igor text file, you can specify the dimensionality of the wave being loaded using the /N=(\<dimensions\>) flag after the WAVES keyword. The parentheses are required. Examples: /N=(100) (for a 1D wave, optional), /N=(25, 25) (for a 2D wave, required).

### While with no do or other flow control mismatch {#while-with-no-do-or-other-flow-control-mismatch}

See [If-Else-Endif Statements](/igorpro/programming/programming.md#if-else-endif-statements) or [Loops](/igorpro/programming/programming.md#loops).

### Windows OS Error - Access denied {#windows-os-error-access-denied}

This typically happens because you don't have write access to the file or to the folder containing it. Try doing a Save As or Save A Copy to save to your home folder.

See [Experiment Save Errors](/igorpro/igor-basics/experiments-files-and-folders.md#experiment-save-errors) for troubleshooting information.

### Wrong format for dependency formula {#wrong-format-for-dependency-formula}

The destination of a dependency formula must be a wave, a global variable or a global string. See [Dependencies](/igorpro/programming/dependencies.md).

### XOP is incompatible with system software or hardware {#xop-is-incompatible-with-system-software-or-hardware}

Igor tried to load an XOP that requires hardware that is not available in the current system. Missing hardware might be a math coprocessor or a memory management unit. The XOP may require a later version of system software.

### XOP is incompatible with this version of Igor {#xop-is-incompatible-with-this-version-of-igor}

Igor tried to load an XOP file that was compiled for an earlier version of Igor. To use this XOP, you need to recompile it with the appropriate Igor XOP support files.

### You don't have sufficient privileges to complete the requested operation {#you-don-t-have-sufficient-privileges-to-complete-the-requested-operation}

This typically happens because you don't have write access to the file or to the folder containing it. Try doing a Save As or Save A Copy to save to your home folder.

See [Experiment Save Errors](/igorpro/igor-basics/experiments-files-and-folders.md#experiment-save-errors) for troubleshooting information.

### You need a coefficients wave for fitting to a user-defined function {#you-need-a-coefficients-wave-for-fitting-to-a-user-defined-function}

See [User-Defined Fitting Functions](/igorpro/analysis/curve-fitting.md#user-defined-fitting-functions).