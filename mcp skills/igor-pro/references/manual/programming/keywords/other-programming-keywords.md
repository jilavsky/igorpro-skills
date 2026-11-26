---
description: "These keywords are used for various purposes when writing Igor procedures."
slug: /programming/keywords/other-programming-keywords
---

These keywords are used for various purposes when writing Igor procedures.

<div className="command-signature">

## <strong>#define</strong> {#define}

</div>

```igor
#define symbol
```

A #define statement is a conditional compilation directive that defines a *symbol* for use only with #ifdef or ifndef expressions. [#undef](/igorpro/programming/keywords/other-programming-keywords.md#undef) removes the definition.

### *Details* {#details}
The defined *symbol* exists only in the file where it is defined; the only exception is in the main procedure window where the scope covers all other procedures except independent modules. See [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation) for information on defining a global *symbol*.

#define cannot be combined inline with other conditional compilation directives.

### *See Also* {#see-also}
The [#undef](/igorpro/programming/keywords/other-programming-keywords.md#undef), [#ifdef-#endif](/igorpro/programming/keywords/other-programming-keywords.md#ifdef-endif), and [#ifndef-#endif](/igorpro/programming/keywords/other-programming-keywords.md#ifndef-endif) statements

[Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation)

<div className="command-signature">

## <strong>#if-#elif-#endif</strong> {#if-elif-endif}

</div>

```igor
#if expression1
	<TRUE part 1>		// Compile if condition 1 is TRUE
#elif expression2
	<TRUE part 2>		// Compile if condition 2 is TRUE and condition 1 is FALSE
[...]
[#else
	<FALSE part>]		// Optionally compile if all conditions are FALSE
#endif
```

In a #if-#elif-#endif conditional compilation statement, when an expression evaluates as TRUE (absolute value > 0.5), then only code corresponding to the TRUE part of that expression is compiled, and then the conditional statement is exited. If all expressions evaluate as FALSE (zero) then FALSE part is compiled when present.

### *Details* {#if-elif-endif-details}
Conditional compiler directives must be either entirely outside or inside function definitions; they cannot straddle a function fragment. Conditionals cannot be used within Macros.

The expressions should involve only built-in functions and literal strings and numbers such as:


```igor
#if exists("PanelResolution") != 3      // if built-in function from Igor 7+ is missing
	Function PanelResolution(panelName)   // implement an Igor 6 or earlier equivalent
		String panelName
		return 72
	End
#endif
```

Constants and StrConstants may not be used in the expression.

The expressions should not reference user-defined macros or functions in a different independent module ("IM"), such as in the following scenario:


```igor
// This code must be in its own procedure file and not in the built-in procedure file:
#pragma IndependentModule = myIM

#if exists("ProcGlobal#test") == 6      // NO: when compiling myIM, code in other IMs may not be compiled yet.
Function myFunction()                   // Won't compile because #if expression will be false
    Execute/Q/Z "ProcGlobal#test()"     // Only ProcGlobal can call into another IM; another IM can't directly call ProcGlobal
End
#endif
// Code in the built-in Procedure window:
Function test()
	Print "testing"
End
```

Running myIM#myFunction() on the command line will fail with a "unknown/inappropriate name or symbol" error.

That is because ProcGlobal procedures (those **not** in procedure windows with a #pragma IndependentModule statement) are compiled after all procedure windows **with** a #pragma IndependentModule statement.

### *See Also* {#if-elif-endif-see-also}
[Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation), [Independent Modules](/igorpro/advanced-topics.md#independent-modules), [Constants](/igorpro/programming/programming.md#constants), [IgorVersion](/igorpro/commands/igorversion.md), [exists](/igorpro/commands/exists.md)

<div className="command-signature">

## <strong>#if-#endif</strong> {#if-endif}

</div>

```igor
#if expression
	<TRUE part>     // Compile if condition is TRUE
[#else
	<FALSE part>]   // Optionally compile if condition is FALSE
#endif
```

A #if-#endif conditional compilation statement evaluates expression. If expression is TRUE (absolute value > 0.5) then the code in TRUE part is compiled, or if FALSE (zero) then the optional FALSE part is compiled.

### *Details* {#if-endif-details}
Conditional compiler directives must be either entirely outside or inside function definitions; they cannot straddle a function fragment. Conditionals cannot be used within Macros.

### *See Also* {#if-endif-see-also}
[Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation)

<div className="command-signature">

## <strong>#ifdef-#endif</strong> {#ifdef-endif}

</div>

```igor
#ifdef symbol
	<TRUE part>         // Compile if symbol is defined
[#else
	<FALSE part>]       // Optionally compile if no symbol
#endif
```

A #ifdef-#endif conditional compilation statement evaluates symbol. When symbol is defined the code in TRUE part is compiled, or if undefined then the optional FALSE part is compiled.

### *Details* {#ifdef-endif-details}
Conditional compiler directives must be either entirely outside or inside function definitions; they cannot straddle a function fragment. Conditionals cannot be used within Macros.

*symbol* must be defined before the conditional with [#define](/igorpro/programming/keywords/other-programming-keywords.md#define).

### *See Also* {#ifdef-endif-see-also}
[#define](/igorpro/programming/keywords/other-programming-keywords.md#define), [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation)

<div className="command-signature">

## <strong>#ifndef-#endif</strong> {#ifndef-endif}

</div>

```igor
#ifndef symbol
	<TRUE part>         // Compile if symbol is undefined
[#else
	<FALSE part>]       // Optionally compile if symbol defined
#endif
```

A #ifndef-#endif conditional compilation statement evaluates symbol. When symbol is undefined the code in TRUE part is compiled, or if defined then the optional FALSE part is compiled.

### *Details* {#ifndef-endif-details}
Conditional compiler directives must be either entirely outside or inside function definitions; they cannot straddle a function fragment. Conditionals cannot be used within Macros.

*symbol* must be defined before the conditional with [#define](/igorpro/programming/keywords/other-programming-keywords.md#define).

### *See Also* {#ifndef-endif-see-also}
[#define](/igorpro/programming/keywords/other-programming-keywords.md#define), [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation)

<div className="command-signature">

## <strong>#include</strong> {#include}

</div>

```igor
#include "file spec" or <file spec>
```

A #include statement in a procedure file automatically opens another procedure file. You should use #include in any procedure file that you write if it requires that another procedure file be open. A #include statement must always appear flush against the left margin in a procedure window.

### *Parameters* {#parameters}
The ".ipf" extension must be omitted from both "*file spec*" and <*file spec*>.

The <*file spec*> syntax is used to include a WaveMetrics procedure file in "Igor Pro Folder/WaveMetrics Procedures". *file spec* is the name of the procedure file without the extension.

The "*file spec*" syntax is used to include a user procedure file typically in "Igor Pro User Files/User Procedures". If *file spec* is the name of or a partial path to the file, Igor interprets it as relative to the "User Procedures" folder. If *file spec* is a full path then it specifies the exact path to the file without the extension.

### *See Also* {#include-see-also}
[The Include Statement](/igorpro/programming/programming-techniques.md#the-include-statement), [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files), [Turning the Included File's Menus Off](/igorpro/programming/programming-techniques.md#turning-the-included-file-s-menus-off)

<div className="command-signature">

## <strong>#pragma</strong> {#pragma}

</div>

#pragma introduces a compiler directive, which is a message to the Igor procedure compiler. A #pragma statement must always appear flush against the left margin in a procedure window.

Igor ignores unknown pragmas such as pragmas introduced in later versions of the program.

Currently, Igor supports the following pragmas:


```igor
#pragma rtGlobals = value
#pragma version = versionNumber
#pragma IgorVersion = versionNumber
#pragma hide = value
#pragma ModuleName = name
#pragma IndependentModule = name
#pragma rtFunctionErrors = value
#pragma TextEncoding = "textEncodingName"                           // Added in Igor Pro 7.00
#pragma DefaultTab = {<mode>,<width in points>,<width in spaces>}   // Added in Igor Pro 9.00
```

### *See Also* {#pragma-see-also}
[Pragmas](/igorpro/programming/programming.md#pragmas), [The rtGlobals Pragma](/igorpro/programming/programming.md#the-rtglobals-pragma), [The version Pragma](/igorpro/programming/programming.md#the-version-pragma), [The IgorVersion Pragma](/igorpro/programming/programming.md#the-igorversion-pragma), [The hide Pragma](/igorpro/programming/programming.md#the-hide-pragma), [The ModuleName Pragma](/igorpro/programming/programming.md#the-modulename-pragma), [The IndependentModule Pragma](/igorpro/programming/programming.md#the-independentmodule-pragma), [The rtFunctionErrors Pragma](/igorpro/programming/programming.md#the-rtfunctionerrors-pragma), [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma), [The DefaultTab Pragma For Procedure Files](/igorpro/programming/procedure-windows.md#the-defaulttab-pragma-for-procedure-files)

<div className="command-signature">

## <strong>#undef</strong> {#undef}

</div>

```igor
#undef symbol
```

A #undef statement removes a nonglobal *symbol* created previously by #define. See [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation) for information on undefining a global *symbol*.

### *See Also* {#undef-see-also}
[#define](/igorpro/programming/keywords/other-programming-keywords.md#define), [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation)

<div className="command-signature">

## <strong>Constant</strong> {#constant}

</div>

```igor
Constant kName = literalNumber
Constant/C kName = (literalNumberReal, literalNumberImag )
```

The Constant declaration defines the number *literalNumber* under the name *kName* for use by other code, such as in a switch construct.

The complex form, using the /C flag to create a complex constant, requires Igor Pro 7.00 or later.

### *See Also* {#constant-see-also}
See the [Strconstant](/igorpro/programming/keywords/other-programming-keywords.md#strconstant) keyword for string types, as well as the [Constant Type](/igorpro/programming/commands.md#constant-type) and [Switch Statements](/igorpro/programming/programming.md#switch-statements) sections.

<div className="command-signature">

## <strong>DefaultTab</strong> {#defaulttab}

</div>

```igor
#pragma DefaultTab={mode,widthInPoints,widthInSpaces}
```

The DefaultTab pragma allows you to specify default tab settings by entering a pragma statement in a procedure file. Specifying tab widths in spaces rather than points provides better results if the procedure window font or font size is changed.

The DefaultTab pragma was added in Igor Pro 9.00. It is ignored by earlier Igor versions.

See [Procedure Window Default Tabs](/igorpro/programming/procedure-windows.md#procedure-window-default-tabs) for details.

<div className="command-signature">

## <strong>DoPrompt</strong>  [/HELP=<em>helpStr</em> ] <em>dialogTitleStr</em>, <em>variable</em>  [, <em>variable</em> ]... {#doprompt}

</div>

The DoPrompt command in a function invokes the simple input dialog. A DoPrompt specifies the title for the simple input dialog and which input variables are to be included in the dialog.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/HELP = *helpStr*</span> | Sets the help topic or help text that appears when the dialog's Help button is pressed. |
|  | *helpStr* can be a help topic and subtopic such as is used by [DisplayHelpTopic](/igorpro/commands/displayhelptopic.md)/K=1 helpStr, or it can be text (255 chars max) that is displayed in a subdialog just as if [DoAlert](/igorpro/commands/doalert.md) 0, *helpStr* had been called, or *helpStr* can be "" to remove the Help button. |

### *Parameters* {#doprompt-parameters}
*variable* is the name of a dialog input variable, which can be real or complex numeric local variable or local string variable, defined by a Prompt statement. You can specify as many as 10 variables.

*dialogTitleStr* is a string or string expression containing the text for the title of the simple input dialog.

### *Details* {#doprompt-details}
Prompt statements are required to define what variables are to be used and the text for any string expression to accompany or describe the input variable in the dialog. When a DoPrompt variable is missing a Prompt statement, you will get a compilation error. Pop-up menu string data cannot be continued across multiple lines as can be done using Prompt in macros. See [Prompt](/igorpro/programming/keywords/other-programming-keywords.md#prompt) for further usage details.

Prompt statements for the input variables used by DoPrompt must come before the DoPrompt statement itself, otherwise, they may be used anywhere within the body of a function. The variables are not required to be input parameters for the function (as is the case for Prompt in macros) and they may be declared within the funtion body. DoPrompts can accept as many as 10 variables.

Functions can use multiple DoPrompt statements, and Prompt statements can be reused or redefined.

When the user clicks the Cancel button, any new input parameter values are not stored in the variables.


|  |  |
| --- | --- |
| DoPrompt sets the variable V_flag as follows: |  |
| V_flag= |<table class="nested-table"><tbody><tr><td>0:</td><td>Continue clicked.</td></tr><tr><td>1:</td><td>Cancel clicked.</td></tr></tbody></table>

### *See Also* {#doprompt-see-also}
[The Simple Input Dialog](/igorpro/programming/interacting-with-the-user.md#the-simple-input-dialog), [Prompt](/igorpro/programming/keywords/other-programming-keywords.md#prompt), [DisplayHelpTopic](/igorpro/commands/displayhelptopic.md)

<div className="command-signature">

## <strong>GalleryGlobal</strong> {#galleryglobal}

</div>

```igor
GalleryGlobal#pictureName
```

The GalleryGlobal keyword is used in an independent module to reference a picture in the global picture gallery which you can view by choosing Misc→Pictures.

### *See Also* {#galleryglobal-see-also}
[Independent Modules and Pictures](/igorpro/advanced-topics.md#independent-modules-and-pictures)

<div className="command-signature">

## <strong>hide</strong> {#hide}

</div>

```igor
#pragma hide=value
```

The hide pragma allows you to make a procedure file invisible.

### *See Also* {#hide-see-also}
[#pragma](/igorpro/programming/keywords/other-programming-keywords.md#pragma), [The hide Pragma](/igorpro/programming/programming.md#the-hide-pragma)

<div className="command-signature">

## <strong>IgorVersion</strong> {#igorversion}

</div>

```igor
#pragma IgorVersion=versNum
```

When a procedure file contains the directive, `#pragma IgorVersion=versNum`, an error will be generated if *versNum* is greater than the current Igor Pro version number. It prevents procedures that use new features added in later versions from running under older versions of Igor in which these features are missing. However, this version check is limited because it does not work with versions of Igor older than 4.0.

### *See Also* {#igorversion-see-also}
[#pragma](/igorpro/programming/keywords/other-programming-keywords.md#pragma), [The IgorVersion Pragma](/igorpro/programming/programming.md#the-igorversion-pragma)

<div className="command-signature">

## <strong>IndependentModule</strong> {#independentmodule}

</div>

```igor
#pragma IndependentModule=imName
```

The IndependentModule pragma designates groups of one or more procedure files that are compiled and linked separately. Once compiled and linked, the code remains in place and is usable even though other procedures may fail to compile. This allows functioning control panels and menus to continue to work regardless of user programming errors.

### *See Also* {#independentmodule-see-also}
[#pragma](/igorpro/programming/keywords/other-programming-keywords.md#pragma), [Independent Modules](/igorpro/advanced-topics.md#independent-modules), [The IndependentModule Pragma](/igorpro/programming/programming.md#the-independentmodule-pragma)

<div className="command-signature">

## <strong>Menu</strong> {#menu}

</div>

```igor
Menu menuNameStr [, hideable, dynamic, contextualmenu]
```

The Menu keyword introduces a menu definition. You can use this to create your own menu, or to add items to a built-in Igor menu.

Use the optional *hideable* keyword to make the menu hideable using [HideIgorMenus](/igorpro/commands/hideigormenus.md).

Use the optional dynamic keyword to cause Igor to re-evaluate the menu definition when the menu is used. This is helpful when the menu item text is provided by a user-defined function. See [Dynamic Menu Items](/igorpro/user-interface/user-defined-menus.md#dynamic-menu-items).

Use the optional contextualmenu keyword for menus invoked by [PopupContextualMenu](/igorpro/commands/popupcontextualmenu.md)/N.

See [User-defined Menus](/igorpro/user-interface/user-defined-menus.md) for further information.

<div className="command-signature">

## <strong>ModuleName</strong> {#modulename}

</div>

```igor
#pragma ModuleName=modName
```

The ModuleName pragma assigns a name, which must be unique among all procedure files, to a procedure file so that you can use static functions and Proc Pictures in a global context, such as in the action procedure of a control or on the Command Line.

Using the ModuleName pragma involves at least two steps. First, within the procedure file assign it a name using `#pragma ModuleName=modName`, and then access objects in the named file by preceding the object name with the name of the module and the # character, such as or example: `ModName#StatFuncName()`.

### *See Also* {#modulename-see-also}
[#pragma](/igorpro/programming/keywords/other-programming-keywords.md#pragma), [Regular Modules](/igorpro/advanced-topics.md#regular-modules)

<div className="command-signature">

## <strong>MultiThread</strong> {#multithread}

</div>

```igor
MultiThread [/NT=numThreads] wave = expression
```

In user-defined functions, the MultiThread keyword can be inserted in front of wave assignment statements to speed up execution on multiprocessor computer systems.

:::caution
Misuse of this keyword can result in a performance penalty or even a crash. Be sure to read [Automatic Parallel Processing with MultiThread](/igorpro/advanced-topics.md#automatic-parallel-processing-with-multithread) before using MultiThread.
:::

The expression must be thread-safe. This means that if it calls a function, the function must be thread-safe. This goes for both built-in and user-defined functions.

Not all built-in functions are thread-safe. Use the Command Help tab in the Igor Help Browser to see which functions are thread-safe.

User-defined functions are thread-safe if they are defined using the [ThreadSafe](/igorpro/programming/keywords/other-programming-keywords.md#threadsafe) keyword. See [ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions) for details.

You can specify the number of threads using the /NT flag. The default value, which takes effect if you omit /NT or specify /NT=0, uses the number returned by [ThreadProcessorCount](/igorpro/commands/threadprocessorcount.md). /NT=1 specifies a single thread and is equivalent to omitting the MultiThread keyword; you might want to turn off threading to avoid its overhead when the wave has few points. *numThreads* values greater than one specify the desired number of threads to be used. Igor may use fewer threads depending on how it is able to partition the task. The /NT flag was added in Igor Pro 8.00.

For more complex multithreading applications, see [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking).

### *See Also* {#multithread-see-also}
[Automatic Parallel Processing with MultiThread](/igorpro/advanced-topics.md#automatic-parallel-processing-with-multithread)

[Waveform Arithmetic and Assignment](/igorpro/igor-basics/waves.md#waveform-arithmetic-and-assignment)

### *Demo* {#demo}
[Open MultiThread Mandelbrot Demo Experiment](#igor-pxp/Examples/Programming/MultiThreadMandelbrot.pxp)

<div className="command-signature">

## <strong>Override</strong> {#override}

</div>

```igor
Override Constant objectName = newNumber
Override StrConstant objectName = "newStringValue"
Override Function funcName()
```

The Override keyword redefines a constant, strconstant, or user function. The *objectName* or *funcName* must be the same as the name of the original object or function that is being redefined. The override must be defined before the target object appears in the compile sequence.

### *See Also* {#override-see-also}
[Function Overrides](/igorpro/programming/programming.md#function-overrides), [Constant Type](/igorpro/programming/commands.md#constant-type)

<div className="command-signature">

## <strong>Popup</strong>  <em>menuList</em> {#popup}

</div>

The Popup keyword is used with Prompt statements in Functions and Macros. It indicates that you want a pop-up menu instead of the normal text entry item in a DoPrompt simple input dialog (or a Macro's missing parameter dialog (archaic)). *menuList* is a string expression containing a list of items, separated by semicolons, that are to appear in the pop-up menu. *menuList* is limited to 255 bytes.

Pop-up menus accept both numeric and string parameters. For numeric parameters, the number of the item selected is placed in a variable. Numbering starts from one. For string parameters, the selected item's text is placed in a string variable.

### *See Also* {#popup-see-also}
[Prompt](/igorpro/programming/keywords/other-programming-keywords.md#prompt), [DoPrompt](/igorpro/programming/keywords/other-programming-keywords.md#doprompt), [Pop-Up Menus in Simple Dialogs](/igorpro/programming/interacting-with-the-user.md#pop-up-menus-in-simple-dialogs)

See [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ImageNameList](/igorpro/commands/imagenamelist.md), [FontList](/igorpro/commands/fontlist.md), [MacroList](/igorpro/commands/macrolist.md), [FunctionList](/igorpro/commands/functionlist.md), [StringList](/igorpro/commands/stringlist.md), and [VariableList](/igorpro/commands/variablelist.md) for ways to generate lists of Igor objects.

<div className="command-signature">

## <strong>ProcGlobal</strong> {#procglobal}

</div>

```igor
ProcGlobal#procPictureName
```

The ProcGlobal keyword is used with Proc Pictures to avoid possible naming conflicts with any other global pictures in the experiment. When you add a picture to an experiment using the Pictures dialog, such a picture is global in scope and may potentially have the same name as a Proc Picture. When a Proc Picture is global (and only then), you should use the ProcGlobal keyword to make sure that the Proc Picture is used with your code and to avoid confusion with pictures in the Pictures dialog.

### *See Also* {#procglobal-see-also}
[Proc Pictures](/igorpro/programming/programming.md#proc-pictures)

<div className="command-signature">

## <strong>Prompt</strong>  <em>variableName</em>, <em>titleStr</em>  [, <em>popup</em>, <em>menuListStr</em> ] {#prompt}

</div>

The Prompt statement is used in functions for the simple input dialog and in macros for the missing parameter dialog. Prompt supplies text to describe *variableName* to the user, and optionally provides a pop-up menu of choices for the value of *variableName*.

### *Parameters* {#prompt-parameters}
*variableName* is the name of a macro input parameter or function variable.

*titleStr* is a string or string expression containing the text to present in the dialog to describe what *variableName* is.

The optional keyword "popup" is used to provide a pop-up list of choices for the values of *variableName*. If popup is used, then *menuListStr* is required.

*menuListStr* is a string or string expression that contains a semicolon-separated list of choices for the value of *variableName*. If *variableName* is a string, choosing from this list will set the string to the selection. If it is a numeric variable, then it is set to the item number of the selection (if the first item is selected, the numeric variable is set to 1, etc.).

### *Details* {#prompt-details}
In macros, there must be a blank line after the set of input parameter declarations and prompt statements and there must not be any blank lines within the set.

In user-defined functions, Prompt may be used anywhere within the body of the function, but must precede any DoPrompt that uses the Prompt variable.

*menuListStr* may be continued on succeeding lines only in macros, as long as no comment is appended to the Prompt line. The additional lines should start with a semicolon, and are appended to the *menuListStrs* on preceding lines.

### *See Also* {#prompt-see-also}
For use in user-defined functions, see [The Simple Input Dialog](/igorpro/programming/interacting-with-the-user.md#the-simple-input-dialog).

For use in macros, see [The Missing Parameter Dialog](/igorpro/programming/macros.md#the-missing-parameter-dialog).

For use in functions and macros, see the [DoPrompt](/igorpro/programming/keywords/other-programming-keywords.md#doprompt) and [popup](/igorpro/programming/keywords/other-programming-keywords.md#popup) keywords.

<div className="command-signature">

## <strong>root</strong> {#root}

</div>

```igor
root[:dataFolderName [:dataFolderName [:...]]][:objectName ]
```

Igor's data folder hierarchy starts with the root folder as its basis. The root data folder always exists and it contains all other objects (waves, variables, strings, and data folders). By default, the root data folder is the current data folder when Igor starts a new experiment. In commands, root is used as part of a path specifying the location of a data object in the folder hierarchy.

### *See also* {#root-see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)

<div className="command-signature">

## <strong>rtGlobals</strong> {#rtglobals}

</div>

```igor
#pragma rtglobals = 0, 1, 2 or 3
```

`#pragma rtglobals=<n>` is a compiler directive that controls compiler and runtime behaviors for the procedure file in which it appears.

This statement must be flush against the left edge of the procedure file with no indentation. It is usually placed at the top of the file.

`#pragma rtglobals=0` turns off runtime creation of globals. This is obsolete.

`#pragma rtglobals=1` is a directive that turns on runtime lookup of globals. This is the default behavior if #pragma rtGlobals is omitted from a given procedure file.

`#pragma rtglobals=2` turns off compatibility mode. This is mostly obsolete. See [Legacy Code Issues](/igorpro/programming/programming.md#legacy-code-issues) for details.

`#pragma rtglobals=3` turns on runtime lookup of globals, strict wave reference mode and wave index bounds checking.

rtGlobals=3 is recommended.

See [The rtGlobals Pragma](/igorpro/programming/programming.md#the-rtglobals-pragma) for a detailed explanation of rtGlobals.

<div className="command-signature">

## <strong>Static</strong> {#static}

</div>


```igor
Static Constant objectName = newNumber
Static StrConstant objectName = "newStringValue"
Static Function funcName()
Static Structure structureName
Static Picture pictName
```

The Static keyword declaration specifies that a constant, user-defined function, structure, or Proc Picture is local to the procedure file in which it appears. Static objects can only be used by other functions; they cannot be accessed from macros; they cannot be accessed from other procedure files or from the command line.

### *See Also* {#static-see-also}
[Static Functions](/igorpro/programming/programming.md#static-functions), [Proc Pictures](/igorpro/programming/programming.md#proc-pictures), [Constants](/igorpro/programming/programming.md#constants)

<div className="command-signature">

## <strong>Strconstant</strong> {#strconstant}

</div>

```igor
Strconstant ksName ="literal string "
```

The Strconstant declaration defines the string *literal string* under the name *ksName* for use by other code, such as in a switch construct.

### *See Also* {#strconstant-see-also}
See the [Constant](/igorpro/programming/keywords/other-programming-keywords.md#constant) keyword for numeric types, as well as the [Constant Type](/igorpro/programming/commands.md#constant-type) and [Switch Statements](/igorpro/programming/programming.md#switch-statements) sections.

<div className="command-signature">

## <strong>Submenu</strong> {#submenu}

</div>

The Submenu keyword introduces a submenu definition. It is used inside a Menu definition. See [User-defined Menus](/igorpro/user-interface/user-defined-menus.md) for further information.

<div className="command-signature">

## <strong>TextEncoding</strong> {#textencoding}

</div>

```igor
#pragma TextEncoding = "<text encoding name>"
```

#pragma TextEncoding is a compiler directive that tells Igor the text encoding used by a procedure file. Igor needs to know this in order to correctly interpret non-ASCII characters in the file. We recommend that you add a TextEncoding pragma to your procedure files.

All new procedure files should use the UTF-8 text encoding:


```igor
#pragma TextEncoding = "UTF-8"
```

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of accepted text encoding names.

This statement must be flush against the left edge of the procedure file with no indentation. It is usually placed at or near the top of the file.

The TextEncoding pragma was added in Igor Pro 7.00 and is ignored by earlier versions.

See [The TextEncoding Pragma](/igorpro/programming/programming.md#the-textencoding-pragma) for further explanation.

<div className="command-signature">

## <strong>ThreadSafe</strong> {#threadsafe}

</div>

```igor
ThreadSafe Function funcName()
```

The ThreadSafe keyword declaration specifies that a user function can be used for preemptive multitasking background tasks on multiprocessor computer systems.

A ThreadSafe function is one that can operate correctly during simultaneous execution by multiple threads. Such functions are generally limited to numeric or utility functions. Functions that access windows are not ThreadSafe. To determine if an operation is ThreadSafe, use the Command Help tab of the Help Browser and choose ThreadSafe from the pop-up menu.

ThreadSafe functions can call other ThreadSafe functions but may not call non-ThreadSafe functions. Non-ThreadSafe functions can call ThreadSafe functions.

### *See Also* {#threadsafe-see-also}
[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)

<div className="command-signature">

## <strong>version</strong> {#version}

</div>

```igor
#pragma version=versNum
```

When the user invokes the File Information dialog, the version pragma provides file version information, which is displayed next to the file name in the dialog. This line must not be indented and must appear in the first 50 lines of the file. See [Procedure File Version Information](/igorpro/programming/programming-techniques.md#procedure-file-version-information).

### *See Also* {#version-see-also}
[#pragma](/igorpro/programming/keywords/other-programming-keywords.md#pragma), [The version Pragma](/igorpro/programming/programming.md#the-version-pragma), [IgorInfo](/igorpro/commands/igorinfo.md)

<!-- IgorOperator -->
## // {#}

The // characters end the executable part of a command line and start a comment. The comment continues only to the end of the line.

<!-- IgorOperator -->
## $ {#}

The $ character is used to convert a string containing a name into a reference to the named object. See [Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using) and [Using $ in Macros](/igorpro/programming/macros.md#using-in-macros) for details.