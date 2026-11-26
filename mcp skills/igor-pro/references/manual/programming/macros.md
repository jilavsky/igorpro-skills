---
description: "When we first created Igor, some time in the last millenium, it supported automation through macros."
slug: /programming/macros
---

# Macros {#macros}

When we first created Igor, some time in the last millenium, it supported automation through macros. The idea of the macro was to allow users to collect commands into conveniently callable routines. Igor interpreted and executed each command in a macro as if it were entered in the command line.

WaveMetrics soon realized the need for a faster, more robust technology that would support full-blown programming. This led to the addition of user-defined functions. Because functions are compiled, they execute much more quickly. Also, compilation allows Igor to catch syntactic errors sooner. Functions have a richer set of flow control capabilities and support many other programming refinements.

Over time, the role of macros has diminished in favor of functions. With rare exceptions, new programming should be done using user-defined functions.

Macros are still supported and there are still a few uses in which they are preferred. When you close a graph, table, page layout, Gizmo plot, or control panel, Igor offers to automatically create a window recreation macro which you can later run to recreate the window. You can also ask Igor to automatically create a window style macro using the Window Control dialog. The vast majority of programming, however, should be done using functions.

The syntax and behavior of macros are similar to the syntax and behavior of functions, but the differences can be a source of confusion for someone first learning Igor programming. If you are just starting, you can safely defer reading the rest of this help file until you need to know more about macros, if that time ever comes.

## Comparing Macros And Functions {#comparing-macros-and-functions}

Like functions, macros are created by entering text in procedure windows. Each macro has a name, a parameter list, parameter declarations, and a body. Unlike functions, a macro has no return value.

Macros and functions use similar syntax. Here is an example of each. To follow along, open the Procedure window (Windows menu) and paste in the macro and function definitions.


```igor
Macro MacSayHello(name)
	String name

	Print "Hello "+name
End

Function FuncSayHello(name)
	String name

	Print "Hello "+name
End
```

Now click on the command window to bring it to the front.

If you execute the following on the command line


```igor
MacSayHello("John"); FuncSayHello("Sue")
```

you will see the following output printed in the history area:


```igor
Hello John
Hello Sue
```

This example may lead you to believe that macros and functions are nearly identical. In fact, there are a lot of differences, as detailed below. The most important differences are:


-	Macros automatically appear in the Macros menu. Functions must be explicitly added to a menu, if desired, using a menu definition.


-	Most errors in functions are detected when procedures are compiled. Most errors in macros are detected when the macro is executed.


-	Functions run a lot faster than macros.


-	Functions support wave parameters, for loops, switches, structures, multithreading, and many other features not available in macros.


-	Functions have a richer syntax.

If you look in the Macros menu, you will see MacSayHello but not FuncSayHello.

If you execute FuncSayHello() on the command line you will see an error dialog. This is because you must supply a parameter. You can execute, for example:


```igor
FuncSayHello("Sam")
```

On the other hand, if you run MacSayHello from the Macros menu or if you execute MacSayHello() on the command line, you will see a dialog where you enter the name before continuing.

<img src="MD_images/Macros/image_0.png" width="75%"/>

This is called [The Missing Parameter Dialog](#the-missing-parameter-dialog). Functions can display a similar dialog, called [The Simple Input Dialog](/igorpro/programming/interacting-with-the-user.md#the-simple-input-dialog), with a bit of additional programming.

Now try this: In both procedures, change "Print" to "xPrint". Then click on the command window. You will see an error dialog complaining about the xPrint in the function.

<img src="MD_images/Macros/image_1.png" width="75%"/>

Click the Edit Procedure button and change "xPrint" back to "Print" in the function but not in the macro. Then click in the command window.

Notice that no error was reported once you fixed the error in the function. This is because only functions are compiled and thus only functions have their syntax completely checked at compile time. Macros are interpreted and most errors are found only when the line in the procedure window in which they occur is executed.

To see this, run the macro by executing "MacSayHello("Sam")" on the command line. Igor displays an error dialog:

<img src="MD_images/Macros/image_2.png" width="75%"/>

Notice the outline around the line containing the error. This outline means you can edit the erroneous command. If you change "xPrint" to "Print" in this dialog, the Retry button becomes enabled. If you click Retry, Igor continues execution of the macro. When the macro finishes, take a look at the Procedure window. You will notice that the correction you made in the dialog was put in the procedure window and your "broken" macro is now fixed.



## Macro Syntax {#macro-syntax}

Here is the basic syntax for macros.


```igor
<Defining keyword> <Name> ( <Input parameter list> ) [:<Subtype>]
	<Input parameter declarations>

	<Local variable declarations>

	<Body code>
End
```

### The Defining Keyword {#the-defining-keyword}

\<Defining keyword\> is one of the following:


| Defining Keyword | Creates Macro In |
| --- | --- |
| Window | Windows menu |
| Macro | Macros menu |
| Proc | -- |

The Window keyword is used by Igor when it automatically creates a window recreation macro. Except in rare cases, you will not write window recreation macros but instead will let Igor create them automatically.

### The Procedure Name {#the-procedure-name}

The names of macros must follow the standard Igor naming conventions. Names can consist of up to 255 characters. Only ASCII characters are allowed. The first character must be alphabetic while the remaining characters can include alphabetic and numeric characters and the underscore character. Names must not conflict with the names of other Igor objects, functions or operations. Names in Igor are case insensitive.

Prior to Igor Pro 8.00, macro names were limited to 31 bytes. If you use long macro names, your procedures will require Igor Pro 8.00 or later.

### The Procedure Subtype {#the-procedure-subtype}

You can identify procedures designed for specific purposes by using a subtype. Here is an example:


```igor
Proc ButtonProc(ctrlName) : ButtonControl
	String ctrlName

	Beep
End
```

Here, " : ButtonControl" tells Igor that this function is intended to be called when a user-defined button control is clicked. Because of the subtype, Igor will include this macro in the list of procedures that appears in the Button Control dialog which you used to create buttons. When Igor automatically generates a procedure it generates the appropriate subtype. See [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes) for details.

### The Parameter List and Parameter Declarations {#the-parameter-list-and-parameter-declarations}

The parameter list specifies the name for each input parameter. Macros have a limit of 10 parameters.

The parameter declaration must declare the type of each parameter using the keywords Variable or String. If a parameter is a complex number, it must be declared Variable/C.

:::note
There should be no blank lines or other commands until after all the input parameters are defined. There should be one blank line after the parameter declarations, before the rest of the procedure. Igor will report errors if these conditions are not met.
:::

Variable and string parameters in macros are always passed to a subroutine by value.

When macros are invoked with some or all of their input parameters missing, Igor displays a missing parameter dialog to allow the user to enter those parameters. In the past this has been a reason to use macros. However, as of Igor Pro 4, functions can present a similar dialog to fetch input from the user, as explained under [The Simple Input Dialog](/igorpro/programming/interacting-with-the-user.md#the-simple-input-dialog).

### Local Variable Declarations {#local-variable-declarations}

The input parameter declarations are followed by the local variable declarations if the macro uses local variables. Local variables exist only during the execution of the macro. They can be numeric or string and are declared using the Variable or String keywords. They can optionally be initialized. Here is an example:


```igor
Macro Example(p1)
	Variable p1

	Variable v1, v2						// Here are the local variables
	Variable v3=0
	Variable/C cv1=cmplx(0,0)
	String s1="test", s2="test2"

	<Body code>
End
```

If you do not supply explicit initialization, Igor automatically initializes local numeric variables with the value zero and local string variables with the value "".

The name of a local variable is allowed to conflict with other names in Igor although they must be unique within the macro. Clearly if you create a local variable named "sin" then you will be unable to use Igor's built-in sin function within the macro.

You can declare a local variable in any part of a macro with one exception. If you place a variable declaration inside a loop in a macro then the declaration will be executed multiple times and Igor will generate an error since local variable names must be unique.

### Macro Body Code {#macro-body-code}

The local variable declarations are followed by the body code. This table shows what can appear in body code of a macro.


| What | Allowed in Macros? | Comment |
| --- | --- | --- |
| Assignment statements | Yes | Includes wave, variable and string assignments. |
| Built-in operations | Yes |  |
| External operations | Yes |  |
| External functions | Yes |  |
| Calls to user functions | Yes |  |
| Calls to macros | Yes |  |
| if-else-endif | Yes |  |
| if-elseif-endif | No |  |
| switch-case-endswitch | No |  |
| strswitch-case-endswitch | No |  |
| try-catch-endtry | No |  |
| Structures | No |  |
| do-while | Yes |  |
| for-endfor | No |  |
| Comments | Yes | Comments start with //. |
| break | Yes | Used in loop statements. |
| continue | No |  |
| default | No |  |
| return | Yes, but with no return value. |  |



## Conditional Statements In Macros {#conditional-statements-in-macros}

The conditional if-else-endif statement is allowed in macros. It works the same as in functions. See [If-Else-Endif Statements](/igorpro/programming/programming.md#if-else-endif-statements).



## Loops In Macros {#loops-in-macros}

The do-while loop is supported in macros. It works the same as in functions. See [Do-While Loop](/igorpro/programming/programming.md#do-while-loop).



## Return Statement In Macros {#return-statement-in-macros}

The return keyword immediately stops execution of the current macro. If it was called by another macro, control returns to the calling macro.

A macro has no return value so return is used just to prematurely quit the macro. Most macros will have no return statement.



## Invoking Macros {#invoking-macros}

There are several ways to invoke a macro:


-	From the command line


-	From the Macros, Windows or user-defined menus


-	From another macro


-	From a button or other user control

The menu in which a macro appears, if any, is determined by the macro's type and subtype.

This table shows how a macro's type determines the menu that Igor puts it in.


| Macro Type | Defining Keyword | Menu |
| --- | --- | --- |
| Macro | Macro | Macros menu |
| Window Macro | Window | Windows menu |
| Proc | Proc | -- |

If a macro has a subtype, it may appear in a different menu. This is described under [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes). You can put macros in other menus as described under [User-Defined Menus](/igorpro/user-interface/user-defined-menus.md).

You cannot directly invoke a macro from a user function. You can invoke it indirectly, using the [Execute](/igorpro/commands/execute.md) operation.



## Using $ In Macros {#using-in-macros}

As shown in the following example, the $ operator can create references to global numeric and string variables as well as to waves.


```igor
Macro MacroTest(vStr, sStr, wStr)
	String vStr, sStr, wStr

	$vStr += 1
	$sStr += "Hello"
	$wStr += 1
End

Variable/G gVar = 0; String/G gStr = ""; Make/O/N=5 gWave = p
MacroTest("gVar", "gStr", "gWave")
```

See [String Substitution Using $](/igorpro/programming/commands.md#string-substitution-using) for additional examples using $.



## Waves as Parameters In Macros {#waves-as-parameters-in-macros}

The only way to pass a wave to a macro is to pass the name of the wave in a string parameter. You then use the $ operator to convert the string into a wave reference. For example:


```igor
Macro PrintWaveStdDev(w)
	String w

	WaveStats/Q $w
	Print V_sdev
End

Make/O/N=100 test=gnoise(1)
Print NamedWaveStdDev("test")
```



## The Missing Parameter Dialog {#the-missing-parameter-dialog}

When a macro that is declared to take a set of input parameters is executed with some or all of the parameters missing, it displays a dialog in which the user can enter the missing values. For example:


```igor
Macro MacCalcDiag(x,y)
	Variable x=10
	Prompt x, "Enter X component: "		// Set prompt for X param
	Variable y=20
	Prompt y, "Enter Y component: "		// Set prompt for X param
	
	Print "diagonal=",sqrt(x^2+y^2)
End
```

If invoked from the command line or from another macro with parameters missing, like this:


```igor
MacCalcDiag()
```

Igor displays the Missing Parameter dialog in which the parameter values can be specified.

The Prompt statements are optional. If they are omitted, the variable name is used as the prompt text.

There must be a blank line after the set of input parameter and prompt declarations and there must not be any blank lines within the set.

The missing parameter dialog supports the creation of pop-up menus as described under [Pop-Up Menus In Simple Dialogs](/igorpro/programming/interacting-with-the-user.md#pop-up-menus-in-simple-dialogs). One difference is that in a missing parameter dialog, the menu item list can be continued using as many lines as you need. For example:


```igor
Prompt color, "Select Color", popup "red;green;blue;"
"yellow;purple"
```



## Macro Errors {#macro-errors}

Igor can find errors in macros at two times:


-	When it scans the macros


-	When it executes the macros

Scanning occurs, after you modify procedure text, when you activate a non-procedure window, click the Compile button or select Compile from the Macros menu. At this point, Igor is just looking for the names of procedures. The only errors that it detects are name conflicts and ill-formed names. If it finds such an error, it displays a dialog you use to fix it.

Igor detects other errors when the macro executes. Execution errors may be recoverable or non-recoverable. If a recoverable error occurs, Igor puts up a dialog in which you can edit the erroneous line.

If the error is non-recoverable, you get a similar dialog except that you can't fix the error and retry. This happens with errors in the parameter declarations and errors related to if-else-endif and do-while structures.



## The Silent Option {#the-silent-option}

Normally Igor displays each line of a macro in the command line as it executes the line. This gives you some idea of what is going on. However it also slows macro execution down considerably. You can prevent Igor from showing macro lines as they are executed by using the Silent 1 command.

You can use Silent 1 from the command line. It is more common to use it from within a macro. The effect of the Silent command ends at the end of the macro in which it occurs. Many macros contain the following line:


```igor
Silent 1; PauseUpdate
```



## The Slow Option {#the-slow-option}

You can observe the lines in a macro as they execute in the command line. However, for debugging purposes, they often whiz by too quickly. The Slow operation slows the lines down. It takes a parameter which controls how much the lines are slowed down. Typically, you would execute something like "Slow 10" from the command line and then "Slow 0" when you are finished debugging.

You can also use the Slow operation from within a macro. You must explicitly invoke "Slow 0" to revert to normal behavior. It does not automatically revert at the end of the macro from which it was invoked.

We never use this feature. Instead, we generally use print statements for debugging or we use the Igor symbolic debugger. See [Debugging](/igorpro/programming/debugging.md).



## Accessing Variables Used by Igor Operations {#accessing-variables-used-by-igor-operations}

A number of Igor's operations return results via variables. For example, the [WaveStats](/igorpro/commands/wavestats.md) operation creates many variables with names such as V_avg, V_sigma, etc.

When you invoke these operations from the command line, they create global variables in the current data folder.

When you invoke them from a user-defined function, they create local variables.

When you invoke them from a macro, they create local variables unless a global variable already exists. If both a global variable and a local variable exist, Igor uses the local variable.

In addition to creating variables, a few operations, such as [CurveFit](/igorpro/commands/curvefit.md) and [FuncFit](/igorpro/commands/funcfit.md), check for the existence of specific variables in order to provide optional behavior. The operations look first for a local variable with a specific name. If the local variable is not found, they then look for a global variable.



## Updates During Macro Execution {#updates-during-macro-execution}

An update is an action that Igor performs. It consists of:


-	Reexecuting assignments for dependent objects whose antecedents have changed


-	Redrawing graphs and tables which display waves that have changed


-	Redrawing page layouts containing graphs, tables, or annotations that have changed


-	Redrawing windows that have been uncovered

When no procedure is executing, Igor continually checks whether an update is needed and does an update if necessary.

During macro execution, Igor checks if an update is needed after executing each line. You can tell Igor to suspend checking using the [PauseUpdate](/igorpro/commands/pauseupdate.md) operation. This is useful when you want an update to occur when a macro finishes but not during the course of the macro's execution.

PauseUpdate has effect only inside a macro. Here is how it is used.


```igor
Window Graph0() : Graph
	PauseUpdate; Silent 1
	Display /W=(5,42,400,250) w0,w1,w2
	ModifyGraph gFont="Helvetica"
	ModifyGraph rgb(w0)=(0,0,0),rgb(w1)=(0,65535,0),rgb(w2)=(0,0,0)
	<more modifies here...>
End
```

Without the PauseUpdate, Igor would do an update after each modify operation. This would take a long time.

At the end of the macro, Igor automatically reverts the state of update-checking to what it was when this macro was invoked. You can use the [ResumeUpdate](/igorpro/commands/resumeupdate.md) operation if you want to resume updates before the macro ends or you can call [DoUpdate](/igorpro/commands/doupdate.md) to force an update to occur at a particular point in the program flow. Such explicit updating is rarely needed.



## Aborting Macros {#aborting-macros}

There are two ways to prematurely stop macro execution: a user abort or a programmed abort. Both stop execution of all macros, no matter how deeply nested.

You can abort macro execution by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations) or by clicking the Abort button in the status bar. You may need to press the keys down for a while because Igor looks at the keyboard periodically and if you don't press the keys long enough, Igor will not see them.

A user abort does not directly return. Instead it sets a flag that tells Igor to stop loops from looping and then returns using the normal calling chain. For this reason some code will still be executed after an abort but execution should stop quickly. This behavior allows Igor to release any temporary memory allocations it may have made during execution.

A **programmed abort** occurs when the [Abort](/igorpro/commands/abort.md) operation is executed. Here is an example:


```igor
if (numCells > 10)
	Abort "Too many cells! Quitting."
endif
// code here doesn't execute if numCells > 10
```



## Converting Macros To Functions {#converting-macros-to-functions}

If you have old Igor procedures written as macros, as you have occasion to revisit them, you can consider converting them to functions. In most cases, this is a good idea. An exception is if the macros are so complex that there would be a substantial risk of introducing bugs. In this case, it is better to leave things as they are.

If you decide to do the conversion, here is a checklist that you can use in the process.


1.	Back up the old version of the procedures.
2.	Change the defining keyword from Macro or Proc to Function.
3.	If the macro contained [Prompt](/igorpro/programming/keywords/other-programming-keywords.md#prompt) statements, then it was used to generate a missing parameter dialog. Change it to generate a simple input dialog as follows:

	- Remove the parameters from the parameter list. The old parameter declarations now become local variable declarations.

	- Make sure that the local variable for each prompt statement is initialized to some value.

	- Add a [DoPrompt](/igorpro/programming/keywords/other-programming-keywords.md#doprompt) statement after all of the [Prompt](/igorpro/programming/keywords/other-programming-keywords.md#prompt) statements.

	- Add a test on V_Flag after the DoPrompt statement to see if the user cancelled.
4.	Look for statements that access global variables or strings and create NVAR and SVAR references for them.
5.	Look for any waves used in assignment statements and create WAVE references for them.
6.	Compile procedures. If you get an error, fix it and repeat step 6.