---
description: "The following keywords and templates are used in Igor to control the sequential flow of execution in procedures."
slug: /programming/keywords/flow-control
---

The following keywords and templates are used in Igor to control the sequential flow of execution in procedures.

<div className="command-signature">

## <strong>AbortOnRTE</strong> {#abortonrte}

</div>

The AbortOnRTE flow control keyword raises an abort when a runtime error has occurred in a user-defined function.

You can place AbortOnRTE immediately after a command that might give rise to a runtime error that you want to handle instead of allowing Igor to handle it by halting procedure execution. Use a [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) block to catch the abort, if it occurs.

AbortOnRTE has very low overhead and should not significantly slow program execution.

### *Details* {#details}
In terms of programming style, you should consider using AbortOnRTE (preceded by a semicolon) on the same line as the command that may give rise to an abort condition.

When using AbortOnRTE after a related sequence of commands, then it should be placed on its own line.

When used with try-catch-endtry, you should place a call to [GetRTError](/igorpro/commands/getrterror.md)(1) in your catch section to clear the runtime error.

### *Example* {#example}
Abort if the wave does not exist:


```igor
WAVE someWave; AbortOnRTE
```

### *See Also* {#see-also}
[Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts) and [AbortOnRTE Keyword](/igorpro/programming/programming.md#abortonrte-keyword) for further details.

The [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) flow control statement.

<div className="command-signature">

## <strong>AbortOnValue</strong>  <em>abortCondition</em>, <em>abortCode</em> {#abortonvalue}

</div>

The AbortOnValue flow control keyword will abort function execution when the *abortCondition* is nonzero and it will return the numeric *abortCode*. No dialog will be displayed when such an abort occurs.

### *Parameters* {#parameters}
*abortCondition* can be any valid numeric expression using comparison or logical operators.

*abortCode* is a nonzero numeric value returned to any abort or error handling code by AbortOnValue whenever it causes an abort.

### *Details* {#abortonvalue-details}
Unlike AbortOnRTE, there is no need to call GetRTError(1) in the catch section of a try-catch-endtry to clear a runtime error, since AbortOnValue does not cause a runtime error.

### *See Also* {#abortonvalue-see-also}
[Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts) and [AbortOnValue Keyword](/igorpro/programming/programming.md#abortonvalue-keyword) for further details.

The [AbortOnRTE](/igorpro/programming/keywords/flow-control.md#abortonrte) keyword and the [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) flow control statement.

<div className="command-signature">

## <strong>break</strong> {#break}

</div>

The break flow control keyword immediately terminates execution of a loop, switch or strswitch. Execution then continues with code following the loop, switch or strswitch.

### *See Also* {#break-see-also}
[Break Statement](/igorpro/programming/programming.md#break-statement), [Loops](/igorpro/programming/programming.md#loops), [Switch Statements](/igorpro/programming/programming.md#switch-statements)

<div className="command-signature">

## <strong>catch</strong> {#catch}

</div>

The catch flow control keyword marks the beginning of code in a try-catch-endtry flow control construct for handling any abort conditions.

### *See Also* {#catch-see-also}
The [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) flow control statement for details.

<div className="command-signature">

## <strong>continue</strong> {#continue}

</div>

The continue keyword returns execution to the beginning of a loop, bypassing the remainder of the loop's code.

### *See Also* {#continue-see-also}
[Continue Statement](/igorpro/programming/programming.md#continue-statement), [Loops](/igorpro/programming/programming.md#loops)

<div className="command-signature">

## <strong>default</strong> {#default}

</div>

The default keyword is used in switch and strswitch statements. When none of the case labels in the switch or strswitch match the evaluation expression, execution will continue with the code following the default label, if it is present.

### *See Also* {#default-see-also}
[Switch Statements](/igorpro/programming/programming.md#switch-statements)

<div className="command-signature">

## <strong>do-while</strong> {#do-while}

</div>

```igor
do
    <body>              // execute the loop body
while (<expression>)    // as long as expression is TRUE
```

### *See Also* {#do-while-see-also}
[Loops](/igorpro/programming/programming.md#loops), [break](/igorpro/programming/keywords/flow-control.md#break)

<div className="command-signature">

## <strong>endtry</strong> {#endtry}

</div>

The endtry flow control keyword marks the end of a try-catch-endtry flow control construct.

### *See Also* {#endtry-see-also}
The [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) flow control statement for details.

<div className="command-signature">

## <strong>for-endfor</strong> {#for-endfor}

</div>

```igor
for(<initialization>; <continuation test>; <update>)
	<loop body>
endfor
```

A for-endfor loop executes the loop body code until the continuation test evaluates as false (zero) or until a break statement is executed in the body code. When the loop starts, the initialization expressions are evaluated once. For each iteration, the continuation test is evaluated at the beginning and the update expressions are evaluated at the end.

### *See Also* {#for-endfor-see-also}
[For Loop](/igorpro/programming/programming.md#for-loop), [Range-based For-Loop](/igorpro/programming/programming.md#range-based-for-loop), [break](/igorpro/programming/keywords/flow-control.md#break)

<div className="command-signature">

## <strong>for-var-in-wave</strong> {#for-var-in-wave}

</div>

```igor
for(<type> varName : <wave>)	// Range-based for loop added in Igor Pro 9.00
	<loop body>
endfor
```

A range-based for loop iterates over each element of a wave. The specified loop variable contains the value of the current wave element.

### *See Also* {#for-var-in-wave-see-also}
[Range-based For-Loop](/igorpro/programming/programming.md#range-based-for-loop), [For Loop](/igorpro/programming/programming.md#for-loop), [break](/igorpro/programming/keywords/flow-control.md#break)

## if-else-endif {#if-else-endif}


```igor
if (<expression>)
	<TRUE part>			// Execute if condition is TRUE
else
	<FALSE part>			// Execute if condition is FALSE
endif
```

### *See Also* {#if-else-endif-see-also}
[Conditional Statements In Functions](/igorpro/programming/programming.md#conditional-statements-in-functions)

<div className="command-signature">

## <strong>if-elseif-endif</strong> {#if-elseif-endif}

</div>

```igor
if (<expression1>)
	<TRUE part 1>		// Execute if condition 1 is TRUE
elseif (<expression2>)
	<TRUE part 2>		// Execute if condition 2 is TRUE and condition 1 is FALSE
[...]
[else
	<FALSE part>]		// Optionally execute if all conditions are FALSE
endif
```

### *See Also* {#if-elseif-endif-see-also}
[Conditional Statements In Functions](/igorpro/programming/programming.md#conditional-statements-in-functions)

<div className="command-signature">

## <strong>if-endif</strong> {#if-endif}

</div>

```igor
if (<expression>)
	<TRUE part>         // Execute if condition is TRUE
[else
	<FALSE part>]       // Optionally execute if condition is FALSE
endif
```

### *See Also* {#if-endif-see-also}
[Conditional Statements In Functions](/igorpro/programming/programming.md#conditional-statements-in-functions)

<div className="command-signature">

## <strong>return</strong>  [<em>expression</em>] {#return}

</div>

The return flow control keyword immediately stops execution of the current procedure. If called by another procedure, it returns *expression* and control to the calling procedure.

Functions can return only a single value directly to the calling procedure with a return statement. The return value must be compatible with the function type. Two values can be returned using a complex variable's real and imaginary parts. A function may contain any number of return statements; only the first one encountered during procedure execution is evaluated.

A macro has no return value, so return simply quits the macro.

### *See Also* {#return-see-also}
[The Return Statement](/igorpro/programming/programming.md#the-return-statement)

<div className="command-signature">

## <strong>strswitch-case-endswitch</strong> {#strswitch-case-endswitch}

</div>

```igor
strswitch(<string expression>)  // string switch
	case <literal><constant>:    // execute if case matches expression
		<code>
		[break] // exit from switch
	case <literal><constant>:    // execute if case matches expression
		<code>
		[break]
	[default:                    // optional default expression executed
		<code>] // when no case matches
endswitch
```

A strswitch-case-endswitch statement evaluates a string expression and compares the result to the case labels using a case-insensitive comparison. If a case label matches string expression, then execution proceeds with code following the matching case label. When none of the cases match, execution will continue at the default label, if it is present, or otherwise the strswitch will be exited with no action taken. Note that although the break statement is optional, in almost all case statements it will be required for the strswitch to work correctly.

### *See Also* {#strswitch-case-endswitch-see-also}
[Switch Statements](/igorpro/programming/programming.md#switch-statements), [break](/igorpro/programming/keywords/flow-control.md#break), [default](/igorpro/programming/keywords/flow-control.md#default)

<div className="command-signature">

## <strong>switch-case-endswitch</strong> {#switch-case-endswitch}

</div>

```igor
switch(<numerical expression>)  // numeric switch
	case <literal><constant>:    // execute if case matches expression
		<code>
		[break]     // exit from switch
	case <literal><constant>:    // execute if case matches expression
		<code>
		[break]
	[default:                    // optional default expression executed
		<code>]     // when no case matches
endswitch
```

A switch-case-endswitch statement evaluates the numeric expression and rounds the result to the nearest integer. If a case label matches the numerical expression, then execution proceeds with code following the matching case label. When no cases match, execution continues at the default label, if present, or otherwise the switch exits with no action taken. Although the break statement is optional, in almost all case statements it is required for the switch to work correctly.

Literal numbers used as case labels are required by the compiler to be integers. Numeric constants used as case labels are rounded by the compiler to the nearest integers.

### *See Also* {#switch-case-endswitch-see-also}
[Switch Statements](/igorpro/programming/programming.md#switch-statements), [break](/igorpro/programming/keywords/flow-control.md#break), [default](/igorpro/programming/keywords/flow-control.md#default)

<div className="command-signature">

## <strong>try</strong> {#try}

</div>

The try flow control keyword marks the beginning of the initial code block in a try-catch-endtry flow control construct.

### *See Also* {#try-see-also}
The [try-catch-endtry](/igorpro/programming/keywords/flow-control.md#try-catch-endtry) flow control statement for details.

<div className="command-signature">

## <strong>try-catch-endtry</strong> {#try-catch-endtry}

</div>

```igor
try
	<code>
catch
	<code to handle abort>
endtry
```

A try-catch-endtry flow control statement provides a means for catching and responding to abort conditions in user functions. A programmatic abort is generated when the code executes Abort, AbortOnRTE or AbortOnValue. A user abort is generated when the user clicks the Abort button or presses the user abort key combination.

When code executes in the try-catch area, a programmatic abort immediately jumps to the code in the catch-endtry area rather than jumping to the end of the user function. A user abort jumps to the catch-endtry area when a flow control keyword such as for or while executes or at the end of the try code. Normal flow (no aborts) skips all code within the catch-endtry area.

### *Details* {#try-catch-endtry-details}
During execution of code in the catch-endtry area, user aborts are suppressed. This means that, if the user attempts to abort procedure execution by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations) or by clicking the Abort button, this will not abort the catch code itself.

When an abort occurs, information about the source of the abort is returned via the V_AbortCode variable as follows:

|  |  |
| --- | --- |
| -4: | Abort triggered by AbortOnRTE |
| -3: | Abort caused by Abort operation |
| -2: | Stack overflow abort |
| -1: | User abort |
| *abortCode*: | Abort triggered by AbortOnValue. |

### *See Also* {#try-catch-endtry-see-also}
[Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts) and [try-catch-endtry Flow Control](/igorpro/programming/programming.md#try-catch-endtry-flow-control) for further details.

[AbortOnRTE](/igorpro/programming/keywords/flow-control.md#abortonrte), [AbortOnValue](/igorpro/programming/keywords/flow-control.md#abortonvalue), [Abort](/igorpro/commands/abort.md)